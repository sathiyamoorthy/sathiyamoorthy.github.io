---
layout: post
title: "Mongodb(v3.2.8) Replication"
excerpt: Why,How??
date: 2016-07-23
status: publish
comments: true
share: true
categories:
- "R & D:Optimize Database Design"
tags:
- "NoSql"
---

	NOTE: Basic mongodb knowledge is so vital to understand this concepts.

## Requirement 
* Minumum 3 server (primary-master, seconday-slave, arbiterary).
* Each server should be communicate each other, openSSL.

## Why?
* It helps to serve the required data from different data center on failure or shutdown of primary data center.
* Configure always an odd number of instance to break tie on voting of primary server election.
* Aribitary server : Just to avoid tie on election. holds no data, no need of high configuration instance, but should be different instance.

STEP 1 : (All machine)
Install the latest version of mongodb. walkthrouth [mongodb installation](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

STEP 2 : (All machine)
Make sure that all the server can communicate each other to their mongo shell.

	mongo --host <hostname> --port <portno>

if not connecting open mongod.conf and comment #bindip & change the port randomly.

STEP 3 : (All machine)
Open mongod.conf file & add a replica set on all these the machines.
	
	replication:
 	replSetName: rep0

STEP 4 : (On primary server)

	> cfg = {"_id" : "rep0", "members" : [{"_id" : 0,"host" : "[<primary-machine-ip]:<primary-machine-port>"}]};
	> rs.initiate(cfg);
	> rs.status();

STEP 5: (on primary server)
create a user on "admin" database for authentication & authenticate it.

	> use admin;
	> db.createUser(
	  {
	    user: "health",
	    pwd: "adminpass",
	    roles: [ { role: "root", db: "admin" } ]
	  }
	);
	> db.auth("health", "adminpass" );
	> db.system.users.find();

STEP 6 :
There are two type of authentication mechanisum

* MONGODB-CR
* SCRAM-SHA-1(v3.0..)

We can rollback to "MONGODB-CR" if needed, For better security go with SCRAN-SHA-1.

STEP 7 : (optional - all machine)
For older version "MONGODB-CR" mechanisum. Current system version is 5 you cant get the list of database and authentication in robomongo, so please change to 3 instead of 5

	> use admin;
	> db.system.version.find();
	> db.system.version.remove({}); 
	> db.system.version.insert({ "_id" : "authSchema", "currentVersion" : 3 })
	> db.system.users.remove({})
	> db.createUser(
	  {
	    user: "health",
	    pwd: "adminpass",
	    roles: [ { role: "root", db: "admin" } ]
	  }
	);

STEP 8 : (on primary server)
We are ready to popup a heartbeat to secondary server and arbitery server.
Open arbiter server mongod.conf file and make it "journal : enabled : false".

	> rs.add("<secondary-server-ip>:<secondary-server-port>")
	> rs.addArb("<arbiter-server-ip>:<arbiter-server-ip>")

STEP 9 : (on primary server)
Make sure that all server connected successfully.

	> rs.status();
	> rs.conf();

STEP 10 : (Use cases)

* Stop mongod servivce on primary server, make sure that secondary server become primary.
* Stop current primary server, make sure that arbiter server remain the same.

STEP 11 : (Security)

* Internal Authentication (security bettween master & slaves)
* Authorization

Enrypted base64 "Keyfile" whicl leads the Internal Authentication & Authorization on client & server, Create this keyfile on primary machine & copy the same to rest over all the machine in same location.

	openssl rand -base64 755 > /root/mongokey
	chmod 700 /root/mongokey
	chown mongodb:mongodb /root/mongokey

STEP 12 : 
Stop mongod service on  all the machine & open "mongod.conf" file and add the generated "keyfile" path.

	security :
		keyFile : /root/mongokey

Start mongod service on all the machine.

## Conculusion
Thats it. Mongodb replication is ready to use in a secure way. Keep in mind that always go with an odd number of instance. 3 server replica set can bear up to 1 failure, 5 server replica set can bear up to 2 failure, 7 can bear upto 3.
