---
layout: post
title: Launching SIGILANCE, or, The Long Way Around
description: A day after launching a product, reflections on long walks through the forest, and the long, winding path from concept to creation. 
category: notes
tags: [personal note]
image:
  feature: 20150701-easy-way-banner.jpg
  credit: Joey Castillo

og_image: images/20150701-easy-way-og.jpg
og_image_type: image/jpg
og_image_width: 640
og_image_height: 400
---

At the risk of burying the lede, I should probably start with this: after eleven months of work, I launched a thing yesterday. It's an [NFC-enabled OpenPGP smart card](https://www.sigilance.com/). It’s not exactly what I thought it would be at the start. In particular, I now see that buying a laser cutter to make fancy crypto boxes was misguided. As was the decision to launch a Kickstarter campaign when the software support wasn’t 100% there. So it goes. Lessons learned. 

In the months since the Kickstarter failed, I’ve worked on advancing not just my crypto project, but the whole OpenPGP ecosystem. I [worked on software support on Android](https://github.com/open-keychain/open-keychain/pull/1278#event-305734837), [diagnosed security vulnerabilities](http://www.networkworld.com/article/2914645/microsoft-subnet/security-flaw-allows-pin-bypass-in-yubikey-neo.html), and kept my head down to focus on the hard work of building a product: writing code and squashing bugs; designing a visual identity; sourcing smart cards and holograms; signing the agreements necessary to get developer tools and documentation; and testing, testing, testing. 

<figure>
    <img src="/images/20150701-the-card.jpg" alt="A product shot of the SIGILANCE OpenPGP Smart Card, sitting on top of an RFID-blocking sleeve for the same.">
    <figcaption>Obligatory "Buy Now" link: <a href="https://www.sigilance.com/store/"><span style="color: red; font-weight: bold; text-decoration: underline;">BUY NOW!</span></a></figcaption>
</figure>

The product that actually launched yesterday is a smart card for securing your email. You can use it out of the box with your Android smart phone or tablet. There’s only [one other solution](https://www.yubico.com/products/yubikey-hardware/yubikey-neo/) for smart card crypto on Android, and at $25, my solution is half the price of a Yubikey NEO. As I wrote to my Kickstarter backers in [an update yesterday](https://www.kickstarter.com/projects/joeycastillo/signet-simple-online-privacy-cards/posts/1279936), I set out with the goal of putting secure communications into the hands of more people, and while the means may have shifted over time, I think what I launched yesterday moves us closer to that goal. 

But I'm not here to talk tech. I'm here to talk about the trail. 

## Find the Blaze

The day after the Kickstarter campaign ended, I packed my backpack and headed out to walk the Appalachian Trail for a couple of days. There's nothing like a long walk to clear your mind. On a Monday I stepped onto a bus at the Port Authority Bus Terminal, and two hours later, I found myself on the side of the highway, miles from the nearest town. I started walking along the shoulder, trying to find the blaze. 

<figure>
    <img src="/images/20150701-the-blaze.jpg" alt="A small, vertical strip of white paint on a tree in the forest.">
</figure>

I should probably explain that term. A "blaze" is a common way to mark a trail. It often takes the form of a stripe of paint on a tree or a rock, in a color that denotes the trail you’re walking. In the case of the Appalachian Trail, it’s a white stripe, painted vertically, and it’s what I was looking for on the side of the highway to find my way to the trail. The blaze is also what you’re looking for if you accidentally wander off onto a deer path, or otherwise find yourself lost in the woods. 

All along the trail, I was searching for a metaphor for the work I’d been doing this past year, and right there at the beginning, I thought it might be about finding the blaze. As I hiked for two days, through terrain that was much tougher than I’d anticipated, I lost the trail at a couple of points. Late on day one, miles behind my goal and with sunlight fading, I found myself standing before what looked like a cliff face with no path forward. I scanned around, and then I saw it: halfway up the cliffside, a single tree with a white stripe. It looked so far away. 

I thought that maybe this last year was about having to find the blaze — about wandering down the wrong path, losing time, burning months of savings and still having to find my way back, only to see another obstacle. That’s certainly a part of it. But it’s more than that. 

## Out Is Through

Back from that first hike, I got back to work. I started out by working on Android support, making some commits to the OpenKeychain project and testing their app with various smart card implementations. It wasn’t long before I discovered a bug. I poked at the bug all day and into the night before I realized that it wasn't just a bug in OpenKeychain. On Friday night, three days back from the trail, I wrote an encrypted email to Yubico, the maker of the Yubikey NEO, detailing a security vulnerability that would eventually become known as [CVE-2015-3298](https://developers.yubico.com/ykneo-openpgp/SecurityAdvisory%202015-04-14.html). 

Some bugs can be fixed with an App Store update. This bug was different. This bug affected devices that were in people’s pockets and on people’s keychains. I got chills when I discovered it, and the feeling didn't go away all night: I'd discovered a zero-day exploit against a widely deployed security device. Knowing you're the only one that knows a thing like that is scary. Yubico, to their immense credit, responded to my message immediately. They published a security advisory and a fix within three days, and announced a product replacement program two weeks later. 

In the meantime, I was writing more code, and continuing my way down the trail. At one point, during a four-day, 44 mile trek from the west bank of the Hudson River to a train station north of Pawling, I thought I had run into another metaphor. Watching the sunrise, I realized that I was far closer to my goal than to the place where I had started. 

<figure>
    <img src="/images/20150701-the-map.jpg" alt="A map depicting a long walk from Warwick, NY to Pawling, NY.">
</figure>

Turning back was no longer an option, and giving up didn't make sense; the nearest offramp from the trail was the very train station I was headed to. At a certain point, the metaphor would go, the best way out is through. That makes sense on the trail, but I still wasn't sure that it was the right way to think about a year spent building something. 

## The Long Path

When I started on the crypto card project, the goal was to hack away at it for six months, do a Kickstarter campaign, and let that be a referendum on whether it was a good idea. If the Kickstarter failed, the plan was to give up and do something else. 

Of course, plans sometimes have plans of their own. There were things I didn’t know at the outset, things I learned along the way, things that changed the fundamental assumptions I made about my plans. When I started out, I didn’t know everything I needed to know about the tech. I downloaded specifications and documents; I pored over them for weeks so I could learn enough to make an impact with the code that I wrote. At some point during the year, I became enough of an expert that I could spot vulnerabilities that had lurked unseen for years. I knew enough to do some good. 

I had false starts to be sure, and diversions that led to dead ends. I remember one moment in a coffeeshop in Austin, testing out an early build of [Keymaster](http://www.joeycastillo.com/notes/2014/12/10/explaining-keymaster/) with one of my beta testers. Fending off glare on a tiny screen, I struggled to peck out information on a tiny keyboard, at prompts reminiscent of Windows 1.0 dialog boxes. I knew immediately that I’d made a mistake. This wasn't the answer. I’d been walking the wrong path for weeks. Still: making that mistake and learning from it made me uniquely qualified to find the right path. 

----

A few weeks ago, my friend Mike picked up my sister and me from the town of Unionville, New York, a few feet from the border with New Jersey. We’d just spent six days on the trail; we'd walked from Pennsylvania, crossed the Delaware River, weathered heat and storms.  I imagine we both looked a bit rough around the edges. 

<figure>
    <img src="/images/20150701-the-long-path.jpg" alt="A picture of Joey and his sister on the trail.">
</figure>

“How do you feel?” Mike asked when he pulled up. 

“Like I just walked through three states,” I told him. 

“You know, we have cars for that,” he said. 

“I guess we took the long way around.” 

Sometimes you don’t know everything you need to know at the outset. Sometimes day one isn’t the right moment. At times in life, there is no shortcut to the lessons you need to learn, or the experiences you need to have to take those lessons to heart. 

Yesterday I launched a thing. It’s better than the thing I set out to do, and it works with things that didn’t exist when I set out to do it. I don't expect runaway success tomorrow, and I don't know what the future holds. 

But I know not to fear the long path, because it's what I walked to get here. 