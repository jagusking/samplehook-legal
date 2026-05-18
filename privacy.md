---
title: SampleHook Privacy Policy
permalink: /privacy/
layout: default
---

# SampleHook Privacy Policy

**Last updated: May 18, 2026**

SampleHook ("the app", "we", "us") is an iOS app that helps producers generate
short vocal samples from a guide recording using third-party AI services. This
Privacy Policy explains exactly what data we handle, why, and where it goes.

We've kept this policy short and specific. If anything is unclear, email us at
**privacy@samplehook.app** and we'll answer in plain English.

## 1. Data we collect

We collect only what's necessary to deliver the generation service:

| Data | Purpose | Where it lives |
|---|---|---|
| **Device identifier** — a random UUID generated on first launch via Apple's `identifierForVendor`. Not your Apple ID, not your name, not your email. | Tracks your monthly credit balance, tier (free / Pro), and per-hour rate limit. | Cloudflare KV, indefinitely (until you delete the app and reinstall). |
| **Recorded guide audio** — the 1–10 second take you record before generating. | Uploaded to our backend so the AI can transcribe lyrics (Whisper) and reference your melody (Suno). | Cloudflare R2, deleted automatically after 30 minutes via a lifecycle rule. We do **not** retain guide recordings. |
| **Generated audio** — the AI-produced vocal returned to your phone. | Delivered to your device for playback / use in your DAW. | Hosted on Suno's servers (presigned URL, ~72 hour expiry) and Replicate's servers (~1 hour expiry). We do not re-host. Your phone caches the final WAV in the app's local Library. |
| **Transcribed lyrics** — text that Whisper extracts from your guide audio. | Pre-populates the lyric-review screen so you can edit before generation. | Held in Cloudflare KV for at most 30 minutes (paired with the temporary R2 audio handle), then deleted. |
| **In-app purchase transaction ID** — the StoreKit `transactionId` for your Pro subscription or credit pack. | Validates your purchase, prevents replay, applies your tier. | Cloudflare KV, retained 60 days for replay protection. |

## 2. What we do NOT collect

- ❌ Your name, email address, phone number, or any Apple ID detail
- ❌ Your location, contacts, photos, or any other system permission beyond microphone
- ❌ Advertising identifiers (IDFA) — we don't run ads
- ❌ Crash analytics from third parties — we use only Apple's built-in TestFlight crash reporting
- ❌ Any behavioral / usage analytics

## 3. Third-party services that process your data

When you tap **Generate**, your recorded audio + selected tags travel through
the following services to produce the result:

| Service | What we send | Why | Their privacy policy |
|---|---|---|---|
| **Cloudflare** (Workers, KV, R2, Workers AI) | Guide audio, tags, device UUID | Backend orchestration, Whisper transcription, temporary audio storage | [cloudflare.com/privacypolicy](https://www.cloudflare.com/privacypolicy/) |
| **Suno** (via the EvoLink gateway) | Style tags, transcribed lyrics, and a public URL to your guide audio | Generates the vocal sample | [suno.com/privacy](https://suno.com/privacy) · [evolink.ai/privacy](https://evolink.ai/privacy) |
| **Replicate** | The Suno-generated audio URL | Isolates the vocal stem via demucs | [replicate.com/privacy](https://replicate.com/privacy) |
| **ElevenLabs** (Tight mode only, currently hidden in v1) | Guide audio + voice selection | Voice conversion | [elevenlabs.io/privacy](https://elevenlabs.io/privacy) |
| **Apple StoreKit** | Purchase receipt | Validates IAP transactions | [apple.com/legal/privacy](https://www.apple.com/legal/privacy/) |

We don't share your data with anyone outside of what's required to produce the
generation you requested. We don't sell, rent, or trade any data.

## 4. Data retention summary

- Guide audio uploads: **30 minutes** (R2 lifecycle rule)
- Transcription handles: **30 minutes** (KV TTL)
- Generated audio: not retained server-side; available from the AI providers' CDNs for 1–72 hours
- Device credit record: **until you delete the app** (and Apple resets `identifierForVendor`)
- IAP transaction IDs: **60 days** for replay protection

## 5. Your rights

Because we don't store any personally identifying information, there's no
account to delete and no profile to edit. To completely erase your SampleHook
data: delete the app from your device. Apple resets the per-vendor UUID, which
breaks the link between your phone and the Cloudflare credit record.

If you'd like us to forcibly purge the credit record sooner — for example
before selling your device — email **privacy@samplehook.app** with the device
UUID (visible in the app's About screen) and we'll delete it within 7 days.

## 6. Children

SampleHook is rated 12+ on the App Store and is not directed at children under
13. We don't knowingly collect data from anyone under 13. If you believe a
child has used the app, email **privacy@samplehook.app** and we'll delete the
associated record.

## 7. Changes to this policy

If we materially change how data is handled, we'll update this page and bump
the "Last updated" date. We'll also note material changes in the next app
release notes.

## 8. Contact

Questions, concerns, deletion requests: **privacy@samplehook.app**
