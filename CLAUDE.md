# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the landing page and Universal Links handler for Limit - a premium Bluesky client for iOS. The site is deployed via GitHub Pages to ios.hyperlimit.app and serves three main purposes:
1. Marketing landing page for the iOS app
2. Universal Links handler for bookmark sharing between app users
3. Fallback web experience for users without the app

## Deployment and Development

### Local Development
Since this is a static site deployed on GitHub Pages, local development is straightforward:
```bash
# Serve the site locally with any static server
python3 -m http.server 8000
# Or with Node.js
npx serve .
```

### Deployment
The site automatically deploys to GitHub Pages when changes are pushed to the main branch. Configuration is handled through:
- `_config.yml` - Jekyll configuration for GitHub Pages
- `CNAME` - Custom domain configuration (ios.hyperlimit.app)

## Architecture and URL Routing

### Universal Links Structure
The site handles bookmark sharing via Universal Links in two formats:
- `/bookmark/{did}/{collection}/{rkey}` - Full format
- `/b/{did}/{collection}/{rkey}` - Shortened format

These URLs trigger the iOS app to open (if installed) via:
1. **Apple App Site Association (AASA)** - `.well-known/apple-app-site-association` configures Universal Links
2. **Custom 404 Handler** - `404.html` acts as a dynamic router for bookmark URLs
3. **Deep Link Fallback** - JavaScript attempts `limit://` custom scheme as backup

### Key Components

1. **Landing Page** (`index.html`)
   - Marketing page with gradient design
   - Features overview and App Store download link
   - Links to privacy policy, GitHub, and Bluesky profile

2. **Bookmark Handler** (`404.html`)
   - Handles all `/bookmark/*` and `/b/*` URLs via GitHub Pages 404 routing
   - Platform detection (iOS vs desktop)
   - Smart App Banner integration for iOS
   - Progressive fallback strategy:
     - First: Universal Link (automatic on iOS)
     - Then: Custom scheme deep link attempt
     - Finally: App Store download prompt

3. **Legacy Bookmark Page** (`bookmark/index.html`)
   - Original bookmark handler (kept for backward compatibility)
   - Similar functionality to 404.html but less sophisticated

4. **AASA Configuration** (`.well-known/apple-app-site-association`)
   - Configures Universal Links for both production and dev app bundles
   - Team ID: 6U9V38M6H4
   - Bundle IDs: P24L.Limit and P24L.Limit.dev

## URL Handling Flow

When a user visits a bookmark URL:
1. GitHub Pages serves `404.html` for unmatched routes
2. JavaScript parses the URL to extract bookmark parameters
3. On iOS: Attempts to open the app via Universal Link or custom scheme
4. On desktop: Shows instructions to open on iOS device
5. If app not installed: Prompts to download from App Store

## Important Notes

- The site uses client-side JavaScript for all dynamic behavior
- No server-side processing or API calls required
- Platform detection differentiates iOS from desktop experience
- Smart App Banner provides native iOS integration
- History manipulation prevents back button loops after redirects