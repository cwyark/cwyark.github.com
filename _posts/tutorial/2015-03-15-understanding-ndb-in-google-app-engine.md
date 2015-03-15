---
layout: post
title: "Understanding NDB in App Engine"
description: "Understanding ndb in App Engine"
category: tutorial
tags: [python, appengine, ndb]
---
{% include JB/setup %}


### NDB in App Engine (Unfinish post)###

####_Entities and Models_####
[App engine's NDB](https://cloud.google.com/appengine/docs/python/ndb/) is a persistent storage whcih is promoted by Google Cloud Platform. It features in schemaless object datastore, automatic caching, sophisticated queries and atomic transactions.

Every data object in NDB is called `Entity`, just like a member's information( name=John, age=18, address=Taipei).If you want to use NDB in your application, you have to define a `Model` whcih is presented as a `Class` in python.This is an example of defining a `Model` (in my_model.py for example)

	from google.appengine.ext import ndb
	
	# define a ndb model
	class User(ndb.Model):
		name = ndb.StringProperty()
		age = ndb.IntegerProperty()
		location = ndb.GeoPtProperty()

Here's a class `User` which is inherited from `ndb.Model`, and `name`, `age`, `location` are the properties of `User`. For more information about property, you could check [here](https://cloud.google.com/appengine/docs/python/ndb/properties).

Once you finish defining a `Model`, you can play with the `Model` by using the [interactive console](http://localhost:8000/console)

	$> from my_model import User
	$> a = User(name='John', age=8)
	$> a.put()

Then you can find a new data(whih is called an `entity`) in your [Datastore Viewer](http://localhost:8000/datastore)

Here's another important thing that there are `Key`, `id` or `Key Name` in your created entity, but you can't remember you have defined these fields in your `Model`. These fields are the special things existing in ndb.

####_Entities and Keys_####

####_Property_####

####_Query_####

####_Index_####
