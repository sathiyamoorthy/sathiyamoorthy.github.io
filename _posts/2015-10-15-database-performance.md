---
layout: post
title: "Table Partition - Way to Improve Performance"
excerpt: "Why,When & How???"
date: 2015-10-15
status: publish
comments: true
share: true
categories:
- "R & D:Optimize Database Design"
tags:
- "RDBMS"
---

NOTE: Basic RDBMS knowlege is a vital one before start reading this concepts.

## Why?
Table Partitioning is one of the feasible way to optimize & keep frequently used records in handy to improve each **"SELECT" in #O(n)** (approx.. worst & best cases are applicable based on no.of.records) even a table contains huge number of records.

## When?
* It should apply on the tables which contains huge amount of data.
* To get rid of old records which not at all used frequently but the data should exist in actual database.
* This terminology won't workout for tables (like master tables) which consists less no of records, and surely it will affect the performance if partition applied.

## How?
It works like Parent & child., 







  

	

