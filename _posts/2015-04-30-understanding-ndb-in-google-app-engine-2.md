---
title: "Understanding NDB in App Engine(2)"
description: "Understanding ndb in App Engine"
category: tutorial
tags: [python, appengine, ndb]
---

### Query Entities ###
In previous talk, every entity has an unique `Key` object. You can retrive your entity by using the `Key`.

``` python
>>> a = User(name='John', age=8)
>>> a_key = a.put()
>>> b_key = a_key.urlsafe()     # duplicate another key from a_key
>>> b = ndb.Key(urlsafe=b_key)  # now b is equal to a entity
```
But how could we retrive a set of entities by a specific condition? We can use the `query` method of the `Model` class.

For example, there are a list of `User` entities below.

| name  | age   |
|------ |-----  |
| John  | 8     |
| Alex  | 16    |
| Mary  | 8     |
| Bob   | 8     |


Now try to open your [interactive console](http://localhost:8000/console)

You can query all of these entities by using ...

``` python
>>> qry = User.query()
>>> result = qry.fetch()
>>> print result
[User(key=Key('User', 4785074604081152), age=8, location=None, name=u'Bob'), User(key=Key('User', 5066549580791808), age=16, location=None, name=u'Alex'), User(key=Key('User', 5629499534213120), age=8, location=None, name=u'John'), User(key=Key('User', 6192449487634432), age=8, location=None, name=u'Mary')]
```

You can query entities with specific condition (age=8 and age > 8 for example) by using `filter` ...

``` python
>>> qry = User.query()
>>> result = qry.filter(User.age==8).fetch()
>>> print result
[User(key=Key('User', 4785074604081152), age=8, location=None, name=u'Bob'), User(key=Key('User', 5629499534213120), age=8, location=None, name=u'John'), User(key=Key('User', 6192449487634432), age=8, location=None, name=u'Mary')]
>>> result = qry.filter(User.age > 8).fetch()
>>> print result
[User(key=Key('User', 5066549580791808), age=16, location=None, name=u'Alex')]
```

Lets try some more complicate queries.

Multiple conditions like User.age == 8 `and` User.name == 'Bob'

``` python
>>> qry = User.query()
>>> result = qry.filter(User.age==8, User.name=='Bob').fetch()
>>> print result
[User(key=Key('User', 4785074604081152), age=8, location=None, name=u'Bob')]
>>> result = qry.filter(ndb.AND(USer.age==8, User.name='Bob')).fetch() 
>>> print result
[User(key=Key('User', 4785074604081152), age=8, location=None, name=u'Bob')]
```

Multiple conditions like User.age == 8 `or` User.name == 'Alex'

``` python
$> qry = User.query()
$> result = qry.filter(ndb.OR(User.name=='Alex, User.age==8)).fetch()
$> print result
[User(key=Key('User', 4785074604081152), age=8, location=None, name=u'Bob'), User(key=Key('User', 5629499534213120), age=8, location=None, name=u'John'), User(key=Key('User', 6192449487634432), age=8, location=None, name=u'Mary'), User(key=Key('User', 5066549580791808), age=16, location=None, name=u'Alex')]
```

Isn't is easy ?

