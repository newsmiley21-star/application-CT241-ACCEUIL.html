<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>CT241 - Gestion Logistique</title>
    
    <!-- Meta tags pour PWA (Installation mobile) -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="CT241">
    <meta name="theme-color" content="#057847">
    
    <!-- Favicon utilisant le logo hébergé -->
    <link rel="icon" type="image/png" href="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png">
    <link rel="apple-touch-icon" href="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png">

    <!-- Lien Manifeste PWA -->
    <link rel="manifest" href='data:application/manifest+json,{"name":"CT241 Livraison Express","short_name":"CT241","start_url":".","display":"standalone","background_color":"#ffffff","theme_color":"#057847","icons":[{"src":"https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png","sizes":"512x512","type":"image/png"}]}'>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        ct241: {
                            green: '#057847', // Vert du texte CT241
                            blue: '#1e40af',  // Bleu de l'aile
                            gold: '#fbbf24'   // Jaune/Or de la flèche
                        }
                    }
                }
            }
        }
    </script>

    <style>
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 0.7s ease-out forwards;
        }
        body {
            -webkit-tap-highlight-color: transparent;
            user-select: none;
        }
        .logo-shadow {
            filter: drop-shadow(0 10px 15px rgba(5, 120, 71, 0.2));
        }
    </style>
