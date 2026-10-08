```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surprise untuk Kamu! 💖</title>
    <!-- Memuat Tailwind CSS untuk styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Memuat Google Fonts: Quicksand untuk kesan lucu dan bulat -->
    <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            overflow-x: hidden; /* Mencegah scroll menyamping */
            background-color: #fdf2f8; /* Tailwind pink-50 */
        }

        /* Animasi berdetak untuk amplop */
        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }
        .animate-heartbeat {
            animation: heartbeat 1.5s infinite;
        }

        /* Animasi muncul (fade in & slide up) */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px) scale(0.95);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }
        .animate-fade-in-up {
            animation: fadeInUp 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        /* Animasi hujan hati */
        .falling-heart {
            position: fixed;
            top: -10vh;
            font-size: 1.5rem;
            user-select: none;
            pointer-events: none;
            z-index: 50;
            animation: fall linear forwards;
        }
        @keyframes fall {
            to {
                transform: translateY(110vh) rotate(360deg);
            }
        }
        
        /* Animasi goyang untuk voucher */
        @keyframes tada {
            0% { transform: scale(1); }
            10%, 20% { transform: scale(0.9) rotate(-3deg); }
            30%, 50%, 70%, 90% { transform: scale(1.1) rotate(3deg); }
            40%, 60%, 80% { transform: scale(1.1) rotate(-3deg); }
            100% { transform: scale(1); }
        }
        .animate-tada {
            animation: tada 1s ease-in-out;
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center relative bg-gradient-to-br from-pink-100 via-pink-50 to-pink-200">

    <!-- Container Audio (Opsional, tapi kita gunakan visual saja agar aman di semua browser tanpa interaksi ekstra) -->

    <!-- HALAMAN 1: Amplop Pembuka -->
    <div id="intro-screen" class="absolute inset-0 flex flex-col items-center justify-center z-40 transition-opacity duration-500 bg-pink-100/80 backdrop-blur-sm">
        <div class="text-center p-6 bg-white rounded-3xl shadow-xl border-4 border-pink-200 cursor-pointer animate-heartbeat hover:bg-pink-50 transition-colors" onclick="openSurprise()">
            <div class="text-7xl mb-4">💌</div>
            <h1 class="text-2xl font-bold text-pink-600 mb-2">Ada Pesan Untukmu!</h1>
            <p class="text-pink-400 font-semibold">Tap amplopnya untuk buka ya 💕</p>
        </div>
    </div>

    <!-- HALAMAN 2: Isi Surat & Ucapan (Disembunyikan di awal) -->
    <div id="main-content" class="hidden w-full max-w-md p-6 z-30 opacity-0">
        <div class="bg-white rounded-3xl shadow-2xl overflow-hidden border-2 border-pink-200 relative">
            
            <!-- Header Kartu -->
            <div class="bg-pink-300 p-6 text-center text-white relative overflow-hidden">
                <!-- Ornamen pita/dekorasi sederhana pake CSS -->
                <div class="absolute -top-10 -left-10 w-24 h-24 bg-pink-400 rounded-full opacity-50"></div>
                <div class="absolute -bottom-10 -right-10 w-24 h-24 bg-pink-400 rounded-full opacity-50"></div>
                <h1 class="text-3xl font-bold relative z-10 drop-shadow-md">YEEEAAAYYY!!! 🎉</h1>
            </div>

            <!-- Body Kartu -->
            <div class="p-8 text-center bg-gradient-to-b from-white to-pink-50">
                <div class="text-6xl mb-4 animate-bounce">👩‍💼💼</div>
                <h2 class="text-2xl font-bold text-pink-600 mb-4">Selamat Lolos Interview!</h2>
                
                <p class="text-gray-600 mb-4 leading-relaxed">
                    Aku bangga banget sama kamu! Semua kerja keras, doa, dan rasa deg-degan kamu akhirnya terbayar lunas. Selamat datang di dunia kerja (lagi)!
                </p>
                <p class="text-pink-500 font-semibold mb-8 italic">
                    "Semoga di tempat yang baru ini, kamu makin bersinar, rezekinya lancar, dan selalu *happy* ya!" ✨
                </p>

                <!-- Area Interaktif: Tombol Hadiah -->
                <div id="reward-section">
                    <button id="btn-klaim" onclick="claimReward()" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-bold py-4 px-6 rounded-2xl shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-1 active:scale-95 flex items-center justify-center gap-2">
                        <span>🎁</span> Klik untuk lihat Hadiahmu! <span>🎁</span>
                    </button>
                </div>

                <!-- Voucher Digital (Disembunyikan di awal) -->
                <div id="voucher-card" class="hidden mt-4 bg-gradient-to-r from-pink-400 to-rose-400 text-white p-4 rounded-2xl shadow-inner border-2 border-dashed border-white">
                    <h3 class="font-bold text-lg mb-1">🎫 VOUCHER SPESIAL 🎫</h3>
                    <p class="text-sm font-medium">Berlaku untuk:</p>
                    <p class="text-xl font-bold text-yellow-200 mt-1 drop-shadow-sm">Traktir Makan Malam & Es Krim! 🍨</p>
                    <p class="text-xs mt-3 opacity-80">*Screenshot voucher ini dan kirim ke aku untuk ditukar hari ini juga! 💕</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Fungsi utama saat amplop diklik
        function openSurprise() {
            const intro = document.getElementById('intro-screen');
            const mainContent = document.getElementById('main-content');
            
            // 1. Pudarkan dan hilangkan layar pembuka
            intro.style.opacity = '0';
            setTimeout(() => {
                intro.style.display = 'none';
                
                // 2. Tampilkan pesan utama dengan animasi
                mainContent.classList.remove('hidden');
                // Sedikit delay agar display:block terender sebelum nambah class animasi
                setTimeout(() => {
                    mainContent.classList.add('animate-fade-in-up');
                }, 50);

                // 3. Mulai hujan hati (confetti)
                startHeartRain();
            }, 500); // 500ms sama dengan durasi transisi Tailwind
        }

        // Fungsi saat tombol hadiah diklik
        function claimReward() {
            const btnKlaim = document.getElementById('btn-klaim');
            const voucherCard = document.getElementById('voucher-card');

            // Sembunyikan tombol
            btnKlaim.style.display = 'none';
            
            // Tampilkan voucher dengan animasi bergoyang (tada)
            voucherCard.classList.remove('hidden');
            voucherCard.classList.add('animate-tada');

            // Tambahkan ekstra ledakan hati
            createHeartBurst();
        }

        // --- SISTEM PARTIKEL ANIMASI HATI --- //
        
        // Array warna dan emoji pink/lucu
        const emojis = ['💖', '💕', '🌸', '✨', '🎀', '💌'];
        
        function createHeart() {
            const heart = document.createElement('div');
            // Pilih emoji acak
            heart.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            heart.classList.add('falling-heart');
            
            // Posisi X acak
            heart.style.left = Math.random() * 100 + 'vw';
            
            // Ukuran acak
            const size = Math.random() * 1.5 + 1; // 1rem to 2.5rem
            heart.style.fontSize = size + 'rem';
            
            // Durasi jatuh acak (antara 3 sampai 6 detik)
            const duration = Math.random() * 3 + 3;
            heart.style.animationDuration = duration + 's';
            
            // Hapus elemen setelah selesai animasi agar memori tidak penuh
            setTimeout(() => {
                heart.remove();
            }, duration * 1000);
            
            document.body.appendChild(heart);
        }

        function startHeartRain() {
            // Buat hati pertama segera
            createHeartBurst();
            
            // Terus buat hati setiap 400ms
            setInterval(createHeart, 400);
        }

        function createHeartBurst() {
            // Buat banyak hati sekaligus
            for (let i = 0; i < 20; i++) {
                setTimeout(createHeart, Math.random() * 500);
            }
        }
    </script>
</body>
</html>
```
