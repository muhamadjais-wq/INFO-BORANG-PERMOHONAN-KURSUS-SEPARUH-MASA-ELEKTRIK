<!DOCTYPE html>
<html lang="ms-MY" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portal Rasmi Kompetensi Elektrik | IKBN Kinarut Sabah</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Oswald:wght@500;700&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <style>
        :root {
            --ikbn-blue: #0f172a;
            --ikbn-accent: #fbbf24;
            --ikbn-gold: #d97706;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #f8fafc;
            color: #1e293b;
        }

        .heading-font { font-family: 'Oswald', sans-serif; }

        .glass-morphism {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(0, 0, 0, 0.05);
        }

        .hero-gradient {
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
        }

        .action-card {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid rgba(0, 0, 0, 0.05);
            cursor: pointer;
        }

        .action-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.12);
            border-color: var(--ikbn-accent);
        }

        /* Visualizer Suara AI */
        .bar { width: 5px; background: var(--ikbn-accent); border-radius: 5px; height: 4px; transition: height 0.15s ease; }
        .anim-voice .bar { animation: voice-wave 0.5s infinite ease-in-out alternate; }
        .anim-voice .bar:nth-child(1) { animation-delay: 0.1s; }
        .anim-voice .bar:nth-child(2) { animation-delay: 0.3s; }
        .anim-voice .bar:nth-child(3) { animation-delay: 0.2s; }
        .anim-voice .bar:nth-child(4) { animation-delay: 0.4s; }
        .anim-voice .bar:nth-child(5) { animation-delay: 0.1s; }
        
        @keyframes voice-wave { from { height: 4px; } to { height: 32px; } }

        @keyframes floating {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        .float-anim { animation: floating 4s ease-in-out infinite; }
    </style>
</head>
<body class="antialiased">

    <!-- Navigasi -->
    <nav class="fixed top-0 w-full z-50 glass-morphism h-20">
        <div class="max-w-7xl mx-auto px-4 h-full flex items-center justify-between">
            <div class="flex items-center gap-4 cursor-pointer" onclick="window.scrollTo({top:0, behavior:'smooth'})">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Coat_of_arms_of_Malaysia.svg/1200px-High_Court_of_Malaya_Seal.svg.png" class="h-10 w-auto" alt="Logo Malaysia">
                <div class="h-8 w-[1px] bg-slate-200"></div>
                <div>
                    <h1 class="heading-font text-xl leading-none uppercase tracking-tight text-slate-900 text-sm md:text-xl">Jabatan Elektrik</h1>
                    <p class="text-[10px] text-slate-500 font-black tracking-[0.2em] uppercase leading-none mt-1">IKBN Kinarut Sabah</p>
                </div>
            </div>
            
            <div class="hidden lg:flex items-center gap-8 text-[11px] font-bold uppercase tracking-widest text-slate-600">
                <button onclick="scrollToId('pusat-tindakan')" class="hover:text-amber-600 transition">Panduan Pantas</button>
                <button onclick="scrollToId('kursus')" class="hover:text-amber-600 transition text-slate-900 font-black">Katalog Program</button>
                <button onclick="scrollToId('muat-turun')" class="hover:text-amber-600 transition">Muat Turun</button>
                <a href="#hubungi" class="bg-slate-900 text-white px-6 py-3 rounded-full hover:bg-amber-500 hover:text-slate-900 transition shadow-lg flex items-center gap-2">
                    <i data-lucide="phone" class="w-4 h-4 text-amber-400"></i> Hubungi Urusetia
                </a>
            </div>
            
            <button class="lg:hidden p-2 text-slate-900" onclick="toggleMenu()" aria-label="Menu">
                <i data-lucide="menu" id="menu-icon" class="w-6 h-6"></i>
            </button>
        </div>

        <div id="mobile-menu" class="hidden lg:hidden absolute top-20 left-0 w-full bg-white border-b border-slate-200 p-6 space-y-4 shadow-2xl">
            <button onclick="scrollToId('pusat-tindakan'); toggleMenu();" class="block w-full text-left font-bold text-slate-700">Pusat Tindakan</button>
            <button onclick="scrollToId('kursus'); toggleMenu();" class="block w-full text-left font-bold text-slate-700">Katalog Kursus</button>
            <button onclick="scrollToId('muat-turun'); toggleMenu();" class="block w-full text-left font-bold text-slate-700">Muat Turun Borang</button>
            <a href="#hubungi" onclick="toggleMenu()" class="block text-center py-3 bg-slate-900 text-white rounded-xl font-bold">Hubungi Urusetia</a>
        </div>
    </nav>

    <!-- Hero -->
    <header class="pt-40 pb-28 hero-gradient relative overflow-hidden">
        <canvas id="hero-bg" class="absolute inset-0 opacity-10"></canvas>
        <div class="max-w-7xl mx-auto px-4 relative z-10 text-center md:text-left">
            <div class="max-w-4xl text-center md:text-left">
                <div class="inline-flex items-center gap-3 bg-amber-500/10 text-amber-400 px-5 py-2.5 rounded-full text-[10px] font-black uppercase tracking-[0.25em] mb-8 border border-amber-500/20 mx-auto md:mx-0">
                    <span class="w-2 h-2 bg-amber-400 rounded-full animate-ping"></span>
                    Pengambilan Sesi 2026 Kini Dibuka
                </div>
                <h2 class="heading-font text-5xl md:text-8xl text-white mb-8 leading-[0.9] tracking-tight">
                    Smart <br><span class="text-amber-400 underline decoration-amber-400/20 underline-offset-[12px]">Kompetensi</span> Portal.
                </h2>
                <p class="text-slate-400 text-lg md:text-xl mb-12 leading-relaxed font-light max-w-2xl mx-auto md:mx-0">
                    Sistem panduan pendaftaran bersepadu mengikut standard **Energy Commission of Sabah (ECoS)**.
                </p>
                <div class="flex flex-wrap gap-5 justify-center md:justify-start">
                    <button onclick="scrollToId('kursus')" class="bg-amber-400 text-slate-900 px-10 py-5 rounded-2xl font-black text-sm uppercase tracking-widest hover:scale-105 transition shadow-[0_20px_50px_rgba(251,191,36,0.3)] flex items-center gap-3">
                        Pilih Program <i data-lucide="arrow-right" class="w-5 h-5"></i>
                    </button>
                    <button onclick="openAssistant()" class="bg-white/5 text-white border border-white/10 px-10 py-5 rounded-2xl font-black text-sm uppercase tracking-widest hover:bg-white/10 transition flex items-center gap-3 backdrop-blur-md">
                        <i data-lucide="bot" class="w-6 h-6 text-amber-400"></i> AI Advisor
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Pusat Tindakan -->
    <section id="pusat-tindakan" class="max-w-7xl mx-auto px-4 -mt-14 relative z-20">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
            <div onclick="scrollToId('muat-turun')" class="action-card bg-white p-8 rounded-[2rem] shadow-2xl border-t-4 border-blue-500">
                <div class="w-14 h-14 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center mb-6 shadow-inner"><i data-lucide="file-down" class="w-7 h-7"></i></div>
                <h3 class="text-xl font-black heading-font uppercase mb-3 tracking-tight text-slate-900">Muat Turun</h3>
                <p class="text-xs text-slate-500 mb-6 leading-relaxed">Borang Permohonan Manual (PDF) & Borang Kesihatan.</p>
                <span class="font-bold text-blue-600 text-[10px] uppercase tracking-widest flex items-center gap-2">Pusat Borang <i data-lucide="arrow-right" class="w-3 h-3"></i></span>
            </div>

            <a href="https://drive.google.com/file/d/1HCY6r9OAjv915onsiJChearIIb4TU1tg/view?usp=sharing" target="_blank" class="action-card bg-white p-8 rounded-[2rem] shadow-2xl border-t-4 border-purple-500">
                <div class="w-14 h-14 bg-purple-50 text-purple-600 rounded-2xl flex items-center justify-center mb-6 shadow-inner"><i data-lucide="calendar" class="w-7 h-7"></i></div>
                <h3 class="text-xl font-black heading-font uppercase mb-3 tracking-tight text-slate-900">Perancangan 2026</h3>
                <p class="text-xs text-slate-500 mb-6 leading-relaxed text-red-600 font-bold">Jadual Pengambilan Terbaru.</p>
                <span class="font-bold text-purple-600 text-[10px] uppercase tracking-widest flex items-center gap-2">Buka Fail <i data-lucide="external-link" class="w-3 h-3"></i></span>
            </a>

            <div onclick="scrollToId('kursus')" class="action-card bg-slate-900 p-8 rounded-[2rem] shadow-2xl text-white border-t-4 border-amber-400">
                <div class="w-14 h-14 bg-amber-400 text-slate-900 rounded-2xl flex items-center justify-center mb-6 shadow-xl shadow-amber-400/20"><i data-lucide="upload-cloud" class="w-7 h-7"></i></div>
                <h3 class="text-xl font-black heading-font uppercase mb-3 tracking-tight text-amber-400">Daftar & Upload</h3>
                <p class="text-xs text-slate-400 mb-6 leading-relaxed text-slate-300">Pilih kursus di bawah untuk pautan hantaran dokumen.</p>
                <span class="font-bold text-amber-400 text-[10px] uppercase tracking-widest flex items-center gap-2">Pilih Kursus <i data-lucide="arrow-right" class="w-3 h-3"></i></span>
            </div>

            <div onclick="openAssistant()" class="action-card bg-white p-8 rounded-[2rem] shadow-2xl border-t-4 border-green-500">
                <div class="w-14 h-14 bg-green-50 text-green-600 rounded-2xl flex items-center justify-center mb-6 shadow-inner"><i data-lucide="sparkles" class="w-7 h-7"></i></div>
                <h3 class="text-xl font-black heading-font uppercase mb-3 tracking-tight text-green-600 text-slate-900">Smart Semakan</h3>
                <p class="text-xs text-slate-500 mb-6 leading-relaxed">AI Advisor untuk cadangan laluan kerjaya anda.</p>
                <span class="font-bold text-green-600 text-[10px] uppercase tracking-widest flex items-center gap-2">Bantuan AI <i data-lucide="sparkles" class="w-3 h-3"></i></span>
            </div>
        </div>
    </section>

    <main class="max-w-7xl mx-auto px-4 py-28 space-y-48">

        <!-- KATALOG PROGRAM -->
        <section id="kursus" class="scroll-mt-24">
            <div class="flex flex-col lg:flex-row justify-between items-end gap-10 mb-20 border-b border-slate-100 pb-12 text-center lg:text-left">
                <div class="max-w-2xl mx-auto lg:mx-0">
                    <h2 class="heading-font text-5xl md:text-6xl uppercase mb-6 leading-none text-slate-900">Katalog Program</h2>
                    <p class="text-slate-500 text-lg">Pendaftaran lengkap mengikut kategori kompetensi.</p>
                </div>
                <div class="bg-slate-100 p-2 rounded-3xl flex gap-1 shadow-inner mx-auto lg:mx-0">
                    <button onclick="scrollToId('section-pw')" class="px-8 py-4 rounded-2xl bg-white shadow-lg font-black text-[10px] uppercase tracking-[0.2em] transition-all hover:bg-amber-400">Kategori PW</button>
                    <button onclick="scrollToId('section-chargeman')" class="px-8 py-4 rounded-2xl hover:bg-white transition-all font-black text-[10px] uppercase tracking-[0.2em] text-slate-500 hover:text-slate-900">Chargeman (A/B)</button>
                </div>
            </div>

            <div class="space-y-40">
                <!-- SECTION PW -->
                <div id="section-pw" class="scroll-mt-32">
                    <h3 class="flex items-center gap-5 text-sm font-black uppercase tracking-[0.5em] text-slate-400 mb-12">
                        <span class="w-16 h-1 bg-blue-500 rounded-full"></span> Pendawai / Wireman
                    </h3>
                    <div class="grid md:grid-cols-2 gap-10">
                        <!-- PW2 -->
                        <div class="bg-white rounded-[3rem] overflow-hidden border border-slate-100 shadow-sm hover:shadow-2xl transition-all duration-500">
                            <div class="bg-slate-900 p-12 text-white relative overflow-hidden">
                                <h4 class="text-5xl font-black heading-font text-amber-400 uppercase tracking-tight">PW2</h4>
                                <p class="text-slate-500 font-bold uppercase text-xs tracking-[0.3em] mt-3 tracking-tighter">Single Phase</p>
                            </div>
                            <div class="p-12 text-center md:text-left">
                                <div class="flex flex-col gap-4">
                                    <a href="#hubungi" class="w-full py-5 bg-slate-900 text-white text-center rounded-[1.5rem] font-black text-xs uppercase tracking-widest hover:bg-amber-400 hover:text-slate-900 transition">Hubungi Urusetia</a>
                                    <a href="https://forms.gle/uvJa9qgGkYsAcFVr7" target="_blank" class="w-full py-4 border-2 border-slate-100 text-slate-400 text-center rounded-[1.5rem] font-bold text-xs uppercase tracking-widest hover:bg-slate-50 transition flex items-center justify-center gap-2">
                                        <i data-lucide="external-link" class="w-4 h-4"></i> Daftar Minat & Muat Naik
                                    </a>
                                </div>
                            </div>
                        </div>
                        <!-- PW4 -->
                        <div class="bg-white rounded-[3rem] overflow-hidden border border-slate-100 shadow-sm hover:shadow-2xl transition-all duration-500">
                            <div class="bg-slate-900 p-12 text-white relative">
                                <h4 class="text-5xl font-black heading-font text-amber-400 uppercase tracking-tight">PW4</h4>
                                <p class="text-slate-500 font-bold uppercase text-xs tracking-[0.3em] mt-3 tracking-tighter">Three Phase</p>
                            </div>
                            <div class="p-12 text-center md:text-left">
                                <div class="flex flex-col gap-4">
                                    <button onclick="scrollToId('hubungi')" class="w-full py-5 bg-orange-500 text-white text-center rounded-[1.5rem] font-black text-xs uppercase tracking-widest hover:bg-orange-600 transition shadow-xl">Hubungi Urusetia</button>
                                    <a href="https://forms.gle/uvJa9qgGkYsAcFVr7" target="_blank" class="w-full py-4 border-2 border-slate-100 text-slate-400 text-center rounded-[1.5rem] font-bold text-xs uppercase tracking-widest hover:bg-slate-50 transition flex items-center justify-center gap-2">
                                        <i data-lucide="external-link" class="w-4 h-4"></i> Daftar Minat & Muat Naik
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- SECTION CHARGEMAN -->
                <div id="section-chargeman" class="pt-10 scroll-mt-32">
                    <h3 class="flex items-center gap-5 text-sm font-black uppercase tracking-[0.5em] text-slate-400 mb-12">
                        <span class="w-16 h-1 bg-amber-500 rounded-full"></span> Chargeman / Penjaga Jentera
                    </h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="bg-white p-8 rounded-[2.5rem] border border-slate-100 flex flex-col justify-between hover:border-amber-400 transition-all shadow-sm">
                            <div>
                                <div class="w-14 h-14 bg-amber-100 text-amber-700 rounded-[1.2rem] flex items-center justify-center font-black text-xl mb-6 shadow-inner">A0</div>
                                <h4 class="text-xl font-black heading-font uppercase mb-4 text-slate-900">Asas VR</h4>
                                <p class="text-[10px] text-slate-400 mb-6 font-bold uppercase tracking-widest">Sistem Tanpa Janakuasa</p>
                            </div>
                            <a href="https://forms.gle/ZeXBrrAGaYtxr2u67" target="_blank" class="w-full py-4 bg-slate-900 text-white text-center rounded-2xl font-bold text-[10px] uppercase tracking-widest hover:bg-amber-400 hover:text-slate-900 transition">Daftar & Upload A0</a>
                        </div>
                        <div class="bg-white p-8 rounded-[2.5rem] border border-slate-100 flex flex-col justify-between hover:border-amber-400 transition-all shadow-sm">
                            <div>
                                <div class="w-14 h-14 bg-amber-100 text-amber-700 rounded-[1.2rem] flex items-center justify-center font-black text-xl mb-6 shadow-inner">A1</div>
                                <h4 class="text-xl font-black heading-font uppercase mb-4 text-slate-900">VR + Talian</h4>
                                <p class="text-[10px] text-slate-400 mb-6 font-bold uppercase tracking-widest">Sistem Talian Atas</p>
                            </div>
                            <a href="https://forms.gle/TJpNuYjMt9GUGNHG8" target="_blank" class="w-full py-4 bg-slate-900 text-white text-center rounded-2xl font-bold text-[10px] uppercase tracking-widest hover:bg-amber-400 hover:text-slate-900 transition">Daftar & Upload A1</a>
                        </div>
                        <div class="bg-white p-8 rounded-[2.5rem] border border-slate-100 flex flex-col justify-between hover:border-amber-400 transition-all shadow-sm">
                            <div>
                                <div class="w-14 h-14 bg-amber-100 text-amber-700 rounded-[1.2rem] flex items-center justify-center font-black text-xl mb-6 shadow-inner">A4</div>
                                <h4 class="text-xl font-black heading-font uppercase mb-4 text-slate-900">VR Penuh</h4>
                                <p class="text-[10px] text-slate-400 mb-6 font-bold uppercase tracking-widest">Termasuk Janakuasa</p>
                            </div>
                            <a href="https://forms.gle/28Fy1RD8dZukcUrP6" target="_blank" class="w-full py-4 bg-slate-900 text-white text-center rounded-2xl font-bold text-[10px] uppercase tracking-widest hover:bg-amber-400 hover:text-slate-900 transition shadow-md">Daftar & Upload A4</a>
                        </div>
                        <div class="bg-slate-900 p-8 rounded-[2.5rem] border-2 border-amber-400/30 flex flex-col justify-between hover:border-amber-400 transition-all shadow-2xl relative overflow-hidden">
                            <div class="absolute -right-4 -top-4 w-20 h-20 bg-amber-400 opacity-10 rounded-full"></div>
                            <div>
                                <div class="w-14 h-14 bg-amber-400 text-slate-900 rounded-[1.2rem] flex items-center justify-center font-black text-xl mb-6 shadow-xl shadow-amber-400/20">B0</div>
                                <h4 class="text-xl font-black heading-font uppercase mb-4 text-amber-400">Voltan Tinggi</h4>
                                <p class="text-[10px] text-slate-400 mb-6 font-bold uppercase tracking-widest">11kV (Penuh & Terhad)</p>
                            </div>
                            <div class="space-y-3">
                                <a href="https://forms.gle/zaMeYgkWMUbQ1HP18" target="_blank" class="block w-full py-3 bg-amber-400 text-slate-900 text-center rounded-xl font-black text-[10px] uppercase tracking-widest hover:bg-white transition">Daftar B0 Penuh</a>
                                <a href="https://forms.gle/3cAfRxsn9AQe63Mv5" target="_blank" class="block w-full py-3 border border-white/20 text-white text-center rounded-xl font-bold text-[10px] uppercase tracking-widest hover:bg-white/5 transition">Modul B0 Terhad</a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- B0 DETAILED INFO SECTION -->
                <div class="bg-slate-900 rounded-[4rem] p-10 md:p-20 text-white relative overflow-hidden border-b-8 border-amber-400">
                    <div class="absolute top-0 right-0 w-full h-full bg-[radial-gradient(circle_at_top_right,rgba(251,191,36,0.1),transparent)]"></div>
                    <div class="relative z-10 grid lg:grid-cols-2 gap-20 items-center">
                        <div>
                            <span class="text-amber-400 font-black uppercase tracking-[0.4em] text-[11px] mb-6 block">Panduan Pendaftaran B0</span>
                            <h3 class="heading-font text-6xl md:text-7xl mb-8 uppercase leading-none tracking-tight">Kategori B0 11kV</h3>
                            <p class="text-slate-400 text-xl leading-relaxed mb-12 font-light text-left">
                                Sila pastikan anda memilih pautan pendaftaran yang tepat mengikut kelayakan pengalaman High Voltage (HV) anda.
                            </p>
                            
                            <div class="grid grid-cols-1 gap-8">
                                <div class="p-8 bg-white/5 rounded-[2rem] border border-white/10 group hover:bg-white/10 transition-all">
                                    <h5 class="text-amber-400 font-black uppercase tracking-widest text-sm mb-3">01. B0 Penuh (11kV Full)</h5>
                                    <p class="text-sm text-slate-400 leading-relaxed italic">Wajib memiliki perakuan A4 selama 2 tahun dan pengalaman kerja di sistem HV secara 'live' selama 2 tahun.</p>
                                </div>
                                <div class="p-8 bg-amber-400/10 rounded-[2rem] border border-amber-400/30 group hover:bg-amber-400/20 transition-all">
                                    <h5 class="text-amber-400 font-black uppercase tracking-widest text-sm mb-3 underline underline-offset-8 decoration-amber-400/30 text-white">02. B0 Terhad (Pencawang)</h5>
                                    <p class="text-sm text-slate-300 leading-relaxed font-semibold">Jika tiada pengalaman kerja HV, anda wajib melengkapkan Modul MKP (Kendalian Pencawang 11kV) selama 80 jam terlebih dahulu.</p>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white p-12 rounded-[3.5rem] text-slate-900 shadow-2xl">
                            <h4 class="font-black heading-font text-2xl uppercase mb-8 border-b-2 border-slate-100 pb-4">Checklist Dokumen B0</h4>
                            <ul class="space-y-6 text-sm font-bold text-slate-600">
                                <li class="flex gap-4 items-start"><i data-lucide="check-square" class="w-5 h-5 text-amber-500 shrink-0 mt-1"></i> <span>Buku Log HV Original (Lengkap & Disahkan)</span></li>
                                <li class="flex gap-4 items-start"><i data-lucide="check-square" class="w-5 h-5 text-amber-500 shrink-0 mt-1"></i> <span>Salinan Sijil Perakuan A4 (Disahkan ECoS)</span></li>
                                <li class="flex gap-4 items-start"><i data-lucide="check-square" class="w-5 h-5 text-amber-500 shrink-0 mt-1"></i> <span>Surat Pengesahan Majikan (Berdaftar ECoS)</span></li>
                                <li class="flex gap-4 items-start"><i data-lucide="check-square" class="w-5 h-5 text-amber-500 shrink-0 mt-1"></i> <span>Borang Kesihatan (Isi melalui Google Form)</span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- MUAT TURUN HAB -->
        <section id="muat-turun" class="bg-white p-12 md:p-24 rounded-[5rem] border border-slate-100 shadow-2xl scroll-mt-24">
            <div class="max-w-4xl mx-auto">
                <div class="text-center mb-20">
                    <span class="text-blue-600 font-black text-xs uppercase tracking-[0.5em] mb-4 block">Pusat Borang</span>
                    <h2 class="heading-font text-5xl uppercase mb-6 leading-none tracking-tight text-slate-900">Download Dokumen</h2>
                    <p class="text-slate-500 text-lg">Semua dokumen manual yang diperlukan untuk sesi pengambilan 2026.</p>
                </div>
                <div class="space-y-6">
                    <div class="flex flex-col md:flex-row items-center justify-between p-8 bg-slate-50 rounded-[2.5rem] group hover:bg-white hover:shadow-2xl transition-all border border-transparent hover:border-blue-100 text-center md:text-left">
                        <div class="flex items-center gap-8 mb-6 md:mb-0">
                            <div class="w-20 h-20 bg-white rounded-[1.5rem] flex items-center justify-center text-blue-600 shadow-inner group-hover:bg-blue-600 group-hover:text-white transition-all"><i data-lucide="file-text" class="w-10 h-10"></i></div>
                            <div><h4 class="font-black uppercase text-lg tracking-tight text-slate-800">Borang Permohonan (PDF)</h4><p class="text-[10px] text-slate-400 font-black uppercase mt-1 tracking-widest">Manual Fill Required</p></div>
                        </div>
                        <a href="https://drive.google.com/file/d/1715CZNVigrQBpf5nZ0Zne6Rne8xC8tUF/view?usp=sharing" target="_blank" class="px-12 py-5 bg-white border-2 border-slate-200 rounded-[1.5rem] font-black text-xs uppercase tracking-widest hover:bg-slate-900 hover:text-white transition-all shadow-sm">Muat Turun</a>
                    </div>
                    <div class="flex flex-col md:flex-row items-center justify-between p-8 bg-slate-50 rounded-[2.5rem] group hover:bg-white hover:shadow-2xl transition-all border border-transparent hover:border-red-100 text-center md:text-left">
                        <div class="flex items-center gap-8 mb-6 md:mb-0">
                            <div class="w-20 h-20 bg-white rounded-[1.5rem] flex items-center justify-center text-red-600 shadow-inner group-hover:bg-red-600 group-hover:text-white transition-all"><i data-lucide="stethoscope" class="w-10 h-10"></i></div>
                            <div><h4 class="font-black uppercase text-lg tracking-tight text-slate-800">Borang Kesihatan ECoS</h4><p class="text-[10px] text-slate-400 font-black uppercase mt-1 tracking-widest">Pemeriksaan Doktor Online</p></div>
                        </div>
                        <a href="https://forms.gle/oz5bwhKqC8yEid226" target="_blank" class="px-12 py-5 bg-white border-2 border-slate-200 rounded-[1.5rem] font-black text-xs uppercase tracking-widest hover:bg-red-600 hover:text-white transition-all shadow-sm text-center">Isi Online</a>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Modal Advisor AI -->
    <div id="assistant-modal" class="fixed inset-0 z-[100] hidden bg-slate-900/98 backdrop-blur-3xl flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white w-full max-w-5xl rounded-[3.5rem] shadow-2xl overflow-hidden my-12">
            <div class="bg-slate-900 p-10 text-white flex justify-between items-center sticky top-0 z-20">
                <div class="flex items-center gap-6">
                    <div class="w-20 h-20 bg-amber-400 rounded-[1.8rem] flex items-center justify-center text-slate-900 float-anim shadow-2xl shadow-amber-400/20"><i data-lucide="bot" class="w-10 h-10"></i></div>
                    <div>
                        <h3 class="font-black heading-font text-3xl uppercase tracking-tighter">Smart Advisor 2.0</h3>
                        <div id="voice-indicator" class="hidden flex items-center gap-1.5 mt-3 anim-voice">
                            <div class="bar"></div><div class="bar"></div><div class="bar"></div><div class="bar"></div><div class="bar"></div>
                            <span class="text-[10px] font-black uppercase tracking-[0.2em] ml-2 text-amber-400 leading-none">Suara Aktif</span>
                        </div>
                    </div>
                </div>
                <button onclick="closeAssistant()" class="p-4 hover:bg-white/10 rounded-full transition active:scale-90"><i data-lucide="x" class="w-8 h-8"></i></button>
            </div>
            <div class="p-10 text-center">
                <div id="assistant-steps">
                    <p class="text-slate-500 mb-10 font-bold text-xl tracking-tight text-center">Sila pilih profil semasa anda untuk syarat lengkap:</p>
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                        <button onclick="analyzePathway('SPM')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="graduation-cap" class="w-8 h-8 text-slate-600 group-hover:text-slate-900"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Lepasan SPM / T5</span>
                        </button>
                        <button onclick="analyzePathway('PW2')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="zap" class="w-8 h-8 text-slate-600 group-hover:text-slate-900"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Memiliki Sijil PW 2</span>
                        </button>
                        <button onclick="analyzePathway('A0')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="activity" class="w-8 h-8 text-slate-600 group-hover:text-slate-900"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Memiliki Perakuan A0</span>
                        </button>
                        <button onclick="analyzePathway('A1')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="award" class="w-8 h-8 text-slate-600 group-hover:text-slate-900"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Memiliki Perakuan A1</span>
                        </button>
                        <button onclick="analyzePathway('A4')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="shield-check" class="w-8 h-8 text-slate-600 group-hover:text-slate-900"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Memiliki Perakuan A4</span>
                        </button>
                        <button onclick="analyzePathway('NON_COMPETENT')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-red-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-red-400 transition-colors shadow-sm group-hover:text-white"><i data-lucide="shield-off" class="w-8 h-8 text-slate-600 group-hover:text-inherit"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Tiada Sijil</span>
                        </button>
                        <button onclick="analyzePathway('NO_COMPANY')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-slate-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-slate-400 transition-colors shadow-sm group-hover:text-white"><i data-lucide="briefcase" class="w-8 h-8 text-slate-600 group-hover:text-inherit"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Tiada Majikan</span>
                        </button>
                        <button onclick="analyzePathway('NO_EXPERIENCE')" class="p-6 border-2 border-slate-50 bg-slate-50 rounded-[2rem] text-left hover:border-amber-400 hover:bg-white transition-all flex flex-col items-center gap-4 group">
                            <div class="p-4 bg-white rounded-2xl group-hover:bg-amber-400 transition-colors shadow-sm"><i data-lucide="clock" class="w-8 h-8 text-slate-600 group-hover:text-inherit"></i></div>
                            <span class="text-[10px] font-black uppercase text-center leading-tight text-slate-900">Kurang Pengalaman</span>
                        </button>
                    </div>
                </div>
                <div id="assistant-result" class="hidden text-left">
                    <div class="bg-slate-900/5 p-12 rounded-[3.5rem] border border-slate-100 mb-10 max-h-[500px] overflow-y-auto">
                        <p id="result-text" class="text-slate-800 leading-relaxed text-lg font-medium whitespace-pre-line text-left"></p>
                    </div>
                    <div class="flex gap-4">
                        <button onclick="resetAssistant()" class="flex-1 py-6 border-2 border-slate-100 rounded-3xl font-black text-xs uppercase tracking-widest hover:bg-slate-50 transition active:scale-95">Mula Semula</button>
                        <button onclick="stopSpeech()" id="stop-speech-btn" class="hidden flex-none px-12 py-6 border-2 border-red-100 text-red-600 rounded-3xl hover:bg-red-50 transition active:scale-90" title="Berhenti Suara">
                            <i data-lucide="volume-x" class="w-6 h-6"></i>
                        </button>
                        <button onclick="repeatSpeech()" class="flex-none px-14 py-6 bg-amber-400 text-slate-900 rounded-3xl transition shadow-xl active:scale-90"><i data-lucide="volume-2" class="w-6 h-6"></i></button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Floating UI -->
    <button onclick="openAssistant()" class="fixed bottom-10 right-10 z-[90] w-20 h-20 bg-amber-400 text-slate-900 rounded-[2.2rem] shadow-2xl flex items-center justify-center hover:scale-110 active:scale-95 transition-all float-anim border-4 border-white p-6">
        <i data-lucide="bot" class="w-10 h-10"></i>
    </button>

    <!-- Footer -->
    <footer id="hubungi" class="bg-slate-900 text-white py-32 border-t-[14px] border-amber-400">
        <div class="max-w-7xl mx-auto px-4 grid md:grid-cols-4 gap-20">
            <div class="md:col-span-1 text-center md:text-left mx-auto md:mx-0">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Coat_of_arms_of_Malaysia.svg/1200px-High_Court_of_Malaya_Seal.svg.png" class="h-16 w-auto mb-10 mx-auto md:mx-0" alt="Logo Malaysia">
                <h4 class="heading-font text-3xl text-amber-400 mb-6 uppercase tracking-tight leading-none text-white">IKBN Kinarut Sabah</h4>
                <p class="text-slate-500 text-[10px] font-black uppercase tracking-[0.4em] leading-loose">Jabatan Elektrik.</p>
            </div>
            
            <div>
                <h5 class="font-black text-amber-400 uppercase text-[10px] tracking-[0.6em] mb-12 text-slate-400">Pegawai Urusetia</h5>
                <div class="space-y-10 text-sm">
                    <p class="text-white text-center lg:text-left">En. Muhamad Jais <br><span class="text-slate-400 font-bold">017-898 6747</span></p>
                    <p class="text-white text-center lg:text-left">En. Hanif <br><span class="text-slate-400 font-bold">012-511 9108</span></p>
                </div>
            </div>

            <div>
                <h5 class="font-black text-amber-400 uppercase text-[10px] tracking-[0.6em] mb-12 text-slate-400">Navigasi</h5>
                <div class="flex flex-col gap-6 text-xs font-black uppercase tracking-widest text-white text-center lg:text-left">
                    <button onclick="scrollToId('kursus')" class="text-center lg:text-left hover:text-amber-400 transition-colors">Katalog Program</button>
                    <button onclick="scrollToId('muat-turun')" class="text-center lg:text-left hover:text-amber-400 transition-colors text-[10px]">Pusat Borang</button>
                    <a href="https://forms.gle/oz5bwhKqC8yEid226" target="_blank" class="hover:text-amber-400 transition-colors">Portal Muat Naik</a>
                </div>
            </div>

            <div>
                <h5 class="font-black text-amber-400 uppercase text-[10px] tracking-[0.6em] mb-12 text-slate-400">Lokasi Kampus</h5>
                <p class="text-sm text-slate-400 leading-relaxed font-bold text-center lg:text-left">Peti Surat No. 1, 89607 Papar, Sabah.</p>
                <a href="https://maps.app.goo.gl/UbdhERujykyLpUrJ7" target="_blank" class="inline-flex items-center gap-3 text-amber-400 font-black uppercase text-[10px] tracking-widest hover:underline decoration-amber-400/40 underline-offset-8 mt-6">Akses Peta <i data-lucide="map-pin" class="w-4 h-4"></i></a>
            </div>
        </div>
        <div class="max-w-7xl mx-auto px-4 mt-32 pt-12 border-t border-white/5 text-center text-slate-600 text-[9px] uppercase font-black tracking-[0.7em]">
            &copy; 2026 Jabatan Elektrik IKBN Kinarut. 
        </div>
    </footer>

    <!-- Scripts -->
    <script type="module">
        // --- DATA NASIHAT LENGKAP ---
        const adviceData = {
            'SPM': `Berikut adalah syarat lengkap bagi Lepasan SPM atau Tamat Tingkatan 5:
            1. Pilihan Pertama (PW2 - Pendawai Fasa Tunggal): 
               - Warganegara Malaysia.
               - Berumur minima 18 tahun.
               - Tamat Tingkatan 5 / SPM.
               - Mempunyai pengalaman kerja elektrik minima 2 tahun dengan syarikat/kontraktor yang berdaftar dengan ECoS.
               - Memiliki Buku Log ECoS yang lengkap mencatatkan pengalaman kerja.

            2. Pilihan Kedua (A0 - Penjaga Jentera Asas):
               - Warganegara Malaysia.
               - Berumur minima 20 tahun.
               - Tamat Tingkatan 5 / SPM.
               - Mempunyai pengalaman kerja minima 3 tahun di sistem elektrik yang sedang beroperasi (Live).
               - Wajib bekerja di bawah majikan berdaftar ECoS dan memiliki Buku Log rasmi.`,

            'PW2': `Bagi pemegang Sijil PW2, berikut adalah syarat untuk peningkatan tahap kompetensi:
            1. Ke PW4 (Three Phase):
               - Memegang perakuan PW1 atau PW2 sekurang-kurangnya selama 1 tahun.
               - Pengalaman kerja elektrik sistem Tiga Fasa minima 1 tahun dengan kontraktor ECoS Kelas C ke atas.
               - Melengkapkan Buku Log bagi sistem 3 fasa.

            2. Ke A0 (Penjaga Jentera):
               - Berumur minima 20 tahun.
               - Mempunyai pengalaman elektrik minima 2 tahun selepas memiliki PW2.`,

            'A0': `Sebagai pemegang perakuan A0, anda layak memohon peningkatan ke kategori A1 atau A4:
            1. Syarat Ke A1 (Talian Atas):
               - Mempunyai perakuan A0 sekurang-kurangnya 1 tahun.
               - Pengalaman kerja tambahan dalam sistem talian atas voltan rendah minima 1 tahun.

            2. Syarat Ke A4 (Janakuasa VR):
               - Perlu melengkapkan pengalaman kerja sistem Janakuasa selama 1 tahun DAN sistem Talian Atas selama 1 tahun.
               - Jika tiada pengalaman genset, anda disyorkan mengambil Modul JKVR di IKBN Kinarut.`,

            'A1': `Syarat peningkatan kompetensi bagi pemegang A1:
            1. Syarat Ke A4:
               - Memiliki perakuan A1 sekurang-kurangnya 1 tahun.
               - Mempunyai pengalaman kerja mengendalikan Janakuasa minima 1 tahun atau melengkapkan Modul JKVR di IKBN Kinarut.
               - Selepas memegang A4 selama 2 tahun, anda layak memohon kategori Voltan Tinggi B0.`,

            'A4': `Laluan ke Voltan Tinggi (B0) bagi pemegang A4:
            1. Syarat B0 Penuh (11kV):
               - Memiliki perakuan A4 sekurang-kurangnya selama 2 tahun.
               - Mempunyai pengalaman kerja praktikal dalam sistem Voltan Tinggi (HV) 11kV selama 2 tahun yang disahkan majikan.

            2. Syarat B0 Terhad (Pencawang Sahaja):
               - Jika tiada pengalaman HV, anda wajib melengkapkan Modul MKP (Kendalian Pencawang 11kV) selama 80 jam di IKBN Kinarut.`,

            'NON_COMPETENT': `Jika anda tiada sijil kompetensi:
            1. Majikan: Mula bekerja dengan syarikat berdaftar ECoS.
            2. Buku Log: Dapatkan Buku Log ECoS dan catat tugasan harian anda setiap minggu.
            3. Pendaftaran: Setelah cukup pengalaman, mohon kursus PW2 atau A0 di sini.`,

            'NO_COMPANY': `PENTING: Syarat wajib ECoS untuk peperiksaan ialah calon MESTI bekerja di bawah majikan berdaftar ECoS. Tanpa syarikat berdaftar, buku log anda tidak akan diiktiraf.`,

            'NO_EXPERIENCE': `Jika kurang pengalaman:
            1. Kumpul Jam: Bekerja di bawah penyeliaan orang kompeten.
            2. Buku Log: Catat tugasan setiap minggu dan dapatkan pengesahan penyelia kompeten.`
        };

        window.scrollToId = (id) => {
            const element = document.getElementById(id);
            if (element) {
                const headerOffset = 100;
                const elementPosition = element.getBoundingClientRect().top;
                const offsetPosition = elementPosition + window.pageYOffset - headerOffset;
                window.scrollTo({ top: offsetPosition, behavior: "smooth" });
            }
        };

        window.toggleMenu = () => {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        };

        // --- SPEECH LOGIC (NATIVE - ms-MY Preferred) ---
        let lastText = "";

        window.openAssistant = () => {
            document.getElementById('assistant-modal').classList.remove('hidden');
            document.body.style.overflow = 'hidden';
        };

        window.closeAssistant = () => {
            stopSpeech();
            document.getElementById('assistant-modal').classList.add('hidden');
            document.body.style.overflow = '';
            resetAssistant();
        };

        window.resetAssistant = () => {
            stopSpeech();
            document.getElementById('assistant-steps').classList.remove('hidden');
            document.getElementById('assistant-result').classList.add('hidden');
            document.getElementById('voice-indicator').classList.add('hidden');
        };

        window.analyzePathway = (status) => {
            const steps = document.getElementById('assistant-steps');
            const result = document.getElementById('assistant-result');
            const resultText = document.getElementById('result-text');

            steps.classList.add('hidden');
            result.classList.remove('hidden');

            const text = adviceData[status] || "Sila hubungi urusetia.";
            lastText = text;
            resultText.innerText = text;

            generateSpeech(text);
        };

        window.stopSpeech = () => {
            window.speechSynthesis.cancel();
            document.getElementById('voice-indicator').classList.add('hidden');
            document.getElementById('stop-speech-btn').classList.add('hidden');
        };

        window.repeatSpeech = () => {
            if (lastText) generateSpeech(lastText);
        };

        function generateSpeech(text) {
            stopSpeech();
            const indicator = document.getElementById('voice-indicator');
            const stopBtn = document.getElementById('stop-speech-btn');

            const utter = new SpeechSynthesisUtterance(text);
            const voices = window.speechSynthesis.getVoices();
            
            // Strictly prefer Malaysian voice (ms-MY) and look for keywords indicating female
            const msVoice = voices.find(v => (v.lang === 'ms-MY' || v.lang.includes('ms')) && 
                (v.name.toLowerCase().includes('female') || v.name.toLowerCase().includes('google') || v.name.toLowerCase().includes('siri')));
            
            // Fallback to any Malay voice if female specific not found
            const fallbackVoice = msVoice || voices.find(v => v.lang === 'ms-MY' || v.lang.includes('ms'));
            
            if (fallbackVoice) {
                utter.voice = fallbackVoice;
            }

            utter.pitch = 1.2; // Slightly higher pitch for female sound
            utter.rate = 0.9;  // Slightly slower for technical clarity
            utter.lang = 'ms-MY';

            utter.onstart = () => {
                indicator.classList.remove('hidden');
                stopBtn.classList.remove('hidden');
            };
            utter.onend = () => {
                indicator.classList.add('hidden');
                stopBtn.classList.add('hidden');
            };

            window.speechSynthesis.speak(utter);
        }

        // Initialize
        window.speechSynthesis.getVoices();
        lucide.createIcons();

        // Background Animation
        const canvas = document.getElementById('hero-bg');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = 700;
        function draw() {
            ctx.clearRect(0,0,canvas.width, canvas.height);
            ctx.fillStyle = "rgba(251, 191, 36, 0.08)";
            for(let i=0; i<35; i++) {
                ctx.beginPath(); ctx.arc(Math.random()*canvas.width, Math.random()*canvas.height, 1, 0, Math.PI*2); ctx.fill();
            }
            requestAnimationFrame(draw);
        }
        draw();
    </script>
</body>
</html>
