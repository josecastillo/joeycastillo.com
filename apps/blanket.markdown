---
layout: page
title: Blanket
permalink: /apps/blanket/
description: Information about Blanket, a concept for a secure messaging app.
---

Blanket was a concept for a secure messaging app based on the in-person exchange of conversation-specific public keys. It was essentially a proof of concept for a simplified trust model, empowering users to generate and exchange trusted keys and credentials directly, via QR codes. It then enabled secure one-to-one text messaging using the libsodium library for public-key cryptography, and the iOS keychain for storing secrets. 

Blanket is open source and [the repository is available on GitHub](https://github.com/josecastillo/blanket/). The README puts it best: "this is my first attempt a cryptography app, so take it for what it is: an attempt to explore some ideas, but not yet a bulletproof cryptography system." 

## Blanket's Goals

 * **Security** — Messages in Blanket are encrypted on the client side, and stored on the server in a manner that only the recipient can decrypt. The blanket server merely accepts ciphertext from the client; it does no encryption or validation of its own, and never sees the clients' keys or any identifying information. 
 * **Loose identity** — Messages are cryptographically signed, but the keys used for encrypting and signing are generated per-conversation, not per-person. Thus, cryptographic keys are tied to a _relationship_, not an _identity_. Alice's secret key for talking to Bob is completely different from her secret key for talking to Charlie. Keys are exchanged in person by scanning QR codes; they are designed to be cheap and disposable, as opposed to GPG keys which are tied more strongly to your identity. 
 * **Simple trust** — Since there is no sense of "identity" on blanket, there is no centralized authority vouching for a person's identity, nor is there a complex "web of trust" for validating identities. By design, Alice's conversation with Bob deserves no more (and no less) trust than Alice puts in the person named Bob with whom she met and swapped keys. 

## Blanket's Past and Future

While I expect to incorporate some of the ideas from Blanket into future work, Blanket was a side project to learn about cryptography, and there are currently no plans to continue development on the app as presented here. 