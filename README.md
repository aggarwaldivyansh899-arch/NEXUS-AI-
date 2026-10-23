# NEXUS-AI-
**NEXUS AI** is a single-file, serverless web chatbot powered by Google's Gemini API. Styled in a purple-and-white glassmorphic interface, it features Markdown rendering, local memory, voice interaction, dark mode, prompt chips, and Hinglish support—running instantly inside any browser.
[index.html](https://github.com/user-attachments/files/33877890/index.html)

<!DOCTYPE html>
<html lang="en">
<head>
<!-- ===== STEP 1: PASTE YOUR API KEY BETWEEN THE QUOTES ON LINE 6 ===== -->
<script>
const API_KEY = "AQ.Ab8RN6LIUg0Y77IUJeb6EuJvUDlVB1vI9uZcwXZoIvUBXaAUTw";
const MODEL = "gemini-3.5-flash-lite";
</script>

<script>
// ===== YOUR CHATBOT'S INSTRUCTIONS (RTCC) =====
const SYSTEM_PROMPT = `
ROLE: Act as a world-class team consisting of an AI systems architect specializing in Small Language Models, a senior HTML, CSS, and JavaScript developer, a futuristic interface designer, an AI orchestration expert, and a security-conscious engineer.
TASK: You are NEXUS AI: Adaptive Intelligence System. Build an assistant experience that chooses appropriate available models, tools, and workflows for different tasks. Be transparent about which capabilities are actually available.
CONTEXT: NEXUS AI is a beginner-friendly prototype designed to evolve into a sophisticated SLM application. Its first version prioritizes reliable core functionality.
CONSTRAINTS:
- Answer helpfully and accurately. Never invent tool results, internet access, file access, memory, model usage, analytics, or performance statistics.
- Explain limitations honestly.
- Use deterministic calculations when possible, and explain calculations clearly.
- Support coding, mathematics, document-related questions, research planning, summarization, and general conversation.
- The browser app has only the tools actually implemented in its JavaScript. Do not claim to have used a tool that was not used.
- Persistent chat storage is browser-local and is not equivalent to AI long-term memory.
- Never ask users to share passwords, API keys, or other secrets in chat.
- For development questions, prefer complete, practical, beginner-friendly instructions.
- If the user writes in Hindi or Hinglish, reply in the same language.
OUTPUT: Give useful, organized responses. Use Markdown when helpful. Explain uncertainty and unsupported capabilities instead of pretending.
`;
</script>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#6d28d9">
<title>NEXUS Ai — Adaptive Intelligence</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>
/* ===== 1. DESIGN SYSTEM ===== */
:root {
  color-scheme: light;
  --bg: #f7f5ff;
  --surface: #ffffff;
  --surface-2: #f1edff;
  --text: #24183c;
  --muted: #827895;
  --border: #e8e0fb;
  --purple: #7543e8;
  --purple-dark: #5427bd;
  --purple-soft: #ede5ff;
  --user-bubble: #7543e8;
  --user-text: #ffffff;
  --bot-bubble: #ffffff;
  --danger: #b42335;
  --danger-bg: #fff0f1;
  --shadow: 0 12px 35px rgba(72, 42, 130, .08);
}

:root[data-theme="dark"] {
  color-scheme: dark;
  --bg: #100c1b;
  --surface: #1a1428;
  --surface-2: #261b3c;
  --text: #f5f0ff;
  --muted: #b4a7ca;
  --border: #382950;
  --purple: #a78bfa;
  --purple-dark: #8b5cf6;
  --purple-soft: #302248;
  --user-bubble: #7444d8;
  --user-text: #ffffff;
  --bot-bubble: #1a1428;
  --danger: #ffb4bd;
  --danger-bg: #401e2b;
  --shadow: 0 12px 35px rgba(0, 0, 0, .2);
}

* { box-sizing: border-box; }

body {
  margin: 0;
  min-height: 100vh;
  background:
    radial-gradient(ellipse at 8% 0%, rgba(139,92,246,.10), transparent 34%),
    var(--bg);
  color: var(--text);
  font-family: "Poppins", sans-serif;
  transition: background .25s, color .25s;
}

button, textarea { font: inherit; }
button { cursor: pointer; }
button:focus-visible, textarea:focus-visible {
  outline: 3px solid var(--purple);
  outline-offset: 3px;
}

button:disabled { cursor: not-allowed; opacity: .55; }

.app {
  max-width: 1440px;
  margin: 0 auto;
  min-height: 100vh;
  padding: 20px;
  display: flex;
  flex-direction: column;
}

.topbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 14px 18px;
  border: 1px solid var(--border);
  border-radius: 20px;
  background: var(--surface);
  box-shadow: var(--shadow);
}

.brand { display: flex; align-items: center; gap: 12px; min-width: 0; }

.brand-logo {
  width: 46px;
  height: 46px;
  flex: 0 0 auto;
  border-radius: 15px;
  display: grid;
  place-items: center;
  color: #fff;
  background: linear-gradient(135deg, #a78bfa, #6d28d9 65%, #4c1d95);
  box-shadow: 0 0 25px rgba(117,67,232,.25);
}

.brand-logo svg { width: 29px; height: 29px; }

.brand-name { margin: 0; font-size: 20px; font-weight: 800; letter-spacing: -.7px; }
.brand-name span { color: var(--purple); }
.brand-sub { margin: 2px 0 0; font-size: 10px; letter-spacing: 1.5px; color: var(--muted); }

.header-actions { display: flex; gap: 8px; align-items: center; }

.icon-btn {
  width: 40px;
  height: 40px;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: var(--surface);
  color: var(--text);
  display: inline-grid;
  place-items: center;
  font-size: 17px;
  transition: transform .2s, background .2s;
}
.icon-btn:hover { background: var(--surface-2); transform: translateY(-1px); }
.icon-btn svg { width: 19px; height: 19px; }

.status-pill {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  font-size: 11px;
  color: var(--muted);
  padding: 8px 11px;
  border-radius: 999px;
  background: var(--surface-2);
}
.status-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #a78bfa;
  box-shadow: 0 0 9px rgba(167,139,250,.7);
}

