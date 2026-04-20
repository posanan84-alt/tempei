<!DOCTYPE html>  
<html lang="ja">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">  
<title>TEMPEI MUSIC JOURNEY</title>  
<style>  
/* ========================================  
   RESET & BASE  
======================================== */  
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }  
  
:root {  
  --bg: #0a0a0a;  
  --bg2: #111111;  
  --bg3: #1a1a1a;  
  --text: #e8e4d9;  
  --text2: #8a8680;  
  --text3: #4a4845;  
  --accent: #c8b99a;  
  --accent2: #8a7a5a;  
  --border: rgba(255,255,255,0.08);  
  --border2: rgba(255,255,255,0.15);  
  --font: 'Helvetica Neue', 'Hiragino Kaku Gothic ProN', 'Yu Gothic', sans-serif;  
  --transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1);  
}  
  
html, body {  
  width: 100%; height: 100%;  
  background: var(--bg);  
  color: var(--text);  
  font-family: var(--font);  
  overflow: hidden;  
  -webkit-tap-highlight-color: transparent;  
}  
  
/* ========================================  
   SCREEN SYSTEM  
======================================== */  
.screen {  
  position: fixed; inset: 0;  
  opacity: 0;  
  pointer-events: none;  
  transition: opacity var(--transition);  
  overflow-y: auto;  
  -webkit-overflow-scrolling: touch;  
}  
.screen.active {  
  opacity: 1;  
  pointer-events: all;  
}  
  
/* ========================================  
   OPENING SCREEN  
======================================== */  
#screen-opening {  
  display: flex;  
  flex-direction: column;  
  align-items: center;  
  justify-content: center;  
  background: var(--bg);  
  gap: 0;  
}  
  
.opening-title {  
  font-size: 11px;  
  letter-spacing: 0.35em;  
  color: var(--text2);  
  font-weight: 300;  
  text-transform: uppercase;  
  margin-bottom: 4px;  
  opacity: 0;  
  animation: fadeUp 1.2s 0.5s ease forwards;  
}  
  
.opening-main {  
  font-size: 28px;  
  letter-spacing: 0.12em;  
  color: var(--text);  
  font-weight: 200;  
  text-transform: uppercase;  
  margin-bottom: 72px;  
  opacity: 0;  
  animation: fadeUp 1.2s 0.9s ease forwards;  
}  
  
.opening-menu {  
  display: flex;  
  flex-direction: column;  
  gap: 28px;  
  opacity: 0;  
  animation: fadeUp 1.2s 1.6s ease forwards;  
}  
  
.opening-btn {  
  background: none;  
  border: none;  
  color: var(--text);  
  font-family: var(--font);  
  font-size: 13px;  
  letter-spacing: 0.3em;  
  font-weight: 300;  
  cursor: pointer;  
  display: flex;  
  align-items: center;  
  gap: 12px;  
  padding: 4px 0;  
  transition: color 0.3s, opacity 0.3s;  
  text-transform: uppercase;  
  position: relative;  
}  
  
.opening-btn::after {  
  content: '';  
  position: absolute;  
  bottom: -2px; left: 0; right: 0;  
  height: 1px;  
  background: var(--accent2);  
  transform: scaleX(0);  
  transform-origin: left;  
  transition: transform 0.4s ease;  
}  
  
.opening-btn:hover { color: var(--accent); }  
.opening-btn:hover::after { transform: scaleX(1); }  
  
.opening-btn.dim { color: var(--text3); }  
.opening-btn.dim:hover { color: var(--text2); }  
  
.btn-arrow {  
  color: var(--accent2);  
  font-size: 10px;  
}  
  
.opening-footer {  
  position: absolute;  
  bottom: 40px;  
  font-size: 10px;  
  letter-spacing: 0.2em;  
  color: var(--text3);  
  text-transform: uppercase;  
  opacity: 0;  
  animation: fadeUp 1.2s 2.4s ease forwards;  
}  
  
/* ========================================  
   MAP SCREEN  
======================================== */  
#screen-map {  
  background: var(--bg);  
  display: flex;  
  flex-direction: column;  
}  
  
