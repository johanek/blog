---
layout: post
title: "puppet modules"
date: 2013-01-17 22:10
comments: true
tags: [puppet, configuration management]
published: false
---

This week I went to the #ldndevops meetup, where sam and bicho gave an interesting talk about their experience of deploying chef on a non trivially sized estate.

There was a ton of good stuff in there, but one of the things that got me thinking most was their view that community chef cookbooks are naive and they had to create their own standards and write most of the modules themselves.

This completely aligns with my experience of using puppet modules from the forge. The sales pitch is 'get a head start with 600 modules from the forge', but in my experience only a very few modules work out of the box. Some may only require minor changes, others may need refactoring to match the standards you require. Moving down the chain, there are some you can only copy patterns from when you write your own module and unfortunately others which you need to disregard.

It's a problem that you need to look at the module's code - and thus need to be able to read the code - to work out if it's usable. 

Usually if I'm downloading code, either an application or a ruby gem or whatever, I'm looking at the features and API. It's a sad indictment of the state of most modules that we're no where near that.


## Dilemmas ##

There's a couple of quite different scenarios for wanting to use a puppet module, and those different needs cause some of these issues.

Sometimes, you want to bootstrap quickly. I want to grab the module and get something working with the minimum amount of effort on my behalf - that' satisfying dependencies and making config decisions. To make this scenario work, the module is going to have to be quite opinionated about how to do things. 

The other use case is you want a very generic module that exposes all the necessary controls to configure the software according to the requirements of the environment.

This argument comes up a lot with regards to package management. Many sysadmins dislike the post install scripts that are supplied with packages because they do things the admin wants to control using configuration management. But the packager is thinking about getting something working out of the box.

~~~~~

OK, now I'm thinking about base, and role modules
http://sysadvent.blogspot.co.uk/2012/12/day-13-configuration-management-as-legos.html



~~~~~

- Get started quickly vs provide something more customisable/parameter driven for advanced users
- Packaging, conflicts with other modules, where to install from


Mantras:

- Data Seperation: Configuration data defined outside the module
- Reusability: Customise the behaviour without changing the code
- Standardisation: Style guide, coherent predicatable interface
- Interoperability: Limit dependencies, be self contained
- Cross OS Support: Easy to add a new OS.
