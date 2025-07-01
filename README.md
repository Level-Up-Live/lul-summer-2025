# 🎮 Game Template Setup

This repository contains a full game system composed of:
- A **Node-based Game Controller**
- A **Node-based Game Selection App (RSO App)**
- A **Unity-based Game** (exported as a `.unitypackage`)

Interns can use this repo to install, configure, and test the complete system on their local machines.



---

## 🧱 Prerequisites

Make sure the following software is installed on your system:

| Tool       | Version Recommendation | Download Link                          |
|------------|------------------------|----------------------------------------|
| Unity      | 2022.3.x LTS or newer  | [unity.com/download](https://unity.com/download) |
| Node.js    | v16 or later           | [nodejs.org](https://nodejs.org/)      |
| Code Editor (optional) | VS Code / Visual Studio | [code.visualstudio.com](https://code.visualstudio.com/) |

---

## 🕹️ 1. Unity Game Setup

### Steps:

1. **Open Unity Hub** and create a new URP project.  
2. **Import the Game Scene**:
   - Open the project.
   - Drag and drop `LUL-Simulator-V*.unitypackage` into the Unity Editor.
   - When prompted, click **Import All**.
3. **Install newtonsoft package from package manager**
   - Open the Package Manager (Window->Package Manager)  
   - Click on "Add Package By Name"
   - Enter `com.unity.nuget.newtonsoft-json` as package name
3. **Open the Simulator Scene**:
   - Navigate to `Assets/Scenes` or wherever the scene was imported.
   - Open the scene (e.g., `Simulator.unity`).
4. **Play the Game**:
   - Click the Play button to ensure everything runs smoothly.
   
---

## ⚙️ 2. Game Controller Setup (Node.js)

### Steps:

1. **Unzip the Game Controller**:
2. Open Windows PowerShell in the unzipped location
3. Install dependencies:
```bash
npm install
```

4. Run the Game Controller:
```bash
npm run dev
```
The controller will launch on a port 3000(e.g., http://localhost:3000).

---
## 🖥️ 3. RSO App Setup (Game Selection Interface)
### Steps:
1. Unzip the RSO App:
2. Open Windows PowerShell in the unzipped location
3. Install dependencies:
```bash
npm install
```
Run the RSO App:
```bash
npm run dev
```
Open your browser and navigate to http://localhost:7700.
⚙️ Ensure that the RSO App is correctly configured to talk to the Game Controller backend.

---
### 🔗 Connecting the System
Follow the video guide to test the entire system.

---

### ✅ Final Setup Checklist
Component	Status
Unity Package	✅ Imported and runs in editor
Game Controller	✅ Starts and listens on port 3000
RSO App	✅ Loads in browser - port 7700
System Integration	✅ All parts communicate properly

### ❓ Troubleshooting
Unity Errors: Check Console for missing scripts or compile errors.

