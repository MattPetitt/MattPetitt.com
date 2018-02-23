---
layout: post
current: post
cover:  assets/images/how-to-roll-your-own-streaming-service.jpg
navigation: True
title: How To Roll Your Own Streaming Service
description: In less than a year we went from two developers without a beta to beating Netflix to an international launch. Pro-tip, it’s half as hard and twice as infuriating as you think.
date: 2016-02-24
tags: [Work, Blog]
class: post-template
subclass: 'post tag-code'
author: mattpetitt
---

## Part 1: Putting the Stream in Streaming Service

In less than a year we went from two developers without a beta to beating Netflix to an international launch. Pro-tip, it’s half as hard and twice as infuriating as you think. But luckily we’ve done the learning for you. This is the first in a series of post that will chronicle the journey of rolling your own streaming service from scratch. Here’s how we did it.

### Realize you can’t out-code or outspend the Big Guys™

Our first challenge was coming to terms with how new streaming technology was, and how almost every solution the big guys had was custom, proprietary, and extremely expensive. In defiance of the Pareto principle, we needed to get 90% of the streaming quality, device support, and features with less than 1% of the resources. The first big hurdle was figuring how to get affordable and bufferless HD streams that work everywhere. It was the one thing we REALLY had to get right.

### What we had to do

Delivering video is vastly more complex than most everything else for a few reasons.

1. You have to be able to view it as you download it.
2. It needs to start almost instantaneously (This is HUGE).
3. Because of (2), content needs be delivered faster than it can be watched.
4. It needs to be in a format playable in all browsers and natively on most devices.
5. Due to HD video file sizes and short attention spans you should only be downloading the bare minimum you need, unless your CDN is dirt cheap (It won’t be).
6. You need to be able start part way through a video without having to re-download everything beforehand (I can’t stress enough how expensive this bandwidth is).
7. Not only do you need to have multiple qualities to account for a user’s bandwidth, you have to be able to switch between them in realtime to prevent buffering or poor quality video.

### What Big Guys™ do

We knew we weren’t going to be the first streaming service for a majority of our users. So we knew their standards were going to be set high. A few companies were pretty obvious. Being owned by Google, Youtube had access to the infrastructure of the largest website in the world. Amazon Prime Video, AWS, you get it. But the one we really looked at was Netflix. They didn’t have the shoulder of hosting giants to stand on. They hopped from physical distribution right into streaming and scaled rapidly. They also now account for almost a third of North America’s streaming traffic and have arguably the best quality to buffering ratio. We found that before their custom build CDN solution with localized ISP boxes they outsourced to a few CDN’s. After going through the slew of demos from every video CDN we could find, we ended up going with Netflix’s old buddy Limelight.

### What we did

At the time we had basically nothing in terms of a product and Limelight was as close to turn-key as we could find with built in encoding, hosting, geo-blocking, a player, closed captions, and a decently extensive CDN. We won’t cover why in this post, but you will eventually replace practically every one of those things with a different solution. What we will say is when you’re picking a CDN, set up some proxies, upload some files, and just test them as hard as they will let you with as much bandwidth as possible.

### What we wish we’d known

We initially started out using HDS encodings, we are now using HLS. It has better device support and seems to perform better than the other Adaptive Bitrate formats.
Get your encoding profiles correct the first time (and have as many bitrate’s as you can). We didn’t, and re-encoding hundreds of hours of video into dozens of bitrates and qualities each is time consuming but necessary because content is king.
Pick a proper player and stick with it, Flowplayer, JW Player, and Video.js are all great. For you and your users sake you don’t want to be switching around between them every time you’re adding a new feature.
Collect as many performance statistics as you can and make them searchable by user. It will make it much easier to debug buffering or playback support tickets. You will get tons of these.
Downtime is the worst thing that can happen to you, and if you are using a 3rd party CDN it will happen and you will be left feeling powerless while your customers suffer. Have a backup on another service that you can switch too.
What we’re going to do

We built CuriosityStream because we truly believe that the future of all media is online. We also believe one of the greatest strength that it gives us is the decentralization of content. By writing this series, open sourcing what we can (soon to come), and being as transparent as possible, we hope to break down the barriers of entry and make quality streaming technology accessible to the layman.