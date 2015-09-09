---
layout: post
title: "Weekend App: TrainFace"
description: A blog post about a weekend project. TrainFace displays New York City subway status on your iPhone and Apple Watch.
category: notes
tags: [app stuff]

og_image: images/20150809-trainface-og.png
og_image_type: image/png
og_image_width: 640
og_image_height: 400

---

From a technical standpoint, my biggest skillset is in iOS development. Nonetheless, it occurred to me last week that I don't have a terribly recent iOS project to show. As a consultant I wrote a ton of great code that solved my clients' problems — but all that code stayed with my clients. The SIGILANCE card was my big personal project this year, but for that I was working mostly in JavaCard and Android. I very recently published the latest [Bushwick Open Studios app](http://www.joeycastillo.com/apps/openstudios/), but even that was maintenance on a codebase I started in 2013. It's still a solid app; it's just not something new, and I was feeling the itch this weekend to make something new. 

So I made TrainFace, a simple app that displays the status of the New York City subway system in an iPhone app, an Apple Watch app and a custom Apple Watch complication. I spent half of Saturday and half of Sunday on it, and you can [check it out on GitHub here](https://github.com/josecastillo/TrainFace). 

## Screenshots

<figure class="third">
	<a href="/images/20150809-trainface-phone-1.png"><img src="/images/20150809-trainface-phone-1.png"></a>
	<a href="/images/20150809-trainface-phone-2.png"><img src="/images/20150809-trainface-phone-2.png"></a>
	<a href="/images/20150809-trainface-phone-3.png"><img src="/images/20150809-trainface-phone-3.png"></a>
	<a href="/images/20150809-trainface-watch-1.png"><img src="/images/20150809-trainface-watch-1.png"></a>
	<a href="/images/20150809-trainface-watch-2.png"><img src="/images/20150809-trainface-watch-2.png"></a>
	<a href="/images/20150809-trainface-watch-3.png"><img src="/images/20150809-trainface-watch-3.png"></a>
	<figcaption>Screenshots from the TrainFace app and Apple Watch app.</figcaption>
</figure>

The rest of this post walks inch by inch through creating the app, linking to commits and showing screenshots at every stage. It's fun to see how things get made, right? 

*Note to non-technical readers: a "commit" is sort of like a checkpoint in the process of writing code. I have links to these checkpoints throughout, but you don't have to click on them; I explain what the code does right here in the post.*

### 2:40 PM: First Commits

Every app has to start somewhere. In this case, the [first commit](https://github.com/josecastillo/TrainFace/commit/ea06a811c40b99c90140a7582bad23c57e83da25#diff-4a51cc075df792504391911abd94cf79R14) is the most basic of basic iOS apps: a list view and a detail view. That's not very exciting though, so in the [second commit](https://github.com/josecastillo/TrainFace/commit/48bdbad283fae7758c295fd4ff0a3805d0d25a5d), I add some fake data to make it more interesting. 

<figure class="third">
	<a href="/images/20150809-trainface-process-01-01.png"><img src="/images/20150809-trainface-process-01-01.png"></a>
	<a href="/images/20150809-trainface-process-02-01.png"><img src="/images/20150809-trainface-process-02-01.png"></a>
	<a href="/images/20150809-trainface-process-02-02.png"><img src="/images/20150809-trainface-process-02-02.png"></a>
	<figcaption>Left: what the app looks like after the first commit. Middle and right: with some fake data.</figcaption>
</figure>

The next few commits aren't much more to look at. Since you'll probably want to prioritize the trains near work and home, I added support for reordering train lines. Also a label telling you when the data was last updated; boring, but necessary. The next commit is fun, though. 

### 4:03 PM: Images and Colors

Given how colorful the screenshots are at the top of the post, you might be surprised to find out that there's not a single image file embedded in the app. Commit number five adds support for generating subway icons right in the code. The whole shebang is a [57-line method](https://github.com/josecastillo/TrainFace/blob/master/TrainFace/Classes/View/UIImage%2BTFSubwayLine.m#L15) in a category on UIImage. We look up the color of the line based on [the MTA style guide](http://web.mta.info/developers/resources/line_colors.htm), then use Core Graphics to draw the thing ourselves. Later, we'll use this same method to generate assets for the Apple Watch app. 

I've always been a huge fan of drawing art in code rather than embedding tons of images; with the explosion of form factors and resolutions, it's not uncommon to have to embed dozens of PNGs for even a simple app. This app requires icons for 21 subway lines in three resolutions for two devices. Being able to do that with zero assets is a massive win. 

[Commit number six](https://github.com/josecastillo/TrainFace/commit/a71994c978986d7dc38dea26adaded9014660791#diff-4a2ad0fd3a67a2124a82a652bbff1d9eR1) adds a splash of color to the main view, with color codes for the various levels of frustration a straphanger is likely to encounter. By this commit, the app is starting to look like a real app; all that's missing is real data. 

<figure class="third">
	<a href="/images/20150809-trainface-process-05-01.png"><img src="/images/20150809-trainface-process-05-01.png"></a>
	<a href="/images/20150809-trainface-process-06-01.png"><img src="/images/20150809-trainface-process-06-01.png"></a>
	<a href="/images/20150809-trainface-process-07-01.png"><img src="/images/20150809-trainface-process-07-01.png"></a>
	<figcaption>Left to right: adding images; adding colors; connecting to live data feed (note the timestamp).</figcaption>
</figure>

With the [last commit on Saturday](https://github.com/josecastillo/TrainFace/commit/923ba79e9c3ca646730de0a3e29f3682e52855ea#diff-268e2f98ef94cb77f914011af3325246R27), we move from mock data to real data. In the rightmost screenshot above, the app is connecting to a JSON feed generated right here on my website. It's based on [the MTA service status API](http://web.mta.info/status/serviceStatus.txt), but has some clever logic to parse out the status of individual train lines, and to boil long service advisories down to short, one-sentence summaries. That's for another blog post, though! 

### Sunday, 1:49 PM: The Apple Watch app

After getting the app to connect to a live data feed on Saturday, it feels like a step backwards to make an Apple Watch extension filled with fake data. But in a lot of ways, the Apple Watch extension is an app all its own; you have to start from the beginning. In [the first commit of the Apple Watch extension](https://github.com/josecastillo/TrainFace/commit/7e4bc9ae38668343c4d0fa88ada8fa6ea8f267ca#diff-d435a431556a867d8e2912f2367538bdR23), I simulate a bad day at 14th and 6th: 

<figure class="third">
	<a href="/images/20150809-trainface-process-11-01.png"><img src="/images/20150809-trainface-process-11-01.png"></a>
	<a href="/images/20150809-trainface-process-11-02.png"><img src="/images/20150809-trainface-process-11-02.png"></a>
	<figcaption>This interface (left) doesn't do much. When you tap it, it taps (right). </figcaption>
</figure>

The [next commit](https://github.com/josecastillo/TrainFace/commit/dc980d493fadfcf35951023bdf4c586c3470a0cf#diff-1e8873ed200c9d086d9241a0b18377afR64) adds commands to fetch live data and icons; all of a sudden, the app is starting to look like something real: 

<figure class="third">
	<a href="/images/20150809-trainface-process-12-01.png"><img src="/images/20150809-trainface-process-12-01.png"></a>
	<a href="/images/20150809-trainface-process-12-02.png"><img src="/images/20150809-trainface-process-12-02.png"></a>
	<figcaption>Scrolling through the list of service status indicators. Useful already! </figcaption>
</figure>

### 8:30 PM: Complications

There was a fair amount of sketching out designs for [commit number thirteen](https://github.com/josecastillo/TrainFace/commit/63e513d5ad0e06738b8c3b1922c8d2fdf17397ff#diff-843e4ae763dab7e3fd5d5a0fd79dc520R17). A "complication" is fancy word for a custom bit of information you display on the face of your watch. Complications are new to WatchOS 2, and they come in different shapes and sizes, from a tiny icon in the corner to a big centerpiece panel. For the moment, the app only supports one style of complication, the big one, which gives us three lines of text to work with. The app attempts to summarize as much as it can in those three lines: 

<figure class="third">
	<a href="/images/20150809-trainface-process-13-01.png"><img src="/images/20150809-trainface-process-13-01.png"></a>
	<a href="/images/20150809-trainface-process-13-03.png"><img src="/images/20150809-trainface-process-13-03.png"></a>
	<a href="/images/20150809-trainface-process-13-02.png"><img src="/images/20150809-trainface-process-13-02.png"></a>
	<figcaption>Left, selecting the complication. When there is a disruption (middle), the complication displays it in the center line. When there are more (right), the complication discards unnecessary lines to make room.</figcaption>
</figure>

Known issue: when switching from the two-line to the three-line table, the font weight changes. Not wild about that. Hey, it's a first draft. 

### 9:25 PM: Last Looks

Rounding out the functionality, it was imperative to [implement a detail view](https://github.com/josecastillo/TrainFace/commit/693432f6bbf13e09693fccb034bc4a0f3653ae0d#diff-c83330ee0e9ec23a28cd3a36d56072a2R17) for the Apple Watch interface; there's no sense telling someone that there's a service change unless you can explain what that service change is. 

<figure class="third">
	<a href="/images/20150809-trainface-process-14-01.png"><img src="/images/20150809-trainface-process-14-01.png"></a>
	<a href="/images/20150809-trainface-process-14-02.png"><img src="/images/20150809-trainface-process-14-02.png"></a>
	<a href="/images/20150809-trainface-process-14-03.png"><img src="/images/20150809-trainface-process-14-03.png"></a>
	<figcaption>Three different disruptions.</figcaption>
</figure>

When the MTA publishes disruptions, they publish based on the trunk line that is disrupted; most apps that consume MTA data can only tell you that the ACE is disrupted. Since my feed can parse out disruptions to specific trains on the line, we're able to show the disruption for the A separately from the disruption for the E. We're also able to show only the most relevant information to the user; a one-sentence summary of the issue is a huge usability win when you're glancing at your wrist. 

Additional commits later in the evening add support for background refresh and implement refresh logic for the complication, but by 9:25 PM, the weekend app is done. 

## Closing Thoughts

It's nice to have a reminder that you've still got it. This weekend app reminded me how fun it is to code for iOS, and introduced me to some bleeding-edge features that aren't even out of beta yet. Is it a polished app? Of course not. But it shows what I'm capable of doing in a couple of days.

Now that the crypto project is launched and out in the world, I'm excited to get back into iOS development. It's where I live. It's what I'm great at. 