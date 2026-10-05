id: build-nus-3d-digital-twin-antigravity
summary: Build a 3D NUS Campus Digital Twin and real-time shuttle bus tracker using OpenStreetMap and Spec-Driven Development in Google Antigravity.
categories: AI Agents, Web, Next.js, Geospatial, 3D, TypeScript
environments: Web
status: Published
feedback link: https://github.com/nusmodifications/nusmods
authors: Jarrett Yeo
keywords: docType:Codelab,category:AiAndMachineLearning,category:Web,product:Antigravity,product:GoogleCloud,product:Gemini,language:TypeScript,framework:Nextjs
layout: scrolling

# Build a 3D NUS Campus Digital Twin & Live Transit Tracker with Spec-Driven Development in Google Antigravity

![3D NUS Digital Twin Banner](images/digital-twin-map-3d.png)

## Overview & Objectives
Duration: 0:04:00

In this codelab, you will build a state-of-the-art **3D NUS Campus Digital Twin & Real-Time Transit Tracker** — an interactive geospatial command center combining:
1. **Interactive 3D Campus Canvas**: A high-performance WebGL digital twin rendered with **MapLibre GL JS** and **OpenStreetMap**, featuring dynamic 3D building extrusions, pitched camera controls, and smooth landmark fly-to transitions across Kent Ridge campus.
2. **Real-Time Campus Transit Tracking**: Live shuttle bus telemetry directly integrated with the official **NUS NextBus API**, delivering authentic stop coordinates, active vehicle telemetry, and live arrival countdowns (ETAs). Learn how real-world ETA-based tracking operates without fake simulations, handling scheduled operations and off-service status cleanly.
3. **3D Energy Pillars & Campus Energy Efficiency Analytics**: Vertical 3D extrusions rising from campus buildings with heights proportional to Energy Use Intensity (EUI), color-coded Green/Yellow/Red, paired with an interactive **Campus Energy Efficiency Bar Chart** that ranks campus facilities and flies the 3D camera to any selected building, alongside a detailed click-to-inspect Energy HUD pulling from the official **NUS Digital Twin API**.
4. **Cloud-Native Serverless Deployment**: Production deployment on **Vercel** with Next.js App Router serverless route handlers, secured API proxy caching, and worldwide edge CDN delivery.

---

### System Architecture & Data Pipeline
This diagram illustrates how your Next.js application ingests university telemetry, processes geospatial features, and renders the 3D twin:

```
                      ┌────────────────────────────────────────────────────────┐
                      │              University & Geospatial APIs              │
                      │  ┌────────────────────────┐  ┌───────────────────────┐ │
                      │  │ NUS NextBus API        │  │ NUS Digital Twin API  │ │
                      │  │  - Stop Coordinates    │  │  - Building Geometry  │ │
                      │  │  - Live Arrival ETAs   │  │  - Energy Intensity   │ │
                      │  │  - Active Telemetry    │  │  (Cooling, Power, Lux)│ │
                      │  │  - Off-Service Status  │  │                       │ │
                      │  └───────────┬────────────┘  └───────────┬───────────┘ │
                      └──────────────┼───────────────────────────┼─────────────┘
                                     │                           │
                                     ▼                           ▼
                      ┌────────────────────────────────────────────────────────┐
                      │          Next.js App Router Backend Handlers           │
                      │   • /api/transit/buses        • /api/buildings         │
                      │   • /api/transit/stops        • lib/digitaltwin.ts     │
                      │   • lib/nextbus.ts            • lib/types.ts           │
                      └────────────────────────────┬───────────────────────────┘
                                                   │
                                                   ▼
                      ┌────────────────────────────────────────────────────────┐
                      │       Interactive 3D Client (MapLibre GL + Three.js)   │
                      │  ┌─────────────────────────┐ ┌──────────────────────┐  │
                      │  │ 3D Building Extrusions  │ │ Revised 3D Buses     │  │
                      │  │ & 3D Energy Pillars     │ │ (Orange Roof #FF7200,│  │
                      │  │ - EUI-proportional      │ │  White Chassis, 2.5x,│  │
                      │  │   Green/Yellow/Red      │ │  Layered Above Route)│  │
                      │  └──────────┬──────────────┘ └──────────┬───────────┘  │
                      │             │                           │              │
                      │  ┌──────────▼──────────────┐ ┌──────────▼───────────┐  │
                      │  │ Energy Efficiency Chart │ │ Live Transit HUD     │  │
                      │  │ - Ranks by Efficiency   │ │ - Real-Time ETAs     │  │
                      │  │ - Click-to-Fly Camera   │ │ - Clean Off-Service  │  │
                      │  └─────────────────────────┘ └──────────────────────┘  │
                      └────────────────────────────────────────────────────────┘
```

