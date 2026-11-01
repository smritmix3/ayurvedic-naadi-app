# 🌿 NaadiFlow: Digital Ayurvedic Pulse & Bio-State Indicator

**NaadiFlow** is a lightweight, browser-based progressive web application (PWA) that bridges traditional Ayurvedic pulse assessment (*Naadi Pariksha*) with modern optical sensor technology. By utilizing contact Photoplethysmography (PPG) via a smartphone's rear camera and flash placed against the inner wrist, the app extracts real-time blood volume pulse signals to evaluate autonomic nervous system balance and map physiological *Vega* (rate) states.

---

## ✨ Key Features

* **Wrist-Placement Contact-PPG:** Bypasses modern multi-lens smartphone restrictions by utilizing the flat inner wrist over the radial artery for stable, rich vascular readings.
* **Robust Signal Processing:** Implements mathematical signal filtering directly in browser JavaScript:
  * *Exponential Moving Average (EMA) Detrending* to strip away low-frequency motion and breathing drift.
  * *Signal Quality Gating* to automatically pause or reject noisy or unsealed sensor reads.
  * *Adaptive Peak Detection* with a refractory window for precise heart rate interval calculation.
* **Ayurvedic State Mapping:** Translates real-time heart rate and variability metrics into descriptive *Vega* indicators (Fast/Vata, Moderate/Pitta, Slow/Kapha proxies).
* **Zero-Friction Architecture:** Built as a single-file vanilla HTML5/JavaScript web app requiring no heavy app-store downloads or native installations.

---

## 🛠️ Tech Stack

* **Frontend:** HTML5, CSS3 (Modern Flexbox/Grid UI), Vanilla JavaScript (ES6+).
* **APIs:** HTML5 MediaDevices API (`getUserMedia`), HTML5 Canvas API for real-time ROI pixel extraction and waveform rendering.
* **Development Toolchain:** VS Code, Live Server, ngrok (for secure HTTPS tunneling required by mobile browser camera permissions).

---

## 🚀 Getting Started Locally

Because mobile browsers strictly require **HTTPS** and explicit camera permissions to access device sensors and flashlights, follow these steps to run the app locally:

1. **Clone the Repository:**
   ```bash
   git clone [https://github.com/your-username/ayurvedic-naadi-app.git](https://github.com/your-username/ayurvedic-naadi-app.git)
   cd ayurvedic-naadi-app