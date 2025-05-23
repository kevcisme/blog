---
title: Poker for Profit?
description: I wonder if I can use ML to become better at Poker
pubDate: 2025-05-15 16:48
author: Kevin Coyle
tags:
  - Sports Analytics
  - ML
imgUrl: '../../assets/can-we-use-ai-poker.png'
layout: ../../layouts/BlogPost.astro
---

# Using ML to Learn Poker
My friend made the mistake of asking me about a math / coding problem. ![](../../assets/can-we-use-ai-poker.png)

The problem is that this hits a sweet spot in a Venn diagram for me of things that involve:
- code, especially ML, and with high potential for a cool looking UI
- math, especially some math that I haven't built a model with (something about novelty here)
- money, especially if it's something that I haven't heard of other people doing to make money

## Contextual background

One of the people I have regular 1:1s with at work is a huge poker fan. He introduced me to solvers at the time when I was learning to program in Rust and that became a mini-obsession for a month last year. He doesn't know this about me, because what non-technical friend asks you which languages you program in? 


## Side projects that might make cash >

If you read my [last post]('./blogpost-25-0430.md') then you know that side projects with "no real line of sight of cash" are something I pride myself in finding and working on. I don't know why, I think it's just that I need "a business guy" to help out with every technical thing I want to implement so he can do the business stuff and I can do the tech stuff.

Also, I am fully aware that I have done the thing where I spin out on side projects. For those counting, I have blog posts detailing:
- [3 mobile apps](./blogpost-241210.md)
- [A site for office pools](./blogpost-250409.md)
- [A loose promise to a groupchat that this is the year I build that Dude Scouts site](./blogpost-250329.md)
- [A to do app to crush all to do apps](./blogpost-250430.md)

Which is a running tally of 6 unfinished apps (I'm not counting unsolved Jira tickets at work, those are _booooring_).

I swear though, these will all come together.

This poker idea is brilliant though, and I don't have to even make it user facing. Me and the guy who poked the bear on it can just make money

Should I focus on this? Should I not? 

Let's let my executive dysfunction decide! 

## Initial findings

My first thought was "this is a reinforcement learning problem." So initial googling resulted in some hype-y like links (youtube videos with titles like "I taught AI to beat people in poker!"). Went to arXiv and found an academic paper from 2019 where someone used a model to beat top players. Strangely enough, there isn't a ton of other academic papers on this. I wonder if that's the economics part of this - anyone that has a model that works probably has it in prod, but to make money for themselves. I'll consider this, but I think I want to learn, as a human, so that I can beat friends and family at poker later.

In 2019, there was a paper released about a model that seems like it did really well [with a model the author titled Libratus](https://www.science.org/doi/full/10.1126/science.aay2400). This actually kind of makes sense already - solving poker with computer systems is a difficult challenge, because like the author writes:

> No other popular recreational game captures the challenges of hidden information as effectively and as elegantly as poker

Additionally, poker, as opposed to say Go or Chess, has evaded people because the nature of it can be multi-player and other games
> involve only two players and are zero-sum games (meaning that whatever one player wins, the other player loses). Every one of those superhuman AI systems was generated by attempting to approximate a Nash equilibrium strategy rather than by, for example, trying to detect and exploit weaknesses in the opponent. 


So this already seems like an awesome challenge. I'm aware that the game of poker has seen a sea-change in that most of the top players now use Game Theory as a way to do scenario planning. 

So now, to add to the list of "things in a Venn diagram that make Kevin want to solve a problem" we add Game Theory and this fire is lit!

## Next steps

Very light research is as far  as I've gotten. If I'm putting on my adult hat - I have a massive backlog of Jira tickets at work and I should be solving _those_. But again, the executive will decide what I do!

Going to look into whether a tutorial exists to create a model to play against. Once I have a simple model up, I envision this sitting behind a simple GUI like with TKINTER or something equally blasé from a graphic design standpoint. 

Here weeeee gooooo!