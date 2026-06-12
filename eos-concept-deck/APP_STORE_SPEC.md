# EOS App Store Specification
## Third-Party App Model & Developer Documentation

---

### 1. Overview

EOS apps are **web-based mini apps** invoked by the AI agent on demand. Developers define the app's behavior through a manifest file and a natural-language prompt that tells the agent how to use the app.

No native code required. No SDK installation. Just a manifest and a prompt.

---

### 2. App Manifest Format

Every EOS app requires a `manifest.json` file:

```json
{
  "eos_app_version": "1.0",
  "app_id": "com.mapdev.city-navigator",
  "name": "City Navigator",
  "version": "1.2.0",
  "description": "Turn-by-turn navigation via text overlay",
  "icon": "🗺️",
  
  "author": {
    "name": "MapDev Studio",
    "email": "dev@mapdev.example"
  },

  "agent_prompt": "When the user asks for directions, navigate to a location, "
                  "or find a place, use Google Maps to get turn-by-turn "
                  "directions. Extract the step-by-step instructions and "
                  "display them as a numbered list. Show estimated time "
                  "and distance at the top.",

  "website_urls": [
    "https://maps.google.com",
    "https://google.com/maps/dir/*"
  ],

  "permissions": [
    "location"
  ],

  "categories": ["navigation", "travel"],

  "screenshots": [
    "https://cdn.example.com/eos/screenshot1.png"
  ]
}
```

### Manifest Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `eos_app_version` | string | ✅ | EOS manifest format version |
| `app_id` | string | ✅ | Reverse-domain identifier |
| `name` | string | ✅ | Human-readable app name |
| `version` | string | ✅ | Semantic version |
| `description` | string | ✅ | Short description (max 200 chars) |
| `icon` | string | ✅ | Single emoji or URL |
| `author` | object | ✅ | Developer contact info |
| `agent_prompt` | string | ✅ | Instructions for the AI agent |
| `website_urls` | string[] | Optional | Allowed websites the agent can browse |
| `permissions` | string[] | Optional | Required permissions |
| `categories` | string[] | Optional | App store categorization |
| `screenshots` | string[] | Optional | Show in app listing |

---

### 3. The Agent Prompt

The `agent_prompt` is the **heart of the app**. It's a natural language instruction injected into the AI agent's system prompt when the app is invoked.

#### Example: Weather App Prompt

```
When the user asks about weather, forecasts, or climate conditions:
1. Visit weather.com or accuweather.com for the requested location
2. Extract: current temperature, conditions, high/low, humidity, wind
3. Format as:
   [Location]
   Currently: [temp]°F - [conditions]
   High: [high]° | Low: [low]°
   Humidity: [humidity]%
   Wind: [wind speed] [direction]
   [Source: weather.com]
4. If the user asks for a multi-day forecast, show each day in a scrollable list
5. Keep it concise — no fluff
```

#### Best Practices

| Practice | Why |
|----------|-----|
| Be specific about URLS | Agent won't waste time browsing irrelevant sites |
| Define output format | Consistent UX across all apps |
| Include error handling | "If the site is unavailable, try source B" |
| Limit scope | Focused prompts = better results |
| Use examples | Show the agent what good output looks like |

---

### 4. Permissions Model

| Permission | Description | User Prompt |
|------------|-------------|-------------|
| `location` | Access device GPS | "City Navigator needs your location for directions. Allow?" |
| `contacts` | Access phone contacts | "App needs access to your contacts." |
| `notifications` | Send proactive info | "App can send updates to your glasses." |
| `calendar` | Read calendar events | "App can check your schedule." |
| `microphone` | Real-time audio access | Rare — only for voice-forward apps |
| `photos` | Access photo library | For camera/sharing apps |

Permissions are requested at install time and can be revoked at any time from Settings.

---

### 5. Developer Workflow

