---
layout: post
title: "Monitorama 2018 AMS Day 1"
date: 2018-09-07 13:00
comments: true
tags: conferences monitoring
---


## You don’t look like an Engineer - Monica Sarbu, Elastic

Issues facing females in technology careers, including work/life balance issues and strategies for managing teams to enhance happiness.

## Nagios, Sensu, Prometheus - Why a change of the framework does not change the mindset - Rick Rackow, Ebay


NOC team & SRE team

Started with Nagios

- high noise level
- high false positives/negatives
- culture of downtiming

Migrated to Sensu

- dropped/refactored checks
- 20% unrefactored (mistake)
- attempted knowledge transfer
- more downtiming than ever
- less false positives
- high noise level
- no dynamic checks created outside of monitoring task force

"Sensu is shit, let's get something new"

Migration to Prometheus. "It's going to solve all our problems"

- event based to metric based
- need to refactor 100%
- less noise IF we follow our principles
- less downtimes IF we follow our principles

What we learned the hard way:

- Involve everyone
- Reconsider everything 
  - what you monitor and how you check
  - reconsider your alerting


## Is observability good for our brain? How about post-mortems? - Radu Gheorghe, Rafał Kuć, Sematext

Interactions with tools, people. Learning and daily structure.

Observability/Tools:

- Monitor everything/Alert on everything/Automate everything
- want to see patterns, get stressed when can't understand why something happening
- humans evolved to be easily distracted, context shifting is expensive. alert fatigue related.
- new technology, status threat - threat to self esteem. barrier to learning

Learning:

- Schools don't teach us how to efficiently learn
- Apprentice Method: mentoring/tutoring. 30-50% faster. Experienced person also gains knowledge
- Crash Test Method: exploratory testing. encoded in brain as experience. Need basic knowledge as starting point.
- Dancer Method: 5-30% data retention from reading. needs to be reinforced with practise.
- Place Switch Method: Switch places/roles in organisation. Encourages you to learn and extend knowledge.
- Parrot Method: To share knowledge, rehearse. Combine reading with emotions, imagine crowd - visualisation. 
- Mastering Method: Taking notes. Writing reinforces knowledge. Writing is most effective, doesn't work with typing.
- Box King Method: Take a step at a time.
- Tutor Method: explain to yourself

People:

- Meetings - Meeting in person first matters
- Feedback: naturally wired to seeing whats wrong. constructive feedback doesn't work and micromanagement bad. need to own your own concerns. share concerns and feelings rather than critising/demanding changes. this lowers status threat.

Structure:

- Eat/Sleep/Exercise. Brain eats lots of sugar
- Morning emails, timebox and use for planning
- Plan all the things




## Unquantified Serendipity: Diversity in Development- Quintessence Anx, logzio

Evaluating skills in hires for what diversity of skills they bring to the team.

Mindset Matters. Coach, don't rescue. Offer information rather than assistance. Provide challenges.

Provide explicit onboarding. Last new hire can onboard new hire, reiterate knowledge and improve process.




## How to build observability into a serverless application- Yan Cui, DAZN

survivor bias in monitoring - only focus on failure modes that we identified through experience

could we monitor and alert on the absence of success? something is wrong, but not what is wrong.

otherwise, this talk was repeat of his talk at Monitorama PDX and didn't answer the questions he posed


## Monitoring what you don't own - Stephen Strowes, Ripe NCC

Easy to monitor things you have control over

Once you put something in the wild you're at the mercy of other people's networks - as well as datacenters, cloud providers, CDNs etc.

Service with anycast - traffic easily goes to the wrong place

Which of your users can reach which of your location? Can you isolate a network problem?

You need vantage points to measure, debug or monitor the public network.

RIPE Atlas: global network of measurement probes.
 
- Allows measurements, you can instruct platform to run measurements and collect results
- Need to run probes to earn credits to spend them on measurements

DNS

- where do ISPs mess with your DNS records? Where are TTLs not honoured?
- querying dns from problam networks can reveal ISP resolver behaviour

