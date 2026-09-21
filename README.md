<title>Simba Copilot</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Gabarito:wght@500;600;700&family=Hanken+Grotesk:ital,wght@0,400;0,500;0,600;1,400&family=JetBrains+Mono:wght@400;500&display=swap">
<style>
  :root {
    --ground: #FFFFFF;
    --surface: #FBF7F3;
    --surface-2: #F4EDE5;
    --line: #E7DCD0;
    --line-strong: #D6C5B4;
    --ink: #1C1613;
    --ink-2: #6B5A4E;
    --ink-3: #9B8878;
    --brown: #8A5223;
    --brown-deep: #5E3714;
    --brown-soft: #F0E3D6;
    --good: #4A6B3D;
    --warn: #8A6A1F;
    --radius: 14px;
    --shadow: 0 1px 2px rgba(48, 30, 16, .06), 0 8px 24px rgba(48, 30, 16, .05);
    color-scheme: light;
  }

  @media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) {
      --ground: #0A0908;
      --surface: #141110;
      --surface-2: #1E1916;
      --line: #2B2320;
      --line-strong: #3E332C;
      --ink: #F3EBE3;
      --ink-2: #B5A294;
      --ink-3: #7E6E62;
      --brown: #C4854A;
      --brown-deep: #E0A96D;
      --brown-soft: #251A12;
      --good: #8FB37C;
      --warn: #D2AC5C;
      --shadow: 0 1px 2px rgba(0, 0, 0, .5), 0 10px 30px rgba(0, 0, 0, .35);
      color-scheme: dark;
    }
  }

  :root[data-theme="dark"] {
    --ground: #0A0908;
    --surface: #141110;
    --surface-2: #1E1916;
    --line: #2B2320;
    --line-strong: #3E332C;
    --ink: #F3EBE3;
    --ink-2: #B5A294;
    --ink-3: #7E6E62;
    --brown: #C4854A;
    --brown-deep: #E0A96D;
    --brown-soft: #251A12;
    --good: #8FB37C;
    --warn: #D2AC5C;
    --shadow: 0 1px 2px rgba(0, 0, 0, .5), 0 10px 30px rgba(0, 0, 0, .35);
    color-scheme: dark;
  }

  * { box-sizing: border-box; }
  html, body { height: 100%; }

  body {
    margin: 0;
    background: var(--ground);
    color: var(--ink);
    font-family: "Hanken Grotesk", ui-sans-serif, system-ui, -apple-system, sans-serif;
    font-size: 15px;
    line-height: 1.55;
    -webkit-font-smoothing: antialiased;
  }

  h1, h2, h3, .display {
    font-family: Gabarito, "Hanken Grotesk", ui-sans-serif, system-ui, sans-serif;
    font-weight: 600;
    letter-spacing: -0.015em;
    text-wrap: balance;
    margin: 0;
  }

  .mono { font-family: "JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, monospace; font-variant-numeric: tabular-nums; }

  :focus-visible { outline: 2px solid var(--brown); outline-offset: 2px; border-radius: 6px; }

  /* ---------- shell ---------- */
  .app {
    display: grid;
    grid-template-columns: 252px minmax(0, 1fr);
    height: 100%;
  }

  /* ---------- sidebar ---------- */
  .rail {
    background: var(--surface);
    border-right: 1px solid var(--line);
    display: flex;
    flex-direction: column;
    min-height: 0;
  }

  .brand {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 18px 18px 14px;
  }

  .mark {
    width: 34px; height: 34px;
    flex: none;
    border-radius: 11px;
    background: linear-gradient(150deg, var(--brown) 0%, var(--brown-deep) 100%);
    display: grid;
    place-items: center;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, .22);
  }

  .mark svg { display: block; }

  .brand-name {
    font-family: Gabarito, sans-serif;
    font-weight: 700;
    font-size: 19px;
    letter-spacing: -0.02em;
    line-height: 1;
  }

  .brand-sub {
    font-size: 10.5px;
    letter-spacing: .14em;
    text-transform: uppercase;
    color: var(--ink-3);
    margin-top: 3px;
  }

  .rail-scroll { overflow-y: auto; padding: 4px 12px 12px; flex: 1; min-height: 0; }

  .rail-label {
    font-size: 10.5px;
    letter-spacing: .13em;
    text-transform: uppercase;
    color: var(--ink-3);
    padding: 14px 6px 7px;
  }

  .thread {
    display: block;
    width: 100%;
    text-align: left;
    background: none;
    border: 0;
    border-radius: 10px;
    padding: 8px 10px;
    color: var(--ink-2);
    font: inherit;
    font-size: 13.5px;
    cursor: pointer;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .thread:hover { background: var(--surface-2); color: var(--ink); }

  .thread[aria-current="true"] {
    background: var(--brown-soft);
    color: var(--brown-deep);
    font-weight: 600;
  }

  .new-chat {
    margin: 0 18px 12px;
    padding: 9px 12px;
    border-radius: 10px;
    border: 1px solid var(--line-strong);
    background: var(--ground);
    color: var(--ink);
    font: inherit;
    font-weight: 600;
    font-size: 13.5px;
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: border-color .15s, background .15s;
  }

  .new-chat:hover { border-color: var(--brown); background: var(--surface-2); }

  .rail-foot {
    border-top: 1px solid var(--line);
    padding: 12px 16px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
  }

  .who { display: flex; align-items: center; gap: 9px; min-width: 0; }

  .avatar {
    width: 26px; height: 26px; flex: none;
    border-radius: 50%;
    background: var(--surface-2);
    border: 1px solid var(--line-strong);
    display: grid;
    place-items: center;
    font-size: 11px;
    font-weight: 600;
    color: var(--ink-2);
  }

  .who-name { font-size: 13px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

  .icon-btn {
    width: 30px; height: 30px;
    flex: none;
    border-radius: 8px;
    border: 1px solid transparent;
    background: none;
    color: var(--ink-2);
    cursor: pointer;
    display: grid;
    place-items: center;
  }

  .icon-btn:hover { background: var(--surface-2); color: var(--ink); border-color: var(--line); }

  /* ---------- main ---------- */
  .main { display: flex; flex-direction: column; min-width: 0; min-height: 0; }

  .topbar {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 22px;
    border-bottom: 1px solid var(--line);
    background: var(--ground);
  }

  .crumb { font-size: 13.5px; color: var(--ink-2); flex: 1; min-width: 0; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
  .crumb strong { color: var(--ink); font-weight: 600; }

  .menu-btn { display: none; }

  .routing {
    display: flex;
    align-items: center;
    gap: 7px;
    font-size: 11.5px;
    color: var(--ink-2);
    background: var(--surface);
    border: 1px solid var(--line);
    border-radius: 999px;
    padding: 4px 10px 4px 8px;
  }

  .dot { width: 6px; height: 6px; border-radius: 50%; background: var(--good); flex: none; }

  .stream {
    flex: 1;
    overflow-y: auto;
    min-height: 0;
    scroll-behavior: smooth;
  }

  .stream-inner {
    max-width: 720px;
    margin: 0 auto;
    padding: 28px 20px 8px;
    display: flex;
    flex-direction: column;
    gap: 26px;
  }

  .turn { display: grid; grid-template-columns: 30px minmax(0, 1fr); gap: 13px; }

  .turn-mark {
    width: 30px; height: 30px;
    border-radius: 9px;
    display: grid;
    place-items: center;
    font-size: 11px;
    font-weight: 600;
  }

  .turn.user .turn-mark { background: var(--surface-2); color: var(--ink-2); border: 1px solid var(--line); }
  .turn.simba .turn-mark { background: linear-gradient(150deg, var(--brown) 0%, var(--brown-deep) 100%); color: #fff; }

  .turn-body { min-width: 0; }

  .turn-who {
    font-size: 11px;
    letter-spacing: .1em;
    text-transform: uppercase;
    color: var(--ink-3);
    margin-bottom: 5px;
  }

  .turn-body p { margin: 0 0 10px; }
  .turn-body p:last-child { margin-bottom: 0; }
  .turn-body ul { margin: 0 0 10px; padding-left: 20px; }
  .turn-body li { margin-bottom: 5px; }
  .turn-body code:not(pre code) {
    font-family: "JetBrains Mono", monospace;
    font-size: 12.5px;
    background: var(--surface-2);
    border: 1px solid var(--line);
    border-radius: 5px;
    padding: 1px 5px;
  }

  pre {
    margin: 0 0 10px;
    background: var(--surface);
    border: 1px solid var(--line);
    border-left: 3px solid var(--brown);
    border-radius: 10px;
    padding: 12px 14px;
    overflow-x: auto;
    font-family: "JetBrains Mono", monospace;
    font-size: 12.5px;
    line-height: 1.6;
    color: var(--ink);
  }

  .tok-key { color: var(--brown); }
  .tok-com { color: var(--ink-3); font-style: italic; }

  .trace {
    border: 1px solid var(--line);
    border-radius: var(--radius);
    background: var(--surface);
    padding: 10px 12px;
    margin-bottom: 12px;
    font-size: 12.5px;
  }

  .trace-head {
    display: flex;
    align-items: center;
    gap: 8px;
    color: var(--ink-2);
    font-size: 11px;
    letter-spacing: .1em;
    text-transform: uppercase;
  }

  .trace-rows { margin-top: 8px; display: flex; flex-direction: column; gap: 6px; }

  .trace-row {
    display: grid;
    grid-template-columns: minmax(0, 1fr) auto auto;
    gap: 10px;
    align-items: center;
    color: var(--ink-2);
  }

  .chip {
    font-family: "JetBrains Mono", monospace;
    font-size: 10.5px;
    letter-spacing: .03em;
    border-radius: 999px;
    padding: 2px 8px;
    border: 1px solid var(--line-strong);
    color: var(--ink-2);
    white-space: nowrap;
  }

  .chip.nano { border-color: color-mix(in srgb, var(--good) 45%, transparent); color: var(--good); }
  .chip.super { border-color: color-mix(in srgb, var(--warn) 50%, transparent); color: var(--warn); }
  .chip.ultra { border-color: var(--brown); color: var(--brown); background: var(--brown-soft); }

  .ms { font-family: "JetBrains Mono", monospace; font-size: 11px; color: var(--ink-3); font-variant-numeric: tabular-nums; }

  .caret {
    display: inline-block;
    width: 7px;
    height: 1.05em;
    background: var(--brown);
    vertical-align: -2px;
    margin-left: 2px;
    animation: blink 1s steps(2) infinite;
  }

  @keyframes blink { 50% { opacity: 0; } }

  .fade-in { animation: rise .32s cubic-bezier(.2, .7, .3, 1) both; }
  @keyframes rise { from { opacity: 0; transform: translateY(7px); } to { opacity: 1; transform: none; } }

  /* ---------- empty state ---------- */
  .welcome { padding: 44px 20px 10px; max-width: 720px; margin: 0 auto; }
  .welcome h1 { font-size: clamp(27px, 5vw, 34px); }
  .welcome p { color: var(--ink-2); margin: 9px 0 0; max-width: 46ch; }

  .starters {
    margin-top: 22px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
    gap: 10px;
  }

  .starter {
    text-align: left;
    background: var(--surface);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 12px 14px;
    color: var(--ink);
    font: inherit;
    font-size: 13.5px;
    cursor: pointer;
    transition: border-color .15s, transform .15s;
  }

  .starter:hover { border-color: var(--brown); transform: translateY(-1px); }
  .starter span { display: block; color: var(--ink-3); font-size: 11.5px; margin-top: 3px; }

  /* ---------- composer ---------- */
  .composer-wrap {
    border-top: 1px solid var(--line);
    background: var(--ground);
    padding: 14px 20px calc(14px + env(safe-area-inset-bottom, 0px));
  }

  .composer {
    max-width: 720px;
    margin: 0 auto;
    background: var(--surface);
    border: 1px solid var(--line-strong);
    border-radius: 16px;
    padding: 10px 10px 8px 14px;
    box-shadow: var(--shadow);
    transition: border-color .15s;
  }

  .composer:focus-within { border-color: var(--brown); }

  .composer textarea {
    width: 100%;
    border: 0;
    background: none;
    resize: none;
    color: var(--ink);
    font: inherit;
    line-height: 1.5;
    max-height: 150px;
    outline: none;
  }

  .composer textarea::placeholder { color: var(--ink-3); }

  .composer-row {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-top: 6px;
  }

  .mode {
    display: flex;
    gap: 2px;
    background: var(--surface-2);
    border: 1px solid var(--line);
    border-radius: 999px;
    padding: 2px;
  }

  .mode button {
    border: 0;
    background: none;
    border-radius: 999px;
    padding: 3px 10px;
    font: inherit;
    font-size: 12px;
    color: var(--ink-2);
    cursor: pointer;
  }

  .mode button[aria-pressed="true"] { background: var(--ground); color: var(--brown-deep); font-weight: 600; box-shadow: 0 1px 2px rgba(0, 0, 0, .08); }

  .spacer { flex: 1; }

  .send {
    width: 34px; height: 34px;
    border-radius: 10px;
    border: 0;
    background: var(--brown);
    color: #fff;
    cursor: pointer;
    display: grid;
    place-items: center;
    transition: background .15s, opacity .15s;
  }

  .send:hover { background: var(--brown-deep); }
  .send:disabled { opacity: .4; cursor: default; }
  :root[data-theme="dark"] .send, :root:not([data-theme="light"]) .send { color: #1a1108; }
  @media (prefers-color-scheme: light) { :root:not([data-theme="dark"]) .send { color: #fff; } }

  .hint { text-align: center; color: var(--ink-3); font-size: 11.5px; margin: 8px auto 0; }

  /* ---------- responsive ---------- */
  .scrim { display: none; }

  @media (max-width: 760px) {
    .app { grid-template-columns: minmax(0, 1fr); }
    .rail {
      position: fixed;
      inset: 0 auto 0 0;
      width: 250px;
      z-index: 20;
      transform: translateX(-102%);
      transition: transform .22s ease;
      padding-top: env(safe-area-inset-top, 0px);
    }
    .rail.open { transform: none; }
    .scrim { display: block; position: fixed; inset: 0; background: rgba(20, 12, 6, .45); z-index: 15; opacity: 0; pointer-events: none; transition: opacity .2s; }
    .scrim.on { opacity: 1; pointer-events: auto; }
    .menu-btn { display: grid; }
    .topbar { padding: 10px 16px; padding-top: calc(10px + env(safe-area-inset-top, 0px)); }
    .routing { display: none; }
    .stream-inner, .welcome { padding-left: 16px; padding-right: 16px; }
    .composer-wrap { padding-left: 16px; padding-right: 16px; }
    .trace-row { grid-template-columns: minmax(0, 1fr) auto; }
    .trace-row .ms { grid-column: 2; }
  }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; }
    .stream { scroll-behavior: auto; }
  }
</style>

<div class="app">
  <aside class="rail" id="rail">
    <div class="brand">
      <div class="mark" aria-hidden="true">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="1.7" stroke-linecap="round" stroke-linejoin="round">
          <circle cx="12" cy="12" r="4.4"></circle>
          <path d="M12 2.2v3M12 18.8v3M2.2 12h3M18.8 12h3M5.1 5.1l2.1 2.1M16.8 16.8l2.1 2.1M18.9 5.1l-2.1 2.1M7.2 16.8l-2.1 2.1"></path>
        </svg>
      </div>
      <div>
        <div class="brand-name">Simba</div>
        <div class="brand-sub">Copilot</div>
      </div>
    </div>

    <button class="new-chat" id="newChat">
      <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M12 5v14M5 12h14"></path></svg>
      New conversation
    </button>

    <div class="rail-scroll">
      <div class="rail-label">Today</div>
      <button class="thread" aria-current="true">Onboarding flow drop-off</button>
      <button class="thread">Rewrite the pricing FAQ</button>
      <button class="thread">Why is the nightly job slow?</button>
      <div class="rail-label">Earlier this week</div>
      <button class="thread">Q3 retro notes → action items</button>
      <button class="thread">Draft reply to the Acme thread</button>
      <button class="thread">Compare the two vendor quotes</button>
      <button class="thread">Checklist for Friday's release</button>
    </div>

    <div class="rail-foot">
      <div class="who">
        <div class="avatar">CS</div>
        <div class="who-name">Chaitanya</div>
      </div>
      <button class="icon-btn" id="themeBtn" title="Switch theme" aria-label="Switch theme">
        <svg id="themeIcon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="12" r="4"></circle><path d="M12 3v2M12 19v2M3 12h2M19 12h2M5.6 5.6l1.4 1.4M17 17l1.4 1.4M18.4 5.6L17 7M7 17l-1.4 1.4"></path></svg>
      </button>
    </div>
  </aside>

  <div class="scrim" id="scrim"></div>

  <main class="main">
    <div class="topbar">
      <button class="icon-btn menu-btn" id="menuBtn" aria-label="Open conversations">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M4 7h16M4 12h16M4 17h16"></path></svg>
      </button>
      <div class="crumb"><strong>Onboarding flow drop-off</strong> · 6 messages</div>
      <div class="routing"><span class="dot"></span> Routing on · 3 models</div>
    </div>

    <div class="stream" id="stream">
      <div class="stream-inner" id="inner">

        <div class="turn user">
          <div class="turn-mark">CS</div>
          <div class="turn-body">
            <div class="turn-who">Chaitanya</div>
            <p>Signups are fine but only 41% of people finish onboarding. Where are we losing them?</p>
          </div>
        </div>

        <div class="turn simba">
          <div class="turn-mark" aria-hidden="true">S</div>
          <div class="turn-body">
            <div class="turn-who">Simba</div>
            <div class="trace">
              <div class="trace-head">
                <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M4 17l6-6 4 4 6-7"></path></svg>
                How this answer was routed
              </div>
              <div class="trace-rows">
                <div class="trace-row"><span>Classify the question</span><span class="chip nano">nano</span><span class="ms">180 ms</span></div>
                <div class="trace-row"><span>Pull the 4 funnel steps</span><span class="chip nano">nano</span><span class="ms">240 ms</span></div>
                <div class="trace-row"><span>Find the cause, rank the fixes</span><span class="chip ultra">ultra</span><span class="ms">6.4 s</span></div>
              </div>
            </div>
            <p>Three of the four steps hold up. The drop is almost all at step 3, the workspace invite.</p>
            <ul>
              <li><strong>Step 1, account</strong> — 100% → 94%. Healthy.</li>
              <li><strong>Step 2, pick a template</strong> — 94% → 88%. Healthy.</li>
              <li><strong>Step 3, invite teammates</strong> — 88% → 52%. <em>This is the leak.</em></li>
              <li><strong>Step 4, first project</strong> — 52% → 41%. Normal for the traffic that reaches it.</li>
            </ul>
            <p>Step 3 has no skip control, so a solo user has nowhere to go. Median time on that screen is 71 seconds, and 3 in 5 of the people who leave never come back the same day.</p>
            <p>The smallest fix is to make the step optional:</p>
<pre><span class="tok-com">// onboarding/steps.ts</span>
{
  id: <span class="tok-key">'invite'</span>,
  required: <span class="tok-key">false</span>,        <span class="tok-com">// was true</span>
  skipLabel: <span class="tok-key">'I'll do this later'</span>,
  remindAfter: <span class="tok-key">'3d'</span>
}</pre>
            <p>Want me to draft the PR, or look at what the people who do invite teammates have in common first?</p>
          </div>
        </div>

      </div>
      <p class="hint" id="demoNote">Sample conversation. Responses here are canned — wire the composer to your model to make it live.</p>
    </div>

    <div class="composer-wrap">
      <div class="composer">
        <label for="input" class="visually-hidden" style="position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);">Message Simba</label>
        <textarea id="input" rows="1" placeholder="Ask Simba anything…"></textarea>
        <div class="composer-row">
          <div class="mode" role="group" aria-label="Answer depth">
            <button id="mAuto" aria-pressed="true">Auto</button>
            <button id="mFast" aria-pressed="false">Fast</button>
            <button id="mDeep" aria-pressed="false">Deep</button>
          </div>
          <div class="spacer"></div>
          <button class="send" id="send" aria-label="Send message" disabled>
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h13M12 5l7 7-7 7"></path></svg>
          </button>
        </div>
      </div>
      <p class="hint">Simba can be wrong. Check anything that matters before you act on it.</p>
    </div>
  </main>
</div>

<script>
  (function () {
    var root = document.documentElement;
    var themeBtn = document.getElementById('themeBtn');
    var icon = document.getElementById('themeIcon');

    var SUN = '<circle cx="12" cy="12" r="4"></circle><path d="M12 3v2M12 19v2M3 12h2M19 12h2M5.6 5.6l1.4 1.4M17 17l1.4 1.4M18.4 5.6L17 7M7 17l-1.4 1.4"></path>';
    var MOON = '<path d="M20 14.5A8.2 8.2 0 0 1 9.5 4a8.3 8.3 0 1 0 10.5 10.5z"></path>';

    function isDark() {
      var t = root.getAttribute('data-theme');
      if (t) return t === 'dark';
      return window.matchMedia('(prefers-color-scheme: dark)').matches;
    }

    function paintIcon() { icon.innerHTML = isDark() ? SUN : MOON; }

    try {
      var saved = localStorage.getItem('simba-theme');
      if (saved === 'dark' || saved === 'light') root.setAttribute('data-theme', saved);
    } catch (e) {}
    paintIcon();

    themeBtn.addEventListener('click', function () {
      var next = isDark() ? 'light' : 'dark';
      root.setAttribute('data-theme', next);
      try { localStorage.setItem('simba-theme', next); } catch (e) {}
      paintIcon();
    });

    /* sidebar on phones */
    var rail = document.getElementById('rail');
    var scrim = document.getElementById('scrim');
    function closeRail() { rail.classList.remove('open'); scrim.classList.remove('on'); }
    document.getElementById('menuBtn').addEventListener('click', function () {
      rail.classList.add('open'); scrim.classList.add('on');
    });
    scrim.addEventListener('click', closeRail);
    Array.prototype.forEach.call(document.querySelectorAll('.thread'), function (t) {
      t.addEventListener('click', function () {
        Array.prototype.forEach.call(document.querySelectorAll('.thread'), function (o) { o.removeAttribute('aria-current'); });
        t.setAttribute('aria-current', 'true');
        closeRail();
      });
    });

    /* depth toggle */
    var modes = [document.getElementById('mAuto'), document.getElementById('mFast'), document.getElementById('mDeep')];
    var depth = 'Auto';
    modes.forEach(function (b) {
      b.addEventListener('click', function () {
        modes.forEach(function (o) { o.setAttribute('aria-pressed', String(o === b)); });
        depth = b.textContent.trim();
      });
    });

    /* composer */
    var input = document.getElementById('input');
    var send = document.getElementById('send');
    var inner = document.getElementById('inner');
    var stream = document.getElementById('stream');
    var busy = false;

    function grow() {
      input.style.height = 'auto';
      input.style.height = Math.min(input.scrollHeight, 150) + 'px';
      send.disabled = busy || !input.value.trim();
    }

    input.addEventListener('input', grow);
    input.addEventListener('keydown', function (e) {
      if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); submit(); }
    });
    send.addEventListener('click', submit);

    function turn(kind, who, markup) {
      var el = document.createElement('div');
      el.className = 'turn ' + kind + ' fade-in';
      el.innerHTML = '<div class="turn-mark">' + (kind === 'user' ? 'CS' : 'S') +
        '</div><div class="turn-body"><div class="turn-who">' + who + '</div>' + markup + '</div>';
      inner.appendChild(el);
      stream.scrollTop = stream.scrollHeight;
      return el;
    }

    function plan() {
      if (depth === 'Fast') {
        return [['Read the question', 'nano', '150 ms'], ['Draft the answer', 'super', '1.1 s']];
      }
      if (depth === 'Deep') {
        return [['Classify the question', 'nano', '170 ms'], ['Gather context', 'super', '900 ms'], ['Reason it through', 'ultra', '7.8 s']];
      }
      return [['Classify the question', 'nano', '160 ms'], ['Draft the answer', 'super', '1.4 s']];
    }

    var REPLIES = [
      "Here is where I would start. The shortest path is to change one thing, measure it for a week, and only then touch anything else — a single change keeps the result readable.",
      "Short answer: yes, but not the way it is set up now. The current approach works until roughly ten thousand rows, then the sort dominates. Move it to the database and it holds.",
      "I pulled the three relevant pieces together. Two of them agree; the third is from an older run, so I am weighting it lower. Say the word and I will reconcile them properly."
    ];
    var replyAt = 0;

    function submit() {
      var text = input.value.trim();
      if (!text || busy) return;
      busy = true;
      var note = document.getElementById('demoNote');
      if (note) note.remove();

      var p = document.createElement('p');
      p.textContent = text;
      turn('user', 'Chaitanya', p.outerHTML);

      input.value = '';
      grow();
      send.disabled = true;

      var steps = plan();
      var rows = steps.map(function (s) {
        return '<div class="trace-row"><span>' + s[0] + '</span><span class="chip ' + s[1] + '">' + s[1] + '</span><span class="ms">' + s[2] + '</span></div>';
      }).join('');

      var el = turn('simba', 'Simba',
        '<div class="trace"><div class="trace-head">' +
        '<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M4 17l6-6 4 4 6-7"></path></svg>' +
        ' How this answer was routed</div><div class="trace-rows">' + rows + '</div></div>' +
        '<p class="out"><span class="caret"></span></p>');

      var out = el.querySelector('.out');
      var body = REPLIES[replyAt % REPLIES.length];
      replyAt++;

      var reduce = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      if (reduce) {
        out.textContent = body;
        busy = false;
        grow();
        return;
      }

      var i = 0;
      var timer = setInterval(function () {
        i += 2;
        out.textContent = body.slice(0, i);
        if (i < body.length) {
          out.appendChild(document.createElement('span')).className = 'caret';
        } else {
          clearInterval(timer);
          busy = false;
          grow();
        }
        stream.scrollTop = stream.scrollHeight;
      }, 16);
    }

    document.getElementById('newChat').addEventListener('click', function () {
      inner.innerHTML = '';
      var w = document.createElement('div');
      w.className = 'welcome fade-in';
      w.innerHTML = '<h1>What are we working on?</h1>' +
        '<p>Simba reads the question first, then picks the model that fits it — so the quick ones stay quick.</p>' +
        '<div class="starters">' +
        '<button class="starter">Explain this error<span>Paste a stack trace</span></button>' +
        '<button class="starter">Turn notes into tasks<span>With owners and dates</span></button>' +
        '<button class="starter">Review my draft<span>Tone, clarity, length</span></button>' +
        '<button class="starter">Plan a change<span>Steps, risks, rollback</span></button>' +
        '</div>';
      inner.appendChild(w);
      Array.prototype.forEach.call(w.querySelectorAll('.starter'), function (b) {
        b.addEventListener('click', function () {
          input.value = b.childNodes[0].nodeValue;
          grow();
          input.focus();
        });
      });
      document.querySelector('.crumb').innerHTML = '<strong>New conversation</strong>';
      closeRail();
    });

    grow();
  })();
</script>