.map-header {  
  position: fixed;  
  top: 0; left: 0; right: 0;  
  z-index: 10;  
  padding: 56px 28px 20px;  
  background: linear-gradient(to bottom, var(--bg) 60%, transparent);  
  pointer-events: none;  
}  
  
.map-header-label {  
  font-size: 10px;  
  letter-spacing: 0.35em;  
  color: var(--text2);  
  text-transform: uppercase;  
  font-weight: 300;  
}  
  
.map-header-title {  
  font-size: 18px;  
  font-weight: 200;  
  letter-spacing: 0.1em;  
  color: var(--text);  
  margin-top: 4px;  
}  
  
.map-container {  
  flex: 1;  
  position: relative;  
  height: 100vh;  
  overflow: hidden;  
}  
  
/* SVG Japan Map */  
#japan-map {  
  width: 100%;  
  height: 100%;  
  display: block;  
}  
  
/* Map Pins */  
.map-pin-group {  
  cursor: pointer;  
}  
  
.map-pin-group:active .pin-dot {  
  transform: scale(1.4);  
}  
  
.pin-dot {  
  transition: transform 0.2s ease;  
  transform-origin: center;  
}  
  
.pin-pulse {  
  animation: pulse 2.5s ease-out infinite;  
  transform-origin: center;  
}  
  
@keyframes pulse {  
  0% { opacity: 0.7; transform: scale(1); }  
  100% { opacity: 0; transform: scale(2.8); }  
}  
  
.pin-label-bg {  
  transition: opacity 0.2s;  
}  
  
.map-back-btn {  
  position: fixed;  
  bottom: 40px; left: 50%;  
  transform: translateX(-50%);  
  background: none;  
  border: 1px solid var(--border2);  
  color: var(--text2);  
  font-family: var(--font);  
  font-size: 10px;  
  letter-spacing: 0.25em;  
  text-transform: uppercase;  
  padding: 12px 28px;  
  cursor: pointer;  
  transition: color 0.3s, border-color 0.3s;  
  border-radius: 0;  
}  
  
.map-back-btn:hover { color: var(--text); border-color: var(--accent2); }  
  
/* ========================================  
   DETAIL SCREEN  
======================================== */  
#screen-detail {  
  background: var(--bg);  
  min-height: 100vh;  
  display: flex;  
  flex-direction: column;  
}  
  
.detail-hero {  
  width: 100%;  
  aspect-ratio: 3/2;  
  overflow: hidden;  
  position: relative;  
  flex-shrink: 0;  
}  
  
.detail-hero-img {  
  width: 100%;  
  height: 100%;  
  object-fit: cover;  
  opacity: 0;  
  transition: opacity 1.2s ease;  
  display: block;  
}  
  
.detail-hero-img.loaded { opacity: 1; }  
  