Traceroute

- routing is not totally within your control, often asymmetic, difficult to debug without path traces
- traceroutes from many locations give you info in aggregate about congestion/loss along the path

Atlas for Monitoring

- Expose data, allow people to write tools on top of this
- streaming API
- ping: status-checks
- results API



## What the NTSB teaches us about incident management & postmortems - Michael Kehoe, Nina Mushiana, Linkedin

Production SREs

NTSB - US National Transportation Safety Board. Aviation, Land Transportation, Marine and Pipeine accidents. Determines probable cause of accidents and reports on findings.

Investigation Process:

- preinvestigation preparation
  - go team, ready for assignments: on call schedule.
  - investigator in charge (IIC)
  - subject matter experts
- notification and initial response
  - regional reponse, notify national headquarters
  - initial PR and stakedown
  - establish severity and assemble go team if necessary
- on scene
  - establish command rooms.
  - first: organisation meeting, bring up to speed, establish tasks, roles and lines of authority
  - IIC most senior person on scene
  - daily on site progress meetings at end of day, plan next day
  - briefing headquarters
- post on scene
  - formal report structure. facts, analysis, conclusions, recommendations, appendices.
  - first: work planning and build timelines.
  - fact report based on field nodes created
  - technical review: all parties review all factual information
  - then dedicated department to write report

NTSB advocates for the most important recommendations from their reports each year.

Applying to operations:

- incident commander pre-assigned
- test pagers, ensure access works
- NOC notifies incident commander
- Once verified launch full response for major incident
- mitigate ASAP
- private + public slack channels
- IC establishes war room. assigns roles and responsibilities, and prioritisation. communication at regular intervals to execs. gather data and update timeline doc

post incident activities:

- post mortem
  - dedicated team
  - template
  - blameless
- postmortem rollup
  - action items are prioritized
  - weekly reporting on status of action-items

The more you invest in the process the more you will get out of it

Vital that there is accountability on improvements and action items. Most action items resolved within one month.

## A thousand and one postmortems: lessons learned from running complex systems at scale - Alexis Lê-Quôc, Datadog

Talking openly about failures

Learn from past mistakes, feel kinship in the face of system failure, share what you learned with others

Datadog: lots of data, all day long, every day under tight processing deadlines.

Complex systems almost always are in stable but degraded mode. Each incident is recording noteworthy deviation from what we expect. Most incidents deserve a post mortem - got good at writing them.

Looking back- two extremes: detailed narative on why and fixes, and also high level aggregates and trends

Looking at all in aggregate, formalise anti-patterns into a living document. Invaluable tool for new and old hands alike.

Facing and acknowledging failure in front of others is difficult. It's a learned skill that needs a safe environment.

Talking about failure in public is even harder. Forget about the specifics and focus on patterns. Recurring themes in why section. Simplify, but keep just enough context to make sense.

Anthology of anti-patterns:

- Configuration: config not immediately picked up, delayed incident. expose config identifier at runtime, assert what runs is what is intended.
- Dependencies: timeouts - loadbalancer timeout of 10s but downstream 60s. expensive requests dominate runtime. downstream services should have timeouts shorter than upstream.
- Deployment: uptime means victory. past results are not an indication of future performance. need explicit sanity checks.
- Development: time, dealing with DST changes. Difficuly to thoroughly test, default to UTC everywhere (except UI).
- Observability: tail of distribution. aggregates and perventiles mask reality of user experience - slowest could be most important. Pay special attention to the tail, check worse requests individually.
- Operations: Expensive roll back or forward. Bad deploy - debate what to do is time consuming. Pick one strategy and invest heavily in it and make it really good.
- Performance: arbitrary resource limits. hard to pick limits for connections, file handles etc. Set reasonable soft limits and ideally no hard limits and let system hit actual resource limits OR reigorously model and validate limits.
- Routing: retry too often. Simplistic retry approaches multiples load on backend systems. Use adaptive retries such as CoDel.
