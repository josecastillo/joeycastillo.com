---
layout: page
title: TweetSheet
permalink: /apps/tweetsheet/
description: TweetSheet was an app for downloading your Twitter history to your iPhone, iPad or iPod Touch, and letting you search your past.
---

TweetSheet was an app for downloading your Twitter history to your iPhone, iPad or iPod Touch, and letting you search your past. It existed in both a paid "Pro" version and a free "Lite" version. 

<figure style="text-align:center">
    <img src="/images/apps-tweetsheet-icon.png" width="200">
    <figcaption>The TweetSheet icon</figcaption>
</figure>

#History

The Twitter service and many of the apps built around it seemed focused on determining what's happening now. TweetSheet built on a different insight: by answering again and again the question, "What are you doing?" Twitter users assemble a rich set of information about their past. This information can speak not just to who we are and what we are doing, but also to who we were and what we have done.

TweetSheet was launched in the spring of 2010, and received updates to add functionality (retweets and adjustable font sizes), and to support Twitter's OAuth switchover. It was discontinued in January of 2012, as Twitter began offering improved tools for account backup and archive.


#Art Direction

<figure class="third">
	<a href="/images/apps-tweetsheet-screenshot-phone-1.jpg"><img src="/images/apps-tweetsheet-screenshot-phone-1.jpg"></a>
	<a href="/images/apps-tweetsheet-screenshot-phone-2.jpg"><img src="/images/apps-tweetsheet-screenshot-phone-2.jpg"></a>
	<a href="/images/apps-tweetsheet-screenshot-phone-3.jpg"><img src="/images/apps-tweetsheet-screenshot-phone-3.jpg"></a>
	<figcaption>Screenshots of TweetSheet running on the iPhone.</figcaption>
</figure>

TweetSheet's design intentionally stepped outside of the usual colors and textures employed by iPhone and iPad apps. The design evoked a finely-crafted notebook, with wood-grain texture for the toolbars and a canvas cover. The intent was to create not a sterile table of entries, but rather something that evoked a real object; the goal was to create something that let you touch your history. 

<figure class="half">
	<a href="/images/apps-tweetsheet-screenshot-pad-1.jpg"><img src="/images/apps-tweetsheet-screenshot-pad-1.jpg"></a>
	<a href="/images/apps-tweetsheet-screenshot-pad-2.jpg"><img src="/images/apps-tweetsheet-screenshot-pad-2.jpg"></a>
	<figcaption>Screenshots of TweetSheet running on the iPad.</figcaption>
</figure>

TweetSheet was also in the unique position of being in development when the iPad was announced. In order to be a part of the iPad launch, a universal interface was created and tested in the iPad Simulator, and submitted to the App Store before iPads became available to developers. As a result, TweetSheet was available for the iPad on the first day iPads were sold. 

#Technologies used

TweetSheet used a custom Python backend, hosted on the [Google App Engine](http://code.google.com/appengine/), to download users' histories. Tests showed that the process of downloading a user's entire history was too network- and processor-intensive to be done on the iPhone itself. Thus, on first run, TweetSheet offloaded the actual download to the server. 

For TweetSheet Pro users, the TweetSheet backend sent a push notification when the download process was complete. 
