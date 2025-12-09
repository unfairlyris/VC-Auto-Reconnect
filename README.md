# VC Auto Reconnect  
**A robust, minimal-overhead BetterDiscord plugin for persistent automatic reconnection to a specific Discord voice channel using its Channel ID.**

![License](https://img.shields.io/badge/License-GNU%20GPLv3-blue.svg)
![Platform](https://img.shields.io/badge/Platform-BetterDiscord-orange.svg)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen.svg)
![Maintained](https://img.shields.io/badge/Maintained-Yes-success.svg)
![Language](https://img.shields.io/badge/Language-JavaScript-yellow.svg)

---

## 🧭 Overview
**VC Auto Reconnect** is a highly focused BetterDiscord plugin designed to automatically reconnect a user to a predetermined Discord voice channel using its Channel ID.

It is engineered for:

- Persistent AFK monitoring setups  
- Real-time communication environments  
- Users with unstable networks  
- Automated workflows requiring sustained VC presence  
- Private workspace channels or audio monitoring streams  

This plugin is built with the philosophy of **minimalism, reliability, and predictability**.

---

## 🎯 Key Features

### ✔ Targeted Voice Reconnection  
Reconnects *only* to the specified voice channel — avoids unintended channel switching.

### ✔ Intelligent Call State Detection  
Automatically detects current voice connection state via UI signals to prevent spam or repeated joins.

### ✔ Automatic Background Operation  
Starts monitoring immediately when the plugin is enabled. Requires no UI interaction.

### ✔ Cooldown-Based Execution  
Ensures stable rejoin logic that avoids Discord’s anti-spam protections and prevents loop conditions.

### ✔ Lightweight Implementation  
Minimal DOM querying, zero dependencies, and low performance footprint.

### ✔ Full Canary + Linux Support  
Compatible with modded environments and experimental Discord UI branches.

---

## 🧩 Technical Architecture

### 🔹 Core Loop  
A periodic interval checks:

1. Whether the user is currently in a voice call  
2. Whether the target voice channel is available  
3. Whether the cooldown has elapsed  
4. Whether reconnection should be triggered  

### 🔹 DOM Selectors  
Selectors target:

- Button elements for "Leave Call" / "Disconnect" indicators  
- Sidebar channel elements via:  
  - `data-list-item-id="channels___<id>"`  
  - `data-list-item-id$=":<id>"`  
  - Fallback `href*="<id>"`

### 🔹 Storage  
Settings utilize:

```
BdApi.Data.load("VCReconnect", key)
BdApi.Data.save("VCReconnect", key, value)
```

### 🔹 No External Libraries  
Pure JavaScript with fully isolated runtime footprint.

---

## 🖥 Compatibility

| Platform | Supported |
|----------|-----------|
| **Discord Stable** | ✔ Yes |
| **Discord Canary** | ✔ Yes |
| **BetterDiscord** | ✔ Required |
| **Windows** | ✔ |
| **Linux** | ✔ (tested) |
| **macOS** | ✔ |
| **Themes / Custom UIs** | ✔ Mostly (as long as VC sidebar is visible) |

---

## 📥 Installation

### **1. Install BetterDiscord**
Official site: https://betterdiscord.app/

### **2. Place the Plugin File**

#### Linux
```
~/.config/BetterDiscord/plugins/
```

#### Discord Canary (Linux)
```
~/.config/discordcanary/BetterDiscord/plugins/
```

#### Windows
```
%appdata%/BetterDiscord/plugins/
```

### **3. Enable the Plugin**
Navigate to:

```
User Settings → BetterDiscord → Plugins → VC Auto Reconnect
```

---

## ⚙ Configuration

### **Target Voice Channel ID**
Enter a valid Discord voice channel ID.

How to obtain:
1. Enable Developer Mode  
2. Right-click the voice channel  
3. Select **Copy ID**

### **Check Interval (ms)**  
Defines how frequently the plugin evaluates reconnection criteria.

Recommended: `5000 – 8000 ms`

---

## 🚀 How It Works

The plugin uses a deterministic, safe loop:

1. Detect voice call participation  
2. Detect availability of the target channel element  
3. Validate cooldown  
4. Issue a `.click()` event on the target channel  
5. Discord handles the voice join internally  

No DOM mutation is performed.  
No override of internal Discord functions occurs.

---

## 🧠 Design Principles

- **Minimalism:** Only essential logic is implemented  
- **Stability:** Avoids interacting with transient UI elements  
- **Predictability:** No hidden behaviors or auto-fallback channels  
- **Fail-Safe:** Errors are logged without interrupting operation  
- **Control:** Reconnects *only* to a user-defined VC  

---

## 🔒 Security Considerations

This plugin:

- Does not transmit data to external servers  
- Does not intercept or modify audio streams  
- Does not modify core Discord functionality  
- Only executes local DOM interactions  

User privacy is fully preserved.

---

## ⚠️ Limitations

- The target voice channel must be visible in the sidebar  
- Will not reconnect if the server UI is collapsed or scrolled away  
- Cannot bypass permission restrictions  
- Will not auto-switch servers if in the wrong guild  
- Does not handle Discord outages or full client reloads  

---

## 🐛 Troubleshooting

### Plugin does not reconnect
- Verify the Channel ID  
- Ensure the channel is visible in the UI  
- Verify the interval is not set too low  
- Check for console errors (`Ctrl+Shift+I → Console`)

### Plugin reconnects too often
Increase `reconnectCheckInterval` or cooldown values.

### Plugin reconnects to the wrong channel
Double-check the Channel ID value in settings.

---

## 👨‍💻 Development Guide

### Local Build / Modification
The plugin is entirely self-contained. No build tools are required.

### Code Style
- ES6 classes  
- Functional helpers for persistence  
- Clean event loop–based architecture  
- Modular and easily extendable  

### Suggested Enhancements
- Optional Toast UI integration  
- Reconnection analytics panel  
- Multiple VC profiles  
- Smart guild switching  

---

## 🤝 Contributing

Contributions, bug reports, and feature requests are welcome.

Please submit via GitHub:

- Issues  
- Pull requests  
- Discussions  

Ensure all contributions adhere to:
- JavaScript style consistency  
- Safety of Discord DOM interactions  
- GNU GPLv3 licensing requirements  

---

## 📜 License  
This project is licensed under the **GNU General Public License v3.0**.

```
Copyright (C) 2025 unfairlyris

This program is free software: you can redistribute it and/or modify  
it under the terms of the GNU General Public License as published by  
the Free Software Foundation, either version 3 of the License, or  
(at your option) any later version.

This program is distributed in the hope that it will be useful,  
but WITHOUT ANY WARRANTY; without even the implied warranty of  
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the  
GNU General Public License for more details.

You should have received a copy of the GNU General Public License  
along with this program. If not, see <https://www.gnu.org/licenses/>.
```

---

## ⭐ Support the Project

If this plugin improves your workflow, consider starring the GitHub repository.  
Your support encourages further development and long-term maintenance.

---
