---
layout: page
title: FOOD & WINE Cocktails™
permalink: /apps/cocktails/
description: Developed for American Express Publishing. A visually arresting cocktail guide published in May of 2012.
---

#FOOD & WINE Cocktails™

FOOD & WINE Cocktails™ is a visually arresting cocktail guide for iPhone and Android, published in May of 2012 by American Express Publishing. Featured multiple times on the front page of Apple's App Store, its stunning design, snappy UI and retina-grade graphics  have made it a stand-out app in the Food & Drink category. It is currently [available for free on the iOS App Store](http://itunes.apple.com/us/app/food-wine-cocktails/id520503449?ls=1&mt=8), as well as well as for Android phones [on the Google Play store](https://play.google.com/store/apps/details?id=com.aexp.foodandwine.cocktails). 

##Art Direction

The app was developed in close conjunction with members of the FOOD & WINE digital design team, especially Patricia Sanchez and Jihae Min, with additional guidance from the [New York-based creative agency Expand the Room](http://www.expandtheroom.com). 

##Technologies Used

###Nuts and Bolts

The FOOD & WINE Cocktails app makes use of **advanced techniques in Core Data**, including dynamic extension of the managed object model at runtime. This allowed for development of a broad, reusable "Recipes" data model, decoupled from the specific needs of a Cocktail guide, that could be reused to power other apps in the Amexpub portfolio. 

The app integrates with the [mOcean mobile](http://www.moceanmobile.com) ad serving platform, and also makes use of **smart push notifications** to bring users a different featured cocktail each week. The push notification backend specifies both the push notification text and sound, as well as metadata necessary to show off the featured cocktail on launch. 

Since cocktails are such a social experience, robust sharing features are included in the app: sharing on Facebook and Twitter via the iOS **Social.framework**, rich **in-app email**, and sharing via **iMessage/SMS**. 

###User Experience

While all of the app UI was bundled in the app bundle, many of the images are loaded from the FOOD & WINE content delivery network. As a result, care was taken at every step to ensure that both standard and **Retina-caliber assets** were available for each of the roughly 420 recipes presented in the app. And naturally, the app was updated to take advantage of the iPhone 5's taller screen on the first day the new phone shipped. 

The app boasts excellent **VoiceOver accessibility**, including attention to ensure that all image-based buttons have appropriate labels. Additionally, the app detects when VoiceOver is running and automatically uses the more accessible list interface instead of the less accessible gallery view. 

Finally, while it may seem small, subtle **animations** are used throughout the app, from the fade-and-slide of the splash screen to the card flip that occurs when a recipe is displayed. These touches, while not specified in the creative brief or mockups, add a subtle sense of polish and quality to the app. 