<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Dashboard Developer | CodeIgniter 4</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="shortcut icon" type="image/x-icon" href="/favicon.ico">
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#fff5f2',
                            500: '#dd4814', // CodeIgniter Flame Orange
                            600: '#c53b0b',
                            900: '#7a1f02',
                        },
                        darkbg: '#0B0F17',
                        darkcard: '#111827',
                        darkborder: '#1F2937'
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        mono: ['JetBrains Mono', 'ui-monospace', 'monospace']
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts & Lucide Icons -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0B0F17;
            color: #F3F4F6;
        }
        .glow-orange {
            box-shadow: 0 0 20px -5px rgba(221, 72, 20, 0.3);
        }
        .glass-panel {
            background: rgba(17, 24, 39, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        /* Custom scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0B0F17;
        }
        ::-webkit-scrollbar-thumb {
            background: #1F2937;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #374151;
        }
    </style>
</head>
<body class="antialiased selection:bg-brand-500 selection:text-white">

    <div class="flex h-screen overflow-hidden">

        <!-- MOBILE BACKDROP -->
        <div id="sidebarBackdrop" onclick="toggleSidebar()" class="fixed inset-0 z-40 bg-black/60 backdrop-blur-sm hidden lg:hidden transition-opacity"></div>

        <!-- SIDEBAR -->
        <aside id="sidebar" class="fixed lg:static inset-y-0 left-0 z-50 w-64 bg-slate-900 border-r border-slate-800 flex flex-col justify-between transform -translate-x-full lg:translate-x-0 transition-transform duration-300 ease-in-out shrink-0">
            <div>
                <!-- BRAND HEADER -->
                <div class="h-16 flex items-center justify-between px-6 border-b border-slate-800/80">
                    <a href="#" class="flex items-center gap-3">
                        <div class="w-9 h-9 rounded-xl bg-brand-500/10 border border-brand-500/30 flex items-center justify-center glow-orange">
                            <i data-lucide="flame" class="w-5 h-5 text-brand-500"></i>
                        </div>
                        <div class="flex flex-col">
                            <span class="font-bold text-base tracking-tight text-white leading-none">CodeIgniter</span>
                            <span class="text-[10px] font-mono text-brand-500 font-semibold tracking-wider uppercase mt-0.5">Control Panel</span>
                        </div>
                    </a>
                    <button onclick="toggleSidebar()" class="lg:hidden text-slate-400 hover:text-white">
                        <i data-lucide="x" class="w-5 h-5"></i>
                    </button>
                </div>

                <!-- NAVIGATION LINKS -->
                <nav class="p-4 space-y-1">
                    <div class="px-3 py-2 text-[11px] font-semibold tracking-wider text-slate-400 uppercase">General</div>
                    
                    <a href="#" class="flex items-center gap-3 px-3 py-2.5 rounded-lg bg-brand-500/10 text-brand-500 font-medium text-sm transition-all border border-brand-500/20">
                        <i data-lucide="layout-dashboard" class="w-4 h-4"></i>
                        <span>Dashboard</span>
                    </a>

                    <a href="https://codeigniter.com/user_guide/" target="_blank" class="flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-400 hover:bg-slate-800/60 hover:text-slate-200 font-medium text-sm transition-all group">
                        <div class="flex items-center gap-3">
                            <i data-lucide="book-open" class="w-4 h-4 text-slate-500 group-hover:text-slate-300"></i>
                            <span>Documentación</span>
                        </div>
                        <i data-lucide="external-link" class="w-3.5 h-3.5 opacity-0 group-hover:opacity-100 transition-opacity"></i>
                    </a>

                    <a href="https://forum.codeigniter.com/" target="_blank" class="flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-400 hover:bg-slate-800/60 hover:text-slate-200 font-medium text-sm transition-all group">
                        <div class="flex items-center gap-3">
                            <i data-lucide="messages-square" class="w-4 h-4 text-slate-500 group-hover:text-slate-300"></i>
                            <span>Foro Comunidad</span>
                        </div>
                        <i data-lucide="external-link" class="w-3.5 h-3.5 opacity-0 group-hover:opacity-100 transition-opacity"></i>
                    </a>

                    <div class="pt-4 px-3 py-2 text-[11px] font-semibold tracking-wider text-slate-400 uppercase">Herramientas Dev</div>

                    <a href="https://github.com/codeigniter4/CodeIgniter4" target="_blank" class="flex items-center justify-between px-3 py-2.5 rounded-lg text-slate-400 hover:bg-slate-800/60 hover:text-slate-200 font-medium text-sm transition-all group">
                        <div class="flex items-center gap-3">
                            <i data-lucide="github" class="w-4 h-4 text-slate-500 group-hover:text-slate-300"></i>
                            <span>Repositorio GitHub</span>
                        </div>
                        <i data-lucide="external-link" class="w-3.5 h-3.5 opacity-0 group-hover:opacity-100 transition-opacity"></i>
                    </a>
                </nav>
            </div>

            <!-- SIDEBAR FOOTER -->
            <div class="p-4 border-t border-slate-800/80 bg-slate-900/50">
                <div class="flex items-center gap-3 p-2.5 rounded-xl bg-slate-800/50 border border-slate-700/50">
                    <div class="relative">
                        <div class="w-2.5 h-2.5 rounded-full bg-emerald-500"></div>
                        <div class="absolute inset-0 rounded-full bg-emerald-500 animate-ping opacity-75"></div>
                    </div>
                    <div class="flex flex-col">
                        <span class="text-xs font-semibold text-slate-200">Servidor Activo</span>
                        <span class="text-[10px] text-slate-400 font-mono">Modo: <?= ENVIRONMENT ?></span>
                    </div>
                </div>
            </div>
        </aside>

        <!-- MAIN CONTENT AREA -->
        <div class="flex-1 flex flex-col min-w-0 overflow-hidden">
            
            <!-- TOP NAVBAR -->
            <header class="h-16 border-b border-slate-800/80 bg-slate-900/60 backdrop-blur-md px-4 sm:px-6 flex items-center justify-between gap-4 sticky top-0 z-30">
                <div class="flex items-center gap-3">
                    <button onclick="toggleSidebar()" class="lg:hidden p-2 rounded-lg text-slate-400 hover:text-white hover:bg-slate-800 focus:outline-none">
                        <i data-lucide="menu" class="w-5 h-5"></i>
                    </button>
                    <div class="flex items-center gap-2">
                        <span class="text-sm font-semibold text-slate-300">Consola de Desarrollo</span>
                        <span class="text-xs px-2 py-0.5 rounded-md bg-slate-800 text-slate-400 font-mono border border-slate-700">v<?= CodeIgniter\CodeIgniter::CI_VERSION ?></span>
                    </div>
                </div>

                <div class="flex items-center gap-3">
                    <!-- COPY ALL PATHS BUTTON -->
                    <button onclick="copyToClipboard('app/Controllers/Home.php \napp/Views/welcome_message.php', 'rutas completas')" class="hidden sm:flex items-center gap-2 text-xs font-medium px-3 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-slate-300 border border-slate-700 transition-all">
                        <i data-lucide="copy" class="w-3.5 h-3.5 text-brand-500"></i>
                        <span>Copiar Rutas</span>
                    </button>
                    <!-- STATUS BADGE -->
                    <div class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 text-xs font-medium">
                        <span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span>
                        <span class="hidden sm:inline">Entorno:</span> <?= ucfirst(ENVIRONMENT) ?>
                    </div>
                </div>
            </header>

            <!-- MAIN SCROLLABLE CONTENT -->
            <main class="flex-1 overflow-y-auto p-4 sm:p-6 lg:p-8 space-y-6">

                <!-- WELCOME BANNER -->
                <div class="relative overflow-hidden rounded-2xl bg-gradient-to-r from-brand-900/40 via-slate-900 to-slate-900 border border-brand-500/20 p-6 sm:p-8">
                    <div class="absolute -right-10 -bottom-10 w-60 h-60 bg-brand-500/10 rounded-full blur-3xl pointer-events-none"></div>
                    <div class="relative z-10 max-w-2xl">
                        <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-brand-500/10 border border-brand-500/30 text-brand-500 text-xs font-semibold mb-3">
                            <i data-lucide="sparkles" class="w-3.5 h-3.5"></i>
                            <span>CodeIgniter 4 Instalado Correctamente</span>
                        </div>
                        <h1 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                            ¡Bienvenido al Panel de Inicio!
                        </h1>
                        <p class="mt-2 text-sm sm:text-base text-slate-400 leading-relaxed">
                            Tu entorno local PHP está configurado y optimizado. Utiliza este panel para monitorear el rendimiento del servidor y estructurar los archivos iniciales de tu proyecto.
                        </p>
                    </div>
                </div>

                <!-- METRICS GRID -->
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    
                    <!-- METRIC 1 -->
                    <div class="glass-panel p-5 rounded-xl flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium uppercase tracking-wider text-slate-400">Versión Framework</p>
                            <h3 class="text-2xl font-extrabold text-white mt-1 font-mono">v<?= CodeIgniter\CodeIgniter::CI_VERSION ?></h3>
                            <p class="text-[11px] text-emerald-400 flex items-center gap-1 mt-1">
                                <i data-lucide="check-circle-2" class="w-3 h-3"></i> Última versión estable
                            </p>
                        </div>
                        <div class="w-12 h-12 rounded-xl bg-blue-500/10 border border-blue-500/20 flex items-center justify-center text-blue-400">
                            <i data-lucide="layers" class="w-6 h-6"></i>
                        </div>
                    </div>

                    <!-- METRIC 2 -->
                    <div class="glass-panel p-5 rounded-xl flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium uppercase tracking-wider text-slate-400">Tiempo Renderizado</p>
                            <h3 class="text-2xl font-extrabold text-white mt-1 font-mono">{elapsed_time} <span class="text-sm font-normal text-slate-400">s</span></h3>
                            <p class="text-[11px] text-brand-500 flex items-center gap-1 mt-1">
                                <i data-lucide="zap" class="w-3 h-3"></i> Ejecución Ultra Rápida
                            </p>
                        </div>
                        <div class="w-12 h-12 rounded-xl bg-brand-500/10 border border-brand-500/20 flex items-center justify-center text-brand-500">
                            <i data-lucide="timer" class="w-6 h-6"></i>
                        </div>
                    </div>

                    <!-- METRIC 3 -->
                    <div class="glass-panel p-5 rounded-xl flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium uppercase tracking-wider text-slate-400">Uso de Memoria</p>
                            <h3 class="text-2xl font-extrabold text-white mt-1 font-mono">{memory_usage} <span class="text-sm font-normal text-slate-400">MB</span></h3>
                            <p class="text-[11px] text-emerald-400 flex items-center gap-1 mt-1">
                                <i data-lucide="arrow-down-right" class="w-3 h-3"></i> Consumo Ligero
                            </p>
                        </div>
                        <div class="w-12 h-12 rounded-xl bg-purple-500/10 border border-purple-500/20 flex items-center justify-center text-purple-400">
                            <i data-lucide="cpu" class="w-6 h-6"></i>
                        </div>
                    </div>

                    <!-- METRIC 4 -->
                    <div class="glass-panel p-5 rounded-xl flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium uppercase tracking-wider text-slate-400">Versión PHP</p>
                            <h3 class="text-2xl font-extrabold text-white mt-1 font-mono"><?= PHP_VERSION ?></h3>
                            <p class="text-[11px] text-slate-400 flex items-center gap-1 mt-1">
                                <i data-lucide="server" class="w-3 h-3"></i> Servidor Local
                            </p>
                        </div>
                        <div class="w-12 h-12 rounded-xl bg-amber-500/10 border border-amber-500/20 flex items-center justify-center text-amber-400">
                            <i data-lucide="hard-drive" class="w-6 h-6"></i>
                        </div>
                    </div>

                </div>

                <!-- CODE PATHS & STRUCTURE SECTION -->
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    
                    <!-- CARD: FILE ARCHITECTURE -->
                    <div class="glass-panel rounded-2xl p-6 border border-slate-800">
                        <div class="flex items-center justify-between mb-4">
                            <div class="flex items-center gap-2">
                                <i data-lucide="file-code-2" class="w-5 h-5 text-brand-500"></i>
                                <h2 class="font-bold text-lg text-white">Archivos de esta Vista</h2>
                            </div>
                            <span class="text-xs text-slate-400">Rutas en el proyecto</span>
                        </div>

                        <div class="space-y-4">
                            <!-- PATH 1 -->
                            <div class="p-4 rounded-xl bg-slate-900/90 border border-slate-800">
                                <div class="flex items-center justify-between mb-1.5">
                                    <span class="text-xs font-semibold text-slate-300 flex items-center gap-2">
                                        <i data-lucide="layout" class="w-3.5 h-3.5 text-blue-400"></i> Archivo de Vista HTML
                                    </span>
                                    <button onclick="copyToClipboard('app/Views/welcome_message.php', 'Vista')" class="text-slate-400 hover:text-white transition-colors">
                                        <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                                    </button>
                                </div>
                                <code class="text-xs font-mono text-brand-500 bg-brand-500/10 px-2.5 py-1 rounded border border-brand-500/20 block w-full overflow-x-auto">
                                    app/Views/welcome_message.php
                                </code>
                            </div>

                            <!-- PATH 2 -->
                            <div class="p-4 rounded-xl bg-slate-900/90 border border-slate-800">
                                <div class="flex items-center justify-between mb-1.5">
                                    <span class="text-xs font-semibold text-slate-300 flex items-center gap-2">
                                        <i data-lucide="cpu" class="w-3.5 h-3.5 text-purple-400"></i> Controlador Principal
                                    </span>
                                    <button onclick="copyToClipboard('app/Controllers/Home.php', 'Controlador')" class="text-slate-400 hover:text-white transition-colors">
                                        <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                                    </button>
                                </div>
                                <code class="text-xs font-mono text-emerald-400 bg-emerald-500/10 px-2.5 py-1 rounded border border-emerald-500/20 block w-full overflow-x-auto">
                                    app/Controllers/Home.php
                                </code>
                            </div>

                            <!-- PATH 3 -->
                            <div class="p-4 rounded-xl bg-slate-900/90 border border-slate-800">
                                <div class="flex items-center justify-between mb-1.5">
                                    <span class="text-xs font-semibold text-slate-300 flex items-center gap-2">
                                        <i data-lucide="git-fork" class="w-3.5 h-3.5 text-amber-400"></i> Configuración de Rutas
                                    </span>
                                    <button onclick="copyToClipboard('app/Config/Routes.php', 'Rutas')" class="text-slate-400 hover:text-white transition-colors">
                                        <i data-lucide="copy" class="w-3.5 h-3.5"></i>
                                    </button>
                                </div>
                                <code class="text-xs font-mono text-amber-400 bg-amber-500/10 px-2.5 py-1 rounded border border-amber-500/20 block w-full overflow-x-auto">
                                    app/Config/Routes.php
                                </code>
                            </div>
                        </div>
                    </div>

                    <!-- CARD: QUICK ACTIONS & GUIDE -->
                    <div class="glass-panel rounded-2xl p-6 border border-slate-800 flex flex-col justify-between">
                        <div>
                            <div class="flex items-center gap-2 mb-4">
                                <i data-lucide="rocket" class="w-5 h-5 text-emerald-400"></i>
                                <h2 class="font-bold text-lg text-white">Siguientes Pasos</h2>
                            </div>
                            <p class="text-xs text-slate-400 mb-4 leading-relaxed">
                                Para comenzar a crear tu aplicación web, edita la función <code class="text-slate-200 font-mono">index()</code> dentro de tu controlador o genera nuevas vistas y modelos con la CLI de Spark.
                            </p>

                            <!-- COMMAND BOX -->
                            <div class="p-4 rounded-xl bg-slate-950 border border-slate-800 font-mono text-xs text-slate-300 space-y-2 mb-4">
                                <div class="text-slate-400 font-sans text-[11px] uppercase tracking-wider mb-1">Comandos Spark Útiles:</div>
                                <div class="flex items-center justify-between group">
                                    <span class="text-brand-500">php spark serve</span>
                                    <span class="text-slate-400 text-[10px]">Iniciar servidor</span>
                                </div>
                                <div class="flex items-center justify-between group">
                                    <span class="text-emerald-400">php spark make:controller Demo</span>
                                    <span class="text-slate-400 text-[10px]">Crear Controlador</span>
                                </div>
                                <div class="flex items-center justify-between group">
                                    <span class="text-blue-400">php spark make:model User</span>
                                    <span class="text-slate-400 text-[10px]">Crear Modelo</span>
                                </div>
                            </div>
                        </div>

                        <div class="grid grid-cols-2 gap-3 pt-2">
                            <a href="https://codeigniter.com/user_guide/intro/index.html" target="_blank" class="flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-semibold transition-all border border-slate-700">
                                <i data-lucide="compass" class="w-4 h-4"></i>
                                <span>Guía de Inicio</span>
                            </a>
                            <a href="https://codeigniter.com/user_guide/cli/spark.html" target="_blank" class="flex items-center justify-center gap-2 px-4 py-2.5 rounded-xl bg-brand-500 hover:bg-brand-600 text-white text-xs font-semibold transition-all glow-orange">
                                <i data-lucide="terminal" class="w-4 h-4"></i>
                                <span>Aprender Spark</span>
                            </a>
                        </div>
                    </div>

                </div>

            </main>

            <!-- FOOTER -->
            <footer class="h-12 border-t border-slate-800/80 bg-slate-900/40 px-6 flex items-center justify-between text-xs text-slate-400">
                <p>&copy; <?= date('Y') ?> CodeIgniter Foundation. Licencia MIT.</p>
                <div class="flex items-center gap-4">
                    <span class="flex items-center gap-1.5">
                        <span class="w-2 h-2 rounded-full bg-emerald-500"></span>
                        <span>Sistema Operativo</span>
                    </span>
                </div>
            </footer>

        </div>
    </div>

    <!-- TOAST NOTIFICATION FOR COPY ACTION -->
    <div id="copyToast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 ease-out pointer-events-none">
        <div class="flex items-center gap-3 px-4 py-3 rounded-xl bg-slate-800 border border-slate-700 text-white shadow-2xl">
            <div class="w-7 h-7 rounded-lg bg-emerald-500/20 text-emerald-400 flex items-center justify-center">
                <i data-lucide="check" class="w-4 h-4"></i>
            </div>
            <div class="text-xs">
                <p class="font-semibold text-slate-200" id="toastTitle">Copiado al portapapeles</p>
                <p class="text-slate-400" id="toastDesc">La ruta ha sido copiada con éxito.</p>
            </div>
        </div>
    </div>

    <!-- SCRIPTS -->
    <script>
        // Initialize Lucide Icons
        lucide.createIcons();

        // Responsive Sidebar Toggle
        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const backdrop = document.getElementById('sidebarBackdrop');
            
            sidebar.classList.toggle('-translate-x-full');
            backdrop.classList.toggle('hidden');
        }

        // Copy to Clipboard Functionality
        function copyToClipboard(text, label) {
            // Safe fallback clipboard copy
            const dummy = document.createElement('textarea');
            document.body.appendChild(dummy);
            dummy.value = text;
            dummy.select();
            document.execCommand('copy');
            document.body.removeChild(dummy);

            // Show Toast
            const toast = document.getElementById('copyToast');
            const toastTitle = document.getElementById('toastTitle');
            const toastDesc = document.getElementById('toastDesc');

            toastTitle.innerText = `¡Ruta de ${label} copiada!`;
            toastDesc.innerText = text;

            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 2500);
        }
    </script>
</body>
</html>
