---
layout: post
title: "Monitorama 2018 PDX Day 1"
date: 2018-06-06 19:44
comments: true
tags: conferences monitoring
---

## Optimising for learning - Logan McDonald


expert intuition is achievable. improve memory.

- prep

hierarchy of learning. important one is rule learning. 

- gaining knowledge

reading docs/textbooks not an effective way to embed knowledge in long term memory. do low stakes testing. best way of learning if to retrieve data. 

- mental models

observabiity and reflection

move from events to patterns to structure

engaging in incident reviews gave opportunity to quiz engineers on their actions during incident

- learning together

symmathesy - systems of understanding

embrace cultural memory



## Serverless and CatOps: Balancing trade-offs in operations and instrumentation - Pam Selle


I sadly missed most of this because I was debugging a problem


## Mentoring Metrics Engineers: How to Grow and Empower Your Own Monitoring Experts - Zach Musgrave, Angelo Licastro (Yelp)

growth in teams, and managing growth in individuals within a team

mandate growth - more skills needed, more knowledge gaps, more planning (meetings), trade offs.

knowledge silos - reaction is mentoring

breadth: build confidence. defined mentor relationship. 

depth: make an advanced contribution to one system.

next steps: end of mentor relationship, can start on-call. hold a retrospective - provide feedback for improvement

impostor syndrome - accept compliments for your work and acknowledge other's contributions

consulting: monitoring is a specialised field. there's a lot of nuance.
make people aware of what tools can solve their problems. talk with other teams, ask insightful questions: what problem are you trying to solve? listen, as assume you know nothing about their problem.


# The Power of Storytelling - Dawn Parzych (Catchpoint)

Cognitive bias

* too much info
* not enough meaning
* not enough time
* not enough memory

To tell better stories, when presenting data view it from the perspective of other parts of the organisation

Persuasive storytelling doesn't need to be complicated - keep it simple

Use simpler language - it doesn't make it less powerful

Present the most important information earlier

* Use visuals when telling a story, keep them simple to understand
* Don't overcomplicate things
* Remember the power of 3


## Principia SLOdica - A Treatise on the Metrology of Service Level Objectives - Jamie Wilkinson


Overloaded team, tasked with reducing load to build a sustainable system they could manage

Symptom Based Alerting - focus on very few expectations about your service, so as system grows you are still focusing on the same things

Symptom: a user is having a bad time. Causes: internal views on the service.

What's your tolerance for failure? Error budget. Set expectations: SLO

Symptom anything that can be measured by the SLO. Symptom based alert, is when SLO is in danger of being missed.

Debugging tools - metrics, tracing, logs - replace cause based alerts


## On-call Simulator! - Building an interactive game for teaching incident response - Franka Schmidt (Mapbox)

On call onboarding

Safe and low stakes place to practice handing on call incidents

Onboarding:

- Buddy System: Observing
- Bucket list: checklist, how far along you are with experiences of being on call
- Alarm scrum: review last days alarms

Simulator - "choose your adventure" type text adventure game. Tool: Twine.

Craft a story - use Incident Reviews, past notes and enrich with detail. Or just make it up.

Iterate and get feedback.



## Observability: the Hard Parts - Peter Bourgon (Fastly)

Level up monitoring story at fastly

Senior engineering org, 120 engineers. Heterogeneous solutions throughout the organisation. Organic growth is good - up to a point.

Goals: are production systems healthy? if not why not?

Non goals: long term storage, replacing logging. (Observed metric usage VERY different from self-reported usage)

Strategy: prometheus, add instrumentation, curate new set of dashboards and alerts, run in parallel to build confidence, decom old systems.

Rollout: Inventory all services. Rank by criticality & friendliness.

The grind... 

Embedded expert model. Pair with responsible engineer to get migration done. Hour or two of pair programming. Let documentation emerge naturally. Deploy prometheus, plumb service into prometheus (time consuming). 

Technical autonomy is a form of technical debt. Focus on local vs. global optimization.

Dashboards and alerts. Import from other systems. Make sure to only build things in service to original goals. Reduce, keep high level views.

Some services, ownership can be indistinct. Senior leadership needed to wield stick, need their buy in.


## Warning: This Talk Contains Content Known to the State of California to Reduce Alert Fatigue - Aditya Mukerjee (Stripe)

[Slides](https://speakerdeck.com/chimeracoder/warning-this-talk-contains-content-known-to-the-state-of-california-to-reduce-alert-fatigue)

We can learn from clinical healthcare

Alert Fatigue - frequency/severity - causes responder to ignore or make mistakes

Decision Fatigue - frequency/complexity of decision points, causes person to avoid devices or make mistakes

Certain patterns of alerts and decisions contribute disproportionately to fatigue. Multiple false positives for an individual patient, impacts that alert over all patients.

Reduce alert fatigue: STAT. Supported, Trustworthy, Actionable, Triaged.

Supported: who owns this alert? Responders should own, or feel ownership over end result.

Trustworthy: do I trust this alert to notify me when a problem happens? stays silent with all is well? give sufficient information to diagnose problems?

Anomaly detection: if you don't understand why an alert triggered, you don't understand if it's real.

Actionable: One decision require to respond. Alerts difficult to action are ignored. Make alerts specific, add decision trees. Alerts must have a specific owner.

Triaged: Triage alerts. Type should reflect urgency. Urgency can change. Commonly understood tiers. Regular re-evaluation process.



## Monitory Report: I Have Seen Your Observability Future. You Can Choose a Better One. - Ian Bennett (Twitter)


Twitter has a big monitoring system and migrating was hard




