# ios.hyperlimit.app

Landing page and Universal Links handler for [Limit](https://github.com/P24L/Limit) - Premium Bluesky Client for iOS.

## Features

- 🌐 Landing page for the iOS app
- 🔗 Universal Links support for bookmark sharing
- 📱 Apple App Site Association (AASA) file
- 🎨 Modern gradient design

## Structure

```
/
├── .well-known/
│   └── apple-app-site-association  # iOS app association file
├── bookmark/
│   └── index.html                  # Bookmark redirect handler
├── index.html                      # Landing page
├── CNAME                           # Custom domain configuration
└── _config.yml                     # Jekyll configuration
```

## Universal Links

The site handles Universal Links in the format:
- `https://ios.hyperlimit.app/bookmark/{did}/{collection}/{rkey}`
- `https://ios.hyperlimit.app/b/{did}/{collection}/{rkey}` (shortened)

## Deployment

This site is automatically deployed via GitHub Pages to [ios.hyperlimit.app](https://ios.hyperlimit.app).

## Main App

- [GitHub Repository](https://github.com/P24L/Limit)
- [App Store](https://apps.apple.com/app/limit-for-sky/id6748037680)