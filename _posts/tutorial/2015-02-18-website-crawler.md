---
layout: post
title: "Web Crawler"
tagline: "Help you to fetch a large scale of data from the Internet"
description: "crawlers can fetch informations from several sites."
category: archive
tags: [python, crawler]
---
{% include JB/setup %}

Most website provide informations for users, but these informations are only shown on the page's view and you could not retrieve specific informations on the page at once. Moreover, they didn't provide any link that can download the historical data in csv, excel file. All of the informations can only retrieved by manual. So people have to use their mouse (or keyboard maybe?) and double click, right click , and then copy and paste. That is very inefficient.Further, if you retrieve these informations manually , you know people may easily get tired if they do the copy and paste repeatly, not to mention tens of thousands targets are waiting for.


__Web crawler can make your data retriving from the internet `easiler`.__

OK, this is just a simple example that explain the disadvantage of the traditional way to fetch data from the internet.

There are more advantages of the web crawler.

* __fetch data from the internet automatically__

	You don't have to do anything after you execute the crawler just like what I said.

* __design the crawling schedule more flexible__

	You can design you crawling schedule with your own need. For example, you want to rapidly show the retrieved data on your website or your service, like the realtime stock information. Or you want to store the retrieved data into your database or excel that can help you to analysis these data for marketing. Every thing is possible if you need this.

* __keep tracking your target__

	Websites like stock bulletin board or online shop, your target (which means you want to retrive data from this) may change their informations as time goes. For example, you want to know several online shop's product price which can help you to make a marketing strategy. But the pricing is always change, and you want keep tracking it. A web cralwer can offer you a 24/7 service to keep tracking the targets.

* __ability to store in database__

	Every retrieved data should be store in the database. No matter some `RMDB` or `NoSQL` , even `excel`, crawler should have ability to access the databse and store data in it. 

Of course, the designed crawler is not controlling and positioning the mouse and double click or right click to fetch the website automatically. It should parse the URL rules and apply the `http` methods like `GET`, `POST` to get the HTML templates. After that, the crawler use some `XML/HTML parsing tools` to parse the template and extract the required data. The crawler should be able to store the data into database like `SQLite`/`MySQL`/`PostgreSQL` or other kinds of database.
