---
layout: post
title: "Like Unlike in rails using Gem"
excerpt: "This post will help to setup like unlike functionality in Rails using Gem. like-dislike gem provides both backend and frontend functionality for like and unlike. It works similar like facebook, youtube, etc.. like dislike."
date: 2015-09-16
status: publish
comments: true
share: true
categories:
- Rails
tags:
- "Rails, like-dislike, vote unvote, like unlike"
<!-- image:
  feature: ruby.jpg -->
---

Like Unlike is a common functionality in many applications. For implementing this simple feature developer have to put lot's off effort to implement this. But `like-dislike` gem just adding few lines in application provides both fronend and backend functionality. 

In this post, we are going to look at how like-dislike gem can use in the application using simple configutation and common use pattern of the gem.

###like-dislike gem

Like Dilike gem built on top of <a href="https://github.com/ryanto/acts_as_votable" target="_blank">act_as_votable</a> gem. Our main goal is end user can click like or dislike, finally in fronend we should show the count of the both like and dislike. So the basic need of this is voter and where he/she is voting this both need to capture and store it one table with the realationship.

###like-dislike and act_as_votable

act-as_votable provides vote and unvote backend feature on model level. It allow any model to be voted on, like/dislike, upvote/downvote, etc. and to be voted under arbitary scopes.



