---
layout: post
title: "Operability Day One"
date: 2015-09-24 13:58
comments: true
tags: [operations, conferences] 
---

Today I've been at the [operability.io](operability.io) conference in London.

The conference in intended to be focused on the ops side of devops, and how to make software operable.

This is a single track conference, here is my personal summary and notes from the talks:

## [Andrew Clay Shafer](https://twitter.com/littleidea), Pivotal - What even is operable?

[Video](https://www.youtube.com/watch?v=6f-AEYJXQkQ&index=1&list=PLK4VB0cauli7-_RIvpmn651ePtddw9_Fp)

I've seen a few talks by Andrew before, and they're full of challenging, rapid fire ideas and only loosely tied together - it's more an expression of his world view rather than a talk on a specific subject. With that in mind, I'm still going to try and summarise it.

Andrew asks the question "what even is operable", and in the end he came to the conclusion that *Operability is the intersection of capability and usability.*

There is an emergent architecture, which he calls cloud native, which are a set of patterns that emerged in organisations that deliver highly available applications continuously at scale - like Amazon, Google, Twitter, Facebook etc. There are many associated labels, like devops, continuous delivery and microservices, and these are all inter-related as part of that architecture.

"Do not seek to follow in the footsteps of the wise. Seek what they sought." - Matsuo Basho

The human tendency is to fixate on the solution. We need to think about the problem more. Principles > Practices > Tools. You're not going to be able to do the right things until you internalise the principles. Otherwise you are just imitating or cargo culting.

Equally, we can focus on automation tools and capabilities, not what is being automated.

Other pertinent points:

- if tetris has touagh me anything is that errors pile up and accomplishments disappear
- systems thinking teeachs that we should minimise resistence rather than push harder
- highlighted borg paper and that all tasks run in born run http server that reports health status and metrics
- operations problems become easier when apps are aware of their own health
- worse is better won: broken gets fixed but shitty lasts forever

Referenced the following for reading:

- [Google Borg Paper](http://research.google.com/pubs/pub43438.html)
- Jeff Hodges - [Notes on distributed systems for young bloods](http://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/)


## [Colin Humphreys](https://twitter.com/hatofmonkeys), CloudCredo - inoperability.io

Colin told a war story about what happens when you completely ignore operations? what's the worst that could happen?

A game he worked on had 5 million users and "Launch issues". It hardly worked, because they expected 20k users and ran initially with no budget for operations.

There was a big launch, but the infrastructure for the system was build the day before and completely untested. It was swamped in 10sec. 1.7 million people tried to play 1st day, but couldn't. There were various media reports of the failure.

As a result, managed to steal some funding from the marketing budger and scale 100x, add caching, and throw lots of hardware at the problem. To use the 64 DB servers, they used sharded PHP ORM to distribute API server traffic.

He did get it working, but in time they found transactions not working, as this was supposed to be addressed within the application. It wasn't because of differences between the development and production environments, and as a result cash was disappearing from the game. As a result, everyone's scores had to be reset.

Personally, Colin worked 54 hours solid to get the thing running. For the three months the site ran, he worked 100hr/weeks.

This is how bad a project can get. "I nearly died". He must certainly have burned out. Took a personal sense of pride in the project. Horrible to other people around. Heroism != success.

**Takeaways**:

- Work as a team
- Communicate


## [Anthony Eden](https://twitter.com/aeden), DNSimple - How small teams accomplish big things 

[Slides](https://slidr.io/aeden/processes-how-small-teams-accomplish-big-things) | [Video](https://www.youtube.com/watch?v=9JjURkuIvy8&index=3&list=PLK4VB0cauli7-_RIvpmn651ePtddw9_Fp)

Anthony's talk is about scaling a team, and how they had to scale the operational processes - as a result from various experiences, but none more so than losing one of the founders, someone who know everything about everything.

**Specific Processes**:

Incident Response Plan, consisting of 4 points: Assess, Communicate, Respond, Document.

**Assess** - think before you act. Determine impact. Have a threshold for requesting help. >10 mins results in everyone in a Google Hangout.

**Communicate** - 1 person responsible to communicate to customers. Update twitter, status page.

**Respond** - minimise impact. Triage first. Everyone ask questiosn and propose solutions. Consider available actions and act one best available.

**Document** - post mortem. what happened? why did it happen? how did we respond and revoer? how might we provent similar issues from occurring again?

Other processes were mentioned: On-call rotation. Security Policies. Security escalation policy. System security, RBAC. Track CVEs. Password rotation - especially on admin passwords. etc.

**What makes a good process?**

- Born from Experience
- Written down and available to all
- Concise & Clear
- Act as guidance

Once they're in place you need to:

Execute it, to test it out. Prune where appropriate. Automate where that makes sense.

## [Bridget Kromhaut](https://twitter.com/bridgetkromhout), Pivotal - distributed: of systems and teams

[Slides](http://www.slideshare.net/bridgetkromhout/distributed-of-systems-and-teams) | [Video](https://www.youtube.com/watch?v=YrpSblFRaI4&list=PLK4VB0cauli7-_RIvpmn651ePtddw9_Fp&index=4)

Bridget's talk compared how distributed systems are complex, but so are distributed teams in many of the same ways.

Firstly, distributed != remote. Having a few people out of the office is not the same.

What's important in teams is people > tools. Focusing on people are communicating more important than the tools and how.

She made various points which are important for distributed teams:

Durable communication encourage honesty, transparency and helps future you - "durable communication exhibits the same characteristics as accidental convenient communication in a co-located space. The powerful difference is how inclusive and transparent it is." - Casey West

- Let your team know when you'll be unavailable. 
- Tell the team what you're doing.
- Misunderstandings are easy, need to over-communicate. Especially to express emotions, it's easy to misinerpret textual communication.
- Be explicit about decisions you're making.
- Distribute decision making

## [Colin Hemmings](https://twitter.com/thegonzohunter), dataloop.io - In god we trust, all else bring data

This talk was about the experience of building dataloop as a startup, from working in other companies, and what was learned speaking to 60 companies about monitoring and focued on dashboards.

Generally see the following kinds of dashboards:

- Analytics dashboards, to diagnose performance issues. Low level, detailed info.
- NOC dashboard, high level overview of services.
- Team dashboards, overview of everything not just technical elements - includes business metrics.
- Public dashboards, high level, simplified & sanitised marketing exercises.

Keeping people in touch of reality is the problem, and knowing what the right thing to work on. Discussions on what features to work on get opinionated. There is data within our applications that we can use to make decisions, and they can be represented on dashboards.

- Stability dashboards: general performance, known trouble spots.- Feature dashboards: customer driven, features forum. "I suggest you..." & voting
- Release dashboards: dashboards for monitoring the continuous delivery pipeline

## [Elik Eizenberg](https://twitter.com/elik_eizenberg), BigPanda - Alert Correlation in modern production environments

My personal favourite talk of the first day.

Elik's contention is that there is a lack of automation in regard to responding to alerts.

Incidents are composed of many distinct symptoms, but monitoring tools don't correlate alerts on those symptoms for us into a single incident.

The number of alerts received might not be proportional to number of incidents. The number of incidents experienced may be similar day to day, but the impact of the incidents can be very different - hence the number of alerts being higher sometimes.

**Existing Approaches:**

- compound metrics (i.e. aggregations, or a compound metric build from many hosts). This is relatively effective, but alerts are received late, and you can miss symptoms in buildup to the alert triggering.
- service hierarchy, i.e. hierarchy of dependencies related to a service. Problem with this approach is that it's hard to create & manage. Applications and their dependencies are generally not hierarchical.

**"What I would like to advocate": Stateful Alert Correlation**

Alerts with a sense of time, aware of what happened before now. 

Alerts can create a newincident, or link themself to an existing incident if it's determined they're related.

How do you know that an alert belongs to an incident?


- Topology - some tag that every alert has. (Service? Datacenter? Role?)
- Time - alerts occuring close in time to another alert
- Modeling - learning if multiple alerts tend to fire within a short timeframe
- Training - Machine Learning. User feedback if correlation good or bad.

Even basic heuristics are effective. There is lots of value to be gained from just applying Topology and Time. 

---

There were two other talks after this, but I had to leave early. Sorry to the presenters for missing their talks!




