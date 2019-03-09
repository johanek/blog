---
layout: post
title: "Testing puppet manifests with toft-puppet"
date: 2012-03-30 16:53
comments: true
tags: [puppet, configuration management, cucumber, lxc, tdd]
---

Toft is a ruby gem to manage testing of configuration management manifests with LXC Linux containers – it can manage nodes, run chef or puppet, run ssh commands and then run any testing framework against those nodes – such as rspec or cucumber.

Using containers for this purpose is incredibly useful as they can be created and destroyed very quickly, even compared to a virtual machine. So we can setup a fresh node with a base OS, run our manifests on that, and then run tests on the system we have created. Since we run the tests from the system that hosts the container, we can run tests both from within and outside the node easily.

I’m using toft from jenkins to run cucumber tests on our manifests. Anytime anyone checks into testing, all my cucumber tests (as well as other things like puppet-lint) are run and when they succeed, we merge into master.

Testing the behaviour of your deployed manifests as part of an automated QA – this is a massive result, and toft makes it just that much easier.

## Installation ##

The QA system will need the following packages:

    libvirt
    lxc

Unfortunately there is no lxc package in EPEL, so I needed to take the source RPM from Fedora 16 and build it on Scientific Linux. This was a hassle free process.

The following gems are required:

    toft-puppet
    cucumber
    rspec
 
These are most easily installed with gem install if you have access to rubygems.org or an internal repository.

## Configuration ##

For libvirtd, disable multicast DNS. Also change host bridge network interface to br0 and set the bridge network as 192.168.20.0:
 
{% highlight bash filename="/etc/libvirt/libvirtd.conf" %}
mdns_adv = 0
{% endhighlight %}


{% highlight xml filename="/etc/libvirt/qemu/networks/default.xml" %}
<network>
<name>default</name>
<uuid>3b673ba9-be12-4299-95a3-2059be18f7b9</uuid>
<bridge name=”br0″ />
<mac address=’52:54:00:BE:D0:1D’/>
<forward/>
<ip address=”192.168.20.1″ netmask=”255.255.255.0″>
<dhcp>
<range start=”192.168.20.2″ end=”192.168.20.254″ />
</dhcp>
</ip>
</network>
{% endhighlight %}

Now we can start the libvirt service with

    service libvirtd start

LXC requires cgroup support, so the cgroup filesystem needs mounting. Add the following to /etc/fstab

{% highlight bash filename="/etc/fstab" %}
none    /cgroup cgroup  defaults        0       0
{% endhighlight %}
 
Then create the directory /cgroup and mount it

    mkdir /cgroup
    mount /cgroup 

Our templates and support files need to be put in place, and directories created. Toft supplies templates for natty, lucid and centos-6. I use Scientific Linux, so I needed to create my own template from the centos-6 template – you can find it here: <https://github.com/johanek/toft/blob/master/scripts/lxc-templates/lxc-scientific-6>

    mkdir -p /usr/lib64/templates/files
    cp lxc-scientific-6 /usr/lib64/lxc/templates/
    chmod 0755 /usr/lib64/lxc/templates/lxc-scientific-6
    cp /usr/lib/ruby/gems/1.8/gems/toft-puppet-0.0.11/scripts/lxc-templates
    /files/rc.local /usr/lib64/lxc/templates/files/
 
## Base Image ##

Now we need to get a base image to run. You can grab one from the OpenVZ project, as the images are compatible. <http://wiki.openvz.org/Download/template/precreated>

Since the image is just a bunch of files on disk, you can extract that tarball and chroot into the resulting directory structure to modify the image to your needs. Once you’re happy, tar.gz the directory tree and copy that file to:

    /var/cache/lxc/scientific-6-x86_64.tar.gz
 
## Test LXC ##

To test lxc is working, create a quick node config file:

{% highlight bash filename="/tmp/n1.conf" %}
lxc.network.type = veth
lxc.network.flags = up
lxc.network.link = br0
lxc.network.name = eth0
lxc.network.ipv4 = 192.168.20.2/24
{% endhighlight %}

Then, create a node by running:

    lxc-create -n n1 -f /tmp/n1.conf -t scientific-6
 
This should extract the image and configure it ready to be started. When you start the image, a a tty on the guest machine will take over your terminal, so it’s best to run the following in a screen session:

    lxc-start -n n1
 
Once that’s booted you should be able to login via your terminal, and ssh to the machine on the IP we configured above. Once that’s working well, we can stop and destroy the guest with the following:

    lxc-stop -n n1
    lxc-destroy -n n1
 
## Running Tests ##

The toft module comes with a lot of example cucumber tests, step definitions and puppet configs to start you off. They’re worth reading through to understand what can be done – I need to modify them for my own needs, so let’s make a copy of the examples as a baseline:

    mkdir /root/cucumber/
    cd /root/cucumber
    rsync -av /usr/lib/ruby/gems/1.8/gems/toft-puppet-0.0.11/features .
    rsync -av /usr/lib/ruby/gems/1.8/gems/toft-puppet-0.0.11/fixtures .
 
