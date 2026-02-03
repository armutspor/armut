
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ARMUT SPOR | Resmi Web Sitesi</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Inter:wght@300;500;800&display=swap');
        
        body { background: #0a0a0a; color: white; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .cyber-border { border: 1px solid #39FF14; box-shadow: 0 0 15px rgba(57, 255, 20, 0.2); }
        .neon-text { color: #39FF14; text-shadow: 0 0 10px rgba(57, 255, 20, 0.5); font-family: 'Orbitron', sans-serif; }
        .glass-card { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.1); transition: 0.3s; }
        .glass-card:hover { transform: translateY(-5px); border-color: #39FF14; }
        .install-btn { background: linear-gradient(90deg, #39FF14, #00ff87); color: black; font-weight: 800; }
    </style>
</head>
<body class="p-4 md:p-8">

    <header class="flex justify-between items-center mb-10 border-b border-gray-800 pb-6">
        <div class="flex items-center gap-4">
            <div class="w-16 h-16 bg-green-500 rounded-full flex items-center justify-center cyber-border">
                <i class="fas fa-volleyball-ball text-3xl text-black"></i>
            </div>
            <div>
                <h1 class="text-3xl md:text-5xl neon-text font-bold">ARMUT SPOR</h1>
                <p class="text-gray-400 text-xs tracking-[0.3em]">PROFESSIONAL CLUB ECOSYSTEM</p>
            </div>
        </div>
        
        <div class="text-right">
            <div id="clock" class="text-2xl font-mono text-green-400">14:40:55</div>
            <div id="date" class="text-gray-500 text-sm">3 ŞUBAT 2026</div>
            <button id="installApp" class="install-btn px-4 py-1 mt-2 rounded text-xs uppercase tracking-tighter">Uygulamayı Yükle</button>
        </div>
    </header>

    <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        <aside class="lg:col-span-3 space-y-6">
            <h3 class="neon-text mb-4"><i class="fas fa-globe-europe mr-2"></i>DÜNYA LİGLERİ</h3>
            <div class="glass-card p-4 rounded-xl">
                <iframe src="https://www.scoreaxis.com/widget/league-top-scorers/8?autoHeight=1&theme=dark&font=Inter" width="100%" height="400" style="border: none;"></iframe>
            </div>
        </aside>

        <main class="lg:col-span-6">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-2xl font-bold italic">FLAŞ TRANSFERLER <span class="text-green-500">2026</span></h2>
                <span class="bg-red-600 px-3 py-1 rounded-full text-xs animate-pulse">CANLI</span>
            </div>
            
            <div class="grid grid-cols-2 gap-4" id="transferGrid">
                </div>
        </main>

        <aside class="lg:col-span-3">
            <div class="mb-6">
                <input type="text" id="playerSearch" placeholder="Futbolcu Ara..." class="w-full bg-transparent border-b-2 border-gray-700 focus:border-green-500 outline-none py-2 px-4 transition-all">
            </div>
            
            <h3 class="neon-text mb-4 text-center italic uppercase">Kariyer Yolculuğu</h3>
            <div class="space-y-3" id="playerList">
                </div>
        </aside>
    </div>

    <div id="infoModal" class="fixed inset-0 bg-black/90 hidden flex items-center justify-center p-4 z-50">
        <div class="bg-gray-900 border-2 border-green-500 p-8 rounded-2xl max-w-md w-full relative">
            <button onclick="closeModal()" class="absolute top-4 right-4 text-2xl">&times;</button>
            <div id="modalContent"></div>
        </div>
    </div>

    <script>
        // VERİ SETİ (2026 GÜNCEL)
        const players = [
            { name: "EMİR ÖZKAYA", team: "ARMUT SPOR ELITE", role: "Manager", bio: "Kulüp Başkanı ve Baş Stratejist. 2026 Vizyonunun mimarı." },
            { name: "İLBER İBRAHİM ÖZKAYA", team: "ARMUT SPOR ELITE", role: "Star Player", bio: "Takımın 10 numarası. Teknik kapasitesiyle dünya devlerinin takibinde." },
            { name: "VICTOR OSIMHEN", team: "Galatasaray", price: "€75M", info: "2026 Sezonu Gol Kralı adayı." },
            { name: "ARDA GÜLER", team: "Real Madrid", price: "€120M", info: "Dünya futbolunun yeni altın çocuğu." },
            { name: "LAMINE YAMAL", team: "Barcelona", price: "€180M", info: "Durdurulamaz sağ kanat fırtınası." }
        ];

        // TRANSFERLERİ YÜKLE
        function loadTransfers() {
            const grid = document.getElementById('transferGrid');
            const news = [
                {p: "Kylian Mbappé", from: "Real Madrid", to: "Man City", img: "https://xsgames.co/randomusers/assets/avatars/male/1.jpg"},
                {p: "Erling Haaland", from: "Man City", to: "Real Madrid", img: "https://xsgames.co/randomusers/assets/avatars/male/2.jpg"},
                {p: "Florian Wirtz", from: "Leverkusen", to: "Bayern", img: "https://xsgames.co/randomusers/assets/avatars/male/3.jpg"},
                {p: "Kenan Yıldız", from: "Juventus", to: "Arsenal", img: "https://xsgames.co/randomusers/assets/avatars/male/4.jpg"}
            ];
            
            grid.innerHTML = news.map(n => `
                <div class="glass-card p-4 rounded-xl text-center border-l-4 border-green-500 cursor-pointer" onclick="showPlayerInfo('${n.p}', 'Transfer Haberleri: ${n.from} -> ${n.to}')">
                    <img src="${n.img}" class="w-20 h-20 rounded-full mx-auto mb-3 border-2 border-gray-700">
                    <h4 class="font-bold text-sm text-green-400">${n.p}</h4>
                    <p class="text-[10px] text-gray-500 uppercase">${n.from} ➔ ${n.to}</p>
                </div>
            `).join('');
        }

        // OYUNCU LİSTESİNİ YÜKLE
        function loadPlayers(filter = "") {
            const list = document.getElementById('playerList');
            const filtered = players.filter(p => p.name.toLowerCase().includes(filter.toLowerCase()));
            
            list.innerHTML = filtered.map(p => `
                <div onclick="showPlayerInfo('${p.name}', '${p.bio || p.info}')" class="flex items-center justify-between p-3 glass-card rounded-lg cursor-pointer hover:bg-green-500/10">
                    <span class="text-xs font-bold tracking-widest">${p.name}</span>
                    <span class="text-[9px] bg-green-900 px-2 py-0.5 rounded text-green-300 uppercase">${p.role || p.team}</span>
                </div>
            `).join('');
        }

        // MODAL FONKSİYONU
        function showPlayerInfo(name, info) {
            document.getElementById('modalContent').innerHTML = `<h2 class="text-2xl font-bold text-green-400 mb-4">${name}</h2><p class="text-gray-300 leading-relaxed">${info}</p>`;
            document.getElementById('infoModal').classList.remove('hidden');
        }

        function closeModal() { document.getElementById('infoModal').classList.add('hidden'); }

        // ARAMA MOTORU
        document.getElementById('playerSearch').addEventListener('input', (e) => loadPlayers(e.target.value));

        // CANLI SAAT
        setInterval(() => {
            const now = new Date();
            document.getElementById('clock').innerText = now.toLocaleTimeString('tr-TR');
        }, 1000);

        // UYGULAMA YÜKLEME SİMÜLASYONU
        document.getElementById('installApp').onclick = () => alert("Armut Spor Uygulaması Cihazınıza Yükleniyor...");

        // BAŞLAT
        loadTransfers();
        loadPlayers();
    </script>
</body>
</html>

