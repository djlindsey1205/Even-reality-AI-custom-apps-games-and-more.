# EOS UX Flow Guide
## User Journeys & Experience Design

---

## Journey 1: "Ask a Question"

```
┌──────────────────────────────────────────────────────────────────┐
│  USER: "Hey EOS, what's the weather in Tokyo?"                   │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: [Mic activates] Recording... ▌                          │
│           [Small red dot in corner indicates listening]          │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: [Processing...]  ⟳                                     │
│           (Brief wait state, subtle animation)                    │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌──────────────────────────────────┐                   │
│           │  🌤  Tokyo, Japan                 │                   │
│           │  Currently: 72°F (22°C)          │                   │
│           │  Feels like: 68°F                │                   │
│           │  Conditions: Partly Cloudy       │                   │
│           │  Humidity: 65%                   │                   │
│           │  ──────────────────────────────  │                   │
│           │  Later: 76°F / Clear skies       │                   │
│           │  [Source: weather.com]           │                   │
│           └──────────────────────────────────┘                   │
│                                                                  │
│  (Text fades after 10 seconds, or dismiss with head nod / tap)   │
└──────────────────────────────────────────────────────────────────┘
```

### States & Transitions

| State | Visual | Duration | Action |
|-------|--------|----------|--------|
| Idle | Transparent / time only | Indefinite | Say wake word or tap |
| Listening | Red dot + "Listening..." | Until speech ends | Speak question |
| Processing | Spinner ⟳ + "Thinking..." | 1-8 seconds | Wait |
| Answer | Text card with answer | 10 seconds auto | Read + nod/tap to dismiss |
| Error | "Sorry, I couldn't find that" | 5 seconds | Retry or rephrase |

---

## Journey 2: Web Search with Agent

```
┌──────────────────────────────────────────────────────────────────┐
│  USER: "Find me the best ramen shops in Shinjuku"                │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: [Agent searching the web...]                           │
│           ┌────────────────────────────────────┐                 │
│           │  🔍 Searching: "best ramen shops   │                 │
│           │     shinjuku tokyo"                 │                 │
│           │  ████████░░ 78% complete           │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  🍜  Top Ramen in Shinjuku         │                 │
│           │                                     │                 │
│           │  1. Ichiran Shinjuku                │                 │
│           │     ⭐ 4.3 | ¥1,200                │                 │
│           │     ────────────────────            │                 │
│           │  2. Afuri Shinjuku                  │                 │
│           │     ⭐ 4.2 | ¥1,100                │                 │
│           │     ────────────────────            │                 │
│           │  3. Fuunji                          │                 │
│           │     ⭐ 4.1 | ¥950                  │                 │
│           │                                     │                 │
│           │  [Tap for details | Scroll for more]│                 │
│           └────────────────────────────────────┘                 │
│           (Head tilt up/down to scroll)                          │
└──────────────────────────────────────────────────────────────────┘
```

### Scroll Interaction

| Gesture | Action |
|---------|--------|
| Head tilt up | Scroll up |
| Head tilt down | Scroll down |
| Double tap (glasses frame) | Select / open details |
| Swipe back (frame gesture) | Go back / dismiss |
| Head nod | Confirm / yes |
| Head shake | Cancel / no |

---

## Journey 3: App Installation

