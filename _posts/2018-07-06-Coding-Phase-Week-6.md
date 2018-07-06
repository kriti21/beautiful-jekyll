---
layout: post
title: GSoC Coding Phase 2 - Mid term
tags: [Google Summer of Code, open-source, coala]
---

Welcome back :) This is another real quick and possibly very short update on my GSoC project. 
Last week has been really terrible for me. Why, you ask? Well, this is a message we got right after our first evalution was over:

> coding phase 2 underway, and most of you have a backlog of tasks incomplete from coding phase 1. And in this coding phase, there are no excuses like exams. Just you and your project. Catch up on the tasks, reconsider the ones which are not yet done, or fail :P 

Those of you who have been following my blog know that the design of my project was changed just a few days before the first evaluation and I was really worried. Not just because of the pending work but I was actually having a hard time undertanding inheritance concepts and how to link different classes. And when this was just starting to make some sense, writing tests posed another difficult challenge. And to top it all, my laptop stopped working one evening and I had to get it repaired. You can imagine how helpless I must have felt.

At this time, I should really stop and say a heart-felt big thank you to two people who have helped me a lot in understanding the concepts of object oriented programming and how I had to link my code wuth the already existing one. They are [@refeed](https://gitter.im/refeed), my mentor and [@virresh](https://gitter.im/virresh), another GSoCer. I can't even count how many times I have bugged these people asking stupid questions. It's because of these people that my code for `VCSCommitBear` is working now ;) For those who are unfamiliar what `VCSCommitBear` is, let me do a quick recap. `VCSCommitBear` is a bear that performs commit analysis and returns the output as `HiddenResult` which can be used for inspection by other bears. It returns information about HEAD commit such as commit sha, commit message, type of commit viz `git merge`, `git revert` or commits that disable CI builds. So this is kind of foundation for my entire project. After this I have to create bears that would perform inspection on each special type of commit separately.

[This](https://github.com/coala/coala-bears/pull/2543) is the link to my PR for `VCSCommitBear` and as you can see it is still not yet because coala-bears repo is broken at the moment. And that is another reason why I am scared these days because evaluations for coding phase 2 start next week. GSoC administrators have already sent a reminder for that. 

Apart from this, following items have been checked of my list:

- (Pull request)[https://github.com/coala/coala-bears/pull/2501] for handling GitHub PR temporary merge commits is merged into master. Yay!! my first and only PR accepted so far.

- I was assigned another [issue](https://github.com/coala/coala-bears/issues/2575) which was not related to my project though but required only some small changes. [Pull request](https://github.com/coala/coala-bears/pull/2576) for that has been merged too.

- Created two issues related to bugs in coala-bears repo. [This](https://github.com/coala/coala-bears/issues/2556) and [this](https://github.com/coala/coala-bears/issues/2557)

- My PR for `VCSCommitBear` cannot be merge as of now but since it was approved by one of my mentors, I have written code for `GitMergeInspectBear` and `CISkipInspectBear` and pushed on my fork so that I can push my changes as soon as possible once the bugs in coala-bears are resolved.

`GitMergeInspectBear` and `CISkipInspectBear` depend on the `HiddenResult` returned by `VCSCommitBear`. The former one inspects `git merge` commits and checks if the user is trying to merge master branch onto the pull request. coala as well as many other organizations do not allow merge commits. And there is a perfectly appropriate reason for such disapproval. merge commit in the feature branch ties together the histories of the feature branch and master. Merging is nice because it’s a non-destructive operation. The existing branches are not changed in any way. 

However, there is a catch :P

> Merging also means that the feature branch will have an extraneous merge commit every time you need to incorporate upstream changes. If master is very active, this can pollute your feature branch’s history quite a bit. While it’s possible to mitigate this issue with advanced git log options, it can make it hard for other developers to understand the history of the project.

Rebase moves the entire feature branch to begin on the tip of the master branch, effectively incorporating all of the new commits in master. But, instead of using a merge commit, rebasing re-writes the project history by creating brand new commits for each commit in the original branch. Therefore, for a cleaner, linear history free of unnecessary merge commits, `git rebase` is preffered over `git merge` when integrating changes from another branch.

And that is the job of `GitMergeInspectBear`. It identifies merge commits and if they are not allowed, it suggests the user to perform `git rebase` instead.

`CISkipInspectBear` as you can probably guess is the improved version of `SkipCIBear` that I discussed in my [Week-2 Blog post](https://kriti21.github.io/2018-05-31-Coding-Phase-Week-2/). The idea is same but implementation is different obviously. Earlier the design involved a lot of changes in the already existing complex bears like `_CommitBear`. But now this bear is dedicated to performing inspection on `ci_skip_commits` and depends only on `VCSCommitBear`. As **The Zen of Python says** *"Simple is better than complex."*

This is it. Next week we have our evaluations. Fingers crossed. Thanks a ton for stopping by. Happy Coding :) 