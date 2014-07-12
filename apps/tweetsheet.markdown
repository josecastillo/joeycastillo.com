---
layout: page
title: TweetSheet
permalink: /apps/tweetsheet/
description: TweetSheet was an app for downloading your Twitter history to your iPhone, iPad or iPod Touch, and letting you search your past.
---

#TweetSheet

TweetSheet was an app for downloading your Twitter history to your iPhone, iPad or iPod Touch, and letting you search your past. It existed in both a paid "Pro" version and a free "Lite" version. 

##History

The Twitter service and many of the apps built around it seem focused on determining what's happening now. TweetSheet builds on a different insight: by answering again and again the question, "What are you doing?" Twitter users assemble a rich set of information about their past. This information can speak not just to who we are and what we are doing, but also to who we were and what we have done.

TweetSheet was launched in the spring of 2010, and received updates to add functionality (retweets and adjustable font sizes), and to support Twitter's OAuth switchover. It was discontinued in January of 2012.

##Technologies used

###App Engine

TweetSheet uses a custom Python backend, hosted on the [Google App Engine](http://code.google.com/appengine/), to download users' histories. Tests showed that the process of downloading a user's entire history was too network- and processor-intensive to be done on the iPhone itself. Thus, on first run, TweetSheet offloads the actual download to the server. 

###Push Notifications

For TweetSheet Pro users, the TweetSheet backend sends a push notification when the download process is complete. Push notifications are sent using [Urban Airship](http://www.urbanairship.com/)'s push notification service.

##Art Direction

TweetSheet's design intentionally steps outside of the usual colors and textures employed by iPhone and iPad apps. The design evokes a finely-crafted notebook, with wood-grain texture for the toolbars and a canvas cover. The intent is to create not a sterile table of entries, but rather something that evokes a real object; the goal is to create something that lets you touch your history. 

All icons and textures were produced in-house using Photoshop CS and [Opacity Express](http://likethought.com/opacity/). 