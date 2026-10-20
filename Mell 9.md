<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CodeIgniter 4 // Terminal Core v4.4</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font: JetBrains Mono -->
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,700;1,400&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        term: {
                            black: '#0a0d0e',
                            dark: '#0f1416',
                            card: '#141c1f',
                            border: '#1f2d33',
                            green: '#00ff66',
                            dimGreen: '#00b347',
                            cyan: '#00e5ff',
                            amber: '#ffb000',
                            red: '#ff3366',
                            comment: '#4a6572'
                        }
                    },
                    fontFamily: {
                        mono: ['"JetBrains Mono"', 'monospace']
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'JetBrains Mono', monospace;
            background-color: #0a0d0e;
            color: #00ff66;
        }

        /* Scanlines Overlay Effect */
        .scanlines {
            background: linear-gradient(
                rgba(18, 16, 16, 0) 50%, 
                rgba(0, 0, 0, 0.35) 50%
            ), linear-gradient(
                90deg,
                rgba(255, 0, 0, 0.03),
                rgba(0, 255, 0, 0.01),
                rgba(0, 0, 255, 0.03)
            );
            background-size: 100% 4px, 6px 100%;
            pointer-events: none;
        }

        /* Terminal Glow Effects */
        .glow-green {
            text-shadow: 0 0 8px rgba(0, 255, 102, 0.6);
        }
        .glow-cyan {
            text-shadow: 0 0 8px rgba(0, 229, 255, 0.6);
        }
        .box-glow {
            box-shadow: 0 0 15px rgba(0, 255, 102, 0.1);
        }
        .box-glow:hover {
            box-shadow: 0 0 20px rgba(0, 255, 102, 0.25);
        }

        /* Scrollbar styling */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #0f1416;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2d33;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00ff66;
        }

        /* Blinking Cursor Animation */
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }
        .cursor-blink {
            animation: blink 1s infinite;
        }
    </style>
