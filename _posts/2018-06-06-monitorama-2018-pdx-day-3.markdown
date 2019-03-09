---
layout: post
title: "Monitorama 2018 PDX Day 3"
date: 2018-06-06 19:46
comments: true
tags: monitoring conferences
---

## Achieving Google-levels of Observability into your Application with OpenCensus - Morgan McLean (Google)

OpenCensus - distributed traces, tags, metrics (+ logs)

Collection of libraries for multiple languages, instrumentation and support for multiple exporters for tracing and metrics

One thing to do all the things



## The present and future of Serverless observability - Yan Cui (DAZN)

New challenges - no agents or daemons on the platform, or background processing, higher concurrency to telemetry systems, adding to user facing latency when sending telemetry in functions, async invocation makes tracing mmore difficult.

Write metrics in logs, as the platform provides logging. Extract that data in post processing.

Async processing - just send metrics in function

Our tools need to do more to help understand the health of the system, rather than a single function


## Putting billions of timeseries to work at Uber with autonomous monitoring - Prateek Rungta (Uber)

Built their own TSDB because existing solutions don't work at their scale - M3DB: [https://github.com/m3db/m3db](https://github.com/m3db/m3db)


## Building Open Source Monitoring Tools - Mercedes Coyle (Sensu)

Lessons learnt in the Sensu v2 rewrite


## Autoscaling Containers... with Math - Allan Espinosa

Using control theory to help regulate an autoscaling system

- Iterate on feedback of the system
- Models that tell you if your feedback is effective
- Linear models go a long way
- Re-evaluate your models

## Assisted Remediation: By trying to build an autoremediation system, we realized we never actually wanted one - Kale Stedman (Demonware)

Online gaming systems

Nagios constantly full of CRIT warnings. Hostile environment for 1st responders: hard to find alerts in the floor, hard to understand context. Cost of making an incorrect decision is high. Low morale, high turnover.

Plan: Rebrand, Auto-remediation, ???, Profit.

Lots of same tasks being run on the same systems.

System as planned: check results, alert processing engine (calls other APIs), remediation runner. Domains: Detection (Sensu), Decision (StackStorm), Remediation (Didn't decide).

Review and process all alerts. Migrated many to sensu. Started processing alerts more thoroughly - put all alerts in JIRA and root causes started to be addressed.

Dropped idea of remediation, as alerts decreased realised they had what they needed already - better info for responder, working on fixing underlying causes

Razz: Detection (sensu), Decision (Stackstorm alert workflow), Enrichment (stackstorm widget workflow), Escalation (Stackstorm JIRA workflow)

Monitoring Maxims:

- Humans are expensive (don't want to waste their time)
- Humans are expensive (make mistakes, unpredictable)
- Keep pages holy (issue must be urgent and for the responder)
- Monitor for success (ask if it is broken, rather than what is broken)
- Complexity extends incidents
- Restoration > investigation
- LCARS: link dashboards, elasticsearch queries, other system statuses, last few alerts

Today:

- Alert volume down
- Data driven decisions up
- Reliability and support quality up
- Team morale up


# Security through Observability - Dave Cadwallader (DNAnexus)

Improve relationship between security and ops

Security and compliance concerns handling medical data.

Compliance is about learning from mistakes and creating best practices. Designed with safety in mind, but doesn't guarantee safety.

Security want to do less compliance, and more time threat hunting. How do we automate compliance checks?

Inspec - compliance as code. Check security in VMs, settings on cloud resources. Community is thriving, plenty of existing baselines available for use.

Run inspec locally, and write out to json. Prometheus to pull the data, custom exporter.

Apply SLOs - actionable compliance alerts. Link back to documentation on compliance documentation. Friendly HTML report pushed to S3 and linked in alert.


# How to include Whistler, Kate Libby, and appreciate that our differences make our teams better. - Beth Cornils (Hashicorp)

Talk about inclusivity in tech, how we can improve



