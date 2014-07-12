---
layout: page
title: Bushwick Open Studios
permalink: /apps/openstudios/
description: A versatile and flexible app for displaying the schedule of arts events and festivals. 
---

#Bushwick Open Studios

The Bushwick Open Studios app comprises both a Django backend for storing information about the three-day arts festival, and a native iPhone client for viewing the schedules and events. The 2012 app was a modest success, downloaded 3,000 times over the course of the festival.

For 2013, the app is being rewritten from the ground up. The Django backend is being replaced with a lightweight web API based on [Flask](http://flask.pocoo.org) and [SQLAlchemy](http://www.sqlalchemy.org), and the iPhone app is being redesigned to match with the new print style. 

Both the backend and the client portions of the app are being built with reusability in mind, which is to say, the code is decoupled from the needs of BOS, and built to support any multi-day festival. 

In addition to the app, I'm working on an eBook style writeup on how to make an app from scratch, using the BOS app as a case study. In the book, the arts festival is simply called "ArtsFest", and the narrative takes us from initial requirements-gathering through to building an API; wireframing and designing screens; building a Core Data model; and then finally designing, implementing and shipping an app. 

A more in-depth writeup will find its way here closer to date of the festival (June 2013). 
