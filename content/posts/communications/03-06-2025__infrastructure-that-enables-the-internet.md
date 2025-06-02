---
title: 'The Infrastructure that enables the Internet'
date: 2025-06-03T01:27:10+05:30
lastmod: 2025-06-03T01:27:10+05:30
slug: '/the-infrastructure-that-enables-the-internet/'
description: 'The second part in a series about networks and the internet: how the internet works.'
image: ''
caption: ''
categories: [comms]
tags: [infrastructure, the-internet, networks, equipment, CPE, UE, radius, authentication, synchronization]
draft: false
---

[&larr; prev](/posts/communications/communications-networks-and-the-internet/)

**DISCLAIMER: THIS ARTICLE IS STILL ACTIVELY BEING WORKED ON**

There are a vast number of options for connecting to the internet; however, the basic premise remains the same: your end devices communicate with your ISP’s network, which in turn communicates with other providers’ networks. Oversimplified, but this is the basis of the internet.

### A bit of Backstory

Early internet connections were based on copper lines. In fact, some connections still use copper today—though the technology has evolved significantly over time.

In the early days, telephone companies, often in collaboration with governments and, later, ISPs, would be involved in setting up nodes (telephone exchanges). These nodes would connect back to their headquarters and to distribution points along residentials areas and commercial hubs. 

*Note that these connecting leads were coupled with power cables in the early days.*

As the electrical signal carried by the copper cabling was analogue in nature, it was prone to attenuation - which to degradation and loss of the signal. The further the signal travelled the more noise there was on the line - this is why repeaters and amplifiers were installed at regular intervals along the line. To the general public these were commonly referred to as "boosters."

### Receiving a connection

When signing up for a new connection, your ISP would need to connect the lead copper cables to your premises. A technician would usually be involved in connecting the copper lead-in to your premises, then DSL wall plates and, optionally, internal cabling would be installed at the premises.

Once set-up was complete, you would connect your modem - that you purchased, or, if you were lucky, received for free from your provider to your premises.

Back then, we only had dial-up modems, they consisted of DSL port and one LAN port. The purpose of this device was to convert the incoming analogue signal into a digital signal understandable to your computer, hence the name modem (modulator, demodulator). It worked both ways (downstream and upstream), to allow for your computer to send and receive information. 

One end of the modem would be connected to the DSL port in the wall (the wallplate) via a DSL (phone) cable connection, and the other end would see a LAN (ethernet) cable connected to your computer or hub and then to your computers, if you had multiple computers at the time.

> To have that many computers in that age... You must have been the envy of all your neighbours in a 5 mile radius!

This wouldn't be enough to connect you to the internet for long however, you would also need to type in your username and password each time you wanted to connect to the internet and if your parents, siblings, or cousins were on the phone - then you'd know the struggles of connecting to the internet in the 80s - good luck trying to connect! Ah yes, family - the bane of my existence, at least when trying to connect to the internet. Good times...

Your dial-up connection used two protocols at the time: PPP - Point-to-point Protocol, and RADIUS - Remote Access Dial-in User Service. This came about as a business practice, to prevent teenagers from mooching off their ISPs without paying for a connection. Although it was largely a success, there were still work-arounds at the time.

You, the user, would simply type in your RADIUS credentials (username and password - provided to you by your ISP), usually without the knowledge of PPP and other lower layer protocols - it was abstracted away for you - peak user-experience at the time!

Your ISP's RADIUS server would then authenticate your login and provide you a connection, if your username and password existed on their database/records.

### Modern Connections

Modern connections are similar in the sense that they need to be authenticated, however the medium of the connection may differ.

Modern connections can take place over a multitude of media. They can be fixed connections or mobile connections and can take place over physical media or over the air. Some examples of these connections are:
- Fixed Connections
  1. Fibre Connections
      1. Fibre to the Premises/House (FTTP/H)
      2. Fibre to the Curb (FTTC)
      3. Fibre to the Node (FTTN)
      4. Fibre to the Building (FTTB)
  2. DSL/Copper Connections
  3. Coaxial Connections
  4. Fixed Wireless
- Mobile connections
  1. Mobile Broadband