.workspace {
  display: grid;
  grid-template-columns: 260px minmax(0, 1fr);
  gap: 20px;
  flex: 1;
  min-height: 0;
  margin-top: 20px;
}

.sidebar { display: flex; flex-direction: column; gap: 16px; }

.panel {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 18px;
  box-shadow: var(--shadow);
}

.panel-title {
  margin: 0 0 14px;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.4px;
  color: var(--muted);
}

.core-wrap { display: grid; justify-items: center; padding: 5px 0 12px; }

.core {
  width: 116px;
  height: 116px;
  position: relative;
  display: grid;
  place-items: center;
  border-radius: 50%;
  background: radial-gradient(circle, #c4b5fd 0%, #8b5cf6 24%, #5427bd 58%, #211239 75%);
  box-shadow: 0 0 25px rgba(139,92,246,.35), inset 0 0 20px rgba(255,255,255,.2);
  animation: float 5s ease-in-out infinite;
}
.core::before, .core::after {
  content: "";
  position: absolute;
  inset: -9px;
  border: 1px solid rgba(139,92,246,.5);
  border-radius: 50%;
  animation: orbit 9s linear infinite;
}
.core::after { inset: -17px; border-color: rgba(167,139,250,.22); animation-direction: reverse; animation-duration: 13s; }
.core svg { width: 48px; height: 48px; color: #fff; filter: drop-shadow(0 0 8px #fff); }

.core-label { text-align: center; font-size: 12px; font-weight: 600; }
.core-caption { text-align: center; color: var(--muted); font-size: 10px; margin-top: 4px; }

@keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-5px); } }
@keyframes orbit { to { transform: rotate(360deg); } }

.activity-row {
  display: flex;
  justify-content: space-between;
  gap: 8px;
  padding: 10px 0;
  border-bottom: 1px solid var(--border);
  font-size: 11px;
}
.activity-row:last-child { border-bottom: 0; padding-bottom: 0; }
.activity-row span { color: var(--muted); }
.activity-row strong { text-align: right; font-weight: 600; overflow-wrap: anywhere; }
.activity-value { color: var(--purple); }

.mini-note { margin: 12px 0 0; color: var(--muted); font-size: 10px; line-height: 1.7; }

.chat-panel {
  min-width: 0;
  min-height: 650px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 22px;
  background: var(--surface);
  box-shadow: var(--shadow);
}

.chat-head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 18px 22px;
  border-bottom: 1px solid var(--border);
}
.chat-head h2 { margin: 0; font-size: 15px; }
.chat-head p { margin: 3px 0 0; font-size: 11px; color: var(--muted); }

.messages {
  flex: 1;
  min-height: 350px;
  max-height: calc(100vh - 310px);
  overflow-y: auto;
  padding: 24px clamp(14px, 4vw, 38px);
  scroll-behavior: smooth;
}

.welcome {
  text-align: center;
  padding: 12px 10px 25px;
}
.welcome-mark {
  width: 62px;
  height: 62px;
  margin: 0 auto 15px;
  border-radius: 21px;
  display: grid;
  place-items: center;
  background: var(--purple-soft);
  color: var(--purple);
  font-size: 28px;
}
.welcome h2 { margin: 0; font-size: clamp(22px, 3vw, 30px); letter-spacing: -1px; }
.welcome h2 span { color: var(--purple); }
.welcome p { max-width: 500px; margin: 9px auto 18px; font-size: 12px; line-height: 1.8; color: var(--muted); }

.chips { display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; }
.chip {
  border: 1px solid var(--border);
  background: var(--surface);
  color: var(--text);
  padding: 9px 12px;
  border-radius: 12px;
  font-size: 11px;
  transition: .2s;
}
.chip:hover { background: var(--purple-soft); border-color: var(--purple); }

.message {
  display: flex;
  gap: 10px;
  align-items: flex-start;
  margin: 0 0 22px;
  animation: appear .22s ease-out;
}
.message.user { flex-direction: row-reverse; }

