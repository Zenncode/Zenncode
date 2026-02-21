<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Zenjan — GitHub Stats Preview</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #0d1117;
      --surface: #161b22;
      --border: #21262d;
      --accent: #00c9ff;
      --accent2: #7f5af0;
      --text: #e6edf3;
      --muted: #8b949e;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'JetBrains Mono', monospace;
      min-height: 100vh;
      padding: 40px 20px;
    }

    .container {
      max-width: 900px;
      margin: 0 auto;
    }

    .section-label {
      font-family: 'Syne', sans-serif;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .section-label::before {
      content: '';
      width: 24px;
      height: 2px;
      background: var(--accent);
      display: inline-block;
    }

    h2 {
      font-family: 'Syne', sans-serif;
      font-size: 28px;
      font-weight: 800;
      margin-bottom: 28px;
      position: relative;
    }

    /* ── TROPHIES ── */
    .trophies-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(110px, 1fr));
      gap: 12px;
      margin-bottom: 60px;
    }

    .trophy-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 16px 10px;
      text-align: center;
      transition: border-color 0.2s, transform 0.2s;
      position: relative;
      overflow: hidden;
    }
    .trophy-card::after {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 50% 0%, rgba(0,201,255,0.06), transparent 70%);
      pointer-events: none;
    }
    .trophy-card:hover {
      border-color: var(--accent);
      transform: translateY(-3px);
    }

    .trophy-icon {
      font-size: 30px;
      margin-bottom: 8px;
      display: block;
    }
    .trophy-title {
      font-size: 9px;
      font-weight: 700;
      letter-spacing: 0.05em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 4px;
    }
    .trophy-value {
      font-family: 'Syne', sans-serif;
      font-size: 16px;
      font-weight: 800;
      color: var(--text);
    }
    .trophy-value.gold { color: #ffd700; }
    .trophy-value.silver { color: #c0c0c0; }
    .trophy-value.bronze { color: #cd7f32; }

    /* ── STATS GRID ── */
    .stats-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      margin-bottom: 60px;
    }

    @media (max-width: 600px) {
      .stats-grid { grid-template-columns: 1fr; }
    }

    .stat-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 24px;
      position: relative;
      overflow: hidden;
      transition: border-color 0.2s;
    }
    .stat-card:hover { border-color: var(--accent2); }

    .stat-card .glow {
      position: absolute;
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(127,90,240,0.15), transparent 70%);
      top: -60px;
      right: -60px;
      pointer-events: none;
    }

    .stat-card-title {
      font-size: 10px;
      font-weight: 700;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 20px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .stat-card-title .dot {
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--accent);
    }

    .stat-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 9px 0;
      border-bottom: 1px solid var(--border);
    }
    .stat-row:last-child { border-bottom: none; }

    .stat-name {
      font-size: 11px;
      color: var(--muted);
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .stat-name .icon { font-size: 14px; }

    .stat-num {
      font-family: 'Syne', sans-serif;
      font-weight: 700;
      font-size: 15px;
      color: var(--text);
    }

    /* streak card */
    .streak-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 28px 32px;
      margin-bottom: 60px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
      flex-wrap: wrap;
      position: relative;
      overflow: hidden;
    }
    .streak-card::before {
      content: '';
      position: absolute;
      bottom: -40px; left: -40px;
      width: 200px; height: 200px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(0,201,255,0.1), transparent 70%);
      pointer-events: none;
    }

    .streak-block { text-align: center; flex: 1; min-width: 120px; }
    .streak-number {
      font-family: 'Syne', sans-serif;
      font-size: 42px;
      font-weight: 800;
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      line-height: 1;
    }
    .streak-label {
      font-size: 10px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--muted);
      margin-top: 6px;
    }
    .streak-divider {
      width: 1px;
      height: 60px;
      background: var(--border);
      flex-shrink: 0;
    }

    /* Top langs */
    .lang-bar-wrap { margin-bottom: 60px; }
    .lang-row {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 10px;
    }
    .lang-name {
      font-size: 11px;
      width: 120px;
      color: var(--muted);
      flex-shrink: 0;
    }
    .lang-bar-bg {
      flex: 1;
      height: 8px;
      background: var(--border);
      border-radius: 99px;
      overflow: hidden;
    }
    .lang-bar-fill {
      height: 100%;
      border-radius: 99px;
      background: linear-gradient(90deg, var(--accent), var(--accent2));
      transition: width 1s ease;
    }
    .lang-pct {
      font-size: 11px;
      font-weight: 700;
      color: var(--text);
      width: 36px;
      text-align: right;
    }

    .note {
      text-align: center;
      font-size: 11px;
      color: var(--muted);
      margin-top: -40px;
      margin-bottom: 40px;
    }

    /* README COPY SECTION */
    .readme-box {
      background: #0d1117;
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 24px;
      margin-top: 60px;
    }
    .readme-box h3 {
      font-family: 'Syne', sans-serif;
      font-size: 14px;
      font-weight: 700;
      color: var(--accent);
      margin-bottom: 16px;
    }
    .readme-box pre {
      font-size: 11px;
      color: #8b949e;
      white-space: pre-wrap;
      word-break: break-all;
      line-height: 1.8;
    }
    .copy-btn {
      background: var(--accent);
      color: #000;
      border: none;
      border-radius: 6px;
      padding: 8px 16px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 11px;
      font-weight: 700;
      cursor: pointer;
      margin-top: 12px;
      transition: opacity 0.2s;
    }
    .copy-btn:hover { opacity: 0.8; }

    hr.divider {
      border: none;
      border-top: 1px solid var(--border);
      margin: 48px 0;
    }
  </style>
