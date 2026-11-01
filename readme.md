# 🌿 NaadiFlow: Digital Ayurvedic Pulse & Bio-State Indicator

**NaadiFlow** is a lightweight, zero-friction, browser-based progressive web application (PWA) that bridges traditional Ayurvedic pulse assessment (*Naadi Pariksha*) with modern optical sensor technology. By utilizing contact Photoplethysmography (PPG) via a smartphone's rear camera and flash placed flat against the inner wrist, the app extracts real-time blood volume pulse signals to evaluate physiological rate (*Vega*) and proxy doshic tendencies.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [How It Works (Physiological & Mathematical Logic)](#-how-it-works)
- [Tech Stack](#-tech-stack)
- [Repository Structure](#-repository-structure)
- [Getting Started & Local Setup](#-getting-started--local-setup)
- [Usage Instructions](#-usage-instructions)
- [Roadmap & Future Extensions](#-roadmap--future-extensions)
- [Medical Disclaimer](#-medical-disclaimer)

---

## 🔍 Overview

Modern smartphones with multi-camera modules often present physical hurdles for traditional single-finger PPG. **NaadiFlow** solves this by utilizing an **inner-wrist placement technique**, aligning directly with the classical *radial artery* location used in *Naadi Pariksha*. 

The app captures green-channel pixel absorption fluctuations from arterial blood flow, runs real-time mathematical filtering directly in JavaScript, and maps the resulting pulse metrics to Ayurvedic bio-state concepts (*Vata*, *Pitta*, and *Kapha* rate proxies).

---

## ✨ Key Features

- **Wrist-Placement Contact-PPG:** Solves multi-lens layout issues by placing the camera module flat against the inner wrist surface for stable, noise-reduced sensor coverage.
- **In-Browser Signal Processing Pipeline:**
  - **Quality Gating:** Detects and rejects frames with inadequate sealing, motion spikes, or light leakage.
  - **Exponential Moving Average (EMA) Detrending:** Strips low-frequency baseline drift (respiration and postural movement).
  - **Bandpass Filter & Smoothing:** Eliminates high-frequency sensor noise.
  - **Refractory Peak Detection:** Prevents double-peaking and calculates inter-beat intervals (IBI).
- **Ayurvedic State Mapping:** Categorizes real-time pulse rate (*Vega*) into proxy states:
  - **Vata (Fast):** $>88 \text{ BPM}$ (Restless / Active proxy)
  - **Pitta (Moderate):** $72 - 88 \text{ BPM}$ (Balanced / Metabolic proxy)
  - **Kapha (Slow):** $<72 \text{ BPM}$ (Calm / Steady proxy)
- **Zero-Friction Architecture:** Runs as a single self-contained application requiring no native app store installations or third-party dependencies.

---

## 🧮 How It Works

```
[ Wrist Radial Artery ]
          │
  (Rear Camera + LED)
          │
          ▼
[ Green Channel Pixel Extraction ]
          │
          ▼
[ Signal Quality Check (Light Gate) ]
          │
          ▼
[ EMA Baseline Detrending ]
          │
          ▼
[ 5-Point Moving Average Smoothing ]
          │
          ▼
[ Peak Detection with Refractory Window ]
          │
          ▼
[ BPM Calculation & Vega/Dosha Mapping ]
```

1. **Optical Capture:** Blood absorbs green light ($520-560 \text{ nm}$) more effectively than red light. As cardiac cycles pump blood through the radial artery, green pixel values vary sinusoidally.
2. **Mathematical Filtering:**
   - **Baseline Detrending:**
     $$y[t] = x[t] - \text{EMA}(x[t])$$
     where $\text{EMA}(x[t]) = \alpha \cdot x[t] + (1 - \alpha) \cdot \text{EMA}[t-1]$ ($\alpha = 0.05$).
   - **Refractory Window:** Imposes a minimum $350 \text{ ms}$ spacing between recognized peaks to prevent false triggers from secondary heart waveforms (dicrotic notches).

---

## 🛠️ Tech Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+).
- **APIs:** 
  - `navigator.mediaDevices.getUserMedia` (HTML5 Camera Access)
  - Canvas API (Real-time pixel processing & waveform rendering)
- **Deployment / Tunneling:** Live Server, ngrok (for mobile HTTPS access).

---

## 📁 Repository Structure

```text
ayurvedic-naadi-app/
├── index.html          # Unified application (HTML, CSS UI, Signal Logic)
├── LICENSE             # MIT License
└── README.md           # Project documentation
```

---

## 🚀 Getting Started & Local Setup

Mobile web browsers require **HTTPS** and explicit permissions to grant access to rear cameras and hardware flashlights.

### Prerequisites

- [Node.js](https://nodejs.org/) (optional, for local servers)
- [VS Code](https://code.visualstudio.com/) with **Live Server** extension
- [ngrok](https://ngrok.com/) (for HTTPS tunneling to mobile devices)

### Setup Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/ayurvedic-naadi-app.git
   cd ayurvedic-naadi-app
   ```

2. **Start a local development server:**
   - In VS Code, open `index.html` and click **"Go Live"** (default port: `5500`).

3. **Tunnel for HTTPS testing on a mobile phone:**
   ```bash
   ngrok http 5500
   ```

4. **Access the App:**
   - Open the generated `https://<your-subdomain>.ngrok-free.app` link on your mobile browser.

---

## 📱 Usage Instructions

1. Open the application link on your phone's browser.
2. Tap **"Start Contact Scan"** and grant camera permissions.
3. Place the phone's **rear camera lens and flash flat against your inner wrist** (just below the thumb along the radial artery).
4. Apply gentle, steady pressure. Avoid pressing too hard (collapses artery) or too softly (lets light leak in).
5. Hold still for **5 to 10 seconds** while the live waveform stabilizes and calculates your *Vega* proxy.

---

## 🔮 Roadmap & Future Extensions

- [ ] **Smartwatch Integration:** Connect passive resting heart rate and background HRV metrics via Apple HealthKit and Google Health Connect APIs.
- [ ] **Circadian (Dinacharya) Dashboard:** Integrate time-of-day dosha tracking (Kapha: 6-10 AM, Pitta: 10-2 PM, Vata: 2-6 PM) to provide dynamic lifestyle nudges.
- [ ] **HRV Time-Domain Analysis:** Calculate **RMSSD** and **SDNN** parameters to measure autonomic stress balance.

---

## ⚠️ Medical Disclaimer

*NaadiFlow is strictly an experimental wellness tool and educational prototype. It does not provide medical diagnoses, clinical measurements, or certified Ayurvedic therapeutic treatments. Always consult a licensed healthcare professional or certified Ayurvedic practitioner for medical advice.*

