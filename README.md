<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Acceuil serveur CT241</title>
    <!-- Tailwind CSS pour le stylage rapide -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons pour les icônes -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 0.7s ease-out forwards;
        }
    </style>
</head>
<body class="bg-slate-50 font-sans text-slate-900 overflow-x-hidden">

    <!-- Écran de chargement (Splash Screen) -->
    <div id="loader" class="fixed inset-0 bg-slate-900 z-[100] flex flex-col items-center justify-center p-6 transition-opacity duration-500">
        <div class="w-full max-w-md text-center">
            <div class="bg-indigo-600 w-16 h-16 rounded-2xl flex items-center justify-center text-white mx-auto mb-8 animate-pulse shadow-lg shadow-indigo-500/20">
                <i data-lucide="layout-dashboard" class="w-8 h-8"></i>
            </div>
            <h2 class="text-white text-xl font-bold mb-2">Système de Gestion</h2>
            <p id="loading-message" class="text-slate-400 mb-8 text-sm italic">Démarrage du système...</p>
            
            <div class="w-full bg-slate-800 rounded-full h-2 mb-4 overflow-hidden">
                <div id="progress-bar" class="bg-indigo-500 h-full w-0 transition-all duration-300 ease-out"></div>
            </div>
            <p id="progress-text" class="text-slate-500 text-xs font-mono">0%</p>
        </div>
    </div>

    <!-- Modal Tuto / Bienvenue -->
    <div id="tuto-modal" class="fixed inset-0 z-50 hidden items-center justify-center p-4 bg-black/60 backdrop-blur-sm transition-all">
        <div class="bg-white rounded-3xl max-w-lg w-full shadow-2xl overflow-hidden scale-95 transition-transform duration-300">
            <div class="p-8">
                <div class="flex justify-between items-start mb-6">
                    <div>
                        <h3 class="text-2xl font-bold text-slate-800">Bienvenue, Utilisateur</h3>
                        <p class="text-slate-500 text-sm">Guide rapide d'utilisation du portail</p>
                    </div>
                    <button onclick="closeTuto()" class="p-2 hover:bg-slate-100 rounded-full transition-colors">
                        <i data-lucide="x" class="w-5 h-5 text-slate-500"></i>
                    </button>
                </div>

                <div class="space-y-6 mb-8 text-left">
                    <div class="flex gap-4">
                        <div class="bg-blue-100 p-3 rounded-xl text-blue-600 h-fit">
                            <i data-lucide="monitor" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-800">Interface Centralisée</h4>
                            <p class="text-sm text-slate-600">Accédez à tous vos services depuis un seul écran sans changer d'URL.</p>
                        </div>
                    </div>
                    <div class="flex gap-4">
                        <div class="bg-emerald-100 p-3 rounded-xl text-emerald-600 h-fit">
                            <i data-lucide="mouse-pointer-click" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-800">Accès Direct</h4>
                            <p class="text-sm text-slate-600">Cliquez sur une carte pour être redirigé vers le module spécifique.</p>
                        </div>
                    </div>
                    <div class="flex gap-4">
                        <div class="bg-amber-100 p-3 rounded-xl text-amber-600 h-fit">
                            <i data-lucide="info" class="w-5 h-5"></i>
                        </div>
                        <div>
                            <h4 class="font-semibold text-slate-800">Suivi en Temps Réel</h4>
                            <p class="text-sm text-slate-600">Les données sont synchronisées avec le Serveur CT241 V.1.</p>
                        </div>
                    </div>
                </div>

                <button onclick="closeTuto()" class="w-full bg-indigo-600 text-white py-4 rounded-xl font-bold hover:bg-indigo-700 transition-colors shadow-lg shadow-indigo-200">
                    Compris, c'est parti !
                </button>
            </div>
        </div>
    </div>

    <!-- Contenu Principal -->
    <div id="main-content" class="invisible">
        <header class="bg-white border-b border-slate-200 py-6 px-4 mb-8 shadow-sm">
            <div class="max-w-6xl mx-auto flex items-center justify-between">
                <div class="flex items-center gap-3">
                    <div class="bg-indigo-600 p-2 rounded-lg text-white">
                        <i data-lucide="SELECTIONNEZ VOTRE OPTION" class="w-6 h-6"></i>
                    </div>
                    <h1 class="text-2xl font-bold tracking-tight text-slate-800">Système de Gestion Intégré</h1>
                </div>
                <button onclick="openTuto()" class="flex items-center gap-2 text-sm font-medium text-slate-500 hover:text-indigo-600 transition-colors bg-slate-100 px-4 py-2 rounded-lg">
                    <i data-lucide="info" class="w-4 h-4"></i> Aide
                </button>
            </div>
        </header>

        <main class="max-w-6xl mx-auto px-4 pb-12 animate-fade-in">
            <div class="mb-10 text-center md:text-left">
                <h2 class="text-xl font-semibold text-slate-700 mb-2">Tableau de bord principal</h2>
                <p class="text-slate-500">Sélectionnez le module opérationnel nécessaire.</p>
            </div>

            <!-- Grille des applications -->
            <div id="apps-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <!-- Les cartes seront injectées ici par JavaScript -->
            </div>

            <div class="mt-16 pt-8 border-t border-slate-200 text-center">
                <p class="text-xs text-slate-400 uppercase tracking-widest font-medium">
                    Interface de Navigation Unifiée • Session Active
                </p>
            </div>
        </main>
    </div>

    <script>
        // Configuration des données
        const apps = [
            {
                title: "Portail des Commandes",
                description: "Gérer et visualiser l'ensemble des commandes clients en temps réel.",
                url: "https://newsmiley21-star.github.io/commandes.html",
                icon: "shopping-cart",
                color: "bg-blue-600",
                shadow: "shadow-blue-500/10"
            },
            {
                title: "Service Livraison",
                description: "Suivi logistique, planification des trajets et états de livraison.",
                url: "https://newsmiley21-star.github.io/livraison.index.html",
                icon: "truck",
                color: "bg-emerald-600",
                shadow: "shadow-emerald-500/10"
            },
            {
                title: "Espace Personnel",
                description: "Accès réservé au personnel : suivi des gains et performances.",
                url: "https://newsmiley21-star.github.io/index.html#suivi-des-gains",
                icon: "trending-up",
                color: "bg-amber-600",
                shadow: "shadow-amber-500/10"
            }
        ];

        const loadingMessages = [
            "Connexion aux serveurs...",
            "Sécurisation de la liaison...",
            "Chargement des modules de gestion...",
            "Finalisation de l'interface..."
        ];

        // Initialisation de la grille
        function initGrid() {
            const grid = document.getElementById('apps-grid');
            grid.innerHTML = apps.map(app => `
                <a href="${app.url}" class="group block bg-white border border-slate-200 rounded-3xl p-6 shadow-sm transition-all duration-500 hover:shadow-2xl hover:border-transparent hover:-translate-y-2">
                    <div class="flex flex-col h-full">
                        <div class="${app.color} w-14 h-14 rounded-2xl flex items-center justify-center text-white mb-6 shadow-lg ${app.shadow} transition-transform group-hover:scale-110 group-hover:rotate-3">
                            <i data-lucide="${app.icon}" class="w-8 h-8"></i>
                        </div>
                        <h3 class="text-xl font-bold mb-3 text-slate-800 group-hover:text-indigo-600 transition-colors">
                            ${app.title}
                        </h3>
                        <p class="text-slate-500 text-sm leading-relaxed mb-8">
                            ${app.description}
                        </p>
                        <div class="mt-auto flex items-center text-sm font-bold text-indigo-600 gap-2 opacity-0 group-hover:opacity-100 translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300">
                            Lancer l'application <i data-lucide="arrow-right" class="w-4 h-4"></i>
                        </div>
                    </div>
                </a>
            `).join('');
            
            // Rafraîchir les icônes Lucide après injection HTML
            lucide.createIcons();
        }

        // Gestion du chargement
        function startLoading() {
            const progressBar = document.getElementById('progress-bar');
            const progressText = document.getElementById('progress-text');
            const messageEl = document.getElementById('loading-message');
            
            let progress = 0;
            const interval = setInterval(() => {
                progress += Math.random() * 15;
                if (progress >= 100) {
                    progress = 100;
                    clearInterval(interval);
                    finishLoading();
                }
                progressBar.style.width = progress + '%';
                progressText.innerText = Math.round(progress) + '%';
                
                const msgIndex = Math.floor((progress / 100) * loadingMessages.length);
                messageEl.innerText = loadingMessages[Math.min(msgIndex, loadingMessages.length - 1)];
            }, 300);
        }

        function finishLoading() {
            const loader = document.getElementById('loader');
            const mainContent = document.getElementById('main-content');
            
            loader.style.opacity = '0';
            setTimeout(() => {
                loader.style.display = 'none';
                mainContent.classList.remove('invisible');
                openTuto();
            }, 500);
        }

        // Fonctions du Modal
        function openTuto() {
            const modal = document.getElementById('tuto-modal');
            modal.classList.remove('hidden');
            modal.classList.add('flex');
            setTimeout(() => {
                modal.querySelector('div').classList.remove('scale-95');
                modal.querySelector('div').classList.add('scale-100');
            }, 10);
        }

        function closeTuto() {
            const modal = document.getElementById('tuto-modal');
            modal.querySelector('div').classList.replace('scale-100', 'scale-95');
            setTimeout(() => {
                modal.classList.replace('flex', 'hidden');
            }, 300);
        }

        // Démarrage au chargement de la page
        window.onload = () => {
            initGrid();
            startLoading();
        };
    </script>
</body>
</html>
