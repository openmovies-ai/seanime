# Seanime Codebase Review

## Overview
Seanime is a self-hosted media server for managing local anime and manga libraries, with web and desktop interfaces. It integrates with external services for metadata and tracking but supports offline operation.

## Local Operation Capability
**Yes, the app can run entirely locally.**
- Core features (library scanning, local playback, manga reading) work without internet.
- Offline mode disables external APIs and uses cached/local data.
- External features (AniList tracking, torrents, online streaming) require internet but are optional.

## Disk Space Requirements
The app itself requires **50-150MB** of disk space:
- Go binary: ~30-60MB (includes embedded web UI and dependencies).
- Desktop apps (Electron/Tauri): ~100-150MB total.
- Media files are stored separately and can be gigabytes/terabytes.

## Must-Have External APIs
These APIs are essential for full functionality (metadata, tracking, extensions):

1. **AniList API** (`https://graphql.anilist.co`)
   - Primary platform for anime/manga tracking and metadata.
   - Free, GraphQL-based, supports anonymous and authenticated queries.

2. **Internal Metadata API** (`https://anime.clap.ing`)
   - Provides detailed anime metadata and ID mappings.
   - Free, publicly accessible.

3. **MyAnimeList (MAL) API**
   - Alternative tracking platform with client ID `51cb4294feb400f3ddc66a30f9b9a00f`.
   - Free, with 60 requests/minute limit.

4. **Seanime Rooms API** (`https://seanime.app/api/rooms`)
   - Handles real-time features (WebSocket connections).
   - Free, part of Seanime's infrastructure.

5. **Extensions Marketplace API** (GitHub raw: `https://raw.githubusercontent.com/5rahim/seanime-extensions/refs/heads/main/marketplace.json`)
   - Fetches community extensions for torrents and streaming.
   - Free, hosted on GitHub.

6. **Announcements API** (GitHub raw: `https://raw.githubusercontent.com/5rahim/hibiki/refs/heads/main/public/announcements.json`)
   - Provides app updates and announcements.
   - Free, hosted on GitHub.

## API Cost Analysis
**All listed APIs are free:**
- No payment or premium tiers required.
- Reasonable rate limits for typical use.
- Seanime includes caching to minimize requests.
- Services may have occasional downtime, but offline mode provides fallback.

## Architecture Notes
- Built in Go with embedded Next.js web UI.
- Uses SQLite for local database.
- Supports multiple platforms (AniList primary, offline fallback).
- Extensions system for torrent/debrid integration.
- No external dependencies for core local functionality.