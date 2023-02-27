---
title: "Discord New"
date: 2023-02-27T14:45:10+04:00
draft: false
---

# The Ultimate Communications Guide Dubai Edition

Since this question is asked quite frequently I thought I'd make a guide on how to voice chat for gaming in the UAE. I'll split this in to two parts, the first part is for normal humans and the second part is for more technical folk and will focus heavily on Discord.

## [EASY] Method 1: Use a known alternative

Steam chat works, and so does Blizzard's chat for VoIP. Blizzard has terrible audio quality from my personal experience, but Steam chat works pretty well. You can create a group with all your friends and people can join and leave the voice channel whenever they like.

## [EASY] Method 2: Use a work-related VOIP service

Google Meet, Zoom, MS Teams, etc., these all work thanks to COVID and the work-from-home phenomenon.


## [MEDIUM] Method 3: Use a lesser known alternative

Raise your hands if you're old enough to remember TeamSpeak! If you're just playing with a group of friends and they don't mind trying out a new service, you can *rent* a TeamSpeak server (they're really cheap). While the interface feels like its from the early 2000's, and some technical knowledge is required (it's pretty straight-forward), the audio quality is much more superior to that of Discord, etc.,

## [MEDIUM-HARD] Method 4: SSH Tunnel w/ Discord Web

So one of the main ways people get around the Discord block is to pair it with a VPN. The problem with this is that a VPN will tunnel ***all*** of your traffic through it. Namely, your CS:GO, CoD, etc., game is jumping from your PC in Dubai to the VPN in Europe, etc., to the game server in Europe, back to the VPN, then to you. Your ping/latency is horrendous. 

One way to get around this is to tunnel only your browser traffic through an SSH tunnel. 

If you're renting a VPS, have a free one, or even have website hosting with SSH access anywhere in the world (yes, it'll probably even work if you're hosting in the UAE too - more on this later), this is pretty easy to acheive.

Use the dynamic flag when connecting your SSH session and assign a random, unused port. Let's say 1337 for the lol's. 

`ssh -D 1337 user@address`

Add a SOCKS proxy toggle add-on to your browser (i.e., Proxy Toggle on Firefox, or Hotplate SOCKS proxy for Chrome)

Configure the add-on to the port you assigned when connecting your SSH session, turn it on et voilà! All of your web browser traffic is now tunnelled through your SSH session. Login to Discord Web and enjoy uninterrupted chat. Remember to disconnect the SOCKS5 Proxy plugin when you're done or you'll get a 'Proxy Server is Refusing Connections' error when you close your SSH session.

**Bonus Exercise:** Set up an alias in your terminal for this command and automate the whole process.

## [MEDIUM] Method 5: UAE VPN

Yes although VPN's are terrible ideas to tunnel your whole traffic through because of the latency, you won't get a lot of extra latency when connecting to a VPN in the UAE. "But...but... won't it still be blocked?", you might ask. No, discord and VoIP in general isn't blocked on *enterprise* internet connections. Meaning if you can set up an SSH tunnel to a *business* internet connection, you can do this too, for free. Alternatively, just pay for a VPN service that has servers in the UAE, and connect to one of those, the added latency is acceptable. 

## [HARD] Method 6: Set-up your own VoIP service

There are plenty of Docker images for great VoIP services that work wonderfully. If you want a pure VoIP service, check out Jisti. If you want something with even more capabilities, and have a server for you and your friends with VoIP, file-sharing, etc., try out Nextcloud, which can be deployed as a Docker container, LXC, snap image in Ubuntu, etc., (I think their VoIP solution is actually based on Jitsi)

Alternatively, if you're looking for a Discord **clone**, then you could deploy Matrix, *although it's a little trickier to set-up VoIP as I believe you need your own STUN/TURN servers*

MatterMost is an enterprise Discord-like solution (it's more of a self-hostable alternative to Slack/Teams), but also works great with VoIP and has a very Discord-like feel with Channels, Hashtags, etc., and comes with its own TURN server (no extra set-up is necessary past the installation/deployment).

Revolt is another self-hosted Discord-clone project I've heard of but have never tried myself.

Once you've deployed your solution, slap it behind a reverse-proxy (NGINX, Traefik), port forward 80 and 443 on your router and you're GUCCI.

## [HARD] Method 7: Make your own VPN

There are plenty of guides on this and I'm pretty sure someone posted a pretty lengthy guide here on how to do this with the Oracle free tier virtual machines. All you need is a VPS/Virtual Machine/Computer with root access. As long as its 1.) On an Enterprise/Business internet connection in the UAE or 2.) Anywhere else in the world where VoIP isn't blocked, you can make your own. I'm pretty sure there are also AWS free-tier images for OpenVPN/WireGuard that you can deploy and have a whole year of your very own VPN hosted in a UAE datacenter.