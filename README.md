<!-- ... existing code ... -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="theme-color" content="#4f46e5" id="meta-theme-color">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="LinguaFlow">
    <title>LinguaFlow - Penerjemah Bahasa Asing & Daerah</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
<!-- ... existing code ... -->
    <script>
        // Terapkan tema sebelum halaman dirender untuk menghindari kedipan (FOUC)
        if (localStorage.getItem('linguaflow_theme') === 'dark' || 
           (!('linguaflow_theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    </script>

    <!-- CSS Variabel & Perlindungan Kontras Tinggi (Mencegah bentrok dengan CSS bawaan CMS/tema) -->
    <style>
        :root {
            --lf-bg-body: #f8fafc;
            --lf-bg-card: #ffffff;
            --lf-bg-subcard: #f1f5f9;
            --lf-bg-input: #ffffff;
            --lf-bg-output: #f8fafc;
            --lf-text-main: #0f172a;
            --lf-text-secondary: #334155;
            --lf-text-muted: #64748b;
            --lf-placeholder: #94a3b8;
            --lf-border: #cbd5e1;
        }

        html.dark {
            --lf-bg-body: #020617;
            --lf-bg-card: #0f172a;
            --lf-bg-subcard: #1e293b;
            --lf-bg-input: #0f172a;
            --lf-bg-output: #131c31;
            --lf-text-main: #f8fafc;
            --lf-text-secondary: #e2e8f0;
            --lf-text-muted: #94a3b8;
            --lf-placeholder: #64748b;
            --lf-border: #334155;
        }

        body.lf-app {
            background-color: var(--lf-bg-body) !important;
            color: var(--lf-text-main) !important;
        }

        .lf-card {
            background-color: var(--lf-bg-card) !important;
            border-color: var(--lf-border) !important;
        }

        .lf-subcard {
            background-color: var(--lf-bg-subcard) !important;
            border-color: var(--lf-border) !important;
        }

        .lf-input-box {
            background-color: var(--lf-bg-input) !important;
        }

        .lf-output-box {
            background-color: var(--lf-bg-output) !important;
        }

        #linguaflow-root textarea.lf-textarea {
            background-color: transparent !important;
            color: var(--lf-text-main) !important;
            caret-color: #6366f1 !important;
        }

        #linguaflow-root textarea.lf-textarea::placeholder {
            color: var(--lf-placeholder) !important;
            opacity: 1 !important;
        }

        #linguaflow-root select.lf-select {
            background-color: var(--lf-bg-card) !important;
            color: var(--lf-text-main) !important;
            border-color: var(--lf-border) !important;
        }

        #linguaflow-root select.lf-select option,
        #linguaflow-root select.lf-select optgroup {
            background-color: var(--lf-bg-card) !important;
            color: var(--lf-text-main) !important;
        }
    </style>