</head>
<body class="bg-term-black text-term-green min-h-screen relative flex flex-col selection:bg-term-green selection:text-term-black">
    
    <!-- CRT Scanline overlay -->
    <div class="fixed inset-0 scanlines z-50"></div>

    <!-- Main Container -->
    <div class="container mx-auto px-4 py-6 max-w-6xl flex-1 flex flex-col gap-6 relative z-10">

        <!-- Top Header Bar -->
        <header class="border border-term-border bg-term-dark p-4 rounded-lg flex flex-wrap justify-between items-center gap-4 box-glow">
            <div class="flex items-center space-x-3">
                <i class="fa-solid fa-terminal text-2xl text-term-green glow-green"></i>
                <div>
                    <h1 class="text-xl font-bold tracking-wider text-white glow-green flex items-center gap-2">
                        CODEIGNITER<span class="text-term-green">4</span>_SHELL
                    </h1>
                    <p class="text-xs text-term-comment">[System Version :: <?= CodeIgniter\CodeIgniter::CI_VERSION ?>]</p>
                </div>
            </div>

            <!-- Status Badges -->
            <div class="flex items-center gap-3 text-xs">
                <span class="px-2.5 py-1 bg-term-card border border-term-border rounded text-term-cyan flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-term-cyan animate-pulse"></span>
                    ENV: <?= ENVIRONMENT ?>
                </span>
                <span class="px-2.5 py-1 bg-term-card border border-term-border rounded text-term-green flex items-center gap-2">
                    <span class="w-2 h-2 rounded-full bg-term-green"></span>
                    STATUS: ONLINE
                </span>
            </div>
        </header>

        <!-- System Telemetry Metrics -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="bg-term-card border border-term-border p-3.5 rounded-lg box-glow">
                <div class="text-xs text-term-comment font-bold mb-1">// RENDER TIME</div>
                <div class="text-lg text-term-cyan font-bold glow-cyan">{elapsed_time} s</div>
                <div class="w-full bg-term-dark h-1.5 mt-2 rounded overflow-hidden border border-term-border">
                    <div class="bg-term-cyan h-full" style="width: 28%"></div>
                </div>
            </div>
            
            <div class="bg-term-card border border-term-border p-3.5 rounded-lg box-glow">
                <div class="text-xs text-term-comment font-bold mb-1">// MEMORY CONSUMPTION</div>
                <div class="text-lg text-term-amber font-bold">1.42 MB</div>
                <div class="w-full bg-term-dark h-1.5 mt-2 rounded overflow-hidden border border-term-border">
                    <div class="bg-term-amber h-full" style="width: 15%"></div>
                </div>
            </div>

            <div class="bg-term-card border border-term-border p-3.5 rounded-lg box-glow">
                <div class="text-xs text-term-comment font-bold mb-1">// PHP ENGINE</div>
                <div class="text-lg text-white font-bold">v<?= PHP_VERSION ?></div>
                <div class="text-[10px] text-term-dimGreen mt-1">Zend Engine v<?= zend_version() ?></div>
            </div>

            <div class="bg-term-card border border-term-border p-3.5 rounded-lg box-glow">
                <div class="text-xs text-term-comment font-bold mb-1">// CONTROLLER NODE</div>
                <div class="text-sm text-term-green truncate font-bold" title="Home::index">Home::index</div>
                <div class="text-[10px] text-term-comment mt-1">app/Controllers/Home.php</div>
            </div>
        </div>

        <!-- Interactive Terminal Simulator -->
        <section class="bg-term-card border border-term-border rounded-lg overflow-hidden box-glow flex flex-col">
            <!-- Terminal Header -->
            <div class="bg-term-dark px-4 py-2 border-b border-term-border flex items-center justify-between">
                <div class="flex items-center space-x-2">
                    <span class="w-3 h-3 rounded-full bg-term-red inline-block"></span>
                    <span class="w-3 h-3 rounded-full bg-term-amber inline-block"></span>
                    <span class="w-3 h-3 rounded-full bg-term-green inline-block"></span>
                    <span class="text-xs text-term-comment ml-2 font-mono">bash - spark@localhost:~</span>
                </div>
                <div class="text-xs text-term-comment">UTF-8</div>
            </div>

            <!-- Terminal Output Window -->
            <div id="terminal-output" class="p-4 h-64 overflow-y-auto space-y-2 text-sm font-mono leading-relaxed bg-term-black/50">
                <p class="text-term-comment">// CodeIgniter 4 Interactive CLI Window</p>
                <p class="text-term-comment">// Type <span class="text-term-amber">'help'</span> or click any command below to execute.</p>
                <div class="text-term-cyan">
                    <span>root@ci4-node:~#</span> <span class="text-white">php spark --version</span>
                </div>
                <div class="text-term-dimGreen pl-4">CodeIgniter CLI Framework v<?= CodeIgniter\CodeIgniter::CI_VERSION ?></div>
            </div>

            <!-- Command Line Input -->
            <div class="p-3 bg-term-dark border-t border-term-border flex items-center gap-2">
                <span class="text-term-green font-bold text-sm">root@ci4-node:~#</span>
                <input type="text" id="cli-input" placeholder="Escribe un comando... (e.g. 'help', 'routes', 'clear')" 
                       class="flex-1 bg-transparent border-none outline-none text-white text-sm font-mono focus:ring-0 placeholder-term-comment"
                       autocomplete="off" spellcheck="false">
                <button onclick="processCommand()" class="px-3 py-1 bg-term-border hover:bg-term-green hover:text-term-black text-xs font-bold transition-colors rounded">
                    RUN
                </button>
            </div>
        </section>

        <!-- Main Content Grid -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            <!-- Left Column: Setup & Page Editing -->
            <div class="lg:col-span-2 space-y-6">
                <!-- File Editing Quick Access -->
                <div class="bg-term-card border border-term-border p-5 rounded-lg box-glow space-y-4">
                    <div class="flex items-center justify-between border-b border-term-border pb-3">
                        <h2 class="text-base font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-code text-term-green"></i> 01. EDITING_TARGETS
                        </h2>
                        <span class="text-xs text-term-comment">// Main Entrypoints</span>
                    </div>

                    <p class="text-xs text-term-dimGreen">
                        Para personalizar esta página o crear nuevas rutas, modifica los siguientes archivos base de la aplicación:
                    </p>

                    <!-- File Cards -->
                    <div class="space-y-3">
                        <div class="bg-term-dark border border-term-border p-3 rounded flex items-center justify-between group hover:border-term-green transition-colors">
                            <div class="overflow-hidden mr-2">
                                <div class="text-xs text-term-comment">// View File Layout</div>
                                <code class="text-sm text-term-cyan font-bold block truncate">app/Views/welcome_message.php</code>
                            </div>
                            <button onclick="copyPath('app/Views/welcome_message.php', this)" class="px-2.5 py-1.5 bg-term-border hover:bg-term-green hover:text-term-black text-xs rounded transition-all flex items-center gap-1.5 shrink-0">
                                <i class="fa-regular fa-copy"></i> Copy
                            </button>
                        </div>

                        <div class="bg-term-dark border border-term-border p-3 rounded flex items-center justify-between group hover:border-term-green transition-colors">
                            <div class="overflow-hidden mr-2">
                                <div class="text-xs text-term-comment">// Controller File</div>
                                <code class="text-sm text-term-cyan font-bold block truncate">app/Controllers/Home.php</code>
                            </div>
                            <button onclick="copyPath('app/Controllers/Home.php', this)" class="px-2.5 py-1.5 bg-term-border hover:bg-term-green hover:text-term-black text-xs rounded transition-all flex items-center gap-1.5 shrink-0">
                                <i class="fa-regular fa-copy"></i> Copy
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Spark CLI Shortcuts -->
                <div class="bg-term-card border border-term-border p-5 rounded-lg box-glow space-y-4">
                    <div class="flex items-center justify-between border-b border-term-border pb-3">
                        <h2 class="text-base font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-bolt text-term-amber"></i> 02. SPARK_COMMANDS
                        </h2>
                        <span class="text-xs text-term-comment">// Click to test in terminal</span>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
                        <button onclick="runSparkShortcut('php spark serve')" class="text-left bg-term-dark border border-term-border p-3 rounded hover:border-term-amber transition-colors group">
                            <div class="text-xs text-term-amber font-bold flex items-center justify-between">
                                php spark serve
                                <i class="fa-solid fa-chevron-right opacity-0 group-hover:opacity-100 transition-opacity"></i>
                            </div>
                            <div class="text-[11px] text-term-comment mt-1">Inicia el servidor de desarrollo local</div>
                        </button>

                        <button onclick="runSparkShortcut('php spark routes')" class="text-left bg-term-dark border border-term-border p-3 rounded hover:border-term-amber transition-colors group">
                            <div class="text-xs text-term-amber font-bold flex items-center justify-between">
                                php spark routes
                                <i class="fa-solid fa-chevron-right opacity-0 group-hover:opacity-100 transition-opacity"></i>
                            </div>
                            <div class="text-[11px] text-term-comment mt-1">Muestra todas las rutas registradas</div>
                        </button>

                        <button onclick="runSparkShortcut('php spark make:controller')" class="text-left bg-term-dark border border-term-border p-3 rounded hover:border-term-amber transition-colors group">
                            <div class="text-xs text-term-amber font-bold flex items-center justify-between">
                                php spark make:controller
                                <i class="fa-solid fa-chevron-right opacity-0 group-hover:opacity-100 transition-opacity"></i>
                            </div>
                            <div class="text-[11px] text-term-comment mt-1">Genera una nueva plantilla de Controlador</div>
                        </button>

                        <button onclick="runSparkShortcut('php spark migrate')" class="text-left bg-term-dark border border-term-border p-3 rounded hover:border-term-amber transition-colors group">
                            <div class="text-xs text-term-amber font-bold flex items-center justify-between">
                                php spark migrate
                                <i class="fa-solid fa-chevron-right opacity-0 group-hover:opacity-100 transition-opacity"></i>
                            </div>
                            <div class="text-[11px] text-term-comment mt-1">Ejecuta las migraciones pendientes</div>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Right Column: Navigation & Docs -->
            <div class="space-y-6">
                <!-- External Resources -->
                <div class="bg-term-card border border-term-border p-5 rounded-lg box-glow space-y-4">
                    <div class="flex items-center justify-between border-b border-term-border pb-3">
                        <h2 class="text-base font-bold text-white flex items-center gap-2">
                            <i class="fa-solid fa-network-wired text-term-cyan"></i> 03. MATRIX_LINKS
                        </h2>
                    </div>

                    <ul class="space-y-2 text-xs">
                        <li>
                            <a href="https://codeigniter.com/userguide/index.html" target="_blank" 
                               class="flex items-center justify-between p-2.5 bg-term-dark rounded border border-term-border hover:border-term-cyan hover:text-term-cyan transition-colors">
                                <span class="flex items-center gap-2">
                                    <i class="fa-solid fa-book text-term-comment"></i> Official User Guide
                                </span>
                                <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                            </a>
                        </li>
                        <li>
                            <a href="https://forum.codeigniter.com/" target="_blank" 
                               class="flex items-center justify-between p-2.5 bg-term-dark rounded border border-term-border hover:border-term-cyan hover:text-term-cyan transition-colors">
                                <span class="flex items-center gap-2">
                                    <i class="fa-solid fa-comments text-term-comment"></i> Community Forum
                                </span>
                                <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                            </a>
                        </li>
                        <li>
                            <a href="https://github.com/codeigniter4/CodeIgniter4" target="_blank" 
                               class="flex items-center justify-between p-2.5 bg-term-dark rounded border border-term-border hover:border-term-cyan hover:text-term-cyan transition-colors">
                                <span class="flex items-center gap-2">
                                    <i class="fa-brands fa-github text-term-comment"></i> GitHub Repository
                                </span>
                                <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                            </a>
                        </li>
                    </ul>
                </div>

                <!-- Environment Warning Box -->
                <div class="bg-term-card border border-term-amber/40 p-4 rounded-lg space-y-2">
                    <div class="text-xs font-bold text-term-amber flex items-center gap-2">
                        <i class="fa-solid fa-triangle-exclamation"></i> SECURITY_NOTICE
                    </div>
                    <p class="text-[11px] text-term-comment leading-relaxed">
                        Asegúrate de cambiar <code class="text-white">CI_ENVIRONMENT</code> a <code class="text-term-green">production</code> en tu archivo <code class="text-white">.env</code> antes de desplegar este servidor a un entorno público.
                    </p>
                </div>
            </div>

        </div>

        <!-- Notification Toast -->
        <div id="toast" class="fixed bottom-6 right-6 bg-term-green text-term-black px-4 py-2.5 rounded shadow-lg font-bold text-xs transform translate-y-20 opacity-0 transition-all duration-300 flex items-center gap-2 pointer-events-none z-50">
            <i class="fa-solid fa-check-circle"></i>
            <span id="toast-message">Copiado al portapapeles</span>
        </div>

        <!-- Footer Bar -->
        <footer class="mt-auto pt-4 border-t border-term-border flex flex-wrap justify-between items-center text-xs text-term-comment gap-2">
            <div>
                SYS_TIME: <span class="text-term-green"><?= date('Y-m-d H:i:s') ?> UTC</span>
            </div>
            <div>
                CodeIgniter 4 CLI Theme &copy; <?= date('Y') ?>
            </div>
        </footer>

    </div>

    <!-- Terminal Logic Script -->
    <script>
        const cliInput = document.getElementById('cli-input');
        const terminalOutput = document.getElementById('terminal-output');

        // Command processing logic
        function processCommand() {
            const cmd = cliInput.value.trim().toLowerCase();
            if (!cmd) return;

            // Echo input command
            appendTerminalLine(`root@ci4-node:~# ${cliInput.value}`, 'text-term-cyan');

            // Handle commands
            switch (cmd) {
                case 'help':
                    appendTerminalLine('Comandos disponibles:', 'text-term-amber');
                    appendTerminalLine(' - help               : Muestra este menú de ayuda');
                    appendTerminalLine(' - routes             : Simula listado de rutas');
                    appendTerminalLine(' - env                : Muestra variables de entorno');
                    appendTerminalLine(' - version            : Versión del Framework');
                    appendTerminalLine(' - clear              : Limpia la consola');
                    appendTerminalLine(' - php spark serve    : Comando de servidor');
                    break;
                case 'routes':
                    appendTerminalLine('+--------+-------------------+-------------------+', 'text-term-comment');
                    appendTerminalLine('| Method | Route             | Handler           |', 'text-term-comment');
                    appendTerminalLine('+--------+-------------------+-------------------+', 'text-term-comment');
                    appendTerminalLine('| GET    | /                 | \\App\\Controllers\\Home::index |');
                    appendTerminalLine('+--------+-------------------+-------------------+', 'text-term-comment');
                    break;
                case 'env':
                    appendTerminalLine('CI_ENVIRONMENT = <?= ENVIRONMENT ?>', 'text-term-green');
                    appendTerminalLine('app.baseURL = http://localhost:8080/', 'text-term-green');
                    break;
                case 'version':
                    appendTerminalLine('CodeIgniter v<?= CodeIgniter\CodeIgniter::CI_VERSION ?>', 'text-term-green');
                    break;
                case 'clear':
                    terminalOutput.innerHTML = '';
                    break;
                default:
                    if (cmd.startsWith('php spark')) {
                        appendTerminalLine(`[EXEC] Running '${cmd}'...`, 'text-term-amber');
                        appendTerminalLine('Command executed successfully in simulation context.', 'text-term-dimGreen');
                    } else {
                        appendTerminalLine(`bash: command not found: ${cmd}. Type 'help' for options.`, 'text-term-red');
                    }
                    break;
            }

            cliInput.value = '';
            terminalOutput.scrollTop = terminalOutput.scrollHeight;
        }

        function appendTerminalLine(text, colorClass = 'text-term-dimGreen') {
            const line = document.createElement('div');
            line.className = colorClass;
            line.innerText = text;
            terminalOutput.appendChild(line);
        }

        function runSparkShortcut(command) {
            cliInput.value = command;
            processCommand();
            cliInput.focus();
        }

        // Listen for enter key in CLI input
        cliInput.addEventListener('keydown', function(e) {
            if (e.key === 'Enter') {
                processCommand();
            }
        });

        // Copy path helper function
        function copyPath(text, buttonElement) {
            var tempInput = document.createElement("input");
            tempInput.value = text;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand("copy");
            document.body.removeChild(tempInput);

            showToast(`Copiado: ${text}`);
        }

        function showToast(message) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toast-message');
            toastMsg.innerText = message;

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
