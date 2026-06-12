# EOS — Everything On Sight
## An AI-Native OS for Even Reality G2 Smart Glasses

---

### Vision Statement
EOS is a lightweight, AI-first operating system for Even Reality G2 smart glasses where your **phone acts as a compute tether** and the **glasses are your always-available display**. An AI agent lives on your phone, listens through your glasses, searches the web on your behalf, and surfaces answers as simple text in your field of view.

---

### System Architecture

```
┌─────────────────────────────────────┐
│         EVEN REALITY G2             │
│  ┌───────────────────────────────┐  │
│  │      EOS LENS LAYER          │  │
│  │  ─ Text rendering engine     │  │
│  │  ─ Voice input (mic)         │  │
│  │  ─ Audio output (speaker)    │  │
│  │  ─ Gesture/head controls     │  │
│  └───────────┬───────────────────┘  │
└──────────────│──────────────────────┘
               │ Bluetooth / WiFi
┌──────────────▼──────────────────────┐
│      PHONE APP (COMPUTE TETHER)     │
│  ┌───────────────────────────────┐  │
│  │       EOS CORE ENGINE        │  │
│  │  ├─ Speech-to-Text (STT)    │  │
│  │  ├─ AI Agent (LLM)          │  │
│  │  ├─ Web Browser Agent       │  │
│  │  └─ Result→Text pipeline    │  │
│  ├───────────────────────────────┤  │
│  │       EOS APP STORE          │  │
│  │  ├─ Third-party mini apps    │  │
│  │  ├─ Permissions manager     │  │
│  │  └─ App discovery           │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

---

### Core Flow: "The Ask"

| Step | Action | Location |
|------|--------|----------|
| 1 | User speaks a question ("What's the weather in Tokyo?") | Glasses mic |
| 2 | Audio streamed to phone via Bluetooth/WiFi | Connection |
| 3 | Speech-to-Text converts audio to text | Phone |
| 4 | AI Agent receives query, decides search strategy | Phone |
| 5 | Agent opens headless browser, searches Google | Phone |
| 6 | Agent navigates results, extracts answer | Phone |
| 7 | Answer formatted as clean plain text | Phone |
| 8 | Text sent back to glasses | Connection |
| 9 | Text rendered in user's field of view | Glasses display |
| 10 | *(Optional)* Agent speaks answer aloud | Glasses speaker |

---

### Core Features

| Feature | Description |
|---------|-------------|
| **AI Voice Agent** | Ask questions naturally, get answers instantly |
| **Web Browser Agent** | Agent browses the web *for you* — no visual browser needed |
| **Text Overlay Display** | Clean, minimal text in your field of view |
| **Notification Mirroring** | Phone notifications relayed to glasses |
| **Third-Party App Store** | Extend functionality with mini apps |
| **Gesture Controls** | Navigate, dismiss, scroll with head gestures/taps |
| **Settings & Config** | Manage agent behavior, display prefs, paired devices |

---

### Third-Party App Model

Apps are **web-based mini apps** invoked by the AI agent:

| Concept | Detail |
|---------|--------|
| **Weather App** | Agent visits a weather site, renders forecast as text |
| **News App** | Agent fetches headlines, shows bullet list |
| **Navigation** | Agent pulls directions, shows turn-by-turn text |
| **Social Feed** | Agent fetches recent posts, scrollable text |
| **Developer Model** | Submit: manifest.json + agent prompt + optional API keys |

---

### Why This Works

✅ **Phone does the heavy lifting** — glasses stay light, battery efficient  
✅ **Simple text output** — AR text is proven, readable, reliable  
✅ **Agent as browser** — no need to build a visual browser for glasses  
✅ **Any website = potential app** — web is the platform  
✅ **No app ecosystem chicken-and-egg** — agent can browse anything from day one  

---

### Next Steps

1. Prototype phone app (AI agent + browser pipeline)
2. Prototype glasses display layer (text rendering)
3. Build the Ask flow end-to-end
4. Define app manifest format
5. Developer SDK documentation