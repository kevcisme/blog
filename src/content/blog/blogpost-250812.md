---
title: Sileninja Update
description: What does Academia have to say about this?
pubDate: 2025-08-12 08:42
author: Kevin Coyle
tags:
  - Full Stack Dev
  - ML
imgUrl: '../../assets/sileninja.jpg'
layout: ../../layouts/BlogPost.astro
---

# Update on Sileninja Progress

When I [last wrote about Sileninja](src/content/blog/blogpost-250217.md) I was mostly just interested in the concept of a "mic blocking" or "mic jamming" app. I ended up going on several side quests: [here](src/content/blog/blogpost-250329.md), [here](src/content/blog/blogpost-250409.md), [here](src/content/blog/blogpost-250430.md), and [here](src/content/blog/blogpost-250515.md). [Author's note: In the preceding sentence, I almost wrote "_unfortunately_ went on several side quests..." but I have amended this. I have decided to lean into the side quest as a way of life]. 

My initial hypothesis is that I can just turn off or mute the microphone. I'm going to go with this as I figure out if there is a sizable enough market for Sileninja. 

However, it also occurs to me to over intellectualize this whole thing and spend hours on Arxiv figuring out what the latest and greatest SOTA is. 

Here's some initial findings.

The NYT wrote an article way back in 2018 about home assistants and people's weariness with always on devices ([source](https://www.nytimes.com/2018/03/31/business/media/amazon-google-privacy-digital-assistants.html)) as did Wired ([source](https://www.wired.com/2016/12/alexa-and-google-record-your-voice/)).

Broadly, it seems like there are two approaches to how to disrupt:
1. Mask the signal of audio. This is basically like shouting down someone when they are trying to give a talk. The shouter is disruptive of the listeners (audience) by shouting over the source (speaker/talker).
2. Occupy the mic. This would involve muting or otherwise shutting down the actual microphone. This is the approach I'm most interested in, as I think it both a.) runs in the background, as a silent process (pun intended) and b.) I'm like 92% certain that apps can't "see" what other apps are doing, so mobile app A - Sileninja - running this technique wouldn't be detectable by mobile app B - sneaky snooper app. 
I'll discuss these in order, even though I'm taking approach #2. This will allow me to get _some_ research on #1 out there.


Many of the articles have some sort of jamming technique with an external device. This probably makes sense for at least two reasons:
1. Consumers probably assume that the tool that is causing their upset is not the tool that would fix it. That would be like saying that the way to get over how gross kale tastes is to eat more kale. 
2. Limitations of what a mobile phone can produce. 

[A Portable and Stealthy Inaudible Voice Attack Based on Acoustic Metamaterials](https://arxiv.org/html/2501.15031v1) leverages acoustic "metamaterials" (a portable device) to achieve this jamming. 

There was an attempt to make a phyical product that follows this [from the University of Chicago](https://techxplore.com/news/2020-02-team-jammer-bracelet-outsmarts-microphones.html#:~:text=The%20bracelet%20emits%20ultrasonic%20noise,24%20kHz%20to%2026%20kHz). It feels like kind of out of the spirit of what I'm trying to accomplish here - one of the main goals is to keep this as low barrier to entry to users. 

Additionally, these wearables are largely hindered by directionality. If blind spots exists, the device's effectiveness is severely hampered. 

The other version of this is an "ultrasonic firewall" from this paper: [SoniControl - A Mobile Ultrasonic Firewall](https://ar5iv.labs.arxiv.org/html/1807.07617). The authors point out that 
> near-ultrasonic signals exchange information across the auditory channel through the loudspeakers and microphones  of mobile devices... This technology, also called _data over audio_ enables effective near field communication capabilities but also opens up a number of security and privacy concerns.

This team's [blog](https://akirchknopf-21436.php.fhstp.cc/blog/) was a treasure trove of info. I somewhat get the sense though that this technology is meant to block NFC types of transmissions, rather than my use case, which is to block incoming signal from apps.

So that brings me to the approach I'll be taking, which is to try to occupy the mic. 

[!](https://y.yarn.co/31612444-b771-44a4-be1b-96f46fec4bd9_text.gif)

[AuDroid: Preventing Attacks on Audio Channels](https://arxiv.org/pdf/1604.00320)'s authors (Petracca et al.) introduced AuDroid, an Android modification that extends the SELinux security monitor to explicitly track audio channel usage. AuDroid can enforce context-dependent policies on when and how apps use the microphone or speaker. For instance, it can prevent a lower-privilege app from accessing the mic if it could create a covert channel with another process. In their evaluation, AuDroid was able to stop several audio-based attacks (like apps trying to misuse the mic or speaker in tandem) while still permitting normal app functionality. To me, I read this like: this paper shows that it’s possible to impose stricter controls on mic usage without unduly breaking app features.

Another whole thread of thought also figured out that apps can circumvent the single occupancy policy via side channels. Since only one app can use the real microphone, attackers have turned to other sensors that are not so strictly regulated. A landmark example is the Gyrophone attack (Stanford, 2014), which showed that a smartphone’s gyroscope (which requires no permission) can pick up vibrations from sound and thus serve as a crude microphone [source](https://crypto.stanford.edu/gyrophone/files/gyromic.pdf).

I'm going to work on coding out the mic occupancy and side channel prevention styles!

