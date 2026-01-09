# The Void Archive

![License](https://img.shields.io/badge/license-MIT-blue) ![Platform](https://img.shields.io/badge/platform-Flutter-02569B) ![Riot API](https://img.shields.io/badge/Riot%20API-riftbound--content--v1-D32936)

> **The Void Archive** is not endorsed by Riot Games and doesn't reflect the views or opinions of Riot Games or anyone officially involved in producing or managing Riot Games properties. Riot Games, and all associated properties are trademarks or registered trademarks of Riot Games, Inc.

---

## Project Overview

**The Void Archive** is a free, open-source companion utility for physical *Riftbound* TCG play. It bridges the gap between printed cards and digital balance updates, streamlining tournament logistics for Local Game Stores (LGS) and competitive events.

**The Void Archive is a reference tool, NOT a game client.** It strictly adheres to Riot Games' developer policies by facilitating manual physical play rather than simulating gameplay.

### Core Features

#### 1. Oracle Lens (AR Overlay & Reference)
* **The Problem:** Physical cards become outdated when balance patches (errata) are released.
* **The Solution:** Uses camera-based AR (Augmented Reality) or manual search to identify a card's ID and fetch the **current official Oracle Text** directly from the Riot API.
* **Compliance Note:** This feature is a *Card Library*. It displays text and assets dynamically; it does not resolve game actions or track board state.

#### 2. Gatekeeper (Deck Validator & Logistics)
* **The Problem:** Manual deck checks at Regionals are slow and prone to human error.
* **The Solution:** A deck builder that validates lists against the live "Standard" or "Eternal" format restrictions (ban lists, region locks, set rotation). It generates a cryptographic QR code for Tournament Organizers to scan and verify legality instantly.
* **Compliance Note:** This feature facilitates *Event Logistics*. It does not include matchmaking, ladders, or ranking systems.

---

## Compliance Self-Assessment

This project has been designed from the ground up to respect Riot Games' ecosystem integrity.

| Riot Policy Requirement | Compliance Implementation |
| :--- | :--- |
| **No Gameplay Automation** | **PASS:** App is a static reference tool. It does not track health, mana, or resolve the stack. |
| **No Standalone Client** | **PASS:** Users cannot play a match of Riftbound within the app. |
| **No Skill Metrics** | **PASS:** App does not scrape or display player MMR, win rates, or meta tier lists. |
| **Asset Usage** | **PASS:** All card art and text is fetched dynamically from the `riftbound-content-v1` endpoint; no assets are bundled in the binary. |
| **Monetization** | **PASS:** Free to use. No paywalls for functionality. |

---

## Technical Architecture

### Stack
* **Framework:** Flutter 3.x (iOS / Android)
* **State Management:** Riverpod
* **Local Database:** Drift (SQLite) for offline caching
* **Networking:** Dio

### Riot API Integration
The app relies on the `riftbound-content-v1` namespace to ensure data is always in sync with the live game.

| Endpoint | Purpose | Data Accessed |
| :--- | :--- | :--- |
| `GET /riftbound/content/v1/cards/{set_id}` | **Oracle Lens:** Fetches current text, art, and "Unique" flags. | Card Name, Oracle Text, Image URLs |
| `GET /riftbound/v1/formats/standard/restrictions` | **Gatekeeper:** Fetches ban lists and set legality. | Banned IDs, Restricted Counts, Legal Sets |

**Data Handling:**
* **No Personal Data:** The app does not require an account for core functionality.
* **Caching:** Implements strict TTL (Time-To-Live) caching for API data to respect rate limits.
* **Token Security:** API keys are injected via build-time environment variables and are never exposed in the client source code.

---

## Roadmap

* **Phase 1: Foundation (Current)**
    * API Client integration & Caching logic.
    * Basic Card Search UI.
* **Phase 2: Gatekeeper**
    * Deck Builder UI.
    * Validation logic (Ban list/Rotation checks).
    * QR Export/Import.
* **Phase 3: Oracle Lens**
    * Camera integration for card ID recognition.
    * AR Text Overlay.

---

## Community & Contribution

This is a volunteer project built for the Riftbound community.

* **Repository:** [github.com/MANRAF04/void-archive](https://github.com/MANRAF04/void-archive)
* **Issues:** Bug reports and feature requests welcome via GitHub Issues.

**Creator:** Built by [@MANRAF04](https://github.com/MANRAF04) — a Riftbound player and software engineer passionate about making physical TCG play smoother.

---

## License

Distributed under the **MIT License**. See `LICENSE` for more information.

*Riftbound and all associated content are © Riot Games, Inc. This project uses the Riot Games API but is not endorsed by Riot Games.*
