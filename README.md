<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LinguaFlow - Penerjemah Bahasa Asing & Daerah</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Font Awesome untuk Ikon -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                        }
                    }
                }
            }
        }
    </script>
    <script>
        // Terapkan tema sebelum halaman dirender untuk menghindari kedipan (FOUC)
        if (localStorage.getItem('linguaflow_theme') === 'dark' || 
           (!('linguaflow_theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    </script>
</head>
<body class="bg-slate-50 dark:bg-slate-950 text-slate-800 dark:text-slate-100 font-sans min-h-screen flex flex-col justify-between transition-colors duration-300 selection:bg-indigo-100 selection:text-indigo-700 dark:selection:bg-indigo-900 dark:selection:text-indigo-200">

    <!-- Navbar / Header -->
    <header class="bg-white/90 dark:bg-slate-900/90 backdrop-blur-md border-b border-slate-200 dark:border-slate-800 sticky top-0 z-30 shadow-sm transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-blue-500 flex items-center justify-center text-white shadow-md shadow-indigo-200 dark:shadow-indigo-950/50">
                    <i class="fa-solid fa-language text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-blue-600 dark:from-indigo-400 dark:to-blue-400">
                        LinguaFlow
                    </h1>
                    <p class="text-[11px] text-slate-400 dark:text-slate-400 font-medium -mt-1 hidden sm:block">Penerjemah Bahasa Asing & Daerah</p>
                </div>
            </div>

            <div class="flex items-center gap-2.5 sm:gap-3">
                <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-medium bg-indigo-50 dark:bg-indigo-950/60 text-indigo-700 dark:text-indigo-300 border border-indigo-100 dark:border-indigo-800/60">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                    <span class="hidden xs:inline">Multi-API</span> Aktif
                </span>

                <!-- Tombol Toggle Mode Gelap / Terang -->
                <button id="theme-toggle" type="button" title="Ubah Tema Gelap / Terang" aria-label="Toggle Dark Mode" class="w-10 h-10 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-indigo-100 dark:hover:bg-slate-700 text-slate-600 dark:text-amber-400 border border-slate-200 dark:border-slate-700 flex items-center justify-center transition-all duration-200 active:scale-95 focus:outline-none focus:ring-2 focus:ring-indigo-400">
                    <i id="theme-icon-dark" class="fa-solid fa-moon text-base dark:hidden"></i>
                    <i id="theme-icon-light" class="fa-solid fa-sun text-base hidden dark:inline"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-grow max-w-6xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-10">
        
        <!-- Kartu Utama Penerjemah -->
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-xl shadow-slate-200/60 dark:shadow-black/40 border border-slate-200/80 dark:border-slate-800 overflow-hidden transition-colors duration-300">
            
            <!-- Bar Pemilihan Bahasa -->
            <div class="bg-slate-50/80 dark:bg-slate-800/60 border-b border-slate-200 dark:border-slate-800 p-3 sm:p-4 flex flex-col sm:flex-row items-center justify-between gap-3">
                
                <!-- Bahasa Sumber -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="source-lang" class="sr-only">Bahasa Sumber</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-globe text-indigo-500 dark:text-indigo-400 absolute left-3.5 pointer-events-none"></i>
                        <select id="source-lang" class="w-full pl-10 pr-8 py-2.5 bg-white dark:bg-slate-800 border border-slate-300 dark:border-slate-700 hover:border-indigo-400 dark:hover:border-indigo-500 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 dark:focus:ring-indigo-900 rounded-xl text-sm font-medium text-slate-700 dark:text-slate-200 transition-all cursor-pointer appearance-none outline-none">
                            <option value="auto" selected>✨ Deteksi Otomatis</option>
                            
                            <optgroup label="🇮🇩 Bahasa Nasional & Daerah Nusantara">
                                <option value="id">🇮🇩 Bahasa Indonesia</option>
                                <option value="jv">🏺 Bahasa Jawa (Jawa)</option>
                                <option value="su">🌿 Bahasa Sunda (Sunda)</option>
                                <option value="ban">🌺 Bahasa Bali (Bali)</option>
                                <option value="min">🏠 Bahasa Minangkabau</option>
                                <option value="bug">⛵ Bahasa Bugis</option>
                                <option value="btx">🧣 Bahasa Batak Toba</option>
                                <option value="ace">🕌 Bahasa Aceh</option>
                                <option value="bjn">💎 Bahasa Banjar</option>
                                <option value="mad">🐂 Bahasa Madura</option>
                                <option value="bew">🎭 Bahasa Betawi</option>
                            </optgroup>

                            <optgroup label="🌏 Bahasa Asia">
                                <option value="en">🇬🇧 Bahasa Inggris</option>
                                <option value="ja">🇯🇵 Bahasa Jepang</option>
                                <option value="ko">🇰🇷 Bahasa Korea</option>
                                <option value="zh-CN">🇨🇳 Mandarin (Sederhana)</option>
                                <option value="zh-TW">🇹🇼 Mandarin (Tradisional)</option>
                                <option value="ar">🇸🇦 Bahasa Arab</option>
                                <option value="ms">🇲🇾 Bahasa Melayu</option>
                                <option value="th">🇹🇭 Bahasa Thailand</option>
                                <option value="vi">🇻🇳 Bahasa Vietnam</option>
                                <option value="hi">🇮🇳 Bahasa Hindi</option>
                                <option value="tl">🇵🇭 Bahasa Tagalog (Filipina)</option>
                                <option value="tr">🇹🇷 Bahasa Turki</option>
                                <option value="fa">🇮🇷 Bahasa Persia (Farsi)</option>
                            </optgroup>

                            <optgroup label="🌍 Bahasa Eropa & Dunia">
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
                        <i class="fa-solid fa-chevron-down text-xs text-slate-400 dark:text-slate-500 absolute right-3.5 pointer-events-none"></i>
                    </div>
                </div>

                <!-- Tombol Tukar Bahasa (Swap) -->
                <div class="flex justify-center">
                    <button id="swap-btn" type="button" title="Tukar Bahasa" class="w-10 h-10 rounded-full bg-white dark:bg-slate-800 border border-slate-200 dark:border-slate-700 hover:border-indigo-300 dark:hover:border-indigo-500 hover:bg-indigo-50 dark:hover:bg-slate-700 text-slate-600 dark:text-slate-300 hover:text-indigo-600 dark:hover:text-indigo-400 flex items-center justify-center shadow-sm transition-all duration-200 active:scale-95 focus:outline-none focus:ring-2 focus:ring-indigo-300 dark:focus:ring-indigo-800">
                        <i class="fa-solid fa-right-left text-sm transition-transform duration-300" id="swap-icon"></i>
                    </button>
                </div>

                <!-- Bahasa Target -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="target-lang" class="sr-only">Bahasa Target</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-flag text-blue-500 dark:text-blue-400 absolute left-3.5 pointer-events-none"></i>
                        <select id="target-lang" class="w-full pl-10 pr-8 py-2.5 bg-white dark:bg-slate-800 border border-slate-300 dark:border-slate-700 hover:border-indigo-400 dark:hover:border-indigo-500 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 dark:focus:ring-indigo-900 rounded-xl text-sm font-medium text-slate-700 dark:text-slate-200 transition-all cursor-pointer appearance-none outline-none">
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
                                <option value="btx">🧣 Bahasa Batak Toba</option>
                                <option value="ace">🕌 Bahasa Aceh</option>
                                <option value="bjn">💎 Bahasa Banjar</option>
                                <option value="mad">🐂 Bahasa Madura</option>
                                <option value="bew">🎭 Bahasa Betawi</option>
                            </optgroup>

                            <optgroup label="🌏 Bahasa Asia Lainnya">
                                <option value="zh-TW">🇹🇼 Mandarin (Tradisional)</option>
                                <option value="ms">🇲🇾 Bahasa Melayu</option>
                                <option value="th">🇹🇭 Bahasa Thailand</option>
                                <option value="vi">🇻🇳 Bahasa Vietnam</option>
                                <option value="hi">🇮🇳 Bahasa Hindi</option>
                                <option value="tl">🇵🇭 Bahasa Tagalog (Filipina)</option>
                                <option value="tr">🇹🇷 Bahasa Turki</option>
                                <option value="fa">🇮🇷 Bahasa Persia (Farsi)</option>
                            </optgroup>

                            <optgroup label="🌍 Bahasa Eropa & Dunia">
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
                        <i class="fa-solid fa-chevron-down text-xs text-slate-400 dark:text-slate-500 absolute right-3.5 pointer-events-none"></i>
                    </div>
                </div>
            </div>

            <!-- Area Kotak Teks (Grid 2 Kolom pada Desktop, 1 Kolom pada Mobile) -->
            <div class="grid grid-cols-1 md:grid-cols-2 divide-y md:divide-y-0 md:divide-x divide-slate-200 dark:divide-slate-800">
                
                <!-- Kolom Kiri: Input Teks Sumber -->
                <div class="flex flex-col justify-between p-4 sm:p-6 bg-white dark:bg-slate-900 relative group transition-colors duration-300">
                    <div class="relative flex-grow">
                        <textarea 
                            id="source-text" 
                            rows="6" 
                            maxlength="2000"
                            placeholder="Ketik atau tempel teks bahasa asing maupun daerah di sini..." 
                            class="w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 pr-9 text-slate-800 dark:text-slate-100 placeholder-slate-400 dark:placeholder-slate-500 text-base sm:text-lg leading-relaxed outline-none bg-transparent"
                        ></textarea>
                        
                        <!-- Tombol Hapus Teks (Muncul jika ada teks) -->
                        <button id="clear-btn" type="button" title="Hapus teks" class="hidden absolute top-0 right-0 w-8 h-8 rounded-lg bg-slate-100 dark:bg-slate-800 hover:bg-rose-100 dark:hover:bg-rose-950 text-slate-500 dark:text-slate-400 hover:text-rose-600 dark:hover:text-rose-400 flex items-center justify-center transition-colors">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>

                    <!-- Toolbar Bawah Input -->
                    <div class="pt-4 mt-2 border-t border-slate-100 dark:border-slate-800 flex items-center justify-between">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-source-btn" type="button" title="Dengarkan teks sumber" class="p-2.5 rounded-xl text-slate-500 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-50 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-source-btn" type="button" title="Salin teks sumber" class="p-2.5 rounded-xl text-slate-500 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-50 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-regular fa-copy"></i>
                            </button>
                        </div>

                        <div class="flex items-center gap-3">
                            <span id="char-count" class="text-xs font-medium text-slate-400 dark:text-slate-500">0 / 2000</span>
                            <button id="translate-btn" type="button" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-indigo-600 to-blue-600 hover:from-indigo-700 hover:to-blue-700 text-white text-sm font-semibold shadow-md shadow-indigo-200 dark:shadow-indigo-950/60 hover:shadow-lg transition-all active:scale-95 flex items-center gap-2">
                                <span>Terjemahkan</span>
                                <i class="fa-solid fa-arrow-right text-xs"></i>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Kolom Kanan: Output Hasil Terjemahan -->
                <div class="flex flex-col justify-between p-4 sm:p-6 bg-slate-50/50 dark:bg-slate-900/50 relative transition-colors duration-300">
                    <div class="relative flex-grow">
                        <!-- Indikator Loading -->
                        <div id="loading-overlay" class="hidden absolute inset-0 bg-slate-50/80 dark:bg-slate-900/80 backdrop-blur-[1px] z-10 flex flex-col items-center justify-center rounded-xl">
                            <div class="w-8 h-8 border-4 border-indigo-200 dark:border-indigo-900 border-t-indigo-600 dark:border-t-indigo-400 rounded-full animate-spin mb-2"></div>
                            <span class="text-xs font-medium text-indigo-600 dark:text-indigo-400">Menerjemahkan...</span>
                        </div>

                        <textarea 
                            id="target-text" 
                            rows="6" 
                            readonly 
                            placeholder="Hasil terjemahan akan muncul di sini..." 
                            class="w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 text-slate-800 dark:text-slate-100 placeholder-slate-400 dark:placeholder-slate-500 text-base sm:text-lg leading-relaxed outline-none bg-transparent"
                        ></textarea>
                    </div>

                    <!-- Toolbar Bawah Output -->
                    <div class="pt-4 mt-2 border-t border-slate-200/70 dark:border-slate-800 flex items-center justify-between flex-wrap gap-2">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-target-btn" type="button" title="Dengarkan hasil terjemahan" class="p-2.5 rounded-xl text-slate-500 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-100/70 dark:hover:bg-slate-800 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-target-btn" type="button" title="Salin hasil terjemahan" class="p-2.5 rounded-xl text-slate-500 dark:text-slate-400 hover:text-indigo-600 dark:hover:text-indigo-400 hover:bg-indigo-100/70 dark:hover:bg-slate-800 transition-colors focus:outline-none flex items-center gap-1.5">
                                <i class="fa-regular fa-copy"></i>
                                <span class="text-xs font-medium hidden sm:inline">Salin</span>
                            </button>
                        </div>

                        <div id="detected-lang-badge" class="hidden text-xs font-medium text-indigo-600 dark:text-indigo-300 bg-indigo-50 dark:bg-indigo-950/80 px-2.5 py-1 rounded-lg border border-indigo-100 dark:border-indigo-800/60">
                            Terdeteksi: <span id="detected-lang-name">-</span>
                        </div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Frasa Cepat / Contoh Penggunaan (Asing & Daerah) -->
        <div class="mt-8">
            <div class="flex items-center justify-between mb-3 px-1">
                <h2 class="text-xs font-semibold uppercase tracking-wider text-slate-400 dark:text-slate-500">Coba Frasa Populer & Daerah</h2>
                <span class="text-[11px] text-slate-400 dark:text-slate-500">Klik untuk langsung menerjemahkan</span>
            </div>
            <div class="flex flex-wrap gap-2">
                <button type="button" data-source="id" data-target="en" class="quick-phrase px-3.5 py-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 hover:border-indigo-300 dark:hover:border-indigo-600 hover:bg-indigo-50/50 dark:hover:bg-slate-800 text-xs sm:text-sm text-slate-600 dark:text-slate-300 hover:text-indigo-700 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🇮🇩 Halo, apa kabar hari ini?
                </button>
                <button type="button" data-source="su" data-target="id" class="quick-phrase px-3.5 py-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 hover:border-indigo-300 dark:hover:border-indigo-600 hover:bg-indigo-50/50 dark:hover:bg-slate-800 text-xs sm:text-sm text-slate-600 dark:text-slate-300 hover:text-indigo-700 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🌿 Kumaha damang? Abdi bade angkat ka Bandung.
                </button>
                <button type="button" data-source="jv" data-target="id" class="quick-phrase px-3.5 py-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 hover:border-indigo-300 dark:hover:border-indigo-600 hover:bg-indigo-50/50 dark:hover:bg-slate-800 text-xs sm:text-sm text-slate-600 dark:text-slate-300 hover:text-indigo-700 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🏺 Sugeng enjang, matur nuwun sanget sampun dibantu.
                </button>
                <button type="button" data-source="ban" data-target="id" class="quick-phrase px-3.5 py-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 hover:border-indigo-300 dark:hover:border-indigo-600 hover:bg-indigo-50/50 dark:hover:bg-slate-800 text-xs sm:text-sm text-slate-600 dark:text-slate-300 hover:text-indigo-700 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🌺 Om Swastyastu, punapi gatra?
                </button>
                <button type="button" data-source="min" data-target="id" class="quick-phrase px-3.5 py-2 rounded-xl bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 hover:border-indigo-300 dark:hover:border-indigo-600 hover:bg-indigo-50/50 dark:hover:bg-slate-800 text-xs sm:text-sm text-slate-600 dark:text-slate-300 hover:text-indigo-700 dark:hover:text-indigo-300 transition-all shadow-sm">
                    🏠 Baa kaba dunsanak sadonyo? Tarimo kasih banyak.
                </button>
            </div>
        </div>

    </main>

    <!-- Toast Notification (Pengganti Alert) -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="bg-slate-900 dark:bg-slate-800 text-white px-4 py-3 rounded-xl shadow-lg border border-slate-700/60 flex items-center gap-3 text-sm font-medium">
            <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
            <span id="toast-message">Pesan notifikasi</span>
        </div>
    </div>

    <!-- Footer -->
    <footer class="border-t border-slate-200 dark:border-slate-800 bg-white dark:bg-slate-900 py-5 mt-8 transition-colors duration-300">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-2 text-xs text-slate-400 dark:text-slate-500">
            <p>&copy; 2026 LinguaFlow Translator. Mendukung Bahasa Dunia & Bahasa Daerah Nusantara.</p>
            <p>Tekan <kbd class="px-1.5 py-0.5 bg-slate-100 dark:bg-slate-800 border border-slate-300 dark:border-slate-700 rounded text-slate-600 dark:text-slate-300 font-mono">Ctrl + Enter</kbd> untuk menerjemahkan cepat.</p>
        </div>
    </footer>

    <!-- Logika JavaScript -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Referensi Elemen DOM
            const themeToggleBtn = document.getElementById('theme-toggle');
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

            // Logika Toggle Mode Gelap / Terang
            themeToggleBtn.addEventListener('click', () => {
                const isDark = document.documentElement.classList.toggle('dark');
                localStorage.setItem('linguaflow_theme', isDark ? 'dark' : 'light');
                showToast(isDark ? 'Mode Gelap diaktifkan' : 'Mode Terang diaktifkan', 'info');
            });

            // Pemetaan Kode Bahasa ke Nama Bahasa Indonesia
            const langNames = {
                'id': 'Indonesia',
                'jv': 'Jawa',
                'su': 'Sunda',
                'ban': 'Bali',
                'min': 'Minangkabau',
                'bug': 'Bugis',
                'btx': 'Batak Toba',
                'ace': 'Aceh',
                'bjn': 'Banjar',
                'mad': 'Madura',
                'bew': 'Betawi',
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
                'ban': 'id-ID', // Fallback pelafalan Nusantara
                'min': 'id-ID',
                'bug': 'id-ID',
                'btx': 'id-ID',
                'ace': 'id-ID',
                'bjn': 'id-ID',
                'mad': 'id-ID',
                'bew': 'id-ID',
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

            let typingTimer;
            const doneTypingInterval = 750; // Auto-translate setelah berhenti mengetik 750ms

            // Fungsi Menampilkan Notifikasi Toast
            let toastTimeout;
            function showToast(message, type = 'success') {
                const toast = document.getElementById('toast');
                const toastMsg = document.getElementById('toast-message');
                const toastIcon = document.getElementById('toast-icon');

                toastMsg.textContent = message;
                
                if (type === 'error') {
                    toastIcon.className = 'fa-solid fa-circle-exclamation text-rose-400';
                } else if (type === 'info') {
                    toastIcon.className = 'fa-solid fa-circle-info text-blue-400';
                } else {
                    toastIcon.className = 'fa-solid fa-circle-check text-emerald-400';
                }

                toast.classList.remove('translate-y-20', 'opacity-0');
                
                clearTimeout(toastTimeout);
                toastTimeout = setTimeout(() => {
                    toast.classList.add('translate-y-20', 'opacity-0');
                }, 2800);
            }

            // Fungsi Salin Teks (Menggunakan execCommand agar kompatibel di iframe)
            function copyToClipboard(text, label) {
                if (!text.trim()) {
                    showToast(`Tidak ada ${label} untuk disalin`, 'info');
                    return;
                }
                const tempInput = document.createElement('textarea');
                tempInput.value = text;
                document.body.appendChild(tempInput);
                tempInput.select();
                try {
                    document.execCommand('copy');
                    showToast(`${label} berhasil disalin!`);
                } catch (err) {
                    showToast('Gagal menyalin teks', 'error');
                }
                document.body.removeChild(tempInput);
            }

            // Fungsi Text-to-Speech (Pengucapan Suara)
            function speakText(text, langCode) {
                if (!text.trim()) {
                    showToast('Masukkan atau terjemahkan teks terlebih dahulu', 'info');
                    return;
                }
                if (!('speechSynthesis' in window)) {
                    showToast('Browser Anda tidak mendukung fitur suara', 'error');
                    return;
                }

                window.speechSynthesis.cancel();

                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = (langCode === 'auto') ? 'id-ID' : (ttsLocaleMap[langCode] || langCode);
                utterance.rate = 0.95;

                utterance.onerror = () => {
                    showToast('Suara tidak tersedia untuk bahasa ini di perangkat Anda', 'info');
                };

                window.speechSynthesis.speak(utterance);
            }

            // Endpoint 1: Google Translate GTX Free API (Sangat akurat untuk bahasa daerah seperti Sunda, Jawa, Bali, Minang, Bugis, dll.)
            async function fetchGoogleGTX(text, sl, tl) {
                const url = `https://translate.googleapis.com/translate_a/single?client=gtx&sl=${encodeURIComponent(sl)}&tl=${encodeURIComponent(tl)}&dt=t&q=${encodeURIComponent(text)}`;
                const response = await fetch(url);
                if (!response.ok) throw new Error('GTX API Error');
                const data = await response.json();
                
                // Gabungkan potongan kalimat hasil terjemahan
                let translated = '';
                if (Array.isArray(data[0])) {
                    data[0].forEach(segment => {
                        if (segment[0]) translated += segment[0];
                    });
                }
                const detected = data[2] || null;
                return { translatedText: translated, detectedLanguage: detected };
            }

            // Endpoint 2: MyMemory API Fallback
            async function fetchMyMemory(text, sl, tl) {
                const sourceParam = (sl === 'auto') ? 'Autodetect' : sl;
                const langPair = `${sourceParam}|${tl}`;
                const apiUrl = `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${encodeURIComponent(langPair)}`;

                const response = await fetch(apiUrl);
                if (!response.ok) throw new Error('MyMemory API Error');
                const data = await response.json();

                if (data.responseStatus === 200 || data.responseData) {
                    return {
                        translatedText: data.responseData.translatedText,
                        detectedLanguage: data.responseData.detectedLanguage || null
                    };
                }
                throw new Error('MyMemory gagal menerjemahkan');
            }

            // Fungsi Utama Terjemahan dengan Dual-Engine Fallback
            async function translateText() {
                const text = sourceText.value.trim();
                
                if (!text) {
                    targetText.value = '';
                    detectedLangBadge.classList.add('hidden');
                    return;
                }

                const sourceLang = sourceLangSelect.value;
                const targetLang = targetLangSelect.value;

                // Cegah terjemahan ke bahasa yang sama persis
                if (sourceLang === targetLang) {
                    targetText.value = text;
                    detectedLangBadge.classList.add('hidden');
                    return;
                }

                loadingOverlay.classList.remove('hidden');

                try {
                    let result;
                    try {
                        // Prioritaskan Google GTX karena dukungan bahasa daerah Indonesia jauh lebih lengkap
                        result = await fetchGoogleGTX(text, sourceLang, targetLang);
                    } catch (primaryErr) {
                        // Jika diblokir atau gangguan, beralih otomatis ke MyMemory API
                        result = await fetchMyMemory(text, sourceLang, targetLang);
                    }

                    targetText.value = result.translatedText;

                    // Tampilkan badge bahasa terdeteksi jika mode auto aktif
                    if (sourceLang === 'auto' && result.detectedLanguage) {
                        const detectedCode = result.detectedLanguage;
                        const baseCode = detectedCode.split('-')[0];
                        const readableName = langNames[detectedCode] || langNames[baseCode] || detectedCode.toUpperCase();
                        
                        detectedLangName.textContent = readableName;
                        detectedLangBadge.classList.remove('hidden');
                    } else {
                        detectedLangBadge.classList.add('hidden');
                    }

                } catch (error) {
                    console.error('Translation Error:', error);
                    showToast('Gagal menerjemahkan. Periksa koneksi internet Anda.', 'error');
                } finally {
                    loadingOverlay.classList.add('hidden');
                }
            }

            // Event Listener: Input Teks & Penghitung Karakter
            sourceText.addEventListener('input', () => {
                const currentLength = sourceText.value.length;
                charCount.textContent = `${currentLength} / 2000`;

                if (currentLength > 0) {
                    clearBtn.classList.remove('hidden');
                } else {
                    clearBtn.classList.add('hidden');
                    targetText.value = '';
                    detectedLangBadge.classList.add('hidden');
                }

                // Debounce auto-translate
                clearTimeout(typingTimer);
                if (currentLength > 0) {
                    typingTimer = setTimeout(translateText, doneTypingInterval);
                }
            });

            // Shortcut Ctrl + Enter untuk menerjemahkan langsung
            sourceText.addEventListener('keydown', (e) => {
                if ((e.ctrlKey || e.metaKey) && e.key === 'Enter') {
                    clearTimeout(typingTimer);
                    translateText();
                }
            });

            // Tombol Terjemahkan Manual
            translateBtn.addEventListener('click', () => {
                clearTimeout(typingTimer);
                if (!sourceText.value.trim()) {
                    showToast('Silakan ketik teks terlebih dahulu', 'info');
                    sourceText.focus();
                    return;
                }
                translateText();
            });

            // Tombol Hapus Teks
            clearBtn.addEventListener('click', () => {
                sourceText.value = '';
                targetText.value = '';
                charCount.textContent = '0 / 2000';
                clearBtn.classList.add('hidden');
                detectedLangBadge.classList.add('hidden');
                window.speechSynthesis.cancel();
                sourceText.focus();
            });

            // Tombol Tukar Bahasa (Swap)
            let rotation = 0;
            swapBtn.addEventListener('click', () => {
                rotation += 180;
                swapIcon.style.transform = `rotate(${rotation}deg)`;

                let currentSource = sourceLangSelect.value;
                const currentTarget = targetLangSelect.value;

                if (currentSource === 'auto') {
                    currentSource = (currentTarget === 'id') ? 'en' : 'id';
                }

                sourceLangSelect.value = currentTarget;
                targetLangSelect.value = currentSource;

                if (targetText.value.trim()) {
                    const tempText = sourceText.value;
                    sourceText.value = targetText.value;
                    targetText.value = tempText;
                    charCount.textContent = `${sourceText.value.length} / 2000`;
                    translateText();
                }
            });

            // Terjemahkan ulang otomatis saat pilihan bahasa diubah
            sourceLangSelect.addEventListener('change', () => {
                if (sourceText.value.trim()) translateText();
            });
            targetLangSelect.addEventListener('change', () => {
                if (sourceText.value.trim()) translateText();
            });

            // Event Listener Tombol Salin
            copySourceBtn.addEventListener('click', () => copyToClipboard(sourceText.value, 'Teks sumber'));
            copyTargetBtn.addEventListener('click', () => copyToClipboard(targetText.value, 'Hasil terjemahan'));

            // Event Listener Tombol Text-to-Speech
            speakSourceBtn.addEventListener('click', () => speakText(sourceText.value, sourceLangSelect.value));
            speakTargetBtn.addEventListener('click', () => speakText(targetText.value, targetLangSelect.value));

            // Event Listener Frasa Cepat (Otomatis mengatur bahasa sumber & target sesuai frasa)
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
