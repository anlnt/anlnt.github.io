---
layout: post
title:  "Tracer Bullet Development"
date:   2021-05-23 09:11:24 +0700
tag: [Software Craftsmanship]
---

Assuming that we are taking part in a shooting game, before taking a shot, we tend to aim at the target as precisely as possible, then shoot and hope. We usually apply the same approach in software development. Specifically, when a project starts, we expect product owners to tell us exactly what requirements are. We then design all the database schema and data models which we assume we need to implement for the project. Next, we divide the requirements to modules which are coded in a vacuum. Modules are combined into higher level models which are further combined until we have an application as a whole to be presented to users and tested. You know what? Projects developed this way usually end up with schedule overrun and working overtime.

An alternative to develop software is Tracer Bullet Development, which is mentioned in the book, [The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-journey-mastery-Anniversary/dp/0135957052). Have a look at the following diagram.

<img src="/assets/images/tracer-bullet-devlopment.png" alt="tracer-bullet-devlopment" width="600">

*(Thomas, David; Hunt, Andrew. The Pragmatic Programmer . Pearson Education. Kindle Edition.)*

This methodology encourages us to deliver features by features which may be incomplete. However, the feature takes through all architectural layers of the system. The most critical features should be selected to build first. Besides, leave the uncertainty and less important details to deal with later. This approach has several advantages I have experienced myself:

**We can get immediate feedback**

We usually complain that requirements keep changing. In fact, that is the nature of software development. Because the customers have never seen the system which is about to be built, their requirements may be vague. Therefore, show them new small working features frequently to seek for feedback. They will tell us what needs changing or adding. That’s the point of tracing bullets. We fire a bullet. If it hits the target, that’s perfect. Otherwise, we adjust our aim until we hit the target.

**The project has a code structure to work in**

At the very beginning of the project, the progress is low. Members in the development team are not sure where to start, not to mention that it’s easy to conflict with others' work. If someone has fired a tracing bullet, achieving an end-to-end connection among the architectural layers of the system, and has merged their code, other teammates will easily start from this overall application for other features in parallel.

**Continuous integration**

Because we deliver code frequently, our pull requests are small, easy to review and test. There are no pull requests that contain giant blocks of code that are delivered on a weekly basis. The problem with big pull requests is that they are hard to do code reviews and tests are usually missing. If there are bugs after the pull requests are deployed, debugging cannot be fast.

**We always have a demonstrable product**

Business people are investing in you to build their products. They are always excited to see if you are progressing. However, they are not interested in how many lines of codes you have written. What they want to see is a working feature. It can be something immature but the point is they see some visible progress toward their products.


# References

- [The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-journey-mastery-Anniversary/dp/0135957052), Topic 12 - Tracer Bullets
