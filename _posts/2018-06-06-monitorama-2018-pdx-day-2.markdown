---
layout: post
title: "Monitorama 2018 PDX Day 2"
date: 2018-06-06 19:44
comments: true
tags: monitoring conferences
---

## Want to solve Over-Monitoring and Alert Fatigue? Create the right incentives! - Kishore Jalleda (Microsoft)

Lessons from healthcare - more monitoring is not always better

Problems of far too many alerts at Zynga. Vision of <2 alerts per shift. Dev on call, SRE for engineering infra and tooling. Zero TVs.

One day massive outage, multiple outages with same root cause.

Idea: Deny SRE coverage based on Alert budgets. Lot of push back - from SRE team and from supported teams. 

Baby steps - focus on monitoring and prove we can do one thing well. Promise of performing higher value work.

Leverage outages - Postmortems, follow ups. Build credibility, show you care.

Find Allies - identify who is aligned with you. Need to go out and find them.

Call your Boss - ensure they are aligned. Get buy in from Senior Leaders.

Establish contracts. Targets for all teams. Give time to clean up before launch.

Reduce alert noise - aggregation, auto remediation, what should be a logs or a tickets or an alert.

Success - 90% drop in alerts, 5min SRE response, uptime improved


## Next-Generation Observability for Next-Generation Data: Video, Sensors, Telemetry - Peter Bailis (Standford CS)

Taking systems engineering/thinking approach to dealing with speeding up applying ML models to video analysis.

Interesting technology and family of tools being developed.

## Coordination through community: A swarm of friendly slack bots to improve knowledge sharing - Aruna Sankaranarayanan (Mapbox)

Chatbots in slack. Commands are AWS lamba functions. 

sumo logic queries. benchmarking. user lookup. get/set rate limits. platform-question: assign questions to an engineer, with escalation.


## Automate Your Context - Andy Domeier (SPS Commerce)

Complexity is increasing to enable velocity

Context: circumstances that form the setting for an event, statement or idea, and in terms which it can be fully understood and assessed

As complexity increases, amount of available context increases. Eficiency of an organisation directly correlated to how effective you are with your available context.

Goal - make the right context available at the right time.

Context. People, monitoring, observability, obscure and hard to find things.

People: One consistent set of operational readiness values. Operation info, Peformance (KPI/Cost), Agility (Deployment maturity), Security

Monitoring: taking action. Examples:

- Put alerts onto SNS topic. Automate actions with lambda functions. Search the wiki for documentation, post back to alerts commenter. 
- JIRA incidents to SNS as well, automate incident communication. Search for recent changes from JIRA. 
- Change management in JIRA, dependency lookup & commment back to JIRA.



## Slack in the Age of Prometheus - George Luong (Slack)

We replace monitoring systems because our needs have evolved

Ganglia & Librato, migrated to Graphite. Looked at migrating away.

User Problems: metrics difficult to discover. Query performance made for slow rendering. Other problems specific to their usage.

Operation Problems: Could not horizontally scale the cluster (lack of tooling, time and effort). Single node fails led to missing metrics. Susceptible to developers accidentally taking down cluster.

Requirements. User: Ease of discover, fast response, custom retention, scales with us. Operational: Remove single node POF. Teams want to own their monitoring. 

Prometheus ticked almost all those boxes, except custom retention and ingestion. (can only be set per box)

Architecture: 

- in region: duplicate prom servers, scraping same servers. primary and secondary. 
- between regions: single pair of federated servers scraping other prom servers.

Configuration Managemenet: terraform & chef. Prom jobs and rules stored in chef, ruby hash converts to yaml.

Webapp server about 70k metrics, x 500 servers (35m)

Job worker, 79k metrics x 300 servers (24m)


## Sparky the fire dog: incident response as code - Tapasweni Pathak (Mapbox)

Sparky the firedog:

SNS topic - lamba function - forwards to Pagerduty

sparky is a npm module

documentation for alarms in github. sparky enriches the alarms.

- reformat the alarm info
- aggregate all your teams alarms into a single Pagerduty policy
- links to targetted searches
- get the root cause analysis?

Future: score an alarm. Does a human need to action this? Based on the triaging/context we have existing in documentation.

Sample questions that need answering on an alert:

- How many errors around trigger time?
- Are the errors ongoing?
- What was the very first error?
- Group and count the errors by time


## Reclaiming your Time: Automating Canary Analysis - Megan Kanne (Twitter)


Is my build healthy? Want to catch errors before causing problems.

Canary - partial deployment. Use canary cluster for canary deploys. Needs production level traffic. Control cluster to compare against canary.

Use statistical tools to compare.

Median Absolute Deviation - maxPercentile

DBSCAN - density based spatial clusering of applications with noise. - toleranceFactor

HDDBSCAN - hierarchial dbscan - minSimilarShardsPercent (minimum cluster size)

Mann-Whitney U Test - tolerance, confidenceLevel, direction

Simplify configuration (of your statistical tests). Sensible defaults speed up adoption. 

Choosing metrics - SLOs, existing alerts.

User Trust - Build it.