@keyframes appear { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

.avatar {
  flex: 0 0 34px;
  width: 34px;
  height: 34px;
  display: grid;
  place-items: center;
  border-radius: 12px;
  background: var(--purple-soft);
  font-size: 17px;
}
.message.user .avatar { background: var(--user-bubble); }

.message-content { max-width: min(82%, 760px); min-width: 0; }
.message.user .message-content { display: flex; flex-direction: column; align-items: flex-end; }

.message-name { font-size: 10px; color: var(--muted); margin: 0 4px 5px; }

.bubble {
  padding: 12px 15px;
  border: 1px solid var(--border);
  border-radius: 5px 17px 17px 17px;
  background: var(--bot-bubble);
  font-size: 12px;
  line-height: 1.85;
  overflow-wrap: anywhere;
  box-shadow: 0 3px 12px rgba(65,40,100,.035);
}
.message.user .bubble {
  color: var(--user-text);
  background: var(--user-bubble);
  border-color: transparent;
  border-radius: 17px 5px 17px 17px;
}
.bubble.error {
  background: var(--danger-bg);
  color: var(--danger);
  border-color: var(--danger);
}

.bubble p { margin: 0 0 10px; }
.bubble p:last-child { margin-bottom: 0; }
.bubble ul, .bubble ol { padding-left: 22px; margin: 7px 0 12px; }
.bubble li { margin: 3px 0; }
.bubble h1, .bubble h2, .bubble h3 { font-size: 1.15em; margin: 14px 0 7px; }
.bubble blockquote { border-left: 3px solid var(--purple); margin: 8px 0; padding-left: 12px; color: var(--muted); }
.bubble code {
  font-family: Consolas, "Courier New", monospace;
  background: var(--purple-soft);
  padding: 2px 5px;
  border-radius: 5px;
  font-size: .95em;
}
.bubble pre {
  position: relative;
  overflow: auto;
  padding: 13px;
  margin: 10px 0;
  background: #171322;
  color: #f3edff;
  border-radius: 11px;
  font-size: 11px;
  line-height: 1.7;
}
.bubble pre code { padding: 0; background: transparent; color: inherit; white-space: pre; }
.bubble a { color: var(--purple); text-decoration: underline; }

.message-tools { display: flex; gap: 5px; margin: 6px 2px 0; }
.tool-btn {
  background: transparent;
  border: 1px solid var(--border);
  border-radius: 8px;
  color: var(--muted);
  font-size: 10px;
  padding: 5px 8px;
}
.tool-btn:hover { background: var(--purple-soft); color: var(--purple); }

.typing { display: flex; align-items: center; gap: 5px; padding: 4px 0; }
.typing span {
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--purple);
  animation: bounce 1s infinite ease-in-out;
}
.typing span:nth-child(2) { animation-delay: .15s; }
.typing span:nth-child(3) { animation-delay: .3s; }
@keyframes bounce { 0%,60%,100% { transform: translateY(0); opacity: .55; } 30% { transform: translateY(-5px); opacity: 1; } }

.composer-wrap { border-top: 1px solid var(--border); padding: 15px 20px 12px; }
.composer {
  display: flex;
  align-items: flex-end;
  gap: 9px;
  padding: 9px;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 17px;
}
#messageInput {
  flex: 1;
  width: 100%;
  min-width: 0;
  max-height: 180px;
  resize: none;
  padding: 8px 6px;
  border: 0;
  outline: 0;
  color: var(--text);
  background: transparent;
  font-size: 12px;
  line-height: 1.7;
}
#messageInput::placeholder { color: var(--muted); }
#messageInput:focus-visible { outline: 0; }
.send-btn {
  width: 42px; height: 42px; flex: 0 0 auto;
  display: grid; place-items: center;
  color: white;
  background: linear-gradient(135deg, #8b5cf6, #6d28d9);
  border: 0; border-radius: 13px;
  box-shadow: 0 5px 14px rgba(109,40,217,.2);
}
.send-btn svg { width: 20px; height: 20px; }
.send-btn:hover:not(:disabled) { filter: brightness(1.08); transform: translateY(-1px); }
.composer-hint { display: flex; justify-content: space-between; gap: 10px; margin: 9px 3px 0; color: var(--muted); font-size: 9px; }
.footer { text-align: center; color: var(--muted); font-size: 10px; padding: 13px 0 3px; }

.toast {
  position: fixed; left: 50%; bottom: 25px; z-index: 10;
  transform: translate(-50%, 20px);
  opacity: 0; pointer-events: none;
  padding: 11px 16px;
  border-radius: 12px;
  background: #25163c; color: #fff;
  box-shadow: var(--shadow);
  font-size: 11px;
  transition: .25s;
}
.toast.show { opacity: 1; transform: translate(-50%, 0); }

@media (max-width: 850px) {
  .workspace { grid-template-columns: 1fr; }
  .sidebar { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .sidebar .panel:first-child { grid-row: span 2; }
  .chat-panel { min-height: 600px; }
  .messages { max-height: 65vh; }
}
@media (max-width: 540px) {
  .app { padding: 9px; }
  .topbar { padding: 11px; border-radius: 16px; }
  .brand-logo { width: 39px; height: 39px; border-radius: 12px; }
  .brand-name { font-size: 17px; }
  .brand-sub { font-size: 8px; letter-spacing: .8px; }
  .header-actions { gap: 5px; }
  .icon-btn { width: 35px; height: 35px; border-radius: 10px; }
  .status-pill { display: none; }
  .workspace { margin-top: 10px; gap: 10px; }
  .sidebar { display: none; }
  .chat-panel { min-height: calc(100vh - 130px); border-radius: 17px; }
  .chat-head { padding: 14px; }
  .messages { padding: 18px 12px; min-height: 330px; }
  .message-content { max-width: 88%; }
  .composer-wrap { padding: 10px; }
  .composer-hint { font-size: 8px; }
}
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: .01ms !important;
    animation-iteration-count: 1 !important;
    scroll-behavior: auto !important;
    transition-duration: .01ms !important;
  }
}
</style>
</head>

