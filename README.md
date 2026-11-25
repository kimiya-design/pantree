# Pantree

A mobile pantry app that turns grocery photos into an inventory and helps you use food before it expires.

![Pantree demo](media/demo.gif)

> The source code is private. I’m happy to walk through the project in an interview or share temporary read-only access.

## What it does

- Scans groceries from a photo, barcode, or manual entry.
- Tracks expiration with a freshness bar: fresh → expiring → expired.
- Shows nutrition facts for each item.
- Suggests recipes and substitutions based on pantry items, prioritizing food that expires soonest.
- Supports dietary preferences set during onboarding or in Settings.
- Expiry push notifications are in progress.

## Screenshots

| Home | Inventory | Scan | Chat |
|---|---|---|---|
| ![Home](media/home.png) | ![Inventory](media/inventory.png) | ![Scan](media/scan.png) | ![Chat](media/chat.png) |

## Built with

- **App:** React Native, React Navigation, Zustand, Reanimated
- **Backend:** Supabase (Postgres, Auth, Edge Functions with TypeScript/Deno)
- **AI:** Gemini Flash for item recognition, Claude fallback when confidence is low, Claude Haiku for chat
- **Food data:** Open Food Facts, USDA FoodData Central
- **Subscriptions and notifications:** RevenueCat, OneSignal

## Architecture

![Pantree architecture](media/architecture.png)

The app sends requests to Supabase Edge Functions; it never calls AI providers directly. Edge Functions keep API keys on the backend, enforce plan limits, call AI models, and write to the database. All tables use row-level security.

## Engineering highlights

- Uses confidence-based fallback from a lower-cost model to a stronger model.
- Enforces quotas server-side with atomic updates, including for parallel requests and modified clients.
- Keeps AI and payment keys on the backend.
- Syncs subscription changes to the database through webhooks.
- Uses idempotent expiry notifications to prevent duplicate alerts.

## Status

In development. Solo project; I built the full stack.

## About me

- **Name:** [name]
- **School / year:** [school/year]
- **LinkedIn:** [LinkedIn]
- **Email:** [email]

## License

Copyright (c) 2026 [name]. All rights reserved.