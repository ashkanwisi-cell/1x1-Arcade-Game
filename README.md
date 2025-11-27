# Adan 1x1

**Adan 1x1** is a vertical, mobile-first arcade mini-game built with a single `index.html` file using pure **HTML + CSS + JavaScript**.  
You control a glowing square sliding through a corridor of white pillars, chaining combos, abusing risk-reward zones, and dashing through obstacles when your AI “coach” is fully charged.

Designed for **portrait mobile** (1080×1920) and meant to run directly in the browser or via **GitHub Pages**.

---

## 🕹 Gameplay Overview

- You control a **single square block** moving up and down.
- White glowing pillars slide from **right to left**.
- Don’t touch the pillars (unless you’re dashing).
- Stay alive as long as possible to increase your **score**, **level**, and **rank**.
- Use power-ups and the **Ultimate Dash** to break through pillars for a short time.
- The AI face in the top-right acts as your **charge meter** and emotional coach.

The core loop is:

> Survive → build combo & flow → earn XP & rewards → unlock skins & trophies → try to beat your best run.

---

## 🎮 Controls

### Mobile (primary target)
- **Drag up / down** on the screen  
  Move the block vertically to dodge pillars.
- **Tap AI face (top-right)** when its ring turns **green**  
  Trigger **Ultimate Dash** and smash through pillars for a few seconds.

### Other
- The game is **designed for mobile/touch**.  
  Desktop/keyboard controls are not the main target and may be limited.

---

## ✨ Core Features

- **Mobile-first portrait canvas**: `1080×1920`, responsive inside a centered, rounded wrapper.
- **Single-file build**: everything is inside `index.html` (HTML, CSS, JS).
- **Player profile**  
  - Asks your **player name** on first launch.  
  - Name is shown in HUD and in **share message**.
- **Score system**
  - Score grows with time, difficulty, and **Flow Zone** multiplier.
  - Best score is saved in `localStorage`.
- **Difficulty & events**
  - Difficulty presets: **Easy / Normal / Hard**.
  - Dynamic events: `Hyper Speed`, `Calm Flow`, `Tight Gaps`.
  - Daily modifier (e.g. slightly faster Hyper, more calm windows, tighter gaps).

---

## 🧠 Flow Zone, Combo & Risk–Reward

- A central horizontal band is the **Flow Zone**:
  - Staying inside it slowly increases your **risk multiplier** (score ×1.3 in full flow).
  - Leaving it causes the multiplier to decay back towards ×1.0.
- **Combo / Streak**
  - Power-ups, close calls, and safe survival push your **Combo xN**.
  - Combos influence score & feeling of “being in the zone”.
  - Near misses trigger short **slow-motion** and “Too close!” feedback.
- **Close Call detection**
  - Getting very close to pillar edges without touching them increases combo and mission counters.

---

## ⚡ Ultimate Dash & AI Face

Top-right you see a **glassy card** with:

- An **outer ring** showing ultimate charge.
- An **inner face** (AI coach) with different **moods**:
  - `neutral`, `happy`, `sad`, `scared`.
  - Reacts to your performance, missions, level-ups, etc.
- When the ring is full → turns **green** → Ultimate is **READY**.

**Ultimate Dash**:

- Tap the AI face (or the central **READY** button when visible).
- For a few seconds:
  - Pillars that collide with you are **destroyed** instead of killing you.
  - Extra glowing particles and stronger glow around the player.
- Dash usage is tracked for missions and trophies.

---

## 🎯 Missions, Trophies & Meta Progression

### Missions

- Stored in `localStorage`, with:
  - `id`, `text`, `type`, `target`, `progress`, `rewardXP`, `done`, `claimed`, `requires`.
- Mission types include:
  - `scoreRun` (reach X score in one run),
  - `dashCount`,
  - `closeCount`,
  - `flowTime`,
  - `comboMax`.
- Missions are **node-based**:
  - Some missions require completion of previous ones.
  - Claiming missions grants **XP**.

### Trophies

Static list defined in JS, examples:

- `first_dash` – used dash once.
- `score_1000`, `score_3000`, `score_5000`.
- `close_10` – 10 close calls total.
- `level_3`, `level_5`, `level_10`.
- `skin_5` – unlocked 5 skins.
- `flow_master` – long Flow Zone control.
- `snake_tunnel` – survived multiple “Snake Tunnel” patterns.

Unlocked trophies are saved and rendered in a dedicated **Trophies** screen.

### XP & Levels

- XP is earned from:
  - Score over time,
  - Missions,
  - Some events / flow bonuses.
- Level thresholds are based on XP (`level * 200`).
- Level-ups:
  - Trigger AI reactions & haptic (where supported),
  - Unlock skins and some trophies.
