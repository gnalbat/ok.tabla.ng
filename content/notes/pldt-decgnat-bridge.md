---
title: PLDT deCGNAT and bridge mode
date: 2025-07-18
tags:
  - tech
  - lessons-learned
---
A few months late (got this done on May). You could probably [search in on reddit](https://www.google.com/search?q=site:reddit.com+pldt+bridge+mode+and+cgnat) (thanks, reddit! True reddit moment, rock on redditors)

I had trouble with our internet service totally going down whenever I started qBittorrent. I probably had so much active torrents (and consequently peers) that the ISP router (FiberHome HG6245D) gets flooded and internet goes down until the router is restarted. The internet doesn't get down when I used a VPN, so it had something to do with packets flooding the router/s. The network was double-NATted into an ASUS RT-AX53U which is definitely more powerful than the ISP router.

In the early days of PLDT, the DSL service included a black modem with only one LAN port. The copper line was split into telephone and ethernet cables. You could forward the DSL modem to a WiFi router and the router would manage the network. Although dynamic IP, the connection wasn't under CGNAT yet circa late 2000s (something about [IPv4 address exhaustion](https://en.wikipedia.org/wiki/IPv4_address_exhaustion)) . So you essentially had a public IP you could port forward to. This time was when I learned web development (well, mainly XAMPP and Wordpress) because of Jonas Roque's Facebuko, a parody site of Facebook satirizing Philippine showbiz (RIP Facebuko).

Advanced network settings for routers were gone when PLDT introduced ISP routers (even before we switched to Fiber in 2021, the DSL connection required PLDT-provided routers and third-party ones wouldn't work if connected to the black DSL model). Before they cracked down on superadmin access in early 2020s, port forwarding was still able to be done through the superadmin account whose password you could find leaked on the internet. The official way was to request superadmin access through signing a waiver of liability, but where is the challenge in that?

Anyway, superadmin access won't fix my situation since the ISP router itself is underpowered for my use case. There were two things to do: request removal from CGNAT, and request for activation of bridge mode. These are mutually exclusive but requesting only one of them doesn't make much sense. DeCGNAT without bridge mode just puts you into a more usually-blocked public IP (at least for Google). Bridge mode without deCGNATting would just use bypass the ISP router but much of advantages you have with bridge mode is useless aside from the fact that the third-party router is more powerful specs-wise (since you don't have an exclusive public IP).

The first request, I sent through Facebook Messenger, was to request for deCGNAT and bridge mode. It was done after a few hours but only the deCGNAT part. The ticket was closed. So I made another through the same platform. This time, they sent a subcontractor who couldn't do much since they only fix physical cables, and couldn't see any problems with the connection, even until the termination line to the router. For the next one, called the 171 hotline, and the agent who handled my request said something about a "Line Test" failing (which I somehow cannot believe, since the connection was fine aside from when packets are flooding), so they made another request to a subcontractor. The next day the subcontractor assigned marked the ticket as solved even without calling me (luckily for me since I don't wanna deal with another guy who couldn't solve my problem, unluckily since there exists these types of people who marks as solved the ticket even without calling once). I finally called 171 for the last time and luckily spoke to an agent who knew what bridge mode is. Bridge mode was activated a few hours after, only after three weeks of distress.

It just bugs me that for officially available requests, not all customer service representatives are made aware that these requests for services are possible and as such, time and effort are wasted from many people. Much like a doctor misdiagnosing your issue.

tldr: ISP router bad, customer service badder