---

### 🚀 The Antigravity Way: Spec-Driven Development (SDD)
Traditional coding workshops require hours of copying boilerplate code, hunting down mismatched TypeScript types, and resolving WebGL canvas context errors.

In this workshop, you will practice **Spec-Driven Development (SDD)** with **Google Antigravity**:
1. **Rule Anchoring (`.agents/rules/`)**: Lock down strict geospatial coordinate bounds, API schemas, MapLibre rendering conventions, and Three.js lifecycle rules.
2. **Implementation Planning (`/plan`)**: Instruct Antigravity to analyze your rules and generate an `implementation_plan.md` architectural blueprint, synthesizing the entire working application in one shot.
3. **Interactive Design Discovery (`/grill-me`)**: Interview Antigravity with specialized design skills to customize and elevate the command center UI to production-grade polish.

<aside class="positive">
<b>What You Will Learn:</b>
<ul>
  <li>How to configure Antigravity workspace rules (<code>.agents/rules/workspace.md</code>) to enforce geospatial, 3D graphics, and university API standards.</li>
  <li>How to use <b>Planning Mode (<code>/plan</code>)</b> to generate an entire production-grade full-stack 3D application from architectural specifications.</li>
  <li>How to consume the <b>NUS Digital Twin API</b> (<code>nus-digital-twin.com/api/v1/buildings</code>) for building footprints and energy intensity metrics.</li>
  <li>How to connect to the authenticated <b>NUS NextBus API</b> for real-time stop coordinates, active telemetry, and live arrival countdowns (ETAs) without fake simulations.</li>
  <li>How to render a 3D vector map with <b>MapLibre GL JS</b>, building extrusions, and vertical <b>3D Energy Pillars</b> color-coded Green/Yellow/Red by EUI.</li>
  <li>How to engineer a revised <b>3D Bus renderer</b> with Three.js proper layer ordering (bus above route lines), self-illuminating materials (vibrant orange roof <code>#FF7200</code>, white chassis, glowing headlights), and 2.5x Mercator scaling.</li>
  <li>How to use <b>Agent Skills</b> and <b>Interactive Discovery (<code>/grill-me</code>)</b> to interview Antigravity and dynamically restyle the command center UI.</li>
  <li>How to deploy the full-stack digital twin to <b>Vercel Serverless Edge</b>.</li>
</ul>
</aside>

---

## Environment Setup, Antigravity Rules & Scaffolding
Duration: 0:08:00

In this step, you will initialize the Next.js TypeScript project, install modern geospatial and 3D rendering packages, configure your university credentials, and anchor Antigravity with workspace rules.

### 1. Prerequisites Check
Ensure your development environment meets these requirements:
* **Node.js**: Version `18.17.0` or higher (`node -v`). Download from [nodejs.org](https://nodejs.org/).
* **Visual Studio Code** with the **Google Antigravity Extension** installed and authenticated.
* **Vercel Account**: A free Hobby account from [vercel.com/signup](https://vercel.com/signup) for Phase 5 (optional challenge).

### 2. Scaffold the Next.js TypeScript Project
1. Open **Visual Studio Code**.
2. Open the integrated terminal (`Terminal > New Terminal` or ``Ctrl+` `` / ``Cmd+` ``).

![Open New Terminal in VS Code](images/vscode-new-terminal.png)

3. Run the following commands to scaffold the project and install all required dependencies:

```bash
# 1. Scaffold Next.js App Router with TypeScript and Tailwind CSS
npx create-next-app@latest nus-digital-twin --typescript --tailwind --eslint --app --src-dir=false --import-alias="@/*" --use-npm --yes

# 2. Enter project directory
cd nus-digital-twin

# 3. Install geospatial, 3D math, icon, and utility dependencies
npm install maplibre-gl three @types/three lucide-react dotenv

# 4. Install dev-time TypeScript execution tools
npm install -D tsx @types/node
```

<aside class="positive">
<b>Key Libraries Explained:</b>
<ul>
  <li><b><code>maplibre-gl</code></b>: The open-source, community-led WebGL vector mapping engine fork of Mapbox GL. Delivers 60 FPS 3D map rendering, pitch, bearing, and native 3D <code>fill-extrusion</code> layers with zero proprietary license keys.</li>
  <li><b><code>three</code> & <code>@types/three</code></b>: High-performance JavaScript 3D engine used for custom 3D mesh rendering, lighting, materials, and Mercator coordinate transformations.</li>
  <li><b><code>lucide-react</code></b>: Crisp, accessible vector icons for the digital twin HUD and analytics charts.</li>
  <li><b><code>tsx</code></b>: TypeScript Execute — runs Node.js TypeScript scripts directly for instant verification without compiling.</li>
</ul>
</aside>

---

### 3. Create Environment Configuration (`.env.local`)
1. In the VS Code file explorer sidebar, right-click on the `nus-digital-twin` folder and select **New File**.
2. Name the new file `.env.local`.

3. Add the following university API configuration:

```env
# NUS NextBus API Basic Authentication (Public University Credentials)
NEXTBUS_BASE_URL="https://nnextbus.nus.edu.sg"
NEXTBUS_USERNAME="NUSnextbus"
NEXTBUS_PASSWORD='13dL?zY,3feWR^"T'

# NUS Digital Twin Public API Endpoint
NUS_DIGITAL_TWIN_API="https://www.nus-digital-twin.com/api/v1/buildings"
```

<aside class="negative">
<b>Security & Quotation Note:</b>
The NextBus password contains special characters (<code>^</code>, <code>"</code>, <code>?</code>). Always wrap it in single quotes (<code>'13dL?zY,3feWR^"T'</code>) in your <code>.env.local</code> to prevent shell expansion errors.
</aside>

---

### 4. Establish Antigravity Rules (`.agents/rules/workspace.md`)
Antigravity uses workspace rules inside `.agents/rules/` to ground its code generator on project-specific architectural decisions, preventing hallucinated packages or conflicting GIS conventions.

1. In your VS Code terminal, create the rules directory:
```bash
mkdir -p .agents/rules
```

2. Create `.agents/rules/workspace.md` and insert the following rules:

```markdown
# NUS 3D Digital Twin & Transit Tracker Rules

## Technology Stack & Architectural Conventions
- Framework: Next.js 14/15 App Router with TypeScript and Tailwind CSS.
- Map Engine: MapLibre GL JS (`maplibre-gl`). Always import `maplibre-gl/dist/maplibre-gl.css`.
- 3D Rendering: Three.js (`three`) for custom 3D vehicle models, lighting, and spatial calculations.
- Client-Side Rendering: MapLibre GL uses browser `window` and `WebGLRenderingContext`. Always wrap map components in Next.js dynamic client import (`dynamic(() => import(...), { ssr: false })`) or `'use client'`.

## Geospatial Anchors & NUS Campus Coordinates
- Kent Ridge Campus Center: `[103.7745, 1.2970]` (Longitude, Latitude).
- Campus Bounding Box: `[103.7650, 1.2900, 103.7850, 1.3100]`.
- Default Camera: Pitch `60`, Bearing `-20`, Zoom `16.2`.
- Key Landmark Coordinates:
  - University Town (UTown): `[103.7738, 1.3040]`, Pitch: 60, Bearing: 45
  - School of Computing (COM3): `[103.7745, 1.2944]`, Pitch: 65, Bearing: -30
  - Central Library (CLB): `[103.7725, 1.2966]`, Pitch: 55, Bearing: 10
  - Kent Ridge MRT Station: `[103.7844, 1.2932]`, Pitch: 60, Bearing: -60

## API Contracts & Data Integration
1. NUS Digital Twin API: `https://www.nus-digital-twin.com/api/v1/buildings`
   - Attributes: `elementId`, `name`, `address`, `postal`, `latitude`, `longitude`, `height`, `floorCount`, `category`.
   - Energy Use Intensity (EUI) Schema: Annual total and monthly breakdown in kWh/m² (`cooling` ~55%, `equipment` ~30%, `lighting` ~15%).
2. NUS NextBus API: `https://nnextbus.nus.edu.sg/`
   - Basic Auth: `NEXTBUS_USERNAME` and `NEXTBUS_PASSWORD`.
   - Endpoints: `/BusStops`, `/ShuttleService?busstopname=<STOP>`.
   - Authentic Telemetry & ETA Tracking: Deduplicate oncoming vehicles across key interchange stops (`UTOWN`, `KR-MRT`, `COM3`, `CLB`, `LT27`, `BIZ2`), projecting coordinates along canonical route shapes (A1, A2, D1, D2).
   - Off-Service Handling: Outside operating hours (07:00–23:00 SGT), set `isOffService: true` and display scheduled operating resumption notices. Do not run synthetic fake wandering simulations.

## 3D Rendering & WebGL Conventions
- 3D Building Extrusions (`campus-3d-buildings`): Extruded physical footprints based on building height (18m–48m), colored by category (#38bdf8 academic, #c084fc residential, #34d399 recreation, #fbbf24 admin).
- 3D Energy Pillars (`campus-energy-pillars`): Concentrated 14m x 14m core polygons rising vertically from building rooftops (`fill-extrusion-base = height`, `fill-extrusion-height = height + (eui * 0.75)`). Color dynamically using MapLibre `step` expression:
  - Efficient (< 160 kWh/m²): Green `#10B981`
  - Moderate (160–200 kWh/m²): Yellow `#F59E0B`
  - Energy Intensive (> 200 kWh/m²): Red `#EF4444`
- Revised 3D Bus Renderer (`nus-shuttle-bus-3d`): Three.js custom layer registered strictly *after* route polylines (layer ordering: roads -> routes -> 3D buses). Self-illuminating materials (vibrant orange roof `#FF7200`, crisp white chassis, warm white glowing headlights, taillights, rubber wheels) with 2.5x Mercator scaling (`meterInMercatorCoordinateUnits() * 2.5`).
- Campus Energy Efficiency Bar Chart: Sorts and displays buildings ranked by efficiency (lowest EUI = rank #1) with click-to-fly 3D camera navigation.
- Building Energy Inspector HUD: Floating glassmorphic sheet showing 12-month energy profiles when a building or pillar is clicked.
```

---

### 🧪 Verification
Run these commands in your VS Code terminal to verify your setup:

```bash
# Verify environment configuration and rules
head -n 5 .env.local
ls -la .agents/rules/workspace.md
```

**Expected Terminal Output:**
```text
NEXTBUS_BASE_URL="https://nnextbus.nus.edu.sg"
NEXTBUS_USERNAME="NUSnextbus"
NEXTBUS_PASSWORD='13dL?zY,3feWR^"T'
NUS_DIGITAL_TWIN_API="https://www.nus-digital-twin.com/api/v1/buildings"
-rw-r--r--  1 student  staff  2980 Oct  5 14:00 .agents/rules/workspace.md
```

---

## Phase 1: Architecture Blueprint & Planning Mode with `/plan`
Duration: 0:10:00

Before generating code, professional developers review an implementation plan to verify architecture, module boundaries, and interfaces.

In Antigravity, **Planning Mode** (`/plan`) reads your project context and `.agents/rules/workspace.md` to generate a structured `implementation_plan.md` artifact detailing every file, API wrapper, 3D layer, and verification test before executing any changes.

### 🤖 The Agentic Prompt (Antigravity)
Open the **Antigravity Chat Panel** and enter the following prompt:

```text
/plan Generate a comprehensive implementation plan to build the NUS 3D Campus Digital Twin & Live Transit Tracker according to our .agents/rules/workspace.md.
Detail the file creations and verification steps for:
1. `lib/types.ts`: TypeScript definitions for `BuildingEnergy`, `CampusBuilding`, `ShuttleEta`, `BusStop`, `ActiveBus`, `CampusRoute`, and `TransitState`.
2. `lib/digitaltwin.ts`: API wrapper fetching building footprints from NUS Digital Twin API, calculating procedural 3D heights (18m-48m), and generating 12-month EUI profiles (cooling 55%, equipment 30%, lighting 15%) with landmark fallbacks (COM3, UTown, CLB, S17).
3. `lib/nextbus.ts`: Authenticated API wrapper for NUS NextBus querying /BusStops and /ShuttleService, projecting active buses along canonical routes (A1, A2, D1, D2), and handling off-service hours (23:00-07:00 SGT) cleanly without synthetic simulations.
4. `app/api/buildings/route.ts`: Next.js App Router REST API endpoint serving building footprints and EUI metrics (revalidate = 3600).
5. `app/api/transit/buses/route.ts` & `app/api/transit/stops/route.ts`: Endpoints for live shuttle telemetry (cache: no-store) and campus stop polylines.
6. `components/MapCanvas.tsx`: High-performance client component initializing MapLibre GL with dark OSM tiles, pitched camera controls, 3D building extrusions, and vertical 3D Energy Pillars (Green/Yellow/Red by EUI).
7. `lib/threeBusLayer.ts`: Three.js custom layer rendering 3D shuttle buses with vibrant orange roof (#FF7200), white chassis, glowing headlights, 2.5x scale factor, and proper layer ordering above routes.
8. `components/BusTracker.tsx`: Live telemetry overlay auto-polling every 5 seconds with countdown timer and off-service badge.
9. `components/CampusEnergyChart.tsx`: Ranked campus energy efficiency bar chart with click-to-fly 3D camera navigation.
10. `components/BuildingEnergyModal.tsx`: Building inspector side sheet displaying 12-month energy breakdown bars.
11. `app/page.tsx`: Dynamic client assembly with top telemetry HUD.
```
### Reviewing & Executing the Implementation Plan
Antigravity will create the `implementation_plan.md` artifact detailing each component's inputs, outputs, error handling strategies, and verification commands.

1. In the Antigravity chat, click on **Implementation Plan** to open the plan viewer in your editor. Review the planned files and architecture.
2. When satisfied, click **Proceed** in the top right of the plan viewer tab.

![Review Implementation Plan and Click Proceed](images/agy-plan-proceed.png)

> 💡 **UI Guide**: In the implementation plan editor tab, click the **Proceed** button in the top right corner to start autonomous code generation.

3. Antigravity will autonomously generate all the project files according to the approved plan. In the following phases, we will inspect, test, and verify each layer of the application.
4. Once Antigravity finishes generating the files, click **Accept all** on the review bar to accept all changes into your workspace.

![Click Accept All](images/accept-all.png)

---

## Phase 2: Inspect Campus 3D & Telemetry Architecture
Duration: 0:08:00

In this phase, we inspect the core architectural layers generated by Antigravity and understand how 3D WebGL meshes, university telemetry, and geospatial projections interconnect.

### 🔍 Generated Files Overview
Take a few moments to open and explore each file in VS Code to see how Antigravity structured the codebase:

* **`lib/types.ts`**: Defines strict TypeScript interfaces for building footprints (`CampusBuilding`), 12-month energy profiles (`BuildingEnergy`), shuttle telemetry (`ActiveBus`), bus stops (`BusStop`), and aggregated transit states (`TransitState`).
* **`lib/digitaltwin.ts`**: Fetches building geometries from `https://www.nus-digital-twin.com/api/v1/buildings`, augmenting each record with procedural 3D heights (18m–48m) and tropical EUI breakdowns (cooling ~55%, equipment ~30%, lighting ~15%).
* **`lib/nextbus.ts`**: Handles authenticated Basic Auth calls to the NUS NextBus API. It queries `/BusStops` and `/ShuttleService`, projects vehicles along canonical campus routes (A1, A2, D1, D2), and handles off-service hours (23:00–07:00 SGT) cleanly without fake wandering simulations.
* **`lib/threeBusLayer.ts`**: Implements a MapLibre `CustomLayerInterface` named `nus-shuttle-bus-3d`. It uses Three.js to render 3D shuttle bus models with self-illuminating materials (vibrant orange roof `#FF7200`, white chassis, glowing LED headlights) and scales them by `2.5x` in Mercator space so they are unmistakably visible across campus roads.
* **`components/MapCanvas.tsx`**: Renders the 3D MapLibre canvas with dark Carto/OSM raster tiles and two synchronized `fill-extrusion` layers:
  1. `campus-3d-buildings`: Base physical footprints extruded to real building heights.
  2. `campus-energy-pillars`: 14m x 14m core rooftop pillars rising proportionally to EUI (`height + eui * 0.75`), styled dynamically with MapLibre's `step` expression (Green `<160`, Yellow `160-200`, Red `>200`).

> 💡 **Poke Around**: Open `lib/threeBusLayer.ts` in VS Code. Look at how `coord.meterInMercatorCoordinateUnits() * 2.5` scales the Three.js mesh and how `map.triggerRepaint()` drives the WebGL render loop!

---

## Phase 3: Launch & Test the 3D Digital Twin
Duration: 0:12:00

Now let's launch our local Next.js development server and interact with our live 3D campus twin.

### 1. Static Type Check
Run static TypeScript validation in your terminal:
```bash
npx tsc --noEmit
```

### 2. Start the Development Server
In your terminal, start the Next.js dev server:
```bash
npm run dev
```

### 3. Explore the Digital Twin in Your Browser
Open `http://localhost:3000` in Google Chrome:

1. **3D Camera & Landmark Navigation**:
   * Observe the dark-mode OpenStreetMap canvas tilted at a 60-degree pitch with smooth 3D perspective.
   * Click the quick navigation buttons in the top-left toolbar (**University Town**, **Computing (COM3)**, **Central Library**, **Kent Ridge MRT**) to experience smooth fly-to camera transitions.
2. **Vertical 3D Energy Pillars**:
   * Look across campus rooftops at the vertical 3D Energy Pillars shooting into the sky:
     * **Stephen Riady Centre (UTown)**: Emerald green pillar (efficient 148 kWh/m²).
     * **Central Library (CLB)**: Amber yellow pillar (moderate 172 kWh/m²).
     * **School of Computing (COM3)**: Towering red pillar (energy-intensive 215 kWh/m²).
3. **Live NextBus Telemetry HUD**:
   * Look at the top-right telemetry pill. Notice the 5-second countdown timer polling `/api/transit/buses`.
   * During daytime operations, active shuttle buses glide along routes with correct headings.
   * During late-night hours (23:00–07:00 SGT), notice the sleek `Services Off-Peak (07:00 Resumption)` badge.
4. **Interactive Campus Energy Efficiency Ranking Bar Chart**:
   * Look at the bottom-right analytics card ranking facilities from most efficient (#1) to least efficient.
   * **Click any building bar** (e.g. Stephen Riady Centre or COM3):
     1. The camera glides across campus and centers on that building with high pitch (65°) and zoom (17.2).
     2. The **Building Energy Inspector** sheet slides into view with detailed cooling, equipment, and lighting distributions and a 12-month consumption trend!

---

## Phase 4: Supercharge Your Agent with Skills & `/grill-me` Design Interview
Duration: 0:12:00

Now that your functional 3D digital twin is running, let's elevate its visual presentation and command center aesthetics from a functional demo to an award-winning geospatial dashboard.

In this phase, you will learn two advanced Antigravity capabilities:
1. **Agent Skills**: Extending Antigravity's capabilities with specialized design system skills.
2. **Interactive Design Discovery (`/grill-me`)**: Letting Antigravity interview you to capture your creative intent before touching code.

### 1. What Are Agent Skills?
In modern agentic AI, **Skills** are modular packages containing specialized instructions, industry heuristics, and design guidelines that extend your agent's problem-solving toolkit. 

Antigravity automatically discovers and loads skills located in your project's `.agents/skills/` directory.

### 2. Install the Frontend Taste Skill
We will install [`taste-skill`](https://github.com/Leonxlnx/taste-skill) — an open-source collection of design intelligence skills (Minimalist UI, High-End Visual Design, Industrial Brutalism, and Brand Kit).

In your VS Code terminal, run:

```bash
npx skills add Leonxlnx/taste-skill -y
```

> **Why `-y`?**: The `-y` flag skips interactive prompts and automatically selects all design skills for Antigravity, copying them directly into `.agents/skills/`.

---

### 3. Trigger the Interactive Design Interview (`/grill-me`)
Instead of trying to write a 500-word prompt detailing exact hex codes and CSS animations, use Antigravity's built-in `/grill-me` slash command. This instructs the agent to ask *you* clarifying questions to uncover your preferred visual aesthetic.

Open the **Antigravity Chat Panel** and prompt:

```text
/grill-me I want to redesign our NUS 3D Campus Digital Twin command center (`app/page.tsx`, `components/MapCanvas.tsx`, and `components/CampusEnergyChart.tsx`) using our newly installed taste skills. 
Grill me with questions about my preferred visual aesthetics (e.g., Cyberpunk Neon, Minimalist Dark Architecture, or High-Contrast Tactical Command Center), HUD density, 3D energy pillar color palettes, camera animation speed, and telemetry badge styling before making any code edits.
```
### 4. Answer Antigravity's Questions & Apply the Redesign
1. Antigravity will interview you with interactive multiple-choice questions directly in the chat panel (e.g. Visual Theme, Glassmorphism HUD density, Energy Pillar color ramp, Landmark button styling).
2. Select your preferred options (or type custom specifications into the write-in box), then click **Continue**.

![Interactive Design Questions in Antigravity](images/agy-grillme-questions.png)

> 💡 **UI Guide**: Antigravity presents interactive multiple-choice cards directly in the chat panel to resolve creative and architectural decisions before writing code.

3. Antigravity will synthesize your preferences into an updated implementation plan. Click **Proceed**.
4. Antigravity will refactor `app/page.tsx`, `components/MapCanvas.tsx`, and `components/CampusEnergyChart.tsx` according to your aesthetic choices. Click **Accept all** when prompted.

![Accept All Design Changes](images/accept-all.png)

5. Return to `http://localhost:3000` to witness your custom-tailored digital twin command center!

---

## Phase 5 (Optional Challenge): One-Click Deploy to Vercel
Duration: 0:05:00

Now that your 3D digital twin is running locally, your challenge is to transition your system to production by deploying to **Vercel Serverless Edge**.

### 1. What is Vercel?
**Vercel** is the native cloud deployment platform created by the authors of Next.js.
* **Serverless Next.js App Router**: API routes defined in `app/api/...` run as serverless micro-functions with zero VM management.
* **Instant Global Edge Routing**: Every deployment receives a free production URL (e.g., `https://nus-digital-twin.vercel.app`) with automatic SSL and CDN caching.

### 2. Deploying via Vercel CLI
1. Log in to Vercel in your VS Code terminal:
   ```bash
   npx vercel login
   ```
   *(Authorize the CLI in your browser when prompted).*

2. Deploy the application to production:
   ```bash
   npx vercel --prod
   ```
   *(Press Enter to accept standard defaults).*

3. Configure Environment Variables in the Vercel Dashboard:
   * Go to [vercel.com/dashboard](https://vercel.com/dashboard) and open your `nus-digital-twin` project.
   * Navigate to **Settings > Environment Variables**.
   * Add each variable with the target environment set to `Production`:

| Variable Key | Type | Production Value |
| :--- | :--- | :--- |
| `NEXTBUS_BASE_URL` | Plaintext | `https://nnextbus.nus.edu.sg` |
| `NEXTBUS_USERNAME` | Plaintext | `NUSnextbus` |
| `NEXTBUS_PASSWORD` | Secret | `13dL?zY,3feWR^"T` |
| `NUS_DIGITAL_TWIN_API` | Plaintext | `https://www.nus-digital-twin.com/api/v1/buildings` |

4. Redeploy to apply the environment variables:
   * In your Vercel project dashboard, navigate to the **Deployments** tab, click the three-dots menu (`...`) on your latest deployment, and select **Redeploy**.
   * Alternatively, trigger a redeployment from your terminal:
   ```bash
   npx vercel --prod --yes
   ```

5. Open your live Vercel production URL on your laptop or smartphone!

---

## Summary & Antigravity Slash Commands Reference
Duration: 0:03:00

Congratulations! You have designed, planned, verified, and deployed a **3D NUS Campus Digital Twin & Live Transit Tracker** using **Spec-Driven Development** in **Google Antigravity**.

### What You Built:
* **Spec-Driven Development (SDD)**: Anchored architectural standards, geospatial coordinates, and API contracts in `.agents/rules/workspace.md`.
* **Planning Mode (`/plan`)**: Built an entire full-stack 3D digital twin from specifications in a single agentic plan.
* **Interactive Design Discovery (`/grill-me`)**: Installed `taste-skill` and conducted an interactive design interview to tailor the visual aesthetic of your command center.
* **3D OpenStreetMap Engine**: Rendered vector tiles, dynamic camera pitch and bearing controls, and physical 3D building extrusions with **MapLibre GL JS**.
* **3D Energy Pillars**: Visualized campus energy intensity with vertical 3D extrusions rising from building rooftops, color-coded Green/Yellow/Red.
* **Revised 3D Shuttle Bus Renderer**: Implemented Three.js 3D buses rendered strictly above route polylines, utilizing self-illuminating materials and a 2.5x scale factor.
* **Interactive Campus Energy Efficiency Bar Chart**: Ranked campus facilities by energy performance with interactive click-to-fly camera transitions.

---

### Antigravity Slash Commands Cheat Sheet
Antigravity provides built-in slash commands in the chat panel to supercharge developer workflows:

| Slash Command | Purpose | When to Use |
| :--- | :--- | :--- |
| **`/plan`** | **Architecture Blueprinting** | Complex tasks requiring step-by-step architectural review and approval before writing code. |
| **`/grill-me`** | **Interactive Interview** | Exploring design decisions, UX preferences, and ambiguous requirements before implementation. |
| **`/browser`** | **Web Automation & QA** | Inspecting live localhost apps, taking screenshots, and verifying visual rendering. |
| **`/schedule`** | **Timers & Recurring Jobs** | Setting background polling, heartbeat timers, or scheduled task notifications. |
| **`/goal`** | **Autonomous Goal Execution** | Extra-thorough, long-running agentic tasks that shouldn't stop until complete. |
| **`/learn`** | **Knowledge Persistence** | Teaching the agent project-specific rules, domain quirks, or setup instructions for future tasks. |

---

### What's Next?
* **Solar PV Potential**: Add rooftop solar irradiance estimation to the building inspector using Singapore BCA solar data.
* **Pedestrian Walkways**: Ingest sheltered walkway graphs from OpenStreetMap to provide rain-free campus routing.
* **IoT Sensor Feeds**: Connect live indoor temperature and occupancy sensors to individual floors in COM3 and UTown!