<body>
<div class="app">
  <!-- ===== 2. HEADER ===== -->
  <header class="topbar">
    <div class="brand">
      <div class="brand-logo" aria-hidden="true">
        <svg viewBox="0 0 32 32" fill="none">
          <circle cx="16" cy="16" r="12" stroke="currentColor" stroke-width="1.4" opacity=".65"/>
          <ellipse cx="16" cy="16" rx="5" ry="12" stroke="currentColor" stroke-width="1.4"/>
          <ellipse cx="16" cy="16" rx="12" ry="5" stroke="currentColor" stroke-width="1.4" transform="rotate(-35 16 16)"/>
          <circle cx="16" cy="16" r="2.5" fill="white"/>
        </svg>
      </div>
      <div>
        <h1 class="brand-name">NEXUS <span>Ai</span></h1>
        <p class="brand-sub">ADAPTIVE INTELLIGENCE SYSTEM</p>
      </div>
    </div>
    <div class="header-actions">
      <span class="status-pill"><span class="status-dot"></span><span id="connectionLabel">Ready to connect</span></span>
      <button class="icon-btn" id="themeBtn" title="Switch appearance" aria-label="Switch appearance">☾</button>
      <button class="icon-btn" id="clearBtn" title="Clear chat" aria-label="Clear chat">⌫</button>
    </div>
  </header>

  <!-- ===== 3. MAIN WORKSPACE ===== -->
  <main class="workspace">
    <aside class="sidebar" aria-label="AI information">
      <section class="panel">
        <h2 class="panel-title">Neural interface</h2>
        <div class="core-wrap">
          <div class="core" aria-hidden="true">
            <svg viewBox="0 0 48 48" fill="none">
              <circle cx="24" cy="24" r="15" stroke="white" stroke-width="1.2" opacity=".8"/>
              <ellipse cx="24" cy="24" rx="6" ry="15" stroke="white" stroke-width="1.2"/>
              <ellipse cx="24" cy="24" rx="15" ry="6" stroke="white" stroke-width="1.2" transform="rotate(45 24 24)"/>
              <circle cx="24" cy="24" r="3" fill="white"/>
            </svg>
          </div>
        </div>
        <div class="core-label">NEXUS Core</div>
        <div class="core-caption">Adaptive interface online</div>
        <p class="mini-note">The animated core is a visual interface. It does not represent hidden AI activity or live neural measurements.</p>
      </section>

      <section class="panel">
        <h2 class="panel-title">Activity monitor</h2>
        <div class="activity-row"><span>State</span><strong class="activity-value" id="activityState">Ready</strong></div>
        <div class="activity-row"><span>Task type</span><strong id="taskType">Awaiting input</strong></div>
        <div class="activity-row"><span>Provider</span><strong>Google Gemini API</strong></div>
        <div class="activity-row"><span>Selected model</span><strong id="modelName">Configured model</strong></div>
        <div class="activity-row"><span>Last latency</span><strong id="latencyValue">Not measured</strong></div>
        <div class="activity-row"><span>Processing</span><strong>Remote API</strong></div>
        <p class="mini-note">Latency is measured locally around API requests. Token counts and cost are not available in this prototype.</p>
      </section>

      <section class="panel">
        <h2 class="panel-title">Workspace status</h2>
        <div class="activity-row"><span>Chat storage</span><strong>Browser local</strong></div>
        <div class="activity-row"><span>Voice input</span><strong id="voiceStatus">Checking…</strong></div>
        <div class="activity-row"><span>Calculator</span><strong>Local tool</strong></div>
        <p class="mini-note">Chat history stays in this browser until you clear it. Avoid saving secrets in messages.</p>
      </section>
    </aside>

    <section class="chat-panel" aria-label="NEXUS chat">
      <div class="chat-head">
        <div>
          <h2>Intelligence workspace</h2>
          <p>Your ideas, connected.</p>
        </div>
        <button class="icon-btn" id="newChatBtn" aria-label="Start a new conversation" title="New conversation">＋</button>
      </div>

      <div class="messages" id="messages" aria-live="polite" aria-relevant="additions text">
        <div class="welcome" id="welcome">
          <div class="welcome-mark" aria-hidden="true">✦</div>
          <h2>Think beyond <span>limits.</span></h2>
          <p>Welcome to NEXUS Ai. Ask a question, explore an idea, or build something extraordinary. Your next breakthrough starts here.</p>
          <div class="chips">
            <button class="chip" data-prompt="Explain small language models in simple terms.">🧠 Explain SLMs</button>
            <button class="chip" data-prompt="Help me build a futuristic AI chatbot website.">💻 Build an AI app</button>
            <button class="chip" data-prompt="Create a practical study plan for learning AI.">🚀 Learn AI</button>
          </div>
        </div>
      </div>

      <div class="composer-wrap">
        <form class="composer" id="chatForm">
          <button type="button" class="icon-btn" id="micBtn" title="Speak to type" aria-label="Start voice input" hidden>🎙</button>
          <textarea id="messageInput" rows="1" maxlength="12000" placeholder="Ask NEXUS anything…" aria-label="Your message"></textarea>
          <button type="submit" class="send-btn" id="sendBtn" aria-label="Send message" title="Send message">
            <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
              <path d="M5 12L19 5L15 19L11.5 13L5 12Z" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round"/>
              <path d="M11.5 13L19 5" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
            </svg>
          </button>
        </form>
        <div class="composer-hint">
          <span>Enter to send · Shift + Enter for a new line</span>
          <span id="charCount">0 / 12000</span>
        </div>
      </div>
    </section>
  </main>

  <footer class="footer">NEXUS Ai · One interface. Adaptive intelligence. Unlimited possibilities.</footer>
</div>
<div class="toast" id="toast" role="status" aria-live="polite"></div>

<script>
// ===== 4. ELEMENTS AND APP STATE =====
"use strict";

const $ = (selector) => document.querySelector(selector);
const messagesEl = $("#messages");
const welcomeEl = $("#welcome");
const inputEl = $("#messageInput");
const sendBtn = $("#sendBtn");
const formEl = $("#chatForm");
const toastEl = $("#toast");

const STORAGE_KEY = "nexus_ai_chat_v1";
const THEME_KEY = "nexus_ai_theme_v1";
const MAX_MESSAGES = 100;

