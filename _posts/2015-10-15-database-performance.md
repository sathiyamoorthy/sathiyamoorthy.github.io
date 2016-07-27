---
layout: post
title: "Table Partition - Way to reduce the cost of an query"
excerpt: "Why,When & How???"
date: 2015-10-20
status: publish
comments: true
share: true
categories:
- "R & D:Optimize Database Design"
tags:
- "RDBMS"
---

	NOTE: Basic RDBMS knowledge is so vital to understand this concepts.

## Why?
Table Partitioning is one of the feasible way to optimize & keep frequently used records in handy to improve each **"SELECT" in #O(n)** (approx.. worst & best cases are applicable based on no.of.records) even a table contains huge number of records. Altimate goal is to reduce the cost & waiting time of an query.

## When?
* It should apply on the tables which contains huge amount of data.
* To get rid of old records which not at all used frequently but the data should exist in actual database.
* This terminology won't workout for tables (like master tables) which consists less no of records, and surely it will affect the performance if partition applied.

## How?
It works like Parent & child., Parent table actually doesnt contain any records, only used for child table to inherits based on constraint. Lets start with an real time example "LOCALIZATION"

STEP 1 : 
	
	Create Database : "dictionary"
	Create Parent Table : "words"
	Parent table Columns : id, en, ch

STEP2 : Create 26 child tables with Rule
	
	CREATE RULE words_insert_a AS
	ON INSERT TO words WHERE
    ( en LIKE "a.%" )
	DO INSTEAD
    INSERT INTO words_a VALUES (NEW.*);

STEP 3 : Create constraints on each child and inherits with parent.
	
	CREATE TABLE words_a (CHECK ( en LIKE 'a.%' )) INHERITS (words);


STEP 4: Populate dummy data on words table.
	
	Migrated 1263002 translation records into words table.


STEP 5: Analyze a cost & total runtime of a query to get a record from 1263002.
	
	EXPLAIN ANALYZE SELECT * FROM words WHERE "en" IN ('game') OR "en" LIKE 'game.%'

RESULT

	| Terms           | Before      | After     |
	|-----------------|-------------|-----------|
	| No.of. record   | 1263002     | 1263002   |
	| Cost of a query | 42145.54    | 40.36     |
	| Total Runtime   | 203.520 ms  | 0.558 ms  |
	| Memory of Table | 157 MB      | 157 MB    |
	| DML Query       | No Changes  | No Changes|


## Conclusion
This was giving tremendous result in the data accessibility. But our "select" query should be added with the same constraint which we used for child table creation, otherwise there is no use of partitioning.


	

	













  

	

