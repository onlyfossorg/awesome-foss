# LanView CLI

[![npm version](https://img.shields.io/npm/v/lanview.svg?style=flat-square)](https://www.npmjs.com/package/lanview) [![npm downloads per week](https://img.shields.io/npm/dw/lanview.svg?style=flat-square)](https://www.npmjs.com/package/lanview) [![npm downloads per month](https://img.shields.io/npm/dm/lanview.svg?style=flat-square)](https://www.npmjs.com/package/lanview) [![npm total downloads](https://img.shields.io/npm/dt/lanview.svg?style=flat-square)](https://www.npmjs.com/package/lanview) [![GitHub stars](https://img.shields.io/github/stars/PrashantDhuri08/lanview-cli.svg?style=flat-square)](https://github.com/PrashantDhuri08/lanview-cli/stargazers) [![GitHub forks](https://img.shields.io/github/forks/PrashantDhuri08/lanview-cli.svg?style=flat-square)](https://github.com/PrashantDhuri08/lanview-cli/network/members) [![License](https://img.shields.io/npm/l/lanview.svg?style=flat-square)](https://github.com/PrashantDhuri08/lanview-cli/blob/main/LICENSE)

**Instantly preview full-stack web applications on your mobile device over local Wi-Fi.**

**LanView** is an open-source, zero-config CLI utility that bridges your frontend and backend into a single local gateway with a scannable QR code directly in your terminal. No cloud tunnels (like ngrok), no data limits, no third-party accounts, and zero manual IP configuration  
**just one single command** !!!

![LanView Demo](assets/lv-demo.gif)

---

## 🛑 The Problem It Solves

When testing a web app on a physical mobile device, developers face two major friction points:

1. **Typing Long URLs:** Manually looking up your machine's local IP address and typing `http://192.168.1.45:3000` into a phone browser is tedious and annoying.
2. **The "Localhost" Backend Broken Link:** If your frontend code contains a reference to `http://localhost:5000/api` for backend requests, **it will fail on your phone**. This is because your phone interprets `localhost` as _itself_, not your computer. Changing your source code to hardcoded IPs every time you want to test on mobile is a terrible developer experience.

---

## The Solution: How It Works

**Lanview** creates a temporary, intelligent bridge on your machine. When run, it executes three core steps completely locally:

### 1. Auto-Discovery (Network Mapping)

The tool queries your operating system's network interfaces, filters out internal virtual addresses, and automatically extracts your computer's active LAN IPv4 address (e.g., `192.168.1.15`).

### 2. Micro Reverse Proxy Server

It spins up a lightweight, local HTTP proxy gateway on port `8080`. This gateway acts as a single point of traffic coordination:

- If a request is for static assets or the user interface, it forwards it to your **Frontend** (e.g., Vite/Next.js on port `3000`).
- If a request path starts with `/api`, it intercepts it and forwards it to your **Backend** (e.g., Node/Express/Python on port `5000`).

This completely eliminates CORS issues and allows you to use relative fetch paths (like `fetch('/api/data')`) seamlessly across both desktop and mobile.

### 3. QR Code Terminal Generation

The tool converts the consolidated gateway URL into a scannable QR Matrix and renders it directly inside the developer's terminal using ANSI text blocks.

![LanView Demo](assets/lv-demo.gif)

---

## 🛠️ Key Technical Features

- **Zero Cloud Dependency:** 100% private and offline. Data never leaves your local Wi-Fi router. There are no data limits, third-party accounts, or external latency.
- **Relative-Path Routing:** Because both frontend and backend are multiplexed through a single local port (`8080`), developers don't have to alter a single line of environmental variables or configuration files.
- **Environment Agnostic:** Works with React, Vue, Svelte, Next.js, Vite, Express, Django, Laravel, or any other framework stack.
- **WebSocket HMR support:** Fully proxies WebSockets, keeping your Hot Module Replacement (HMR) connection active on mobile devices.

---

## 📋 Architectural Workflow

```
[ Mobile Phone ] (Connected to Wi-Fi)
       │
       │ (Scans QR -> Hits 192.168.1.XX:8080)
       ▼
  [ Lanview Proxy ]
       │
       ├─── (Default Path / )   ───► [ Local Frontend Server ] (Port 3000)
       │
       └─── (Path is /api/* )   ───► [ Local Backend API ]    (Port 5000)
```

---

## 🚀 Getting Started

### Installation

#### Option A: From NPM

Install the package globally:

```bash
npm install -g lanview
```

Or run it directly with `npx`:

```bash
npx lanview
```

#### Option B: From Source (Local Development)

You can also install and run it from source:

1. **Clone the repository and install dependencies:**

   ```bash
   git clone https://github.com/PrashantDhuri08/lanview-cli.git
   cd lanview
   npm install
   ```

2. **Link the CLI command globally:**
   ```bash
   npm link
   ```
   _(This creates a global symlink so the `lanview` command can be run from any folder on your machine)._

### Usage

Simply run:

```bash
lanview
```

By default, this will run a proxy gateway on port `8080` routing:

- `/api/*` to `http://localhost:5000`
- Everything else to `http://localhost:3000`

#### Serving Static Files (Live Server mode)

Host a folder of static files over the LAN with live reload on save — a drop-in replacement for the VS Code **Live Server** extension, but scannable from your phone:

```bash
lanview --static                # serve current directory
lanview --static ./public       # serve a specific folder
lanview --static ./dist --spa   # SPA: unknown paths serve index.html
lanview --static ./site --no-reload   # disable live reload
lanview --static --open         # serve + open in your browser
```

In `--static` mode:

- Live reload is **on** by default (a tiny WebSocket client is injected into served HTML; the file watcher debounces and pushes a reload message on change).
- If a directory has no `index.html`, a directory listing is rendered.
- `node_modules`, `.git`, and dotfile entries are ignored by the watcher.
- `--spa` makes unknown non-file paths fall back to `index.html` (handy for React Router / Vue Router build output).
- **Linux caveat:** Node's `fs.watch({ recursive: true })` only watches the top-level directory on Linux (subdirectory changes are not detected). On Windows and macOS, recursive watching works natively.

#### Auto-Opening the Browser

Add `--open` (or `-o`) to launch your system's default browser at the gateway URL on start. Works in both proxy and static mode:

```bash
lanview --open
lanview --static --open
```

#### Customization

You can customize the ports and paths via CLI options:

```bash
lanview --frontend 4000 --backend 8000 --gateway 9000 --api-prefix /graphql
```

Options:

- `-f, --frontend <port>` - Port of the frontend server (proxy mode, default: `3000`)
- `-b, --backend <port>` - Port of the backend server (proxy mode, default: `5000`)
- `-g, --gateway <port>` - Port of the proxy gateway / static server (default: `8080`)
- `-p, --api-prefix <path>` - URL prefix to forward to the backend (default: `/api`, `none` if no prefix)
- `-h, --host <ip>` - Manually specify your host IP instead of auto-discovery
- `-s, --static [dir]` - Serve static files from a directory (Live Server mode). Disables proxy mode. Defaults to the current directory.
- `--spa` - SPA fallback: serve `index.html` for unknown paths (only with `--static`)
- `--no-reload` - Disable live reload in static mode (reload is on by default)
- `-o, --open` - Auto-open the gateway URL in your default browser on start
- `--help` - Show help information