</head>
<body class="bg-slate-50 font-sans text-slate-900 overflow-x-hidden">

    <!-- Écran de chargement (Splash Screen) -->
    <div id="loader" class="fixed inset-0 bg-white z-[100] flex flex-col items-center justify-center p-6 transition-opacity duration-500">
        <div class="w-full max-w-md text-center">
            <div class="mb-8 animate-bounce">
                <img src="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png" alt="Logo CT241" class="w-32 h-32 object-contain mx-auto rounded-2xl logo-shadow">
            </div>
            <h2 class="text-ct241-green text-2xl font-black mb-1 tracking-tighter">CT241</h2>
            <p id="loading-message" class="text-slate-500 mb-8 text-sm font-medium tracking-wide uppercase">Initialisation du portail logistique...</p>
            
            <div class="w-full bg-slate-100 rounded-full h-1.5 mb-4 overflow-hidden max-w-[250px] mx-auto">
                <div id="progress-bar" class="bg-ct241-green h-full w-0 transition-all duration-300 ease-out"></div>
            </div>
            <p id="progress-text" class="text-slate-400 text-xs font-mono">0%</p>
        </div>
    </div>

    <!-- Bannière d'installation -->
    <div id="install-banner" class="fixed bottom-6 left-6 right-6 bg-ct241-green text-white p-4 rounded-2xl shadow-2xl z-[60] flex items-center justify-between hidden animate-fade-in">
        <div class="flex items-center gap-3">
            <div class="bg-white p-1 rounded-lg">
                <img src="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png" class="w-8 h-8 object-contain">
            </div>
            <div>
                <p class="font-bold text-sm text-white">Installer CT241</p>
                <p class="text-xs text-green-100 font-medium">Accès direct sur votre écran.</p>
            </div>
        </div>
        <button id="btn-install" class="bg-white text-ct241-green px-4 py-2 rounded-xl text-sm font-bold shadow-sm active:scale-95 transition-transform">Installer</button>
    </div>

    <!-- Modal Tuto / Bienvenue -->
    <div id="tuto-modal" class="fixed inset-0 z-50 hidden items-center justify-center p-4 bg-slate-900/40 backdrop-blur-md transition-all">
        <div class="bg-white rounded-[2.5rem] max-w-lg w-full shadow-2xl overflow-hidden scale-95 transition-transform duration-300 border border-slate-100">
            <div class="p-8">
                <div class="text-center mb-8">
                    <img src="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png" class="w-20 h-20 object-contain mx-auto mb-4 rounded-xl">
                    <h3 class="text-2xl font-black text-slate-800 tracking-tight">Bienvenue chez CT241</h3>
                    <p class="text-slate-500 text-sm font-medium">Livraison Express et Logistique</p>
                </div>

                <div class="space-y-4 mb-8 text-left">
                    <div class="flex gap-4 p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <div class="bg-white p-2.5 rounded-xl shadow-sm text-ct241-green h-fit">
                            <i data-lucide="package-check" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-slate-800 text-sm">Gestion Unifiée</h4>
                            <p class="text-xs text-slate-500 leading-relaxed">Centralisez vos commandes et livraisons sur un seul terminal mobile.</p>
                        </div>
                    </div>
                    <div class="flex gap-4 p-4 bg-slate-50 rounded-2xl border border-slate-100">
                        <div class="bg-white p-2.5 rounded-xl shadow-sm text-ct241-blue h-fit">
                            <i data-lucide="zap" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h4 class="font-bold text-slate-800 text-sm">Vitesse & Précision</h4>
                            <p class="text-xs text-slate-500 leading-relaxed">Interface fluide conçue pour les opérations sur le terrain.</p>
                        </div>
                    </div>
                </div>

                <button onclick="closeTuto()" class="w-full bg-ct241-green text-white py-4 rounded-2xl font-bold hover:bg-opacity-90 active:scale-95 transition-all shadow-lg shadow-green-900/10">
                    Accéder au Dashboard
                </button>
            </div>
        </div>
    </div>

    <!-- Contenu Principal -->
    <div id="main-content" class="invisible">
        <header class="bg-white border-b border-slate-100 py-4 px-6 mb-8 shadow-sm sticky top-0 z-40">
            <div class="max-w-6xl mx-auto flex items-center justify-between">
                <div class="flex items-center gap-4">
                    <img src="https://i.ibb.co/xKY76DgR/Gemini-Generated-Image-1pvtp31pvtp31pvt-1.png" alt="Logo" class="w-10 h-10 object-contain rounded-lg">
                    <div>
                        <h1 class="text-lg font-black tracking-tighter text-ct241-green leading-none">CT241</h1>
                        <span class="text-[10px] text-slate-400 font-bold uppercase tracking-widest">Express Hub</span>
                    </div>
                </div>
                <button onclick="openTuto()" class="bg-slate-50 p-2.5 rounded-xl text-slate-400 hover:text-ct241-green transition-colors border border-slate-100">
                    <i data-lucide="help-circle" class="w-5 h-5"></i>
                </button>
            </div>
        </header>

        <main class="max-w-6xl mx-auto px-6 pb-24 animate-fade-in">
            <div class="mb-10">
                <h2 class="text-2xl font-black text-slate-800 tracking-tight">Tableau de Bord</h2>
                <p class="text-slate-400 text-sm font-medium">Sélectionnez votre zone d'opération.</p>
            </div>

            <div id="apps-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5">
                <!-- Cartes injectées ici -->
            </div>
        </main>

        <!-- Nav basse style App -->
        <nav class="fixed bottom-0 left-0 right-0 bg-white border-t border-slate-100 px-8 py-4 flex justify-around items-center z-40 md:hidden">
            <div class="text-ct241-green flex flex-col items-center gap-1">
                <i data-lucide="layout-grid" class="w-6 h-6"></i>
                <span class="text-[10px] font-bold">Menu</span>
            </div>
            <div class="text-slate-300 flex flex-col items-center gap-1">
                <i data-lucide="history" class="w-6 h-6"></i>
                <span class="text-[10px] font-bold">Archives</span>
            </div>
            <div class="text-slate-300 flex flex-col items-center gap-1" onclick="openTuto()">
                <i data-lucide="user-cog" class="w-6 h-6"></i>
                <span class="text-[10px] font-bold">Profil</span>
            </div>
        </nav>
    </div>

    <script>
        // PWA registration
        if ('serviceWorker' in navigator) {
            const swCode = `self.addEventListener('fetch', (e) => e.respondWith(fetch(e.request)));`;
            const blob = new Blob([swCode], { type: 'text/javascript' });
            navigator.serviceWorker.register(URL.createObjectURL(blob));
        }

        const apps = [
            {
                title: "Commandes",
                url: "https://newsmiley21-star.github.io/commandes.html",
                icon: "shopping-bag",
                color: "text-ct241-blue",
                bg: "bg-blue-50",
                desc: "Gestion des commandes flux CT241."
            },
            {
                title: "Livraison",
                url: "https://newsmiley21-star.github.io/livraison.index.html",
                icon: "truck",
                color: "text-ct241-green",
                bg: "bg-emerald-50",
                desc: "Suivi logistique et expéditions."
            },
            {
                title: "Personnel",
                url: "https://newsmiley21-star.github.io/index.html#suivi-des-gains",
                icon: "bar-chart-3",
                color: "text-ct241-gold",
                bg: "bg-amber-50",
                desc: "Calcul des gains et performances."
            }
        ];

        let deferredPrompt;
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            deferredPrompt = e;
            document.getElementById('install-banner').classList.remove('hidden');
        });

        document.getElementById('btn-install').addEventListener('click', async () => {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                const { outcome } = await deferredPrompt.userChoice;
                if (outcome === 'accepted') document.getElementById('install-banner').classList.add('hidden');
                deferredPrompt = null;
            }
        });

        function initGrid() {
            const grid = document.getElementById('apps-grid');
            grid.innerHTML = apps.map(app => `
                <a href="${app.url}" class="group block bg-white border border-slate-100 rounded-[2rem] p-6 shadow-sm transition-all duration-300 hover:shadow-xl hover:border-ct241-green/20 hover:-translate-y-1">
                    <div class="flex items-center gap-5">
                        <div class="${app.bg} ${app.color} w-16 h-16 rounded-[1.25rem] flex items-center justify-center shadow-inner">
                            <i data-lucide="${app.icon}" class="w-8 h-8"></i>
                        </div>
                        <div class="flex-1">
                            <h3 class="font-black text-slate-800 text-lg leading-tight">${app.title}</h3>
                            <p class="text-xs text-slate-400 font-medium mt-1">${app.desc}</p>
                        </div>
                        <div class="bg-slate-50 p-2 rounded-full text-slate-300 group-hover:text-ct241-green group-hover:bg-green-50 transition-all">
                            <i data-lucide="arrow-up-right" class="w-5 h-5"></i>
                        </div>
                    </div>
                </a>
            `).join('');
            lucide.createIcons();
        }

        function startLoading() {
            const bar = document.getElementById('progress-bar');
            const text = document.getElementById('progress-text');
            const msg = document.getElementById('loading-message');
            const messages = ["Sécurisation du tunnel...", "Chargement de la logistique...", "Optimisation CT241...", "Prêt."];
            let p = 0;
            const int = setInterval(() => {
                p += Math.random() * 25;
                if (p >= 100) {
                    p = 100;
                    clearInterval(int);
                    setTimeout(finishLoading, 400);
                }
                bar.style.width = p + '%';
                text.innerText = Math.round(p) + '%';
                msg.innerText = messages[Math.floor((p/101) * messages.length)];
            }, 180);
        }

        function finishLoading() {
            document.getElementById('loader').style.opacity = '0';
            setTimeout(() => {
                document.getElementById('loader').style.display = 'none';
                document.getElementById('main-content').classList.remove('invisible');
                if(!localStorage.getItem('ct241_tuto_done')) {
                    openTuto();
                    localStorage.setItem('ct241_tuto_done', 'true');
                }
            }, 500);
        }

        function openTuto() {
            const m = document.getElementById('tuto-modal');
            m.classList.replace('hidden', 'flex');
            setTimeout(() => m.querySelector('div').classList.replace('scale-95', 'scale-100'), 10);
        }

        function closeTuto() {
            const m = document.getElementById('tuto-modal');
            m.querySelector('div').classList.replace('scale-100', 'scale-95');
            setTimeout(() => m.classList.replace('flex', 'hidden'), 200);
        }

        window.onload = () => {
            initGrid();
            startLoading();
        };
    </script>
</body>
</html>
