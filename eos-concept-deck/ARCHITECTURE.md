# EOS System Architecture
## Technical Architecture Document

---

### 1. High-Level Component Diagram

```
┌────────────────────────────────────────────────────────────┐
│                    EVEN REALITY G2                          │
│                        (LENS LAYER)                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │ Voice Input  │  │ Text Display │  │ Gesture/Head     │  │
│  │ (Mic Stream) │  │ (OLED/AR)    │  │ Controls         │  │
│  └──────┬───────┘  └──────▲───────┘  └──────────────────┘  │
└─────────┼─────────────────┼─────────────────────────────────┘
          │ Bluetooth/WiFi  │
          │ (Audio Stream)  │ (Text Output)
┌─────────▼─────────────────▼─────────────────────────────────┐
│                    PHONE APP                                 │
│                  (COMPUTE TETHER)                            │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │               EOS CORE ENGINE                        │   │
│  │                                                      │   │
│  │  ┌──────────────┐    ┌───────────────────────────┐  │   │
│  │  │ STT Pipeline │───>│  AI Agent                 │  │   │
│  │  │ (Whisper /   │    │  ┌─────────────────────┐  │  │   │
│  │  │  on-device)  │    │  │ Intent Router       │  │  │   │
│  │  └──────────────┘    │  │  ├─ Web Search      │  │  │   │
│  │                      │  │  ├─ App Invocation  │  │  │   │
│  │  ┌──────────────┐    │  │  └─ Direct Answer   │  │  │   │
│  │  │ TTS Pipeline │<───│  └─────────────────────┘  │  │   │
│  │  │ (on-device)  │    └───────────────────────────┘  │   │
│  │  └──────────────┘                                    │   │
│  │                                                      │   │
│  │  ┌──────────────────────────────────────────────┐   │   │
│  │  │         Web Browser Agent                    │   │   │
│  │  │  ┌──────────┐  ┌──────────┐  ┌──────────┐   │   │   │
│  │  │  │ Headless │  │ Page     │  │ Content  │   │   │   │
│  │  │  │ Browser  │─>│ Reader   │─>│ Extractor│   │   │   │
│  │  │  └──────────┘  └──────────┘  └──────────┘   │   │   │
│  │  └──────────────────────────────────────────────┘   │   │
│  │                                                      │   │
│  │  ┌──────────────────────────────────────────────┐   │   │
│  │  │         Memory & Context Manager             │   │   │
│  │  │  ┌──────────┐  ┌──────────┐  ┌──────────┐   │   │   │
│  │  │  │ Session  │  │ User     │  │ App      │   │   │   │
│  │  │  │ History  │  │ Profile  │  │ Registry │   │   │   │
│  │  │  └──────────┘  └──────────┘  └──────────┘   │   │   │
│  │  └──────────────────────────────────────────────┘   │   │
│  │                                                      │   │
│  │  ┌──────────────────────────────────────────────┐   │   │
│  │  │         EOS App Store                        │   │   │
│  │  │  ┌──────────┐  ┌──────────┐  ┌──────────┐   │   │   │
│  │  │  │ App      │  │ Permis-  │  │ App      │   │   │   │
│  │  │  │ Registry │  │ sions    │  │ Runtime  │   │   │   │
│  │  │  └──────────┘  └──────────┘  └──────────┘   │   │   │
│  │  └──────────────────────────────────────────────┘   │   │
│  └──────────────────────────────────────────────────────┘   │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  Notification Relay                                   │   │
│  │  ┌──────────┐  ┌──────────┐                         │   │
│  │  │ iOS/     │  │ Format   │──> to glasses display    │   │
│  │  │ Android  │  │ & Filter │                         │   │
│  │  └──────────┘  └──────────┘                         │   │
│  └──────────────────────────────────────────────────────┘   │
└──────────────────────────────────────────────────────────────┘
```

---

### 2. Data Flow: Voice Query

