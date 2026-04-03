---
name: national-trust-planner
description: Find National Trust properties near a location, along a driving route, or on a multi-stop trip — sorted by distance, alphabetically, or popularity. Can exclude previously visited properties and pick a surprise recommendation.
metadata:
  homepage: https://github.com/your-username/national-trust-planner
---

# National Trust Visit Planner

## Instructions

When the user asks about National Trust properties, call the `run_js` tool with the following exact parameters:

- script name: index.html
- data: A JSON string with the following fields:

  **For a simple radius search:**
  - location: String. Place name, town, or postcode (e.g. "Shrewsbury", "LL14 5AF").
  - radiusMiles: Number (optional). Search radius in miles. Default 20.

  **For a route or multi-stop search:**
  - waypoints: Array of 2 or more place names in order (e.g. ["Shrewsbury", "Llandudno"] or ["Shrewsbury", "Wrexham", "Llandudno"]).
  - radiusMiles: Number (optional). Corridor width either side of route in miles. Default 20.

  **Both modes support:**
  - exclusions: Array of strings (optional). Distinctive name fragments to exclude — e.g. ["Attingham", "Chirk"] will exclude "Attingham Park", "Attingham Park Estate", "Chirk Castle" etc. Keep track of these across the conversation.
  - maxResults: Number (optional). Maximum number of results to return. Use when the user asks for a specific number (e.g. "show me the closest 5", "find 20 properties"). Default 10 for radius searches; route searches auto-scale with distance. Hard cap 50.

## Behaviour notes

- Use **waypoints** whenever the user mentions a journey, a route, a road trip, or "on the way to".
- Use **location** for simple "near me" or "near [place]" questions.
- After showing results, remember any properties the user says they have visited and include them in exclusions on the next call.
- The webview has sort buttons (nearest / A–Z / popular) and a 🍂 Surprise me button — mention these to the user.

## After the tool returns

Briefly summarise: mention the nearest property, any route info (distance/time), and remind the user they can sort results or tap Surprise me. If no properties found, suggest a larger radius or different place name.
