# TasteRoute

TasteRoute is a small agentic route planner for the Qloo Agentic Hackathon. A user gives it a mood, a city, and an optional cultural anchor. The server resolves the anchor through Qloo entity search, uses the Qloo Insights API to find related places, and composes a three-stop route with an explicit interpretation trace.

## Run locally

This project is a dependency-free Cloudflare Worker. The page is embedded in `worker/index.js` so the same source can run locally or on Sites.

1. Set `QLOO_API_KEY` to a hackathon key when you want live recommendations.
2. Run the worker with the Sites worker starter or a compatible Cloudflare Worker runtime.
3. Open `/` and submit a mood, city, and anchor.

Without `QLOO_API_KEY`, the app uses a clearly labelled built-in demo route. The demo does not claim to be live Qloo data.

## Qloo integration

Live mode uses the hackathon base URL `https://hackathon.api.qloo.com`, sends the key in the `X-Api-Key` header, calls `/search` to resolve the cultural anchor, and calls `/v2/insights` with `filter.type=urn:entity:place`, the resolved entity as `signal.interests.entities`, and the requested city as `filter.location.query`.

The key is read only from the server environment. It is never embedded in the browser page or returned to the client.

## Product flow

1. Interpret the free-text mood.
2. Ground the mood with a Qloo entity search.
3. Retrieve culturally related places for the city.
4. Compose three stops with a deliberate energy curve and show the grounding trace.

The route is a planning suggestion. It does not book, purchase, or message any venue.

## Hackathon submission notes

- The application is open source under the MIT license.
- The live deployment must have `QLOO_API_KEY` configured as a server secret.
- The Devpost submission needs a public code repository, a public functional demo URL, and an English description.
- Qloo API documentation: <https://docs.qloo.com/reference/qloo-llm-hackathon-developer-guide>.
