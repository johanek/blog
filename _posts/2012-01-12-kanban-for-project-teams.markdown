---
layout: post
title: "Kanban for Project Teams"
date: 2012-01-12 22:00
tags: kanban
---

For the past 9 months I've been managing the day to day activities of a team. Before that I really had no experience of this sort of task. All the team members are very experienced and are considered subject matter experts within the business, so my role is not mentoring as with past senior sysadmin roles. During this time I'd been struggling to find a way of keeping track of the tasks and projects the team were working on. I ended up with boring weekly meetings, and taking notes of live projects where the notes just got longer, and longer each week.

Then late last year, I started considering doing Kanban after reading this article: <http://agilesysadmin.net/kanban_sysadmin> - So I researched Kanban further, read [David Anderson's book about Kanban](http://www.amazon.co.uk/Kanban-David-J-Anderson/dp/0984521402/ref=sr_1_1?ie=UTF8&qid=1326406289&sr=8-1), and bought a whiteboard and a bunch of cards and magnets.

This week, I introduced the concept to the team. We're a project delivery team, rather than your regular operational sysadmin team. But we're all operations sysadmins at heart, we understand those problems and have worked in that environment - but we only deliver projects and no one pages us.

So we spend a lot more of our time tracking larger projects - but these projects involve a lot of smaller activities, which involve people coming to your desk and asking for something quickly. Everyone works on multiple projects at once and is quite busy - things develop and need to be delivered fast, with as little resource as possible - so balancing the time requirements and due dates of multiple projects is an art of itself.

The goals of this experiment are twofold: make the intra-team communication less of a burden, and to try and improve our agility. I don't have to ask everyone what they're doing all the time, rather I can look at the board and get the highlights at a glance.

Here's a really stupid paint diagram of what the board looks like to start:

![image](/sysadmin/assets/images/kanban.png)

I'll try to get a picture of what the real board looks like at some point.

We went for this model, as it reflects the individuals workload within the team, which is what we are interested in. Cards move left to right, are in a big pool when they're still TODOs, but then they jump into an individuals swimlane when in flight.

We also discussed the possibility of having a more project focused structure - with an extra project column at the start, holding project cards which each have their own swimlane. The system we have doesn't really cater for understanding the current tasks from a project perspective. Let's leave that for the Project Managers...

I kept the rules simple for now - cards only move to the right, and respect the board - only work on things that are on the board. One "rule" that I set as a guideline to be discussed was sizing of the tasks. I suggested that the size of the tasks on each card should allow someone else to perform the task. (We also suggested a task of roughly one day's effort is roughly the right size).

A problem that I see with our team is that everyone has been tightly fit into roles - Windows, Linux/Application Environments and Storage. We've had a reasonable turnover of staff recently, and we've grown in size from 4 to 6. This helps provide the opportunity for transformation of working practise, so I want to promote more sharing of tasks - at the moment we're too reliant on individual availability, and this is affecting project delivery.

For now, I've also neglected to impose any work in progress limits. The board is an experiment that I hope will help us identify workflow problems. I suspect that too much work in progress is a problem, and we would see the benefits of reducing it - but until that happens I'm not going to apply it. Visualising the bottlenecks is the key, and they have to be clearly seen for everyone in the team to understand the reasoning behind work in progress limits.