.detail-hero-placeholder {  
  position: absolute; inset: 0;  
  background: linear-gradient(160deg, #1a1a1a 0%, #0d0d0d 100%);  
  display: flex;  
  align-items: center;  
  justify-content: center;  
}  
  
.detail-hero-placeholder-text {  
  font-size: 10px;  
  letter-spacing: 0.3em;  
  color: var(--text3);  
  text-transform: uppercase;  
}  
  
.detail-body {  
  flex: 1;  
  padding: 32px 28px 48px;  
  display: flex;  
  flex-direction: column;  
  gap: 0;  
}  
  
.detail-era {  
  font-size: 10px;  
  letter-spacing: 0.35em;  
  color: var(--accent2);  
  text-transform: uppercase;  
  font-weight: 300;  
  margin-bottom: 12px;  
}  
  
.detail-name-en {  
  font-size: 13px;  
  letter-spacing: 0.25em;  
  color: var(--text2);  
  text-transform: uppercase;  
  font-weight: 300;  
  margin-bottom: 6px;  
}  
  
.detail-name {  
  font-size: 30px;  
  font-weight: 200;  
  letter-spacing: 0.06em;  
  color: var(--text);  
  line-height: 1.2;  
  margin-bottom: 20px;  
}  
  
.detail-divider {  
  width: 40px;  
  height: 1px;  
  background: var(--accent2);  
  margin-bottom: 20px;  
}  
  
.detail-intro {  
  font-size: 14px;  
  letter-spacing: 0.05em;  
  color: var(--text);  
  font-weight: 300;  
  line-height: 1.8;  
  margin-bottom: 8px;  
}  
  
.detail-desc {  
  font-size: 12px;  
  letter-spacing: 0.04em;  
  color: var(--text2);  
  font-weight: 300;  
  line-height: 1.9;  
  margin-bottom: 36px;  
}  
  
/* YouTube embed */  
.detail-video-wrap {  
  width: 100%;  
  aspect-ratio: 16/9;  
  background: #000;  
  margin-bottom: 40px;  
  position: relative;  
  overflow: hidden;  
}  
  
.detail-video-placeholder {  
  width: 100%;  
  height: 100%;  
  display: flex;  
  flex-direction: column;  
  align-items: center;  
  justify-content: center;  
  gap: 10px;  
  background: var(--bg3);  
  border: 1px solid var(--border);  
}  
  
.detail-video-placeholder p {  
  font-size: 11px;  
  letter-spacing: 0.2em;  
  color: var(--text3);  
  text-transform: uppercase;  
}  
  
.detail-video-placeholder span {  
  font-size: 10px;  
  color: var(--text3);  
  letter-spacing: 0.1em;  
}  
  
.detail-video-wrap iframe {  
  position: absolute; inset: 0;  
  width: 100%; height: 100%;  
  border: none;  
}  
  
/* Action buttons */  
.detail-actions {  
  display: flex;  
  flex-direction: column;  
  gap: 16px;  
}  
  
.detail-btn {  
  background: none;  
  border: 1px solid var(--border);  
  color: var(--text2);  
  font-family: var(--font);  
  font-size: 11px;  
  letter-spacing: 0.3em;  
  text-transform: uppercase;  
  padding: 18px 24px;  
  cursor: pointer;  
  transition: color 0.3s, border-color 0.3s, background 0.3s;  
  text-align: left;  
  display: flex;  
  align-items: center;  
  justify-content: space-between;  
  font-weight: 300;  
}  
  
.detail-btn.primary {  
  border-color: var(--accent2);  
  color: var(--accent);  
}  
  
.detail-btn:hover {  
  border-color: var(--accent2);  
  color: var(--text);  
  background: rgba(255,255,255,0.02);  
}  
  
.detail-btn-arrow {  
  color: var(--accent2);  
  font-size: 14px;  
  font-weight: 300;  
}  
  
/* ========================================  
   AMBIENT NOTE  
======================================== */  
.detail-ambient {  
  margin-top: 48px;  
  padding-top: 24px;  
  border-top: 1px solid var(--border);  
}  
  
.detail-ambient p {  
  font-size: 11px;  
  letter-spacing: 0.15em;  
  color: var(--text3);  
  font-weight: 300;  
  line-height: 1.8;  
  font-style: italic;  
}  
  
/* ========================================  
   LOADING  
======================================== */  
#loading {  
  position: fixed; inset: 0;  
  background: var(--bg);  
  display: flex;  
  align-items: center;  
  justify-content: center;  
  z-index: 100;  
  transition: opacity 0.8s ease;  
}  
  
#loading.hide {  
  opacity: 0;  
  pointer-events: none;  
}  
  
.loading-dot {  
  width: 4px; height: 4px;  
  background: var(--text3);  
  border-radius: 50%;  
  animation: loadDot 1.4s ease-in-out infinite;  
}  
  
@keyframes loadDot {  
  0%, 80%, 100% { opacity: 0.2; transform: scale(0.8); }  
  40% { opacity: 1; transform: scale(1); }  
}  
  
