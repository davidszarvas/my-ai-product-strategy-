# The Prototype Bet

## What I Built
A web app prototype where users enter the calories they have left for dinner (0–1200) and get AI-generated recipe cards, browsable in a carousel, whose calories match that amount per 300g, with protein, fat and sugar shown in grams.

## Tool Used
Lovable

## Prototype Link
https://lovable.dev/preview/c2jAKu15EnQlEvHddV2pfRybL9xaGQIQ

*Note: this link is only active for 7 days.*

## AI Value Archetype
Creator

## The Bet in One Sentence
We are building Exact Calorie for people who lose weight or must count calories for dietary reasons, giving them dinner recipes that hit their remaining daily calories exactly, because generative AI can now produce recipes to hard numeric constraints, so users no longer have to guess or do the math themselves.

## Kill Criteria
We stop if any of these hold after a pilot with real users and real (non-dummy) recipe generation:

- **Accuracy:** Fewer than 90% of generated recipes land within ±5% of the requested calories/300g when checked against a nutrition database.
- **Trust:** Fewer than 50% of users say they would actually cook a generated recipe, or fewer than 60% rate the macro data (protein, fat, sugar) as believable.
- **Retention:** Fewer than 25% of users return and generate again within 7 days.
- **Cost:** Cost per generation is too high to support a viable price point.
- **Safety:** Recipes repeatedly give nutrition data that is wrong in a way that could harm users with medical dietary needs (e.g. diabetes, allergies), and it cannot be fixed with validation.
