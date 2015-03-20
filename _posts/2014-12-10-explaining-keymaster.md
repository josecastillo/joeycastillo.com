---
layout: post
title: Explaining Keymaster — The What and Why of Crypto
description: Crypto keys protect your stuff. When you trust other people to hold them, it makes it easier for spouses to snoop and for hackers to steal your snaps. I'm building Keymaster to put your keys into your hands. 
category: notes
tags: [the crypto project]
image:
  feature: 20141210-keymaster-banner.jpg
  credit: Joey Castillo
---

This is long, and I was told I needed a TL;DR, so here it is: **Crypto keys protect your stuff, but right now you're trusting other people to hold on to those keys.** This makes it easier for spouses to snoop and for hackers to steal your sexy snapchats. I'm building a machine that puts your keys in your hands, and keeps them out of everyone else's. 

That's the gist. But I encourage you to read the whole thing; one of the points of this project is to demystify crypto, and I'm hoping this blog post is a start. 

---

If you follow me on Facebook or Instagram, you've probably seen me post about an strange boxy looking machine I built called "Keymaster". When I posted the photo, a friend of mine asked "WHAT IS THIS", and I realized that I my answer wasn't terribly easy for the layperson to understand. This blog post aims to fix that. 

<figure>
    <img src="/images/20141210-keymaster-hero.jpg" alt="A photograph of the Keymaster machine from above. The machine has two USB ports on top labeled 'Red USB' and 'Black USB', along with a credit card sized slot labeled 'Card'.">
    <figcaption>I promise you'll understand this thing by the end of this blog post.</figcaption>
</figure>

The internet is a dangerous place for personal information. Sure, there's encryption on the internet that protects things in transit — it would be difficult ([but not impossible](https://github.com/thebradbain/snapception)) for someone to intercept a selfie while you're sending to Snapchat. But once your selfie makes it to Snapchat's servers, it's stored unencrypted while it waits for your recipient to download it. Even services that promise to encrypt your stored data, like Dropbox, encrypt it in a way where Dropbox holds the keys. And that's before we even talk about email; generally speaking, email gets zapped around and stored totally unencrypted, waiting only for a [rouge IT guy](http://www.smh.com.au/it-pro/business-it/email-snooping-it-admins-like-dracula-in-charge-of-the-blood-bank-20120413-1wxnu.html) or a [pervy spy](http://arstechnica.com/tech-policy/2014/07/snowden-nsa-employees-routinely-pass-around-intercepted-nude-photos/) to peep in. 

We're uploading more and more of our lives to the internet, and bad people want in on that. From creepy hackers [stealing snapchats](http://www.thedailybeast.com/articles/2014/10/13/the-snappening-is-real-90k-private-photos-and-9k-videos-hacked-and-leaked-online.html) and [nude photos of celebrities](http://www.independent.co.uk/news/people/news/jennifer-lawrence-naked-photos-leak-more-celebrities-targeted-as-third-wave-of-hacked-images-is-released-9760393.html?origin=internalSearch) to significant others that [snoop on your emails](http://nymag.com/thecut/2014/01/15-people-on-snooping.html), this isn’t hypothetical: there are real world threats, today, to your personal information. You need good crypto to protect your stuff. The challenge is locking down your stuff while still giving you easy access. And so far, the answer to that challenge has been pretty crappy: it's been to just let someone else hold the keys. 

## Hang on: what are keys?