/* ========================================  
   TOAST NOTIFICATION  
======================================== */  
.toast {  
  position: fixed;  
  bottom: 100px; left: 50%;  
  transform: translateX(-50%) translateY(20px);  
  background: var(--bg3);  
  border: 1px solid var(--border2);  
  color: var(--text2);  
  font-size: 11px;  
  letter-spacing: 0.15em;  
  padding: 12px 20px;  
  opacity: 0;  
  transition: opacity 0.4s, transform 0.4s;  
  pointer-events: none;  
  white-space: nowrap;  
  z-index: 50;  
}  
  
.toast.show {  
  opacity: 1;  
  transform: translateX(-50%) translateY(0);  
}  
  
/* ========================================  
   ANIMATIONS  
======================================== */  
@keyframes fadeUp {  
  from { opacity: 0; transform: translateY(16px); }  
  to { opacity: 1; transform: translateY(0); }  
}  
  
.fade-in {  
  animation: fadeUp 0.7s ease forwards;  
}  
  
/* ========================================  
   SCROLLBAR (hide on mobile)  
======================================== */  
.screen::-webkit-scrollbar { display: none; }  
.screen { scrollbar-width: none; }  
  
/* ========================================  
   SAFE AREA (iPhone notch)  
======================================== */  
@supports (padding-top: env(safe-area-inset-top)) {  
  .map-header { padding-top: calc(env(safe-area-inset-top) + 20px); }  
  .map-back-btn { bottom: calc(env(safe-area-inset-bottom) + 28px); }  
  #screen-opening .opening-footer { bottom: calc(env(safe-area-inset-bottom) + 28px); }  
}  
</style>  
</head>  
<body>  
  
<!-- ========================================  
     LOADING  
======================================== -->  
<div id="loading">  
  <div class="loading-dot"></div>  
</div>  
  
<!-- ========================================  
     TOAST  
======================================== -->  
<div class="toast" id="toast"></div>  
  
<!-- ========================================  
     OPENING SCREEN  
======================================== -->  
<div class="screen active" id="screen-opening">  
  <p class="opening-title">A Piano Journey by</p>  
  <h1 class="opening-main">Tempei Nakamura</h1>  
  <nav class="opening-menu">  
    <button class="opening-btn" id="btn-start" onclick="startNewJourney()">  
      <span class="btn-arrow">▶</span>  
      Start a New Journey  
    </button>  
    <button class="opening-btn dim" id="btn-continue" onclick="continueJourney()">  
      <span class="btn-arrow">▶</span>  
      Continue  
    </button>  
  </nav>  
  <p class="opening-footer">Tempei Music Journey</p>  
</div>  
  
<!-- ========================================  
     MAP SCREEN  
======================================== -->  
<div class="screen" id="screen-map">  
  <div class="map-header">  
    <p class="map-header-label">Select a destination</p>  
    <h2 class="map-header-title">Japan Chapter</h2>  
  </div>  
  
  <div class="map-container">  
    <!-- SVG Japan Map + Pins -->  
    <svg id="japan-map" viewBox="0 0 400 520" xmlns="http://www.w3.org/2000/svg">  
      <!-- Japan simplified outline (stylized) -->  
      <defs>  
        <filter id="glow-pin">  
          <feGaussianBlur stdDeviation="2" result="blur"/>  
          <feComposite in="SourceGraphic" in2="blur" operator="over"/>  
        </filter>  
      </defs>  
  
      <!-- Background ocean hint -->  
      <rect width="400" height="520" fill="var(--bg)"/>  
  
      <!-- Hokkaido -->  
      <path d="M190,30 L220,28 L255,40 L270,55 L265,75 L248,88 L230,90 L210,85 L195,72 L185,58 L183,42 Z"  
        fill="#1e1e1e" stroke="#2a2a2a" stroke-width="1"/>  
  
      <!-- Honshu (main island) - simplified -->  
      <path d="M155,95 L175,90 L200,92 L225,95 L260,100 L290,115 L305,132 L310,152 L302,175 L288,195 L275,210 L268,235 L270,260 L265,278 L255,295 L240,305 L228,310 L215,315 L205,318 L195,316 L182,310 L170,298 L162,280 L158,258 L155,235 L150,210 L145,188 L142,165 L140,142 L142,120 L148,105 Z"  
        fill="#1c1c1c" stroke="#282828" stroke-width="1"/>  
  
      <!-- Shikoku -->  
      <path d="M195,325 L218,320 L238,325 L248,338 L242,352 L225,358 L208,355 L196,343 L193,332 Z"  
        fill="#1a1a1a" stroke="#252525" stroke-width="1"/>  
  
      <!-- Kyushu -->  
      <path d="M148,305 L165,295 L175,300 L178,318 L172,338 L160,352 L148,356 L138,348 L132,332 L135,318 L142,308 Z"  
        fill="#1a1a1a" stroke="#252525" stroke-width="1"/>  
  
      <!-- Ryukyu hint -->  
      <ellipse cx="145" cy="390" rx="6" ry="4" fill="#161616" stroke="#222" stroke-width="0.5"/>  
      <ellipse cx="132" cy="408" rx="5" ry="3" fill="#161616" stroke="#222" stroke-width="0.5"/>  
      <ellipse cx="120" cy="424" rx="5" ry="3" fill="#161616" stroke="#222" stroke-width="0.5"/>  
  
      <!-- === MAP PINS === -->  
      <!-- Will be injected by JS -->  
      <g id="map-pins"></g>  
    </svg>  
  </div>  
  
  <button class="map-back-btn" onclick="showScreen('opening')">← Back</button>  
