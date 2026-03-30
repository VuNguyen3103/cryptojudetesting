<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CryptoJudge — Decision Support</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Fraunces:ital,wght@0,300;0,400;0,600;0,700;1,300;1,400&display=swap');

:root {
  --bg: #f5f2ec;
  --bg2: #ede9e0;
  --bg3: #e4dfd3;
  --ink: #1a1714;
  --ink2: #4a4540;
  --ink3: #8a8078;
  --rule: #d4cec4;
  --buy: #1a7a4a;
  --buy-bg: #e8f5ee;
  --buy-border: #a8d4bb;
  --sell: #a0241c;
  --sell-bg: #faecea;
  --sell-border: #e0a8a4;
  --hold: #7a5a1a;
  --hold-bg: #faf5e8;
  --hold-border: #d4bc80;
  --accent: #2a4a8a;
  --mono: 'DM Mono', monospace;
  --serif: 'Fraunces', serif;
  --radius: 10px;
  --shadow: 0 2px 12px rgba(26,23,20,0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background: var(--bg);
  color: var(--ink);
  font-family: var(--serif);
  font-size: 15px;
  line-height: 1.6;
  min-height: 100vh;
}

/* ── Layout ── */
.page {
  max-width: 980px;
  margin: 0 auto;
  padding: 48px 24px 80px;
}

/* ── Header ── */
.header {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  border-bottom: 2px solid var(--ink);
  padding-bottom: 20px;
  margin-bottom: 40px;
}
.header-left h1 {
  font-size: 36px;
  font-weight: 700;
  letter-spacing: -1.5px;
  line-height: 1;
  font-style: italic;
}
.header-left h1 span { font-style: normal; }
.header-left p {
  font-size: 13px;
  color: var(--ink3);
  margin-top: 6px;
  font-family: var(--mono);
  font-style: normal;
}
.header-right {
  text-align: right;
  font-family: var(--mono);
  font-size: 11px;
  color: var(--ink3);
  line-height: 1.8;
}
.header-right strong { color: var(--ink); font-weight: 500; display: block; }

/* ── Two-column layout ── */
.layout { display: grid; grid-template-columns: 1fr 380px; gap: 28px; align-items: start; }

/* ── Form Sections ── */
.form-sections { display: flex; flex-direction: column; gap: 20px; }

.section {
  background: #fff;
  border: 1px solid var(--rule);
  border-radius: var(--radius);
  overflow: hidden;
  box-shadow: var(--shadow);
}

.section-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 14px 18px;
  background: var(--bg2);
  border-bottom: 1px solid var(--rule);
}
.section-title {
  font-size: 12px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  font-family: var(--mono);
  color: var(--ink2);
  display: flex;
  align-items: center;
  gap: 8px;
}
.section-badge {
  font-size: 9px;
  padding: 2px 7px;
  border-radius: 20px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.8px;
  font-family: var(--mono);
}
.badge-mandatory { background: #1a1714; color: #f5f2ec; }
.badge-recommended { background: var(--rule); color: var(--ink2); }
.badge-optional { background: var(--bg3); color: var(--ink3); }

.section-body { padding: 18px; display: flex; flex-direction: column; gap: 14px; }

/* ── Form Fields ── */
.field { display: flex; flex-direction: column; gap: 6px; }
.field-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.field-row-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; }

label {
  font-size: 12px;
  font-weight: 500;
  color: var(--ink2);
  font-family: var(--mono);
  display: flex;
  align-items: center;
  gap: 6px;
}
.label-hint { font-weight: 400; color: var(--ink3); font-size: 11px; }

input[type="number"], input[type="text"] {
  width: 100%;
  padding: 9px 12px;
  border: 1px solid var(--rule);
  border-radius: 7px;
  background: var(--bg);
  color: var(--ink);
  font-family: var(--mono);
  font-size: 13px;
  transition: border-color 0.15s, box-shadow 0.15s;
  outline: none;
}
input[type="number"]:focus, input[type="text"]:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(42,74,138,0.1);
  background: #fff;
}
input::placeholder { color: var(--ink3); }

/* ── Segmented Controls ── */
.seg-group { display: flex; border: 1px solid var(--rule); border-radius: 8px; overflow: hidden; background: var(--bg); }
.seg-btn {
  flex: 1;
  padding: 8px 6px;
  font-size: 11px;
  font-family: var(--mono);
  font-weight: 500;
  text-align: center;
  cursor: pointer;
  color: var(--ink3);
  border: none;
  background: transparent;
  transition: all 0.15s;
  border-right: 1px solid var(--rule);
  line-height: 1.2;
}
.seg-btn:last-child { border-right: none; }
.seg-btn:hover { background: var(--bg2); color: var(--ink2); }
.seg-btn.active-bull { background: var(--buy-bg); color: var(--buy); border-color: var(--buy-border); }
.seg-btn.active-bear { background: var(--sell-bg); color: var(--sell); border-color: var(--sell-border); }
.seg-btn.active-neu  { background: var(--hold-bg); color: var(--hold); border-color: var(--hold-border); }
.seg-btn.active-blue { background: #e8eef8; color: var(--accent); border-color: #b0c0e0; }

/* ── RSI Slider ── */
.rsi-wrap { position: relative; }
.rsi-slider {
  width: 100%;
  height: 6px;
  -webkit-appearance: none;
  border-radius: 3px;
  outline: none;
  cursor: pointer;
  background: linear-gradient(to right, #2a8a6a 0%, #2a8a6a 33%, #d4bc40 33%, #d4bc40 66%, #c0402a 66%, #c0402a 100%);
}
.rsi-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 18px; height: 18px;
  border-radius: 50%;
  background: var(--ink);
  border: 3px solid #fff;
  box-shadow: 0 1px 4px rgba(0,0,0,0.2);
  cursor: pointer;
  transition: transform 0.1s;
}
.rsi-slider::-webkit-slider-thumb:hover { transform: scale(1.15); }
.rsi-labels { display: flex; justify-content: space-between; font-size: 10px; color: var(--ink3); font-family: var(--mono); margin-top: 5px; }
.rsi-val {
  font-family: var(--mono); font-size: 18px; font-weight: 500;
  text-align: center; padding: 8px;
  background: var(--bg);
  border: 1px solid var(--rule);
  border-radius: 7px;
  margin-bottom: 8px;
}

/* ── Price inputs ── */
.price-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; }

