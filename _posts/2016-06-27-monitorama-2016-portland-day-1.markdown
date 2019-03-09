---
layout: post
title: "Monitorama 2016 Portland Day 1"
date: 2016-06-27 20:00
comments: true
tags: conferences monitoring
---

This year I was lucky enough to attend Monitorama in Portland. Thanks to [Sohonet](http://sohonet.com) for sending me! I'd wanted to attend again since going to Berlin in 2013, because the quality of the talks is the highest I've seen in any conference that's relevant to my interests. I wasn't disappointed, it was awesome again.

Here are my notes from the conference:

## [Adrian Cockcroft](https://twitter.com/adrianco), Battery Ventures - Monitoring Challenges

[Slides](http://www.slideshare.net/adriancockcroft/monitoring-challenges-monitorama-2016-monitoringless) | [Video](https://vimeo.com/173609948)

This talk reflected on new trends and how things have changed since Adrian talked about monitoring "new rules" in 2014

What problems does monitoring address?

 - measuring business value (customer happiness, cost efficiency)

Why isn't it solved?

- Lots of change, each generation has different vendors and tools.
- New vendors have new schemas, cost per node is much lower each generation so vendors get disrupted

Talked about serverless model - now monitorable entities only exist during execution. Leads to zipkin style distributed tracing inside the functions.

Current Monitoring Challenges:

- There's too much new stuff
- Monitored entities are too ephemeral
- Price disruption in compute resources - how can you make money from monitoring it?
 
## [Greg Poirier](https://twitter.com/grepory), Opsee - Monitoring is Dead

[References](https://github.com/grepory/monitorama2016) | [Video](https://vimeo.com/173610062)

Greg gave a history and definition of monitoring, and argued that how we think about monitoring needs to change.

Historically monitoring is about taking a single thing in isolation and making assertions about it.

- resource utilisation, process aliveness, system aliveness
- thresholds
- timeseries

Made a defintion of monitoring:

Observability: A system is observable if you can determine the behaviour of the system based on it's outputs

Behaviour: Manner in which a system acts

Outputs: Concrete results of it's behaviours

Sensors: Emit data

Agents: Interpret data

*Monitoring is the action of observing and checking the bahaviour and outputs of a system and its components over time*

Failures in distributed systems are now: responds too slowly, fails to respond.

Monitoring should now be about Service Level Objectives - can it respond in a certain time, handle a certain throughput, better health checks

We need to better Understand Problems (of distributed systems), and to Build better tools (event correlation particularly)

## [Nicole Forsgren](https://twitter.com/nicolefv), Chef - How Metrics Shape Your Culture

[Slides](http://www.slideshare.net/nicolefv/2016-metricsasculture) | [Video](https://vimeo.com/173607646)

Measurement is culture. Something to talk about, across silos/boundaries

Good ideas must be able to seek an objective test. Everyone must be able to experiment, learn and iterate. For innovation to flourish, measurement must rule. - Greg Linden

Data over opinions

You can't improve what yu don't measure. Always measure things that matter. That which is measured gets managed. If you capture only one metric you know what will be gamed.

Metrics inform incentives, shape behaviour:

- Give meaningful names
- Define well
- Communicate them across boundaries

## [Cory Watson](https://twitter.com/gphat), Stripe - Building a Culture of Observability at Stripe

[Video](https://vimeo.com/173610034)

To create a culture of observability, how can we get others to agree and work toward it?

Where to begin? Spend time with the tools, improve if possible, replace if not, leverage past knowledge of teams

Empathy - People are busy, doing best with what they have, help people be great at their jobs

Nemawashi - Move slowly. Lay a foundation and gather feedback. (Write down and attribute feedback). Ask how you can improve. 

Identify Power Users - Find interested parties, give them what they need, empower them to help others

What are you improving? How do you measure it?

Get started. Be willing to do the work, shave the preposterous line of yaks. Strike when opportunies arise (incidents). Stigmergy - how uncordinated systems work together.

Advertise - promote accomplishments, and accomplishment of others. 

Alerts with context - link to info, runbooks etc. Get feedback on alerts, was it useful?

Start small, seek feedback, think about your value, measure effectiveness

## [Kelsey Hightower](https://twitter.com/kelseyhightower), Google - /healthz

[Video](https://vimeo.com/173610242)

Kelsey gave a demo of the /healthz pattern, and how that can protect you from deploying non-functional software on a platform that can leverage internal health checks.

Stop reverse engineering apps and start monitoring from the inside

Move health/db checks and functional/smoke tests inside app, and expose over a HTTP endpoint

Ops need to move closer to the application.

## Brian Smith, Facebook - The Art of Performance Monitoring

[Video](https://vimeo.com/173609989)

Gave an overview of some of the guiding ideas behind monitoring at facebook

Bad stuff:

- High Cardinality - same notifications for 100x machines
- Reactive Alarms - alarms which are no londer relevant
- Tool Fatigure - too few/too many

It can Mechanical, Simple and Obvious to do these things at the time. But the cumulative effect is a thing thats hard to maintain.

Properties of Good Alarms:

- Signal
- Actionability
- Relevancy

Your Dashboards are a debugger - metrics are debugger in production.

## [Caitie McCaffrey](https://twitter.com/caitie), Twitter - Tackling Alert Fatigue

[Slides](https://speakerdeck.com/caitiem20/tackling-alert-fatigue) | [References](http://github.com/caitiem20/monitorama2016) | [Video](https://vimeo.com/173704290)

When alerts ae more often false than true, people are desensitised to alerts.

Unhappy customers is the result, but they are also unplanned work, and a distraction from focusing on your core business.

Same problem experienced by nurses responding to alarms in hospitals. What they have done:

- Increase thresholds
- Only crisis alarms would emit audible aleters
- Nursing staff required to tune false positive alerts

What Caitie's team did:

- Runbook and alert audits - ensure ther eare runbooks for alerts, templated, single page for all alerts, each alert has customer impact and remediation steps. Importantly, also includes notification steps.

- Empower oncall - tune alert thresholds, delete alerts or re-time them (only alert during business hours)

- Weekly on-call retro - handoff ongoing issues, review alerts, schedule work to improve on-call

This resuted in less alerts, and improved visibility on systems that alert a lot.

To prevent alert fatigue:

- Critical alerts need to be actionable
- Do not alert on machine specific metrics
- Tech lead or Eng manager should be on call

## [Mark Imbriaco](https://twitter.com/markimbriaco), Operable - Human Scale Systems

[Video](https://vimeo.com/173607645)

It's common to say now that "Tools don't matter" ... but they do. We sweat the details of our tools because they matter. All software is horrible.

We operate in a complex Socio-Technical System. Human practitioners are the adaptable element of complex systems.

Make sure you think about the interface and interactions (human - software interactions)

- Think about the intent, what problem are you likely to be solving (use cases)
- Consistency is really important
- Will it blend - how does it interact with other systems
- Consider state of mind - high intensity situations/ tired operators

## [Sarah Hagan](https://twitter.com/thesarahhagan), Redfin - Going for Brokerage: People analytics at Redfin

[Video](https://vimeo.com/173610283)

Redfin is an online Estate Agency with agents on ground

Monitoring hiring

- Capture lots of data on the market
- Where should we move?
- How many staff should we have in each location?
- Useful tooling for the audience
- Hire employees rather than contractors, analyse sold house price data to make sure employees earn enough vs. commission agents

Monitoring employees

- Customer reviews for agents
- Agents paid based on rating
- Let the customer monitor the business
- Monitor loading capacity of agents

Monitoring culture

- Internal forums for feedback on tooling.


## [Pete Cheslock](https://twitter.com/petecheslock), Threat Stack - Everything [@obfuscurity](https://twitter.com/obfuscurity) Taught Me About Monitoring

[Slides](http://www.slideshare.net/petecheslock/everything-obfuscurity-taught-me-about-monitoring) | [Video](https://vimeo.com/173607648)

Told the story of his history of learning about monitoring, and how he has approached monitoring problems at his current startup.

Telemetry and Alerting system is not core competancy.

- Do simple things early when it makes sense (put metrics in logs). 
- When it's necessary to get more data - just buy something.
- Hosted TSDB is useful and just works, but there a faster non-durable metrics which are important. So he used graphite for 10s interval metrics, with 2 collectd processes writing to two outputs
- Ended up with a full graphite deployment
