# 7ports

Building AI-native developer tooling — infrastructure, agents, and games at the frontier of human-AI collaboration.

---

## Projects

### [Project Voltron](https://github.com/7ports/project-voltron)

**MCP server providing specialized agent teams for Claude Code**

Scaffold any project with battle-tested subagent definitions. Voltron gives Claude Code a coordinated team of specialists — a scrum-master that decomposes work, a project-planner that designs architecture, and domain experts that implement it. Specialist agents run in Docker containers for blast-radius isolation. Agents self-improve through post-session reflections: a GitHub Actions workflow (Mon/Wed/Fri at 10:00 UTC) reads accumulated feedback and patches templates automatically, opening PRs for human review before anything reaches `main`.

**Agent Teams:**
- **Core (all projects):** scrum-master · project-planner
- **Unity:** scene-architect · csharp-dev · shader-artist · build-validator · asset-manager
- **Web / Fullstack:** fullstack-dev · devops-engineer · ui-designer · qa-tester

**MCP Tools:** `scaffold_project` · `run_agent_in_docker` · `submit_reflection` · `update_progress` · `get_progress` · `generate_dashboard` · `check_for_updates` · `list_templates` · `get_template`

**Integrates with [Project Alexandria](#project-alexandria) — agents consult the shared knowledge base before any tool installation.**

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)](https://github.com/7ports/project-voltron)
[![MCP SDK](https://img.shields.io/badge/MCP_SDK-Claude_Code-7c3aed?style=flat)](https://github.com/7ports/project-voltron)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)](https://github.com/7ports/project-voltron)
[![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=github-actions&logoColor=white)](https://github.com/7ports/project-voltron)

[**GitHub →**](https://github.com/7ports/project-voltron) &nbsp;|&nbsp; [**Docs →**](https://7ports.github.io/project-voltron/) &nbsp;|&nbsp; `v2.3.8`

---

### [Project Alexandria](https://github.com/7ports/project-alexandria)

**Collaboratively maintained knowledge base shared across Claude instances via MCP**

Every Claude instance with Alexandria installed becomes both a consumer and a contributor. Before installing any tool, agents call `quick_setup` — this is mandatory, not optional. After setup, agents call `update_guide` to document what they learned: platform quirks, version notes, working commands, error/fix pairs. Tool knowledge accumulates across projects and sessions instead of being rediscovered from scratch every time.

Strictly for non-project-specific, reusable knowledge. Project-specific decisions belong in `CLAUDE.md`.

**Available Guides:**
CoPlay (Unity) · Git · GitHub · GitHub CLI · Memory MCP · Firebase · AWS CLI · Fetch MCP · Claude in Chrome · Claude Preview · Beads · Alexandria MCP · Claude Code GitHub Actions

**MCP Tools:** `quick_setup` · `search_guides` · `read_guide` · `update_guide` · `list_guides` · `get_project_setup_recommendations` · `get_onboarding` · `get_guide_template`

[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)](https://github.com/7ports/project-alexandria)
[![MCP SDK](https://img.shields.io/badge/MCP_SDK-Claude_Code-7c3aed?style=flat)](https://github.com/7ports/project-alexandria)
[![Markdown](https://img.shields.io/badge/Markdown-000000?style=flat&logo=markdown&logoColor=white)](https://github.com/7ports/project-alexandria)

[**GitHub →**](https://github.com/7ports/project-alexandria) &nbsp;|&nbsp; [**Docs →**](https://7ports.github.io/project-alexandria/)

---

### [Project Pepper](https://github.com/7ports/project-pepper)

**2D strategic card game — Unity 6 · WebGL**

A hand-of-cards variant on 4×4 Tic-Tac-Toe with AI opponents across Easy, Medium, and Hard difficulties. Built in Unity 6 with the Universal Render Pipeline and deployed as a WebGL build. Cards are ScriptableObjects — each with unique effects applied to the 4×4 grid. Firebase Analytics tracks gameplay events via a custom JavaScript bridge (Unity jslib → browser Firebase JS SDK), guarded with `#if UNITY_WEBGL && !UNITY_EDITOR` throughout.

**Key Details:**
- 4×4 grid variant with hand-based card mechanic — cards alter board state in unique ways
- Three AI difficulty levels with distinct strategies
- Firebase Analytics via `FirebaseWebGL.cs` → `FirebaseAnalytics.jslib` → `window.analytics` bridge
- URP renderer with custom sprite materials; TextMesh Pro for all UI text
- Fully managed by Voltron agent team: scrum-master · csharp-dev · scene-architect · shader-artist · build-validator · asset-manager

[![Unity](https://img.shields.io/badge/Unity_6-000000?style=flat&logo=unity&logoColor=white)](https://github.com/7ports/project-pepper)
[![C#](https://img.shields.io/badge/C%23-239120?style=flat&logo=c-sharp&logoColor=white)](https://github.com/7ports/project-pepper)
[![WebGL](https://img.shields.io/badge/WebGL-990000?style=flat)](https://github.com/7ports/project-pepper)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat&logo=firebase&logoColor=black)](https://github.com/7ports/project-pepper)
[![URP](https://img.shields.io/badge/URP-000000?style=flat&logo=unity&logoColor=white)](https://github.com/7ports/project-pepper)

[**GitHub →**](https://github.com/7ports/project-pepper) &nbsp;|&nbsp; [**Play on itch.io →**](https://sevenports.itch.io/x-o) &nbsp;|&nbsp; `Alpha`

---

### [Project Hammer](https://github.com/7ports/project-hammer)

**Real-time Toronto Island Ferry tracker — React PWA · AIS · Fly.io**

Streams live AIS vessel positions from aisstream.io through a Node.js proxy on Fly.io and renders them on a MapLibre GL map with 60fps smooth interpolation via `lerp()` + `requestAnimationFrame`. The React PWA shows live vessel cards with MMSI tracking, schedule lookup, weather strip, dock markers, and wake trails. The backend proxies the aisstream.io WebSocket (which blocks direct browser connections) and relays position updates as SSE — so `EventSource` auto-reconnects with no WebSocket library on the client.

**Tracked Vessels:** Sam McBride (316045069) · Wm Inglis (316045081) · Thomas Rennie (316045082) · Marilyn Bell I (316050853)

**Key Details:**
- SSE relay over WebSocket — unidirectional AIS data fits EventSource perfectly; auto-reconnect built in
- 60fps vessel movement with position interpolation between ~10s AIS ping intervals
- MapLibre GL JS v5 + react-map-gl v8 + MapTiler Ocean chart style — open source, no proprietary lock-in
- Full production infra: Terraform (S3 + CloudFront + ACM + Route53) · Fly.io (yyz region) · GitHub Actions CI/CD
- PWA with service worker, installable offline-capable app

[![React](https://img.shields.io/badge/React_18-61DAFB?style=flat&logo=react&logoColor=black)](https://github.com/7ports/project-hammer)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://github.com/7ports/project-hammer)
[![MapLibre](https://img.shields.io/badge/MapLibre_GL_JS-396CB2?style=flat)](https://github.com/7ports/project-hammer)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)](https://github.com/7ports/project-hammer)
[![Fly.io](https://img.shields.io/badge/Fly.io-8B5CF6?style=flat)](https://github.com/7ports/project-hammer)
[![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat&logo=amazon-aws&logoColor=white)](https://github.com/7ports/project-hammer)
[![Terraform](https://img.shields.io/badge/Terraform-623CE4?style=flat&logo=terraform&logoColor=white)](https://github.com/7ports/project-hammer)

[**GitHub →**](https://github.com/7ports/project-hammer) &nbsp;|&nbsp; [**Live →**](https://ferries.yyz.live) &nbsp;|&nbsp; `Prototype`

---

## Tech Stack

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Unity](https://img.shields.io/badge/Unity_6-000000?style=flat-square&logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat-square&logo=c-sharp&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=github-actions&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-FF9900?style=flat-square&logo=amazon-aws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-623CE4?style=flat-square&logo=terraform&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black)
![Fly.io](https://img.shields.io/badge/Fly.io-8B5CF6?style=flat-square)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![MapLibre](https://img.shields.io/badge/MapLibre_GL-396CB2?style=flat-square)
![Cloudflare](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat-square&logo=cloudflare&logoColor=white)
