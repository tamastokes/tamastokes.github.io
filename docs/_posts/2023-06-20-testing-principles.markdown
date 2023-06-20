---
layout: post
title:  "Testing principles"
date:   2023-06-20 12:37:00 +0100
categories: testing
---
In [Part #1](https://tamastokes.github.io/testing/2023/06/19/who-should-be-responsible-for-software-quality.html) I tried to show the consequences of the setup where a separate testing team tries to take responsibility for code quality, i.e. holding the mandate of being a quality gate.  OK, not quality gate, but then what?

Do you remember COVID-tests?  What did we use them for?  I think a reasonable summary of the purpose of COVID-testing is that we use them to collect information for global (whether to lock down or not) and local (whether to visit my grandparents) decision making.  (Note how ridiculous it would have been if the people creating or executing the COVID tests had made such decisions.  We expect that governments make decisions on lock-downs, whereas we decide going to or avoid crowdy areas if there's no lock-down.)

**Principle #1: The purpose of testing is to provide information on how buggy our code is for global and local decision making.**
**Principle #2: The developers should be held accountable for the quality of the code create.**
**Principle #3: The manager having all necessary information about risks, costs, business expectations should be accountable for collecting the adequate information before any release decision.**


## The testing pyramid

A good end-to-end test can reduce uncertainty more than a good unit test, but:
* Some scenarios are difficult to trigger in an end-to-end test, e.g. testing how my code reacts if a database operation deadlocks.
* If the test fails, it usually takes a lot of time to localize the bug, or even to figure out if it was a false or true positive.
* Combinatorial boom of edge cases.  Say, you have 5 components with 5 edge cases each.  You'll natuarally write 5 * 5=25 unit tests for them.  But if you want to test each combination in end-to-end tests, then the number of test cases will be 5^5=3125.
* The execution time of an end-to-end test case can be order of magnitudes slower than that of a unit test, as an entire environment needs to be brought up.

**Principle #4: a reasonable compromise to resolve the trade-offs around end-to-end testing is the testing pyramid: write zillions of unit tests, fewer integration tests, and even fewer end-to-end tests, typically only for the happy paths.**

Why are still so many teams end up with a so large but intolerably slow (and often unsustainable) set of end-to-end tests?  Because in a setup with a separate test team (with a quality gate mandate) it's the testers who write the tests, and -- as they aren't allowed close to the code base -- the only type of tests they can write is end-to-end tests.  Plus, as the developers don't feel themselves responsible for the code quaility, they tend to neglect writing the adequate number of unit tests.
**Principle #5: Most of the tests should be written by the developers.**


## Team structure
Separate testing teams inevitably leads to hand-overs (instead of cooperation), which leads to longer feedback loops.  Fixing a bug committed 2 months ago can easily be order of magnitutes more costly than fixing a bug you committed yesterday, due to the overhead of resetting your development environment accordingly, and figuring out what was in your mind back then.  If you combine this with principles #2 and #5 above, you'll naturally end up with the options as follows:

1. No testers at all.  This option sounds too risky for most managers despite the vast amount of evidence that it works without issue.  In most cases they'll use the "Our use case is more complex" argument.
2. Testers are integrated into the dev teams with a developer-tester ratio that makes it impossible for developers to not deal with testing.  If incentives are set right (short cycle times and taking responsibility for bugs), developers and testers will quickly learn how to cooperate on a daily basis and from early stages of user stories.
3. Some very experienced testers form a so called Enabling Team (referring to the concept described in the Team Topologies book).  All testing activity happens in the dev teams, which a tester may temporarily join to give advise.


## How much testing?

More information reduces uncertainty, hence usually leads to better decisions.  However, collecting more information is costly (not only money-wise but also time-wise).  Also, I think it's a fair assumption that the cost-information curve is non-linear.  Assuming a diminishing return, it becomes an optimisation problem.  More on that in Part #3.