</head>
<body id="linguaflow-root" class="lf-app font-sans min-h-screen flex flex-col justify-between transition-colors duration-300 selection:bg-indigo-100 selection:text-indigo-700 dark:selection:bg-indigo-900 dark:selection:text-indigo-200">

    <!-- Navbar / Header -->
    <header class="lf-card backdrop-blur-md border-b sticky top-0 z-30 shadow-sm transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-2">
            <div class="flex items-center gap-3 min-w-0">
                <div class="w-10 h-10 shrink-0 rounded-xl bg-gradient-to-tr from-indigo-600 to-blue-500 flex items-center justify-center text-white shadow-md shadow-indigo-200 dark:shadow-indigo-950/50">
                    <i class="fa-solid fa-language text-xl"></i>
                </div>
                <div class="truncate">
                    <h1 class="text-lg sm:text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-blue-600 dark:from-indigo-400 dark:to-blue-400 truncate">
                        LinguaFlow
                    </h1>
                    <p class="text-[11px] text-slate-500 dark:text-slate-400 font-medium -mt-0.5 hidden sm:block">Penerjemah Bahasa Asing & Daerah</p>
                </div>
            </div>

            <div class="flex items-center gap-2 sm:gap-2.5 shrink-0">
                <!-- Tombol Install Aplikasi (PWA) -->
                <button id="install-app-btn" type="button" title="Pasang Aplikasi ke HP / Perangkat" class="inline-flex items-center gap-1.5 px-3 py-2 rounded-xl text-xs font-semibold bg-indigo-600 hover:bg-indigo-700 text-white shadow-sm shadow-indigo-500/20 transition-all active:scale-95">
                    <i class="fa-solid fa-download"></i>
                    <span>Install App</span>
                </button>

                <span class="hidden md:inline-flex items-center gap-1.5 px-3 py-1.5 rounded-full text-xs font-medium bg-indigo-50 dark:bg-indigo-950/80 text-indigo-700 dark:text-indigo-300 border border-indigo-200 dark:border-indigo-800">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                    Multi-API Aktif
                </span>

                <!-- Tombol Toggle Mode Gelap / Terang -->
                <button id="theme-toggle" type="button" title="Ubah Tema Gelap / Terang" aria-label="Toggle Dark Mode" class="w-10 h-10 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-indigo-100 dark:hover:bg-slate-700 text-slate-700 dark:text-amber-400 border border-slate-300 dark:border-slate-700 flex items-center justify-center transition-all duration-200 active:scale-95 focus:outline-none focus:ring-2 focus:ring-indigo-400">
                    <i id="theme-icon-dark" class="fa-solid fa-moon text-base dark:hidden"></i>
                    <i id="theme-icon-light" class="fa-solid fa-sun text-base hidden dark:inline"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-grow max-w-6xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-10">
        
        <!-- Kartu Utama Penerjemah -->
        <div class="lf-card rounded-2xl shadow-xl shadow-slate-200/60 dark:shadow-black/50 border overflow-hidden transition-colors duration-300">
            
            <!-- Bar Pemilihan Bahasa -->
            <div class="lf-subcard border-b p-3 sm:p-4 flex flex-col sm:flex-row items-center justify-between gap-3">
                
                <!-- Bahasa Sumber -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="source-lang" class="sr-only">Bahasa Sumber</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-globe text-indigo-600 dark:text-indigo-400 absolute left-3.5 pointer-events-none z-10"></i>
                        <select id="source-lang" class="lf-select w-full pl-10 pr-8 py-2.5 border hover:border-indigo-400 dark:hover:border-indigo-500 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 dark:focus:ring-indigo-900 rounded-xl text-sm font-semibold transition-all cursor-pointer appearance-none outline-none">
                            <option value="auto" selected>✨ Deteksi Otomatis</option>
                            
                            <optgroup label="🇮🇩 Bahasa Nasional & Daerah Nusantara">
                                <option value="id">🇮🇩 Bahasa Indonesia</option>
                                <option value="jv">🏺 Bahasa Jawa (Jawa)</option>
                                <option value="su">🌿 Bahasa Sunda (Sunda)</option>
                                <option value="ban">🌺 Bahasa Bali (Bali)</option>
                                <option value="min">🏠 Bahasa Minangkabau</option>
                                <option value="bug">⛵ Bahasa Bugis</option>
                                <option value="mak">⚓ Bahasa Makassar</option>
                                <option value="btx">🧣 Bahasa Batak Toba</option>
                                <option value="ace">🕌 Bahasa Aceh</option>
                                <option value="bjn">💎 Bahasa Banjar</option>
                                <option value="mad">🐂 Bahasa Madura</option>
                                <option value="bew">🎭 Bahasa Betawi</option>
                                <option value="sas">🏝️ Bahasa Sasak (Lombok)</option>
                            </optgroup>

                            <optgroup label="🌏 Bahasa Asia">
