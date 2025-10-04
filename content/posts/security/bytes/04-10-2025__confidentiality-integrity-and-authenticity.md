---
title: 'The Backbone of InfoSec: Confidentiality, Integrity, and Availability'
date: 2025-10-04T02:03:10+05:30
lastmod: 2025-10-04T17:58:00+05:30
slug: '/confidentiality-integrity-and-authenticity/'
description: 'The first part in my new series: security bytes'
image: 'images/default-placeholder.png'
caption: ''
categories: [security, bytes]
tags: [CIA-triad, CIANA, infosec, cyber-security]
draft: false
---

# The CIA Triad

Whether you're new to InfoSec or you're a professional, you've definitely come across the CIA Triad. I, too, started here - freshman year of college.

> The CIA? Triads? What are you even talking about?

To borrow a line from my mentor:"Na, not that CIA."

The CIA triad make up the pillars of InfoSec. Most, if not all, security processes are designed around them. If you're a student looking to get into InfoSec, I'd start here. Preserving the CIA triad the foundational basis for InfoSec.

Extending the concept, we get the acronym CIANA (Confidentiality, Integrity, Availability, Non-Repudiation, Authenticity). This less commonly taught, however I got lucky in college with my professor being ex-military, and later with my mentor.

Let's get into it:

## Confidentiality

Confidentiality ensures data is not disclosed to unauthorized third parties. 

Think of the last time you called your Bank or Financial Institution. They are required to maintain the security of your information and finances by law, only allowing you access (or other authorized parties if you have different accounting arrangements). 

The goal here is to minimize what can be known by adversaries.

## Integrity

When I hear the word integrity, I immediately think "ships, Hull Integrity."

"Hull Integrity," you ask?

Why yes, it refers to how strong and structurally sound a ship or other vessel's hull is, if the hull of this vessel is weak or cannot withstand significant pressure, it ends up buckling beneath its weight. This may create holes in vessel through which may enter, causing it to lose buoyancy or the pressure may cause the vessel to implode in part or in full. Remember OceanGate?

The Integrity of your data is no different. We must maintain that the data, has, in no way, been modified by an unauthorized third party.

> Loose lips sink ships.

You'll see this come into play in everyday life. Developers usually make the hash and source code for their software available, to make sure the software you've downloaded has not been tampered with you can run a check against the has provided by the developer and the has of the app itself.

Most software distributors (distribution centers) or app stores, if you prefer, do this in the background when downloading or updating apps (Google Play Store, Apple App Store, Microsoft Store, etc).

&#42; **Not that I would use or recommend proprietary software, but these are good examples.**

** *Consider fighting back against digital surveillance by switching to software that respects your freedoms.*

#### Another example: 
Maintaining the integrity of your communications. When sending out an email, using PGP ensures that your recipient receives your original text. It preserves the integrity of your communication. An added bonus? It also preserves your privacy (confidentiality). How does this work? Math. Maybe I'll do a write-up on this later.

## Availability

What use is information if it is not available when you need it?

If you're in need of a resource, but you're unable to reach it, view it or otherwise utilize it given tight security measures, the security measures are basically useless. Now no-one can access it.

Availability makes sure a resource is available whilst also being secure.

In the words of my mentor, Dennis Devey of Roppers, "it doesn't matter if the data is secret and not tampered with if nobody can access it. Providing availability is critical to ensuring that the world can benefit from the information."

Side note: this also links into Saltzer and Schroeder's Security Principles. You'll find a strong conncection to "Psychological Acceptability."

# Extensions to the CIA Triad

## Non-Repudiation

To repudiate is to rebut or to deny or claim that you did not do something, when someone claims you did.

Repudiation is defined as "the act of refusing to accept something or someone as true, good, or reasonable." Non-repudiation is its opposite-the outright refusal to accept or the denial of something and someone as true, good, or reasonable.

Think of Non-Repudiation as the combination of the Authentication and Integrity pillars.

In terms of cyber risk principles? Non-repudiation is the outright denial by an individual/user of their involvement in a given communication/transaction.

For instance, assume, if you will, that I've created a pseudonymous email account with an email provider. I then use this email to sign up for a sock-puppet social media account and what-have-you. I still leave a digital trace, but nobody will be able to tie it back to me as long as I have a good threat model-following it religiously, with proper opsec.

Non-repudiation may also refer making sure that an email came from a particular user. One way of doing this is to sign off on an email with a gpg key, in addition to looking at the sender.

Another use of this princple is with blockchain, take Bitcoin, for example. The bitcoin ledger consists of multiple blocks, and since its genesis, each block was associated with its checksum and the identity of the next block. Over time, this forms a unique pattern on the ledger with transaction IDs and wallet IDs of course. Correlating all that data, it is undeniable that a given wallet ID made a certain transaction. Correlating this to an individual requires a bit more data, but still entirely plausible. Think of it as a Swiss bank account, if you will.

## Authenticity

Some prefer to call this pillar "Authentication" instead. Debate is good, but let's not get into the semantics of this concept right now, after all, we do not want to give into Sophistic Emulation.

Authentication makes sure that a user is who they say they are (Zero Trust Frameworks and Identity Management systems are based on this).

Based on their credentials, MFA codes, and answers to security questions (hot take, these are more like insecurity questions), they are granted access to information.

Think of the banking example from before, if you call your bank (or any other service provider for that matter), their standard operating procedures require that they verify your identity before they assist (related to risk, compliance, and government KYC laws). This, then, ties into confidentiality. Your information is not shared with unauthorized third parties.

I don't like service providers maintaining vast databases more than the next guy. My suggestion: create a 512-bit hash of customer records instead and verify their information (convert speech to text if you have to*, but please do not maintain identity records and personal information databases). Storing a one-way hashed record of customer information and verifying these hashes in real time like we do with passwords is paramount to security, given that it is only a matter of time large corporations experience a data breach.

*Heck, they already do.

#### Cliff notes

Consider a triangle with each of its points labeled CIA (or maybe you want to do a pentagon for CIANA), you'll soon realize that it is impossible to realize all three pillars(try filling the triangle with an inscribed circle*). If you decide to go down the extreme privcacy route (100 percenting confidentiality, you begin losing out on convenience, you might still be able to 100 percent integrity though).

*The maximum area of this circle is the maximum area it may take up the shape it is inscribed in (does not need to be a circle if it has an equivalent area).

This brings us to the next in this series: Risk and Threat Modelling.

Check back in later for more.


P.S. If you're a student and you're looking for a good place to begin your security journey, check out [roppers](https://www.roppers.org). It's free.

I recommend starting out with the Computer Fundamentals course. Dennis runs it all out of pocket, so throw him a dollar or two, I'm sure it would help with the upkeep.
