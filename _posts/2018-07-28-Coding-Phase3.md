---
layout: post
title: GSoC Coding Phase 3
tags: [Google Summer of Code, open-source, coala]
---

Hallo! Wie geht es Menschen?

I have been thinking for a long time now of learning a new language. And finally German it is. It has been more than a week now since I started learning this beautiful language. By the way, I came to know about German culture from my mentor Saurav Singh who is an Indian working in Germany. According to him, people there are very punctual. Delay is absolutely unacceptable in German culture. Isn't that incredible ? Okay, enough trash talk. :P Let's get back to GSoC.

I am so late to write about this but I made it to the final phase, third coding phase of GSoC 2018. Thanks again to my mentors Rafid Aslam and Saurav Singh.  

This blog will be very short one because I am not going to discuss the details about my task for phase 3 here (Next blog for that). Just a couple of other things that I have been doing for now.

So as always, the "foundation" of my entire project i.e. `VCSCommitBear` is now called `VCSCommitMetadataBear`. One more layer of abstraction is added to the design so as to make this bear fully generic. This means that unlike before when I wrote code for fetching git commits here making it git specific, it can now be integrated with any other VCS as well. Quite obviously, the VCS specific code goes in another bear called `GitCommitMetadataBear`. This bear fetches the HEAD commit in git repository, analyzes it and returns the result to `VCSCommitMetadataBear` which further returns a `HiddenResult` to be used by other bears. So for other VCS like Mercurial, we will have to make `MercurialCommitMetadataBear` and everything else remains nice and tidy. See how proper designing can make complex things simple and simple things even more efficient.

When a proper design is made and coded, the next big and very important challenge is testing. The importance of good testing skills is so crucial for being a good programmer. And I won't lie, I didn't know a thing about it before GSoC. Even now, I face a lot of problems while writing tests, not generally with possible test cases, but with the way functions are called and executed. Object oriented programming stuff ;) My mentor has been helping me a lot with this.

I have started working on `GitRevertInspectBear` also which is my task for phase 3 besides improving my previous work. That's all for now. This is even shorter than I thought. Happy Coding :)