---
layout: post
title:  "Unit test: back to basics"
date:   2020-04-18 11:35:46 +0700
tag: [Software Testing]
---
## What is Unit Testing?
When we first learned programming, we may have practiced writing a method that calculates the sum of two numbers. The function written in Ruby programming language would be as follows:

```ruby
def sum(a, b)
  a + b
end
```

Then we may have used a tool, [IRB](https://github.com/ruby/irb), to interactively exercise the method to see if it worked the way we think it should.

```bash
➜  ~ irb
2.4.6 :001 > def sum(a, b)
2.4.6 :002?>     a + b
2.4.6 :003?>   end
 => :sum
2.4.6 :004 > sum(5, 10)
 => 15
```

I call the above testing a unit test. To be more accurate, it is a manual unit test. A unit test is performed to prove that a unit, probably a method or a class, does what the developer thinks it should do. By “manual”, I mean we have to look at the output from the shell to decide if the method works the way we expect. There is a better way to perform a unit test, automated unit testing. We are going to talk about it later.

## Coding with confidence
Programming is all about writing code to solve a problem. Someone may start with a big problem, developing class to class, method to method until they feel that their job has been done. They start a verification of all this code by using the top-level program which may be an end-user feature. They are usually surprised that the feature does not work the way they are expecting but have no idea what is going on. They spend a lot of time using a debugger, going back and forth to figure out where the bug is. They are sometimes reported a bug right after they deliver something and it turns out that it is just a syntax error.

On the other hand, there is a school of programming where the developer decomposes a big problem into many small ones each of which can be resolved by implementing a method or a class, which is considered as a unit as I mentioned above. For each unit they implement, they do full unit tests to make sure that the unit does what it is supposed to do. They refuse to move on until the unit they are working on can prove itself. Imagine that software development is similar to build a house of cards, units, where a higher card relies on several lower ones. If one little nudge at the bottom, the whole thing collapses.

<img src="/assets/images/house_of_cards_20200418.jpg" alt="house_of_cards" width="300">

No matter which between top-down and bottom-up approach chosen to develop a program, a developer who strongly believes in unit testing will not move on to the next level until all units in the current level have been tested. Thanks to this discipline, they are able to deliver bug-free features in a sustainable space.

## Regression testing
Have you ever seen that a developer has just delivered something and someone tells him that he has broken another module which seems unrelated to the work he has done? It happens a lot in the field of software development and that is one of the reasons why building software is hard, risky, and time-consuming. Ideally, when you change a unit, in addition to test the unit itself, you have to test all higher level units that are relying on the one you are changing. You may say that if you spend too much time testing, you will miss certain schedules and deadlines. Good point! Automate your unit tests.

## Automated unit testing
An automated unit test is a piece of code that tests a unit. Continue with the example at the beginning of the post, we have an automated unit test as follows:

```ruby
describe 'sum' do
  it do
    expect(sum(5, 10)).to eq(15)
  end
end
```

It’s easy to run the unit test without human interaction. For example, we can put the test in a file named `sum_spec.rb` and run it simply by the following command:

```bash
➜  ~ rspec sum_spec.rb
```

There is a test report after testing is done. If the testing does not have any failures, we get the following report:

```bash
sum
  should eq 15

Finished in 0.66649 seconds (files took 4.99 seconds to load)
1 example, 0 failures
```

If somehow the method does not do what we mean, the test report will tell us.

```bash
sum
  should eq 15 (FAILED - 1)

Failures:

sum should eq 15
    Failure/Error: expect(sum(5, 10)).to eq(15)
       expected: 15
       got: 14

Finished in 0.94319 seconds (files took 5.1 seconds to load)
1 example, 1 failure

```

## Benefits of automated unit testing
- Regression testing becomes machinery work. When you change a unit, you can run the entire test suite to confirm that you don’t break anything else.
- Encourage refactoring. Refactoring means that we change the existing code structure to make it easy to understand and extend, without affecting its behavior. How do we know we don’t accidentally change the current behavior? Unit tests again.

I have just mentioned two major benefits of unit testing that keep a software project developed sustainably in the long run. There are a lot more, especially once you master it.

## Software engineers and unit testing
Persuading someone is hard. Persuading a software engineer is harder. Persuading a software engineer to write unit tests is much harder. I used to develop softwares without writing unit tests in the first five years of my career and I understand how difficult it is. Employing unit testing makes our life better. Anyone agrees with this, in the same way those who agree that eating more vegetables and exercising regularly are vital for a healthy life. That doesn’t mean they actually do these things, however. I think it is because of what we think of unit testing. Unit testing is a methodology for programming. It’s the ability to deliver reliable code piece by piece, slowly but precisely, with a confidence that we don’t break unrelated areas. Once a piece of code is delivered, it’s safe for other higher-level code to use it. An alternative is pumping out a bunch of code containing a lot of assumptions, hard to determine what’s working and what’s not.

# References

- [Pragmatic Unit Testing in Java with JUnit](https://www.amazon.com/Pragmatic-Unit-Testing-Java-JUnit/dp/0974514012)
- [Developer Testing: Building Quality into Software](https://www.amazon.com/Developer-Testing-Building-Addison-Wesley-Signature/dp/0134291069)
- [The Clean Coder](https://www.amazon.com/Clean-Coder-Conduct-Professional-Programmers/dp/0137081073), Chapter 1 Professionalism
