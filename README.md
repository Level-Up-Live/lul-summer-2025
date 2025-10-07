
# 🛠️ Custom Games Integration – Game System Setup

This branch provides a customizable game system, allowing developers to integrate their own Unity-based games and connect them with a node-based backend and frontend (RSO App).

It includes:

- A Custom Unity Game Package (`Simulator_CustomGames.unitypackage`)
- A Custom Game Controller (`game-controller-customgames.zip`)

Use this README to install, configure, and integrate your custom game into the system.

## 🧱 Prerequisites

Ensure the following software is installed:

| Tool | Version Recommendation | Download Link |
|------|-------------------------|---------------|
| Unity | 2022.3.x LTS or newer | [unity.com/download](https://unity.com/download) |
| Node.js | v16 or later | [nodejs.org](https://nodejs.org) |
| Code Editor (optional) | VS Code / Visual Studio | [code.visualstudio.com](https://code.visualstudio.com) |

## 🕹️ 1. Unity Game Setup (Custom)

**Steps:**

1. Open Unity Hub and create a new URP project.
2. Import the Custom Game Scene:
   - Open the project.
   - Drag and drop `Simulator_CustomGames.unitypackage` into the Unity Editor.
   - Click **Import All** when prompted.
3. Install `Newtonsoft.Json` package:
   - Go to `Window > Package Manager`
   - Click "Add Package by Name"
   - Enter: `com.unity.nuget.newtonsoft-json`
4. Open the Simulator Scene:
   - Navigate to `Assets/Scenes` and open `Simulator.unity`.
5. **Play the Game:**
   - Hit the Play button to verify everything loads correctly.

## ⚙️ 2. Game Controller Setup (Custom)

**Steps:**

1. Unzip `game-controller-customgames.zip`
2. Open Windows PowerShell in the unzipped folder.
3. Install dependencies:

```bash
npm install
```

4. Start the Game Controller:

```bash
npm run dev
```


## 🖥️ 3. RSO App Setup (Game Selection Interface)

**Steps:**

1. Unzip the RSO App (if not already).
2. Open Windows PowerShell in the unzipped location.
3. Install dependencies:

```bash
npm install
```

4. Run the RSO App:

```bash
npm run dev
```

- Visit: `http://localhost:7700`

✅ Ensure the RSO App is configured to communicate with the Game Controller.

## 🧩 4. Adding Your Custom Game to the System

To make your game selectable in the RSO App and Game Controller:

### 🔧 Step 1: Create a Game Entry in Game Controller

- Navigate to: `Game-Controller/games/`
- Create a new `.yml` file for your game (you can copy and rename `client-driven-test.yml`).
- Update the file:
  - Set `clientDriven: true`
  - Assign a unique `gameId`
  - Update other fields like `name`, `description`, etc.

### 🎮 Step 2: Integrate Your Game in Unity

- In the **Hierarchy**, locate the `CustomGames` GameObject.
- Under `CustomGames`, create child GameObjects for your game:
  - One per lane (e.g., `AsteroidGame_Lane1`, `AsteroidGame_Lane2`)
- For each of these lane GameObjects:
  - Add the `CustomGame` script.
  - In the Inspector:
    - Set **Game ID** (same as in the `.yml` file)
    - Set the **Lane Number**
- Add each lane GameObject as a child of `CustomGames`.
- Under each lane object, add your actual gameplay logic (child objects, scripts, prefabs, etc.)

## 🚦 5. Game Flow: Starting, Running, and Ending

### ✅ Game Start

Use the RSO App to select your game and begin the countdown.

Unity receives a start command and:

- Checks if the game is a custom game.
- Matches **Game ID + Lane Number** with your GameObject.
- Invokes the `StartGame` action on the `CustomGame` script.

### 🧠 Your Script Integration

Subscribe to `StartGame` action:

```csharp
yourCustomGameInstance.StartGame += () => {
    // Your start logic here
};
```

### 🛑 Ending the Game

To end your game, invoke this action:

```csharp
CustomGames.EndCustomGame?.Invoke(gameId, laneNumber);
```

## 🎯 Target Interaction

### Starting a Target

Call this method to start a target:

```csharp
SocketCommunicator.Instance.RequestTarget("targetId");
```

### Deactivating a Target

To deactivate a target:

```csharp
SocketCommunicator.Instance.DeactivateTarget("targetId");
```

### Reacting to Target Hits

When a physical target is hit, this method is triggered:

```csharp
void targetHit(string deviceId)
{
    // Use this to respond in your game
}
```

## 🔗 System Integration

Once your game is added and the system is running:

✅ Unity Game starts and listens for commands  
✅ Game Controller handles game lifecycle and communication  
✅ RSO App allows selection and starting of your game

## ✅ Final Setup Checklist

| Component | Status |
|----------|--------|
| Unity Package | ✅ `Simulator_CustomGames.unitypackage` imported |
| Game Controller | ✅ Runs on port 3000 with custom game entry |
| RSO App | ✅ Loads in browser on port 7700 |
| System Integration | ✅ All parts communicate and custom game starts/stops |

## ❓ Troubleshooting

- **Unity Errors:** Check the Console for missing references or scripts.
- **Game not starting:** Verify Game ID and Lane Number match between Unity and `.yml`.
- **Target issues:** Confirm you're using the correct target ID and that the game is active.