</head>
<body>
<div class="container">

  <!-- HEADER -->
  <div style="margin-bottom:48px; padding-bottom:24px; border-bottom: 1px solid #21262d;">
    <div class="section-label">GitHub Profile</div>
    <h2 style="font-size:36px;">Zenjan Kiervin B. Arce</h2>
    <p style="color:var(--muted); font-size:12px;">Fullstack Developer · OJT Intern @ FTCC Solutions Inc.</p>
  </div>

  <!-- TROPHIES -->
  <div class="section-label">Achievements</div>
  <h2>🏆 GitHub Trophies</h2>
  <div class="trophies-grid">
    <div class="trophy-card">
      <span class="trophy-icon">🏆</span>
      <div class="trophy-title">Commits</div>
      <div class="trophy-value gold">Gold</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🌟</span>
      <div class="trophy-title">Stars</div>
      <div class="trophy-value silver">Silver</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🔁</span>
      <div class="trophy-title">Followers</div>
      <div class="trophy-value bronze">Bronze</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🗂️</span>
      <div class="trophy-title">Repos</div>
      <div class="trophy-value gold">Gold</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🐣</span>
      <div class="trophy-title">Experience</div>
      <div class="trophy-value" style="color:var(--accent)">Junior</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🔀</span>
      <div class="trophy-title">Pull Req.</div>
      <div class="trophy-value silver">Silver</div>
    </div>
    <div class="trophy-card">
      <span class="trophy-icon">🐛</span>
      <div class="trophy-title">Issues</div>
      <div class="trophy-value bronze">Bronze</div>
    </div>
  </div>
  <p class="note">*Trophy levels are illustrative — badges load dynamically from github-profile-trophy.vercel.app</p>

  <hr class="divider"/>

  <!-- STATS -->
  <div class="section-label">Activity</div>
  <h2>📊 GitHub Stats</h2>
  <div class="stats-grid">
    <div class="stat-card">
      <div class="glow"></div>
      <div class="stat-card-title"><span class="dot"></span>Overview</div>
      <div class="stat-row">
        <span class="stat-name"><span class="icon">⭐</span>Total Stars Earned</span>
        <span class="stat-num">—</span>
      </div>
      <div class="stat-row">
        <span class="stat-name"><span class="icon">🔁</span>Total Commits (2024)</span>
        <span class="stat-num">—</span>
      </div>
      <div class="stat-row">
        <span class="stat-name"><span class="icon">🔀</span>Total PRs</span>
        <span class="stat-num">—</span>
      </div>
      <div class="stat-row">
        <span class="stat-name"><span class="icon">🐛</span>Total Issues</span>
        <span class="stat-num">—</span>
      </div>
      <div class="stat-row">
        <span class="stat-name"><span class="icon">📦</span>Contributed To</span>
        <span class="stat-num">—</span>
      </div>
    </div>

    <div class="stat-card">
      <div class="glow"></div>
      <div class="stat-card-title"><span class="dot"></span>Top Languages</div>
      <div class="lang-bar-wrap" style="margin-bottom:0">
        <div class="lang-row">
          <span class="lang-name">TypeScript</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" style="width:72%"></div></div>
          <span class="lang-pct">72%</span>
        </div>
        <div class="lang-row">
          <span class="lang-name">JavaScript</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" style="width:55%"></div></div>
          <span class="lang-pct">55%</span>
        </div>
        <div class="lang-row">
          <span class="lang-name">Python</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" style="width:38%"></div></div>
          <span class="lang-pct">38%</span>
        </div>
        <div class="lang-row">
          <span class="lang-name">PHP</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" style="width:20%"></div></div>
          <span class="lang-pct">20%</span>
        </div>
        <div class="lang-row">
          <span class="lang-name">Java</span>
          <div class="lang-bar-bg"><div class="lang-bar-fill" style="width:14%"></div></div>
          <span class="lang-pct">14%</span>
        </div>
      </div>
    </div>
  </div>

  <hr class="divider"/>

  <!-- STREAK -->
  <div class="section-label">Consistency</div>
  <h2>🔥 Contribution Streak</h2>
  <div class="streak-card">
    <div class="streak-block">
      <div class="streak-number">—</div>
      <div class="streak-label">Total Contributions</div>
    </div>
    <div class="streak-divider"></div>
    <div class="streak-block">
      <div class="streak-number">—</div>
      <div class="streak-label">Current Streak</div>
    </div>
    <div class="streak-divider"></div>
    <div class="streak-block">
      <div class="streak-number">—</div>
      <div class="streak-label">Longest Streak</div>
    </div>
  </div>

  <hr class="divider"/>

  <!-- README SNIPPET -->
  <div class="readme-box">
    <h3>📋 Fixed README Snippet — Copy & Replace</h3>
    <pre id="readme-code">