```
User: "What's the stock price of Apple?"

  Step 1: Audio Capture
  ┌─────────┐     AAC/OPUS      ┌──────────────┐
  │ Glasses │ ────────────────> │ Phone App    │
  │ Mic     │   Bluetooth/WiFi  │ Audio Buffer │
  └─────────┘                   └──────┬───────┘
                                       │
  Step 2: Speech-to-Text              ▼
                               ┌──────────────┐
                               │ STT Engine   │
                               │ (Whisper /   │
                               │  on-device)  │
                               └──────┬───────┘
                                      │ "what is the stock
                                      │  price of Apple"
                                      ▼
  Step 3: AI Agent Processing  ┌──────────────┐
                               │ AI Agent     │
                               │ (LLM)        │
                               │              │
                               │ Detects:     │
                               │ Intent:      │
                               │  stock_query │
                               │ Entity:      │
                               │  AAPL        │
                               └──────┬───────┘
                                      │
  Step 4: Web Browser Agent          ▼
                               ┌──────────────┐
                               │ Headless     │
                               │ Browser      │
                               │              │
                               │ Visits:      │
                               │ finance.yahoo│
                               │ /quote/AAPL  │
                               └──────┬───────┘
                                      │
  Step 5: Content Extraction         ▼
                               ┌──────────────┐
                               │ Content      │
                               │ Extractor    │
                               │              │
                               │ Result:      │
                               │ "AAPL:       │
                               │  $187.68     │
                               │  (+1.24%)"  │
                               └──────┬───────┘
                                      │
  Step 6: Text to Glasses            ▼
                               ┌──────────────┐
                               │ Formatter    │
                               │              │
                               │ Output:      │
                               │ "Apple (AAPL)│
                               │  $187.68     │
                               │  +1.24% today│
                               └──────┬───────┘
                                      │
  Step 7: Display                    ▼
                               ┌──────────────┐
                               │ Glasses      │
                               │ Display      │
                               │ [Apple (AAPL)│
                               │  $187.68     │
                               │  +1.24%]     │
                               └──────────────┘
```

---

### 3. Communication Protocol

| Layer | Protocol | Purpose | Latency Target |
|-------|----------|---------|----------------|
| Audio Stream | Bluetooth A2DP / LE Audio | Mic audio from glasses → phone | <100ms |
| Text Output | Bluetooth SPP / Custom | Display text phone → glasses | <50ms |
| Commands | Bluetooth LE GATT | Gestures, controls, pairing | <20ms |
| Network | WiFi | Heavy web browsing (phone) | N/A |

---

### 4. AI Agent Stack

| Component | Technology | Notes |
|-----------|------------|-------|
| Speech-to-Text | Whisper (on-device) | Runs on phone, optimized for latency |
| LLM Agent | Llama 3 / Mistral / Phi (on-device) | Fine-tuned for search & browse tasks |
| Text-to-Speech | On-device TTS | Optional audio responses |
| Browser Engine | WebKit / Chromium headless (phone) | Full web rendering sans display |
| Content Extraction | Readability / Mozilla Readability | Strips ads, extracts main content |

---

### 5. Security Model

- **All AI processing stays on-device** — user queries never leave the phone
- **Web browsing is agent-mediated** — user doesn't browse directly, reducing phishing/XSS risk
- **Permission-based app access** — each mini app requests specific capabilities
- **Bluetooth pairing requires confirmation** — glasses paired via secure handshake
- **No cloud dependency** for core functionality — optional cloud for heavy compute

---

### 6. Battery & Performance Targets

| Metric | Target |
|--------|--------|
| Glasses battery life | 4+ hours active use |
| Phone battery drain | <15% per hour of active agent use |
| Query response time | <3 seconds (simple), <8 seconds (web search) |
| Display refresh | Smooth scrolling at 30fps text |
| STT latency | <500ms for 5-second utterance |