---
layout: post
title: "Kanban update"
date: 2012-03-29 16:46
comments: true
tags: kanban
---

So, here’s what our Kanban board looked like:

![image](/sysadmin/assets/images/kanban.jpg)

In the first week or so, we made some subtle changes – first we renamed backlog to task pool, and made that area much bigger than I’d originally allowed.

Secondly, we also added a “not ready” section at the bottom of the task pool area. This is for tasks that are blocked but not yet started – for example, a task might be to install software on a server, but I’m still waiting for the server networking to be configured, so I can’t start that yet.

This worked fine for us, and we didn’t make any further changes. Initially, the board was used a lot, but after about a month or so everyone started falling back to their own spreadsheets, checklists, notebooks etc. and not really updating the board. That is very frustrating, I’ve constantly struggled with reporting compliance throughout my time in this role.

We started by doing daily standups, but I found not much was happening in them, so I stopped them after about a week & had ad-hoc discussions with individuals as required. I believe stopping these meetings hurt compliance. I was motivated by allowing everyone to push their status to the board, and my managers and myself could check over that as required – getting out of people’s way by reducing the number of meetings they required. That only works if the push happens! I’ve often tried to think – what does the reporter get out of using system X? What justification can I give as a good motivation for them? Unfortunately, the motivation for a lot of this is reporting and forecasting effort for headcount so the benefits are entirely for the consumer.

I expected to find a couple of bottlenecks – after all, this is what kanban is all about. But mostly, everyone kept their work in progress down. You can see on the board, someone has four tasks on the go. Given the kind of tasks we do, this can be a reasonable amount.

There are a couple of reasons why I believe we didn’t find any blockers. One is that the world changed for the two individuals who were the blockages before – one got very ill, so hasn’t been in much this year. The other got put on a major project, so we hired additional resources to assist with their responsibilities and this helped reduce the backlog.

Additionally, it’s become clear to me that we are in no way a team who can pick up each others tasks. The technology components we work with are too different – Windows, Linux and Storage. Perhaps the only crossover is that we all have to co-ordinate activities for system provisioning – hardware installation, networking etc. But in general we have a bunch of individuals with individual streams of work. So what we’re looking at on the board is a number of todo lists for a component of a system – it’s in no way giving a view of the system as a whole.

My time in this role is finishing in a few weeks. Since the company wants this information to be stored in electronic tools, I wrapped up the board last week and asked everyone to move their tasks back into JIRA. The experienment is over.

Of course, I did this first to lead the way – and instantly realised how much I disliked JIRA. I found it very hard to look at my tasks and answer “what am i doing now?” “whats in my task pool?” – so I immediately had to configure Greenhopper, Altassian’s Kanban tool, to create a new personal Kanban board! As soon as I had that configured, a bunch of people were over my shoulder saying “I like that, can I have that too?” – including members of other teams.

So my experience is that I really like displaying a backlog and work in progress queue, and physically moving tasks between statuses. However, as a workflow analysis tool and to improve status reporting, the experiment wasn’t particularly successful.

