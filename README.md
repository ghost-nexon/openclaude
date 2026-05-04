<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>OpenClaude Android • Ollama Edition</title>
  <meta name="description" content="Run an autonomous, hardware-aware AI agent directly on your Android device with Ollama and full God-Mode control."/>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg-primary: #0f0f11;
      --bg-secondary: #18181b;
      --bg-tertiary: #27272a;
      --text-primary: #f4f4f5;
      --text-secondary: #a1a1aa;
      --accent: #8b5cf6;
      --accent-hover: #7c3aed;
      --success: #22c55e;
      --warning: #f59e0b;
      --border: #3f3f46;
      --shadow: 0 10px 40px -10px rgba(0,0,0,0.5);
      --radius: 16px;
      --radius-sm: 12px;
      --radius-xs: 8px;
      --transition: all 0.2s ease;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      background: var(--bg-primary);
      color: var(--text-primary);
      line-height: 1.6;
      overflow-x: hidden;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 24px;
    }

    /* Header */
    header {
      padding: 24px 0;
      position: sticky;
      top: 0;      background: rgba(15, 15, 17, 0.9);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      z-index: 100;
    }

    .header-content {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 700;
      font-size: 1.25rem;
      color: var(--text-primary);
      text-decoration: none;
    }

    .logo-icon {
      width: 36px;
      height: 36px;
      background: linear-gradient(135deg, var(--accent), #6366f1);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
    }

    .badges {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 6px 12px;
      background: var(--bg-tertiary);
      border: 1px solid var(--border);
      border-radius: 20px;
      font-size: 0.75rem;
      font-weight: 500;      color: var(--text-secondary);
      text-decoration: none;
      transition: var(--transition);
    }

    .badge:hover {
      border-color: var(--accent);
      color: var(--text-primary);
      transform: translateY(-1px);
    }

    .badge svg { width: 14px; height: 14px; }

    /* Hero */
    .hero {
      padding: 64px 0 40px;
      text-align: center;
    }

    .hero-image {
      width: 100%;
      max-width: 900px;
      margin: 0 auto 32px;
      border-radius: var(--radius);
      overflow: hidden;
      border: 1px solid var(--border);
      box-shadow: var(--shadow);
      background: var(--bg-secondary);
    }

    .hero-image img {
      width: 100%;
      height: auto;
      display: block;
    }

    .hero h1 {
      font-size: 2.5rem;
      font-weight: 700;
      margin-bottom: 16px;
      background: linear-gradient(135deg, #fff, #a5b4fc);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero p {
      font-size: 1.125rem;
      color: var(--text-secondary);
      max-width: 700px;      margin: 0 auto 24px;
    }

    .hero-description {
      background: linear-gradient(135deg, var(--accent), #6366f1);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      font-weight: 600;
    }

    /* Sections */
    section {
      padding: 48px 0;
      border-top: 1px solid var(--border);
    }

    section:first-of-type { border-top: none; }

    .section-title {
      font-size: 1.75rem;
      font-weight: 700;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .section-title svg {
      width: 28px;
      height: 28px;
      color: var(--accent);
    }

    .section-subtitle {
      color: var(--text-secondary);
      margin-bottom: 32px;
      font-size: 1.05rem;
    }

    /* Features Grid */
    .features-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 20px;
    }

    .feature-card {
      background: var(--bg-secondary);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);      padding: 24px;
      transition: var(--transition);
    }

    .feature-card:hover {
      border-color: var(--accent);
      transform: translateY(-2px);
      box-shadow: 0 8px 30px -8px rgba(139, 92, 246, 0.25);
    }

    .feature-icon {
      width: 48px;
      height: 48px;
      background: linear-gradient(135deg, rgba(139, 92, 246, 0.2), rgba(99, 102, 241, 0.2));
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 16px;
      color: var(--accent);
    }

    .feature-card h3 {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 8px;
    }

    .feature-card p {
      color: var(--text-secondary);
      font-size: 0.95rem;
    }

    /* Steps & Lists */
    .steps {
      display: grid;
      gap: 16px;
      margin-top: 24px;
    }

    .step {
      display: flex;
      gap: 16px;
      padding: 16px;
      background: var(--bg-secondary);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
    }

    .step-number {      min-width: 28px;
      height: 28px;
      background: var(--accent);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      font-size: 0.875rem;
      flex-shrink: 0;
    }

    .step-content h4 {
      font-weight: 600;
      margin-bottom: 4px;
    }

    .step-content a {
      color: var(--accent);
      text-decoration: none;
      font-weight: 500;
    }

    .step-content a:hover { text-decoration: underline; }

    /* Code Blocks */
    .code-block {
      background: var(--bg-secondary);
      border: 1px solid var(--border);
      border-radius: var(--radius-sm);
      margin: 20px 0;
      overflow: hidden;
    }

    .code-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 16px;
      background: var(--bg-tertiary);
      border-bottom: 1px solid var(--border);
      font-size: 0.85rem;
      color: var(--text-secondary);
    }

    .code-actions {
      display: flex;
      gap: 8px;
    }
    .copy-btn {
      display: flex;
      align-items: center;
      gap: 6px;
      padding: 6px 12px;
      background: var(--bg-primary);
      border: 1px solid var(--border);
      border-radius: 6px;
      color: var(--text-secondary);
      font-size: 0.8rem;
      cursor: pointer;
      transition: var(--transition);
    }

    .copy-btn:hover {
      border-color: var(--accent);
      color: var(--accent);
    }

    .copy-btn.copied {
      color: var(--success);
      border-color: var(--success);
    }

    .copy-btn svg { width: 14px; height: 14px; }

    .code-content {
      padding: 16px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.9rem;
      overflow-x: auto;
      color: #e4e4e7;
      background: var(--bg-primary);
    }

    .code-content code { white-space: pre; }

    .code-content .comment { color: #71717a; }
    .code-content .command { color: var(--accent); }
    .code-content .url { color: #60a5fa; }

    /* Usage Box */
    .usage-box {
      background: linear-gradient(135deg, rgba(139, 92, 246, 0.1), rgba(99, 102, 241, 0.1));
      border: 1px solid var(--accent);
      border-radius: var(--radius-sm);
      padding: 20px 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;      gap: 16px;
      margin-top: 16px;
    }

    .usage-command {
      font-family: 'JetBrains Mono', monospace;
      font-size: 1.25rem;
      font-weight: 600;
      color: var(--text-primary);
    }

    /* Disclaimer */
    .disclaimer {
      background: linear-gradient(135deg, rgba(245, 158, 11, 0.1), rgba(234, 88, 12, 0.1));
      border: 1px solid var(--warning);
      border-radius: var(--radius-sm);
      padding: 20px 24px;
      margin-top: 24px;
    }

    .disclaimer-title {
      display: flex;
      align-items: center;
      gap: 8px;
      font-weight: 600;
      color: var(--warning);
      margin-bottom: 8px;
    }

    .disclaimer p {
      color: var(--text-secondary);
      font-size: 0.95rem;
    }

    /* Footer */
    footer {
      padding: 40px 0;
      text-align: center;
      border-top: 1px solid var(--border);
      color: var(--text-secondary);
      font-size: 0.9rem;
    }

    footer a {
      color: var(--accent);
      text-decoration: none;
      font-weight: 500;
    }

    footer a:hover { text-decoration: underline; }
    .developer {
      margin-top: 12px;
      font-size: 0.95rem;
    }

    .developer strong { color: var(--text-primary); }

    /* Responsive */
    @media (max-width: 768px) {
      .hero h1 { font-size: 2rem; }
      .section-title { font-size: 1.5rem; }
      .header-content { flex-wrap: wrap; }
      .badges { width: 100%; justify-content: center; }
      .usage-box { flex-direction: column; text-align: center; }
    }

    /* Toast Notification */
    .toast {
      position: fixed;
      bottom: 24px;
      right: 24px;
      background: var(--bg-secondary);
      border: 1px solid var(--success);
      border-radius: var(--radius-xs);
      padding: 12px 20px;
      display: flex;
      align-items: center;
      gap: 10px;
      color: var(--text-primary);
      font-size: 0.9rem;
      box-shadow: var(--shadow);
      transform: translateY(100px);
      opacity: 0;
      transition: all 0.3s ease;
      z-index: 1000;
    }

    .toast.show {
      transform: translateY(0);
      opacity: 1;
    }

    .toast svg {
      width: 18px;
      height: 18px;
      color: var(--success);
      flex-shrink: 0;
    }
    /* Scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track { background: var(--bg-primary); }
    ::-webkit-scrollbar-thumb {
      background: var(--bg-tertiary);
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover { background: var(--border); }
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="container header-content">
      <a href="#" class="logo">
        <div class="logo-icon">🤖</div>
        <span>OpenClaude Android</span>
      </a>
      <div class="badges">
        <a href="https://opensource.org/licenses/MIT" class="badge" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
          License: MIT
        </a>
        <span class="badge">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="5" y="2" width="14" height="20" rx="2"/><path d="M12 18h.01"/></svg>
          Platform: Android
        </span>
        <span class="badge">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/></svg>
          Powered By: Ollama
        </span>
      </div>
    </div>
  </header>

  <!-- Hero -->
  <section class="hero">
    <div class="container">
      <div class="hero-image">
        <img src="https://github.com/user-attachments/assets/c447fce1-2eb5-4035-b9ad-b99b67603167" alt="OpenClaude Android Screenshot" loading="lazy"/>
      </div>
      <h1>📱 OpenClaude Android <span style="color:var(--accent)">(Ollama Edition)</span></h1>
      <p>
        Run an autonomous, hardware-aware AI agent directly on your Android device. 
        <span class="hero-description">This version is modified to run locally via Ollama with full "God-Mode" hardware control.</span>
      </p>
    </div>  </section>

  <!-- Features -->
  <section>
    <div class="container">
      <h2 class="section-title">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2v4M12 18v4M4.93 4.93l2.83 2.83M16.24 16.24l2.83 2.83M1 12h4M19 12h4M4.93 19.07l2.83-2.83M16.24 7.76l2.83-2.83"/></svg>
        ✨ Features
      </h2>
      <p class="section-subtitle">Powerful capabilities designed for autonomous Android control</p>
      
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="24" height="24"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>
          </div>
          <h3>Local LLM Support</h3>
          <p>Run high-performance models locally using <strong>Ollama</strong> — no cloud required, full privacy.</p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="24" height="24"><rect x="2" y="3" width="20" height="14" rx="2"/><path d="M8 21h8M12 17v4"/></svg>
          </div>
          <h3>Autonomous UI Control</h3>
          <p>The AI can "see" your screen and simulate taps, swipes, and typing using Shizuku and UIAutomator.</p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="24" height="24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          </div>
          <h3>Hardware Integration</h3>
          <p>Control WiFi, Battery, Camera, and Volume directly through the AI chat interface.</p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" width="24" height="24"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>
          </div>
          <h3>1-Click Setup</h3>
          <p>Fully automated Termux environment configuration — get started in minutes.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- Prerequisites -->
  <section>
    <div class="container">      <h2 class="section-title">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
        🛠 Prerequisites
      </h2>
      <p class="section-subtitle">To use the "God-Mode" hardware features, install the following:</p>
      
      <div class="steps">
        <div class="step">
          <div class="step-number">1</div>
          <div class="step-content">
            <h4>Termux</h4>
            <p>Install from <a href="https://f-droid.org/packages/com.termux/" target="_blank" rel="noopener">F-Droid</a> or GitHub. <strong>Do not use Play Store version.</strong></p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">2</div>
          <div class="step-content">
            <h4>Termux:API</h4>
            <p>Install from <a href="https://f-droid.org/en/packages/com.termux.api/" target="_blank" rel="noopener">F-Droid</a> to allow hardware sensor access.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">3</div>
          <div class="step-content">
            <h4>Ollama</h4>
            <p>Must be installed (<code>pkg install ollama</code>) and running (<code>ollama serve</code>) in a separate Termux tab.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">4</div>
          <div class="step-content">
            <h4>Shizuku <span style="color:var(--success)">(Recommended)</span></h4>
            <p>Required for autonomous UI interaction without root. Enables secure bypass of Android application sandbox. <a href="https://play.google.com/store/apps/details?id=moe.shizuku.privileged.api" target="_blank" rel="noopener" style="color:var(--accent);">Get it on Google Play</a></p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Shizuku Setup -->
  <section>
    <div class="container">
      <h2 class="section-title">⚙️ Shizuku Configuration</h2>
      <p class="section-subtitle">Required for system-level control without root access</p>
      
      <a href="https://play.google.com/store/apps/details?id=moe.shizuku.privileged.api" 
         target="_blank" 
         rel="noopener"
         style="display:inline-flex; align-items:center; gap:8px; padding:12px 20px; background:linear-gradient(135deg, #3DDC84, #28a745); color:#000; text-decoration:none; border-radius:8px; font-weight:600; margin:24px 0; transition:transform 0.2s; box-shadow:0 4px 14px rgba(61, 220, 132, 0.3);">
        <svg viewBox="0 0 24 24" fill="currentColor" width="20" height="20"><path d="M3,20.5V3.5C3,2.91 3.34,2.39 3.84,2.15L13.69,12L3.84,21.85C3.34,21.6 3,21.09 3,20.5M16.81,15.12L6.05,21.34L14.54,12.85L16.81,15.12M20.16,10.81C20.5,11.08 20.75,11.5 20.75,12C20.75,12.5 20.53,12.9 20.18,13.18L17.89,14.5L15.39,12L17.89,9.5L20.16,10.81M6.05,2.66L16.81,8.88L14.54,11.15L6.05,2.66Z" /></svg>        Get Shizuku on Google Play
      </a>
      
      <div class="steps">
        <div class="step">
          <div class="step-number">1</div>
          <div class="step-content">
            <h4>Install Shizuku</h4>
            <p>Download from the <a href="https://play.google.com/store/apps/details?id=moe.shizuku.privileged.api" target="_blank" rel="noopener" style="color:var(--accent); text-decoration:underline;">Google Play Store</a>.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">2</div>
          <div class="step-content">
            <h4>Enable Developer Options</h4>
            <p>Tap "Build Number" 7 times under <strong>Settings > About Phone</strong>.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">3</div>
          <div class="step-content">
            <h4>Enable Wireless Debugging</h4>
            <p>Inside Developer Options, toggle on <strong>Wireless Debugging</strong>.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">4</div>
          <div class="step-content">
            <h4>Pair & Authorize</h4>
            <p>Open Shizuku → <strong>Pairing</strong> → follow instructions using Android pairing code.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-number">5</div>
          <div class="step-content">
            <h4>Start Service</h4>
            <p>Tap <strong>Start</strong> to initiate the background service.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Ollama Installation -->
  <section>
    <div class="container">
      <h2 class="section-title">🦙 Ollama Installation</h2>
      <p class="section-subtitle">Install and run Ollama in Termux</p>
      
      <div class="code-block">        <div class="code-header">
          <span>termux • ollama setup</span>
          <div class="code-actions">
            <button class="copy-btn" data-clipboard="termux-setup-storage&#10;pkg instal1. Install **Shizuku** from the .[Google Play Store](https://play.google.com/store/apps/details?id=moe.shizuku.privileged.api)
2. Enable **Developer Options** on your Android device (tap "Build Number" 7 times under Settings > About Phone).
3. Inside Developer Options, enable **Wireless Debugging**.
4. Open the Shizuku application, select **Pairing**, and follow the on-screen instructions to authorize the service using an Android pairing code.
5. Tap **Start** to initiate the background service.


## Ollama Installation
Open **Termux** and paste the following command. This will install and run the ollama on your phone
```
termux-setup-storage
pkg install ollama
ollama serve
```
## 🚀 One-Line Installation (Leaked ClaudeCode)

Open **Termux** and paste the following command. This will update your system, download the setup script, and configure everything automatically:

```
pkg update -y && pkg upgrade -y && pkg install curl -y && curl -sL https://raw.githubusercontent.com/ghost-nexon/openclaude/main/install.sh -o ~/install.sh && chmod +x ~/install.sh && bash ~/install.sh
```
## ⚙️ How to Use
```
claude
```
## ⚖️ Disclaimer
This project is for educational and research purposes only. Use "Limitless Mode" with caution as it allows the AI to execute commands on your device autonomously.

Developed by - **ghost-nexon**

