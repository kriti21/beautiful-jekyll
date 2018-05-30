---
layout: post
title: GSoC Coding Phase - Week 1
tags: [Google Summer of Code, open-source, coala]
---

It's been two weeks since GSoC coding phase started. I had my university exams starting just two days after the coding phase began so these last two weeks were really hectic. But I am glad my exams are over now and I can resume my pending work with full focus. This blog will give details about my task for coding phase 1.

## Quick update on current status

As I said in my last post for community bonding period that I had some milestones to achieve. Well 80% of those tasks are done and the remaining 20% is actively being updated i.e. the coala Enhancement Proposal for my project [link]() is in progress almost complete. I am hopeful of getting it merged in next one or two days time. But this is a very valuable lesson for me as this kind of lagging is strictly not allowed in coding phase period.

I have divided my goal for coding phase 1 into two distinct tasks. I am going to discuss the first one in this post, the problem that I have to solve and how I plan to approach it. Let's dive in :P

## The problem - Travis merge commits

Travis merge commits are sort of *magic* commits ;) They are created automatically when a PR is merged using the GitHub UI. To be honest, this was totally a new concept that I had seen for the very first time. A big thanks to my mentor Saurav Singh who helped me a lot in understanding the problem. Look for more details [here](https://github.com/coala/coala-bears/issues/1037)

Initially I thought these merge commits were created by GitHub and only in cases when one person authors a pull request which is later committed by two or more people other than the author itself. But after having discussion with my mentors, it turns out that this is not the case. Travis merge commits, in fact happen for every type of commit. Also since this is just Travis specific thing, the fact that whether GitHub creates these commits or Travis CI does is still not known. So the only knowledge left at our disposal is that these are merge commits with fixed length of 92 characters following this format:

```
 r('^Merge ([0-9a-f]{40}) into ([0-9a-f]{40})$')
```

Some useful links related to this issue that might be helpful to someone stuck with some similar problem: 
[link 1](https://github.com/travis-ci/travis-ci/issues/7418) and [link 2](https://github.com/travis-ci/travis-ci/issues/8400)

The `GitCommitBear` of coala does not identify Travis merge commit and run checks on it like length of commit shortlog and body, issue reference etc. This being a merge commit does not satisfy these requirements causing the `GitCommitBear` to fail which in turn fails Travis CI build for the corresponding pull request as well. 

## Solution approach & Current status

So what we need the `GitCommitBear` to do is:
- Identify Travis CI merge commits and ignore them and
- Run commit checks on the unmerged parent commit of this commit

The identification part can be done using regex i.e. the commit content should match with the above pattern. For each match being true, the sha of parent commit is extracted from the commit message. Now, 
`GitCommitBear` can use this commit hash to get the contents of original commit and perform checks on the latter.

A pull request has been made in coala-bears repository that implements the changes mentioned above. Please have a look [here](https://github.com/coala/coala-bears/pull/2501).

That's all for now. Stay tuned for further updates ;)
