# 🤖 3D AI Mascot - Real-Time Lip Sync & Animation

A web-based, interactive 3D mascot designed to act as a frontend interface for AI conversational agents. This project features a fully rigged 3D character with idle breathing animations, custom branded clothing, and real-time audio-to-mouth synchronization (visemes).

![3D Mascot Screenshot](<img width="1916" height="988" alt="Screenshot 2026-06-29 155155" src="https://github.com/user-attachments/assets/63b2f250-c97e-41bf-b133-f599e3dc8a29" />) 


## ✨ Features
* **Real-Time Lip Sync:** Uses facial morph targets (Shape Keys) mapped to audio timestamps to simulate natural talking.
* **Idle Animations:** Includes a continuous "breathing" loop blended with the facial movements.
* **Custom PBR Textures:** Modified UV maps allowing for custom branding and logos on the character's clothing.
* **Interactive 3D Camera:** Built with Three.js `OrbitControls`, allowing users to click, drag, rotate, and zoom around the mascot.
* **Optimized for Web:** Packaged as a single `.glb` (glTF Binary) file for fast loading and rendering.

## 🛠️ Tech Stack
* **3D Engine:** [Three.js](https://threejs.org/) (Vanilla ES6 Modules)
* **3D Modeling & Animation:** Blender, Avaturn, Mixamo
* **Lip-Sync Mapping:** Rhubarb Lip Sync standard (mapping audio phonemes to 3D visemes)

## 📂 Repository Structure
```text
📦 repo-name
 ┣ 📜 index.html              # Main frontend UI and Three.js logic
 ┣ 📜 AI_Mascot.glb           # The 3D model (Meshes, Textures, Morph Targets, Animations)
 ┣ 🔊 voice.wav               # Sample audio file for lip-sync testing
 ┗ 📜 README.md
```

## 🚀 How to Run Locally
Because this project loads external 3D files (`.glb`) and uses ES6 modules, you **cannot** just double-click the `index.html` file (your browser will block it due to CORS security policies). You must run it through a local web server.

**Method 1: VS Code (Recommended)**
1. Open this folder in Visual Studio Code.
2. Install the **Live Server** extension.
3. Right-click `index.html` and select **"Open with Live Server"**.

**Method 2: Python (Command Line)**
1. Open your terminal/command prompt.
2. Navigate to this folder.
3. Run: `python -m http.server 8000`
4. Open your browser and go to `http://localhost:8000`

## 🧠 AI Integration Pipeline (For Backend Developers)
Currently, this repo demonstrates the frontend logic using a pre-recorded audio file and hardcoded JSON timestamps. 

To connect this mascot to a live AI backend, the system should follow this pipeline:
1. **LLM Generation:** Send user text to an LLM (e.g., OpenAI, Anthropic).
2. **Text-to-Speech (TTS):** Convert the text response into an audio buffer (e.g., ElevenLabs, Azure TTS).
3. **Viseme Generation:** Generate an array of mouth shapes and timestamps based on the audio. *(Note: Azure TTS natively returns this data. Other TTS engines require running the audio through a tool like Rhubarb Lip Sync on the backend).*
4. **WebSocket/API Return:** Send the audio file and the JSON array to this frontend.
5. **Render Loop Sync:** The Three.js `requestAnimationFrame` loop will read the `audio.currentTime` and apply a `lerp` to the corresponding 3D morph target (A, B, C, D, etc.) to animate the mouth dynamically.

## 📝 3D Model Notes
* If replacing the `.glb` model in the future, ensure the new model uses the same **Morph Target dictionary names** (e.g., `viseme_aa`, `viseme_O`, `viseme_E`) or update the mapping object in the `index.html` script.
* Ensure exported `.glb` models have their transforms applied (Scale 1,1,1) in Blender before uploading to the web.
```
