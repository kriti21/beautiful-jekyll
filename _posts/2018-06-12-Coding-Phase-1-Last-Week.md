---
layout: post
title: GSoC Coding Phase 1 - Last week 
tags: [Google Summer of Code, open-source, coala]
---

Most of us have been taught the definition of software development in colleges which goes like:

	> Software development is the process of creating a computer software.
	> It includes preparing a design, coding the program, and fixing the
	> bugs. The final goal of software development is to translate user
	> needs to software product, while continuously improving the team
	> and the process.

This week I experienced the truth of these statements. When I am given a problem, my fingers tend to reach for the keyboard without having a concrete design in my mind. In my last post, I wrote about my task which was to inspect commits that disable CI builds. Well I did some work on that and made a pull request. As it turns out, the way I was approaching this problem was quite different that the actual requirement. In the words of [John](https://gitter.im/jayvdb)

	> an extra level is needed in the abstraction, which needs to be a
	> separate PR before this.
	> this isnt creating a meta bear.
	> 
	> A meta bear is like URLBear, which only yields HiddenResult.
	> See URLHeadBear and InvalidLinkBear for how they all link together.
	> 
	> We need a VCSCommitBear which only yields a CommitResult(HiddenResult).
	> SkipCIBear would then receive those CommitResult and only yield the
	> CommitResult if the commit was a CI skip.
	> 
	> (and while trying to understand this, it is better to simply ignore
	> GitCommitBear and HgCommitBear -- 
	> those will need to be glued back in after the redesign.)

So then I started working on this meta bear and lack of Object Oriented Programming Skills took hold of me. 
I had the correct code written but I was executing in the wrong way and it was giving wrong output, quite obviously. I looked and looked but in vain. This was the first time in life when I actually read a lot, a lot about classes, meta classes, abstract classes, multiple inheritance etc in Python. Honestly, just one class and its instances have been the limit till now. It took me two days to realize that my code is correct but I was executing it the wrong way. As they say:

	> Overload, clutter, and confusion are not attributes of information,
	> they are failures of design.

That is all for this post. We have our first evaluations this week and I am afraid that my work isn't complete yet. So I am gonna go do my work. Hopefully, In-progress tasks would be considered and I shall make it to the next coding phase.