For the most part in this article, we're going to talk about somehting called *public-key cryptography*. Sorry for the jargon; I'll try to keep it as jargon-light as possible. We call it public key crypto because a key is divided into two parts: the public part or *public key*, and the secret part or *secret key*. The keys are just some big fancy numbers, cooked up using [some really clever math](http://en.wikipedia.org/wiki/RSA_(cryptosystem)) that was invented in the 1970s. 

<figure>
    <img src="/images/20141210-key-generation.jpg" alt="A whiteboard diagram showing how math creates a secret part, then math creates a public part from the secret part. Finally, the diagram notes that the public part and the secret part, taken together, represent your key." unused="BEWARE: MATH INCOMING! Basically we generate a bunch of reeeeeally big random numbers until we find two that are prime; we'll call them p and q. Keep those a secret. We multiply them together, p×q, to get a number called n, which is basically your public key. There's some other math involved; your public key also includes another number called e, but everyone uses the same one these days. There's some more math involving p, q and e to generate another secret called d, but the gist is that p and q are secret, and n is public.">
    <figcaption>Red parts are secret; black parts are public. It's not much more complicated than this.</figcaption>
</figure>

Once you have a key that's set up this way, your computer can use some more clever math to do some really neat things. What kind of neat things? Three in particular are pretty great: 

1\. **Encryption** - Let's say you want to send a sexy sext to Boyfriend. Like we mentioned earlier, if you send *sexy.jpg* over Snapchat, it's stored in a way that anyone who hacks Snapchat can steal your photo. But with encryption, you can do this: 

<code>MATH(sexy.jpg, boyfriend's public key) => sexy.gibberish</code>

And out the other end pops a file that only boyfriend can decrypt. You could post this file in public to Facebook, and nobody would be able to decrypt it. Boyfriend, on the other hand, can do this:  

<code>MATH(sexy.gibberish, <span style="color:red">boyfriend's secret key</span>) => sexy.jpg</code>

As long as Boyfriend is the only one holding that secret key, he's the only person in the world that can do that. 

2\. **Signing** - Little known fact: anyone on the internet can forge an email to look like it's from anyone else. It's true: the "From" line you see in your email program is based on the honor system. So it should be no surprise that hackers steal tons of passwords just by faking an email from Bank, and asking people to give them their Bank password. But here's a cool thing that Bank can do with public key crypto: 

<code>MATH(email, <span style="color:red">bank's secret key</span>) => signed.email</code>

Unlike the first example, there's no encryption here; the email comes through just like a regular email. But with a signed email, your mail app can do this: 

<code>MATH(signed.email, bank's public key) => verification</code>

This verifies that Bank's email actually came from them; now your mail app can display a soothing blue checkmark, and tell you everything is okay. As long as Bank is the only one holding their secret key, no hacker can ever fake a signed email from Bank. 

3\. **Authentication** - This one is a lot like signing — it even uses the same math — but it's pretty cool in its own right. When you want to log into a website today, you give it a password. If a hacker [guesses your password](http://www.nytimes.com/2010/01/21/technology/21password.html), or [snoops it from over your shoulder](https://en.wikipedia.org/wiki/Shoulder_surfing_(computer_security)), or [steals it over a coffeeshop wifi connection](https://medium.com/matter/heres-why-public-wifi-is-a-public-health-hazard-dd5b8dcb55e6), Bad Things happen. Public key crypto can help here too. When you want to log into Website, and Website has your public key, it can issue you a challenge. You take that challenge, and do this: 

<code>MATH(challenge, <span style="color:red">your secret key</span>) => response</code>

Then Website can do some math of its own: 

<code>MATH(response, your public key) => verification</code>

Again, as long as nobody else is holding your secret key, nobody else can log in to Website as you. And even if the coffeeshop hacker sniffs out everything, it wouldn't help them to log in as you later; the next time hacker visits Website, Website will send a new challenge; the old response is worthless without the secret key that created it. 

## Sounds good! What's the catch? 

Here's the problem with crypto keys: making them is complicated, and using them is complicated. The most popular way to protect a key that lives on your computer is to encrypt it with a long passphrase, meaning that several times a day you'll have to type in a long, complicated, fairly random phrase that you've memorized before being allowed to read your email. 

Using passphrases safely is an even bigger problem. If bad software gets on your computer, it can steal your encrypted keys, and then it can log all your keystrokes to capture your passphrase. Once a hacker has your keys and knows your passphrase, he can decrypt all your sexy sexts; he can forge spammy emails from you; and he can log on to all the websites you were trying to protect. 

Bummer. 

This leads to all the crazy security arcana that you saw in this season of the Newsroom or in CITIZENFOUR, where you go and buy a laptop that you never connect to the internet. Suddenly you find yourself carefully moving encrypted files back and forth on thumb drives, and covering your keyboard with a blanket when you type in your passwords, because someone might be watching, or there might be a security camera, or hey, you know what, the Internet is a dangerous place, and you never know. 

<figure>
    <img src="/images/20141210-blanket.jpg" alt="Next to a christmas tree, the author types on his laptop while covered head-to-hands with an oversized hoodie.">
    <figcaption>Welcome to the future! It's not that bad, I promise...</figcaption>
</figure>

In reality, long before you reach this point you'll have probably decided that good crypto is just too complicated, and maybe we'll just have to live in a world where we know that all our sexy sexts will eventually end up on CNN when we decide to run for president. 

Me, I disagree with that. Good crypto is essential to modern life, and you deserve to be the one holding your keys. It's up to technologists like me to design systems that make that possible. Which brings us to — 

## Keymaster: How We Give People Their Key

Keymaster is a system designed to generate keys for people and put them on a smart card. Hey, sorry, jargon again! A smart card is a little computer that fits on a credit card. Some of your credit cards might be smart cards; you'll recognize the little metal bit on the left side. You may have also used them to get into a hotel room, or to pay at a laundromat; lots of laundry places use smart cards instead of quarters. 

<figure>
    <img src="/images/20141210-smartcards.jpg" alt="A pile of smart cards on the left; one has the logo of the Clean-Rite Laundry Center; another depicts instructions for opening a hotel room door. On the right is a smart card labeled 'G N U P G'.">
    <figcaption>The cards on the left are smartcards; the card on the right is smarter.</figcaption>
</figure>

You can program a smart card to do all kinds of things, but in this case, you can program a card like this one to hang onto those secret keys, and to do all the MATH from above that dealt with secret stuff. What this means is once you put your secret keys on a smart card, you can still use them, AND there's no way for anyone to steal them. You can use your card to decrypt sexy.jpg, to sign emails to your stock broker, to log on to websites. It's like chip-and-pin for crypto. Passphrases are complicated, but everyone understands a card and a PIN. And some smart cards, like the ones I want to put in people's pockets, can communicate wirelessly with your cellphone and do MATH without even being plugged in. 

The details of how to build a Keymaster and how to use it are probably too big for this post; it's already pretty long. But the idea is that it's a tool that someone knowledgable can use to guide you through the process of making your keys, putting them on a card, and backing them up in case you lose the card. It's a tool for putting your keys in your hands, in a form that's so easy to use it's like plugging in headphones. 

<figure>
    <img src="/images/20141210-keymaster-output.jpg" alt="">
    <figcaption>The output from Keymaster. The red things hold your secret keys; you keep all of them.</figcaption>
</figure>

When you use Keymaster, you walk away with the only copies, and all the backups of your secret things. The card uses a 4-6 digit PIN for day to day crypto, which you can change if someone discovers it; and even if someone has your PIN, the card will never give up your secret keys. No blankets required. 

## I have my keys. Now what? 

Immediately? The keys are an open standard, and the card works with gnupg and Enigmail, the encrypted email plugin. You can use your card to encrypt files on your hard drive. You can send encrypted emails to anyone who has crypto keys of their own. 

Admittedly, there aren't a lot of those, especially among people you know. And there are basically no websites at all that use this method for authentication. It's a network effect problem: not enough people use them because not enough people have them, and not enough people have them because not enough people have them. Keymaster is an attempt to change that. I want to get these cards in the hands of everyone I know, and everyone they know and everyone they know. Keymaster is an attempt to get more people in control of their cryptographic destiny. 

Once everyone is holding their own secure keys in their wallet or purse, technologists like me can start building tools that you can actually use, tools that can better protect your information. In your lifetime you're going to upload a lot more of yourself to the internet. You deserve better control of that information, and the first step in that process is putting the keys to your stuff in your hands, and yours alone. 