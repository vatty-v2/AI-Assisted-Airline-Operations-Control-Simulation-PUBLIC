# ◈ AI-Assisted Airline Operations Control Simulation

> **An interactive OCC simulation with a live flight board, disruption injection engine, and Claude-powered decision support — running entirely in the browser.**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![Claude API](https://img.shields.io/badge/Claude-Sonnet_4-D97706?style=flat&logo=anthropic&logoColor=white)](https://anthropic.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()

---

## What is this?

This project simulates an **Airline Operations Control Centre (OCC)**. The nerve centre where controllers manage aircraft, crew, and schedules in real time when disruptions occur.

It models a live network of 15 flights across 6 aircraft, with a time-accelerated simulation engine. When a disruption is injected (weather, mechanical fault, ATC restriction, etc.), a **Large Language Model decision support layer** analyses the situation and returns structured recovery options. Just as a real AI co-pilot tool would in an operational OCC.

**Built to explore:** how LLM-generated operational advice performs under realistic airline scheduling constraints, and how structured outputs can support time-critical decision-making.

---

## Development Note

This project was originally developed in a private repository and later published here as a public portfolio project. The commit history has been condensed as part of that transition.

---

## Features

- **Live Flight Progress Board** - 15 flights advancing through `SCH → BRD → DEP → ARR` states in simulated time (1×, 30×, 120×, 300× speed)
- **Aircraft Allocation Tracker** - 6 aircraft (A320/B738/A321) with real-time position, utilisation bars, and AOG detection
- **Disruption Injection Engine** - 7 disruption types × 3 severities (21 scenarios), each with realistic delay ranges that cascade across the network
- **Claude-Powered Decision Support** - sends full flight/fleet/network context to Claude Sonnet 4 and renders structured recovery options with delay impact scores and passenger impact ratings
- **Network Performance Metrics** - live OTP %, total delay minutes, and IROPS count in the header
- **Zero dependencies** - single self-contained HTML file, no build step, no server

---

## Tech Stack

| Layer | Technology |
|---|---|
| Simulation Engine | Vanilla JavaScript (ES6+) |
| UI / Styling | Pure CSS with CSS variables |
| LLM Integration | Anthropic Claude API (`claude-sonnet-4`) |
| Font | JetBrains Mono + IBM Plex Sans |
| Deployment | Single HTML file - open in any browser |

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/vatty-v2/AI-Assisted-Airline-Operations-Control-Simulation-PUBLIC.git
cd AI-Assisted-Airline-Operations-Control-Simulation-PUBLIC
```

### 2. Open the simulation

No build step required. Simply open the file in your browser:

```bash
open occ_simulation.html        # macOS
start occ_simulation.html       # Windows
xdg-open occ_simulation.html    # Linux
```

### 3. Add your Anthropic API key

On first load, a key prompt appears in the bottom-right corner. Enter your `sk-ant-api03-...` key.It is stored in `localStorage` and sent **only** to `api.anthropic.com`.

Get a key at [console.anthropic.com](https://console.anthropic.com) → API Keys.

> The key badge in the top-right header shows `⚿ KEY SET` (green) once saved. Click it anytime to update.

---

## Usage

### Running a disruption scenario

1. Click **`+ DISRUPTION`** in the top-right of the flight board
2. Select a disruption type, severity, and affected airport
3. Optionally add context notes (e.g. *"Runway 08L closed due to FOD"*)
4. Click **Inject Disruption** - delays cascade across all flights at that airport

### Triggering AI analysis

1. In the **Active Disruptions** panel, click **`◈ Analyse with AI`**
2. The full operational context is sent to Claude Sonnet 4:
   - Disruption metadata (type, severity, description)
   - Affected flight details (route, STD, current delay, status)
   - Fleet status (registration, type, position, AOG flag)
   - Network-level KPIs (total delay minutes, cancellations, diversions)
3. The AI returns a structured response rendered as:
   - **Immediate Actions** (0–15 min)
   - **Three Recovery Options** with delay impact and passenger impact scores
   - **Recommended option** with justification
   - **KPIs to monitor**

### Simulation speed

Use the **Sim speed** dropdown (top-right) to advance time:
- `1×` - real-time observation
- `120×` - default, one hour of ops per 30 seconds
- `300×` - full day scenario in ~3 minutes

---

## License

MIT — see [LICENSE](LICENSE) for details

---

*Not affiliated with any airline or OCC operator.*