&lt;!-- ════════════ TROPHIES ════════════ --&gt;
&lt;h2 align="center"&gt;🏆 GitHub Trophies&lt;/h2&gt;
&lt;p align="center"&gt;
  &lt;img src="https://github-profile-trophy.vercel.app/?username=zenncode&amp;theme=darkhub&amp;no-frame=true&amp;no-bg=true&amp;margin-w=6&amp;column=7&amp;rank=SECRET,SSS,SS,S,AAA,AA,A,B,C" alt="trophies"/&gt;
&lt;/p&gt;

&lt;br/&gt;

&lt;!-- ════════════ GITHUB STATS ════════════ --&gt;
&lt;h2 align="center"&gt;📊 GitHub Stats&lt;/h2&gt;

&lt;div align="center"&gt;
  &lt;img src="https://github-readme-stats.vercel.app/api?username=zenncode&amp;show_icons=true&amp;theme=tokyonight&amp;hide_border=true&amp;count_private=true&amp;include_all_commits=true" height="175"/&gt;
  &amp;nbsp;&amp;nbsp;
  &lt;img src="https://github-readme-stats.vercel.app/api/top-langs/?username=zenncode&amp;layout=compact&amp;theme=tokyonight&amp;hide_border=true&amp;langs_count=8" height="175"/&gt;
&lt;/div&gt;

&lt;br/&gt;

&lt;!-- ════════════ STREAK ════════════ --&gt;
&lt;p align="center"&gt;
  &lt;img src="https://streak-stats.demolab.com?user=zenncode&amp;theme=tokyonight&amp;hide_border=true&amp;date_format=M%20j%5B%2C%20Y%5D" alt="GitHub Streak"/&gt;
&lt;/p&gt;
    </pre>
    <button class="copy-btn" onclick="
      navigator.clipboard.writeText(document.getElementById('readme-code').innerText.trim());
      this.textContent = '✓ Copied!';
      setTimeout(() => this.textContent = 'Copy README Snippet', 2000);
    ">Copy README Snippet</button>
  </div>

  <p style="text-align:center; color:var(--muted); font-size:11px; margin-top:32px;">
    Preview by Claude · Stats load live from GitHub APIs
  </p>

</div>
</body>
</html>