- Level and XP are persisted in `localStorage`.

### Season Progress

- A simple **Season Neon** progress bar:
  - Tier = floor(XP / 1000) + 1.
  - Progress percentage inside current 1000 XP.
- Shown both in **Main Menu** and **Missions** screen.

---

## 🎨 Skins & Study Mode

### Skins

- Several named skins (e.g. `Repin Line`, `Structural Grid`, etc.).
- Each skin has:
  - A **color**,
  - A **required level** to unlock.
- Skin selection:
  - `Skins` screen with preview box, name, status.
  - Only skins at or below your level are usable.
- Unlocking 5 skins triggers a trophy.

### Hidden Study Mode

- **Secret toggle**:
  - Tap the level badge in the main menu **3 times quickly**.
- When active:
  - Extra structural lines & guides are drawn in the background.
  - Label “Study Mode” appears.
- Saved in `localStorage`, can be toggled on/off again the same way.

---

## 🔊 Audio: SFX & Custom Background Music

### SFX (Sound Effects)

- All SFX are generated **in code** via the **Web Audio API**:
  - No external audio files.
  - Simple 8-bit–style bleeps using oscillators (triangle/square/sine/sawtooth).
- Sound events:
  - UI clicks
  - Game start
  - Hits
  - Dash
  - Power-ups
  - Combos / milestones
- SFX can be **toggled on/off** from **Settings**:
  - `SFX: On / Off`
  - The choice is saved with `localStorage`.

### Background Music (User File)

- In **Settings** there is a **file input**:
  - Accepts `audio/*` (`mp3`, `wav`, etc., depending on browser).
  - The selected file is loaded via `URL.createObjectURL`.
  - Played as a looping background track while the game is open.
- No upload to server; the audio stays **local in the browser session**.

---

## ⚙️ Settings

Settings screen lets you choose:

- **Difficulty**: `Easy`, `Normal`, `Hard`.
- **Graphics**: `High` (glow & particles) or `Low` (simpler visuals).
- **Vibration**: `On / Off` (for devices that support `navigator.vibrate`).
- **SFX**: `On / Off` (new option).
- **Community Tag**: e.g. `KURD-TEAM`, `FRIENDS-01`.
  - This tag appears in the **share text**, so players can build local “leagues”.
- **Custom Background Music**: local audio file selector.

All settings are persisted in `localStorage`.

---

## 📱 UI / UX Notes

- Visual style inspired by **iOS glassmorphism**:
  - Rounded cards,
  - Blur, soft borders, subtle gradients,
  - Pill buttons with highlight/pressed animation.
- Main screens:
  - **Name** (first launch / change name)
  - **Home / Main Menu**
  - **Play**
  - **Pause**
  - **Game Over**
  - **Missions**
  - **Trophies**
  - **Skins**
  - **Settings**
  - **Credits**
  - **Tutorial**
- Buttons use a small **“tap bounce”** animation to feel native on mobile.

---

## 🧩 File Structure

This project is intentionally minimal:

```text
/
└── index.html    # Everything is here: HTML, CSS, JavaScript game logic and UI

🚀 Running Locally


Clone or download the repository.


Open index.html in a modern browser (Chrome, Edge, Safari, etc.).


For best results on mobile:


Serve the file with a tiny local server (optional but recommended):


# Python 3
python -m http.server 8000

Then open:
http://localhost:8000/index.html



Open the URL in your phone browser (same Wi-Fi) to experience the game as intended.



🌐 Deploying on GitHub Pages


Create a new GitHub repository.


Add index.html to the root of the repo.


Commit and push.


In GitHub:


Go to Settings → Pages,


Source: Deploy from a branch,


Branch: main (or master), folder: / (root).




Save, wait for deployment.


Your game will be available at:
https://<your-username>.github.io/<your-repository>/



Open that URL on your phone for the full mobile experience.

🔧 Customization Tips
All logic lives in index.html. Some places you might want to tweak:


Difficulty tuning


Search for difficulty === "easy", hard, etc.


Adjust gapSize, obstacleSpeed, spawn intervals.




Events


Functions: startRandomEvent() and clearEvent().




Missions & trophies


Arrays: defaultMissions() and TROPHY_DEFS.




Skins


Array: playerSkins – add new entries with name, color, unlockLevel.




Audio


SFX logic is in the section marked SFX SYSTEM.


You can change oscillator types, frequencies and durations.





👤 Credits


Game name: Adan 1x1


Concept & creator: @ashkanwaisi


Label / author: ashkan wisi


Tech: HTML + CSS + JavaScript (no external libs)


Feel free to fork, tweak, and adapt this mini-game for your own experiments or portfolio.