</div>  
  
<!-- ========================================  
     DETAIL SCREEN  
======================================== -->  
<div class="screen" id="screen-detail">  
  <!-- Hero image -->  
  <div class="detail-hero" id="detail-hero">  
    <div class="detail-hero-placeholder" id="detail-hero-placeholder">  
      <p class="detail-hero-placeholder-text">Loading image…</p>  
    </div>  
    <img class="detail-hero-img" id="detail-img" src="" alt="" onload="this.classList.add('loaded')">  
  </div>  
  
  <!-- Body content -->  
  <div class="detail-body" id="detail-body">  
    <p class="detail-era" id="detail-era"></p>  
    <p class="detail-name-en" id="detail-name-en"></p>  
    <h2 class="detail-name" id="detail-name"></h2>  
    <div class="detail-divider"></div>  
    <p class="detail-intro" id="detail-intro"></p>  
    <p class="detail-desc" id="detail-desc"></p>  
  
    <!-- Video -->  
    <div class="detail-video-wrap" id="detail-video-wrap">  
      <div class="detail-video-placeholder" id="detail-video-placeholder">  
        <p>Video</p>  
        <span>Tap play to watch</span>  
      </div>  
    </div>  
  
    <!-- Actions -->  
    <div class="detail-actions">  
      <button class="detail-btn primary" id="btn-play-video" onclick="playVideo()">  
        <span>Play Video</span>  
        <span class="detail-btn-arrow">▶</span>  
      </button>  
      <button class="detail-btn" id="btn-next" onclick="goNext()">  
        <span>Next Destination</span>  
        <span class="detail-btn-arrow">→</span>  
      </button>  
      <button class="detail-btn" onclick="showScreen('map')">  
        <span>Back to Map</span>  
        <span class="detail-btn-arrow">↩</span>  
      </button>  
    </div>  
  
    <!-- Ambient note -->  
    <div class="detail-ambient" id="detail-ambient">  
      <p id="detail-ambient-text"></p>  
    </div>  
  </div>  
</div>  
  
<!-- ========================================  
     JAVASCRIPT  
======================================== -->  
<script>  
// ================================================  
// CONFIG  
// ================================================  
  
// GASをデプロイしたら、以下のURLを差し替えてください  
const GAS_URL = 'https://script.google.com/macros/s/AKfycbza39yZvhrfxn4LNk2JB-2nFAI2czQgRi3B0Y6h2pmEdTyU-fDZkWxAO3droUt_zIAeJA/exec';  
  