```
1. CREATE
   ┌──────────────────────┐
   │ Write manifest.json  │
   │ Write agent_prompt   │
   │ Test with simulator  │
   └──────────┬───────────┘
              │
2. SUBMIT    ▼
   ┌──────────────────────┐
   │ Submit via EOS       │
   │ Developer Portal     │
   │ (or GitHub PR)       │
   └──────────┬───────────┘
              │
3. REVIEW    ▼
   ┌──────────────────────┐
   │ Automated:           │
   │  - Manifest valid    │
   │  - URLs reachable    │
   │  - No malicious      │
   │  prompt patterns     │
   │                      │
   │ Manual (optional):   │
   │  - Quality review    │
   └──────────┬───────────┘
              │
4. PUBLISH   ▼
   ┌──────────────────────┐
   │ App appears in       │
   │ EOS App Store        │
   │ within 24 hours      │
   └──────────────────────┘
```

---

### 6. App Categories

| Category | Example Apps |
|----------|--------------|
| 🔍 Search & Reference | Wikipedia, Dictionary, Stack Overflow |
| 🗺️ Navigation | City Navigator, Transit Finder |
| 📰 News & Info | BBC Reader, Hacker News, ESPN Scores |
| 🌤️ Weather | Weather Now, Radar Viewer |
| 🎵 Music & Audio | Song Finder, Concert Alerts |
| 🍔 Food & Drink | Restaurant Finder, Recipe Guide |
| 🏋️ Health & Fitness | Step Counter, Workout Timer |
| 🛒 Shopping | Price Compare, Product Search |
| 🎮 Entertainment | Trivia, Word Games (text-based) |
| 🔧 Productivity | Timer, Calculator, Todo List |
| 💻 Developer Tools | JSON Viewer, Regex Tester, API Checker |
| 🧪 AI Experiments | Custom agent prompts (experimental) |

---

### 7. Example Apps

#### 7.1 News Reader

```json
{
  "app_id": "com.news.bbc-reader",
  "name": "BBC News Reader",
  "icon": "📰",
  "agent_prompt": "When the user asks for news, visit bbc.com/news. "
                  "Extract the top 5 headlines with brief summaries. "
                  "Format as a numbered list with [Headline] - [1-sentence summary]. "
                  "Add a source footer.",
  "permissions": [],
  "website_urls": ["https://bbc.com/news"],
  "categories": ["news"]
}
```

#### 7.2 Stock Tracker

```json
{
  "app_id": "com.finance.stock-tracker",
  "name": "Stock Tracker",
  "icon": "📈",
  "agent_prompt": "When the user asks about stock prices or market data: "
                  "1. Visit finance.yahoo.com to look up the ticker "
                  "2. Extract: current price, change ($ and %), day range "
                  "3. Format: [TICKER] $[price] [Δ$] ([Δ%]) | Day: [low]-[high] "
                  "4. Source: finance.yahoo.com",
  "permissions": [],
  "website_urls": ["https://finance.yahoo.com"],
  "categories": ["finance"]
}
```

#### 7.3 Timer App

```json
{
  "app_id": "com.eos.timer",
  "name": "Timer",
  "icon": "⏱️",
  "agent_prompt": "This is a built-in timer utility. When the user asks to "
                  "set a timer for X minutes, start counting down on the phone "
                  "and show remaining time on the glasses display every 30 seconds. "
                  "When the timer completes, alert the user with a message and sound. "
                  "No external websites needed.",
  "permissions": ["notifications"],
  "website_urls": [],
  "categories": ["productivity"]
}
```

---

### 8. Review Guidelines

| Check | Rule |
|-------|------|
| Manifest validity | All required fields present and correctly formatted |
| Prompt safety | No instructions to extract user data, bypass security, or access unauthorized sites |
| URL whitelist | All website_urls must be HTTPS and publicly accessible |
| Permissions | App must only request permissions it actually needs |
| Functionality | App must actually work when tested (automated) |
| Content policy | No adult content, spam, or hateful prompts |
| Quality | Agent prompt must produce readable, useful output |

---

### 9. Monetization (Future)

| Model | Description |
|-------|-------------|
| Free | No cost, available to all users |
| Premium | One-time purchase for advanced features |
| Subscription | Recurring revenue for ongoing services |
| Freemium | Basic free tier, premium paid features |

Revenue split: **70/30** (developer / EOS platform) — industry standard.

---

### 10. Developer Resources

- **Template Repository**: GitHub template for scaffolding new apps
- **Simulator**: Test your app against the EOS agent locally
- **Documentation**: Full agent prompt engineering guide
- **Community Forum**: Share tips and get feedback
- **Sample Apps**: Open-source reference implementations