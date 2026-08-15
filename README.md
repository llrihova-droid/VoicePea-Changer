# 🎙️ VoicePea Changer

VoicePea Changer is a GPU-accelerated, lightweight Web App and Progressive Web Application (PWA) designed for real-time voice synthesis, pitch shifting, and custom voice profile recording.

Built with a **Liquid Glassmorphism UI**, VoicePea delivers responsive 60 FPS performance, mobile optimization, and native backend compatibility.

---

## ✨ Features

* **Liquid Glass UI:** Ultra-smooth, hardware-accelerated CSS with `cubic-bezier` motion curves and backdrop blurs.
* **Modal Overlay Architecture:** Clean, uncluttered interface that displays recorder and hardware permission views only when triggered.
* **Custom Voice Sampling:** Capture raw PCM buffers to synthesize 10-second custom voice pitch profiles.
* **Cross-Platform Responsive Layout:** 
  * Full controls & fine-tuning sliders on **Desktop/PC**.
  * Streamlined single-column layout on **Mobile & PWA**.
* **Flask Python Backend:** Lightweight serving of web assets with zero-dependency static file routing.

---

## 📁 Project Structure

```text
.
├── index.html       # Primary UI template with embedded GPU CSS & modal controllers
├── main.py          # Flask backend server & static asset router
├── app.js           # Client-side audio processing & Web Audio API logic
├── manifest.json    # Progressive Web App (PWA) configuration
├── sw.js            # Service worker for offline functionality
└── README.md        # Project documentation
