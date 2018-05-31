---
layout: post
title: GSoC Coding Phase - Week 2
tags: [Google Summer of Code, open-source, coala]
---

In this post I shall talk about the second task that I have to do for coding phase 1 i.e. **Handle commits that skip CI build**

## What is CI ?

Continuous integration (CI) is a software engineering practice in which isolated changes are immediately tested and reported on when they are added to a larger code base. The goal of CI is to provide rapid feedback so that if a defect is introduced into the code base, it can be identified and corrected as soon as possible.

Best practices of CI include:

- Committing code frequently.
- Categorizing developer tests.
- Using a dedicated integration build machine.
- Using continuous feedback mechanisms.
- Staging builds.

So naturally CI is an essential part of open-source development especially because multiple people work on the same project at the same time so lot of changes occur in very less time.

*But my task is to inspect commits that disable CI build. Ouestion is why do we need this if CI is so important?*

## Why commits that skip CI build should be allowed ?

[This](https://github.com/travis-ci/travis-ci/issues/5374) is an important discussion presenting different opinions people have about skipping CI build in a pull request. Following points summarize the same:

- In cases when code modifications need to be verified by peers before running tests.
- For documentation related changes that do not require tests.
- To have discussions on Work-In-Progress PRs without having to care about CI initially.
- For small code correction where the build deployment and further tests are not required.
- Updates to scripts that do not affect anything in the testable code.

*But these scenarios should be dealt very carefully because any change in master branch without complete testing can create huge mess if it breaks any code. And this is my project* ;)

## The problem

As mentioned above, my task is to inspect commits that disable CI build. Inspection here means that such commits should only modify files not covered by `.coafile` or tests (`.coafile` is configuration file for coala to specify what checks should run with what bear in one file for the entire project).  

## Solution approach & Current status

For this task, I am creating a new bear in [coala-bears repository](https://github.com/coala/coala-bears/) called `SkipCIBear`. This bear would work for all the CI providers that coala supports like Travis CI, Circle CI, GitLab CI, Semaphore CI etc. 

Most of these CI providers support the sequences `[ci skip]` or `[skip ci]` in the commit message to disable CI build from occuring. Commits that have either of these sequences anywhere in the commit message
are ignored by these CI engines. This bear would detect the changes in such commits and verify that they can skip CI build that is with respect to modified files and whether the corresponding CI engine allows skipping build or not. An appropriate message is returned if skipping build is not supported by the CI engine used by the organization.

I am working on the implementation of this bear as of now. Today I had a talk with my mentor Saurav Singh about some issues that I have been facing lately. He was very nice and helped me by giving examples of how I can approach this. I will make a pull request for this soon. Readers will be duly updated in my next blog.

Thanks for stopping by. Happy Coding :)