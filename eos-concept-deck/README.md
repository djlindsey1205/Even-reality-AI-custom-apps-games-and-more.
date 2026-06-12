# 🥽 EOS — Everything On Sight

**An AI-Native OS for Even Reality G2 Smart Glasses**

---

## 📋 Project Overview

This concept deck defines **EOS** (Everything On Sight), a lightweight operating system concept for Even Reality G2 smart glasses. The core idea: your **phone acts as a compute tether**, your **glasses are the display**, and an **AI agent browses the web** to answer your questions — delivering results as simple text in your field of view.

## 📁 Files

| File | Description |
|------|-------------|
| [`CONCEPT_DECK.md`](./CONCEPT_DECK.md) | 🎯 Vision, features, and high-level overview |
| [`ARCHITECTURE.md`](./ARCHITECTURE.md) | 🏗️ System architecture, data flow, security model |
| [`UX_FLOW.md`](./UX_FLOW.md) | 🎨 User journeys, interactions, display guidelines |
| [`APP_STORE_SPEC.md`](./APP_STORE_SPEC.md) | 📦 Third-party app model, manifest format, developer docs |

## 🎯 Key Concept

```
User speaks ──> Glasses mic ──> Phone app (AI Agent) ──> Web Search
                                                              │
User sees   <── Glasses display <── Formatted text <─────────┘
```

- **Phone does the heavy lifting** — AI, browsing, processing
- **Glasses are the display** — simple text overlay in your field of view
- **Agent is the browser** — no visual browser needed, the agent browses for you
- **Any website = potential app** — third-party apps are just prompts + URLs

## 🚀 Next Steps

1. Prototype phone app (AI agent + headless browser pipeline)
2. Prototype glasses display layer (text rendering)
3. Build the "Ask" flow end-to-end
4. Define app manifest format
5. Create Developer SDK documentation