/* ── Checkbox toggle ── */
.toggle-row {
  display: flex; align-items: center; justify-content: space-between;
  padding: 10px 14px;
  background: var(--bg);
  border: 1px solid var(--rule);
  border-radius: 7px;
  cursor: pointer;
}
.toggle-row:hover { background: var(--bg2); }
.toggle-label { font-size: 13px; color: var(--ink2); }
.toggle-switch {
  width: 36px; height: 20px;
  background: var(--rule);
  border-radius: 10px;
  position: relative;
  transition: background 0.2s;
  flex-shrink: 0;
}
.toggle-switch.on { background: var(--buy); }
.toggle-switch::after {
  content: '';
  position: absolute;
  width: 14px; height: 14px;
  border-radius: 50%;
  background: #fff;
  top: 3px; left: 3px;
  transition: transform 0.2s;
  box-shadow: 0 1px 3px rgba(0,0,0,0.2);
}
.toggle-switch.on::after { transform: translateX(16px); }

/* ── Right Panel ── */
.panel { display: flex; flex-direction: column; gap: 16px; position: sticky; top: 24px; }

/* ── Signal Output Card ── */
.signal-card {
  background: #fff;
  border: 1px solid var(--rule);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  overflow: hidden;
}
.signal-top {
  padding: 24px;
  text-align: center;
  border-bottom: 1px solid var(--rule);
  position: relative;
}
.signal-idle {
  padding: 36px 24px;
  text-align: center;
  color: var(--ink3);
}
.signal-idle-icon { font-size: 32px; margin-bottom: 12px; opacity: 0.4; }
.signal-idle-text { font-size: 13px; font-family: var(--mono); line-height: 1.6; }

.signal-label-text {
  font-size: 11px;
  font-family: var(--mono);
  color: var(--ink3);
  text-transform: uppercase;
  letter-spacing: 1.5px;
  margin-bottom: 10px;
}
.signal-word {
  font-size: 56px;
  font-weight: 700;
  letter-spacing: -3px;
  line-height: 1;
  font-style: italic;
}
.signal-word.BUY  { color: var(--buy); }
.signal-word.SELL { color: var(--sell); }
.signal-word.HOLD { color: var(--hold); }

.signal-score {
  margin-top: 12px;
  font-family: var(--mono);
  font-size: 13px;
  color: var(--ink3);
}
.signal-score strong { color: var(--ink); }

.signal-metrics {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--rule);
  border-top: 1px solid var(--rule);
}
.metric-box {
  background: #fff;
  padding: 14px 16px;
  text-align: center;
}
.metric-label { font-size: 10px; font-family: var(--mono); color: var(--ink3); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px; }
.metric-val { font-size: 20px; font-weight: 600; font-style: italic; }
.metric-val.green { color: var(--buy); }
.metric-val.red   { color: var(--sell); }
.metric-val.yellow { color: var(--hold); }
.metric-val.blue  { color: var(--accent); }

/* ── Confidence bar ── */
.conf-bar-outer {
  height: 8px;
  background: var(--bg3);
  border-radius: 4px;
  overflow: hidden;
  margin-top: 6px;
}
.conf-bar-inner { height: 100%; border-radius: 4px; transition: width 0.5s ease; }

/* ── Score Breakdown ── */
.score-card {
  background: #fff;
  border: 1px solid var(--rule);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  overflow: hidden;
}
.score-header {
  padding: 12px 16px;
  background: var(--bg2);
  border-bottom: 1px solid var(--rule);
  font-size: 11px;
  font-family: var(--mono);
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: var(--ink2);
}
.score-list { padding: 12px; display: flex; flex-direction: column; gap: 5px; }
.score-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 7px 10px;
  border-radius: 6px;
  font-size: 12px;
}
.score-item.pos { background: var(--buy-bg); }
.score-item.neg { background: var(--sell-bg); }
.score-item.neu { background: var(--bg); border: 1px solid var(--rule); }
.score-item-label { color: var(--ink2); flex: 1; }
.score-item-pts {
  font-family: var(--mono);
  font-weight: 500;
  font-size: 12px;
  padding: 2px 8px;
  border-radius: 4px;
  min-width: 40px;
  text-align: center;
}
.score-item.pos .score-item-pts { color: var(--buy); }
.score-item.neg .score-item-pts { color: var(--sell); }
.score-item.neu .score-item-pts { color: var(--ink3); }

.score-total {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  background: var(--bg2);
  border-top: 1px solid var(--rule);
  font-family: var(--mono);
  font-size: 13px;
}
.score-total-val { font-size: 20px; font-weight: 500; }

