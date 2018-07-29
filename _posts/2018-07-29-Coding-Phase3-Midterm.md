---
layout: post
title: GSoC Coding Phase 3 - Midterm
tags: [Google Summer of Code, open-source, coala]
---

Some more PRs merged. Yippee!!

- cEP for Git Commit Content Inspection project is merged.
- Pull request for `VCSCommitMetadataBear` is merged. 
- Pull request for `GitMergeInspectBear` also merged.

And pull request for `CISkipInspectBear` is in progress. So now remains only `GitRevertInspectBear` which is my task for phase 3. It has already been two weeks since phase 3 started and I am not going to lie, this bear will be more challenging than the other two i.e. `GitMergeInspectBear` and `CISkipInspectBear`. I have started implementing it and hopefully I will be able to do it in time.

So what exactly will `GitRevertInspectBear` do?

This bear will be responsible for handling `git revert` commits made in the project. Unlike `git merge` commits, revert commits are often needed and use by projects. So there inspection becomes very important because sometimes users tend to do more than just reverting an existing commit in the revert commit.

There are mainly - challeges involved:

- Identify whether the HEAD commit is a `git revert` commit.
- Get the reverted commit from the revert commit.
- Load commit patches of both the commits.
- Compare both patches and see if they are in fact revert of each other.
- Write tests for everything above.

With regard to comparison, checking added files and deleted files should be quite easy but checking modified files and comparing each modification is the most challenging part. [unidiff](https://github.com/matiasb/python-unidiff) will be used for the same. Unidiff is simple Python library to parse and interact with unified diff data.

That's it for this blog. Happy Coding :)