---
layout: post
title:  "Who should be responsible for software quality"
date:   2023-06-19 11:22:00 +0100
categories: testing
---
Is this setup familiar to you: a separate test team with the mandate of being a "quality gate"?

If so, are the following patterns also familiar to you?
* Developers tend to neglect doing even the most basic testing-related duties, they rather simply hand over stuff to testers.
* For reproducibility, testers spend a lot of time setting up test environments utilizing clever but unscalable and unsustainable workarounds.
* The number of end-to-end test cases accumulate to a level where it takes days (if automated) or weeks (if manual) to execute.
* Quite a big fluctuation in the test team, moreover, often the best of them leave first (typically for a job with more money and prestige).
* Developers regularly fix bugs several weeks or months after they had committed the original code, spending a lot of time setting up their dev environment accordingly and trying to remember what they did (and why they did what they did).
* Along with hand-overs, workflow-states also start to appear: rather than working in continuous discovery-development-delivery cycles, you hear about code freezes (sometimes even so-called feature-freezes), bug-fixing periods and release committees.  Project managers thrive, stress levels fluctuate.
* Developers regularly fix bugs several weeks or months after they committed the original code, spending a lot of time setting up their dev environment accordingly and trying to remember what they did (and why they did what they did).
* After each annoying production bug the developers finger-point to testers ("I can't believe they didn't catch it!") and vica-versa ("If they at least tried it out before checking the code in!"), and the testing lead argues that they would have caught it had the had more time and resources.

Lot of frustration combined with inefficient practices for a questionable outcome.

I believe most of this is down to a misunderstanding about the role of testing.  With a separated testing team its too attrictive for every participant to reach a consensus that it's the testing team who should be accountable for code quality: the developers are happy to drop this responsibility whereas the testers are happy to take it.

However, if you are responsible for something you can't control (show me a company where a tester can fire a developer committing too many bugs), it can only lead to frustration and inefficient practices.  I think this story is very similar to the one where system administrators struggle with the operation of software written by others, the realization of which lead to the devops movement. (It's such a shame that the industry completely misunderstood devops and reacted by simply renaming system admin role to devops roles.  (And this whole story repeated recently with scrum masters...))

In part 2, I'll propose a different setup.