// GASが未設定の場合のフォールバックデータ  
const FALLBACK_DATA = [  
  {  
    location_id: 'JP_KUMANO',  
    country_group: '日本',  
    country: '日本',  
    region: '三重県',  
    location_name: '熊野市',  
    location_name_en: 'Kumano',  
    latitude: 33.888,  
    longitude: 136.100,  
    category: 'nature',  
    display_order: 1,  
    is_active: true,  
    intro_text: '音が消える場所',  
    description_short: '海と祈りの気配が残る場所',  
    hero_image_url: '',  
    youtube_embed_url: '',  
    music_id: 'MUSIC_001',  
    ambient_note: '波音と風の印象',  
    era_label: 'Japan Chapter',  
    unlock_order: 1  
  },  
  {  
    location_id: 'JP_HOKKAIDO',  
    country_group: '日本',  
    country: '日本',  
    region: '北海道',  
    location_name: '北海道',  
    location_name_en: 'Hokkaido',  
    latitude: 43.064,  
    longitude: 141.347,  
    category: 'nature',  
    display_order: 2,  
    is_active: true,  
    intro_text: 'どこまでも続く音',  
    description_short: '広がる景色の中に音が溶けていく場所',  
    hero_image_url: '',  
    youtube_embed_url: '',  
    music_id: 'MUSIC_002',  
    ambient_note: '風と遠さの印象',  
    era_label: 'Japan Chapter',  
    unlock_order: 2  
  },  
  {  
    location_id: 'JP_YAMANASHI',  
    country_group: '日本',  
    country: '日本',  
    region: '山梨県',  
    location_name: '河口湖町',  
    location_name_en: 'Yamanashi',  
    latitude: 35.4899,  
    longitude: 138.7633,  
    category: 'nature',  
    display_order: 3,  
    is_active: true,  
    intro_text: '音がぶつかる場所',  
    description_short: '河口湖から望む雄大な富士の威厳を感じる場所',  
    hero_image_url: '',  
    youtube_embed_url: '',  
    music_id: 'MUSIC_003',  
    ambient_note: '荘厳な富士の印象',  
    era_label: 'Japan Chapter',  
    unlock_order: 3  
  }  
];  
  
// ================================================  
// STATE  
// ================================================  
let locations = [];  
let currentLocationId = null;  
let currentVideoEmbedUrl = null;  
  
// ================================================  
// PIN POSITIONS (SVG座標 - SVGの地図に合わせた相対位置)  
// 経緯度からSVG座標へのマッピング  
// ================================================  
function latLonToSVG(lat, lon) {  
  // 日本の範囲: lat 24-46, lon 122-146  
  const LAT_MAX = 46, LAT_MIN = 24;  
  const LON_MIN = 124, LON_MAX = 146;  
  const SVG_W = 400, SVG_H = 520;  
  const MARGIN = 30;  
  
  const x = MARGIN + ((lon - LON_MIN) / (LON_MAX - LON_MIN)) * (SVG_W - MARGIN * 2);  
  const y = MARGIN + ((LAT_MAX - lat) / (LAT_MAX - LAT_MIN)) * (SVG_H - MARGIN * 2);  
  return { x: Math.round(x), y: Math.round(y) };  
}  
  
// ================================================  
// INIT  
// ================================================  
window.addEventListener('DOMContentLoaded', async () => {  
  await loadLocations();  
  checkContinue();  
  setTimeout(() => {  
    document.getElementById('loading').classList.add('hide');  
  }, 800);  
});  
  
async function loadLocations() {  
  if (GAS_URL === 'YOUR_GAS_DEPLOYMENT_URL_HERE') {  
    locations = FALLBACK_DATA;  
    renderMapPins();  
    return;  
  }  
  
  try {  
    const res = await fetch(GAS_URL);  
    const json = await res.json();  
    if (json.locations && json.locations.length > 0) {  
      locations = json.locations;  
    } else {  
      locations = FALLBACK_DATA;  
    }  
  } catch (e) {  
    console.warn('GAS fetch failed, using fallback data', e);  
    locations = FALLBACK_DATA;  
  }  
  renderMapPins();  
}  
  
// ================================================  
// CONTINUE CHECK  
// ================================================  
function checkContinue() {  
  const saved = localStorage.getItem('tempei_last_location');  
  const btn = document.getElementById('btn-continue');  
  if (saved && locations.find(l => l.location_id === saved)) {  
    btn.classList.remove('dim');  
  } else {  
    btn.classList.add('dim');  
  }  
}  
  