let history = [];
let isWaiting = false;
let typingEl = null;
let toastTimer = null;
let activeController = null;
let recognition = null;

// ===== 5. SAFE STORAGE =====
function readSavedHistory() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return [];
    const saved = JSON.parse(raw);
    if (!Array.isArray(saved)) return [];
    return saved
      .filter(m =>
        m &&
        (m.role === "user" || m.role === "assistant") &&
        typeof m.text === "string"
      )
      .slice(-MAX_MESSAGES)
      .map(m => ({ role: m.role, text: m.text }));
  } catch (error) {
    console.warn("Chat history could not be loaded.", error);
    return [];
  }
}

function saveHistory() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(history.slice(-MAX_MESSAGES)));
  } catch (error) {
    showToast("Browser storage is unavailable or full.");
    console.warn("Chat history could not be saved.", error);
  }
}

// ===== 6. BASIC SAFE MARKDOWN =====
// Escape all HTML before applying a small Markdown subset.
// Model output is never inserted as raw HTML.
function escapeHTML(value) {
  return String(value)
    .replace(/&/g, "&amp;")
    .replace(/</g, "&lt;")
    .replace(/>/g, "&gt;")
    .replace(/"/g, "&quot;")
    .replace(/'/g, "&#39;");
}

function safeHref(value) {
  try {
    const url = new URL(value);
    if (url.protocol === "https:" || url.protocol === "http:") {
      return escapeHTML(url.href);
    }
  } catch (_) {}
  return "";
}

function renderInline(text) {
  let s = escapeHTML(text);

  // Inline code first, so Markdown inside code is not interpreted.
  const codeParts = [];
  s = s.replace(/`([^`\n]+)`/g, (_, code) => {
    const token = "NEXUSCODE" + codeParts.length + "TOKEN";
    codeParts.push("<code>" + code + "</code>");
    return token;
  });

  s = s.replace(/\*\*(.+?)\*\*/g, "<strong>$1</strong>");
  s = s.replace(/(^|[^*])\*([^*\n]+)\*/g, "$1<em>$2</em>");

  // Make plain HTTP(S) links clickable without accepting other protocols.
  s = s.replace(/https?:\/\/[^\s<]+/g, (candidate) => {
    const trailing = candidate.match(/[.,!?;:)]+$/);
    const urlText = trailing ? candidate.slice(0, -trailing[0].length) : candidate;
    const href = safeHref(urlText);
    if (!href) return candidate;
    return '<a href="' + href + '" target="_blank" rel="noopener noreferrer">' +
      urlText + "</a>" + (trailing ? trailing[0] : "");
  });

  s = s.replace(/NEXUSCODE(\d+)TOKEN/g, (_, index) => codeParts[Number(index)] || "");
  return s;
}

function renderMarkdown(text) {
  const source = String(text).replace(/\r\n?/g, "\n");
  const lines = source.split("\n");
  const out = [];
  let paragraph = [];
  let listType = null;
  let listItems = [];
  let inCode = false;
  let codeLines = [];
  let codeLanguage = "";

  function flushParagraph() {
    if (paragraph.length) {
      out.push("<p>" + paragraph.map(renderInline).join("<br>") + "</p>");
      paragraph = [];
    }
  }
  function flushList() {
    if (!listType) return;
    const tag = listType === "ol" ? "ol" : "ul";
    out.push("<" + tag + ">" + listItems.map(item => "<li>" + renderInline(item) + "</li>").join("") + "</" + tag + ">");
    listType = null;
    listItems = [];
  }

  for (const line of lines) {
    if (line.startsWith("```")) {
      flushParagraph();
      flushList();
      if (!inCode) {
        inCode = true;
        codeLanguage = line.slice(3).trim();
        codeLines = [];
      } else {
        const safeCode = escapeHTML(codeLines.join("\n"));
        const languageLabel = codeLanguage ? ' data-language="' + escapeHTML(codeLanguage.slice(0, 30)) + '"' : "";
        out.push("<pre" + languageLabel + "><code>" + safeCode + "</code></pre>");
        inCode = false;
        codeLanguage = "";
      }
      continue;
    }

    if (inCode) {
      codeLines.push(line);
      continue;
    }

    if (!line.trim()) {
      flushParagraph();
      flushList();
      continue;
    }

    const heading = line.match(/^(#{1,3})\s+(.+)$/);
    if (heading) {
      flushParagraph();
      flushList();
      const level = heading[1].length;
      out.push("<h" + level + ">" + renderInline(heading[2]) + "</h" + level + ">");
      continue;
    }

    const quote = line.match(/^>\s?(.*)$/);
    if (quote) {
      flushParagraph();
      flushList();
      out.push("<blockquote>" + renderInline(quote[1]) + "</blockquote>");
      continue;
    }

    const bullet = line.match(/^\s*[-*+]\s+(.+)$/);
    const numbered = line.match(/^\s*\d+[.)]\s+(.+)$/);
    if (bullet || numbered) {
      flushParagraph();
      const newType = numbered ? "ol" : "ul";
      if (listType && listType !== newType) flushList();
      if (!listType) listType = newType;
      listItems.push((bullet || numbered)[1]);
      continue;
    }

    flushList();
    paragraph.push(line);
  }

  if (inCode) {
    out.push("<pre><code>" + escapeHTML(codeLines.join("\n")) + "</code></pre>");
  }
  flushParagraph();
  flushList();
  return out.join("") || "<p></p>";
}

// ===== 7. CHAT RENDERING =====
function scrollToBottom() {
  messagesEl.scrollTop = messagesEl.scrollHeight;
}

function hideWelcome() {
  if (welcomeEl && welcomeEl.parentNode) welcomeEl.remove();
}

