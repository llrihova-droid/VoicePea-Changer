<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>VoicePea Changer</title>

  <!-- PWA Manifest & App Settings -->
  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#18181b">

  <style>
    /* =========================================================
       1. CORE ACCELERATION & LIQUID GLASS BASE
       ========================================================= */
    * {
      box-sizing: border-box;
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
      -webkit-font-smoothing: antialiased;
    }

    body {
      background-color: #0b0c0e;
      background-image: 
        radial-gradient(at 0% 0%, rgba(29, 185, 84, 0.15) 0px, transparent 50%),
        radial-gradient(at 100% 100%, rgba(59, 130, 246, 0.15) 0px, transparent 50%);
      color: #f4f4f5;
      margin: 0;
      padding: 40px 20px;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    /* MAIN APP CONTAINER */
    .voizz-box {
      width: 650px;
      max-width: 95vw;
      padding: 32px;
      border-radius: 28px;
      position: relative;
      transform: translateZ(0);
      background: rgba(255, 255, 255, 0.06) !important;
      backdrop-filter: blur(28px) saturate(210%) !important;
      -webkit-backdrop-filter: blur(28px) saturate(210%) !important;
      border: 1px solid rgba(255, 255, 255, 0.18) !important;
      box-shadow: 0 30px 60px rgba(0, 0, 0, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.25) !important;
    }

    .app-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      padding-bottom: 12px;
    }

    .app-header h2 {
      margin: 0;
      font-size: 22px;
      color: #1db954;
    }

    /* CARD PANELS */
    .card-panel {
      background: rgba(0, 0, 0, 0.3);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 20px;
      padding: 22px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .card-panel h3 {
      margin: 0;
      font-size: 15px;
      color: #1db954;
      text-transform: uppercase;
    }

    /* INPUTS & BUTTONS */
    input[type="text"], input[type="password"], select {
      width: 100%;
      padding: 12px 16px;
      background: rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 12px;
      color: #ffffff;
      outline: none;
    }

    input[type="range"] {
      -webkit-appearance: none;
      width: 100%;
      height: 6px;
      border-radius: 3px;
      background: rgba(255, 255, 255, 0.15);
      outline: none;
    }

    input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 18px;
      height: 18px;
      border-radius: 50%;
      background: #1db954;
      cursor: pointer;
    }

    .btn {
      padding: 12px 18px;
      border: none;
      border-radius: 12px;
      font-weight: 600;
      font-size: 14px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn:hover { transform: translateY(-2px); filter: brightness(1.15); }
    .btn:active { transform: translateY(1px) scale(0.98); }

    .btn-primary { background: #1db954; color: #000; }
    .btn-secondary { background: rgba(255, 255, 255, 0.1); color: #fff; }
    .btn-success { background: #22c55e; color: #000; }
    .btn-warning { background: #f59e0b; color: #000; }
    .btn-dark { background: #27272a; color: #fff; border: 1px solid rgba(255, 255, 255, 0.1); }

    .btn-group, .action-bar {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    /* =========================================================
       2. MODAL OVERLAYS (THIS FIXES ALL UIS SHOWING AT ONCE!)
       ========================================================= */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 9999;
      
      /* HIDE POPUPS BY DEFAULT */
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.3s ease;
    }

    /* ACTIVE MODAL STATE */
    .modal-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }

    .modal-content {
      width: 500px;
      max-width: 90vw;
      background: #18181b;
      border: 1px solid rgba(255, 255, 255, 0.2);
      border-radius: 24px;
      padding: 28px;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
      transform: scale(0.9);
      transition: transform 0.3s ease;
    }

    .modal-overlay.active .modal-content {
      transform: scale(1);
    }

    /* RESPONSIVE MOBILE BREAKPOINTS */
    @media screen and (max-width: 1023px) {
      .pc-only-settings { display: none !important; }
    }
  </style>
</head>
<body>

  <!-- =========================================================
       MAIN UI WINDOW (ALWAYS VISIBLE)
     ========================================================= -->
  <div class="voizz-box">
    
    <header class="app-header">
      <h2>🎙️ VoicePea Changer</h2>
    </header>

    <main class="card-panel">
      
      <div style="text-align: center; padding: 10px; background: #fff; color: #000; border-radius: 12px; font-weight: bold; font-size: 14px; cursor: pointer;">
        Sign in with Google
      </div>

      <input type="text" placeholder="Type text to speak, or press the mic">

      <div>
        <label style="font-size: 12px; color: #aaa;">Select Engine Voice Target:</label>
        <select>
          <option>Custom Voice 1 (Custom)</option>
          <option>Cyber Pitch Alpha</option>
          <option>Deep Robotic Low</option>
        </select>
      </div>

      <!-- PC ONLY SETTINGS -->
      <div class="pc-only-settings" style="display: flex; flex-direction: column; gap: 12px;">
        <div>
          <label style="font-size: 12px; color: #aaa;">Playback Rate / Speed:</label>
          <input type="range" min="0.5" max="2.0" step="0.1" value="1.0">
        </div>
        <div>
          <label style="font-size: 12px; color: #aaa;">DSP Waveshaper Distortion:</label>
          <input type="range" min="0.0" max="1.0" step="0.05" value="0.2">
        </div>
        <div>
          <label style="font-size: 12px; color: #aaa;">Chunk Time-Inversion (Reverse):</label>
          <input type="range" min="0.0" max="1.0" step="0.05" value="0.0">
        </div>
      </div>

      <!-- MAIN ACTION BUTTONS -->
      <div class="action-bar">
        <button class="btn btn-dark">▶ Speak</button>
        <button class="btn btn-dark">⏹ Stop</button>
        <button class="btn btn-dark">🔄 Loop</button>
        <button class="btn btn-warning" id="openCustomVoiceBtn">🎨 Custom Voice</button>
      </div>

      <div style="font-size: 13px; text-align: center; margin-top: 5px;">
        Nor-Tec Streaming: <strong style="color: #e91429;">OFFLINE</strong>
      </div>

    </main>

  </div>


  <!-- =========================================================
       MODAL 1: RECORD CUSTOM VOICE SAMPLE (HIDDEN BY DEFAULT)
     ========================================================= -->
  <div class="modal-overlay" id="customVoiceModal">
    <div class="modal-content card-panel">
      <h3>🎙️ Record Custom Voice Sample</h3>
      <p style="font-size: 13px; color: #ccc; margin: 0;">
        Record a 10-second sample of your voice. VoicePea will capture raw PCM buffers to synthesize your profile into the voice selector.
      </p>

      <div>
        <label style="font-size: 12px; color: #aaa;">Voice Profile Label:</label>
        <input type="text" value="Cyber Pitch Alpha">
      </div>

      <blockquote style="font-style: italic; font-size: 13px; color: #aaa; border-left: 3px solid #1db954; margin: 0; padding-left: 10px;">
        "Safehost VoicePea changer streams high-definition real-time digital audio."
      </blockquote>

      <div style="font-size: 24px; font-weight: bold; text-align: center; color: #1db954;">
        10.0s
      </div>

      <div class="btn-group">
        <button class="btn btn-success" style="flex: 1;">🔴 Start 10s Recording</button>
        <button class="btn btn-secondary" id="closeCustomVoiceBtn">Cancel</button>
      </div>
    </div>
  </div>


  <!-- =========================================================
       MODAL 2: HARDWARE ACCESS (HIDDEN BY DEFAULT)
     ========================================================= -->
  <div class="modal-overlay" id="hardwareModal">
    <div class="modal-content card-panel">
      <h3>🎙️ Hardware Access</h3>
      <p style="font-size: 13px; color: #ccc; margin: 0;">
        VoicePea Changer needs access to your hardware microphone to process real-time voice distortion, capture speech, and clone custom pitch profiles.
      </p>
      <div style="color: #aaa; font-size: 13px;">Detecting hardware devices...</div>
      <div class="btn-group">
        <button class="btn btn-secondary" id="closeHardwareBtn">Deny</button>
        <button class="btn btn-primary">Grant Mic Access</button>
      </div>
    </div>
  </div>


  <!-- JAVASCRIPT CONTROLLER TO SHOW/HIDE MODALS -->
  <script>
    const customModal = document.getElementById('customVoiceModal');
    const openCustomBtn = document.getElementById('openCustomVoiceBtn');
    const closeCustomBtn = document.getElementById('closeCustomVoiceBtn');

    // Open Custom Voice Modal when clicking "🎨 Custom Voice"
    openCustomBtn.addEventListener('click', () => {
      customModal.classList.add('active');
    });

    // Close Custom Voice Modal when clicking "Cancel"
    closeCustomBtn.addEventListener('click', () => {
      customModal.classList.remove('active');
    });
  </script>

  <script src="app.js"></script>
</body>
</html>