// ================================================  
// SCREEN NAVIGATION  
// ================================================  
function showScreen(name) {  
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));  
  const target = document.getElementById('screen-' + name);  
  if (target) {  
    target.classList.add('active');  
    target.scrollTop = 0;  
  }  
}  
  
// ================================================  
// OPENING ACTIONS  
// ================================================  
function startNewJourney() {  
  showScreen('map');  
  setTimeout(() => {  
    const first = locations.find(l => l.unlock_order == 1) || locations[0];  
    if (first) showDetail(first.location_id);  
  }, 400);  
}  
  
function continueJourney() {  
  const saved = localStorage.getItem('tempei_last_location');  
  if (saved && locations.find(l => l.location_id === saved)) {  
    showScreen('map');  
    setTimeout(() => showDetail(saved), 400);  
  } else {  
    showToast('No saved journey. Start a new one.');  
    startNewJourney();  
  }  
}  
  
// ================================================  
// MAP PINS  
// ================================================  
function renderMapPins() {  
  const container = document.getElementById('map-pins');  
  container.innerHTML = '';  
  
  locations.forEach(loc => {  
    const pos = latLonToSVG(Number(loc.latitude), Number(loc.longitude));  
  
    const g = document.createElementNS('http://www.w3.org/2000/svg', 'g');  
    g.setAttribute('class', 'map-pin-group');  
    g.setAttribute('onclick', `showDetail('${loc.location_id}')`);  
  
    // pulse circle  
    const pulse = document.createElementNS('http://www.w3.org/2000/svg', 'circle');  
    pulse.setAttribute('cx', pos.x);  
    pulse.setAttribute('cy', pos.y);  
    pulse.setAttribute('r', '8');  
    pulse.setAttribute('fill', 'none');  
    pulse.setAttribute('stroke', '#c8b99a');  
    pulse.setAttribute('stroke-width', '1');  
    pulse.setAttribute('class', 'pin-pulse');  
    pulse.style.animationDelay = Math.random() * 2 + 's';  
  
    // dot  
    const dot = document.createElementNS('http://www.w3.org/2000/svg', 'circle');  
    dot.setAttribute('cx', pos.x);  
    dot.setAttribute('cy', pos.y);  
    dot.setAttribute('r', '4');  
    dot.setAttribute('fill', '#c8b99a');  
    dot.setAttribute('class', 'pin-dot');  
  
    // label background  
    const labelW = 68, labelH = 16;  
    const lx = pos.x - labelW / 2;  
    const ly = pos.y + 10;  
    const rect = document.createElementNS('http://www.w3.org/2000/svg', 'rect');  
    rect.setAttribute('x', lx);  
    rect.setAttribute('y', ly);  
    rect.setAttribute('width', labelW);  
    rect.setAttribute('height', labelH);  
    rect.setAttribute('rx', '2');  
    rect.setAttribute('fill', 'rgba(10,10,10,0.8)');  
  
    // label text  
    const text = document.createElementNS('http://www.w3.org/2000/svg', 'text');  
    text.setAttribute('x', pos.x);  
    text.setAttribute('y', ly + 11);  
    text.setAttribute('text-anchor', 'middle');  
    text.setAttribute('font-size', '9');  
    text.setAttribute('font-family', 'Helvetica Neue, sans-serif');  
    text.setAttribute('letter-spacing', '1');  
    text.setAttribute('fill', '#8a8680');  
    text.textContent = loc.location_name_en.toUpperCase();  
  
    g.appendChild(pulse);  
    g.appendChild(dot);  
    g.appendChild(rect);  
    g.appendChild(text);  
    container.appendChild(g);  
  });  
}  
  
