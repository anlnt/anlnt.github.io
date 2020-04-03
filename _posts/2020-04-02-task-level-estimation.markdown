---
layout: post
title:  "Task-level estimation"
date:   2020-04-02 23:19:46 +0700
tag: [Software Estimation]
---
In the previous [post](/2020/03/28/what-is-software-estimation.html), I shared why business people often ask us to give an estimate and some misunderstandings in relation to software estimation. Today I am going to tell you some basic techniques I have used to estimate a task. These techniques are suitable for tasks that do not take more than two weeks for a team of four or five developers. More importantly, we expect these estimates to be as accurate as possible.

When you start to work on a task, someone, probably your team lead or stakeholder, asks you how long the task is going to take. If you have a **precedent** of the work you are about to do, estimation should be easy. For example, you did implement a survey feature where a user can submit two types of questions including free-text and multiple choice with a single answer. If the stakeholder asks you how long you need to add a new type of question, multiple choice with multiple answers, without thinking too much, you can make up a list of required sub-tasks. Even better, you can predict a reasonable amount of time needed to complete each sub-task.

Obviously, estimation based on precedent is never a problem. However, too often we have to add a feature for which we don’t have any precedent. For instance, to implement the new feature, we have to work on a microservice owned by another team, which we have never touched. Even harder, the changes we are about to make will be placed in legacy modules where the recent changes were several years ago, the authors have gone, code was written without unit tests, 3rd party libraries or code conventions are outdated. Some people may make a guess on how long something would take in these systems by using their experiences in prior projects. High chance that their assumptions will turn out to be wrong. If we haven’t touched a software engineering system, we usually don’t know what we don’t know there. I attach a chart that Steve McConnell used to show the correlation between guessing and the estimation error as follows:

<img src="/assets/images/guessing-and-error-20200402.png" alt="guessing-and-error" width="500">

So, my advice is not to guess. Instead, spend dedicated time to do an **investigation** on the system we are about to change. Specifically, explore core features in the system as a user. If there is a feature that is similar to what we are going to build, try it. Understand the data flow in the features. Figure out what users enter into the UI, what are submitted to servers, what are read from or written to database systems, and what are returned to clients. Learn related features because the change you will make may cause them to be changed too for consistency. You may need to dig deeper those features and the entire system for components which you can reuse to implement the new features.

When you have done the investigation and you feel that you have gained a sufficient understanding of all pieces of code you need to touch to implement the new features, the next step is to **break features into individual tasks** needed to complete, each of which will be given an estimate in hours. You will find that the estimate which is resulted in summing from individual tasks is far more accurate than that being derived from the big one. Besides, the smaller a task is, the easier the estimation is. I don’t have a formal approach to give an estimate to an individual task. I almost use my experiences from prior projects. If it is the first time I touch a system, I expect that my estimation is less accurate. However, each individual task is small enough that the estimation error will not be too big. After I make several deliveries to the system, my estimation becomes more accurate because I get familiar with data models, system design and architect, 3rd party libraries as well as tech debts in the system.

Finally, I strongly believe that **breaking a task down** and giving each an accurate estimate is a crucial skill an effective software engineer should obtain. It’s not easy at all. You need years of experiences together with patience and attention to detail. In the first few attempts, you may get a mess. You may have a task that you don’t need. Or you may miss a task that you do need. You may be an underestimator or overestimator. Don’t give up. You will find it incredible once you acquire this skill.

# References

- [Agile Estimating and Planning](https://www.amazon.com/Agile-Estimating-Planning-Mike-Cohn/dp/0131479415)
- [Software Estimation: Demystifying the Black Art](https://www.amazon.com/Software-Estimation-Demystifying-Developer-Practices/dp/0735605351)
- [The Clean Coder](https://www.amazon.com/Clean-Coder-Conduct-Professional-Programmers/dp/0137081073), Chapter 10 Estimation
