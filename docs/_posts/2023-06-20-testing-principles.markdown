---
layout: post
title:  "Testing principles"
date:   2023-06-20 12:37:00 +0100
categories: testing
---
In [Part #1](https://tamastokes.github.io/testing/2023/06/19/who-should-be-responsible-for-software-quality.html) I tried to show the consequences of the setup where a separate testing team tries to take responsibility for code quality, i.e. holding the mandate of being a quality gate.  But if not quality gate, then what?

## Why we test

Do you remember COVID-tests?  What did we use them for?  In my opinion, we used COVID testing to collect information to reduce our uncertainty before making global (whether to lock down or not) or local (whether to visit my grandparents) decision making.

(Note how ridiculous it would have been if the people creating or executing the COVID tests had made such decisions.  We expect that governments make decisions on lock-downs, whereas we decide going to or avoid crowdy areas if there's no lock-down.)

**Principle #1: The purpose of testing is to provide more information on how buggy our code is to help global and local decision making by reducing our uncertainty.**

**Principle #2: Not the testers but the developers should be held accountable for the quality of the code they commit.**

**Principle #3: The manager having all necessary information about risks, costs, business expectations, etc. should be accountable for collecting the adequate level of information before any release-related decision.**


## The testing pyramid

We like end-to-end tests because they can reduce our uncertainty whether the code works as expected the most, but here's a trade-off:
* Some scenarios are difficult to trigger in an end-to-end test, e.g. testing how my code reacts if a database operation deadlocks.
* If the test fails, it usually takes a lot of time to localize the bug, sometimes even to figure out if it was a false or true positive.
* Combinatorial boom of edge cases.  Say, you have 5 components with 5 edge cases each.  You'll natuarally write 5 * 5 = 25 unit tests for them.  But if you want to cover each combination with end-to-end tests, then the number of test cases will be 5^5=3125.
* The execution time of an end-to-end test case can be order of magnitudes slower than that of a unit test, as an entire environment needs to be brought up and down for each test case.

**Principle #4: a reasonable compromise to resolve the trade-offs around end-to-end testing is the testing pyramid: write zillions of unit tests, fewer integration tests, and even fewer end-to-end tests, typically only for the happy paths.**

Why are still so many teams end up with a so large but intolerably slow (and often unsustainable) set of end-to-end tests?  Because in a setup with a separate test team (with a quality gate mandate) it's typically the testers who write the tests, and -- as they aren't allowed close to the code base -- the only type of tests they can write is end-to-end tests.  Plus, as the developers don't feel themselves responsible for the code quaility, they tend to neglect writing the adequate number of unit tests.

**Principle #5: Most of the tests should be written by the developers.**


## Team structure
Separate testing teams inevitably lead to hand-overs (instead of cooperation), which in turn lead to longer feedback loops.  Fixing a bug committed 2 months ago can easily be order of magnitutes more costly than fixing a bug you committed yesterday, due to the overhead of resetting your development environment accordingly, and figuring out what was in your mind back then. 

**Principle #6: Set up a team structure that promotes shorter cycle times and cooperation over hand-overs**

I see these options as follows:
1. No testers at all.  This option sounds too risky for most managers despite the vast amount of evidence that it works without issue.  In most cases they'll use the "Our use case is more complex" argument.
2. Testers are integrated into the dev teams with a developer-tester ratio that makes it impossible for developers to not deal with testing.  If incentives are set right (short cycle times and taking responsibility for bugs), developers and testers will quickly learn how to cooperate on a daily basis and from early stages of user stories.
3. Some very experienced testers form a so called Enabling Team (referring to the concept described in the Team Topologies book).  All testing activity still happens in the dev teams, but if they run in to a problem that requires deeper expertise, a tester from the Enabling Team temporarily joins them (to give advise and walk them through the solution, not to actually do the work).


## How much testing?

More information reduces uncertainty, hence usually leads to better decisions.  However, collecting more information is costly (not only money-wise but also time-wise).  Also, I think it's a fair assumption that the cost-information curve is non-linear.  Assuming a diminishing return, it becomes an optimisation problem.  More on that in Part #3.
