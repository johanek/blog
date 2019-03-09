---
layout: post
title: "Monitorama 2016 Portland Day 3"
date: 2016-06-29 20:00
comments: true
tags: conferences monitoring
---

## [Justin Reynolds](https://twitter.com/jrsquared), Netflix - Intuition Engineering at Netflix

[Video](https://vimeo.com/173607639) 


Discussed problems at Netflix that regions were siloed, they worked on serving users out of any region.

To fail regions, need to scale up other regions to server all traffic

Dashboards, good at looking back, but need to know now. How to provide intuition of the now?

Created vizceral - see the blog post for screenshots & video: [http://techblog.netflix.com/2015/10/flux-new-approach-to-system-intuition.html](http://techblog.netflix.com/2015/10/flux-new-approach-to-system-intuition.html)

## Brian Brazil, Robust Perceiver - Prometheus

[Slides](http://www.slideshare.net/brianbrazil/prometheus-monitorama-2016) | [Video](https://vimeo.com/173704322)

Prometheus is a TSDB offering 'whitebox monitoring' for looking inside applications. supports labels, alerting and graphing are unified, using the same language.

Pull based system, links into service discovery. HTTP api for graphing, supports persistent queries which are used for alerting.

Provides instrumentation library, incredibly simple to instrument functiions and expose metrics to prometheus. Client libraries don't tie you into prometheus - can use graphite.

Can use prometheous as a clearing house to translate between different data formats.

Doesn't use a notion of a machine. HA by duplicating servers, but alertmanager deduplicates alerts. Alertmanager can also group alerts.

Data stored as file per database on disk, not round-robin - stores all data without downsampling.

## [Torkel Ödegaard](https://twitter.com/torkelo), Raintank - Grafana Master Class

[Video](https://vimeo.com/173607651)

Gave a demo on how to use grafana, as well as recently added and future features.

## [Katherine Daniels](https://twitter.com/beerops), Etsy - How to Teach an Old Monitoring System New Tricks

[Slides](https://speakerdeck.com/kdaniels/teaching-an-old-monitoring-system-new-tricks) | [Video](https://vimeo.com/173607641)

Old Monitoring System == Nagios

Adding new servers.

- Use deployinator to deploy nagios configs. Uses chef to provide inventory to generate a currently list of hosts and hostgroups.
- Run validation via Jenkins by running *nagios -v*, as well as writing tool for nagios validation.
- New hosts are added with scheduled downtime so they don't alert until the next day. Chat bots send reminders when downtime is going to finish.

Making Alerts (Marginally) Less Annoying

- Created nagdash to provide federated view of multiple nagios instances.
- Created nagios-herald to add context to nagios alerts. Also supports allowing people to sign up to alerts for things they're interested in.

Tracking Sleep

- Ops weekly tool. Provides on call reports, engineers flag what they had to do with alerts. 
- Sleep tracking and alert tracking for on call staff to understand how many alerts they're facing and how it's impacting their sleep.

An On Call bedtime story

- Plenty of alerts because scheduled downtime expired for ongoing work. 
- Create daily reports of what downtime will soon expire and which will raise alerts.

## [Joe Damato](https://twitter.com/joedamato), packagecloud.io - All of Your Network Monitoring is (probably) Wrong

[Slides](http://blog.packagecloud.io/eng/2016/06/29/monitorama-2016-all-of-your-network-monitoring-is-probably-wrong/) | [Video](https://vimeo.com/173610178)

There's too much stuff to know about

- ever copy paste config or tune settings you didn't understand?
- do you really understand every graph you're generating?
- what makes you think you can monitor this stuff?

Claim: the more complex the system is the harder it is to monitor.

whats p. complicated? linux networking stack! lots of features, lots of bugs. with no docs!

- /proc/net stats can be buggy
- ethtool inconsistent, not always implemented
- meaning of driver stats are not standardised
- stats meaning for a dirver/device can change over time
- /proc/net/snmp has bugs: double counting, not being counted correctly

Monitoring something requires a very deep understanding of what you're monitoring.

Properly monitoring and setting alerts requires significant investment.

## [Megan Kanne](https://twitter.com/megankanne), [Justin Nguyen](https://twitter.com/justanguyen), and [Dan Sotolongo](https://twitter.com/sortalongo), Twitter - Building Twitter’s Next-Gen Alerting System

[Slides](https://docs.google.com/presentation/d/1K4e7uB0wBzrlq5EctCvWEyok0gTOz-1Sh9Ya-o6NeRw/edit) | [Video](https://vimeo.com/173607647)

3.5B metrics per minute

Old Alerting System

- 25k alerts/minute, 3m alert monitors
- single config language, lot of existing example, easy to write and add
- all those points were good and bad!
- lots of orphaned and unmaintained configs, no validation
- alerts and dashboards were seperate
- problems with reliability when zones suffer problems

Solution

- combined alerts and dashboard configuration
- dashboards defined in python, common libraries that can be included
- python allows testing configs
- created multi-zone alerting system
- reduced time to detect from 2.5mins to 1.75mins

Helping Human Reasoning

- bring together global, dependencies and local context
- including runbooks, contacts and escalations directly in the UI

Lessons Learned

- distributed system, challenges about consistency, structural complexity and reasoning about time
- sharding choices are hard, impossible to always avoid making mistakes
- support and collaborate with users, try and reduce support burden with good information at interaction points (UI, CLI etc.), good user guides and docs
- migrating - some happy to move, others not. some push back. had to accept schedule compromise and extra work.

## [Joey Parsons](https://twitter.com/joeyparsons), Airbnb - Monitoring and Health at Airbnb

[Video](https://vimeo.com/173704175)

Perfers to buy stuff:

- New Relic
- Datadog, instrument apps using dogstatsd
- Alerting through metrics

Created open source tool, Interferon, to store alerts configuration as code. 

Volunteer on call system. SREs make sure things in place so anyone can be on call.

- Sysops training for volunteers, monitoring systems, how to be effective and learn from historical incidents
- Shadow on call, learn from current primary/secondary
- Promoted to on call

Weekly sysops meeting, go through incidents, hand offs, discuss scheduled maintenance.

On call health:

- are alerting trends appropriate?
- do we understand impact on engineers?
- do we need to tune false positives?
- are notifications and notification policies appropriate?

Dashboards for:

- incident numbers over time
- counts by service
- total notifcations per user and how many come at night
- false positive incident counts

## [Heinrich Hartmann](https://twitter.com/heinrichhartman), Circonus - Statistics for Engineers

[Slides](http://www.slideshare.net/HeinrichHartmann/statistics-for-engineers-63589022) | [Video](https://vimeo.com/173610069)

Monitoring Goals

- Measure user experience/ quality of service
- Determine implications of service degradation
- Define sensible SLA targets

External API Monitoring:

- sythetic request, measures availability, but bad for user experience
- on long time ranges, rolled-up data is commonly displayed, erodes spikes

Log Analysis:

- write request stats to log file
- rich information but expensive and delay for indexing

Monitoring Latency Averages:

- mean values, cheap to collect, store and analyse, but skewed by outliers/low volumes
- percentiles, cheap to collect store and abalyse, robust to outliers but up front percentile choice required and cannot be aggregated

percentiles: keep all your data. don't take averages! store percentiles for all reporting periods you are interested in - i.e. per min/hour/day. store all percentiles you'll ever be interested in.

Mointoring with Histograms:

- divide latency scale into bands
- divide time scale into reporting periods
- count the name of samples in each band x period

Can be aggregated across times. Can be visualised as heatmaps.


## John Banning, Google - Monarch, Google’s Planet-Scale Monitoring Infrastructure

[Video](https://vimeo.com/173607638)

Huge volume, global span, many teams - constant change

Previously borgmon. Each group had it's own borgmon. Large load on anyone doing monitoring. Hazing ritual - new engineer gets to do borgmon config maintenance.

Wanted:

- can handle the scale
- small/no load to get up and running
- capable of handling the largest services

Monitor locally. Collect and store the data near where it's generated. Each zone has a monarch. 

- Targets collect data with streamz library. Metrics are multi dimensional information, stores histogram. 
- Metrics sent to monarch ingestion router, send to leaf which is in-memory data store and also written to recovery log. From log to long term disk respository.
- Streams stored in a table, basis for queries
- Evaluator runs queries and stores new data for streams or sends notifications

Integrate Globally. Global Monarch - Distributed across zones, but a single place to configure/query all monarchs in all zones.

Provides both Web UI and Python interfaces.

Monarch is backend for Stackdriver

Monitoring as a service is the right idea. Make the service a platform to build monitoring solutions.