function addMessage(role, text, options = {}) {
  hideWelcome();

  const message = document.createElement("article");
  message.className = "message " + (role === "user" ? "user" : "assistant");

  const avatar = document.createElement("div");
  avatar.className = "avatar";
  avatar.setAttribute("aria-hidden", "true");
  avatar.textContent = role === "user" ? "🙂" : "✦";

  const content = document.createElement("div");
  content.className = "message-content";

  const name = document.createElement("div");
  name.className = "message-name";
  name.textContent = role === "user" ? "You" : "NEXUS Ai";

  const bubble = document.createElement("div");
  bubble.className = "bubble";
  if (options.error) bubble.classList.add("error");
  bubble.innerHTML = renderMarkdown(text);

  content.append(name, bubble);

  if (role === "assistant" && !options.typing) {
    const tools = document.createElement("div");
    tools.className = "message-tools";

    const copyBtn = document.createElement("button");
    copyBtn.className = "tool-btn";
    copyBtn.type = "button";
    copyBtn.textContent = "▣ Copy";
    copyBtn.setAttribute("aria-label", "Copy AI response");
    copyBtn.addEventListener("click", async () => {
      try {
        await copyText(text);
        showToast("Response copied.");
      } catch (_) {
        showToast("Copy failed. Select and copy the text manually.");
      }
    });

    const speakBtn = document.createElement("button");
    speakBtn.className = "tool-btn";
    speakBtn.type = "button";
    speakBtn.textContent = "🔊 Read aloud";
    speakBtn.setAttribute("aria-label", "Read AI response aloud");
    speakBtn.addEventListener("click", () => speakText(text));

    tools.append(copyBtn, speakBtn);
    content.appendChild(tools);
  }

  message.append(avatar, content);
  messagesEl.appendChild(message);
  scrollToBottom();
  return message;
}

function showTyping() {
  hideWelcome();
  const message = document.createElement("article");
  message.className = "message";
  const avatar = document.createElement("div");
  avatar.className = "avatar";
  avatar.textContent = "✦";
  avatar.setAttribute("aria-hidden", "true");

  const content = document.createElement("div");
  content.className = "message-content";
  const name = document.createElement("div");
  name.className = "message-name";
  name.textContent = "NEXUS Ai is responding";

  const bubble = document.createElement("div");
  bubble.className = "bubble";
  bubble.innerHTML = '<div class="typing" aria-label="Generating response"><span></span><span></span><span></span></div>';
  content.append(name, bubble);
  message.append(avatar, content);
  messagesEl.appendChild(message);
  typingEl = message;
  scrollToBottom();
}

function hideTyping() {
  if (typingEl) typingEl.remove();
  typingEl = null;
}

function drawHistory() {
  messagesEl.innerHTML = "";
  welcomeEl = null;
  if (!history.length) {
    const welcome = document.createElement("div");
    welcome.className = "welcome";
    welcome.id = "welcome";
    welcome.innerHTML =
      '<div class="welcome-mark" aria-hidden="true">✦</div>' +
      '<h2>Think beyond <span>limits.</span></h2>' +
      '<p>Welcome to NEXUS Ai. Ask a question, explore an idea, or build something extraordinary. Your next breakthrough starts here.</p>' +
      '<div class="chips">' +
      '<button class="chip" data-prompt="Explain small language models in simple terms.">🧠 Explain SLMs</button>' +
      '<button class="chip" data-prompt="Help me build a futuristic AI chatbot website.">💻 Build an AI app</button>' +
      '<button class="chip" data-prompt="Create a practical study plan for learning AI.">🚀 Learn AI</button>' +
      '</div>';
    messagesEl.appendChild(welcome);
    welcomeEl = welcome;
    return;
  }
  history.forEach(item => addMessage(item.role, item.text));
  scrollToBottom();
}

// ===== 8. ADAPTIVE TASK CLASSIFICATION =====
// This lightweight heuristic labels tasks for the dashboard.
// It does not select a second model or invoke a hidden agent.
function classifyTask(text) {
  const s = text.toLowerCase();
  if (/\b(2\s*[+\-*/]\s*\d+|calculate|calculator|what is \d+|solve \d+|percent(age)?|square root)\b/.test(s)) return "Math / calculation";
  if (/\b(code|javascript|html|css|python|debug|program|function|error in|api)\b/.test(s)) return "Coding";
  if (/\b(summarize|summary|rewrite|plan|checklist|outline|organize)\b/.test(s)) return "Planning / summary";
  if (/\b(document|pdf|file|attachment|uploaded)\b/.test(s)) return "Document question";
  if (/\b(research|latest|current news|sources|look up|search the web)\b/.test(s)) return "Research request";
  return "General conversation";
}

