---
title: "Let's break the information gap"
url: "/aboutme/projects/lets_break_the_information_gap"
summary: aboutme
ShowReadingTime: false
---
> A free web application that create a two-host daily podcast of the news that matters to you. Just add your favorite RSS feeds from news sites, blogs, and social media. Our app will automatically generate conversational scripts using an LLM and then produce a customized audio episode with text-to-speech. It's the perfect way to stay updated on your commute.

[code available in github](https://github.com/Kingjinsight/Lets-break-the-information-gap)

<iframe width=100% height=450 src="https://www.youtube.com/embed/Xx2ari_n_f0?si=af_64RookXLDccYE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>   


## Motivation
The idea of having a  J.A.R.V.I.S. from the Marvel movies, is a common dream. With today's advancements in LLM and TTS technology, we can now offer a real-world experience that captures a part of that dream.

For me, I love to start my mornings by checking my favorite blogs for updates, scrolling through X for new tech news, or quickly scanning the day's headlines. With this application, I could simply wake up, click a button to generate my podcast, and then, while having breakfast or commuting, listen to a personalized summary of everything that happened overnight. If a specific story catches my interest, I can then go back and read the full article later. I think its an efficient way to stay informed.

## Tech stack

| Area | Technology |
| :------ | :---------------------------------------------------------------------- |
| **Backend** | FastAPI, Python, SQLAlchemy, PostgreSQL, Pydantic |
| **Frontend** | React, Javascript, TypeScript, Vite, Tailwind CSS |
| **AI & TTS** | Google Gemini 2.5 Pro API |
| **Deployment** | Render (Web Service, Static Site, background worker), Docker (local dev for velkey(alternative for redis)) |
| **AI assistant** | Gemini 2.5 pro, Claude sonnet 4 |
## Issues I met
1. Gemini api timeout: 
   - The current Gemini API has a 60-second request timeout, which is insufficient for generating a 10-minute podcast with a single text-to-speech (TTS) request. To solve this, my initial thought was to segment the entire podcast script into smaller parts and generate each segment separately.
   - However, a new challenge arose with the TTS service's free plan, which limits me to just 15 requests per day. This makes the segmentation approach impractical for daily use.
   - My temporary fix has been to adjust the script prompt to generate shorter content, but this method is unreliable and doesn't always prevent timeouts.
   - The long-term solution will be to upgrade to a paid TTS service with a longer API request timeout. This will allow for single, uninterrupted podcast generation, solving the issue at its root.

## Roadmap
- 2025-09: Migrate deployment from Render to my personal server
- 2025-10: Add more social medias RSS feeds
- 2025-12: Multi-format input file support
- Future:
  - Use fine-tuning TTS model
  - Improve user experience
  - Support spotify export

## Summary
This project takes me 2 month from learning tech stacks to final outcome. I want to say AI really helped me a lot during the building process, whereas from learning tech stacks to fix bugs. From this prject, I experience both frontend and backend project building, frontend is just like building an artwprk, it really need me to keep patient, backend is more interesting since it relative to many different fields like crud operations, building database schemas and endpoints and connection between database, background worker. I also experience the magic of containerization, its so convenient. - 2025.08.14