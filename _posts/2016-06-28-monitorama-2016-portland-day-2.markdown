---
layout: post
title: "Monitorama 2016 Portland Day 2"
date: 2016-06-28 20:00
comments: true
tags: conferences monitoring
---

## Brian Overstreet, Pinterest - Scaling Pinterest's Monitoring

[Video](https://vimeo.com/173704315)

Started with Ganglia, Pingdom

Deployed Graphite, single box

Second Graphite architecture - Load Balancer, 2x relay servers, multiple cache/web boxes etc.

Suffered lots of UDP packet receive errors

Put statsd everywhere

- fixed packet loss, unique metric names per host
- latency only per host, too many metrics

Sharded statsd

- not unique per host now,
- shard mapping in client, client version needs to be same everywhere

Multiple graphite clusters - one per application (python/java)

More maintenance, more routing rules etc.

Problems with reads, multiple glob searches can be slow

Deployed OpenTSDB

Replace statsd

- local metrics agent, kafka, storm - send to graphite/opentsdb

Metrics-agent:

- interface for opentsdb and statsd
- sends metrics to kafka
- processed by storm

120k/sec graphite, 1.5m/sec opentsdb. no more graphite, move to opentsdb.

Create statsboard - integrates graphite and opentsdb for dashboards and alerts

Graphite User Education - underlying info about how metrics are collected, precision, aggregation etc.

Protect System from Clients 

- alert on unique metrics
- block metrics using zookeeper and shared blacklist (created on fly)

Lessen Operational Overhead

- more tools, more overhead
- more monitoring systems, more monitoring of the monitoring system
- removing a tool in prod is hard

Set expectations

- data has a lifetime
- not magical data warehouse tool that returns data instantly
- not all metrics will be efficient

Summary:

- match monitoring system to where the company is at
- user editation is key to scale tools organizationally
- tools scale with the number of engineers, not users


## [Emily Nakashima](https://twitter.com/eanakashima), Bugsnag - What your javascript does when you're not around

[Video](https://vimeo.com/173610415)

Lots of app moving to frontend, so running in browser not on backend servers

Toolkit:
 
- capture load performance from browser, send to app server, use statsd + grafana & google analytics
- capture uncaught exections in the browser, using their own product

Sorry, Javascript is just not that relevant in my line of work

## [Eron Nicholson](https://twitter.com/vinzclortho) and [Noah Lorang](https://twitter.com/noahhlo), Basecamp - CHICKEN and WAFFLES: Identifying and Handling Malice

[Slides](https://github.com/sohonet/monitorama2016/blob/master/Chicken%20and%20Waffles%20-%20Monitorama%202016.pdf) | [Video](https://vimeo.com/173704281)


Suffered DDoS and blackmail. 80 gigabits - DNS reflection, NTP reflection, SYN floods, ICMP flood

Defense and Mitigation:

- DC partner filters for them
- More 10G circuits and routers
- Arrangements with vendors to provide emergency access and other mitigation tools

Experience got them serious about more subtle application level attacks:

- vulnerability scanners
- repeat slow page requests
- brute force attempts
- nefarious crawlers

What do we want from a defense system?

1. Protection against application-level attacks
2. Keep user access uninterrupted
3. Take advantage of the data we have available
4. Transparent in what gets blocked and why

Chicken: who is a real user and who is malicious?

Considered Machine Learning classification. Problems: really hard to get a good training set. Need to be able to explain why an IP was blocked.

Simpler approach: 

- Some behaviours are known to be from people up to no good. crawling phpmyadmin, path reversal, repeated failed login attempts etc.
- Request history gives a good idea of whether someone is a normal user, broken script or a malicious actor.
- External indicators: geoip databases, badip dbs, facebook threat exchange

Removing simple things reduces noise. Every incoming request is scored and per-IP aggregate score calculated based on return code. Create Exponentially Weighted Moving Average from that data. About 12% had negative reputation.

Scaning for blockable actions and scoring requests in near real-time using request byproducts.

Request logs, netflow data, threat exchange -> kafka -> request scoring, scanner for known bad bahaviour, tools for manual evaluation.

Average IP reputation gives an early indicator to monitor for application level attack.

Provides list of good, bad, and dubious IPs.

Enforcement:

- originally provided by iptables rules on haproxy hosts
- then tried rule on loadbalancer
- then tried null routing on routers
- finally created waffles

Using BGP flowspec to send data from routers to waffles, which then decides what path to take: error, app or challenge. Waffles host live in a seperate network with limited access. 

Waffles is redis and nginx.

## [John Stanford](https://twitter.com/jxstanford), Solinea - Fake It Until You Make It

[Video](https://vimeo.com/173610212)


Monitoring an openstack cluster, 1 controller and 6 compute nodes, taking logs with heja and sending it to elasticsearch. Can I scale this up to a thousand nodes? How big can it get?

How do you go about figuring that out?

- took 7 days of logs from lab, 25k messages/hr
- number of logs coming from a node
- number of logs coming from a component
- 7 day message rate, look at histograms, identifies recurring outlier
- message size, percentiles of payload size

What models look like what we're doing for simulation? Add some random noise.

Flood process, monitoring everything, repeat until it breaks. System sustained 4k x 1k messages/sec, started to pause above that, but no messages were dropped.

Next steps:
- find bottlenecks
- improve the model


## [Tammy Butow](https://twitter.com/tammybutow), Dropbox - Database Monitoring at Dropbox

[Slides](https://paper.dropbox.com/doc/Database-Monitoring-at-Dropbox--0JUfRc532EeRDAc1aPYCv) | [Video](https://vimeo.com/173607649)


Achieving any goal requires honest and regular monitoring of your progress.

Originally used nagios, thruk (web ui) and ganglia

Created own tool vortex in 2013

why create in house monitoring?

- performance, reliability iissues, scaling number of metrics fast

Create Vortex: 

- Time Series Database with dashboards, alerting, aggregation
- Rich metric metadata, tag a metric with lots of attributes

Monthra: single way of scheduling and relaying metrics, discourage scheduling with cron

Service Metrics:
- what durability, reliability goals? align monitoring to goals?
- threads running/ threads connected

Run a Monthly Metrics Review (great idea)


## [Dave Josephsen](https://twitter.com/davejosephsen), Librato - 5 Lines I couldn't draw

[Video](https://vimeo.com/173610048)

1. Making cofnitive leap to use monitoring tools to recognise system behaviour independent of alerting. misapprehension about what monitoring was and whom it was for.

2. Monitoring is not for alerting. Nobody owns moitoring. 'Tape measure that I share with every engineer I work with'. Ops owns monitoring vs everyone owns monitoring. Monitoring is for asking questions.

3. Complexity isolates. Effective monitoring gives you the things that allow you to 'Cynefin' - make things more familiar and knowable. Reduce complexity rather than embracing it. Monitoring can build bridges to help people understand things across boundaries.

4. Effective monitoring can bring about cultural change, how people interact between each other.

5. Repeated point 4

## [Jessie Frazelle](https://twitter.com/jessfraz), Google - Everything is broken

[Video](https://vimeo.com/173704265)

Talked about problems with Software Engineering and Operations

Demonstrated how they monitored community and external maintainer PR statistics for Docker project.

## [James Fryman](https://twitter.com/jfryman), Auth0 - Metrics are for Chumps - Understanding and overcoming the roadblocks to implementing instrumentation

[Video](https://vimeo.com/173704302)

Story of implementation of instrumentation at Auth0

Wanted data driven conversations. Metrics implementation happened in past, was ripped out because not well understood, thought to cause latency. Created adversions.

Make the chase. Get buy-in.

To have good decent conversations with someone you need to have metrics. 

Pushback:

- Not the most important feature - but it is!
- Cannot start until we understand the data retention requirements - premature optimisations
- We don't run a SaaS - need to understand what your software is doing regardless

Make decisions based on knowledge, not intuition or luck.

Be opportunistic - success is 90% planning, 10% timing and luck. Find opportunites to accellerate efforts.

Needed to get something going fast - went for full service SaaS Datadog, but with common interfaces and shims to allow moving things in house later. Don't delay, jump in and iterate.

Keep in sync with developers - change is difficult and there will be resistance, pay attention to feedback. Need to support interpretation of data.

Build out data flows, find potention choke points in system, take a baseline measurement, check systems in isolation

Fix and Repair bottlenecks. Solved 3 major bottlenecks, went from 500 to 10k RPS.