The supplied puppet.conf file has lots of localisations specific to the developers setup, so I created a very simple one designed just to specify the path to our puppet modules

{% highlight bash filename="fixtures/puppet/conf/puppet.conf" %}
[main]
# The Puppet log directory.
# The default value is ‘$vardir/log’.
logdir = /var/log/puppet
 
# Where Puppet PID files are kept.
# The default value is ‘$vardir/run’.
rundir = /var/run/puppet
 
# Where SSL certificates are kept.
# The default value is ‘$confdir/ssl’.
ssldir = $vardir/ssl
 
modulepath = /tmp/toft-puppet-tmp/modules/
 
[agent]
# The file in which puppetd stores a list of the classes
# associated with the retrieved configuratiion. Can be loaded in
# the separate “puppet“ executable using the “–loadclasses“
# option.
# The default value is ‘$confdir/classes.txt’.
classfile = $vardir/classes.txt
 
# Where puppetd caches the local configuration. An
# extension indicating the cache format is added automatically.
# The default value is ‘$confdir/localconfig’.
localconfig = $vardir/localconfig
{% endhighlight %}

At this point I also removed the chef examples, to avoid any errors related to software I’m not using

    rm -rf fixtures/chef

Now we need to copy our own modules to fixtures/puppet/modules/

Toft uses a routine located in the rc.local file we copied earlier to update DNS with the hostname of the new node. It does this via nsupdate. Since I’m only ever going to create one node with a known IP, and access it from the one machine we’re running the tests from, I can just add the hostname to /etc/hosts:

    192.168.20.2    n1    n1.foo
 
Now we’re ready to write tests – again there are a lot of examples of cucumber tests in the features directory. I removed them all, apart from puppet.features, which I pared down and added my own tests:

{% highlight bash filename="features/puppet.feature" %}
 
Feature: Puppet support
 
Scenario: Run Puppet manifest on nodes
Given I have a clean running node n1
When I run puppet manifest “manifests/test.pp” on node “n1″
Then Node “n1″ should have file or directory “/tmp/puppet_test”
 
Scenario: Apache module
Given I have a clean running node n1
When I run puppet manifest “manifests/apache.pp” with config file “puppet.conf” on node “n1″
Then Node “n1″ should have package “httpd” installed in the centos box
And Node “n1″ should have service “httpd” running in the centos box
{% endhighlight %}

Note the references to the “centos box” – that’s just the way the step definitions have been written in the toft module and can be modified easily. My Apache module test has an associated manifest:

{% highlight bash filename="fixtures/puppet/manifests/apache.pp" %}
 
include apache
{% endhighlight %} 

Now we can run our tests:

    cd features
    cucumber puppet.feature
 
Which gives a result like:

    Creating Scientific Linux 6 node…
    Checking image cache in /var/cache/lxc/rootfs-x86_64 …
    Extracting rootfs image to /var/lib/lxc/n1/rootfs …
    Set root password to ‘root’
    ‘scientific-6′ template installed
    ‘n1′ created
    Feature: Puppet support
    Scenario: Run Puppet manifest on nodes # puppet.feature:3
    Starting host node…
    Waiting for host ssdh ready………….
    Waiting for host to be reachable.
    SSH connection on ‘n1/192.168.20.2′ is ready.
    Given I have a clean running node n1 # step_definitions/node.rb:1
    notice: /Stage[main]/Test/File[/tmp/puppet_test]/ensure: created
    notice: Finished catalog run in 0.04 seconds
    When I run puppet manifest “manifests/test.pp” on node “n1″ # step_definitions/puppet.rb:1
    Then Node “n1″ should have file or directory “/tmp/puppet_test” # step_definitions/checker.rb:5
 
    Scenario: Apache module # puppet.feature:8
    Starting host node…
    Waiting for host ssdh ready.
    Waiting for host to be reachable.
    SSH connection on ‘n1/192.168.20.2′ is ready.
    Given I have a clean running node n1 # step_definitions/node.rb:1
    notice: /Stage[main]/Apache::Install/Package[httpd]/ensure: created
    notice: /Stage[main]/Apache::Service/Service[httpd]/ensure: ensure changed ‘stopped’ to ‘running’
    notice: Finished catalog run in 10.68 seconds
    When I run puppet manifest “manifests/apache.pp” with config file “puppet.conf” on node “n1″ # step_definitions/puppet.rb:5
    httpd-2.2.15-15.sl6.x86_64
    Then Node “n1″ should have package “httpd” installed in the centos box # step_definitions/centos/checks.rb:1
    9
    And Node “n1″ should have service “httpd” running in the centos box # step_definitions/centos/checks.rb:6
 
    2 scenarios (2 passed)
    7 steps (7 passed)
    0m26.193s
 

Job done – now you can write more tests and automate them with Jenkins.
