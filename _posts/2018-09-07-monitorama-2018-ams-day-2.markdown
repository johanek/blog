---
layout: post
title: "Monitorama 2018 AMS Day 2"
date: 2018-09-07 13:03
comments: true
tags: conferences monitoring
---

## Prometheus for Practitioners: Migrating to Prometheus at Fastly - Marcus Barczak, Fastly

First monitoring system: Ganglia + Icinga. Tried to move to SaaS, ended up supporting two systems, growing pains doubled.

Company infrastructure was scaling horizontally, require scaling monitoring vertically.

Project to review monitoring and replace existing systems: scale with infrastructure growth, easy to deploy and operate, engineer friendly instrumentation, first class API support.

Get started:

- build proof of concept
- pair with pilot team to instrument their services
- iterate through the rest

Infrastructure:

- Pair of instances in each POP, both scraping same devices in the POP.
- Frontend in GCP. Grafana, nginx router, federation and alert manager.

Prometheus server:

- ghost tunnel, tls termination and auth
- service discovery sidecar
- rules loader

Created their own service discovery and proxy for prometheus.

Rough Edges:

- Metrics exploration without prior knowledge
- Alertmanager too flexible
- Federation and global views
- Long term storage still an open question


## Rethinking UX for AI-driven Monitoring Tools - Stephen Boak, Datadog

This was a really great talk and my notes could never do it justice.

https://bit.ly/2MNDlZ9


## Building a monitoring strategy and gaining consensus - Gregory Parker, Trevor Morgan, Standard Chartered Bank

No monitoring strategy for company

Back to Basics: What do your users want? Where is their pain points. Put the building blocks in place. Forget what you have and focus on what you need.

- Talk to business and tech influencers
- Listen to fedback and understand contraints
- Publish clear and detailed first principles based strategy
- Get feedback from stakeholders, revise early and often

Get teams to plug in. Avoid mandates, generate awareness, encourage modern solutions, enlist champions.

Build a data lake with common event structure

What went well:

- Engaged with customers throughout
- Inclusive approach, extensible data model
- Roadshows, Show and Tell, Awareness sessions

What could be changed:

- Spend more time gaining consensus early stage
- Work out how to pay for it
- Focus less on legacy technologies

## Self-hosted & open-source time series analysis for your infrastructure - Alexey Velikiy

Analytic unit - shuld be isolated and customisable

Hastic - python app for processing ts data & plugin for grafana with ui for labelling and rendering preductions

Label patterns in grafana, and then it will generate detections. Pattern is a "shape" - peaks, jumps, troughs etc.

Custom models in python. 

https://github.com/hastic/hastic-server

## Monitoring Serverless Things - Mandy Waite, Google

Functions as a Service

By definition, the servers are not accessible. More pieces of monitor and operate.

Retrying function executions is the simplest way to handle failures with serverless functions. Making a function idempotent is required to make it behave correctly on retried execution attempts.

Two distinct variants of functions - http functions, at most once. background functions, at least once.


## How AI Helps Observe Decentralised Systems - Dominic Wellington, Moogsoft

We are living in a different world from the one our systems and processes were designed for

Old world: Static environment, managable alert volumes.
New world: fast growing, fast changing environment, massive alert volumes.

What happens on network edge is now more important, and the edge is far away.

Single faults no longer cause impacts: fault tolerance does not mean zero incidents.

So how do we fix monitoring?

Existing monitoring is incident driven. Assumption that faults are easy to detect, and all failure conditions are knowable.

Dashboards are artefacts of a past failure. Internal health is irrelevant, user requests are what they care about. (Symptom based monitoring)

Observability: continuous stream, high cardinality, build into infra and apps, insight driven. "Actionable Understanding"

Monitoring as it should be: everything passes over a message bus. Then add AI.

AI in IT ops: bring interesting information to the attention of human operators - without having to define it beforehand.

Where to use AI in IT ops:

- Ingestion: reduce noise and false alarms. 
- Correlation: identify related events across domains, avoid duplication of effort and missed signals. 
- Collaboration: intelligent teaming, root cause analysis, knowledge capture.

Teaching the machine. Inputs matter, choose the right feature vectors. Regression problems: continuous distribution. Classification vs clustering: set of dategories.

In Practise:

- Speed matters, work in real time
- You don't know what you need to know
- AI is a tool, not magic
- Process is how you make sure it works for users

## Incremental-decremental Methods For Real-Time Monitoring - Joe Ross, SignalFx

Statistically grounded approaches: dynamic environments, complexity, volume.

Demands streaming algorithms for time series.

Simple calculation: 3 sigma. Implementation: rolling windows. Framework: prime and stream.

Rolling windows are natural foundation for streaming algorithms.

Comparing distributons is not enough. Metods for modeling: double exponention smoothing, and detecting non-stationary series.

Forecasting:

level change: current window differs from forecast. mean is a poor forecast.

exponential weighted moving average: more recent data more relevant. 

double exponential smoothing: models two quantities - level of the series and trend of the series.

incremental decremental solution. how to remove influence of oldest values in sliding window. store additional state: track influence of the initial terms on the terminal values.


Time series classification:

A time series is stationary if it's ditribution does not change over time.
level stationary statistic: tests that a series is stationary around its mean

incremental decremental rolling window implementation: algebraic machinations
