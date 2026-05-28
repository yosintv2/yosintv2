# YoSinTV

## Overview

YoSinTV is a sports streaming and live match information platform focused on delivering cricket and football content through web and mobile platforms.

The platform uses a dynamic configuration system powered by remote JSON files, allowing content and features to update without requiring full application updates.

---

# Features

## Live Match System

* Cricket live matches
* Football live matches
* Match schedules
* Match countdowns
* Live status indicators
* Backup stream support
* Responsive player layouts

---

# Match Status Logic

The platform supports automated match states:

| Status      | Description                 |
| ----------- | --------------------------- |
| Coming Soon | Before scheduled start      |
| Start Soon  | Shortly before match starts |
| Live Now    | Match currently live        |
| Match End   | Match completed             |

---

# Platform Components

## Website

* Responsive design
* Dynamic content loading
* Remote configuration support
* Ad-supported layout
* Embedded players

## Android App

Built using Flutter.

Features include:

* Remote config support
* Dynamic match loading
* AdMob integration
* Embedded streaming support
* Automatic content updates

---

# Configuration System

The project uses remotely managed JSON configurations.

Supported configuration areas:

* Branding
* Theme colors
* Match data
* Notices
* Feature toggles
* Popup controls
* Stream settings
* API endpoints
* Advertisement controls

---

# Advertisement System

Supported ad formats:

* Banner ads
* Popup ads
* Overlay ads
* Video ads

Features:

* Timed ad display
* Auto-close support
* Redirect support
* Configurable ad frequency

---

# Streaming Features

* iframe player support
* External stream support
* Multiple stream links
* Video pre-roll support
* Skip functionality
* Responsive layouts

---

# Admin Utilities

Internal management tools support:

* Match editing
* JSON editing
* Search and replace utilities
* Live content updates

---

# Branding

YoSinTV also produces sports-related social media content for platforms like TikTok and short-video services.

Content includes:

* Match previews
* Live announcements
* Sports updates
* Promotional graphics

---

# Tech Stack

## Frontend

* HTML
* CSS
* JavaScript

## Mobile

* Flutter

## Backend/Data

* JSON APIs
* CDN-hosted assets
* Remote configuration system

---

# Goals

* Fast live match updates
* Lightweight streaming experience
* Remote-controlled content management
* Easy scalability
* Mobile-first usability

---

# Important Notes

* Sensitive URLs, API keys, ad IDs, tokens, and private infrastructure details are intentionally excluded from this public documentation.
* Environment-specific configurations should be stored securely and never committed publicly.
* Private credentials should be managed using environment variables or private configuration files.

---

# Repository Structure (Example)

```bash
/assets
/config
/js
/css
/flutter-app
/api
/admin
```

---

# Future Improvements

* Advanced admin dashboard
* Push notifications
* Better analytics
* Enhanced player UI
* Improved backup systems
* Multi-language support

---

# License

Private / Custom License

---

# Author

YoSinTV
