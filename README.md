<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LinguaFlow - Penerjemah Bahasa Modern</title>
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
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col justify-between selection:bg-indigo-100 selection:text-indigo-700">

    <!-- Navbar / Header -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-blue-500 flex items-center justify-center text-white shadow-md shadow-indigo-200">
                    <i class="fa-solid fa-language text-xl"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-indigo-600 to-blue-600">
                        LinguaFlow
                    </h1>
                    <p class="text-[11px] text-slate-400 font-medium -mt-1 hidden sm:block">Penerjemah Cerdas & Cepat</p>
                </div>
            </div>

            <div class="flex items-center gap-2 sm:gap-4">
                <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-medium bg-indigo-50 text-indigo-700 border border-indigo-100">
                    <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                    API Aktif
                </span>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="flex-grow max-w-6xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 sm:py-10">
        
        <!-- Kartu Utama Penerjemah -->
        <div class="bg-white rounded-2xl shadow-xl shadow-slate-200/60 border border-slate-200/80 overflow-hidden">
            
            <!-- Bar Pemilihan Bahasa -->
            <div class="bg-slate-50/80 border-b border-slate-200 p-3 sm:p-4 flex flex-col sm:flex-row items-center justify-between gap-3">
                
                <!-- Bahasa Sumber -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="source-lang" class="sr-only">Bahasa Sumber</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-globe text-indigo-500 absolute left-3.5 pointer-events-none"></i>
                        <select id="source-lang" class="w-full pl-10 pr-8 py-2.5 bg-white border border-slate-300 hover:border-indigo-400 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 rounded-xl text-sm font-medium text-slate-700 transition-all cursor-pointer appearance-none outline-none">
                            <option value="Autodetect" selected>✨ Deteksi Otomatis</option>
                            <option value="id-ID">🇮🇩 Bahasa Indonesia</option>
                            <option value="en-GB">🇬🇧 Bahasa Inggris</option>
                            <option value="ja-JP">🇯🇵 Bahasa Jepang</option>
                            <option value="ko-KR">🇰🇷 Bahasa Korea</option>
                            <option value="es-ES">🇪🇸 Bahasa Spanyol</option>
                            <option value="fr-FR">🇫🇷 Bahasa Prancis</option>
                            <option value="ar-SA">🇸🇦 Bahasa Arab</option>
                            <option value="zh-CN">🇨🇳 Bahasa Mandarin</option>
                            <option value="de-DE">🇩🇪 Bahasa Jerman</option>
                        </select>
                        <i class="fa-solid fa-chevron-down text-xs text-slate-400 absolute right-3.5 pointer-events-none"></i>
                    </div>
                </div>

                <!-- Tombol Tukar Bahasa (Swap) -->
                <div class="flex justify-center">
                    <button id="swap-btn" type="button" title="Tukar Bahasa" class="w-10 h-10 rounded-full bg-white border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50 text-slate-600 hover:text-indigo-600 flex items-center justify-center shadow-sm transition-all duration-200 active:scale-95 focus:outline-none focus:ring-2 focus:ring-indigo-300">
                        <i class="fa-solid fa-right-left text-sm transition-transform duration-300" id="swap-icon"></i>
                    </button>
                </div>

                <!-- Bahasa Target -->
                <div class="w-full sm:w-5/12 relative">
                    <label for="target-lang" class="sr-only">Bahasa Target</label>
                    <div class="relative flex items-center">
                        <i class="fa-solid fa-flag text-blue-500 absolute left-3.5 pointer-events-none"></i>
                        <select id="target-lang" class="w-full pl-10 pr-8 py-2.5 bg-white border border-slate-300 hover:border-indigo-400 focus:border-indigo-500 focus:ring-2 focus:ring-indigo-200 rounded-xl text-sm font-medium text-slate-700 transition-all cursor-pointer appearance-none outline-none">
                            <option value="en-GB" selected>🇬🇧 Bahasa Inggris</option>
                            <option value="id-ID">🇮🇩 Bahasa Indonesia</option>
                            <option value="ja-JP">🇯🇵 Bahasa Jepang</option>
                            <option value="ko-KR">🇰🇷 Bahasa Korea</option>
                            <option value="es-ES">🇪🇸 Bahasa Spanyol</option>
                            <option value="fr-FR">🇫🇷 Bahasa Prancis</option>
                            <option value="ar-SA">🇸🇦 Bahasa Arab</option>
                            <option value="zh-CN">🇨🇳 Bahasa Mandarin</option>
                            <option value="de-DE">🇩🇪 Bahasa Jerman</option>
                        </select>
                        <i class="fa-solid fa-chevron-down text-xs text-slate-400 absolute right-3.5 pointer-events-none"></i>
                    </div>
                </div>
            </div>

            <!-- Area Kotak Teks (Grid 2 Kolom pada Desktop, 1 Kolom pada Mobile) -->
            <div class="grid grid-cols-1 md:grid-cols-2 divide-y md:divide-y-0 md:divide-x divide-slate-200">
                
                <!-- Kolom Kiri: Input Teks Sumber -->
                <div class="flex flex-col justify-between p-4 sm:p-6 bg-white relative group">
                    <div class="relative flex-grow">
                        <textarea 
                            id="source-text" 
                            rows="6" 
                            maxlength="1000"
                            placeholder="Ketik atau tempel teks yang ingin diterjemahkan di sini..." 
                            class="w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 text-slate-800 placeholder-slate-400 text-base sm:text-lg leading-relaxed outline-none bg-transparent"
                        ></textarea>
                        
                        <!-- Tombol Hapus Teks (Muncul jika ada teks) -->
                        <button id="clear-btn" type="button" title="Hapus teks" class="hidden absolute top-0 right-0 w-8 h-8 rounded-lg bg-slate-100 hover:bg-rose-100 text-slate-500 hover:text-rose-600 flex items-center justify-center transition-colors">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>

                    <!-- Toolbar Bawah Input -->
                    <div class="pt-4 mt-2 border-t border-slate-100 flex items-center justify-between">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-source-btn" type="button" title="Dengarkan teks sumber" class="p-2.5 rounded-xl text-slate-500 hover:text-indigo-600 hover:bg-indigo-50 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-source-btn" type="button" title="Salin teks sumber" class="p-2.5 rounded-xl text-slate-500 hover:text-indigo-600 hover:bg-indigo-50 transition-colors focus:outline-none">
                                <i class="fa-regular fa-copy"></i>
                            </button>
                        </div>

                        <div class="flex items-center gap-3">
                            <span id="char-count" class="text-xs font-medium text-slate-400">0 / 1000</span>
                            <button id="translate-btn" type="button" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-indigo-600 to-blue-600 hover:from-indigo-700 hover:to-blue-700 text-white text-sm font-semibold shadow-md shadow-indigo-200 hover:shadow-lg transition-all active:scale-95 flex items-center gap-2">
                                <span>Terjemahkan</span>
                                <i class="fa-solid fa-arrow-right text-xs"></i>
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Kolom Kanan: Output Hasil Terjemahan -->
                <div class="flex flex-col justify-between p-4 sm:p-6 bg-slate-50/50 relative">
                    <div class="relative flex-grow">
                        <!-- Indikator Loading -->
                        <div id="loading-overlay" class="hidden absolute inset-0 bg-slate-50/80 backdrop-blur-[1px] z-10 flex flex-col items-center justify-center rounded-xl">
                            <div class="w-8 h-8 border-4 border-indigo-200 border-t-indigo-600 rounded-full animate-spin mb-2"></div>
                            <span class="text-xs font-medium text-indigo-600">Menerjemahkan...</span>
                        </div>

                        <textarea 
                            id="target-text" 
                            rows="6" 
                            readonly 
                            placeholder="Hasil terjemahan akan muncul di sini..." 
                            class="w-full h-44 sm:h-56 resize-none border-0 focus:ring-0 p-0 text-slate-800 placeholder-slate-400 text-base sm:text-lg leading-relaxed outline-none bg-transparent"
                        ></textarea>
                    </div>

                    <!-- Toolbar Bawah Output -->
                    <div class="pt-4 mt-2 border-t border-slate-200/70 flex items-center justify-between">
                        <div class="flex items-center gap-1.5">
                            <button id="speak-target-btn" type="button" title="Dengarkan hasil terjemahan" class="p-2.5 rounded-xl text-slate-500 hover:text-indigo-600 hover:bg-indigo-100/70 transition-colors focus:outline-none">
                                <i class="fa-solid fa-volume-high"></i>
                            </button>
                            <button id="copy-target-btn" type="button" title="Salin hasil terjemahan" class="p-2.5 rounded-xl text-slate-500 hover:text-indigo-600 hover:bg-indigo-100/70 transition-colors focus:outline-none flex items-center gap-1.5">
                                <i class="fa-regular fa-copy"></i>
                                <span class="text-xs font-medium hidden sm:inline">Salin</span>
                            </button>
                        </div>

                        <div id="detected-lang-badge" class="hidden text-xs font-medium text-indigo-600 bg-indigo-50 px-2.5 py-1 rounded-lg border border-indigo-100">
                            Terdeteksi: <span id="detected-lang-name">-</span>
                        </div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Frasa Cepat / Contoh Penggunaan -->
        <div class="mt-8">
            <h2 class="text-xs font-semibold uppercase tracking-wider text-slate-400 mb-3 px-1">Coba Frasa Populer</h2>
            <div class="flex flex-wrap gap-2">
                <button type="button" class="quick-phrase px-3.5 py-2 rounded-xl bg-white border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50/50 text-xs sm:text-sm text-slate-600 hover:text-indigo-700 transition-all shadow-sm">
                    Halo, apa kabar hari ini?
                </button>
                <button type="button" class="quick-phrase px-3.5 py-2 rounded-xl bg-white border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50/50 text-xs sm:text-sm text-slate-600 hover:text-indigo-700 transition-all shadow-sm">
                    Terima kasih banyak atas bantuannya.
                </button>
                <button type="button" class="quick-phrase px-3.5 py-2 rounded-xl bg-white border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50/50 text-xs sm:text-sm text-slate-600 hover:text-indigo-700 transition-all shadow-sm">
                    Di mana stasiun kereta terdekat?
                </button>
                <button type="button" class="quick-phrase px-3.5 py-2 rounded-xl bg-white border border-slate-200 hover:border-indigo-300 hover:bg-indigo-50/50 text-xs sm:text-sm text-slate-600 hover:text-indigo-700 transition-all shadow-sm">
                    Saya sedang belajar membuat aplikasi web.
                </button>
            </div>
        </div>

    </main>

    <!-- Toast Notification (Pengganti Alert) -->
    <div id="toast" class="fixed bottom-5 right-5 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="bg-slate-900 text-white px-4 py-3 rounded-xl shadow-lg flex items-center gap-3 text-sm font-medium">
            <i id="toast-icon" class="fa-solid fa-circle-check text-emerald-400"></i>
            <span id="toast-message">Pesan notifikasi</span>
        </div>
    </div>

    <!-- Footer -->
    <footer class="border-t border-slate-200 bg-white py-5 mt-8">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row items-center justify-between gap-2 text-xs text-slate-400">
            <p>&copy; 2026 LinguaFlow Translator. Didukung oleh MyMemory API & Web Speech API.</p>
            <p>Tekan <kbd class="px-1.5 py-0.5 bg-slate-100 border border-slate-300 rounded text-slate-600 font-mono">Ctrl + Enter</kbd> untuk menerjemahkan cepat.</p>
        </div>
    </footer>

    <!-- Logika JavaScript -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Referensi Elemen DOM
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

            // Pemetaan Kode Bahasa ke Nama Bahasa Indonesia
            const langNames = {
                'id': 'Indonesia', 'id-ID': 'Indonesia',
                'en': 'Inggris', 'en-GB': 'Inggris', 'en-US': 'Inggris',
                'ja': 'Jepang', 'ja-JP': 'Jepang',
                'ko': 'Korea', 'ko-KR': 'Korea',
                'es': 'Spanyol', 'es-ES': 'Spanyol',
                'fr': 'Prancis', 'fr-FR': 'Prancis',
                'ar': 'Arab', 'ar-SA': 'Arab',
                'zh': 'Mandarin', 'zh-CN': 'Mandarin',
                'de': 'Jerman', 'de-DE': 'Jerman'
            };

            let typingTimer;
            const doneTypingInterval = 800; // Auto-translate setelah berhenti mengetik 800ms

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

                // Hentikan suara yang sedang berjalan
                window.speechSynthesis.cancel();

                const utterance = new SpeechSynthesisUtterance(text);
                // Jika deteksi otomatis, gunakan bahasa default browser atau Indonesia
                utterance.lang = (langCode === 'Autodetect') ? 'id-ID' : langCode;
                utterance.rate = 0.95;

                utterance.onerror = () => {
                    showToast('Gagal memutar suara untuk bahasa ini', 'error');
                };

                window.speechSynthesis.speak(utterance);
            }

            // Fungsi Utama Terjemahan menggunakan MyMemory API
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
                    return;
                }

                loadingOverlay.classList.remove('hidden');

                try {
                    // Format langpair untuk MyMemory API
                    const langPair = `${sourceLang}|${targetLang}`;
                    const apiUrl = `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${encodeURIComponent(langPair)}`;

                    const response = await fetch(apiUrl);
                    if (!response.ok) throw new Error('Gangguan jaringan');

                    const data = await response.json();

                    if (data.responseStatus === 200 || data.responseData) {
                        targetText.value = data.responseData.translatedText;

                        // Tampilkan bahasa yang terdeteksi jika mode Autodetect aktif
                        if (sourceLang === 'Autodetect' && data.responseData.detectedLanguage) {
                            const detectedCode = data.responseData.detectedLanguage;
                            const baseCode = detectedCode.split('-')[0];
                            const readableName = langNames[detectedCode] || langNames[baseCode] || detectedCode.toUpperCase();
                            
                            detectedLangName.textContent = readableName;
                            detectedLangBadge.classList.remove('hidden');
                        } else {
                            detectedLangBadge.classList.add('hidden');
                        }
                    } else {
                        throw new Error(data.responseDetails || 'Gagal menerjemahkan');
                    }
                } catch (error) {
                    console.error('Translation Error:', error);
                    showToast('Terjadi kesalahan saat menerjemahkan. Coba lagi.', 'error');
                } finally {
                    loadingOverlay.classList.add('hidden');
                }
            }

            // Event Listener: Input Teks & Penghitung Karakter
            sourceText.addEventListener('input', () => {
                const currentLength = sourceText.value.length;
                charCount.textContent = `${currentLength} / 1000`;

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
                charCount.textContent = '0 / 1000';
                clearBtn.classList.add('hidden');
                detectedLangBadge.classList.add('hidden');
                window.speechSynthesis.cancel();
                sourceText.focus();
            });

            // Tombol Tukar Bahasa (Swap)
            let rotation = 0;
            swapBtn.addEventListener('click', () => {
                // Animasi rotasi ikon
                rotation += 180;
                swapIcon.style.transform = `rotate(${rotation}deg)`;

                // Jika sumber adalah Autodetect, ubah ke bahasa Indonesia saat ditukar
                let currentSource = sourceLangSelect.value;
                const currentTarget = targetLangSelect.value;

                if (currentSource === 'Autodetect') {
                    currentSource = (currentTarget === 'id-ID') ? 'en-GB' : 'id-ID';
                }

                sourceLangSelect.value = currentTarget;
                targetLangSelect.value = currentSource;

                // Tukar isi teks jika hasil terjemahan sudah ada
                if (targetText.value.trim()) {
                    const tempText = sourceText.value;
                    sourceText.value = targetText.value;
                    targetText.value = tempText;
                    charCount.textContent = `${sourceText.value.length} / 1000`;
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

            // Event Listener Frasa Cepat
            quickPhrases.forEach(btn => {
                btn.addEventListener('click', () => {
                    sourceText.value = btn.textContent.trim();
                    charCount.textContent = `${sourceText.value.length} / 1000`;
                    clearBtn.classList.remove('hidden');
                    translateText();
                });
            });
        });
    </script>
</body>
</html>
