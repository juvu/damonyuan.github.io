---
title:  "Another Interview Experience"
description: "Another Interview Experience"
date: 2019-09-20 15:04:23
hidden: true
categories: [Tech]
tags: [Interview Others]
---

> * Author: [Damon Yuan](https://www.damonyuan.com)
> * Date: 2019-09-20

It is a good experience for a technical discussion / interview, just to mark it down :)

## Q: What are the factors when you design a system?

 - Security
 - Scalability
 - Extensibility
 - Performance
 - Affordability
 - Reliability (Hm... I forgot it... how come... this is the part the CI/CD will contribute to.)

## Q: Do we really need to draw the system diagram for each feature requests?

  The answer at the moment was that it is better to have the diagram drawn every time before the implementation... 
  
  I think the better answer should be: it depends on the nature of the project. If the project is an one-off project and will be throw away once used, and will never be shared to other team members, then it is fine to have no docs/diagrams prepared for the feature. While if it is going to be shared to others or if it is going to grow up with more features with better quality, then it is every important to have documentation about it.
  
  Remember there is a movie of which the name is "Lucy", it says that it's up to us to push the rules and laws, and go from evolution, to revolution by accumulating and passing the knowledge through time. Maybe it is a bit exaggerate in this case, however for a team, it is every important to pass and share the knowledge around.
  
  Finally the PlanetUML should hire me as their salesman... I marketed it for them freely again... (http://plantuml.com/)

## Q: Pixel Boot?

Hm... what's that? Similar to Android boot flow? Definitely a TODO...

## Q: The most recent security issues you have read ...

Hm... the hacker take the control of whole kubernetes cluster by some means? ... and Linux something? ... Sorry my bad memory...

## Q: How to fix a bug ... blablabla

First of all, prepare a checklist for all the possible failure points...

Hm... logging system ... no logging system / broken? ssh into the host and check the logs ... 

Excessive authorization? and no API gateway / Nginx / HAProxy? no those components in the structure ... then... maybe iptable rules to block the IP? hm... no root access? ... ... ... .... maybe disable the account?

correct. :)

## Q: Why to use Frameworks?

From my point of view, frameworks are just templates that make the pattern of the solution for a typical problem well understood by the majority of the programmers. 

Shell script can be created based on a template so that we don't need to go into every line of the source code for some boilerplate parts; web framework can be created based on a framework/template so that all the web developers can understand the background rationale of each components of the source code, also preventing repeat ourselves in creating boilerplate code. 

Some Business requires less frameworks to be involved because they might include a lot of code not required by the typical business, therefore will introduce some risks especially when the the framework is not fully grasped by the developer. While we can still borrow the ideas from the framework when we are implementing the features from scratch.

## Q: Why the release cycle for the mobile team cannot achieve the target like 2000 times per month?

It is decided by the nature of the project and the ability of the team. The project is mobile and by default it will require Apple & Google's review before publishing and it is not as easy to be rollback as those backend service or web application. 

And to achieve the real Agile everyone inside the team will be required to understand how TDD / BDD works and the team need to use TDD / BDD to verify the result of a feature implementation. Also the coverage rate of the project should be high enough to ensure the releasing won't have any regression issues and impact the production users.

