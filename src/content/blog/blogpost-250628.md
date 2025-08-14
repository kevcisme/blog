---
title: Adventure Time with Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-06-28 9:20
author: Kevin Coyle
tags:
  - Adventure
  - Full Stack Development
imgUrl: '../../assets/dude-scouts.png'
layout: ../../layouts/BlogPost.astro
---

# How about EVEN MORE features?

I had another monetization idea: what if dude scouts not only encouraged IRL meetups, but also provided a way to book travel packages?

For those counting, that brings us to like 4 monetization opportunities:
1. Subscription to the site (I'll keep it low, just to cover costs of running the site and maybe donations?)
2. Buying courses/badges. Pays the instructors a bit.
3. An ecommerce shop with some swag
4. Travel packages

I'm only doing this because I assume I'll screw up all 4 of these channels, so hopefully by not putting all eggs in the same basket, I can keep this thing profitable.

Also, the travel packages are just like bucket list travel packages/lads trips ideas. The in person meetups should be free.

### From mock shop to curated adventures: a new travel vertical and community events

Between “Create mock products in shop with badge images” and “Add curated travel packages,” we leveled up from a static merch showcase to an “Adventures” vertical with curated travel packages and upcoming meetings. This adds real site depth, clearer navigation, and a foundation for future bookings.

### What shipped

- **New Adventures section**
  - `adventures/` hub with two clear entry points: Meetings and Curated Travel.

- **Curated Travel packages**
  - Page: `adventures/travel` renders a hero and a grid of packages via `TravelPackageList` + `TravelPackageCard`.
  - Data: `mockTrips.ts` provides destination, dates, price, and imagery.

```src/app/adventures/travel/page.tsx
import Navigation from "@/components/Navigation";
import TravelPackageList from "@/components/TravelPackageList";
import { mockTrips } from "@/data/mockTrips";
import type { Metadata } from "next";

export const metadata: Metadata = {
  title: "Curated Travel | Dude Scouts",
  description: "Adventure travel packages coming soon.",
};

export default function TravelPage() {
  return (
    <div className="min-h-screen bg-white">
      <Navigation />
      <section className="py-20 bg-gradient-to-br from-green-50 to-blue-50">
        <div className="max-w-2xl mx-auto px-4 text-center space-y-4">
          <h1 className="text-4xl font-bold">Curated Travel Adventures</h1>
          <p className="text-gray-700">
            Book a fully-planned getaway with your fellow Dude Scouts. All trips
            include lodging and activities.
          </p>
```

```src/components/TravelPackageCard.tsx
import { Card, CardContent, CardFooter, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import type { TripPackage } from "@/data/mockTrips";

export default function TravelPackageCard({ trip }: { trip: TripPackage }) {
  return (
    <Card className="flex flex-col h-full">
      <CardHeader>
        <CardTitle className="text-center">{trip.title}</CardTitle>
      </CardHeader>
      <CardContent className="flex-grow flex flex-col items-center text-center space-y-2">
        <img src={trip.imageUrl} alt={trip.title} className="w-full h-48 object-cover rounded-md" />
        <p className="text-gray-500 text-sm">{trip.destination}</p>
        <p className="text-gray-500 text-sm">{trip.dateRange}</p>
        <p className="text-gray-700">{trip.description}</p>
```

- **Meetings page**
  - Page: `adventures/meetings` lists upcoming community events from `mockMeetings.ts`.
  - Clean card-like list with date, location, and description to drive engagement.

- **Adventures index**
  - Page: `adventures/` acts as a simple hub with CTA buttons for Meetings and Travel.

- **Navigation updates**
  - Ensures users can discover Adventures from the global nav (consistent with prior Shop and auth updates).

### Why this matters

- **Depth and retention**: Adventures introduces meaningful content beyond the store—reasons to come back, plan, and participate.
- **SEO-ready**: Each page sets `Metadata` for titles/descriptions; card content is crawlable and human-readable.
- **Composable UI**: Travel components mirror the shop’s pattern (List + Card + mock data), making a clean path to live data later.
- **Conversion path groundwork**: Price and “Book” CTA stubs are in place, making Stripe/booking integration straightforward.

### What’s next

- Replace `mockTrips`/`mockMeetings` with real data (CMS or API).
- Add analytics events (view_trip, click_book) reusing the Snowplow pattern.
- Introduce a basic booking funnel (availability, checkout) and authenticated reservations.
- Add travel detail pages (`/adventures/travel/[slug]`) with richer itineraries and galleries.

- Ensure navigation highlights current section; consider breadcrumbs on deeper pages.

- Extend Meetings with RSVP/ICS export to grow attendance.

- Performance: lazy-load images, add Next/Image domains as needed.

- Accessibility: audit interactive elements and color contrast; ensure keyboard reachability across cards and CTAs.

- CI/CD: preview deploys for Adventures pages to test content changes quickly.

- Monitoring: track impressions and clicks to prioritize which packages to launch first.

- **Adventures vertical added** with curated travel and meetings.
- **Reusable components** (`TravelPackageList`, `TravelPackageCard`) and mock data introduced.
- **SEO and UX improvements**: metadata, hero sections, consistent design system usage.
- **Ready for next step**: instrument events, wire real data, and add booking flows.