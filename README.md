# ITM-Hackathon
# BlenderMCP - Blender Model Context Protocol Integration

BlenderMCP connects Blender to Claude AI through the Model Context Protocol (MCP), allowing Claude to directly interact with and control Blender. This integration enables prompt assisted 3D modeling, scene creation, and manipulation.

## Prerequisites
- Blender 3.0 or newer
- Python 3.10 or newer
- uv package manager

## Installation

### Cursor integration

Run blender-mcp without installing it permanently through uvx.

- Go to **Cursor Settings** > **MCP** and paste this as a command.

uvx blender-mcp

- For Windows users, add a new server in **Settings** > **MCP** with the following settings:

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

## Installing the Blender Addon

Download the addon.py file from this repo

Open Blender

Go to Edit > Preferences > Add-ons
Click "Install..." and select the addon.py file

Enable the addon by checking the box next to "Interface: Blender MCP"

## Footer
This document is made by team Aditya & Shubham
