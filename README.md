# Pantree

A mobile pantry app that turns grocery photos into an inventory and helps you use food before it expires.

> The source code is private. Feel free to reach out for a read-only access.

## What it does

- Scans groceries from a photo, barcode, or manual entry.
- Tracks expiration with a freshness bar: fresh → expiring → expired.
- Shows nutrition facts for each item.
- Suggests recipes and substitutions based on pantry items, prioritizing food that expires soonest.
- Supports dietary preferences set during onboarding or in Settings.
- Expiry push notifications are in progress.

## Built with

- **App:** React Native, React Navigation, Zustand, Reanimated
- **Backend:** Supabase (Postgres, Auth, Edge Functions with TypeScript/Deno)
- **AI:** Gemini Flash for item recognition, Claude fallback when confidence is low, Claude Haiku for chat
- **Food data:** Open Food Facts, USDA FoodData Central
- **Subscriptions and notifications:** RevenueCat, OneSignal

## Architecture

The app sends requests to Supabase Edge Functions; it never calls AI providers directly. Edge Functions keep API keys on the backend, enforce plan limits, call AI models, and write to the database. All tables use row-level security.

## Engineering highlights

- Uses confidence-based fallback from a lower-cost model to a stronger model.
- Enforces quotas server-side with atomic updates, including for parallel requests and modified clients.
- Keeps AI and payment keys on the backend.
- Syncs subscription changes to the database through webhooks.
- Uses idempotent expiry notifications to prevent duplicate alerts.

## Status

In development
