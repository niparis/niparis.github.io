---
title: "Product Engineering Teams - Principles"
date: 2021-01-05T23:06:55+08:00
draft: false
ShowToc: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true  
categories: ["product"]

cover:
    image: "images/test.png" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
---

Organising software teams effectively to build products is tough. I strive to create **empowered, autonomous product engineering teams**. This way to organize product teams is used by many successful product startups and is extremely effective, though pretty different from the way software teams are led in most places. Here's how it has worked for me.

<!--more-->

A product is built by one or several **product engineering teams**, each of them responsible for a set of features or services. A **product leadership team** defines the vision of the product, shapes the feature to be developed and prioritize them.

A typical product engineering team is made of 3-7 people. The central principle is to give **autonomy** to each of those teams. 

At its core, an **autonomous product engineering team** is a team that has all the resources necessary to deliver a **working feature in production, and maintain it**. This means a diverse skillset: backend, frontend, devops, testing, etc. - in some companies non-technical roles can even be involved in the team, such as TransferWise which often includes legal in their product teams. Each team has a clear lead, who should be able to identify what skillset is necessary for the team to be able to reach its goal.

For each principle I’ve also highlighted an opposite principle : as it’s easiest to know what Good is if you know what Evil is, it is easier to know what these principles stand for if you also know what they stand against.

These principles are coming from a variety of sources: product companies who have found success and individuals who helped them. You’ll find some links at the bottom. 

### I. Autonomy (vs Handoff)
Autonomy means **removing any dependencies and reliance on shared resources or central teams**. It means moving by yourself without waiting for  authorization, it means being assessed on results and not on how (process) or how many (output).

In practice, autonomy goes hand in hand with independence: the team is given **all the resources it needs to reach its goal, so that it doesn't depend on other teams to reach it.**

Each team decides which tools it uses, which language is best for the software it develops - within the constraints setup by Engineering.

There should never be a case where a team "hands off" something to another team - hands off is where responsibility is destroyed.

To exist meaningfully, the product engineering team must make good use of the autonomy they are provided with by showing their impact.

### II. Impact (vs Velocity)
Speed doesn't matter if we're not going in the right direction. Effort without results is pure pain. To counteract this, product engineering teams are measured on **impact**, which is a measure or metric that is **perceived by the users**.

Those client facing KPIs need to all be based on **actions that the team can directly impact** - there needs to be a clear line of causality between the KPI and the feature set the team is responsible for. They should be reviewed on a quarterly basis - enough time for the team to implement a plan and see initial results, without being too inflexible.

Note that implicitly, this means that teams are expected to share concerns if they are asked to implement features that do not help their KPIs.

### III. People (vs Process)
Probably the most important point of the agile manifesto (which you should read if you haven’t - a one minute read ==> https://agilemanifesto.org) - the principle is well known, but it is important as processes tend to creep it everywhere.

It means that everyone is aligned and **working towards goals**, so that they can by themselves prioritize and make decisions, rather than letting a tool or a process decide for them.

### IV. Direct contact with users and clients  (vs only business should be talking to clients)
Feature teams should have frequent contact with users, at all stages of the relationship (pre sales, post sales, support). 

There are several goals to this principles: humanizing the various user personas - which will help create the emontional connection needed to empathize with the users and create features that solves their problems. There's also the aspect of seeing how clients reacts to the projects, and to not be shielded from user disappointments.

This repeated contact with users helps the team implement features in a way that will make them best by their intended users.

### V. Cross Pollination (vs Standards)

![Example image](https://imgs.xkcd.com/comics/standards_2x.png#center)
*[XKCD on standards](https://xkcd.com/927/)*

Rather than codifying best practices into standards (and make sure we stop evolving and create cargo cults), each team can adopt or create the best practices that fits their way of working. Teams should share the best practices they are using if they think it could benefit the rest of the organization.



Best practices adopted by a team can be challenged by other leaders, but ultimately the product engineering team owns their decisions.

Note that this principle is not absolute, and some high level standards will be setup by the engineering leadership.

### VI. Weak code ownership (vs Nobody touches my code !)
If a product engineering team uses a code base maintained by a different team, they should never feel blocked should they need to fix a bug or add a feature. 

If the team owning the feature does not have time to implement that feature or fix that bug, the team needing it should be free to implement it, by writing the code and raising a Pull Request, which of course will be reviewed by the team owning the feature.

In that way, a team controlling a critical service is never perceived as a blocker (demands for changes tends to come in bulk), and can not use the importance of their service for political purposes.

Weak code ownership is necessary to make autonomy work. 

### VII. Blameless post mortem (vs finding who's guilty)
Surfacing problems as fast as possible is critical to avoid buildups leading to massive failures. How do we achieve that ? 

Regular post mortems giving the opportunity to present and discuss issues, where participants have the confidence that no blame will be assigned, and that the only focus will be to find and implement a solution.

### VIII. Own your code in production (vs Ops and QA got your back )
This is implied by the first principle on autonomy, but it's important enough to be explicitly called out: the autonomy implies that the product engineering team fully owns their code in production.

Yes, it means that in addition of owning the release cycle, and the setup and maintenance of the infrastructure, the team is also on pager duty should anything require their immediate attention.

The fact that you are on call fundamentally changes the relationship has with code: performance discussions become much more focused and less abstract, and tasks often perceived as chores (such as unit testing, or IaC) become life vests.

 

## Sources and inspirations - in order
- Personal experience and mentors
- [Agile Manifesto](https://agilemanifesto.org)
- [Marty Cagan & SVPG](https://svpg.com/articles/), and his book [Inspired](https://svpg.com/inspired-how-to-create-products-customers-love/)
- [Shapeup](https://basecamp.com/shapeup) by BaseCamp
- [Scrum](https://www.amazon.com/Scrum-Doing-Twice-Work-Half/dp/038534645X) by Jeff Sutherland 
- [Transferwise: Product Engineering Principles](https://tech.transferwise.com/product-engineering-principles-transferwise/)
- Spotify on Product Engineering: [Part1](https://blog.crisp.se/2014/03/27/henrikkniberg/spotify-engineering-culture-part-1), [Part2](https://blog.crisp.se/2014/03/27/henrikkniberg/spotify-engineering-culture-part-2)
- [Weaknesses in the Spotify model](https://www.jeremiahlee.com/posts/failed-squad-goals/)

#### Revisions

v1.2 - July 18th, 2021 - Minor edits
v1.1 - Jan 5th, 2021