<!-- ... existing code ... -->
                <!-- Tombol Tukar Bahasa (Swap) -->
                <div class="flex justify-center">
                    <button id="swap-btn" type="button" title="Tukar Bahasa" class="lf-card w-10 h-10 rounded-full border hover:border-indigo-400 dark:hover:border-indigo-500 hover:bg-indigo-50 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-400 flex items-center justify-center shadow-sm transition-all duration-200 active:scale-95 focus:outline-none focus:ring-2 focus:ring-indigo-300 dark:focus:ring-indigo-800">
                        <i class="fa-solid fa-right-left text-sm transition-transform duration-300" id="swap-icon"></i>
                    </button>
                </div>

                <!-- Bahasa Target -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="target-lang" class="sr-only">Bahasa Target</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-flag text-blue-600 dark:text-blue-400 absolute left-3.5 pointer-events-none z-10"></i>
                        <select id="target-lang" class="lf-select w-full pl-10 pr-8 py-2.5 border hover:border-indigo-400 dark:hover:border-indigo-500 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 dark:focus:ring-indigo-900 rounded-xl text-sm font-semibold transition-all cursor-pointer appearance-none outline-none">
                            <optgroup label="🌏 Bahasa Populer">
                                <option value="en" selected>🇬🇧 Bahasa Inggris</option>
                                <option value="id">🇮🇩 Bahasa Indonesia</option>
                                <option value="ja">🇯🇵 Bahasa Jepang</option>
                                <option value="ko">🇰🇷 Bahasa Korea</option>
                                <option value="ar">🇸🇦 Bahasa Arab</option>
                                <option value="zh-CN">🇨🇳 Mandarin (Sederhana)</option>
                            </optgroup>

                            <optgroup label="🇮🇩 Bahasa Daerah Nusantara">
                                <option value="jv">🏺 Bahasa Jawa (Jawa)</option>
                                <option value="su">🌿 Bahasa Sunda (Sunda)</option>
                                <option value="ban">🌺 Bahasa Bali (Bali)</option>
                                <option value="min">🏠 Bahasa Minangkabau</option>
                                <option value="bug">⛵ Bahasa Bugis</option>
                                <option value="mak">⚓ Bahasa Makassar</option>
                                <option value="btx">🧣 Bahasa Batak Toba</option>
                                <option value="ace">🕌 Bahasa Aceh</option>
                                <option value="bjn">💎 Bahasa Banjar</option>
                                <option value="mad">🐂 Bahasa Madura</option>
                                <option value="bew">🎭 Bahasa Betawi</option>
                                <option value="sas">🏝️ Bahasa Sasak (Lombok)</option>
                            </optgroup>

                            <optgroup label="🌏 Bahasa Asia Lainnya">
