---
layout: post
title: "Operability Day Two"
date: 2015-09-25 09:31
comments: true
tags: [operations, conferences]
---

[Day one is available here](http://johan.org.uk/sysadmin/blog/2015/09/24/operability-day-one/)

## Charity Majors, Parse/Facebook - Building a world class ops team

[Slides](http://johan.org.uk/sysadmin/blog/2015/09/24/operability-day-one/)

This was a talk focusing on bootstrapping an ops team for startups.

**Do you need an ops team?**

Ops engineering at scale is a specialised skillset. is is not someone to do all the annoying parts of the running systems. Or do you need software engineers to get better at ops?

You need an ops team if you have hard problems:

- extreme reliability
- extreme scalability (3x-10x year over year)
- extreme security
- solving operational problems for the whole internet

**What makes a good startup ops hire?**

Its not possible to hire people who are good at everything - unicorns. What you can get are engineers who are good at some things, bad at others. People who can learn on the fly are valuable.

"A good operations engineer is broadly literate and can go deep on at least one or two areas"

Great ops engineers:

- strong automation instincts
- ownership over their systems
- strong opinions, weakly held
- simplify 
- excellent communication skills, calm in a crisis
- value process (as that is what stops you making the same mistakes over again)
- empathy

Things that aren't good indicators:

- whiteboarding code
- any particular technology or language
- any particular degree
- big company pedigree

Succeeds at a big company:

- structured roadmap
- execute well on small coherent slices
- classical cs backgrounds
- value cleanliness & correctness
- technical depth

Succeeds at startup:

- comfortable with chaos
- knows when to solve 80% and move on
- total responsibility for outcomes
- good judgement
- highly reactive
- technical breadth


**How do you interview and sort for these qualities?**

Don't hire for lack of weaknesses. Figure out what strengths you really need and hire for those.

Good questions:

- leading and broad, probe the candidates self reported strengths
- related to your real problems
- ask culture questions, screen for learned helplessness

Bad questions:

- depend on a specific technology
- designed to trip then up, looking for a reason to say no
- deny candidates the resources they would use to solve something in the real world

**You hired an ops engineer, now what?**

How to spot a bad ops enginner:

- tweaking indefinitely and pointlessly
- walling off production from developers
- adding complexity
- won't admit they don't know things
- disconnected from customer experience

How to lose good ops engineers:

- all the responsibility, none of the authority
- all the tedious shitwork
- blameful culture
- no interesting operational problems

## [David Mytton](https://twitter.com/davidmytton), Server Density - Human Ops - Scaling teams and handling incidents

[Slides](http://www.slideshare.net/serverdensity/scaling-humans-ops-teams-and-incident-management)
 
This talk covered how incidents are handled at Server Density.

We should expect downtime - prepare, respond, postmortem.

**Prepare**

Things that need to be in place before an incident

- on call schedue with primary & secondary
- off call - 24hr recovery after overnight incident
- docs, and must be located independently from primary infrastructure
- key info must be available: team contacts, vendor contacts, credentials
- plan for unexpected situations: loss of communication, loss of internet access
- use war games to practise for incidents

**Respond**

Process to follow during an incident:

- First responder
  - load incident response checklist
  - log into ops war room
  - log incident in jira
- Follow Checklist(s)
  - due to complexity
  - easy to follow in times of stress and fatigue
  - take a beginners mind - ego can get in the way, don't wing it
- Key Principles
  - log everything (all commands run, by who and where and what the result was)
  - communicate frequently
  - gather the whole team for major incidents

**Postmortem**

- Do within a few days
- Tell the story of what happened - from your logs
- Cover the appropriate technical detail
- What failed, and why? How is it going to be fixed?

## [Emma Jane Hogbin Westby](https://twitter.com/emmajanehw), Trillium Consultancy - Emphatically Empathetic

Emma talked about how she taught herself to be more empathetic.

Normal people have a lack of empathy, it's a skill that can be practised and learned.

What is empathy: ability to understand the feelings of another

**Level 1: Care just enough to learn about a person's life**

Doing this improves team cohesion, but requires a time investment.

Collect stories - learn about people by asking them questions. Shut up and listen. Respond in a way to encourage more info gathering.

Later, refer back to stories and follow up for more information.

**Level 2: Strategies to structure interactions**

Doing this you can engineer successful outcomes, and improve capacity for diverse thinking. But you risk being perceived as manipulative.

It's a mistake to believe there is only one way to have a connection. Try to uncover motivation, why do people behave the way they do?

There are three types of thinking strategies, and you'll see language patterns that match each of them.

**creative thinking**: 'can we try...' 'what about...

**understanding thinking**: 'so what you're saying is...' 'just to clarify...'

**decision thinking**: 'im ready to move on to...' 'last time we tried this...'

How can you create outcome based interactions for these sort of people? Perhaps you can plan for specific types of discussions in meeting agendas.

Find a system to use with your team to make communications more explicit, and to take advantage of the thinking strategies they use.

**Level 3, engage with work from another's perspective**

This can foster creative problem solving. The risks are it is potentially overwhelming, and can cause doubt for self worth.

Seek to understand - complain about yourself from the other's prespective, or situation. Live your day through the other's constraints.

Thinking process should be no more left to chance than the delivery practise of a skill.

---

There was an interesting question after Emma's talk - "How do I make Bob care about Dave from another team". Her suggestion was to create a situation where they can bond over a common enemy - i.e. say something you know to be untrue and that they would both respond to in a similar way.

## [Scott Klein](https://twitter.com/scootklein) statuspage.io - Effective Incident Communication

Remember that there is someone on the other end of our incidents who is affected personally.

The talk covered what to do before, during and after an incident. You need a dedicate place to communicate system status to your users.

**Before**

Get a status page. It needs the following:

- timestamps
- to be very fast, very reliable
- keep away from primary infrastructure, even DNS
- contact info - give a way to get in touch

**During**

- communicate early. say you are investigating - it means 'we have no clue but at least we're not asleep'
- communicate often. always communicate when the next update is.
- communicate precisely: be very declarative
  - don't do etas, they will disappoint people
  - don't speculate, 'were still tracking down the cause'
  - 'verification of the fix is underway' not 'we think we fixed it'
- communicate together. have pre-written templates.
- one person needs to be assigned as incident communicator

**After**

- apologise first
- don't name names
- be personal. "I'm very sorry". Take responsbility.
- details inspire confidence
- close the loop - what we're doing about it


**Why do this?**

- gain trust with users/customers
- turn bad experience into good experience
- service recover paradox - people think more highly of a company if they respond properly.
- show that you do your job well

## [Rich Archbold](https://twitter.com/rich_archbold), Intercom.io - Leading a Team with Values

Talk covered Rich's experience of introducing core values to drive performance of the team. They reduced downtime and infrastructure costs, and number of ops pages.

Enabled autonomy, distributed decision making.

**Problems they were facing:**

- roadmap randomisation. easily distrated from what planned to do.
- projects take a long time and delivered late
- not feeling like a tribe

**Criteria for values:**

- fit with the business
- personal, specific
- aspirational and inspirational
- drive daily decision making
- not dogma - needed to be flexible

**These are the Values they came up with:**

1. Security, Availablilty, Performance, Scalability, Cost - prioritize for maximum impact
2. Faster, Safer, Easier, Shipping
3. Zero Touch Ops
4. Run Less Software

Afterwards they gathered lots of metrics of unplanned work. From this they worked out that they need to multiply estimates by 2.7 to get accurate roadmap planning.

## [Matthew Skelton](https://twitter.com/matthewpskelton), Skeleton Thatcher Consulting - Un-Broken Logging, the foundation of software operability

[Slides](http://www.slideshare.net/SkeltonThatcher/unbroken-logging-operabilityio-2015-matthew-skelton)

The way we use logging is broken, how to make it more awesome

What is logging for? It provides an execution trace.

How is logging usually broken? It's often unloved, discontinuous, contains errors only, bolten on, doesn't have aggregation and search, severeties aren't useful because they need to be determined up front.

Also, logs aren't free. You need to allocate budget and time to make them useful.

Why do we log? For verification, traceability, accountability, and charting the waters.

**How to make logging awesome**

Continuous Event IDs - use to respresent distinct states. Describe what's useful for the team to know and describe that as a seperate state. Use enums.

Transaction tracing - Create uniqueish identifier for each request, as pass it through the layers. 

Decouple Severity - allow configurable severity levels. Log level should not be fixed at compile or build time. Map Event IDs to a severity.

Log aggregation and search tools - As we move from monolith to microserverice, the debugger does not have the full view anymore.
Need an aggregated view of logs across a system. Develop software using log aggregation as a first class thing.

Design for logging - logging is another system component, and needs to be testable.

NTP - Time sync is crucially important for correlating log entries

Referenced the following video:

[Evan Phoenix - Structured Logging](https://www.youtube.com/watch?v=Z-JskKlIBOA)

## [Gareth Rushgrove](https://twitter.com/garethr), Puppet Labs - Taking the Operating System out of operations

[Slides](https://speakerdeck.com/garethr/operations-without-the-operating-system)

The age of the general purpose operating system is over. What does this mean for operators?

Lots of new OSes have appeared in the last year

**New Breed:**

- Atomic (RedHat)
- CoreOS
- Snappy (ubuntu, replace dpkg with contrainers)
- RancherOS (docker all the way down)
- Nano - tiny alternative to Windows Server
- VMWare Bonneville

**Common themes:**

- Cluster native
- RO file systems
- Transactional updates
- Integrated with containers 

**Why the interest in New OSes?**

- Lots of homogeneous workloads
- Security is front page news
- Size as a proxy for complexity
- Utilisation matters at scale
- Increasingly interacting with higher level abstractions anyway

**Unikernels** 

Compile an application down to a kernel, there is no userspace. Only include the capabilities and libraries you need - everything is opt-in.

- Hypervisor/hardware isolation
- Smaller attack surface
- Less running code
- Enforced immutability
- No default remote access

**What happens to operators?**

Hypervisor becomes the "platform".

Everything else as an application. Firewalls. Network Switches. IDS. Remote access.

Everyone not running the hypervisor is an application developer.
Standards required: Platforms, Containers, Monitoring. Publish more schemas than incompatible implementations in code.

Infrastructure *is* code.

Revolution not evolution. Distance between old infrastructure and new will be huge. Models of interaction and the skills required to operate.

**Conclusions:**

We have fundamental problems that date back more than 40 years. It Might take a different evolutionary process to build better infrastructure. We may have to throw away things we care about, such as Linux. This is all driven from security concerns.


## [Ben Hughes](https://twitter.com/benjammingh), Etsy - Security for Non-Unicorns 

[Slides](https://speakerdeck.com/barnbarn/security-for-non-unicorns)

Security is hard. Tiny little bugs turn into giant things.

You're already being probed for security holes, do you want to know or not? Bug Bounties are a way of getting attackers working for you.

You need to prepare a lot for bug bounties. Try and get all the low hanging fruit yourself. The first few weeks will be hell.

With much of our infrastructure in the cloud, it's easy to expose sensitive information, such as credentials, on places like github. [Gitrob](https://github.com/michenriksen/gitrob) helps to analyse git repos for you.

People trust random files off the internet - like docker images, vagrant images, and curl|bash installs etc.





