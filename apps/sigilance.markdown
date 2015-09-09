---
layout: page
title: SIGILANCE OpenPGP Smart Card
permalink: /apps/sigilance/
description: Information about the SIGILANCE OpenPGP Smart Card.
---

In 2014, I began working on a concept for secure cryptographic key generation via small, purpose-built systems. After testing and iterating on the concept, this evolved into SIGILANCE, an NFC-enabled OpenPGP smart card that brings smart card cryptography to mobile devices at a lower price point than existing solutions. 

<figure>
    <img src="/images/20150701-the-card.jpg" alt="A product shot of the SIGILANCE OpenPGP Smart Card, sitting on top of an RFID-blocking sleeve for the same.">
    <figcaption>The SIGILANCE OpenPGP Smart Card.</figcaption>
</figure>

## The Case for Smart Cards

PGP was designed in the early 1990s, a time when many people owned only one computer that spent most of its time offline. Back then, it was sufficient to store cryptographic keys on that computer and protect them with a passphrase. Times have changed, however. Today, people are much more likely to own multiple devices such as a smartphone, a tablet and a laptop, and it's safe to assume that they all have a persistent, always-on connection to the Internet. A user who wants to access their encrypted email on all of their devices would have to store their cryptographic key file on all of those devices, and type their passphrase into each of these devices. This dramatically increases the surface area available to an attacker seeking to compromise those keys. 

The OpenPGP smart card, first specified in the early 2000s, was a solution to this problem. A smart card with cryptographic capabilities can function as a secure, air-gapped system that is capable of securely storing cryptographic keys and performing cryptographic tasks without disclosing the keys to a host machine. Since the initial publication of the specification, several manufacturers have created OpenPGP smart cards and compatible security tokens. But until recently, these smart cards only worked with desktop operating systems via USB smart card readers. 

<iframe src="https://player.vimeo.com/video/135714967" width="500" height="281" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

The SIGILANCE OpenPGP smart card includes a traditional contact-based interface, which makes it compatible with PC operating systems via a smart card reader. The key innovation is that it also includes an NFC interface, which makes it compatible with Android smartphones and tablets with NFC functionality. While some high-end security tokens have incorporated an NFC interface, the SIGILANCE OpenPGP Smart Card is the first NFC-enabled card to support OpenPGP, and it does so at a lower price point than any product currently on the market. 

## Software Support: OpenPGP on Mobile

In early 2015, the open source Android project OpenKeychain began implementing support for the Yubikey security token via NFC. At least initially, the support was limited to signing and decrypting messages; administrative tasks like generating keys for the token still needed to be done on a desktop machine. 

I applied my knowledge of the OpenPGP specification to make some substantive contributions to that project, including functionality for changing card data and PINs, and for moving cryptographic keys from the Android tablet onto a smart card. As of mid-2015, you can generate an OpenPGP identity on an Android tablet and move it to an NFC-enabled smart card, all through an intuitive graphical user interface rather than a complex command-line interaction. 

<figure class="half">
	<a href="/images/apps-sigilance-cardedit-screenshot-1.png"><img src="/images/apps-sigilance-cardedit-screenshot-1.png"></a>
	<a href="/images/apps-sigilance-cardedit-screenshot-2.png"><img src="/images/apps-sigilance-cardedit-screenshot-2.png"></a>
	<figcaption>Screenshots of the SIGILANCE CardEdit app for Android.</figcaption>
</figure>

In addition to my contributions to OpenKeychain, I also implemented a small utility app called SIGILANCE CardEdit, which allows users to edit the metadata stored on their OpenPGP smart card in a manner similar to the GnuPG card-edit facility. 

## Security Audit

While evaluating existing open source implementations of the OpenPGP smart card standard, I was able to identify a critical vulnerability ([CVE-2015-3298](https://developers.yubico.com/ykneo-openpgp/SecurityAdvisory%202015-04-14.html)) in the javacardopenpgp applet that affected the Yubikey NEO. I disclosed this vulnerability to the manufacturer of the vulnerable devices and offered a fix, they implemented this fix and announced a product replacement program in April of 2015. 

## Design and Branding

I designed the logo and visual identity for SIGILANCE myself; while I am mostly a software engineer, I thought that good design would be imperative to get widespread adoption of a device like this. The SIGILANCE smart card design incorporates a clean look without extraneous logos or branding. A hologram on the face of the card serves the dual purpose of showing that the card is genuine, and displaying the card's unique serial number. 

The face of the card also incorporates space for the two most important bits of information for most people who use OpenPGP's Web of Trust: your identifying information, and the key fingerprint tied to your identity. If you've ever signed someone's key or asked someone to sign your key, these are the two essential bits of data required for that task. You can either write on the card with a permanent marker, or print out a label and stick it on. 

## SIGILANCE going forward

[SIGILANCE OpenPGP smart cards are available for purchase](https://www.sigilance.com/store/) at the SIGILANCE website. In addition to compatibility with the GnuPG ecosystem on the desktop, the cards work with Android devices using the OpenKeychain software for key management and the K-9 mail app for secure email. Robust [documentation](https://www.sigilance.com/documentation/) also exists for a number of workflows and key management scenarios. 