---
title: Scaffolding Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-03-30 10:15
author: Kevin Coyle
tags:
  - Life Updates
  - Full Stack Development
imgUrl: '../../assets/dude-scouts-logo-light.png'
layout: ../../layouts/BlogPost.astro
---

# Let's build something cool

## Initial Scaffolding

I want to build this with a pretty modern stack. What are the cool kids using? Let's set this site up as a modern Next.js app with TypeScript, Tailwind, and PostCSS.

## General layout

My initial layout of UI should look pretty clean because everything else is going to be messy af. I really dig the aesthetics of those national park signs. I grew up going to the Sierra Nevadas on the weekends, and I think it would be cool to bring that spirit into this.

I also want to take some inspo from other LMS-es like Udemy and Salesforce's Trailhead.

Lastly, while I'm developing, I've made the decision to come up with a bunch of mock courses as mock data to fill out everything. At some point, I'll turn these into courses!

### The first delightful micro-interaction

- **flip words in the hero** 
  - Added `src/components/ui/flip-words.tsx`.
  - Integrated into `src/app/page.tsx` to animate a rotating set of words in the hero.
  - Light `package.json`/`package-lock.json` updates as needed.

### Why this sequence mattered

- **Incremental composability**: Established a reliable app shell before layering pages and visuals.
- **Content-first**: Early mock data and assets let us validate UX quickly.
- **Polished interaction**: The flipping hero words are a simple, joyful detail that sets the tone.

### Notable files added/changed on the way to the hero

- App shell and pages: `src/app/layout.tsx`, `src/app/page.tsx`, `src/app/about/page.tsx`, `src/app/trails/page.tsx`, `src/app/lesson/[lessonId]/page.tsx`, `src/app/module/[moduleId]/page.tsx`
- Components: `src/components/Navigation.tsx`, `src/components/ui/flip-words.tsx`
- Data: `src/data/mockTrails.ts`
- Assets: `public/badge-images/*`, `trailhead-*.png`, `screenshot*.png`
- Config: `next.config.js`, `postcss.config.js`, `globals.css`, `package.json`, `package-lock.json`
