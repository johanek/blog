---
layout: post
title: "Monitorama roundup part 2"
date: 2013-09-23 11:37
comments: true
tags: [monitoring]
---

[Part one is available here](http://johan.org.uk/sysadmin/blog/2013/09/20/monitorama-roundup-part-1/)

During the second day there were multiple tracks available - I mostly followed the workshop track, only catching one presentation on the speaker track.



##  [Florian Forster](https://twitter.com/flocto), collectd - Collecting custom metrics ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-collectd-workshop-florian-forster)

Described the collectd data model and how to use the Exec plugin to execute arbitray scripts for collecting custom metrics.

Also presented a statsd plugin - implementation of statsd network protocol inside collectd.


## [Abe Stanway](https://www.twitter.com/abestanway) - Kale (Skyline and Oculus) ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-kale-workshop-abe-stanway)

Presentation of architecture for the kale suite of tools recently released by etsy. 

You can find a better description on [the etsy blog](http://codeascraft.com/2013/06/11/introducing-kale/)


**Skyline** - Analyse time series for anomalies in (almost) real time

The setup at etsy includes 250k metrics, which takes about 70sec for anomaly discovery, and requires 64GB memory to store 24 hours of metrics in memory.

- carbon-relay is used to forward metrics to the horizon listener
- metrics are stored in redis
- data is stored in redis as messagepack (allows efficient binary array stream)
- roomba runs intermittely to clean up old metrics from redis 
- amalyzer does it's thing and writes info to disk in JSON for the web front end

To identify anomalies, skyline uses some of the techniques that Abe talked about in his presentation the previous day. It uses the consensus model, where a number of models are used and they vote - so if a majority of models detect an anomaly, then that is reported.

**Oculus** - analyse time series for correlation

Oculus figures out which time series are correlated using Euclidian Distance - the difference between time series values.

It also uses Dynamic Time Warping - to allow for phase shifts, if the change in one series occurs later than in the other. But this is slow, so it's targeted on the time series to could be correlated by comparing shape descriptions.

- data pulled from skyline redis and stored in elasticsearch
- time series converted to shape description (limited number of keywords that describe the pattern)
- phrase search done for shared shape description fingerprints
- run dynamic time warping on that data



## [Pierre-Yves Ritschard](https://twitter.com/pyr) - Riemann ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-riemann-workshop-pierre-yves-ritschard)

Unfortunately this presentation was marred by a projector/slide deck failure which made it hard to follow. It was incredibly disappointing because there was a lot of positive discussion around Riemann and I was looking forward to a better exposition of the tool.

Riemann is a event stream processing tool.

- All events sent to riemann have a key value data structure - for logs, metrics, etc.
- You can use all your current collectors: collectd, logstash etc, and has an in app statsd replacement
- Those events can be manipulated in many ways, and sent to many outputs
- The query language, clojure, is data driven & from lisp family
- There is storage available for event correlation but I didn't really understand from his discussion


## [Devdas Bhagat](https://twitter.com/f3ew) - Big Graphite ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-big-graphite-workshop-devdas-bhagat)

This workshop covered how booking.com have scaled their graphite setup.

They have somewhere in the region of 5000 hosts, multiple terabytes of data stored in whisper.

Both IO and CPU have become bottlenecks and in each instance they have thrown hardware at the problem to run more agents and shard their data.

I/O probems:

- Ran into IO wall, disks 100% writing. Lots of seeking
- Have ended up using SSD drives in RAID0
- Sharding becomes hard to maintain and balance 
  - Don't know in advance in which namespace metrics will be created
  - Rebalancing tricky when adding more backends - they have a script that replicates graphite hashing function and manually move things
- Found SSDs not as reliable as spinning disk under high update conditions
  - Lots of drive failures, so replicate data to separate datacenters to provide availability
- FusionIO performance no improvement from SSDs (I find this hard to believe)

CPU problems:

- Relays start maxing out CPUs
   - Multiple relay hosts (per datacenter)
   - Multiple relays on each host (1 per core)
   - Use haproxy load balancer (prevent losing metrics)

Other Problems:

- Software breaking on updates (whisper failure on upgrade)
- People can use the software in surprising ways - not time series data, or one record a day


## [David Goodlad](https://twitter.com/michaelgorsuch) - Infrastructure is Secondary ##

[Slides](https://speakerdeck.com/monitorama/berlin-2013-session-david-goodlad) | [Video](https://vimeo.com/75664601)

David presented that your primary metrics should be your business metrics, and that your infrastructure metrics are secondary. Which is not to say infrastructure metrics aren't important, but the business metrics are measures of how your business is performing and this is the data which you should be alerting on. 

- Alerts should be informational and actionable - not just "cool story, bro"
- Consider what matters to customers - i.e. instead of measuring queue size, use time to process
- When a business metric alerts, then correlate against infrastructure monitoring
- Keep the infrastructure thresholds, but don't alert on that information - you can access it when necessary

He gave a great one liner to help decide what you should be measuring - "What would get your boss fired?" - Measure these things deeply.

Also pushed the idea of sharing your information outside the team - to be more transparent and visible to the rest of the business, particularly since the information you hold are business metrics. This will provide feedback about the metrics which are important to others.


## [Michael Gorsuch](https://twitter.com/michaelgorsuch) - Graph Automation ##

This workshop was a practical introduction to instrumentation and exploration - stepping through configuring StatsD, graphite and collectd to instrument an application and exploring graphs using descartes.