// ===== 9. LOCAL CALCULATOR =====
// Supports only a small, explicit arithmetic grammar. No eval() is used.
function calculateLocally(text) {
  const match = text.trim().match(/^(?:calc(?:ulate)?\s*:?\s*)?([-+*/().\d\s]+)\s*=?\s*\??$/i);
  if (!match) return null;

  const expression = match[1].trim();
  if (!expression || !/\d/.test(expression)) return null;
  if (!/^[\d+\-*/().\s]+$/.test(expression)) return null;

  // Tokenize and parse arithmetic with standard operator precedence.
  const tokens = expression.match(/\d+(?:\.\d+)?|[()+\-*/]/g);
  if (!tokens || tokens.join("") !== expression.replace(/\s/g, "")) return null;
  let pos = 0;

  function parseExpression() {
    let value = parseTerm();
    while (tokens[pos] === "+" || tokens[pos] === "-") {
      const op = tokens[pos++];
      const rhs = parseTerm();
      value = op === "+" ? value + rhs : value - rhs;
    }
    return value;
  }
  function parseTerm() {
    let value = parseUnary();
    while (tokens[pos] === "*" || tokens[pos] === "/") {
      const op = tokens[pos++];
      const rhs = parseUnary();
      if (op === "/" && rhs === 0) throw new Error("Division by zero");
      value = op === "*" ? value * rhs : value / rhs;
    }
    return value;
  }
  function parseUnary() {
    if (tokens[pos] === "+") { pos++; return parseUnary(); }
    if (tokens[pos] === "-") { pos++; return -parseUnary(); }
    if (tokens[pos] === "(") {
      pos++;
      const value = parseExpression();
      if (tokens[pos++] !== ")") throw new Error("Unmatched parenthesis");
      return value;
    }
    const token = tokens[pos++];
    if (!token || !/^\d/.test(token)) throw new Error("Invalid expression");
    return Number(token);
  }

  try {
    const result = parseExpression();
    if (pos !== tokens.length || !Number.isFinite(result)) return null;
    return Object.is(result, -0) ? "0" : String(Number(result.toPrecision(12)));
  } catch (_) {
    return null;
  }
}

// ===== 10. GEMINI API CONNECTION =====
// Kept in the request format specified for this prototype.
async function callAI(history) {
  // history = [{ role: "user" | "assistant", text: "..." }, ...]
  const url = "https://generativelanguage.googleapis.com/v1beta/models/" + MODEL + ":generateContent";
  const res = await fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json", "x-goog-api-key": API_KEY.trim() },
    body: JSON.stringify({
      system_instruction: { parts: [{ text: SYSTEM_PROMPT }] },
      contents: history.map(m => ({
        role: m.role === "assistant" ? "model" : "user",
        parts: [{ text: m.text }]
      }))
    }),
    signal: activeController ? activeController.signal : undefined
  });
  const data = await res.json().catch(() => ({}));
  if (!res.ok) throw new Error("Error " + res.status + ": " + ((data.error && data.error.message) || "Request failed"));
  const parts = (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts) || [];
  const text = parts.filter(p => p.text && !p.thought).map(p => p.text).join("");
  if (!text) throw new Error("The AI sent an empty reply. Try asking again.");
  return text;
}

// ===== 11. CHAT REQUEST FLOW =====
function setActivity(state, task) {
  $("#activityState").textContent = state;
  if (task) $("#taskType").textContent = task;
  $("#connectionLabel").textContent = isWaiting ? "Thinking" : "Ready";
}

function updateWaiting(waiting) {
  isWaiting = waiting;
  sendBtn.disabled = waiting;
  inputEl.disabled = waiting;
  $("#micBtn").disabled = waiting;
  $("#connectionLabel").textContent = waiting ? "Thinking" : "Ready";
  sendBtn.title = waiting ? "Waiting for response" : "Send message";
}

async function sendMessage(rawText) {
  const text = String(rawText || "").trim();
  if (!text || isWaiting) return;

  // Deterministic local arithmetic is preferred for simple arithmetic-only input.
  const mathResult = calculateLocally(text);
  history.push({ role: "user", text });
  history = history.slice(-MAX_MESSAGES);
  addMessage("user", text);
  saveHistory();
  inputEl.value = "";
  updateCharCount();
  inputEl.style.height = "auto";

  const task = classifyTask(text);
  setActivity("Understanding", task);

  if (mathResult !== null) {
    const reply = "The result is **" + mathResult + "**.\n\nCalculated locally by the NEXUS arithmetic tool; no AI API request was needed.";
    history.push({ role: "assistant", text: reply });
    history = history.slice(-MAX_MESSAGES);
    addMessage("assistant", reply);
    saveHistory();
    setActivity("Completed", task);
    $("#latencyValue").textContent = "Local calculation";
    $("#connectionLabel").textContent = "Ready";
    return;
  }

  if (!API_KEY.trim() || API_KEY.trim() === "PASTE_YOUR_API_KEY_HERE") {
    const message = "Paste your API key on line 6 of index.html, save, and refresh. For security, do not share your key in chat or publish this file with a real key.";
    addMessage("assistant", message, { error: true });
    setActivity("API key needed", task);
    $("#connectionLabel").textContent = "Key required";
    return;
  }

  if (!navigator.onLine) {
    addMessage("assistant", "No internet connection detected. NEXUS currently uses the remote Gemini API, so connect to the internet and try again.", { error: true });
    setActivity("Offline", task);
    $("#connectionLabel").textContent = "Offline";
    return;
  }

  updateWaiting(true);
  showTyping();
  setActivity("Selecting route", task);
  activeController = new AbortController();
  const startedAt = performance.now();

  try {
    setActivity("Generating", task);
    const reply = await callAI(history);
    const latency = Math.round(performance.now() - startedAt);
    history.push({ role: "assistant", text: reply });
    history = history.slice(-MAX_MESSAGES);
    hideTyping();
    addMessage("assistant", reply);
    saveHistory();
    $("#latencyValue").textContent = latency + " ms";
    setActivity("Completed", task);
  } catch (error) {
    hideTyping();
    const errorText = error && error.name === "AbortError"
      ? "The request was cancelled."
      : (error && error.message ? error.message : "An unknown error occurred.");
    addMessage("assistant", "Request failed: " + errorText, { error: true });
    setActivity("Request failed", task);
  } finally {
    activeController = null;
    updateWaiting(false);
    inputEl.disabled = false;
    sendBtn.disabled = false;
    $("#connectionLabel").textContent = "Ready";
    inputEl.focus();
  }
}

