---
title: Let's get Social with Dude Scouts
description: The Boy Scouts meets silly goose energy meets coding
pubDate: 2025-05-18 5:04
author: Kevin Coyle
tags:
  - Adventure
  - Full Stack Development
imgUrl: '../../assets/dude-scouts.png'
layout: ../../layouts/BlogPost.astro
---

# Analytics? Why Not

The project evolved from a deploy-ready full-stack app to an instrumented platform with backend analytics. Here’s a breakdown of the key improvements and why they matter.

### Highlights

- **Snowplow analytics added to the backend**
  - New tracking module centralizes analytics configuration:
```backend/app/core/tracking.py
import os
from snowplow_tracker import Tracker, Emitter

emitter = Emitter(os.environ["SNOWPLOW_COLLECTOR"])
tracker = Tracker(emitter, namespace="backend", app_id="dude-scouts")
```
I first came across Snowplow when I was working as the Data Engineer/Data Scientist/MLE/Salesforce Dev at Alo Yoga. I was pushed to learn to use this when I mentioned that I wanted to build a data warehouse that contained click level data from the ecom site. I was told they didn't have budget, which is all gucci. Restriction is the mother of all invention or whatever. Anywho, now I know how snowplow works and as someone who always loves the idea of a cool dashboard, I figured we could collect user analytics with Snowplow. Also, I could keep my chops a little sharper.

  - First event wired into the API root to validate pipeline:
```backend/app/main.py
from app.core.tracking import tracker

@app.get("/")
async def root():
    tracker.track_struct_event("api", "root")
    return {"message": "Dude Scouts API", "environment": settings.environment}
```

- **Safer, environment-aware configuration**
  - My `config.py` got formatting cleanups and clarified environment handling for CORS and LocalStack endpoints.
  - Keeps dev/prod behaviors cleanly separated (LocalStack in dev, real AWS in prod).

- **Backend endpoints enhanced with analytics signals**
  - Community API now emits a structured event when a post is created:
```backend/app/api/v1/community.py
from app.core.tracking import tracker

# inside create_post(...)
tracker.track_struct_event("community", "create_post", label=str(row["id"]))
```

- **Frontend community UX refresh**
  - `src/app/community/page.tsx` and `[questionId]/page.tsx` were modernized:
    - Added `Navigation`, improved layout/typography, and adopted shared UI components (`Card`, `Textarea`, `Input`).
  - `AnswerForm.tsx`, `AnswerList.tsx`, `QuestionForm.tsx` switched to design-system inputs for consistency and better accessibility.

- **Test and dependency alignment**
  - Backend requirements and pyproject updated to include Snowplow and keep test fixtures aligned.
  - My conftest ensures a sensible default for the collector in test runs.

### Why this matters

- **Observability from day one**: With Snowplow wired in at the API edge and critical write paths, we gain immediate visibility into user activity and API health without waiting for frontend-only data.
- **Deployment confidence**: The earlier commit ensured Docker-first deployments; I added some  commits that adds the analytics layer that teams typically need once traffic starts.
- **DX and UX upgrades**: Cleaner configuration boundaries reduce surprise behaviors across environments, while the refreshed community UI makes the feature more discoverable and pleasant to use.

### What to configure after pulling

Some stuff I need to do, now that I've added in Snowplow
- Verify a Snowplow collector endpoint is reachable from the backend.
- Expand event coverage (votes, answers, errors) using `tracker.track_struct_event(domain, action, {label, property, value})`.
- Add alerts/dashboards on Snowplow events to monitor traffic and key flows post-deploy.
- Confirm CORS origins in prod 

Summary
- Added backend analytics via Snowplow with a dedicated module and initial events.
- Updated environment docs for dev/prod collector configuration.
- Improved backend config clarity and frontend community UI consistency.
- Positioned the app for data-informed iteration right after deployment.

