---
layout: page
title: SmokeBreak
permalink: /apps/smokebreak/
description: SmokeBreak was an iPhone, iPod Touch and Android app for helping smokers track and control their smoking habit or help them quit.
---

#SmokeBreak

SmokeBreak was an iPhone, iPod Touch and Android app for helping smokers track and control their smoking habit or help them quit. It was designed to be non-judgmental and fun. 

##History

SmokeBreak was conceived in the summer of 2010. It launched in October 2010 and quickly gained traction; within a month it was featured in Apple's **What's Hot in Healthcare and Fitness** in the U.S. and Czech App Stores; and after a localization to Spanish, quickly climbed to be one of the **top 10 healthcare and fitness apps in Spain**. 

SmokeBreak was discontinued in October of 2011. It ended its life with 75,000 downloads across all platforms, a four-star average rating in the Android app store, and and a five-star average rating in the iPhone App Store. 

##Art Direction

After researching existing smoking-related apps in the App Store, a disheartening lack of design sense was evident. Several apps featured poorly lit photographs of ashtrays or cigarettes; others had confusing, poorly designed UI elements. It was clear that a beautiful, usable design would separate SmokeBreak from the pack. 

The design is crisp and clean, eschewing gaudy colors and aiming for a more subdued, cool monochrome tone overall, with color reserved for the buttons and awards. 

The title is set in Gotham Rounded, a Hoefler & Frere-Jones typeface licensed specifically for this project. 

###Information Design

How should we visualize information about the user's smoking habit in a way that encourages them? One way is by using **sparklines** to show the last seven days at a glance. 

For a more fun presentation of data, the motif of an elementary-school style "report card" allows for clear feedback in the form of stars. It also offers encouragement; stars are awarded based on the user's goals: bronze for meeting the goal, silver for being under, and gold for having no cigarettes in a given day. 

The app also gives awards for streaks and certain combinations of stars; three stars in a row, for example, earns the "Trifecta Award." 

###Resolution Independence

All the artwork is Retina Display ready, and there certainly is a lot of it! Indeed, the 'streak' awards required six groupings of stars, presented in three colors and at three resolutions — a whopping 54 images! Yet by utilizing intelligent workflow in [Opacity Express](http://likethought.com/opacity/), all these images were generated from a single file; tweaking the color of the stars would require editing just one variable. 

##Technologies Used

###Facebook Integration

SmokeBreak integrates with **Facebook Connect** to allow users to post awards to their walls and share them with friends. The Awards backend is a lightweight Python webapp that stores awards using a REST API. It runs on the **Google App Engine**.

###Localization

SmokeBreak is designed from the ground up for localization, and currently boasts **full localization** in both English and Spanish. Both the mobile app and the awards backend are localization-aware, so Spanish-speaking users are able to share Spanish-language awards on Facebook without ever setting a preference.

###Local Notifications

One downside of an app that relies on daily user input is that the user may forget to open the app one day. SmokeBreak takes care of this by allowing users to set reminders at times they often smoke cigarettes; this is accomplished using the new **UILocalNotification** class introduced in iOS 4. The notification also plays a **custom notification sound** which was developed in-house.