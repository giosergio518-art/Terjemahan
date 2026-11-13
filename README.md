<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#4f46e5">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="apple-mobile-web-app-title" content="LinguaFlow">
  <link rel="manifest" href="./manifest.json">
  <link rel="apple-touch-icon" href="https://cdn-icons-png.flaticon.com/512/3898/3898082.png">
  <title>LinguaFlow — Penerjemah Bahasa Asing & Daerah</title>
  <style>
    #lf-wrapper, #lf-wrapper * {
      box-sizing: border-box;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    #lf-wrapper {
      --lf-bg: #f1f5f9;
      --lf-surface: #ffffff;
      --lf-surface-alt: #f8fafc;
      --lf-border: #cbd5e1;
      --lf-text: #0f172a;
      --lf-text-muted: #475569;
      --lf-primary: #4f46e5;
      --lf-primary-hover: #4338ca;
      --lf-badge-bg: #dcfce7;
      --lf-badge-text: #15803d;
      --lf-shadow: 0 10px 25px -5px rgba(15, 23, 42, 0.08);

      background-color: var(--lf-bg);
      color: var(--lf-text);
      min-height: 100vh;
      width: 100%;
      padding: 20px 16px 48px;
      transition: background-color 0.25s ease, color 0.25s ease;
    }

    #lf-wrapper.lf-dark {
      --lf-bg: #0b1120;
      --lf-surface: #1e293b;
      --lf-surface-alt: #0f172a;
      --lf-border: #334155;
      --lf-text: #f8fafc;
      --lf-text-muted: #94a3b8;
      --lf-primary: #6366f1;
      --lf-primary-hover: #818cf8;
      --lf-badge-bg: rgba(34, 197, 94, 0.15);
      --lf-badge-text: #4ade80;
      --lf-shadow: 0 10px 30px -5px rgba(0, 0, 0, 0.5);
    }

    .lf-container {
      max-width: 960px;
      margin: 0 auto;
      width: 100%;
    }

    .lf-header {
      background-color: var(--lf-surface);
      border: 1px solid var(--lf-border);
      border-radius: 16px;
      padding: 16px 20px;
      margin-bottom: 20px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      box-shadow: var(--lf-shadow);
    }

    .lf-brand {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .lf-logo {
      width: 44px;
      height: 44px;
      border-radius: 12px;
      background: linear-gradient(135deg, #4f46e5, #7c3aed);
      color: #ffffff;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      font-size: 18px;
      flex-shrink: 0;
    }

    .lf-title {
      font-size: 20px;
      font-weight: 800;
      color: var(--lf-text);
      line-height: 1.2;
    }

    .lf-subtitle {
      font-size: 12px;
      color: var(--lf-text-muted);
      margin-top: 2px;
    }

    .lf-actions {
      display: flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .lf-btn-install {
      background-color: var(--lf-primary);
      color: #ffffff !important;
      border: none;
      border-radius: 999px;
      padding: 8px 16px;
      font-size: 13px;
      font-weight: 600;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: background 0.2s;
    }

    .lf-btn-install:hover {
      background-color: var(--lf-primary-hover);
    }

    .lf-status {
      background-color: var(--lf-badge-bg);
      color: var(--lf-badge-text);
      font-size: 12px;
      font-weight: 600;
      padding: 7px 12px;
      border-radius: 999px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .lf-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background-color: currentColor;
    }

    .lf-theme-btn {
      background-color: var(--lf-surface-alt);
      color: var(--lf-text);
      border: 1px solid var(--lf-border);
      width: 38px;
      height: 38px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 17px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .lf-card {
      background-color: var(--lf-surface);
      border: 1px solid var(--lf-border);
      border-radius: 18px;
      overflow: hidden;
      box-shadow: var(--lf-shadow);
    }

    .lf-lang-bar {
      display: grid;
      grid-template-columns: 1fr auto 1fr;
      align-items: center;
      gap: 10px;
      padding: 14px 18px;
      background-color: var(--lf-surface-alt);
      border-bottom: 1px solid var(--lf-border);
    }

    .lf-select {
      width: 100%;
      background-color: var(--lf-surface);
      color: var(--lf-text) !important;
      border: 1px solid var(--lf-border);
      border-radius: 10px;
      padding: 10px 12px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      outline: none;
    }

    .lf-select:focus {
      border-color: var(--lf-primary);
    }

    .lf-swap-btn {
      width: 38px;
      height: 38px;
      border-radius: 50%;
      background-color: var(--lf-surface);
      color: var(--lf-text);
      border: 1px solid var(--lf-border);
      cursor: pointer;
      font-size: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: transform 0.2s, border-color 0.2s;
    }

    .lf-swap-btn:hover {
      border-color: var(--lf-primary);
      transform: rotate(180deg);
    }

    .lf-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
    }

    .lf-pane {
      padding: 18px;
      display: flex;
      flex-direction: column;
      min-height: 250px;
    }

    .lf-pane-left {
      background-color: var(--lf-surface);
      border-right: 1px solid var(--lf-border);
    }

    .lf-pane-right {
      background-color: var(--lf-surface-alt);
    }

    .lf-textarea-wrap {
      position: relative;
      flex: 1;
      display: flex;
    }

    .lf-textarea {
      width: 100%;
      min-height: 165px;
      resize: vertical;
      border: none;
      outline: none;
      background: transparent !important;
      color: var(--lf-text) !important;
      font-size: 17px;
      line-height: 1.6;
      padding-right: 32px;
    }

    .lf-textarea::placeholder {
      color: var(--lf-text-muted);
      opacity: 0.75;
    }

    .lf-clear-btn {
      position: absolute;
      top: 0;
      right: 0;
      width: 28px;
      height: 28px;
      border-radius: 8px;
      border: 1px solid var(--lf-border);
      background-color: var(--lf-surface-alt);
      color: var(--lf-text-muted);
      cursor: pointer;
      display: none;
      align-items: center;
      justify-content: center;
      font-size: 14px;
    }

    .lf-output-box {
      flex: 1;
      min-height: 165px;
      font-size: 17px;
      line-height: 1.6;
      color: var(--lf-text);
      white-space: pre-wrap;
      word-break: break-word;
    }

    .lf-placeholder {
      color: var(--lf-text-muted);
      opacity: 0.75;
    }

    .lf-toolbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding-top: 12px;
      margin-top: 12px;
      border-top: 1px solid var(--lf-border);
    }

    .lf-tool-group {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .lf-icon-btn {
      background-color: var(--lf-surface-alt);
      color: var(--lf-text);
      border: 1px solid var(--lf-border);
      border-radius: 8px;
      padding: 7px 11px;
      font-size: 13px;
      font-weight: 500;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 5px;
    }

    .lf-icon-btn:hover {
      border-color: var(--lf-primary);
    }

    .lf-char-count {
      font-size: 12px;
      color: var(--lf-text-muted);
    }

    .lf-translate-btn {
      background-color: var(--lf-primary);
      color: #ffffff !important;
      border: none;
      border-radius: 10px;
      padding: 9px 18px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      transition: background 0.2s;
    }

    .lf-translate-btn:hover {
      background-color: var(--lf-primary-hover);
    }

    .lf-phrases-section {
      margin-top: 22px;
      background-color: var(--lf-surface);
      border: 1px solid var(--lf-border);
      border-radius: 16px;
      padding: 16px 18px;
    }

    .lf-section-title {
      font-size: 13px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: var(--lf-text-muted);
      margin-bottom: 12px;
    }

    .lf-phrases-list {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .lf-phrase-chip {
      background-color: var(--lf-surface-alt);
      color: var(--lf-text);
      border: 1px solid var(--lf-border);
      border-radius: 999px;
      padding: 7px 14px;
      font-size: 13px;
      cursor: pointer;
      transition: border-color 0.2s, transform 0.1s;
    }

    .lf-phrase-chip:hover {
      border-color: var(--lf-primary);
      transform: translateY(-1px);
    }

    .lf-toast {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #0f172a;
      color: #ffffff;
      padding: 10px 18px;
      border-radius: 999px;
      font-size: 13px;
      font-weight: 500;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
      z-index: 99999;
      display: none;
    }

    .lf-modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.6);
      display: none;
      align-items: center;
      justify-content: center;
      padding: 16px;
      z-index: 99999;
    }

    .lf-modal {
      background-color: var(--lf-surface);
      color: var(--lf-text);
      border: 1px solid var(--lf-border);
      border-radius: 16px;
      max-width: 420px;
      width: 100%;
      padding: 20px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
    }

    .lf-modal h3 {
      font-size: 17px;
      margin-bottom: 10px;
    }

    .lf-modal p, .lf-modal li {
      font-size: 13px;
      line-height: 1.6;
      color: var(--lf-text-muted);
      margin-bottom: 8px;
    }

    .lf-modal ul {
      padding-left: 18px;
      margin-bottom: 14px;
    }

    @media (max-width: 720px) {
      .lf-lang-bar {
        grid-template-columns: 1fr;
      }
      .lf-swap-btn {
        justify-self: center;
        transform: rotate(90deg);
      }
      .lf-grid {
        grid-template-columns: 1fr;
      }
      .lf-pane-left {
        border-right: none;
        border-bottom: 1px solid var(--lf-border);
      }
    }
  </style>
</head>
<body>

<div id="lf-wrapper">
  <div class="lf-container">

    <header class="lf-header">
      <div class="lf-brand">
        <div class="lf-logo">A文</div>
        <div>
          <div class="lf-title">LinguaFlow</div>
          <div class="lf-subtitle">Penerjemah Bahasa Asing &amp; Daerah Nusantara</div>
        </div>
      </div>

      <div class="lf-actions">
        <button type="button" id="lf-install-btn" class="lf-btn-install" title="Install Aplikasi ke HP">
          📲 Install Aplikasi
        </button>
        <div class="lf-status">
          <span class="lf-dot"></span>
          <span id="lf-status-text">Siap Menerjemahkan</span>
        </div>
        <button type="button" id="lf-theme-toggle" class="lf-theme-btn" title="Ganti Mode Gelap / Terang">
          🌙
        </button>
      </div>
    </header>

    <main class="lf-card">
      <div class="lf-lang-bar">
        <select id="lf-source-lang" class="lf-select" aria-label="Bahasa Sumber">
          <option value="auto">🌐 Deteksi Bahasa Otomatis</option>
          <optgroup label="Bahasa Utama">
            <option value="id" selected>🇮🇩 Bahasa Indonesia</option>
            <option value="en">🇬🇧 Bahasa Inggris (English)</option>
            <option value="ar">🇸🇦 Bahasa Arab (العربية)</option>
            <option value="ja">🇯🇵 Bahasa Jepang (日本語)</option>
            <option value="ko">🇰🇷 Bahasa Korea (한국어)</option>
            <option value="zh-CN">🇨🇳 Mandarin Sederhana (简体中文)</option>
            <option value="zh-TW">🇹🇼 Mandarin Tradisional (繁體中文)</option>
          </optgroup>
          <optgroup label="Bahasa Daerah Nusantara">
            <option value="jw">🏝️ Bahasa Jawa</option>
            <option value="su">🌿 Bahasa Sunda</option>
            <option value="ban">🌺 Bahasa Bali</option>
            <option value="min">🏠 Bahasa Minangkabau</option>
            <option value="bug">⛵ Bahasa Bugis</option>
            <option value="bbc">📜 Bahasa Batak Toba</option>
            <option value="ace">🕌 Bahasa Aceh</option>
            <option value="bjn">💎 Bahasa Banjar</option>
            <option value="mad">🐂 Bahasa Madura</option>
            <option value="bew">🎭 Bahasa Betawi</option>
          </optgroup>
          <optgroup label="Bahasa Asia & Timur Tengah">
            <option value="ms">🇲🇾 Bahasa Melayu</option>
            <option value="th">🇹🇭 Bahasa Thailand</option>
            <option value="vi">🇻🇳 Bahasa Vietnam</option>
            <option value="tl">🇵🇭 Bahasa Tagalog (Filipina)</option>
            <option value="hi">🇮🇳 Bahasa Hindi</option>
            <option value="ur">🇵🇰 Bahasa Urdu</option>
            <option value="tr">🇹🇷 Bahasa Turki</option>
            <option value="fa">🇮🇷 Bahasa Persia</option>
          </optgroup>
          <optgroup label="Bahasa Eropa & Dunia">
            <option value="es">🇪🇸 Bahasa Spanyol</option>
            <option value="fr">🇫🇷 Bahasa Prancis</option>
            <option value="de">🇩🇪 Bahasa Jerman</option>
            <option value="nl">🇳🇱 Bahasa Belanda</option>
            <option value="ru">🇷🇺 Bahasa Rusia</option>
            <option value="it">🇮🇹 Bahasa Italia</option>
            <option value="pt">🇵🇹 Bahasa Portugis</option>
            <option value="pl">🇵🇱 Bahasa Polandia</option>
            <option value="sv">🇸🇪 Bahasa Swedia</option>
            <option value="el">🇬🇷 Bahasa Yunani</option>
          </optgroup>
        </select>

        <button type="button" id="lf-swap-btn" class="lf-swap-btn" title="Tukar Bahasa">⇄</button>

        <select id="lf-target-lang" class="lf-select" aria-label="Bahasa Tujuan">
          <optgroup label="Bahasa Utama">
            <option value="en" selected>🇬🇧 Bahasa Inggris (English)</option>
            <option value="id">🇮🇩 Bahasa Indonesia</option>
            <option value="ar">🇸🇦 Bahasa Arab (العربية)</option>
            <option value="ja">🇯🇵 Bahasa Jepang (日本語)</option>
            <option value="ko">🇰🇷 Bahasa Korea (한국어)</option>
            <option value="zh-CN">🇨🇳 Mandarin Sederhana (简体中文)</option>
            <option value="zh-TW">🇹🇼 Mandarin Tradisional (繁體中文)</option>
          </optgroup>
          <optgroup label="Bahasa Daerah Nusantara">
            <option value="jw">🏝️ Bahasa Jawa</option>
            <option value="su">🌿 Bahasa Sunda</option>
            <option value="ban">🌺 Bahasa Bali</option>
            <option value="min">🏠 Bahasa Minangkabau</option>
            <option value="bug">⛵ Bahasa Bugis</option>
            <option value="bbc">📜 Bahasa Batak Toba</option>
            <option value="ace">🕌 Bahasa Aceh</option>
            <option value="bjn">💎 Bahasa Banjar</option>
            <option value="mad">🐂 Bahasa Madura</option>
            <option value="bew">🎭 Bahasa Betawi</option>
          </optgroup>
          <optgroup label="Bahasa Asia & Timur Tengah">
            <option value="ms">🇲🇾 Bahasa Melayu</option>
            <option value="th">🇹🇭 Bahasa Thailand</option>
            <option value="vi">🇻🇳 Bahasa Vietnam</option>
            <option value="tl">🇵🇭 Bahasa Tagalog (Filipina)</option>
            <option value="hi">🇮🇳 Bahasa Hindi</option>
            <option value="ur">🇵🇰 Bahasa Urdu</option>
            <option value="tr">🇹🇷 Bahasa Turki</option>
            <option value="fa">🇮🇷 Bahasa Persia</option>
          </optgroup>
          <optgroup label="Bahasa Eropa & Dunia">
            <option value="es">🇪🇸 Bahasa Spanyol</option>
            <option value="fr">🇫🇷 Bahasa Prancis</option>
            <option value="de">🇩🇪 Bahasa Jerman</option>
            <option value="nl">🇳🇱 Bahasa Belanda</option>
            <option value="ru">🇷🇺 Bahasa Rusia</option>
            <option value="it">🇮🇹 Bahasa Italia</option>
            <option value="pt">🇵🇹 Bahasa Portugis</option>
            <option value="pl">🇵🇱 Bahasa Polandia</option>
            <option value="sv">🇸🇪 Bahasa Swedia</option>
            <option value="el">🇬🇷 Bahasa Yunani</option>
          </optgroup>
        </select>
      </div>

      <div class="lf-grid">
        <div class="lf-pane lf-pane-left">
          <div class="lf-textarea-wrap">
            <textarea id="lf-input" class="lf-textarea" maxlength="2000" placeholder="Ketik atau tempel teks di sini..."></textarea>
            <button type="button" id="lf-clear-btn" class="lf-clear-btn" title="Hapus teks">✕</button>
          </div>
          <div class="lf-toolbar">
            <div class="lf-tool-group">
              <button type="button" id="lf-speak-src" class="lf-icon-btn" title="Dengarkan suara">🔊</button>
              <button type="button" id="lf-copy-src" class="lf-icon-btn" title="Salin teks asal">📋</button>
            </div>
            <div class="lf-tool-group">
              <span id="lf-char-count" class="lf-char-count">0 / 2000</span>
              <button type="button" id="lf-translate-btn" class="lf-translate-btn">Terjemahkan →</button>
            </div>
          </div>
        </div>

        <div class="lf-pane lf-pane-right">
          <div id="lf-output" class="lf-output-box">
            <span class="lf-placeholder">Hasil terjemahan akan muncul di sini...</span>
          </div>
          <div class="lf-toolbar">
            <div class="lf-tool-group">
              <button type="button" id="lf-speak-tgt" class="lf-icon-btn" title="Dengarkan hasil terjemahan">🔊 Suara</button>
              <button type="button" id="lf-copy-tgt" class="lf-icon-btn" title="Salin hasil terjemahan">📋 Salin</button>
            </div>
          </div>
        </div>
      </div>
    </main>

    <section class="lf-phrases-section">
      <div class="lf-section-title">Coba Frasa Populer &amp; Bahasa Daerah</div>
      <div class="lf-phrases-list">
        <button type="button" class="lf-phrase-chip" data-src="id" data-tgt="en" data-text="Halo, apa kabar hari ini?">🇮🇩 Halo, apa kabar hari ini?</button>
        <button type="button" class="lf-phrase-chip" data-src="su" data-tgt="id" data-text="Kumaha damang? Abdi bade angkat ka Bandung.">🌿 Kumaha damang? (Sunda)</button>
        <button type="button" class="lf-phrase-chip" data-src="jw" data-tgt="id" data-text="Sugeng enjang, matur nuwun sanget sampun dibantu.">🏝️ Sugeng enjang (Jawa)</button>
        <button type="button" class="lf-phrase-chip" data-src="ban" data-tgt="id" data-text="Om Swastyastu, punapi gatra?">🌺 Punapi gatra? (Bali)</button>
        <button type="button" class="lf-phrase-chip" data-src="min" data-tgt="id" data-text="Baa kaba dunsanak sadonyo?">🏠 Baa kaba dunsanak? (Minang)</button>
        <button type="button" class="lf-phrase-chip" data-src="id" data-tgt="ja" data-text="Terima kasih banyak atas bantuan Anda.">🇯🇵 Terima kasih → Jepang</button>
      </div>
    </section>

  </div>
</div>

<div id="lf-toast" class="lf-toast"></div>

<div id="lf-install-modal" class="lf-modal-overlay">
  <div class="lf-modal">
    <h3>📲 Pasang LinguaFlow ke HP</h3>
    <p>Untuk memasang aplikasi ini ke layar utama HP:</p>
    <ul>
      <li><strong>Android (Chrome):</strong> Ketuk ikon titik tiga <strong>⋮</strong> di kanan atas browser, lalu pilih <strong>"Install aplikasi"</strong> atau <strong>"Tambahkan ke Layar utama"</strong>.</li>
      <li><strong>iPhone (Safari):</strong> Ketuk ikon <strong>Bagikan (Share)</strong> di bawah, lalu pilih <strong>"Tambah ke Layar Utama"</strong>.</li>
    </ul>
    <div style="display:flex; gap:8px; justify-content:flex-end;">
      <button type="button" id="lf-close-modal" class="lf-translate-btn">Mengerti</button>
    </div>
  </div>
</div>

<script>
(function () {
  const wrapper = document.getElementById('lf-wrapper');
  const themeToggle = document.getElementById('lf-theme-toggle');
  const sourceLang = document.getElementById('lf-source-lang');
  const targetLang = document.getElementById('lf-target-lang');
  const swapBtn = document.getElementById('lf-swap-btn');
  const inputEl = document.getElementById('lf-input');
  const outputEl = document.getElementById('lf-output');
  const clearBtn = document.getElementById('lf-clear-btn');
  const charCount = document.getElementById('lf-char-count');
  const translateBtn = document.getElementById('lf-translate-btn');
  const statusText = document.getElementById('lf-status-text');
  const toastEl = document.getElementById('lf-toast');

  let debounceTimer = null;
  let currentTranslation = '';
  let deferredPrompt = null;

  if ('serviceWorker' in navigator) {
    window.addEventListener('load', () => {
      navigator.serviceWorker.register('./sw.js').catch(() => {});
    });
  }

  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault();
    deferredPrompt = e;
    const btn = document.getElementById('lf-install-btn');
    if (btn) btn.style.display = 'inline-flex';
  });

  const installModal = document.getElementById('lf-install-modal');
  document.getElementById('lf-install-btn').addEventListener('click', async () => {
    if (deferredPrompt) {
      deferredPrompt.prompt();
      const { outcome } = await deferredPrompt.userChoice;
      if (outcome === 'accepted') {
        showToast('LinguaFlow sedang dipasang ke HP...');
      }
      deferredPrompt = null;
    } else {
      installModal.style.display = 'flex';
    }
  });

  document.getElementById('lf-close-modal').addEventListener('click', () => {
    installModal.style.display = 'none';
  });

  function applyTheme(dark) {
    if (dark) {
      wrapper.classList.add('lf-dark');
      themeToggle.textContent = '☀️';
      localStorage.setItem('lf_theme', 'dark');
    } else {
      wrapper.classList.remove('lf-dark');
      themeToggle.textContent = '🌙';
      localStorage.setItem('lf_theme', 'light');
    }
  }

  applyTheme(localStorage.getItem('lf_theme') === 'dark');
  themeToggle.addEventListener('click', () => {
    applyTheme(!wrapper.classList.contains('lf-dark'));
  });

  function showToast(msg) {
    toastEl.textContent = msg;
    toastEl.style.display = 'block';
    clearTimeout(toastEl._t);
    toastEl._t = setTimeout(() => {
      toastEl.style.display = 'none';
    }, 2600);
  }

  async function translateText() {
    const text = inputEl.value.trim();
    if (!text) {
      currentTranslation = '';
      outputEl.innerHTML = '<span class="lf-placeholder">Hasil terjemahan akan muncul di sini...</span>';
      return;
    }

    const sl = sourceLang.value;
    const tl = targetLang.value;

    if (sl === tl && sl !== 'auto') {
      currentTranslation = text;
      outputEl.textContent = text;
      return;
    }

    statusText.textContent = 'Menerjemahkan...';
    outputEl.innerHTML = '<span class="lf-placeholder">Sedang menerjemahkan...</span>';

    try {
      const url = `https://translate.googleapis.com/translate_a/single?client=gtx&sl=${encodeURIComponent(sl)}&tl=${encodeURIComponent(tl)}&dt=t&q=${encodeURIComponent(text)}`;
      const res = await fetch(url);
      if (res.ok) {
        const data = await res.json();
        if (data && Array.isArray(data[0])) {
          const result = data[0].map(item => item[0]).join('');
          if (result) {
            currentTranslation = result;
            outputEl.textContent = result;
            statusText.textContent = 'API Utama Aktif';
            return;
          }
        }
      }
    } catch (e) {}

    try {
      const srcCode = sl === 'auto' ? 'id' : sl;
      const pair = `${srcCode}|${tl}`;
      const res2 = await fetch(`https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${encodeURIComponent(pair)}`);
      const data2 = await res2.json();

      if (data2 && data2.responseStatus === 200 && data2.responseData && data2.responseData.translatedText) {
        const translated = data2.responseData.translatedText;
        if (!translated.includes('IS AN INVALID') && !translated.includes('LANGPAIR=')) {
          currentTranslation = translated;
          outputEl.textContent = translated;
          statusText.textContent = 'API Cadangan Aktif';
          return;
        }
      }
      throw new Error();
    } catch (err2) {
      statusText.textContent = 'Periksa Koneksi';
      outputEl.innerHTML = '<span class="lf-placeholder">Pasangan bahasa ini sedang tidak tersedia. Coba bahasa lain.</span>';
    }
  }

  inputEl.addEventListener('input', () => {
    const len = inputEl.value.length;
    charCount.textContent = `${len} / 2000`;
    clearBtn.style.display = len > 0 ? 'flex' : 'none';
    clearTimeout(debounceTimer);
    debounceTimer = setTimeout(translateText, 550);
  });

  clearBtn.addEventListener('click', () => {
    inputEl.value = '';
    charCount.textContent = '0 / 2000';
    clearBtn.style.display = 'none';
    currentTranslation = '';
    outputEl.innerHTML = '<span class="lf-placeholder">Hasil terjemahan akan muncul di sini...</span>';
    inputEl.focus();
  });

  translateBtn.addEventListener('click', translateText);
  sourceLang.addEventListener('change', translateText);
  targetLang.addEventListener('change', translateText);

  swapBtn.addEventListener('click', () => {
    if (sourceLang.value === 'auto') {
      sourceLang.value = targetLang.value;
      targetLang.value = 'id';
    } else {
      const temp = sourceLang.value;
      sourceLang.value = targetLang.value;
      targetLang.value = temp;
    }
    if (currentTranslation) {
      inputEl.value = currentTranslation;
      charCount.textContent = `${inputEl.value.length} / 2000`;
      clearBtn.style.display = inputEl.value.length > 0 ? 'flex' : 'none';
    }
    translateText();
  });

  function speakText(text, lang) {
    if (!text) return showToast('Tidak ada teks untuk dibacakan');
    if (!('speechSynthesis' in window)) return showToast('Browser tidak mendukung suara');
    window.speechSynthesis.cancel();
    const utter = new SpeechSynthesisUtterance(text);
    utter.lang = lang === 'auto' ? 'id-ID' : lang;
    window.speechSynthesis.speak(utter);
  }

  document.getElementById('lf-speak-src').addEventListener('click', () => speakText(inputEl.value.trim(), sourceLang.value));
  document.getElementById('lf-speak-tgt').addEventListener('click', () => speakText(currentTranslation, targetLang.value));

  document.getElementById('lf-copy-src').addEventListener('click', () => {
    if (!inputEl.value.trim()) return;
    navigator.clipboard.writeText(inputEl.value.trim());
    showToast('Teks asal disalin!');
  });

  document.getElementById('lf-copy-tgt').addEventListener('click', () => {
    if (!currentTranslation) return;
    navigator.clipboard.writeText(currentTranslation);
    showToast('Hasil terjemahan disalin!');
  });

  document.querySelectorAll('.lf-phrase-chip').forEach(btn => {
    btn.addEventListener('click', () => {
      sourceLang.value = btn.dataset.src;
      targetLang.value = btn.dataset.tgt;
      inputEl.value = btn.dataset.text;
      charCount.textContent = `${inputEl.value.length} / 2000`;
      clearBtn.style.display = 'flex';
      translateText();
    });
  });
})();
</script>

</body>
</html>
