# ITM-Hackathon

# 🎨 BlenderMCP — Blender Model Context Protocol Integration

> **Connect Blender to Claude AI through the Model Context Protocol (MCP) and unlock prompt-assisted 3D modeling, scene creation, and manipulation — all from natural language.**

![Blender](https://img.shields.io/badge/Blender-3.0%2B-orange?logo=blender&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![MCP](https://img.shields.io/badge/Protocol-MCP-purple)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
  - [Installing the Blender Addon](#1--installing-the-blender-addon)
  - [Cursor Integration](#2--cursor-integration)
  - [Claude Desktop Integration](#3--claude-desktop-integration)
- [Usage](#-usage)
- [Architecture](#-architecture)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [Credits](#-credits)

---

## 🌟 Overview

**BlenderMCP** connects Blender to Claude AI through the **Model Context Protocol (MCP)**, allowing Claude to directly interact with and control Blender. This integration enables prompt-assisted 3D modeling, scene creation, and manipulation — simply describe what you want, and watch it come to life in Blender.

---

## ✨ Features

| Category | Capabilities |
|---|---|
| **🧊 3D Object Management** | Create, modify, delete, and inspect objects (Cube, Sphere, Cylinder, Plane, Cone, Torus, and more) |
| **🎨 Materials & Textures** | Apply and edit materials, set colors (RGBA), adjust metallic/roughness/specular properties |
| **📸 Rendering** | Render scenes with custom resolution, output path, and format settings |
| **🌄 PolyHaven Integration** | Browse and download high-quality HDRIs, textures, and 3D models from [PolyHaven](https://polyhaven.com) |
| **🤖 AI 3D Generation** | Generate 3D models from text prompts using **Hyper3D Rodin** AI (supports both main site and fal.ai backends) |
| **💻 Code Execution** | Execute arbitrary Python code inside Blender for advanced automation |
| **🔍 Scene Inspection** | Get detailed scene info — object names, types, locations, rotations, scales, bounding boxes, and more |

---

## 📋 Prerequisites

Before you begin, make sure you have the following installed:

- **Blender 3.0** or newer — [Download Blender](https://www.blender.org/download/)
- **Python 3.10** or newer — [Download Python](https://www.python.org/downloads/)
- **uv** package manager — [Install uv](https://docs.astral.sh/uv/getting-started/installation/)

---

## 🚀 Installation

### 1. 🧩 Installing the Blender Addon

1. **Download** the `addon.py` file from this repository.
2. **Open Blender**.
3. Go to **Edit → Preferences → Add-ons**.
4. Click **"Install..."** and select the downloaded `addon.py` file.
5. **Enable** the addon by checking the box next to **"Interface: Blender MCP"**.
6. You should now see a **BlenderMCP** panel in the 3D Viewport sidebar (`N` key to toggle).

### 2. 🖱️ Cursor Integration

Run `blender-mcp` without installing it permanently through `uvx`:

- Go to **Cursor Settings → MCP** and paste this as a command:

  ```
  uvx blender-mcp
  ```

- **For Windows users**, add a new server in **Settings → MCP** with the following configuration:

  ```json
  {
      "mcpServers": {
          "blender": {
              "command": "cmd",
              "args": [
                  "/c",
                  "uvx",
                  "blender-mcp"
              ]
          }
      }
  }
  ```

### 3. 🖥️ Claude Desktop Integration

To use BlenderMCP with the **Claude Desktop** app, add the following to your Claude Desktop MCP configuration:

```json
{
    "mcpServers": {
        "blender": {
            "command": "uvx",
            "args": ["blender-mcp"]
        }
    }
}
```

---

## 🛠️ Usage

1. **Start the server** — Open Blender, go to the **BlenderMCP** panel in the sidebar, and click **Start Server**. The server listens on `localhost:9876` by default.
2. **Connect from Claude** — Use Cursor, Claude Desktop, or any MCP-compatible client connected to the `blender-mcp` server.
3. **Give natural-language commands** — Examples:
   - *"Create a red sphere at position (2, 0, 1)"*
   - *"Add a metallic gold material to the cube"*
   - *"Render the scene at 1920×1080"*
   - *"Download an HDRI from PolyHaven and set it as the world background"*
   - *"Generate a 3D model of a medieval sword using Hyper3D"*

---

## 🏗️ Architecture

```
┌──────────────┐        MCP         ┌──────────────────┐
│  Claude AI   │◄──────────────────►│  blender-mcp     │
│  (LLM)       │   (stdio / SSE)   │  (MCP Server)    │
└──────────────┘                    └────────┬─────────┘
                                             │ TCP :9876
                                             ▼
                                    ┌──────────────────┐
                                    │  Blender Addon   │
                                    │  (addon.py)      │
                                    │  Socket Server   │
                                    └──────────────────┘
```

- **Claude AI** sends high-level commands via MCP.
- **blender-mcp** (the MCP server) translates them into JSON commands.
- **addon.py** (running inside Blender) receives commands over a local TCP socket and executes them in Blender's Python environment.

---

## ❓ Troubleshooting

| Issue | Solution |
|---|---|
| **Server won't start** | Make sure no other process is using port `9876`. Check the Blender console for error messages. |
| **Connection refused** | Ensure the Blender addon is enabled and the server is running (green status in the panel). |
| **`uvx` not found** | Install the `uv` package manager: `pip install uv` or see the [uv docs](https://docs.astral.sh/uv/getting-started/installation/). |
| **Addon not visible** | Press `N` in the 3D Viewport to open the sidebar, then look for the **BlenderMCP** tab. |
| **PolyHaven assets fail** | Check your internet connection. PolyHaven API requires network access. |
| **Hyper3D generation fails** | Verify your API key is set correctly in the addon preferences. A free trial key is included by default. |

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve BlenderMCP:

1. **Fork** this repository.
2. **Create** a feature branch: `git checkout -b feature/my-feature`
3. **Commit** your changes: `git commit -m "Add my feature"`
4. **Push** to the branch: `git push origin feature/my-feature`
5. **Open a Pull Request** and describe your changes.

---

## 👥 Credits

**Made with ❤️ by Team Aditya & Shubham**

*Built for the ITM Hackathon*

---

<p align="center">
  <i>If you find this project useful, give it a ⭐ on GitHub!</i>
</p>