<!-- ... existing code ... -->
            <!-- Area Kotak Teks (Grid 2 Kolom pada Desktop, 1 Kolom pada Mobile) -->
            <div class="grid grid-cols-1 md:grid-cols-2 divide-y md:divide-y-0 md:divide-x divide-slate-200 dark:divide-slate-700">
                
                <!-- Kolom Kiri: Input Teks Sumber -->
                <div class="lf-input-box flex flex-col justify-between p-4 sm:p-6 relative group transition-colors duration-300">
                    <div class="relative flex-grow">
                        <textarea 
                            id="source-text" 
                            rows="6" 
                            maxlength="2000"
                            placeholder="Ketik atau tempel teks bahasa asing maupun daerah di sini..." 
                            class="lf-textarea w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 pr-9 text-base sm:text-lg font-normal leading-relaxed outline-none"
                        ></textarea>
                        
                        <!-- Tombol Hapus Teks (Muncul jika ada teks) -->
                        <button id="clear-btn" type="button" title="Hapus teks" class="hidden absolute top-0 right-0 w-8 h-8 rounded-lg bg-slate-200 dark:bg-slate-800 hover:bg-rose-100 dark:hover:bg-rose-950 text-slate-600 dark:text-slate-300 hover:text-rose-600 dark:hover:text-rose-400 flex items-center justify-center transition-colors">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>

                    <!-- Toolbar Bawah Input -->
                    <div class="pt-4 mt-2 border-t border-slate-200 dark:border-slate-800 flex items-center justify-between">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-source-btn" type="button" title="Dengarkan teks sumber" class="p-2.5 rounded-xl text-slate-600 dark:text-slate-300 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-50 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-source-btn" type="button" title="Salin teks sumber" class="p-2.5 rounded-xl text-slate-600 dark:text-slate-300 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-50 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-regular fa-copy"></i>
                            </button>
                        </div>

                        <div class="flex items-center gap-3">
                            <span id="char-count" class="text-xs font-medium text-slate-500 dark:text-slate-400">0 / 2000</span>
                            <button id="translate-btn" type="button" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-indigo-600 to-blue-600 hover:from-indigo-700 hover:to-blue-700 text-white text-sm font-semibold shadow-md shadow-indigo-500/25 hover:shadow-lg transition-all active:scale-95 flex items-center gap-2">
                                <span>Terjemahkan</span>
                                <i class="fa-solid fa-arrow-right text-xs"></i>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Kolom Kanan: Output Hasil Terjemahan -->
                <div class="lf-output-box flex flex-col justify-between p-4 sm:p-6 relative transition-colors duration-300">
                    <div class="relative flex-grow">
                        <!-- Indikator Loading -->
                        <div id="loading-overlay" class="hidden absolute inset-0 bg-slate-100/85 dark:bg-slate-900/85 backdrop-blur-[1px] z-10 flex flex-col items-center justify-center rounded-xl">
                            <div class="w-8 h-8 border-4 border-indigo-200 dark:border-indigo-900 border-t-indigo-600 dark:border-t-indigo-400 rounded-full animate-spin mb-2"></div>
                            <span class="text-xs font-semibold text-indigo-700 dark:text-indigo-300">Menerjemahkan...</span>
                        </div>

                        <textarea 
                            id="target-text" 
                            rows="6" 
                            readonly 
                            placeholder="Hasil terjemahan akan muncul di sini..." 
                            class="lf-textarea w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 text-base sm:text-lg font-normal leading-relaxed outline-none"
                        ></textarea>
                    </div>

                    <!-- Toolbar Bawah Output -->
                    <div class="pt-4 mt-2 border-t border-slate-200 dark:border-slate-800 flex items-center justify-between flex-wrap gap-2">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-target-btn" type="button" title="Dengarkan hasil terjemahan" class="p-2.5 rounded-xl text-slate-600 dark:text-slate-300 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-100/70 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-target-btn" type="button" title="Salin hasil terjemahan" class="p-2.5 rounded-xl text-slate-600 dark:text-slate-300 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-100/70 dark:hover:bg-slate-800 transition-colors focus:outline-none flex items-center gap-1.5">
                                <i class="fa-regular fa-copy"></i>
                                <span class="text-xs font-semibold hidden sm:inline">Salin</span>
                            </button>
                        </div>

                        <div id="detected-lang-badge" class="hidden text-xs font-semibold text-indigo-700 dark:text-indigo-300 bg-indigo-100 dark:bg-indigo-950 px-2.5 py-1 rounded-lg border border-indigo-200 dark:border-indigo-800">
                            Terdeteksi: <span id="detected-lang-name">-</span>
                        </div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Frasa Cepat / Contoh Penggunaan (Asing & Daerah) -->
        <div class="mt-8">
            <div class="flex items-center justify-between mb-3 px-1">
                <h2 class="text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400">Coba Frasa Populer & Daerah</h2>
                <span class="text-[11px] text-slate-500 dark:text-slate-400">Klik untuk langsung menerjemahkan</span>
            </div>
            <div class="flex flex-wrap gap-2">
                <button type="button" data-source="id" data-target="en" class="lf-card quick-phrase px-3.5 py-2 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 text-xs sm:text-sm font-medium text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🇮🇩 Halo, apa kabar hari ini?
                </button>
                <button type="button" data-source="su" data-target="id" class="lf-card quick-phrase px-3.5 py-2 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 text-xs sm:text-sm font-medium text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🌿 Kumaha damang? Abdi bade angkat ka Bandung.
                </button>
                <button type="button" data-source="jv" data-target="id" class="lf-card quick-phrase px-3.5 py-2 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 text-xs sm:text-sm font-medium text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🏺 Sugeng enjang, matur nuwun sanget sampun dibantu.
                </button>
                <button type="button" data-source="ban" data-target="id" class="lf-card quick-phrase px-3.5 py-2 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 text-xs sm:text-sm font-medium text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🌺 Om Swastyastu, punapi gatra?
                </button>
                <button type="button" data-source="min" data-target="id" class="lf-card quick-phrase px-3.5 py-2 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 text-xs sm:text-sm font-medium text-slate-700 dark:text-slate-200 hover:text-indigo-600 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🏠 Baa kaba dunsanak sadonyo? Tarimo kasih banyak.
                </button>
            </div>
        </div>

        <!-- Riwayat Terjemahan Singkat -->
        <div id="history-section" class="mt-8 hidden">
            <div class="flex items-center justify-between mb-3 px-1">
                <h2 class="text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400">Riwayat Terjemahan Terakhir</h2>
                <button id="clear-history-btn" type="button" class="text-xs font-medium text-rose-600 dark:text-rose-400 hover:underline">Hapus Riwayat</button>
            </div>
            <div id="history-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-3"></div>
        </div>

    </main>

    <!-- Modal Panduan Install Aplikasi ke HP (PWA) -->
    <div id="install-modal" class="hidden fixed inset-0 z-50 bg-slate-950/70 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="lf-card max-w-md w-full rounded-2xl border p-6 shadow-2xl relative animate-fade-in">
            <button id="close-install-modal" type="button" class="absolute top-4 right-4 w-8 h-8 rounded-lg bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300 hover:text-rose-500 flex items-center justify-center">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <div class="flex items-center gap-3 mb-4">
                <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-indigo-600 to-blue-500 flex items-center justify-center text-white shadow-md">
                    <i class="fa-solid fa-mobile-screen-button text-2xl"></i>
                </div>
                <div>
                    <h3 class="text-lg font-bold text-slate-900 dark:text-white">Pasang LinguaFlow di HP</h3>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Gunakan seperti aplikasi native tanpa browser</p>
                </div>
            </div>

            <div class="space-y-3 text-sm text-slate-700 dark:text-slate-300">
                <div class="p-3 rounded-xl bg-slate-100 dark:bg-slate-800/90 border border-slate-200 dark:border-slate-700">
                    <p class="font-semibold text-indigo-600 dark:text-indigo-400 mb-1"><i class="fa-brands fa-android mr-1.5"></i>Pengguna Android (Chrome):</p>
                    <p class="text-xs leading-relaxed">Ketuk ikon menu <strong>titik tiga (⋮)</strong> di pojok kanan atas browser, lalu pilih <strong>"Tambahkan ke Layar utama"</strong> atau <strong>"Install aplikasi"</strong>.</p>
                </div>
                <div class="p-3 rounded-xl bg-slate-100 dark:bg-slate-800/90 border border-slate-200 dark:border-slate-700">
                    <p class="font-semibold text-blue-600 dark:text-blue-400 mb-1"><i class="fa-brands fa-apple mr-1.5"></i>Pengguna iPhone / iPad (Safari):</p>
                    <p class="text-xs leading-relaxed">Ketuk tombol <strong>Bagikan (Share <i class="fa-solid fa-arrow-up-from-bracket"></i>)</strong> di bagian bawah layar, gulir ke bawah, lalu pilih <strong>"Tambah ke Layar Utama" (Add to Home Screen)</strong>.</p>
                </div>
            </div>

            <div class="mt-5 flex justify-end gap-2">
                <button id="download-html-btn" type="button" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 text-slate-800 dark:text-slate-200 text-xs font-semibold transition-colors">
                    <i class="fa-solid fa-file-code mr-1"></i> Simpan File Offline (.html)
                </button>
                <button id="ok-install-modal" type="button" class="px-4 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-semibold transition-colors">
                    Mengerti
                </button>
            </div>
        </div>
    </div>

    <!-- Toast Notification (Pengganti Alert) -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="bg-slate-900 dark:bg-slate-800 text-white px-4 py-3 rounded-xl shadow-lg border border-slate-700 flex items-center gap-3 text-sm font-medium">
            <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
            <span id="toast-message">Pesan notifikasi</span>
        </div>
    </div>

    <!-- Footer -->
    <footer class="lf-card border-t py-5 mt-8 transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-2 text-xs text-slate-500 dark:text-slate-400">
            <p>&copy; 2026 LinguaFlow Translator. Mendukung Bahasa Dunia & Bahasa Daerah Nusantara.</p>
            <p>Tekan <kbd class="px-1.5 py-0.5 bg-slate-100 dark:bg-slate-800 border border-slate-300 dark:border-slate-700 rounded text-slate-700 dark:text-slate-300 font-mono">Ctrl + Enter</kbd> untuk menerjemahkan cepat.</p>
        </div>
    </footer>

    <!-- Logika JavaScript & PWA Setup -->
    <script>
        // ==========================================
        // 1. INISIALISASI PWA (Manifest & Service Worker Dinamis)
        // ==========================================
        (function initPWA() {
            // Ikon aplikasi SVG resolusi tinggi sebagai Data URI
            const appIconSvg = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><defs><linearGradient id="g" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stop-color="#4f46e5"/><stop offset="100%" stop-color="#2563eb"/></linearGradient></defs><rect width="512" height="512" rx="112" fill="url(#g)"/><text x="50%" y="54%" dominant-baseline="middle" text-anchor="middle" fill="#ffffff" font-family="sans-serif" font-weight="bold" font-size="220">文A</text></svg>`;
            const appIconDataUri = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(appIconSvg);

            // Pasang Apple Touch Icon
            const appleIcon = document.createElement('link');
            appleIcon.rel = 'apple-touch-icon';
            appleIcon.href = appIconDataUri;
            document.head.appendChild(appleIcon);

            // Buat Web App Manifest secara dinamis via Blob URL
            const manifestObj = {
                name: 'LinguaFlow - Penerjemah Bahasa Asing & Daerah',
                short_name: 'LinguaFlow',
                description: 'Aplikasi penerjemah cepat bahasa asing dunia dan bahasa daerah Nusantara.',
                start_url: window.location.href,
                display: 'standalone',
                background_color: '#0f172a',
                theme_color: '#4f46e5',
                orientation: 'portrait-primary',
                icons: [
                    {
                        src: appIconDataUri,
                        sizes: '192x192',
                        type: 'image/svg+xml',
                        purpose: 'any maskable'
                    },
                    {
                        src: appIconDataUri,
                        sizes: '512x512',
                        type: 'image/svg+xml',
                        purpose: 'any maskable'
                    }
                ]
            };

            try {
                const manifestBlob = new Blob([JSON.stringify(manifestObj)], { type: 'application/manifest+json' });
                const manifestUrl = URL.createObjectURL(manifestBlob);
                const manifestLink = document.createElement('link');
                manifestLink.rel = 'manifest';
                manifestLink.href = manifestUrl;
                document.head.appendChild(manifestLink);
            } catch (e) {
                console.warn('Manifest PWA tidak dapat dimuat pada environment ini:', e);
            }

            // Daftarkan Service Worker inline jika berjalan di protokol HTTPS/localhost
            if ('serviceWorker' in navigator && (window.location.protocol === 'https:' || window.location.hostname === 'localhost')) {
                const swCode = `
                    const CACHE_NAME = 'linguaflow-v1';
                    self.addEventListener('install', (event) => {
                        self.skipWaiting();
                    });
                    self.addEventListener('activate', (event) => {
                        event.waitUntil(clients.claim());
                    });
                    self.addEventListener('fetch', (event) => {
                        if (event.request.method !== 'GET') return;
                        event.respondWith(
                            fetch(event.request).catch(() => caches.match(event.request))
                        );
                    });
                `;
                try {
                    const swBlob = new Blob([swCode], { type: 'application/javascript' });
                    const swUrl = URL.createObjectURL(swBlob);
                    navigator.serviceWorker.register(swUrl).catch(() => {});
                } catch (e) {}
            }
        })();

        document.addEventListener('DOMContentLoaded', () => {
            // Referensi Elemen DOM
            const themeToggleBtn = document.getElementById('theme-toggle');
            const metaThemeColor = document.getElementById('meta-theme-color');
            const installAppBtn = document.getElementById('install-app-btn');
            const installModal = document.getElementById('install-modal');
            const closeInstallModal = document.getElementById('close-install-modal');
            const okInstallModal = document.getElementById('ok-install-modal');
            const downloadHtmlBtn = document.getElementById('download-html-btn');

            const sourceLangSelect = document.getElementById('source-lang');
            const targetLangSelect = document.getElementById('target-lang');
            const swapBtn = document.getElementById('swap-btn');
            const swapIcon = document.getElementById('swap-icon');
            
            const sourceText = document.getElementById('source-text');
            const targetText = document.getElementById('target-text');
            const charCount = document.getElementById('char-count');
            const clearBtn = document.getElementById('clear-btn');
            const translateBtn = document.getElementById('translate-btn');
            const loadingOverlay = document.getElementById('loading-overlay');
            
            const speakSourceBtn = document.getElementById('speak-source-btn');
            const speakTargetBtn = document.getElementById('speak-target-btn');
            const copySourceBtn = document.getElementById('copy-source-btn');
            const copyTargetBtn = document.getElementById('copy-target-btn');
            
            const detectedLangBadge = document.getElementById('detected-lang-badge');
            const detectedLangName = document.getElementById('detected-lang-name');
            const quickPhrases = document.querySelectorAll('.quick-phrase');
            const historySection = document.getElementById('history-section');
            const historyList = document.getElementById('history-list');
            const clearHistoryBtn = document.getElementById('clear-history-btn');

            // Sinkronisasi warna status bar HP saat load
            if (document.documentElement.classList.contains('dark')) {
                metaThemeColor.setAttribute('content', '#0f172a');
            }

            // Logika Toggle Mode Gelap / Terang
            themeToggleBtn.addEventListener('click', () => {
                const isDark = document.documentElement.classList.toggle('dark');
                localStorage.setItem('linguaflow_theme', isDark ? 'dark' : 'light');
                metaThemeColor.setAttribute('content', isDark ? '#0f172a' : '#4f46e5');
                showToast(isDark ? 'Mode Gelap diaktifkan' : 'Mode Terang diaktifkan', 'info');
            });

            // Logika Install PWA ke HP
            let deferredPrompt = null;
            window.addEventListener('beforeinstallprompt', (e) => {
                e.preventDefault();
                deferredPrompt = e;
            });

            installAppBtn.addEventListener('click', async () => {
                if (deferredPrompt) {
                    deferredPrompt.prompt();
                    const { outcome } = await deferredPrompt.userChoice;
                    if (outcome === 'accepted') {
                        showToast('LinguaFlow sedang dipasang ke layar utama!');
                    }
                    deferredPrompt = null;
                } else {
                    // Tampilkan panduan instalasi manual (untuk iOS Safari, Firefox, atau WebView)
                    installModal.classList.remove('hidden');
                }
            });

            closeInstallModal.addEventListener('click', () => installModal.classList.add('hidden'));
            okInstallModal.addEventListener('click', () => installModal.classList.add('hidden'));
            installModal.addEventListener('click', (e) => {
                if (e.target === installModal) installModal.classList.add('hidden');
            });

            // Fitur Download File HTML langsung ke penyimpanan HP
            downloadHtmlBtn.addEventListener('click', () => {
                const htmlContent = '<!DOCTYPE html>\n' + document.documentElement.outerHTML;
                const blob = new Blob([htmlContent], { type: 'text/html;charset=utf-8' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = 'LinguaFlow-Translator.html';
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                installModal.classList.add('hidden');
                showToast('File aplikasi LinguaFlow.html berhasil diunduh!');
            });

            // Pemetaan Kode Bahasa ke Nama Bahasa Indonesia
            const langNames = {
                'id': 'Indonesia',
                'jv': 'Jawa',
                'su': 'Sunda',
                'ban': 'Bali',
                'min': 'Minangkabau',
                'bug': 'Bugis',
                'mak': 'Makassar',
                'btx': 'Batak Toba',
                'ace': 'Aceh',
                'bjn': 'Banjar',
                'mad': 'Madura',
                'bew': 'Betawi',
                'sas': 'Sasak',
                'en': 'Inggris',
                'ja': 'Jepang',
                'ko': 'Korea',
                'zh-CN': 'Mandarin (Sederhana)',
                'zh-TW': 'Mandarin (Tradisional)',
                'zh': 'Mandarin',
                'ar': 'Arab',
                'ms': 'Melayu',
                'th': 'Thailand',
                'vi': 'Vietnam',
                'hi': 'Hindi',
                'tl': 'Tagalog',
                'tr': 'Turki',
                'fa': 'Persia',
                'es': 'Spanyol',
                'fr': 'Prancis',
                'de': 'Jerman',
                'nl': 'Belanda',
                'ru': 'Rusia',
                'it': 'Italia',
                'pt': 'Portugis',
                'pl': 'Polandia',
                'sv': 'Swedia',
                'el': 'Yunani'
            };

            // Pemetaan Kode Bahasa untuk Web Speech API (TTS)
            const ttsLocaleMap = {
                'id': 'id-ID',
                'jv': 'jv-ID',
                'su': 'su-ID',
                'ban': 'id-ID',
                'min': 'id-ID',
                'bug': 'id-ID',
                'mak': 'id-ID',
                'btx': 'id-ID',
                'ace': 'id-ID',
                'bjn': 'id-ID',
                'mad': 'id-ID',
                'bew': 'id-ID',
                'sas': 'id-ID',
                'en': 'en-US',
                'ja': 'ja-JP',
                'ko': 'ko-KR',
                'zh-CN': 'zh-CN',
                'zh-TW': 'zh-TW',
                'ar': 'ar-SA',
                'ms': 'ms-MY',
                'th': 'th-TH',
                'vi': 'vi-VN',
                'hi': 'hi-IN',
                'tl': 'fil-PH',
                'tr': 'tr-TR',
                'fa': 'fa-IR',
                'es': 'es-ES',
                'fr': 'fr-FR',
                'de': 'de-DE',
                'nl': 'nl-NL',
                'ru': 'ru-RU',
                'it': 'it-IT',
                'pt': 'pt-PT',
                'pl': 'pl-PL',
                'sv': 'sv-SE',
                'el': 'el-GR'
            };

            // Manajemen Riwayat Terjemahan
            let translationHistory = JSON.parse(localStorage.getItem('linguaflow_history') || '[]');

            function renderHistory() {
                if (translationHistory.length === 0) {
                    historySection.classList.add('hidden');
                    return;
                }
                historySection.classList.remove('hidden');
                historyList.innerHTML = '';

                translationHistory.forEach((item) => {
                    const card = document.createElement('div');
                    card.className = 'lf-card p-3.5 rounded-xl border hover:border-indigo-400 dark:hover:border-indigo-500 cursor-pointer transition-all shadow-sm';
                    card.innerHTML = `
                        <div class="flex items-center justify-between text-[11px] font-semibold text-indigo-600 dark:text-indigo-400 mb-1">
                            <span>${langNames[item.sl] || item.sl} &rarr; ${langNames[item.tl] || item.tl}</span>
                        </div>
                        <p class="text-xs font-medium text-slate-800 dark:text-slate-100 line-clamp-1">${escapeHtml(item.src)}</p>
                        <p class="text-xs text-slate-500 dark:text-slate-400 line-clamp-1 mt-0.5">${escapeHtml(item.tgt)}</p>
                    `;
                    card.addEventListener('click', () => {
                        sourceLangSelect.value = item.sl;
                        targetLangSelect.value = item.tl;
                        sourceText.value = item.src;
                        targetText.value = item.tgt;
                        charCount.textContent = `${item.src.length} / 2000`;
                        clearBtn.classList.remove('hidden');
                    });
                    historyList.appendChild(card);
                });
            }

            function saveToHistory(sl, tl, src, tgt) {
                if (!src || !tgt || src.toLowerCase() === tgt.toLowerCase()) return;
                // Hindari duplikat berurutan
                if (translationHistory.length > 0 && translationHistory[0].src === src && translationHistory[0].tl === tl) return;
                
                translationHistory.unshift({ sl, tl, src, tgt });
                if (translationHistory.length > 6) translationHistory.pop();
                localStorage.setItem('linguaflow_history', JSON.stringify(translationHistory));
                renderHistory();
            }

            function escapeHtml(str) {
                const div = document.createElement('div');
                div.textContent = str;
                return div.innerHTML;
            }

            clearHistoryBtn.addEventListener('click', () => {
                translationHistory = [];
                localStorage.removeItem('linguaflow_history');
                renderHistory();
                showToast('Riwayat terjemahan dihapus', 'info');
            });

            renderHistory();

            let typingTimer;
            const doneTypingInterval = 750;
// ... existing code ...
                    targetText.value = result.translatedText;

                    // Simpan ke riwayat singkat
                    const effectiveSource = (sourceLang === 'auto' && result.detectedLanguage) ? result.detectedLanguage : sourceLang;
                    saveToHistory(effectiveSource, targetLang, text, result.translatedText);

                    // Tampilkan badge bahasa terdeteksi jika mode auto aktif
                    if (sourceLang === 'auto' && result.detectedLanguage) {
// ... existing code ...
            quickPhrases.forEach(btn => {
                btn.addEventListener('click', () => {
                    // Hapus emoji bendera/ikon di awal teks frasa
                    const rawText = btn.textContent.trim().replace(/^[^\p{L}\p{N}]+/u, '').trim();
                    const srcLang = btn.getAttribute('data-source');
                    const tgtLang = btn.getAttribute('data-target');

                    if (srcLang) sourceLangSelect.value = srcLang;
                    if (tgtLang) targetLangSelect.value = tgtLang;

                    sourceText.value = rawText;
                    charCount.textContent = `${sourceText.value.length} / 2000`;
                    clearBtn.classList.remove('hidden');
                    translateText();
                });
            });
        });
    </script>
</body>
</html>