```
┌──────────────────────────────────────────────────────────────────┐
│  USER: "Open the app store"                                      │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  📦  EOS App Store                  │                 │
│           │                                     │                 │
│           │  ┌──────────────────────────────┐   │                 │
│           │  │ 🔍 Search apps...            │   │                 │
│           │  └──────────────────────────────┘   │                 │
│           │                                     │                 │
│           │  Featured                           │                 │
│           │  ┌─────────────────────────────┐   │                 │
│           │  │ 📰 News Reader          ★  │   │                 │
│           │  │ Fetch headlines from BBC │   │                 │
│           │  ├─────────────────────────────┤   │                 │
│           │  │ 🗺️  City Navigator      ★  │   │                 │
│           │  │ Turn-by-turn directions  │   │                 │
│           │  ├─────────────────────────────┤   │                 │
│           │  │ 🎵 Music Finder         New │   │                 │
│           │  │ Find songs near you     │   │                 │
│           │  └─────────────────────────────┘   │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
                              │
         USER: "Install City Navigator"
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  🗺️  City Navigator              │                 │
│           │  by MapDev Studio                  │                 │
│           │                                     │                 │
│           │  Turn-by-turn navigation via text   │                 │
│           │  overlay in your field of view      │                 │
│           │                                     │                 │
│           │  Permissions requested:             │                 │
│           │  ✅ Location                        │                 │
│           │  ❌ Contacts                        │                 │
│           │  ❌ Microphone                      │                 │
│           │                                     │                 │
│           │  ┌────────────────────────────┐     │                 │
│           │  │     Install App            │     │                 │
│           │  └────────────────────────────┘     │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
                              │
         USER: "Install" (tap)
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  ✅ City Navigator installed!      │                 │
│           │                                     │                 │
│           │  Say "Open City Navigator" or       │                 │
│           │  "Navigate to Shibuya Station"       │                 │
│           │                                     │                 │
│           │              [Dismiss]              │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
```

---

## Journey 4: Notifications

```
┌──────────────────────────────────────────────────────────────────┐
│  PHONE: Receives iMessage / SMS / App notification               │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  💬  Sarah                          │                 │
│           │  "Are we still on for dinner at     │                 │
│           │   7pm?"                            │                 │
│           │                                     │                 │
│           │  [Tap to reply] [Dismiss]           │                 │
│           └────────────────────────────────────┘                 │
│           (Fades after 8 seconds if not interacted with)          │
└──────────────────────────────────────────────────────────────────┘
                              │
         USER: "Reply: Yes, see you there!"
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  ✅ Message sent!                   │                 │
│           │                                     │                 │
│           │  Said: "Yes, see you there!"        │                 │
│           │                                     │                 │
│           │              [Dismiss]              │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
```

---

## Journey 5: Settings & Configuration

```
┌──────────────────────────────────────────────────────────────────┐
│  USER: "Open settings"                                           │
└──────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│  GLASSES: ┌────────────────────────────────────┐                 │
│           │  ⚙️  EOS Settings                  │                 │
│           │                                     │                 │
│           │  ├─ Agent                           │                 │
│           │  │  • Personality: Professional     │                 │
│           │  │  • Verbosity: Balanced           │                 │
│           │  │  • Auto-speak answers: Off       │                 │
│           │  │                                   │                 │
│           │  ├─ Display                          │                 │
│           │  │  • Text size: Medium              │                 │
│           │  │  • Brightness: Auto               │                 │
│           │  │  • Time before fade: 10s          │                 │
│           │  │                                   │                 │
│           │  ├─ Notifications                    │                 │
│           │  │  • Show on glasses: On            │                 │
│           │  │  • Apps: Select...                │                 │
│           │  │                                   │                 │
│           │  ├─ Bluetooth                        │                 │
│           │  │  • Connected: EOS Glasses         │                 │
│           │  │                                   │                 │
│           │  └─ About                            │                 │
│           │     • EOS v1.0.0                     │                 │
│           │     • Build 2026.12                  │                 │
│           └────────────────────────────────────┘                 │
└──────────────────────────────────────────────────────────────────┘
```

---

## Display Guidelines

### Text Card Design

```
┌──────────────────────────────────────┐
│  [Icon/Emoji]  Title/Header          │  ← Max 2 lines
│                                      │
│  Main content text goes here...      │  ← Max 8 lines
│  Wrapped cleanly within the card     │
│                                      │
│  ──────────────────────────────────  │  ← Divider (optional)
│  [Footer / Source / Timestamp]       │  ← Max 1 line
└──────────────────────────────────────┘
```

### Visual Rules

| Rule | Value |
|------|-------|
| Max lines per card | 10 |
| Max characters per line | 40 (including spaces) |
| Font | Monospace or clean sans-serif |
| Background | Semi-transparent dark (glass-like) |
| Text color | White / high contrast |
| Border radius | 12px |
| Margin from view edges | 20px minimum |
| Auto-dismiss timeout | 10 seconds (configurable) |
| Fade animation | 500ms ease-out |