// ================================================  
// DETAIL  
// ================================================  
function showDetail(locationId) {  
  const loc = locations.find(l => l.location_id === locationId);  
  if (!loc) return;  
  
  currentLocationId = locationId;  
  currentVideoEmbedUrl = loc.youtube_embed_url || '';  
  
  // Save to localStorage  
  localStorage.setItem('tempei_last_location', locationId);  
  
  // Populate fields  
  document.getElementById('detail-era').textContent = loc.era_label || 'Japan Chapter';  
  document.getElementById('detail-name-en').textContent = loc.location_name_en || '';  
  document.getElementById('detail-name').textContent = loc.location_name || '';  
  document.getElementById('detail-intro').textContent = loc.intro_text || '';  
  document.getElementById('detail-desc').textContent = loc.description_short || '';  
  document.getElementById('detail-ambient-text').textContent = loc.ambient_note ? '— ' + loc.ambient_note : '';  
  
  // Hero image  
  const img = document.getElementById('detail-img');  
  const placeholder = document.getElementById('detail-hero-placeholder');  
  img.classList.remove('loaded');  
  if (loc.hero_image_url && loc.hero_image_url.startsWith('http')) {  
    img.src = loc.hero_image_url;  
    img.alt = loc.location_name;  
    placeholder.style.display = 'none';  
    img.style.display = 'block';  
  } else {  
    img.style.display = 'none';  
    placeholder.style.display = 'flex';  
    placeholder.querySelector('p').textContent = loc.location_name;  
  }  
  
  // Video - reset (autoplay off)  
  const videoWrap = document.getElementById('detail-video-wrap');  
  const videoPlaceholder = document.getElementById('detail-video-placeholder');  
  const existingIframe = videoWrap.querySelector('iframe');  
  if (existingIframe) existingIframe.remove();  
  videoPlaceholder.style.display = 'flex';  
  videoPlaceholder.querySelector('p').textContent = 'Video';  
  videoPlaceholder.querySelector('span').textContent = loc.location_name || 'Tap play to watch';  
  
  // Next button label  
  const nextLoc = getNextLocation(locationId);  
  const nextBtn = document.getElementById('btn-next');  
  if (nextLoc) {  
    nextBtn.querySelector('span:first-child').textContent = 'Next: ' + nextLoc.location_name_en;  
    nextBtn.style.display = 'flex';  
  } else {  
    nextBtn.style.display = 'none';  
  }  
  
  showScreen('detail');  
  checkContinue();  
}  
  
// ================================================  
// VIDEO PLAY  
// ================================================  
function playVideo() {  
  if (!currentVideoEmbedUrl || !currentVideoEmbedUrl.startsWith('http')) {  
    showToast('Video URL is not set yet');  
    return;  
  }  
  
  const videoWrap = document.getElementById('detail-video-wrap');  
  const placeholder = document.getElementById('detail-video-placeholder');  
  
  // Build iframe  
  let src = currentVideoEmbedUrl;  
  if (!src.includes('autoplay=')) {  
    src += (src.includes('?') ? '&' : '?') + 'autoplay=1&rel=0';  
  }  
  
  const iframe = document.createElement('iframe');  
  iframe.src = src;  
  iframe.allow = 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture';  
  iframe.allowFullscreen = true;  
  
  placeholder.style.display = 'none';  
  videoWrap.appendChild(iframe);  
}  
  
// ================================================  
// NEXT LOCATION  
// ================================================  
function getNextLocation(currentId) {  
  const current = locations.find(l => l.location_id === currentId);  
  if (!current) return null;  
  const currentOrder = Number(current.unlock_order);  
  const next = locations  
    .filter(l => Number(l.unlock_order) > currentOrder)  
    .sort((a, b) => Number(a.unlock_order) - Number(b.unlock_order))[0];  
  return next || null;  
}  
  
function goNext() {  
  const next = getNextLocation(currentLocationId);  
  if (next) {  
    showDetail(next.location_id);  
  } else {  
    showToast('This is the last destination');  
  }  
}  
  
// ================================================  
// TOAST  
// ================================================  
function showToast(msg) {  
  const toast = document.getElementById('toast');  
  toast.textContent = msg;  
  toast.classList.add('show');  
  setTimeout(() => toast.classList.remove('show'), 2500);  
}  
</script>  
</body>  
</html>  
