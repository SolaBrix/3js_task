# ☀ Shadow Simulation Project – Test Assignment

## 📌 Objective

This project is a technical test to evaluate your skills in 3D modeling, light simulation, and camera setup using **Three.js**. The goal is to visualize a 3D object placed on the ground and display its **real-world sun shadow** as it would appear on **22nd December 2025 at 5:00 PM**, based on your **actual home coordinates**.

---

## 🎯 Requirements

### ✅ Core Features:
- Load a 3D model (example: cube)
- Set up a **Three.js** scene with:
  - **Directional light** acting as the sun
  - **Ground plane** to receive shadows
  - **Orthographic camera** to capture shadow clearly
- Use your own **latitude and longitude**
- Calculate the sun's position for:
  - 📅 **Date:** 21st December 2025
  - 🕔 **Time:** 5:00 PM (local time)
- Render shadows accurately on the plane

---

## 🌍 Sun Positioning
Use a library like [SunCalc](https://github.com/mourner/suncalc) or [suncalc3](https://www.npmjs.com/package/suncalc3) to get:
- **Altitude** (vertical angle of the sun)
- **Azimuth** (horizontal angle from North)

Use this to position your directional light in the scene like so:

js
// Example
const { altitude, azimuth } = SunCalc.getPosition(new Date("2025-12-22T17:00:00"), latitude, longitude);

// Convert to directional light position
const distance = 100;
const x = distance * Math.cos(altitude) * Math.sin(azimuth);
const y = distance * Math.sin(altitude);
const z = distance * Math.cos(altitude) * Math.cos(azimuth);

directionalLight.position.set(x, y, z);
`

---

## 🎥 Camera

Use an **OrthographicCamera** for accurate, non-distorted shadow representation. Suggested top-down or isometric angle:

js
const aspect = window.innerWidth / window.innerHeight;
const frustumSize = 20;

const camera = new THREE.OrthographicCamera(
  (frustumSize * aspect) / -2,
  (frustumSize * aspect) / 2,
  frustumSize / 2,
  frustumSize / -2,
  1,
  1000
);

camera.position.set(10, 10, 10); // adjust as needed
camera.lookAt(0, 0, 0);


---

## 🖼 Output

### Expected Output:

* A working **webpage** (hosted via `index.html`)
* Shadows cast by the object as per real-world sun position
* Clean interface; camera should clearly show the object + shadows

---

## 📦 How to Run

1. Clone this repo:

   bash
   git clone https://github.com/YOUR-USERNAME/shadow-simulation-test.git
   cd shadow-simulation-test
   

2. Install dependencies:

   bash
   npm install
   

3. Run the project locally:

   bash
   npm run dev
   

   Or simply open `index.html` in your browser if no build tools are used.
