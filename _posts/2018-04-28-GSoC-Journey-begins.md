---
layout: post
title: GSoC journey begins
tags: [Google Summer of Code, open-source, coala]
---

I would like to make a confession before I start. GSoC has been my long awaited dream and though I had contributed to a few organizations before [coala](https://coala.io/#/home), this is where I truly belong.
It might sound silly but that's the feeling I got here :) The community and work culture at coala is so welcoming and nice that a **"Hello World!!"** [here](https://gitter.im/coala/coala) is just enough to fit in :P 

## How it all started?

So it was late in December 2017 and I had three to four organizations selected that I would like to contribute to for GSoC 2018. Soon I realized that this startegy is more time consuming with little effectiveness in my overall work. Therefore, I decided to stick to one organization only. And as you already know, coala it is. So I spent the next few months understanding the project and contributing to it. For those who are new to open-source, contribution in general is a broad term. It not only means solving issues but more about knowing the project. Everything from fixing typo errors in documentation to solving complex code issues is counted as a contribution. A major part of it goes to reviewing other people's code and helping each other along the way. 

Sometimes it might seem hard to keep up but everything is worth the effort. 

## About my project

![Project Intro](/img/intro1.png)

coala has a GitCommitBear that is responsible for verifying that commits made to coala repository are as per the set standards. My project is about improving it so that it is more useful for some special type of commits.

The GitCommitBear at present performs a check on the content of regular commits made to coala. However, there are many special types of commit messages that should be only used in conjunction with patches containing a special type of content.

For example, git revert commit which is used to revert any previous commit and git merge commit which is generated whenever someone performs a git rebase and tries to merge master onto the pull request. Such commits generate a default commit message that is very concise and not according to coala’s standards. 
The coala project wants to allow `git revert` commits, but does not want to accept `git merge` commits as the repositories are strictly fast-forward merges that do not have an extra commit.

In addition there are special sequences that can be added to git commit messages to instruct tools to operate in a certain way. For example in cases where some tests are not required by any pull request made to coala, some special sequences can be added to git commit messages to instruct tools to operate in a certain way.

This project is about detecting such commits and verifying that they are correct according to the configuration settings.

## The Road ahead

This is officially the bonding period where gsoc students are expected to get familiar with their organization and understand their workflow etc.

![Project Intro](/img/intro2.png)

My tasks for this period include writing a coala Enhancement Proposal for my project that will soon be available [here](https://github.com/coala/cEPs/) and two more issues on the basis of which this project will be built. One of them is to identify different types of commits I discussed in the introduction and the other is to load patches of the corresponding commits. 
This is the status so far:

![Project Intro](/img/intro3.png)

I am hopeful of completing my bonding tasks on time and will keep you, the readers updated about my progress. Thanks for stopping by. Happy coding :)
