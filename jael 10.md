<!DOCTYPE html>
<html lang="es" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to CodeIgniter 4</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        // Configuración de Tailwind para soporte de modo oscuro
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        ci: {
                            orange: '#dd4814',
                            dark: '#222222',
                            blue: '#0284c7'
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome para Iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        code, pre { font-family: 'Fira Code', monospace; }
        .glass { background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(10px); }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-900 dark:text-slate-100 min-h-full transition-colors duration-300 flex flex-col">

    <!-- HEADER DEGRADADO -->
    <header class="bg-gradient-to-r from-blue-700 via-indigo-600 to-slate-900 text-white shadow-xl relative overflow-hidden">
        <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#fff_1px,transparent_1px)] [background-size:16px_16px]"></div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 relative z-10 flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center space-x-4">
                <div class="p-3 bg-white/10 rounded-2xl backdrop-blur-md border border-white/20 shadow-inner">
                    <i class="fa-solid font-bold text-3xl text-orange-500 fa-fire"></i>
                </div>
                <div>
                    <h1 class="text-3xl font-extrabold tracking-tight">CodeIgniter <span class="text-orange-500">4.x</span></h1>
                    <p class="text-blue-100 text-sm font-medium">Framework PHP rápido, flexible y liviano</p>
                </div>
            </div>
            
            <div class="flex items-center gap-3">
                <button id="darkModeToggle" onclick="toggleDarkMode()" class="p-2.5 rounded-xl bg-white/10 hover:bg-white/20 border border-white/20 transition-all text-white flex items-center gap-2 text-sm font-medium focus:outline-none">
                    <i id="darkModeIcon" class="fa-solid fa-moon"></i>
                    <span id="darkModeText">Modo Oscuro</span>
                </button>
            </div>
        </div>
    </header>

    <!-- METRICS DASHBOARD -->
    <section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 -mt-6 relative z-20 w-full">
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-md border border-slate-200/80 dark:border-slate-700/60 flex items-center space-x-3">
                <div class="p-3 bg-green-100 dark:bg-green-900/40 text-green-600 dark:text-green-400 rounded-xl">
                    <i class="fa-solid fa-server text-lg"></i>
                </div>
                <div>
                    <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">Estado Servidor</p>
                    <p class="text-sm font-semibold text-green-600 dark:text-green-400 flex items-center gap-1">
                        <span class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></span> Activo
                    </p>
                </div>
            </div>

            <div class="bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-md border border-slate-200/80 dark:border-slate-700/60 flex items-center space-x-3">
                <div class="p-3 bg-blue-100 dark:bg-blue-900/40 text-blue-600 dark:text-blue-400 rounded-xl">
                    <i class="fa-brands fa-php text-lg"></i>
                </div>
                <div>
                    <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">Versión PHP</p>
                    <p class="text-sm font-semibold">8.2.12 (CLI)</p>
                </div>
            </div>

            <div class="bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-md border border-slate-200/80 dark:border-slate-700/60 flex items-center space-x-3">
                <div class="p-3 bg-purple-100 dark:bg-purple-900/40 text-purple-600 dark:text-purple-400 rounded-xl">
                    <i class="fa-solid fa-code text-lg"></i>
                </div>
                <div>
                    <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">Entorno</p>
                    <p class="text-sm font-semibold text-purple-600 dark:text-purple-400">development</p>
                </div>
            </div>

            <div class="bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-md border border-slate-200/80 dark:border-slate-700/60 flex items-center space-x-3">
                <div class="p-3 bg-amber-100 dark:bg-amber-900/40 text-amber-600 dark:text-amber-400 rounded-xl">
                    <i class="fa-solid fa-eye text-lg"></i>
                </div>
                <div>
                    <p class="text-xs text-slate-500 dark:text-slate-400 font-medium">Visitas Locales</p>
                    <p id="visitCount" class="text-sm font-semibold">1</p>
                </div>
            </div>
        </div>
    </section>

    <!-- CONTENIDO PRINCIPAL -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8 flex-grow w-full">

        <!-- BUSCADOR / FILTRO DINÁMICO -->
        <div class="bg-white dark:bg-slate-800 p-4 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="relative w-full sm:w-96">
                <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-1/2 -translate-y-1/2 text-slate-400"></i>
                <input type="text" id="searchInput" onkeyup="filterCards()" placeholder="Buscar tarjeta, recurso o prueba..." class="w-full pl-10 pr-4 py-2 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 text-sm">
            </div>
            <span id="searchStats" class="text-xs text-slate-500 dark:text-slate-400">Mostrando todas las tarjetas</span>
        </div>

        <!-- GRID DE TARJETAS (CARDS GRID) -->
        <div id="cardsGrid" class="grid grid-cols-1 md:grid-cols-3 gap-6">

            <!-- Card 1: Controlador por Defecto -->
            <div class="card-item bg-white dark:bg-slate-800 rounded-2xl shadow-sm hover:shadow-xl transition-all duration-300 border border-slate-200 dark:border-slate-700 p-6 flex flex-col justify-between group">
                <div>
                    <div class="w-12 h-12 bg-blue-100 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-compass text-xl"></i>
                    </div>
                    <h3 class="text-lg font-bold mb-2 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors">Controlador Actual</h3>
                    <p class="text-slate-600 dark:text-slate-300 text-sm mb-4">La página que estás viendo es generada dinámicamente por el controlador predeterminado:</p>
                    <div class="bg-slate-100 dark:bg-slate-900/80 p-3 rounded-xl border border-slate-200 dark:border-slate-800 flex items-center justify-between group/code mb-3">
                        <code class="text-xs text-orange-600 dark:text-orange-400 font-mono overflow-x-auto">app/Controllers/Home.php</code>
                        <button onclick="copyToClipboard('app/Controllers/Home.php', this)" class="text-slate-400 hover:text-blue-500 p-1.5 rounded-lg hover:bg-slate-200 dark:hover:bg-slate-800 transition-colors">
                            <i class="fa-regular fa-copy"></i>
                        </button>
                    </div>
                </div>
                <span class="text-xs text-slate-400">Ruta: <code>/</code></span>
            </div>

            <!-- Card 2: Vista de Plantilla -->
            <div class="card-item bg-white dark:bg-slate-800 rounded-2xl shadow-sm hover:shadow-xl transition-all duration-300 border border-slate-200 dark:border-slate-700 p-6 flex flex-col justify-between group">
                <div>
                    <div class="w-12 h-12 bg-orange-100 dark:bg-orange-900/30 text-orange-600 dark:text-orange-400 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-file-code text-xl"></i>
                    </div>
                    <h3 class="text-lg font-bold mb-2 group-hover:text-orange-600 dark:group-hover:text-orange-400 transition-colors">Vista Rendereada</h3>
                    <p class="text-slate-600 dark:text-slate-300 text-sm mb-4">El diseño HTML y la maquetación provienen del siguiente archivo de vista:</p>
                    <div class="bg-slate-100 dark:bg-slate-900/80 p-3 rounded-xl border border-slate-200 dark:border-slate-800 flex items-center justify-between group/code mb-3">
                        <code class="text-xs text-orange-600 dark:text-orange-400 font-mono overflow-x-auto">app/Views/welcome_message.php</code>
                        <button onclick="copyToClipboard('app/Views/welcome_message.php', this)" class="text-slate-400 hover:text-orange-500 p-1.5 rounded-lg hover:bg-slate-200 dark:hover:bg-slate-800 transition-colors">
                            <i class="fa-regular fa-copy"></i>
                        </button>
                    </div>
                </div>
                <span class="text-xs text-slate-400">Plantilla principal HTML</span>
            </div>

            <!-- Card 3: Documentación & Guías -->
            <div class="card-item bg-white dark:bg-slate-800 rounded-2xl shadow-sm hover:shadow-xl transition-all duration-300 border border-slate-200 dark:border-slate-700 p-6 flex flex-col justify-between group">
                <div>
                    <div class="w-12 h-12 bg-indigo-100 dark:bg-indigo-900/30 text-indigo-600 dark:text-indigo-400 rounded-xl flex items-center justify-center mb-4 group-hover:scale-110 transition-transform">
                        <i class="fa-solid fa-book text-xl"></i>
                    </div>
                    <h3 class="text-lg font-bold mb-2 group-hover:text-indigo-600 dark:group-hover:text-indigo-400 transition-colors">Aprender Más</h3>
                    <p class="text-slate-600 dark:text-slate-300 text-sm mb-4">Consulta la documentación oficial de CodeIgniter 4 para dominar el framework rápidamente.</p>
                    <div class="flex flex-col gap-2">
                        <a href="https://codeigniter.com/user_guide/" target="_blank" class="text-xs text-blue-600 dark:text-blue-400 hover:underline flex items-center gap-1">
                            <i class="fa-solid fa-arrow-up-right-from-square"></i> Manual de Usuario Oficial
                        </a>
                        <a href="https://forum.codeigniter.com/" target="_blank" class="text-xs text-blue-600 dark:text-blue-400 hover:underline flex items-center gap-1">
                            <i class="fa-solid fa-users"></i> Foro de la Comunidad
                        </a>
                    </div>
                </div>
                <span class="text-xs text-slate-400 mt-4">Recursos externos</span>
            </div>

        </div>

        <!-- GENERADOR DE PLANTILLAS DE RUTAS Y CONTROLADORES PHP (NUEVA MODIFICACIÓN SOLICITADA) -->
        <section class="bg-white dark:bg-slate-800 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between pb-4 mb-4 border-b border-slate-200 dark:border-slate-700 gap-2">
                <div>
                    <h2 class="text-xl font-bold flex items-center gap-2">
                        <i class="fa-solid fa-laptop-code text-blue-600 dark:text-blue-400"></i> Generador de Plantillas PHP (Snippet Builder)
                    </h2>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Genera código estándar para tus controladores, modelos, middleware y servicios con un clic.</p>
                </div>
                <button onclick="copySnippet()" class="self-start sm:self-auto px-3 py-2 bg-blue-600 hover:bg-blue-700 text-white rounded-xl text-xs font-semibold flex items-center gap-2 transition-all shadow-md">
                    <i class="fa-regular fa-copy"></i> Copiar Código PHP
                </button>
            </div>

            <!-- Selector de Pestañas (Tabs) -->
            <div class="flex flex-wrap gap-2 mb-4" id="snippetTabs">
                <button onclick="selectSnippet('rest')" id="tab-rest" class="snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-blue-600 text-white transition-all">
                    <i class="fa-solid fa-network-wired mr-1"></i> REST API Controller
                </button>
                <button onclick="selectSnippet('filter')" id="tab-filter" class="snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 transition-all">
                    <i class="fa-solid fa-shield-halved mr-1"></i> Filtro / Middleware
                </button>
                <button onclick="selectSnippet('model')" id="tab-model" class="snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 transition-all">
                    <i class="fa-solid fa-database mr-1"></i> Modelo Entity
                </button>
                <button onclick="selectSnippet('routes')" id="tab-routes" class="snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 transition-all">
                    <i class="fa-solid fa-route mr-1"></i> Rutas API (Routes.php)
                </button>
            </div>

            <!-- Visor de Código -->
            <div class="relative bg-slate-900 rounded-xl p-4 overflow-x-auto border border-slate-800 shadow-inner">
                <pre><code id="snippetCode" class="text-xs font-mono text-emerald-400 leading-relaxed"></code></pre>
            </div>
        </section>

        <!-- MÓDULO DE PRUEBAS RÁPIDAS -->
        <section class="bg-white dark:bg-slate-800 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
            <h2 class="text-xl font-bold mb-2 flex items-center gap-2">
                <i class="fa-solid fa-vial text-purple-600 dark:text-purple-400"></i> Módulo de Pruebas Rápidas
            </h2>
            <p class="text-xs text-slate-500 dark:text-slate-400 mb-6">Simula respuestas de endpoints, conexión a base de datos y envío de correos sin recargar la página.</p>

            <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mb-6">
                <button onclick="runTest('db')" class="p-4 rounded-xl border border-slate-200 dark:border-slate-700 hover:border-blue-500 dark:hover:border-blue-500 hover:bg-blue-50/50 dark:hover:bg-blue-900/10 text-left transition-all group">
                    <div class="flex items-center justify-between mb-2">
                        <i class="fa-solid fa-database text-lg text-blue-500"></i>
                        <i class="fa-solid fa-play text-xs text-slate-400 group-hover:text-blue-500 transition-colors"></i>
                    </div>
                    <p class="font-bold text-sm">Test de Base de Datos</p>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Verifica parámetros de conexión PDO</p>
                </button>

                <button onclick="runTest('api')" class="p-4 rounded-xl border border-slate-200 dark:border-slate-700 hover:border-emerald-500 dark:hover:border-emerald-500 hover:bg-emerald-50/50 dark:hover:bg-emerald-900/10 text-left transition-all group">
                    <div class="flex items-center justify-between mb-2">
                        <i class="fa-solid fa-bolt text-lg text-emerald-500"></i>
                        <i class="fa-solid fa-play text-xs text-slate-400 group-hover:text-emerald-500 transition-colors"></i>
                    </div>
                    <p class="font-bold text-sm">Test de Endpoint JSON</p>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Simula respuesta API 200 OK</p>
                </button>

                <button onclick="runTest('mail')" class="p-4 rounded-xl border border-slate-200 dark:border-slate-700 hover:border-amber-500 dark:hover:border-amber-500 hover:bg-amber-50/50 dark:hover:bg-amber-900/10 text-left transition-all group">
                    <div class="flex items-center justify-between mb-2">
                        <i class="fa-solid fa-paper-plane text-lg text-amber-500"></i>
                        <i class="fa-solid fa-play text-xs text-slate-400 group-hover:text-amber-500 transition-colors"></i>
                    </div>
                    <p class="font-bold text-sm">Test Servicio Mail</p>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Simula cola de correos SMTP</p>
                </button>
            </div>

            <!-- HISTORIAL DE PRUEBAS -->
            <div class="border-t border-slate-200 dark:border-slate-700 pt-4">
                <div class="flex justify-between items-center mb-3">
                    <h3 class="text-xs font-bold uppercase tracking-wider text-slate-400">Historial de Ejecución</h3>
                    <button onclick="clearLogs()" class="text-xs text-red-500 hover:text-red-700 flex items-center gap-1 focus:outline-none">
                        <i class="fa-solid fa-trash-can"></i> Limpiar Historial
                    </button>
                </div>
                <div id="testLogs" class="space-y-2 max-h-48 overflow-y-auto pr-1">
                    <p id="emptyLogText" class="text-xs text-slate-400 italic">No hay pruebas ejecutadas en esta sesión.</p>
                </div>
            </div>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-white dark:bg-slate-800 border-t border-slate-200 dark:border-slate-700 py-6 mt-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex flex-col sm:flex-row justify-between items-center gap-4 text-xs text-slate-500 dark:text-slate-400">
            <p>CodeIgniter 4 - Renderizado dinámico de página de bienvenida</p>
            <p class="flex items-center gap-1">
                Página generada en <span class="font-semibold text-slate-700 dark:text-slate-200">0.034</span> segundos. Uso de memoria: <span class="font-semibold text-slate-700 dark:text-slate-200">2.4 MB</span>
            </p>
        </div>
    </footer>

    <!-- JAVASCRIPT DE FUNCIONALIDADES -->
    <script>
        // --- 1. MODO OSCURO (DARK MODE) CON PERSISTENCIA ---
        function initDarkMode() {
            const savedTheme = localStorage.getItem('ci4_theme');
            const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
            if (savedTheme === 'dark' || (!savedTheme && prefersDark)) {
                document.documentElement.classList.add('dark');
                updateDarkModeUI(true);
            } else {
                document.documentElement.classList.remove('dark');
                updateDarkModeUI(false);
            }
        }

        function toggleDarkMode() {
            const isDark = document.documentElement.classList.toggle('dark');
            localStorage.setItem('ci4_theme', isDark ? 'dark' : 'light');
            updateDarkModeUI(isDark);
        }

        function updateDarkModeUI(isDark) {
            const icon = document.getElementById('darkModeIcon');
            const text = document.getElementById('darkModeText');
            if (isDark) {
                icon.className = 'fa-solid fa-sun text-amber-400';
                text.textContent = 'Modo Claro';
            } else {
                icon.className = 'fa-solid fa-moon';
                text.textContent = 'Modo Oscuro';
            }
        }

        // --- 2. CONTADOR DE VISITAS LOCALES ---
        function updateVisitCounter() {
            let visits = parseInt(localStorage.getItem('ci4_visits') || '0') + 1;
            localStorage.setItem('ci4_visits', visits);
            document.getElementById('visitCount').textContent = visits;
        }

        // --- 3. COPIAR AL PORTAPAPELES ---
        function copyToClipboard(text, buttonEl) {
            const tempInput = document.createElement('textarea');
            tempInput.value = text;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand('copy');
            document.body.removeChild(tempInput);

            // Retroalimentación visual
            const originalHTML = buttonEl.innerHTML;
            buttonEl.innerHTML = '<i class="fa-solid fa-check text-green-500"></i>';
            setTimeout(() => {
                buttonEl.innerHTML = originalHTML;
            }, 1500);
        }

        // --- 4. BUSCADOR EN TIEMPO REAL ---
        function filterCards() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const cards = document.querySelectorAll('.card-item');
            let visibleCount = 0;

            cards.forEach(card => {
                const text = card.textContent.toLowerCase();
                if (text.includes(query)) {
                    card.style.display = 'flex';
                    visibleCount++;
                } else {
                    card.style.display = 'none';
                }
            });

            document.getElementById('searchStats').textContent = `Mostrando ${visibleCount} de ${cards.length} tarjetas`;
        }

        // --- 5. GENERADOR DE PLANTILLAS DE CÓDIGO (CODE SNIPPET BUILDER) ---
        const snippets = {
            rest: `<?php

namespace App\\Controllers;

use CodeIgniter\\RESTful\\ResourceController;

class ProductsController extends ResourceController
{
    protected $modelName = 'App\\Models\\ProductModel';
    protected $format    = 'json';

    public function index()
    {
        return $this->respond($this->model->findAll());
    }

    public function show($id = null)
    {
        $data = $this->model->find($id);
        if (!$data) return $this->failNotFound('Producto no encontrado');
        return $this->respond($data);
    }
}`,
            filter: `<?php

namespace App\\Filters;

use CodeIgniter\\Filters\\FilterInterface;
use CodeIgniter\\HTTP\\RequestInterface;
use CodeIgniter\\HTTP\\ResponseInterface;

class AuthFilter implements FilterInterface
{
    public function before(RequestInterface $request, $arguments = null)
    {
        if (! session()->get('isLoggedIn')) {
            return redirect()->to('/login');
        }
    }

    public function after(RequestInterface $request, ResponseInterface $response, $arguments = null)
    {
        // Lógica posterior a la respuesta
    }
}`,
            model: `<?php

namespace App\\Models;

use CodeIgniter\\Model;

class ProductModel extends Model
{
    protected $table            = 'products';
    protected $primaryKey       = 'id';
    protected $allowedFields    = ['name', 'price', 'sku', 'created_at'];
    protected $useTimestamps     = true;
}`,
            routes: `<?php

use CodeIgniter\\Router\\RouteCollection;

/**
 * @var RouteCollection $routes
 */
$routes->get('/', 'Home::index');

$routes->group('api/v1', ['namespace' => 'App\\Controllers'], static function ($routes) {
    $routes->resource('products', ['controller' => 'ProductsController']);
});`
        };

        let activeSnippetKey = 'rest';

        function selectSnippet(key) {
            activeSnippetKey = key;
            document.getElementById('snippetCode').textContent = snippets[key];

            // Actualizar pestañas
            document.querySelectorAll('.snippet-tab').forEach(btn => {
                btn.className = 'snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-slate-100 dark:bg-slate-700 text-slate-600 dark:text-slate-300 hover:bg-slate-200 transition-all';
            });

            const activeBtn = document.getElementById(`tab-${key}`);
            if (activeBtn) {
                activeBtn.className = 'snippet-tab px-4 py-2 rounded-xl text-xs font-semibold bg-blue-600 text-white transition-all';
            }
        }

        function copySnippet() {
            const codeText = snippets[activeSnippetKey];
            copyToClipboard(codeText, event.currentTarget);
        }

        // --- 6. SIMULADOR DE PRUEBAS RÁPIDAS ---
        function runTest(type) {
            const logsContainer = document.getElementById('testLogs');
            const emptyText = document.getElementById('emptyLogText');
            if (emptyText) emptyText.remove();

            const timestamp = new Date().toLocaleTimeString();
            let title = '';
            let details = '';
            let statusClass = '';

            switch (type) {
                case 'db':
                    title = 'Conexión BD (MySQL/PostgreSQL)';
                    details = 'Respuesta en 12ms. Tablas verificadas: 8.';
                    statusClass = 'border-l-4 border-green-500 bg-green-50 dark:bg-green-900/20';
                    break;
                case 'api':
                    title = 'Endpoint REST API JSON';
                    details = 'HTTP STATUS 200 OK. Content-Type: application/json';
                    statusClass = 'border-l-4 border-emerald-500 bg-emerald-50 dark:bg-emerald-900/20';
                    break;
                case 'mail':
                    title = 'Prueba SMTP Mailer';
                    details = 'Mensaje encolado correctamente en memoria local.';
                    statusClass = 'border-l-4 border-amber-500 bg-amber-50 dark:bg-amber-900/20';
                    break;
            }

            const logItem = document.createElement('div');
            logItem.className = `p-3 rounded-lg text-xs flex items-center justify-between transition-all ${statusClass}`;
            logItem.innerHTML = `
                <div>
                    <span class="font-bold">${title}</span>
                    <p class="text-slate-600 dark:text-slate-400 mt-0.5">${details}</p>
                </div>
                <span class="text-[10px] text-slate-400 font-mono pl-2">${timestamp}</span>
                `;

            logsContainer.prepend(logItem);
        }

        function clearLogs() {
            const logsContainer = document.getElementById('testLogs');
            logsContainer.innerHTML = '<p id="emptyLogText" class="text-xs text-slate-400 italic">No hay pruebas ejecutadas en esta sesión.</p>';
        }
          initDarkMode();
            updateVisitCounter();
            selectSnippet('rest'); // Inicializar snippet por defecto
        };
    </script>
</body>
</html>
        // --- INICIALIZACIÓN AL CARGAR LA PÁGINA ---
        window.onload = function() {
