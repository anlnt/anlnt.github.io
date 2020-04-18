---
layout: post
title:  "When a software starts to decay"
date:   2020-04-09 15:49:46 +0700
tag: [Software Craftsmanship]
---
Have you ever found yourself in a situation where you couldn’t add additional logic to a module for implementing a new feature in a software project? Specifically, there is an API that is extremely slow. The new feature requires you to add more database queries but you know that it only makes the performance issue worse. You start to dig deeper into the API, investigating why it is slow. You then know the root cause but unfortunately you cannot make any changes to improve the performance because the current system design makes the module too hard to modify. Ultimately, you have to rewrite the entire API so that it is easier to change e.g. optimizing database queries or adding new logic. What if we keep adding new logic without improving the API design?

- The API becomes slower and slower. You may be woken up early morning because a customer is angry, waiting a page for more than ten seconds to show up. Even worse, the customer decides to leave your product due to the bad experience.
- The current design gets more complicated. You will be slower the next time you add additional logic. Moreover, when a new member maintains this API, it is easy to introduce a bug because it is too hard to fully understand the API.
- The most interesting thing is when someone sees a bad design existing for a long time, becoming a burden for the team, they tend to think that nothing can be fixed and no one cares. Then do not manage to keep the system clean, being easy to understand and extend. In addition, like a virus, this negative thought spreads across the team. As a result, the system starts being destroyed. This phenomenon is mentioned as “A broken window” in the book [The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-special-David-Thomas/dp/0135957052/).

Scientists in the field of crime and urban decay have found that the fastest way to turn a clean, tidy, intact, and occupied apartment to a dirty, damaged and abandoned one is a broken window. When an individual notices a window broken for ages, without any repairs, they get a sense of abandonment. They assume that the management does not care about the building. Trashes are dropped all over the place. No one bothers to recover damaged walls or floors. As the time goes on, another window is broken and other parts of the building get ruined. As I mentioned before, this negative thought and behavior spread across inhabitants in the building, making it destroyed dramatically beyond the owner’s ability to fix it.

So how do we deal with broken windows? We all want our building clean and intact so any broken windows or damages need fixing as soon as they are discovered. However, in real software projects, we can’t. We are always under pressure to deliver more features as quickly as possible. In my opinion, the following is what we can do:
- Do not add more broken windows although it’s hard to resist the temptation to add junk code or hack the current system for a quick delivery.
- Keep improving existing system designs along the way developing features. For example, you may change the current design so that it fits the new features before implementing. Don’t build things upon a bad design to avoid tech debts. There is always an interest rate you have to pay on the debt. Compounding interest kicks in if you don’t get out of the debt soon. Be careful or you go bankrupt.
- If you have to choose “do it quick” over “do it right”, commit yourself to fix it as soon as it’s delivered.
- Learn [Code Refactoring](https://en.wikipedia.org/wiki/Code_refactoring) which comprises principles and methods to improve existing system designs.

# References

- [The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-special-David-Thomas/dp/0135957052/)
- [Refactoring: Ruby Edition](https://www.amazon.com/Refactoring-Ruby-Addison-Wesley-Professional/dp/0321984137)
- [Refactoring to Patterns](https://www.amazon.com/Refactoring-Patterns-Joshua-Kerievsky/dp/0321213351)
- [97 Things Every Programmer Should Know](https://www.amazon.com/Things-Every-Programmer-Should-Know/dp/0596809484), Act with Prudence