/* ── Reasoning ── */
.reasoning-card {
  background: #fff;
  border: 1px solid var(--rule);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
}
.reasoning-list { padding: 12px; display: flex; flex-direction: column; gap: 6px; }
.reason-item {
  font-size: 12px;
  padding: 9px 12px;
  border-radius: 6px;
  line-height: 1.5;
  border-left: 3px solid transparent;
}
.reason-item.pos { background: var(--buy-bg); border-color: var(--buy); color: #0f4a2a; }
.reason-item.neg { background: var(--sell-bg); border-color: var(--sell); color: #6a1410; }
.reason-item.neu { background: var(--hold-bg); border-color: var(--hold); color: #5a3c0a; }
.reason-item.warn { background: #faecd0; border-color: #d07020; color: #6a3800; }

/* ── Warnings ── */
.warn-box {
  background: #fff8e8;
  border: 1px solid #e0c060;
  border-radius: 8px;
  padding: 12px 14px;
  font-size: 12px;
  color: #6a4a00;
  font-family: var(--mono);
  line-height: 1.6;
  display: none;
}
.warn-box.visible { display: block; }

/* ── JSON Output ── */
.json-card {
  background: var(--ink);
  border-radius: var(--radius);
  overflow: hidden;
  box-shadow: var(--shadow);
}
.json-header {
  padding: 10px 14px;
  background: #2a2520;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: var(--mono);
  font-size: 11px;
  color: #8a8078;
}
.json-copy {
  cursor: pointer;
  padding: 3px 8px;
  border: 1px solid #3a3530;
  border-radius: 4px;
  font-size: 10px;
  background: transparent;
  color: #8a8078;
  font-family: var(--mono);
  transition: all 0.15s;
}
.json-copy:hover { background: #3a3530; color: #c4bcb0; }
.json-body {
  padding: 16px;
  font-family: var(--mono);
  font-size: 11px;
  line-height: 1.7;
  white-space: pre;
  overflow-x: auto;
}
.jk { color: #88c0d0; }
.jvs { color: #a3be8c; }
.jvn { color: #d08770; }
.jvc { color: #81a1c1; }

/* ── Run Button ── */
.run-btn {
  width: 100%;
  padding: 14px;
  background: var(--ink);
  color: var(--bg);
  border: none;
  border-radius: var(--radius);
  font-family: var(--serif);
  font-size: 16px;
  font-weight: 600;
  font-style: italic;
  cursor: pointer;
  transition: all 0.15s;
  letter-spacing: -0.3px;
}
.run-btn:hover { background: #2a2520; transform: translateY(-1px); box-shadow: 0 4px 16px rgba(26,23,20,0.2); }
.run-btn:active { transform: translateY(0); }

.reset-btn {
  width: 100%;
  padding: 10px;
  background: transparent;
  border: 1px solid var(--rule);
  border-radius: 7px;
  font-family: var(--mono);
  font-size: 12px;
  color: var(--ink3);
  cursor: pointer;
  transition: all 0.15s;
}
.reset-btn:hover { background: var(--bg2); color: var(--ink2); }

/* ── Score meter ── */
.score-meter {
  padding: 16px;
  border-bottom: 1px solid var(--rule);
}
.meter-track {
  position: relative;
  height: 10px;
  background: linear-gradient(to right, var(--sell-bg) 0%, var(--hold-bg) 50%, var(--buy-bg) 100%);
  border-radius: 5px;
  border: 1px solid var(--rule);
  margin: 10px 0 6px;
  overflow: visible;
}
.meter-bar {
  position: absolute;
  top: -3px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: var(--ink);
  border: 3px solid #fff;
  box-shadow: 0 1px 4px rgba(0,0,0,0.25);
  transform: translateX(-50%);
  transition: left 0.5s ease;
  left: 50%;
}
.meter-line-buy { position: absolute; right: 25%; top: -4px; height: calc(100% + 8px); width: 1px; background: var(--buy); opacity: 0.5; }
.meter-line-sell { position: absolute; left: 25%; top: -4px; height: calc(100% + 8px); width: 1px; background: var(--sell); opacity: 0.5; }
.meter-labels { display: flex; justify-content: space-between; font-size: 10px; font-family: var(--mono); }

/* ── Anim ── */
@keyframes fadeUp { from { opacity:0; transform:translateY(12px); } to { opacity:1; transform:translateY(0); } }
.signal-card, .score-card, .reasoning-card, .json-card { animation: fadeUp 0.4s ease both; }
.result-flash { animation: flash 0.5s ease; }
@keyframes flash { 0%,100%{opacity:1} 50%{opacity:0.6} }

/* ── Responsiveness ── */
@media (max-width: 768px) {
  .layout { grid-template-columns: 1fr; }
  .panel { position: static; }
  .header { flex-direction: column; align-items: flex-start; gap: 12px; }
  .header-right { text-align: left; }
  .field-row, .field-row-3, .price-grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>
<div class="page">

  <!-- Header -->
  <div class="header">
    <div class="header-left">
      <h1><span>Crypto</span>Judge</h1>
      <p>manual decision-support system · not financial advice</p>
    </div>
    <div class="header-right">
      <strong>How to use</strong>
      Fill in what you know<br>
      Leave unknown fields blank<br>
      Press <em>Analyse</em> to get signal
    </div>
  </div>

  <div class="layout">

    <!-- ── LEFT: Input Form ── -->
    <div class="form-sections">

      <!-- Section 1: Price Action -->
      <div class="section">
        <div class="section-header">
          <span class="section-title">① Price Action</span>
          <span class="section-badge badge-mandatory">Mandatory</span>
        </div>
        <div class="section-body">

          <div class="field">
            <label>Current Price <span class="label-hint">(any asset, any currency)</span></label>
            <input type="number" id="currentPrice" placeholder="e.g. 84000" step="any" min="0">
          </div>

          <div class="field">
            <label>Recent Trend</label>
            <div class="seg-group" id="trendGroup">
              <button class="seg-btn" data-val="strong_up" onclick="setSeg(this,'trendGroup','bull')">Strong<br>Uptrend</button>
              <button class="seg-btn" data-val="weak_up" onclick="setSeg(this,'trendGroup','bull')">Weak<br>Uptrend</button>
              <button class="seg-btn" data-val="sideways" onclick="setSeg(this,'trendGroup','neu')">Sideways</button>
              <button class="seg-btn" data-val="weak_down" onclick="setSeg(this,'trendGroup','bear')">Weak<br>Downtrend</button>
              <button class="seg-btn" data-val="strong_down" onclick="setSeg(this,'trendGroup','bear')">Strong<br>Downtrend</button>
            </div>
          </div>

          <div class="price-grid">
            <div class="field">
              <label>Support Level</label>
              <input type="number" id="support" placeholder="e.g. 80000" step="any" min="0">
            </div>
            <div class="field">
              <label>Resistance Level</label>
              <input type="number" id="resistance" placeholder="e.g. 88000" step="any" min="0">
            </div>
            <div class="field">
              <label>Near Support/Resistance?</label>
              <div class="seg-group" id="nearLevelGroup" style="height:42px">
                <button class="seg-btn" data-val="near_support" onclick="setSeg(this,'nearLevelGroup','bull')" style="font-size:10px">Near<br>Support</button>
                <button class="seg-btn" data-val="near_resistance" onclick="setSeg(this,'nearLevelGroup','bear')" style="font-size:10px">Near<br>Resistance</button>
                <button class="seg-btn" data-val="midrange" onclick="setSeg(this,'nearLevelGroup','neu')" style="font-size:10px">Mid-<br>range</button>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Section 2: Technical Indicators -->
      <div class="section">
        <div class="section-header">
          <span class="section-title">② Technical Indicators</span>
          <span class="section-badge badge-recommended">Recommended</span>
        </div>
        <div class="section-body">

          <div class="field">
            <label>RSI (14) <span class="label-hint">— drag the slider</span></label>
            <div class="rsi-val" id="rsiVal">50</div>
            <div class="rsi-wrap">
              <input type="range" class="rsi-slider" id="rsiSlider" min="0" max="100" value="50" oninput="updateRSI(this.value)">
              <div class="rsi-labels">
                <span style="color:var(--buy)">0 — Oversold</span>
                <span>30</span>
                <span style="color:var(--hold)">50 — Neutral</span>
                <span>70</span>
                <span style="color:var(--sell)">100 — Overbought</span>
              </div>
            </div>
            <div style="display:flex;align-items:center;gap:8px;margin-top:8px">
              <input type="checkbox" id="rsiEnabled" checked onchange="document.getElementById('rsiSlider').disabled=!this.checked;document.getElementById('rsiVal').style.opacity=this.checked?1:0.3" style="width:14px;height:14px;cursor:pointer">
              <label for="rsiEnabled" style="font-size:11px;cursor:pointer">Include RSI in analysis</label>
            </div>
          </div>

          <div class="field">
            <label>MACD Signal</label>
            <div class="seg-group" id="macdGroup">
              <button class="seg-btn" data-val="bullish_cross" onclick="setSeg(this,'macdGroup','bull')">Bullish<br>Crossover</button>
              <button class="seg-btn" data-val="above_zero" onclick="setSeg(this,'macdGroup','bull')">Above<br>Zero</button>
              <button class="seg-btn" data-val="neutral" onclick="setSeg(this,'macdGroup','neu')">Neutral /<br>Unclear</button>
              <button class="seg-btn" data-val="below_zero" onclick="setSeg(this,'macdGroup','bear')">Below<br>Zero</button>
              <button class="seg-btn" data-val="bearish_cross" onclick="setSeg(this,'macdGroup','bear')">Bearish<br>Crossover</button>
            </div>
          </div>

          <div class="field">
            <label>Moving Average Position</label>
            <div class="seg-group" id="maGroup">
              <button class="seg-btn" data-val="well_above" onclick="setSeg(this,'maGroup','bull')">Well above<br>MA50/200</button>
              <button class="seg-btn" data-val="slightly_above" onclick="setSeg(this,'maGroup','bull')">Slightly above<br>MA</button>
              <button class="seg-btn" data-val="at_ma" onclick="setSeg(this,'maGroup','neu')">At MA<br>(testing)</button>
              <button class="seg-btn" data-val="below_ma" onclick="setSeg(this,'maGroup','bear')">Below<br>MA</button>
              <button class="seg-btn" data-val="well_below" onclick="setSeg(this,'maGroup','bear')">Well below<br>MA50/200</button>
            </div>
          </div>

        </div>
      </div>

      <!-- Section 3: Volume & Momentum -->
      <div class="section">
        <div class="section-header">
          <span class="section-title">③ Volume &amp; Momentum</span>
          <span class="section-badge badge-recommended">Recommended</span>
        </div>
        <div class="section-body">

          <div class="field-row">
            <div class="field">
              <label>Volume Trend</label>
              <div class="seg-group" id="volumeGroup" style="flex-direction:column">
                <button class="seg-btn" data-val="increasing" onclick="setSeg(this,'volumeGroup','bull')" style="border-right:none;border-bottom:1px solid var(--rule)">Increasing</button>
                <button class="seg-btn" data-val="stable" onclick="setSeg(this,'volumeGroup','neu')" style="border-right:none;border-bottom:1px solid var(--rule)">Stable</button>
                <button class="seg-btn" data-val="decreasing" onclick="setSeg(this,'volumeGroup','bear')" style="border-right:none">Decreasing</button>
              </div>
            </div>
            <div class="field">
              <label>Breakout Detected?</label>
              <div class="seg-group" id="breakoutGroup" style="flex-direction:column">
                <button class="seg-btn" data-val="yes_bullish" onclick="setSeg(this,'breakoutGroup','bull')" style="border-right:none;border-bottom:1px solid var(--rule)">Yes — Bullish</button>
                <button class="seg-btn" data-val="yes_bearish" onclick="setSeg(this,'breakoutGroup','bear')" style="border-right:none;border-bottom:1px solid var(--rule)">Yes — Bearish</button>
                <button class="seg-btn" data-val="no" onclick="setSeg(this,'breakoutGroup','neu')" style="border-right:none">No / Unclear</button>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Section 4: Market Sentiment -->
      <div class="section">
        <div class="section-header">
          <span class="section-title">④ Market Sentiment</span>
          <span class="section-badge badge-recommended">Recommended</span>
        </div>
        <div class="section-body">

          <div class="field">
            <label>Overall Sentiment</label>
            <div class="seg-group" id="sentimentGroup">
              <button class="seg-btn" data-val="positive" onclick="setSeg(this,'sentimentGroup','bull')">Positive</button>
              <button class="seg-btn" data-val="neutral" onclick="setSeg(this,'sentimentGroup','neu')">Neutral</button>
              <button class="seg-btn" data-val="negative" onclick="setSeg(this,'sentimentGroup','bear')">Negative</button>
            </div>
          </div>

          <div class="field-row">
            <div class="field">
              <label>News Impact</label>
              <div class="seg-group" id="newsGroup">
                <button class="seg-btn" data-val="bullish" onclick="setSeg(this,'newsGroup','bull')">Bullish</button>
                <button class="seg-btn" data-val="none" onclick="setSeg(this,'newsGroup','neu')">None</button>
                <button class="seg-btn" data-val="bearish" onclick="setSeg(this,'newsGroup','bear')">Bearish</button>
              </div>
            </div>
            <div class="field">
              <label>Social Hype Level</label>
              <div class="seg-group" id="hypeGroup">
                <button class="seg-btn" data-val="low" onclick="setSeg(this,'hypeGroup','neu')">Low</button>
                <button class="seg-btn" data-val="medium" onclick="setSeg(this,'hypeGroup','bull')">Medium</button>
                <button class="seg-btn" data-val="high" onclick="setSeg(this,'hypeGroup','bear')">High</button>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Section 5: Market Context -->
      <div class="section">
        <div class="section-header">
          <span class="section-title">⑤ Market Context</span>
          <span class="section-badge badge-optional">Optional</span>
        </div>
        <div class="section-body">

          <div class="field-row">
            <div class="field">
              <label>Market Regime</label>
              <div class="seg-group" id="regimeGroup" style="flex-direction:column">
                <button class="seg-btn" data-val="bull_market" onclick="setSeg(this,'regimeGroup','bull')" style="border-right:none;border-bottom:1px solid var(--rule)">Bull Market</button>
                <button class="seg-btn" data-val="sideways_market" onclick="setSeg(this,'regimeGroup','neu')" style="border-right:none;border-bottom:1px solid var(--rule)">Sideways</button>
                <button class="seg-btn" data-val="bear_market" onclick="setSeg(this,'regimeGroup','bear')" style="border-right:none">Bear Market</button>
              </div>
            </div>
            <div class="field">
              <label>Volatility Level</label>
              <div class="seg-group" id="volatilityGroup" style="flex-direction:column">
                <button class="seg-btn" data-val="low" onclick="setSeg(this,'volatilityGroup','bull')" style="border-right:none;border-bottom:1px solid var(--rule)">Low</button>
                <button class="seg-btn" data-val="medium" onclick="setSeg(this,'volatilityGroup','neu')" style="border-right:none;border-bottom:1px solid var(--rule)">Medium</button>
                <button class="seg-btn" data-val="high" onclick="setSeg(this,'volatilityGroup','bear')" style="border-right:none">High</button>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Action Buttons -->
      <button class="run-btn" onclick="runAnalysis()">Analyse → Get Signal</button>
      <button class="reset-btn" onclick="resetAll()">↺ Reset all inputs</button>

    </div>

    <!-- ── RIGHT: Output Panel ── -->
    <div class="panel" id="outputPanel">

      <!-- Idle state -->
      <div class="signal-card" id="idleCard">
        <div class="signal-idle">
          <div class="signal-idle-icon">◈</div>
          <div class="signal-idle-text">Fill in the form on the left,<br>then press <strong>Analyse</strong><br>to receive your signal.</div>
        </div>
      </div>

      <!-- Result cards (hidden until analysis) -->
      <div id="resultCards" style="display:none;flex-direction:column;gap:16px">

        <!-- Signal -->
        <div class="signal-card" id="signalCard">
          <div class="signal-top" id="signalTop">
            <div class="signal-label-text">Decision Signal</div>
            <div class="signal-word" id="signalWord">BUY</div>
            <div class="signal-score" id="signalScoreText">Total score: <strong>+6</strong></div>
            <div class="score-meter" style="padding:16px 0 0;border-bottom:none">
              <div class="meter-track">
                <div class="meter-line-sell"></div>
                <div class="meter-line-buy"></div>
                <div class="meter-bar" id="meterDot"></div>
              </div>
              <div class="meter-labels">
                <span style="color:var(--sell)">← SELL</span>
                <span style="color:var(--ink3)">HOLD</span>
                <span style="color:var(--buy)">BUY →</span>
              </div>
            </div>
          </div>
          <div class="signal-metrics">
            <div class="metric-box">
              <div class="metric-label">Confidence</div>
              <div class="metric-val" id="confVal">—</div>
              <div class="conf-bar-outer"><div class="conf-bar-inner" id="confBar" style="width:0%"></div></div>
            </div>
            <div class="metric-box">
              <div class="metric-label">Risk Level</div>
              <div class="metric-val" id="riskVal">—</div>
            </div>
            <div class="metric-box">
              <div class="metric-label">Score</div>
              <div class="metric-val blue" id="scoreVal">—</div>
            </div>
            <div class="metric-box">
              <div class="metric-label">Inputs Used</div>
              <div class="metric-val blue" id="inputsVal">—</div>
            </div>
          </div>
        </div>

        <!-- Warnings -->
        <div class="warn-box" id="warnBox"></div>

        <!-- Score breakdown -->
        <div class="score-card">
          <div class="score-header">Score Breakdown</div>
          <div class="score-list" id="scoreList"></div>
          <div class="score-total">
            <span>Total Score</span>
            <span class="score-total-val" id="scoreTotalVal">0</span>
          </div>
        </div>

        <!-- Reasoning -->
        <div class="reasoning-card">
          <div class="score-header">Signal Reasoning</div>
          <div class="reasoning-list" id="reasoningList"></div>
        </div>

        <!-- JSON -->
        <div class="json-card">
          <div class="json-header">
            <span>output.json</span>
            <button class="json-copy" onclick="copyJSON()">copy</button>
          </div>
          <div class="json-body" id="jsonBody"></div>
        </div>

      </div>
    </div>

  </div>
</div>

<script>
// ─── Segmented control helper ────────────────────────────────────
const segState = {};

function setSeg(btn, groupId, colorClass) {
  const group = document.getElementById(groupId);
  group.querySelectorAll('.seg-btn').forEach(b => {
    b.classList.remove('active-bull','active-bear','active-neu','active-blue');
  });
  const cls = colorClass === 'bull' ? 'active-bull' : colorClass === 'bear' ? 'active-bear' : 'active-neu';
  btn.classList.add(cls);
  segState[groupId] = btn.dataset.val;
}

function getVal(groupId) {
  return segState[groupId] || null;
}

function updateRSI(val) {
  document.getElementById('rsiVal').textContent = val;
  const color = val < 30 ? 'var(--buy)' : val > 70 ? 'var(--sell)' : 'var(--hold)';
  document.getElementById('rsiVal').style.color = color;
}

// ─── Analysis Engine ──────────────────────────────────────────────
function runAnalysis() {
  const entries = [];
  const reasoning = [];
  const warnings = [];
  let totalScore = 0;
  let inputCount = 0;
  let maxPossible = 0;

  // ─ 1. Trend (weight 3) ─
  const trend = getVal('trendGroup');
  maxPossible += 3;
  if (trend) {
    inputCount++;
    const trendMap = {
      strong_up:   { score: 3, cls:'pos', text:'Strong uptrend — powerful bullish momentum' },
      weak_up:     { score: 2, cls:'pos', text:'Weak uptrend — mild bullish pressure' },
      sideways:    { score: 0, cls:'neu', text:'Sideways trend — no directional edge from price action' },
      weak_down:   { score:-2, cls:'neg', text:'Weak downtrend — mild bearish pressure' },
      strong_down: { score:-3, cls:'neg', text:'Strong downtrend — powerful bearish momentum' },
    };
    const t = trendMap[trend];
    totalScore += t.score;
    entries.push({ label:'Price Trend', pts: t.score, cls: t.score>0?'pos':t.score<0?'neg':'neu' });
    reasoning.push({ cls: t.cls, text: t.text });
  } else {
    warnings.push('⚠ Trend not selected — this is the most important input.');
  }

  // ─ 2. Price position vs levels ─
  const currentPrice = parseFloat(document.getElementById('currentPrice').value);
  const support = parseFloat(document.getElementById('support').value);
  const resistance = parseFloat(document.getElementById('resistance').value);
  const nearLevel = getVal('nearLevelGroup');

  if (currentPrice > 0) inputCount++;

  if (nearLevel) {
    inputCount++;
    maxPossible += 2;
    if (nearLevel === 'near_support') {
      totalScore += 2;
      entries.push({ label:'Near Support', pts: +2, cls:'pos' });
      reasoning.push({ cls:'pos', text:'Price near support level — potential bounce zone, risk/reward favourable' });
    } else if (nearLevel === 'near_resistance') {
      totalScore -= 2;
      entries.push({ label:'Near Resistance', pts: -2, cls:'neg' });
      reasoning.push({ cls:'neg', text:'Price near resistance — likely selling pressure, potential rejection' });
    } else {
      entries.push({ label:'Price Level', pts: 0, cls:'neu' });
    }
  }

  // ─ 3. RSI ─
  const rsiEnabled = document.getElementById('rsiEnabled').checked;
  if (rsiEnabled) {
    inputCount++;
    maxPossible += 2;
    const rsi = parseInt(document.getElementById('rsiSlider').value);
    let rsiScore = 0, rsiText = '', rsiCls = 'neu';
    if (rsi < 25) { rsiScore = 3; rsiText = `RSI extremely oversold (${rsi}) — strong mean-reversion signal`; rsiCls='pos'; maxPossible++; }
    else if (rsi < 35) { rsiScore = 2; rsiText = `RSI oversold (${rsi}) — bullish reversal likely`; rsiCls='pos'; }
    else if (rsi > 75) { rsiScore = -3; rsiText = `RSI extremely overbought (${rsi}) — high reversal risk`; rsiCls='neg'; maxPossible++; }
    else if (rsi > 65) { rsiScore = -2; rsiText = `RSI overbought (${rsi}) — momentum may be exhausted`; rsiCls='neg'; }
    else if (rsi >= 45 && rsi <= 55) { rsiScore = 1; rsiText = `RSI neutral (${rsi}) — no extreme signal, slight bullish bias in neutral zone`; rsiCls='neu'; }
    else { rsiText = `RSI at ${rsi} — neutral, no strong directional signal`; }
    totalScore += rsiScore;
    entries.push({ label:`RSI (${rsi})`, pts: rsiScore, cls: rsiScore>0?'pos':rsiScore<0?'neg':'neu' });
    reasoning.push({ cls: rsiCls, text: rsiText });
  }

  // ─ 4. MACD ─
  const macd = getVal('macdGroup');
  maxPossible += 2;
  if (macd) {
    inputCount++;
    const macdMap = {
      bullish_cross: { score: 2, cls:'pos', text:'MACD bullish crossover — momentum shifting upward' },
      above_zero:    { score: 1, cls:'pos', text:'MACD above zero — bullish momentum ongoing' },
      neutral:       { score: 0, cls:'neu', text:'MACD neutral — no strong directional signal' },
      below_zero:    { score:-1, cls:'neg', text:'MACD below zero — bearish momentum ongoing' },
      bearish_cross: { score:-2, cls:'neg', text:'MACD bearish crossover — momentum shifting downward' },
    };
    const m = macdMap[macd];
    totalScore += m.score;
    entries.push({ label:'MACD', pts: m.score, cls: m.score>0?'pos':m.score<0?'neg':'neu' });
    reasoning.push({ cls: m.cls, text: m.text });
  }

  // ─ 5. Moving Averages ─
  const ma = getVal('maGroup');
  maxPossible += 2;
  if (ma) {
    inputCount++;
    const maMap = {
      well_above:    { score: 2, cls:'pos', text:'Price well above MA50/200 — strong bull structure confirmed' },
      slightly_above:{ score: 1, cls:'pos', text:'Price above moving averages — bullish structure intact' },
      at_ma:         { score: 0, cls:'neu', text:'Price testing MA — key decision zone, watch for breakout or rejection' },
      below_ma:      { score:-1, cls:'neg', text:'Price below moving averages — bearish structure' },
      well_below:    { score:-2, cls:'neg', text:'Price well below MA50/200 — strong bear structure confirmed' },
    };
    const m = maMap[ma];
    totalScore += m.score;
    entries.push({ label:'Moving Averages', pts: m.score, cls: m.score>0?'pos':m.score<0?'neg':'neu' });
    reasoning.push({ cls: m.cls, text: m.text });
  }

  // ─ 6. Volume ─
  const vol = getVal('volumeGroup');
  const brk = getVal('breakoutGroup');
  maxPossible += 2;
  if (vol) {
    inputCount++;
    let volScore = 0, volText = '', volCls = 'neu';
    if (vol === 'increasing' && brk === 'yes_bullish') {
      volScore = 3; volText = 'Increasing volume + bullish breakout — high conviction move'; volCls='pos'; maxPossible++;
    } else if (vol === 'increasing' && brk === 'yes_bearish') {
      volScore = -3; volText = 'Increasing volume + bearish breakdown — high conviction sell'; volCls='neg'; maxPossible++;
    } else if (vol === 'increasing') {
      volScore = 1; volText = 'Increasing volume without clear breakout — accumulation possible'; volCls='pos';
    } else if (vol === 'decreasing') {
      volScore = -1; volText = 'Decreasing volume — weak conviction, possible trend exhaustion'; volCls='neg';
    } else {
      volText = 'Stable volume — neutral, no volume confirmation signal';
    }
    if (brk === 'yes_bullish' && vol !== 'increasing') {
      volScore += 1; volText += ' (breakout without strong volume — less reliable)'; volCls='neu';
    } else if (brk === 'yes_bearish' && vol !== 'increasing') {
      volScore -= 1; volText += ' (breakdown without strong volume — less reliable)'; volCls='neu';
    }
    totalScore += volScore;
    entries.push({ label:'Volume / Breakout', pts: volScore, cls: volScore>0?'pos':volScore<0?'neg':'neu' });
    reasoning.push({ cls: volCls, text: volText });
  }

  // ─ 7. Sentiment ─
  const sent = getVal('sentimentGroup');
  maxPossible += 1;
  if (sent) {
    inputCount++;
    const sentMap = {
      positive: { score: 1, cls:'pos', text:'Positive market sentiment — crowd psychology supports upward move' },
      neutral:  { score: 0, cls:'neu', text:'Neutral market sentiment — no crowd-driven edge' },
      negative: { score:-1, cls:'neg', text:'Negative market sentiment — fear dominates, bearish pressure likely' },
    };
    const s = sentMap[sent];
    totalScore += s.score;
    entries.push({ label:'Sentiment', pts: s.score, cls: s.score>0?'pos':s.score<0?'neg':'neu' });
    reasoning.push({ cls: s.cls, text: s.text });
  }

  // ─ 8. News ─
  const news = getVal('newsGroup');
  maxPossible += 1;
  if (news) {
    inputCount++;
    if (news === 'bullish') {
      totalScore += 1;
      entries.push({ label:'News Impact', pts:+1, cls:'pos' });
      reasoning.push({ cls:'pos', text:'Bullish news catalyst — fundamental support for upward move' });
    } else if (news === 'bearish') {
      totalScore -= 1;
      entries.push({ label:'News Impact', pts:-1, cls:'neg' });
      reasoning.push({ cls:'neg', text:'Bearish news catalyst — fundamental headwind' });
    }
  }

  // ─ 9. Social hype ─
  const hype = getVal('hypeGroup');
  if (hype) {
    inputCount++;
    if (hype === 'high') {
      totalScore -= 1;
      entries.push({ label:'Social Hype (high)', pts:-1, cls:'neg' });
      reasoning.push({ cls:'neg', text:'High social hype — contrarian warning, often signals local top' });
    } else if (hype === 'medium') {
      entries.push({ label:'Social Hype (medium)', pts:0, cls:'neu' });
    }
  }

  // ─ 10. Market Regime ─
  const regime = getVal('regimeGroup');
  maxPossible += 1;
  if (regime) {
    inputCount++;
    if (regime === 'bull_market') {
      totalScore += 1;
      entries.push({ label:'Bull Market Regime', pts:+1, cls:'pos' });
      reasoning.push({ cls:'pos', text:'Overall bull market — macro tailwind supports longs' });
    } else if (regime === 'bear_market') {
      totalScore -= 1;
      entries.push({ label:'Bear Market Regime', pts:-1, cls:'neg' });
      reasoning.push({ cls:'neg', text:'Overall bear market — macro headwind, higher risk for longs' });
    }
  }

  // ─ 11. Volatility ─
  const volatility = getVal('volatilityGroup');
  let volatilityPenalty = 0;
  if (volatility) {
    inputCount++;
    if (volatility === 'high') {
      volatilityPenalty = 20;
      warnings.push('⚠ High volatility detected — confidence reduced. Signals are less reliable.');
      reasoning.push({ cls:'warn', text:'High volatility: reduce position size, widen stop-loss, or wait for clearer setup' });
    } else if (volatility === 'medium') {
      volatilityPenalty = 5;
    }
  }

  // ─ Missing data penalty ─
  const missingPenalty = Math.max(0, (5 - inputCount) * 4);
  if (inputCount < 4) {
    warnings.push(`⚠ Only ${inputCount} input categories filled. Confidence reduced due to incomplete data.`);
  }

  // ─ Conflict detection ─
  const hasConflict = entries.some(e => e.cls==='pos') && entries.some(e => e.cls==='neg') && Math.abs(totalScore) <= 2;
  if (hasConflict) {
    warnings.push('⚠ Mixed signals detected — bullish and bearish factors conflict. Defaulting toward HOLD.');
  }

  // ─ Final signal ─
  let signal, signalCls;
  if (totalScore >= 3 && !hasConflict) {
    signal = 'BUY';
    signalCls = 'BUY';
  } else if (totalScore <= -3 && !hasConflict) {
    signal = 'SELL';
    signalCls = 'SELL';
  } else {
    signal = 'HOLD';
    signalCls = 'HOLD';
  }

  // Override: if trend is mandatory but missing
  if (!getVal('trendGroup')) {
    signal = 'HOLD';
    signalCls = 'HOLD';
  }

  // ─ Confidence ─
  const signalStrength = Math.min(Math.abs(totalScore) / 10, 1);
  const dataCoverage = Math.min(inputCount / 8, 1);
  const alignment = entries.length > 0 ? entries.filter(e => (signal==='BUY'&&e.cls==='pos')||(signal==='SELL'&&e.cls==='neg')||(signal==='HOLD'&&e.cls==='neu')).length / entries.length : 0;
  let confidence = Math.round((signalStrength * 40 + dataCoverage * 30 + alignment * 30) * 100 - volatilityPenalty - missingPenalty);
  confidence = Math.max(10, Math.min(95, confidence));

  // ─ Risk ─
  let riskLevel = 'medium';
  if (volatility === 'high' || confidence < 40) riskLevel = 'high';
  else if (confidence > 70 && Math.abs(totalScore) >= 5 && volatility !== 'high') riskLevel = 'low';

  // ─ Render ─
  renderResults({ signal, signalCls, totalScore, confidence, riskLevel, entries, reasoning, warnings, inputCount });
}

function renderResults({ signal, signalCls, totalScore, confidence, riskLevel, entries, reasoning, warnings, inputCount }) {
  document.getElementById('idleCard').style.display = 'none';
  const rc = document.getElementById('resultCards');
  rc.style.display = 'flex';

  // Signal word
  const sw = document.getElementById('signalWord');
  sw.textContent = signal;
  sw.className = 'signal-word result-flash ' + signalCls;
  setTimeout(() => sw.classList.remove('result-flash'), 600);

  document.getElementById('signalScoreText').innerHTML = `Total score: <strong>${totalScore >= 0 ? '+' : ''}${totalScore}</strong>`;

  // Meter
  const pct = Math.max(5, Math.min(95, (totalScore + 12) / 24 * 100));
  document.getElementById('meterDot').style.left = pct + '%';

  // Metrics
  const confEl = document.getElementById('confVal');
  confEl.textContent = confidence + '%';
  confEl.className = 'metric-val ' + (confidence > 65 ? 'green' : confidence > 40 ? 'yellow' : 'red');

  const confBar = document.getElementById('confBar');
  confBar.style.width = confidence + '%';
  confBar.style.background = confidence > 65 ? 'var(--buy)' : confidence > 40 ? 'var(--hold)' : 'var(--sell)';

  const riskEl = document.getElementById('riskVal');
  riskEl.textContent = riskLevel.charAt(0).toUpperCase() + riskLevel.slice(1);
  riskEl.className = 'metric-val ' + (riskLevel === 'low' ? 'green' : riskLevel === 'medium' ? 'yellow' : 'red');

  const scoreEl = document.getElementById('scoreVal');
  scoreEl.textContent = (totalScore >= 0 ? '+' : '') + totalScore;
  scoreEl.className = 'metric-val ' + (totalScore > 0 ? 'green' : totalScore < 0 ? 'red' : 'yellow');

  document.getElementById('inputsVal').textContent = inputCount + '/8';

  // Warnings
  const wb = document.getElementById('warnBox');
  if (warnings.length > 0) {
    wb.innerHTML = warnings.join('<br>');
    wb.classList.add('visible');
  } else {
    wb.classList.remove('visible');
  }

  // Score breakdown
  document.getElementById('scoreList').innerHTML = entries.map(e =>
    `<div class="score-item ${e.cls}">
      <span class="score-item-label">${e.label}</span>
      <span class="score-item-pts">${e.pts >= 0 ? '+' : ''}${e.pts}</span>
    </div>`
  ).join('') || '<div style="padding:12px;font-size:12px;color:var(--ink3);font-family:var(--mono)">No inputs scored yet.</div>';

  const stv = document.getElementById('scoreTotalVal');
  stv.textContent = (totalScore >= 0 ? '+' : '') + totalScore;
  stv.style.color = totalScore >= 3 ? 'var(--buy)' : totalScore <= -3 ? 'var(--sell)' : 'var(--hold)';

  // Reasoning
  document.getElementById('reasoningList').innerHTML = reasoning.map(r =>
    `<div class="reason-item ${r.cls}">${r.text}</div>`
  ).join('') || '<div style="padding:12px;font-size:12px;color:var(--ink3)">Fill in more inputs for detailed reasoning.</div>';

  // JSON
  const reasonTexts = reasoning.slice(0,5).map(r => `  <span class="jvs">"${r.text.split('—')[0].trim()}"</span>`).join(',\n');
  document.getElementById('jsonBody').innerHTML =
`{
  <span class="jk">"signal"</span>: <span class="jvs">"${signal}"</span>,
  <span class="jk">"confidence"</span>: <span class="jvn">${confidence}</span>,
  <span class="jk">"risk_level"</span>: <span class="jvs">"${riskLevel}"</span>,
  <span class="jk">"score"</span>: <span class="jvn">${totalScore}</span>,
  <span class="jk">"inputs_provided"</span>: <span class="jvn">${inputCount}</span>,
  <span class="jk">"reasoning"</span>: [
${reasonTexts}
  ],
  <span class="jk">"decision_rule"</span>: <span class="jvs">"score ≥ +3 → BUY | score ≤ -3 → SELL | else → HOLD"</span>,
  <span class="jk">"disclaimer"</span>: <span class="jvs">"Not financial advice. Decision-support only."</span>
}`;
}

function resetAll() {
  // Clear segmented buttons
  document.querySelectorAll('.seg-btn').forEach(b => b.classList.remove('active-bull','active-bear','active-neu','active-blue'));
  Object.keys(segState).forEach(k => delete segState[k]);

  // Clear inputs
  document.getElementById('currentPrice').value = '';
  document.getElementById('support').value = '';
  document.getElementById('resistance').value = '';
  document.getElementById('rsiSlider').value = 50;
  document.getElementById('rsiVal').textContent = 50;
  document.getElementById('rsiVal').style.color = '';
  document.getElementById('rsiEnabled').checked = true;
  document.getElementById('rsiSlider').disabled = false;
  document.getElementById('rsiVal').style.opacity = 1;

  // Hide results
  document.getElementById('idleCard').style.display = '';
  document.getElementById('resultCards').style.display = 'none';
}

function copyJSON() {
  const txt = document.getElementById('jsonBody').innerText;
  navigator.clipboard?.writeText(txt).then(() => {
    const btn = document.querySelector('.json-copy');
    btn.textContent = 'copied!';
    setTimeout(() => btn.textContent = 'copy', 1500);
  });
}
</script>
</body>
</html>

