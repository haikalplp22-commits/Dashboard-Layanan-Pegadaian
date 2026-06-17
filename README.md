<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kiosk Reservasi & Layanan - Pegadaian</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --pg-green: #006633;
            --pg-green-dark: #004d26;
            --pg-green-light: #e6f0eb;
            --pg-gold: #F1C40F;
            --pg-gold-dark: #d4ac0d;
            --bg-color: #f4f7f6;
            --text-main: #2d3748;
            --text-muted: #718096;
            --white: #ffffff;
            --danger: #e74c3c;
        }

        * { box-sizing: border-box; font-family: 'Poppins', sans-serif; margin: 0; padding: 0; }

        body {
            background-color: var(--bg-color);
            background-image: radial-gradient(circle at top right, #e6f0eb 0%, transparent 40%),
                              radial-gradient(circle at bottom left, #fcf6e3 0%, transparent 40%);
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
        }

        /* HEADER PEGADAIAN STYLE */
        header {
            background: linear-gradient(135deg, var(--pg-green) 0%, var(--pg-green-dark) 100%);
            color: var(--white);
            padding: 20px 50px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 20px rgba(0, 102, 51, 0.3);
            z-index: 20;
        }

        .logo-area { display: flex; align-items: center; gap: 15px; }
        .logo-placeholder {
            background: var(--white);
            color: var(--pg-green);
            width: 50px; height: 50px;
            border-radius: 50%;
            display: flex; justify-content: center; align-items: center;
            font-weight: 800; font-size: 24px;
            box-shadow: 0 0 15px rgba(241, 196, 15, 0.5);
        }
        .header-text h1 { font-size: 26px; font-weight: 700; letter-spacing: 0.5px; }
        .header-text p { color: var(--pg-gold); font-weight: 500; font-size: 14px; letter-spacing: 1px; text-transform: uppercase; }

        .time-area { text-align: right; }
        .time-area p { font-size: 12px; color: #e2e8f0; letter-spacing: 1px; }
        .time-area h2 { font-size: 28px; font-weight: 700; color: var(--pg-gold); }

        /* NEWS TICKER INTERAKTIF */
        .news-ticker {
            background-color: var(--pg-gold);
            color: var(--pg-green-dark);
            padding: 8px 50px;
            font-size: 14px;
            font-weight: 600;
            display: flex;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            z-index: 15;
            position: relative;
            overflow: hidden;
        }
        .news-label {
            background: var(--pg-green); color: var(--white);
            padding: 4px 15px; border-radius: 20px; font-size: 12px;
            margin-right: 15px; z-index: 2; position: relative;
        }
        .marquee {
            white-space: nowrap;
            overflow: hidden;
            display: inline-block;
            animation: marquee 25s linear infinite;
        }
        @keyframes marquee {
            0% { transform: translateX(100%); }
            100% { transform: translateX(-100%); }
        }

        /* NAVIGATION TABS */
        .nav-tabs {
            display: flex; justify-content: center; gap: 20px;
            padding: 20px 50px;
            background: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid #e2e8f0;
        }
        .tab-btn {
            padding: 12px 25px; font-size: 16px; font-weight: 600;
            background: var(--white); border: 2px solid #e2e8f0;
            border-radius: 30px; cursor: pointer; color: var(--text-muted);
            transition: 0.3s; display: flex; align-items: center; gap: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.02);
        }
        .tab-btn:hover { color: var(--pg-green); border-color: var(--pg-green); transform: translateY(-2px); }
        .tab-btn.active {
            color: var(--white); background: var(--pg-green);
            border-color: var(--pg-green); box-shadow: 0 4px 10px rgba(0,102,51,0.2);
        }

        /* CONTENT AREA */
        .content-area { flex: 1; padding: 20px 50px; overflow-y: auto; display: flex; justify-content: center; }
        .section { display: none; width: 100%; max-width: 1100px; animation: slideUp 0.4s ease forwards; }
        .section.active { display: block; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        .section-title { font-size: 26px; font-weight: 700; color: var(--pg-green-dark); margin-bottom: 5px; }
        .section-subtitle { font-size: 15px; color: var(--text-muted); margin-bottom: 25px; }

        /* PROMO SLIDER (GAMBAR BERJALAN) */
        .promo-slider {
            position: relative;
            width: 100%;
            height: 220px;
            border-radius: 16px;
            overflow: hidden;
            margin-bottom: 30px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            background-color: #000;
        }
        .slide {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }
        .slide.active { opacity: 1; z-index: 2; }
        
        .slide img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: brightness(0.65); /* Agar teks lebih mudah dibaca */
        }
        .promo-text {
            position: absolute;
            bottom: 0; left: 0; right: 0;
            background: linear-gradient(to top, rgba(0,77,38,0.95), transparent);
            color: white;
            padding: 40px 25px 20px;
        }
        .promo-text h3 { font-size: 24px; margin-bottom: 5px; color: var(--pg-gold); text-shadow: 1px 1px 3px rgba(0,0,0,0.3); }
        .promo-text p { font-size: 15px; opacity: 0.95; }

        /* 1. RESERVASI ANTREAN (REAL-TIME ESTIMATION) */
        .reservation-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 25px;
        }
        .res-card {
            background: var(--white); border-radius: 16px; padding: 25px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.05); position: relative;
            border: 2px solid transparent; transition: 0.3s; overflow: hidden;
        }
        .res-card:hover {
            border-color: var(--pg-green); transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,102,51,0.15);
        }
        .res-icon { font-size: 40px; margin-bottom: 10px; display: block; }
        .res-title { font-size: 20px; font-weight: 700; color: var(--text-main); margin-bottom: 15px; }
        
        .res-stats {
            background: var(--pg-green-light); padding: 15px; border-radius: 12px;
            display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;
        }
        .stat-item { display: flex; flex-direction: column; }
        .stat-label { font-size: 12px; color: var(--pg-green-dark); font-weight: 600; }
        .stat-value { font-size: 18px; font-weight: 800; color: var(--pg-green); }
        .stat-time { font-size: 18px; font-weight: 800; color: #d35400; }

        .btn-reserve {
            width: 100%; background: var(--pg-gold); color: var(--pg-green-dark);
            border: none; padding: 15px; font-size: 16px; font-weight: 700;
            border-radius: 10px; cursor: pointer; transition: 0.3s;
        }
        .btn-reserve:hover { background: var(--pg-gold-dark); color: var(--white); }

        /* 2. SIGNAGE / ALUR */
        .info-card { background: var(--white); padding: 30px; border-radius: 16px; box-shadow: 0 5px 15px rgba(0,0,0,0.05); }
        .timeline { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; margin-top: 20px; }
        .t-step { text-align: center; position: relative; }
        .t-icon {
            width: 70px; height: 70px; background: var(--pg-green-light); color: var(--pg-green);
            border-radius: 50%; display: flex; align-items: center; justify-content: center;
            font-size: 28px; margin: 0 auto 15px; font-weight: bold; border: 3px solid var(--white);
            box-shadow: 0 4px 10px rgba(0,102,51,0.1);
        }
        .t-step h4 { font-size: 16px; color: var(--pg-green-dark); margin-bottom: 10px; }
        .t-step p { font-size: 13px; color: var(--text-muted); }

        /* 3. FPK DIGITAL & FEEDBACK */
        .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .form-group { margin-bottom: 20px; }
        .form-group.full { grid-column: span 2; }
        .form-group label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 14px; color: var(--text-main); }
        .form-control {
            width: 100%; padding: 15px; font-size: 15px; border: 2px solid #e2e8f0;
            border-radius: 10px; background: #f8fafc; transition: 0.3s;
        }
        .form-control:focus { outline: none; border-color: var(--pg-green); background: var(--white); }
        .btn-submit {
            background: var(--pg-green); color: var(--white); border: none; padding: 15px 30px;
            font-size: 16px; font-weight: 600; border-radius: 10px; cursor: pointer; width: 100%; transition: 0.3s;
        }
        .btn-submit:hover { background: var(--pg-green-dark); }
        .rating-stars { display: flex; flex-direction: row-reverse; justify-content: center; font-size: 60px; cursor: pointer; margin: 20px 0; }
        .star { color: #e2e8f0; transition: 0.2s; padding: 0 5px; }
        .star.selected, .star:hover, .star:hover ~ .star { color: var(--pg-gold); transform: scale(1.1); }

        /* MODAL (TIKET RESERVASI REALISTIS) */
        .modal {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.6); backdrop-filter: blur(5px); justify-content: center; align-items: center; z-index: 100;
        }
        .ticket-receipt {
            background: var(--white); padding: 40px; width: 90%; max-width: 400px;
            text-align: center; border-radius: 10px; position: relative;
            box-shadow: 0 20px 50px rgba(0,0,0,0.3); border-top: 15px solid var(--pg-green);
        }
        .ticket-receipt h4 { color: var(--text-muted); font-size: 14px; margin-top: 10px; }
        .ticket-receipt h1 { color: var(--text-main); font-size: 60px; margin: 10px 0; border-bottom: 2px dashed #ccc; padding-bottom: 10px; }
        .est-box { background: #fff8e1; border: 1px solid var(--pg-gold); padding: 15px; border-radius: 8px; margin: 20px 0; }
        .est-box p { font-size: 12px; color: #d35400; font-weight: bold; margin-bottom: 5px; }
        .est-box h2 { font-size: 24px; color: var(--text-main); }
        .btn-close { background: var(--pg-green-light); color: var(--pg-green-dark); border: none; padding: 12px; font-weight: 700; border-radius: 8px; cursor: pointer; width: 100%; margin-top: 15px; }
    </style>
</head>
<body>

    <!-- HEADER PEGADAIAN -->
    <header>
        <div class="logo-area">
            <div class="logo-placeholder">P</div>
            <div class="header-text">
                <h1>Pegadaian</h1>
                <p>Melayani Dengan Sepenuh Hati</p>
            </div>
        </div>
        <div class="time-area">
            <p>WAKTU SETEMPAT</p>
            <h2 id="clock">00:00:00</h2>
        </div>
    </header>

    <!-- BERITA INTERAKTIF / NEWS TICKER -->
    <div class="news-ticker">
        <span class="news-label">INFO TERKINI</span>
        <div class="marquee">
            📢 Harga Emas Hari Ini: Rp 1.450.000/gram &nbsp;&nbsp; | &nbsp;&nbsp; 🟢 Promo Gadai & Cicil Emas DP Ringan &nbsp;&nbsp; | &nbsp;&nbsp; 📱 Gunakan Aplikasi Pegadaian Digital untuk kemudahan transaksi Anda &nbsp;&nbsp; | &nbsp;&nbsp; ⚠️ Waspada Penipuan! Pegadaian tidak pernah meminta OTP Anda.
        </div>
    </div>

    <!-- TABS NAVIGASI -->
    <div class="nav-tabs">
        <button class="tab-btn active" onclick="openTab('reservasi')">🎟️ Reservasi Antrean</button>
        <button class="tab-btn" onclick="openTab('info')">📖 Info & Signage</button>
        <button class="tab-btn" onclick="openTab('fpk')">📝 FPK Digital</button>
        <button class="tab-btn" onclick="openTab('feedback')">⭐ Penilaian Layanan</button>
    </div>

    <!-- MAIN CONTENT -->
    <div class="content-area">
        
        <!-- 1. RESERVASI & ESTIMASI REAL-TIME -->
        <div id="reservasi" class="section active">
            
            <!-- GAMBAR PROMO INFORMASI BERJALAN (SLIDER) -->
            <div class="promo-slider">
                <!-- Slide 1: Cicil Emas -->
                <div class="slide active">
                    <img src="https://images.unsplash.com/photo-1610375461246-83df859d849d?auto=format&fit=crop&w=1200&q=80" alt="Cicil Emas Pegadaian">
                    <div class="promo-text">
                        <h3>Cicil Emas Makin Mudah & Aman</h3>
                        <p>Miliki logam mulia impian dengan cicilan ringan mulai dari Rp 10.000an per hari khusus nasabah Pegadaian.</p>
                    </div>
                </div>
                <!-- Slide 2: Gadai Kendaraan -->
                <div class="slide">
                    <img src="https://images.unsplash.com/photo-1549317661-bd32c8ce0db2?auto=format&fit=crop&w=1200&q=80" alt="Gadai Kendaraan">
                    <div class="promo-text">
                        <h3>Gadai Kendaraan Proses Cepat</h3>
                        <p>Butuh dana mendesak? Gadai BPKB kendaraan Anda dengan prosedur mudah, aman, dan sewa modal ringan.</p>
                    </div>
                </div>
                <!-- Slide 3: Tabungan Emas -->
                <div class="slide">
                    <img src="https://images.unsplash.com/photo-1579621970563-ebec7560ff3e?auto=format&fit=crop&w=1200&q=80" alt="Tabungan Emas">
                    <div class="promo-text">
                        <h3>Investasi Tabungan Emas Pegadaian</h3>
                        <p>Mulai menabung emas untuk masa depan Anda. Beli dan titip emas mulai dari pecahan terkecil dengan mudah.</p>
                    </div>
                </div>
            </div>

            <h2 class="section-title">Reservasi Layanan Cerdas</h2>
            <p class="section-subtitle">Sistem otomatis menghitung estimasi waktu layanan Anda berdasarkan antrean yang sedang berjalan.</p>
            
            <div class="reservation-grid" id="queue-container">
                <!-- Kartu Antrean di-generate via JavaScript -->
            </div>
        </div>

        <!-- 2. INFO & SIGNAGE -->
        <div id="info" class="section">
            <div class="info-card">
                <h2 class="section-title">Alur Layanan Gadai</h2>
                <p class="section-subtitle">Proses cepat, aman, dan terpercaya di Pegadaian.</p>
                <div class="timeline">
                    <div class="t-step">
                        <div class="t-icon">1</div>
                        <h4>Reservasi / Ambil Tiket</h4>
                        <p>Pilih layanan pada layar kiosk ini untuk mendapatkan nomor antrean dan estimasi waktu.</p>
                    </div>
                    <div class="t-step">
                        <div class="t-icon">2</div>
                        <h4>Siapkan Dokumen</h4>
                        <p>Siapkan KTP asli dan barang jaminan (Emas, Elektronik, BPKB) yang ingin digadai.</p>
                    </div>
                    <div class="t-step">
                        <div class="t-icon">3</div>
                        <h4>Taksir Jaminan</h4>
                        <p>Penaksir kami akan memeriksa kondisi barang untuk menentukan nilai pinjaman maksimal.</p>
                    </div>
                    <div class="t-step">
                        <div class="t-icon">4</div>
                        <h4>Pencairan Tunai/Transfer</h4>
                        <p>Tanda tangani Surat Bukti Gadai (SBG) dan dana langsung cair ke tangan Anda.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 3. FPK DIGITAL (AUTOMATION) -->
        <div id="fpk" class="section">
            <div class="info-card">
                <h2 class="section-title">Formulir Pengajuan Digital (FPK)</h2>
                <p class="section-subtitle">Isi data diri Anda sembari menunggu untuk mempercepat proses administrasi di loket.</p>
                <form onsubmit="submitFPK(event)">
                    <div class="form-grid">
                        <div class="form-group full">
                            <label>Nama Lengkap Nasabah (Sesuai KTP)</label>
                            <input type="text" class="form-control" required placeholder="Masukkan Nama Anda">
                        </div>
                        <div class="form-group">
                            <label>Nomor Induk Kependudukan (NIK)</label>
                            <input type="number" class="form-control" required placeholder="16 Digit NIK">
                        </div>
                        <div class="form-group">
                            <label>Jenis Barang Jaminan</label>
                            <select class="form-control" required>
                                <option value="">-- Pilih Jenis Jaminan --</option>
                                <option value="emas">Emas Perhiasan / Logam Mulia</option>
                                <option value="elektronik">Barang Elektronik (HP/Laptop)</option>
                                <option value="kendaraan">Kendaraan Bermotor</option>
                            </select>
                        </div>
                    </div>
                    <button type="submit" class="btn-submit">Kirim Form ke Sistem Loket</button>
                </form>
            </div>
        </div>

        <!-- 4. FEEDBACK -->
        <div id="feedback" class="section">
            <div class="info-card" style="text-align: center; max-width: 700px; margin: 0 auto;">
                <h2 class="section-title">Penilaian Layanan</h2>
                <p class="section-subtitle">Bantu kami terus meningkatkan kualitas pelayanan Pegadaian kepada seluruh nasabah.</p>
                <div class="rating-stars">
                    <span class="star" data-value="5" onclick="setFeedback(5)">★</span>
                    <span class="star" data-value="4" onclick="setFeedback(4)">★</span>
                    <span class="star" data-value="3" onclick="setFeedback(3)">★</span>
                    <span class="star" data-value="2" onclick="setFeedback(2)">★</span>
                    <span class="star" data-value="1" onclick="setFeedback(1)">★</span>
                </div>
                <div class="form-group" style="text-align: left;">
                    <label>Saran & Masukan (Opsional)</label>
                    <textarea class="form-control" rows="3" placeholder="Ceritakan pengalaman Anda..."></textarea>
                </div>
                <button class="btn-submit" onclick="submitFeedback()">Kirim Penilaian</button>
            </div>
        </div>

    </div>

    <!-- MODAL TIKET RESERVASI -->
    <div id="popupModal" class="modal">
        <div class="ticket-receipt">
            <h2 style="color: var(--pg-green); font-weight: 800; margin-bottom: 5px;">PEGADAIAN</h2>
            <p style="font-size: 12px; color: #777;">Kiosk Layanan Mandiri</p>
            <h4 id="modalTitle">Layanan: Gadai Baru</h4>
            <h1 id="modalTicket">A-001</h1>
            
            <div class="est-box">
                <p>ESTIMASI DILAYANI PUKUL:</p>
                <h2 id="modalEstTime">14:30</h2>
            </div>
            
            <p style="font-size: 13px; color: var(--text-muted);">Silakan menuju ruang tunggu. Anda dapat memperkirakan waktu berdasarkan estimasi di atas.</p>
            <button class="btn-close" onclick="closeModal()">Selesai & Cetak Tiket</button>
        </div>
    </div>

    <script>
        // Logika Slider / Carousel Promo
        let currentSlide = 0;
        const slides = document.querySelectorAll('.slide');
        
        function showNextSlide() {
            slides[currentSlide].classList.remove('active');
            currentSlide = (currentSlide + 1) % slides.length;
            slides[currentSlide].classList.add('active');
        }
        // Ubah gambar otomatis setiap 5 detik
        setInterval(showNextSlide, 5000);

        // Data Antrean (Rata-rata layanan 12 menit)
        const avgServiceTime = 12; // menit
        const queueData = [
            { code: 'A', name: 'Gadai Baru', icon: '📄', waiting: 4, nextNum: 1 },
            { code: 'B', name: 'Perpanjangan', icon: '🔄', waiting: 2, nextNum: 1 },
            { code: 'C', name: 'Pelunasan', icon: '💰', waiting: 1, nextNum: 1 },
            { code: 'D', name: 'Tebus Barang', icon: '📦', waiting: 3, nextNum: 1 }
        ];

        // 1. Fungsi Clock & Real-Time Estimation Update
        function updateClockAndEstimations() {
            const now = new Date();
            // Update Jam Header
            document.getElementById('clock').innerText = now.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
            
            // Generate & Update Grid Kartu Antrean
            const container = document.getElementById('queue-container');
            container.innerHTML = ''; // Bersihkan kontainer

            queueData.forEach(q => {
                // Hitung Estimasi (Waktu Sekarang + (Jumlah Tunggu * 12 Menit))
                let estDate = new Date(now.getTime() + (q.waiting * avgServiceTime * 60000));
                let estTimeString = estDate.toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit' });

                let cardHTML = `
                    <div class="res-card">
                        <span class="res-icon">${q.icon}</span>
                        <div class="res-title">${q.name}</div>
                        <div class="res-stats">
                            <div class="stat-item">
                                <span class="stat-label">Menunggu</span>
                                <span class="stat-value">${q.waiting} Orang</span>
                            </div>
                            <div class="stat-item" style="text-align:right;">
                                <span class="stat-label">Estimasi Dilayani</span>
                                <span class="stat-time">${estTimeString}</span>
                            </div>
                        </div>
                        <button class="btn-reserve" onclick="takeReservation('${q.code}', '${q.name}', '${estTimeString}')">Ambil Reservasi</button>
                    </div>
                `;
                container.innerHTML += cardHTML;
            });
        }

        // Jalankan update setiap detik
        setInterval(updateClockAndEstimations, 1000);
        updateClockAndEstimations(); // Panggilan pertama

        // 2. Fungsi Navigasi Tab
        function openTab(tabId) {
            document.querySelectorAll('.section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            event.currentTarget.classList.add('active');
        }

        // 3. Fungsi Ambil Reservasi (Popup)
        function takeReservation(code, name, estTime) {
            let qIndex = queueData.findIndex(q => q.code === code);
            let currentNum = queueData[qIndex].nextNum;
            let formattedNum = code + "-" + currentNum.toString().padStart(3, '0');
            
            document.getElementById('modalTitle').innerText = "Layanan: " + name;
            document.getElementById('modalTicket').innerText = formattedNum;
            document.getElementById('modalEstTime').innerText = estTime;
            
            document.getElementById('popupModal').style.display = 'flex';
            
            // Update Data untuk nasabah berikutnya
            queueData[qIndex].nextNum++;
            queueData[qIndex].waiting++;
            updateClockAndEstimations(); // Segarkan tampilan seketika
        }

        // 4. Submit FPK
        function submitFPK(e) {
            e.preventDefault();
            alert("Data Formulir Pengajuan Kredit berhasil dikirim ke Sistem Loket. Terima kasih!");
            e.target.reset();
            openTab('reservasi');
        }

        // 5. Logic Feedback
        let selectedStar = 0;
        function setFeedback(rating) {
            selectedStar = rating;
            let stars = document.querySelectorAll('.star');
            stars.forEach(s => s.classList.remove('selected'));
            event.target.classList.add('selected');
            let prev = event.target.nextElementSibling;
            while(prev) { prev.classList.add('selected'); prev = prev.nextElementSibling; }
        }
        function submitFeedback() {
            if (selectedStar === 0) return alert("Pilih bintang penilaian terlebih dahulu.");
            alert("Terima kasih atas penilaian Anda! Data telah direkap untuk memonitor kinerja pelayanan kami.");
            selectedStar = 0;
            document.querySelectorAll('.star').forEach(s => s.classList.remove('selected'));
            document.querySelector('#feedback textarea').value = "";
            openTab('reservasi');
        }

        function closeModal() { document.getElementById('popupModal').style.display = 'none'; }
    </script>
</body>
</html>
