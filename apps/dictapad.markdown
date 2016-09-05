---
layout: page
title: Dictapad 2
permalink: /apps/dictapad/
description: Case study on Dictapad, the best-in-class transcription aid for the iPad.
---

Dictapad is a [universal iOS app that aids in the transcription of long audio files](http://itunes.apple.com/us/app/dictapad/id408477445?mt=8). It's a snappy text editor with an integrated audio player that offers keyboard shortcuts to adjust playback rate, scrub back and forth and insert timestamps automatically.

First launched for the iPad in August of 2011, Dictapad received regular updates over the years to maintain compatibility and implement new features. More recently, Dictapad underwent a ground-up rewrite in Swift. This update implemented a slew of new features and made the app universal to both iPad and iPhone.

<figure style="text-align:center">
    <img src="/images/apps-dictapad-icon.png" width="200">
    <figcaption>The Dictapad icon</figcaption>
</figure>

Dictapad version 2 was released as a free update to all existing users in August of 2016. For new users, the app costs $4.99 US and is [available on the App Store](http://itunes.apple.com/us/app/dictapad/id408477445?mt=8).

## History

Dictapad was conceived in the course of transcribing and editing interviews for [The Outcomes Project](/multimedia/outcomes). The iPad with an external keyboard was an ideal device for writing, managing photo releases and maintaining the database of participants, but the task of transcribing required a Mac. I dreamed up Dictapad as a tool to help me transcribe on the iPad.

The initial functionality — a text editor with a variable-rate audio player — came together within 24 hours. UI polish and additional functionality came in the weeks that followed; after extensive testing with interviews from the project, it was released to the public in August of 2011. Between 2012 and 2015, Dictapad gained support for new features: AirPrint, Dynamic Type, customizable keyboard shortcuts and Dropbox integration, among others.

### Dictapad 2.0

Dictapad has seen consistent sales over the years, but by the summer of 2016, the app was beginning to show its age. Dictapad's core architecture was designed in the iOS 3.2 era; incremental changes notwithstanding, the app was failing to take advantage of many modern APIs that would accelerate the pace of development and make it easier to support new device classes.

I decided to rewrite Dictapad from the ground up using Swift, and to target iOS 9 as the minimum OS version. This meant cleaner support for features like high quality audio stretching, and a modern architecture to support not only iPhones and iPads, but also new multitasking scenarios like Split Screen and Slide Over.

<!-- Unlike in 2011, Dictapad 2.0 underwent a more formal beta testing process with a core group of existing Dictapad users, as well as a group of new users recruited through social media. The 2.0 update was released seamlessly to existing users in August of 2016.  -->

## User Interface Design

Dictapad uses a split view with a file list on the left and a text editor on the right.

<figure class="third" style="text-align:center">
    <a href="/images/apps-dictapad-screenshot-ios6.jpg"><img src="/images/apps-dictapad-screenshot-ios6.jpg" alt="A screenshot of Dictapad under iOS 6"></a>
    <a href="/images/apps-dictapad-screenshot-ios7.png"><img src="/images/apps-dictapad-screenshot-ios7.png" alt="A screenshot of Dictapad under iOS 7"></a>
    <a href="/images/apps-dictapad-screenshot-ios9.png"><img src="/images/apps-dictapad-screenshot-ios9.png" alt="A screenshot of Dictapad under iOS 9"></a>
    <figcaption>From left: a comparison of the main UI in iOS 5, iOS 7 and iOS 9. Click to expand.</figcaption>
</figure>

Back in iOS 5 days, the design focused on cool, dark toolbars and navigation bars, and a subtle pinstripe behind the file list. The text editor used the Optima typeface, and featured subtle gray lines over an off-white background.

When iOS 7 arrived, a redesign was undertaken to bring the art direction in line with the flatter feel of the new operating system. In addition, the typography was modified to take advantage of new Dynamic Type technology; this enabled Dictapad to follow the user's device-wide preferences for fonts and sizes.

By iOS 9, the flat design ethos was in full effect; gone were the shades of gray, and in their place, a crisp black and white design. Only the Dictapad Blue tint marks the app's few buttons and sliders. In addition, Dictapad 2 made all keyboard shortcut functions available via on-screen controls for the first time. Dictapad had been designed to be best experienced with a keyboard, but making the controls accessible to people without one was a definite usability win.

### The Icon

<figure style="text-align:center">
    <img src="/images/apps-dictapad-icons.png" alt="A side-by-side comparison of the old and new Dictapad icons">
</figure>

The original design of the icon drew inspiration from classic microcassette tapes that enabled old dictation workflows; the icon was a retro-styled tape cartridge compressed down to a square icon.

With the flatter design ethos of iOS 7-9, the icon was redesigned to maintain the same character, but with fewer of the skeuomorphic cues of the original design. Gone were the capstan holes, textured background and faux-grain overlay, along with the pixel art letterforms. In their place: a clean gradient, and a logotype set in the more friendly Gotham Rounded typeface.

The 2016 rewrite also involved designing an icon for a new extension point, the "Transcribe in Dictapad" action. This icon had different requirements: action icons are monochrome, and cannot be full-bleed since iOS places them in a white box.

<figure style="text-align:center">
    <img src="/images/apps-dictapad-icon-extension.png" alt="A screenshot of several extension point icons, including the Transcribe in Dictapad icon">
</figure>

The "Transcribe in Dictapad" icon hearkens back to the design inspiration for the original icon, the microcasette tape. It adopts a rectangular aspect ratio, while maintaining the familiar thick and thin line patterns of the Dictapad app icon. While this icon represents a completely different shape that does not appear elsewhere in the Dictapad experience, it feels of a piece with the rest of the design, which is what the extension icon needs to accomplish.

## Technologies

### Keyboard Controls

In 2011, the only way to implement keyboard shortcuts was to look for a character the user wanted to type, and interpret that as a command instead. This meant the keyboard shortcuts had to be printable characters, and Dictapad initially settled on the accent key, the backslash, the tilde and the pipe (``` ` \ ~ |```) to scrub back, scrub forward, slow down and speed up playback, respectively. Their positions at the far left and far right of the keyboard made them natural spots for these shortcut actions.

In modern iOS, the UIKeyCommand API makes first-class keyboard shortcuts a reality, and Dictapad 2 takes advantage of this: the modern keyboard shortcuts are ```Control``` + ```Left``` / ```Right``` / ```Up``` / ```Down```.

<figure style="text-align:center">
    <a href="/images/apps-dictapad-screenshot-tutorial.png"><img src="/images/apps-dictapad-screenshot-tutorial.png" alt="A screenshot of the tutorial screen in Dictapad"></a>
    <figcaption>The new tutorial screen in Dictapad 2.</figcaption>
</figure>

To avoid impacting existing users' workflows, an option was added to preserve the legacy keyboard shortcuts. This option was automatically enabled for users upgrading from Dictapad 1, while users new to Dictapad 2 got the modern shortcuts by default. In addition, a new tutorial screen educated users about the new options available to them in Dictapad 2.

### Workflow Integration

Dictapad is a simple tool that's meant to fit snugly into a larger workflow. To this end, it has to be dead simple to get audio in, and get documents out.

Dictapad 2 adds a "Transcribe in Dictapad" extension point for importing voice notes directly into the app. You can AirDrop files to Dictapad from an iPhone, iPad or even a Mac. It supports Dropbox, iTunes File Sharing, import from the iPad's music library, and from any app that uses the iOS standard sharing sheet. This means that from the iPad's mail app and a number of iPad voice recorders, getting audio into Dictapad is as simple as tapping your audio file and selecting Dictapad from the resulting list of apps.

Dictapad also supports getting your transcriptions out quickly and easily. Dictapad uses the iOS document interaction API to offer a text file to Notes, Pages, PlainText, Byword, or your favorite iPad text editor.

<figure style="text-align:center">
    <a href="/images/apps-dictapad-screenshot-airprint.png"><img src="/images/apps-dictapad-screenshot-airprint.png" alt="A screenshot of the print dialog in Dictapad"></a>
</figure>

Printing is a natural feature for a document-based app, and Dictapad is no slouch here. Dictapad's printouts are clean and well designed, going above and beyond what most iPad text editors offer. Printouts include page numbers and other basic information in a header on each page. They also offer space for custom header text, such as a project name or a copyright notice — that can be changed in Settings.

## Conclusions

This is by far the longest app writeup on my website, but it's also the longest-running app I have on the App Store. Dictapad is a good example of the evolution of a utility application on the App Store: evolving with the times, publishing compatibility updates, implementing features, and eventually paying down technical debt. The 2016 release of Dictapad 2.0 — published five years to the day after its introduction — is a solid foundation for the future of Dictapad. I look forward to updating this page again in the future.