// ===== 12. BUTTONS AND INPUT EVENTS =====
formEl.addEventListener("submit", event => {
  event.preventDefault();
  sendMessage(inputEl.value);
});

inputEl.addEventListener("keydown", event => {
  if (event.key === "Enter" && !event.shiftKey && !event.isComposing) {
    event.preventDefault();
    if (!isWaiting) sendMessage(inputEl.value);
  }
});

inputEl.addEventListener("input", () => {
  inputEl.style.height = "auto";
  inputEl.style.height = Math.min(inputEl.scrollHeight, 180) + "px";
  updateCharCount();
});

function updateCharCount() {
  $("#charCount").textContent = inputEl.value.length + " / 12000";
}

messagesEl.addEventListener("click", event => {
  const button = event.target.closest("[data-prompt]");
  if (button) sendMessage(button.dataset.prompt);
});

$("#clearBtn").addEventListener("click", clearChat);
$("#newChatBtn").addEventListener("click", clearChat);

function clearChat() {
  if (isWaiting && activeController) activeController.abort();
  hideTyping();
  updateWaiting(false);
  history = [];
  try {
    localStorage.removeItem(STORAGE_KEY);
  } catch (_) {}
  if ("speechSynthesis" in window) window.speechSynthesis.cancel();
  drawHistory();
  setActivity("Ready", "Awaiting input");
  $("#latencyValue").textContent = "Not measured";
  $("#connectionLabel").textContent = "Ready";
  inputEl.disabled = false;
  sendBtn.disabled = false;
  inputEl.value = "";
  updateCharCount();
  showToast("Chat cleared.");
  inputEl.focus();
}

function showToast(message) {
  toastEl.textContent = message;
  toastEl.classList.add("show");
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => toastEl.classList.remove("show"), 2300);
}

async function copyText(text) {
  if (navigator.clipboard && window.isSecureContext) {
    await navigator.clipboard.writeText(text);
    return;
  }
  const helper = document.createElement("textarea");
  helper.value = text;
  helper.style.position = "fixed";
  helper.style.opacity = "0";
  document.body.appendChild(helper);
  helper.select();
  const ok = document.execCommand("copy");
  helper.remove();
  if (!ok) throw new Error("Copy command failed");
}

// ===== 13. DARK / LIGHT MODE =====
function applyTheme(theme) {
  document.documentElement.dataset.theme = theme;
  $("#themeBtn").textContent = theme === "dark" ? "☀" : "☾";
  $("#themeBtn").setAttribute("aria-label", theme === "dark" ? "Switch to light appearance" : "Switch to dark appearance");
  try { localStorage.setItem(THEME_KEY, theme); } catch (_) {}
}

let initialTheme = "light";
try {
  const savedTheme = localStorage.getItem(THEME_KEY);
  if (savedTheme === "dark" || savedTheme === "light") initialTheme = savedTheme;
} catch (_) {}
applyTheme(initialTheme);

$("#themeBtn").addEventListener("click", () => {
  applyTheme(document.documentElement.dataset.theme === "dark" ? "light" : "dark");
});

// ===== 14. OPTIONAL SPEECH OUTPUT =====
function speakText(text) {
  if (!("speechSynthesis" in window) || !("SpeechSynthesisUtterance" in window)) {
    showToast("Speech output is not supported in this browser.");
    return;
  }
  window.speechSynthesis.cancel();
  const utterance = new SpeechSynthesisUtterance(text);
  utterance.lang = "en-IN";
  utterance.rate = 1;
  window.speechSynthesis.speak(utterance);
}

// ===== 15. OPTIONAL SPEECH RECOGNITION =====
const SpeechRecognitionAPI = window.SpeechRecognition || window.webkitSpeechRecognition;

if (SpeechRecognitionAPI) {
  $("#micBtn").hidden = false;
  $("#voiceStatus").textContent = "Available";
  recognition = new SpeechRecognitionAPI();
  recognition.lang = "en-IN";
  recognition.interimResults = true;
  recognition.continuous = false;

  recognition.addEventListener("result", event => {
    let transcript = "";
    for (let i = event.resultIndex; i < event.results.length; i++) {
      transcript += event.results[i][0].transcript;
    }
    inputEl.value = transcript;
    updateCharCount();
    inputEl.style.height = "auto";
    inputEl.style.height = Math.min(inputEl.scrollHeight, 180) + "px";
  });
  recognition.addEventListener("error", event => {
    showToast("Voice input: " + event.error);
  });
  recognition.addEventListener("end", () => {
    $("#micBtn").textContent = "🎙";
    $("#micBtn").title = "Speak to type";
  });
  $("#micBtn").addEventListener("click", () => {
    try {
      recognition.start();
      $("#micBtn").textContent = "●";
      $("#micBtn").title = "Listening…";
    } catch (_) {
      showToast("Voice input is already active. Try again shortly.");
    }
  });
} else {
  $("#micBtn").hidden = true;
  $("#voiceStatus").textContent = "Unsupported";
}

// ===== 16. STARTUP =====
$("#modelName").textContent = MODEL;

history = readSavedHistory();
drawHistory();
updateCharCount();
setActivity("Ready", "Awaiting input");
$("#connectionLabel").textContent =
  (!API_KEY.trim() || API_KEY.trim() === "PASTE_YOUR_API_KEY_HERE")
    ? "Key required"
    : (navigator.onLine ? "Ready" : "Offline");

window.addEventListener("online", () => {
  if (!isWaiting) $("#connectionLabel").textContent = "Ready";
});
window.addEventListener("offline", () => {
  $("#connectionLabel").textContent = "Offline";
});

</script>
</body>
</html>
