---
layout: post
title: "Of Crescent Moons and Calendars, or, Anatomy of a New Feature"
description: When a cloudy day in Mecca broke calendars around the world, I had to implement the most interesting feature request to ever hit my inbox.
category: notes
tags: [app stuff]
image:
  feature: 20160918-crescent-banner.jpg
  credit: Joey Castillo

og_image: images/20160918-moonrise-og.jpg
og_image_type: image/png
og_image_width: 640
og_image_height: 400

---

Of all the apps I've written, Better Day may just be my favorite. On the one hand, it looks dead simple: it's a calendar, an app that shows the days of the month in a grid. But like most things that look simple, there's complexity lurking just below the surface. For one thing, the app is translated into 21 languages, supports 16 calendar systems and operates in more than 30 time zones — the 24 you expect, along with places like Newfoundland, which offsets its time by two and a half hours, and Nepal where the time is offset by 5:45. If you're in Kathmandu on December 31, your calendar would be ringing in the new year at 6:15 GMT. 

Spend enough time reading Apple's date and calendar documentation, and you'll find gems like this: 

> **startOfDay(for date: Date)** - Returns the first moment of a given Date. If there were two midnights, it returns the first.  If there was none, it returns the first moment that did exist.

Better Day launched last October, and it's been chugging along telling people the date for almost a year now without incident. Until this month, when I received a couple of messages from users of the Islamic calendar. Paraphrasing: 

> It is known that the Islamic calendar follows the moon phases and not the sun. This means that occasionally, the date will change suddenly at the end of the month. This month it happened. It has been announced that today is 11/30/1437, not 12/1/1437. Usually, Islamic calendar apps give users the option to fix this by adding or subtracting a day as a manual fix. 

Forget leap seconds: this has to be the most interesting edge case in Better Day. The start of the month in the Islamic calendar depends on the sighting of the first crescent moon. If you think this sounds complex, you'd be right: historically, different regions could easily disagree on the date, depending on the local time of the moonrise and its phase when it dipped below the horizon. 

<figure>
    <img src="/images/20160918-moonrise.jpg" alt="A crescent moon rises above Masjid Khadijah Bint Khwailid in Austin, Texas.">
    <figcaption>A crescent moon rises above Masjid Khadijah Bint Khwailid in Austin, Texas. File photo by Joey Castillo.</figcaption>
</figure>

Nowadays, most of the world agrees on the *Umm al-Qura* calendar, which synchronizes on the sighting of the first crescent moon in Mecca. Still, a cloudy day in the right part of Saudi Arabia can delay the sighting of the crescent moon — and [that seems to be what happened this month](http://www.aljazeera.com/news/2016/09/eid-al-adha-2016-160901181404738.html). 

## A change in three parts

Armed with a clear understanding of the problem (date is off by one), and a clear understanding of the solution (add a date offset feature), I implemented the fix. And as I worked, it occurred to me that this was the perfect kind of feature to dissect: big enough to be interesting, yet small enough to explain clearly. 

<figure>
    <img src="/images/20160918-threeweeks.png" alt="Twenty-one screenshots of the Better Day calendar. The calendar is correct on Thursday, Dhu'l Qi'dah 29, but incorrectly displays Friday as Dhu'l Hijjah 1.">
    <figcaption>The problem. When Dhu'l Qi'dah got extended by a day, Saturday became the 1st of Dhu'l Hijjah, not the 2nd. The displays in red are all incorrect.</figcaption>
</figure>

So here it is: the anatomy of a new feature in three parts. The goal: create a methodology to make the app display 12/1 even if the OS thinks it's 12/2. 

### 1. Figure out where we need to adjust the date

Fir starters, we create a new method on the ```Date``` called ```adjustedDate``` that doesn't do anything. 

```swift
extension Date
{
    func adjustedDate() -> Date
    {
        return self
    }
}
```

We make sure to use it whenever we want to display an adjusted date, for example, in the complication that displays "SAT 9/2": 

```swift
let firstLine = calendarDataSource.twoLineWeekdayForComplicationWithDate(date)
let secondLine = calendarDataSource.twoLineMonthAndDayForComplicationWithDate(date.adjustedDate())
complication.line1TextProvider = CLKSimpleTextProvider(text: firstLine)
complication.line2TextProvider = CLKSimpleTextProvider(text: secondLine)
```

In this case, we want to avoid adjusting the date when displaying the weekday — Saturday didn't become Friday when this change was announced — but we do want to adjust the month and day, since the 2nd did become the 1st.

Again though, this change doesn't actually do the thing. It just makes clear **where** we want to do the thing. If in the future I need to revisit this change, or someone else takes over the codebase and needs to understand what was going on, having this checkpoint in the code will help. 

### 2. Add setting for date adjustment

If we're going to offset the date, we need for the user to be able to set that offset, and we need to have a place to store that offset. Not going to bog you down in code too much; suffice it to say that we make a new setting called ```SettingsManager.dateOffset``` that holds on to the number of days to add or subtract. We also add a new sceeen that lets the user pick a date offset: 

<figure>
    <img src="/images/20160918-settings.png" alt="A screenshot of the new settings screen, and the date offset selection table.">
</figure>

This kind of interface is very common; when you load it, it asks the settings manager for the current date offset and highlights that row; then, when you tap one of the rows, it tells the settings manager that there's a new dateOffset. 

### 3. Implement date offset method

Finally, we get to implement the change. In Apple's date framework, we have a concept called "date components". Think of ```DateComponents``` as a box that can hold the concept of a day or two weeks, eight hours or ten years — basically any subdivision of time in the abstract. It can do other things too, but for our purposes, we can use it to add or subtract a day from the current date. 

```swift
func adjustedDate() -> Date
{
    let calendar = CalendarDataSource.sharedInstance.calendar
    var components = DateComponents()
    components.day = SettingsManager.dateOffset
    return calendar.date(byAdding: components, to: self) ?? self
}
```

A naïve implementation might try to figure out the number of seconds in a day and add that to the date, but as we discussed earlier, dates are finicky beasts. What if today had 23 hours? What if there was a leap second yesterday? Better to trust the calendar to do the work for us; it knows. 

## Testing and Shipping

Final steps: we run our unit tests; if those look good, we bundle up a build and send it to TestFlight, which sends it out to the loyal group of Better Day beta testers. After some testing and some tweaking I submitted Better Day 1.15 to the App Store. 

<figure>
    <img src="/images/20160918-threeweeks-fixed.png" alt="Twenty-one screenshots of the Better Day calendar. The calendar is correct on Thursday, Dhu'l Qi'dah 29, displays a blank day on Friday, and shows Dhu'l Hijjah 1 on Saturday.">
    <figcaption>The Better Day 1.15 fix. I can't extend Dhu'l Qi'dah by a day, but I can fix the rest of Dhu'l Hijjah from the 1st onward.</figcaption>
</figure>

In addition to some new features for watchOS 3 — and an unrelated fix for an problem with weekdays in Australia that's a story of its own — there's this line in the change log: 

> This version of Better Day adds a "Date Offset" feature to the Calendar & Language section of the app settings. This is intended for use with lunar calendars like the Islamic calendar, where the actual date can be offset from the expected date due to differences in observed lunar phase. 

And that's how a new feature gets made. 

**Errata:** _The code snippets presented here are simplified somewhat from their real-life counterparts, as I wanted to make this article accessible to non-technical readers. I also simplified the development process just a bit; this is how I built the feature, but finalizing the behavior did require adjustments based on feedback from the beta test group._
