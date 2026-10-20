<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Portal de Desarrollo | CodeIgniter 4</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="shortcut icon" type="image/x-icon" href="/favicon.ico">

    <style>
        :root {
            --bg-dark: #0f172a;
            --bg-card: #1e293b;
            --bg-hover: #334155;
            --accent: #f97316;
            --accent-glow: rgba(249, 115, 22, 0.25);
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --border-color: #334155;
            --font-mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: background-color 0.2s ease, border-color 0.2s ease;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-primary);
            font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* HEADER & SEARCH */
        header {
            background-color: var(--bg-card);
            border-bottom: 1px solid var(--border-color);
            padding: 2.5rem 1.5rem;
            text-align: center;
            position: relative;
        }

        .header-content {
            max-width: 700px;
            margin: 0 auto;
        }

        .logo-title {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.75rem;
            margin-bottom: 0.75rem;
        }

        .logo-title svg {
            height: 36px;
        }

        .logo-title h1 {
            font-size: 1.75rem;
            font-weight: 700;
        }

        .tagline {
            color: var(--text-secondary);
            font-size: 1rem;
            margin-bottom: 1.5rem;
        }

        .search-box {
            position: relative;
            max-width: 500px;
            margin: 0 auto;
        }

        .search-box input {
            width: 100%;
            padding: 0.85rem 1rem 0.85rem 2.75rem;
            background-color: var(--bg-dark);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            color: var(--text-primary);
            font-size: 0.95rem;
            outline: none;
        }

        .search-box input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }

        .search-icon {
            position: absolute;
            left: 0.9rem;
            top: 50%;
            transform: translateY(-50%);
            fill: var(--text-secondary);
            width: 18px;
            height: 18px;
        }

        /* CONTAINER & LAYOUT */
        .container {
            max-width: 1000px;
            margin: 2rem auto;
            padding: 0 1.5rem;
            flex: 1;
            width: 100%;
        }

        .info-pills {
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
            margin-bottom: 2rem;
        }

        .pill {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            padding: 0.5rem 1.25rem;
            border-radius: 50px;
            font-size: 0.875rem;
            color: var(--text-secondary);
        }

        .pill span {
            color: var(--accent);
            font-weight: 600;
        }

        /* ACCORDION / SECTIONS */
        .section-title {
            font-size: 1.25rem;
            margin-bottom: 1rem;
            color: var(--text-primary);
        }

        .accordion {
            display: flex;
            flex-direction: column;
            gap: 0.75rem;
            margin-bottom: 2.5rem;
        }

        .accordion-item {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            overflow: hidden;
        }

        .accordion-header {
            width: 100%;
            padding: 1rem 1.25rem;
            background: none;
            border: none;
            color: var(--text-primary);
            text-align: left;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .accordion-header:hover {
            background-color: var(--bg-hover);
        }

        .accordion-content {
            display: none;
            padding: 1rem 1.25rem;
            border-top: 1px solid var(--border-color);
            background-color: rgba(15, 23, 42, 0.5);
            font-size: 0.925rem;
            color: var(--text-secondary);
        }

        .accordion-content.show {
            display: block;
        }

        .code-block {
            background-color: var(--bg-dark);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 0.75rem 1rem;
            font-family: var(--font-mono);
            color: var(--accent);
            font-size: 0.875rem;
            margin-top: 0.5rem;
        }

        /* LINKS GRID */
        .resources-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1rem;
        }

        .resource-card {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 1.25rem;
            text-decoration: none;
            color: var(--text-primary);
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .resource-card:hover {
            border-color: var(--accent);
            transform: translateY(-2px);
        }

        .resource-card h4 {
            color: var(--accent);
            font-size: 1rem;
        }

        .resource-card p {
            font-size: 0.875rem;
            color: var(--text-secondary);
        }

        /* FOOTER */
        footer {
            background-color: var(--bg-card);
            border-top: 1px solid var(--border-color);
            padding: 1.5rem;
            text-align: center;
            font-size: 0.875rem;
            color: var(--text-secondary);
        }
    </style>
</head>
<body>

    <!-- HEADER -->
    <header>
        <div class="header-content">
            <div class="logo-title">
                <svg viewBox="0 0 2100 500" height="32"><path fill="#f97316" d="M148.2 411c-20.53-9.07-34.48-28.61-36.31-50.99 1.2-23.02 13.36-44.06 32.67-56.61-3.17 7.73-2.4 16.53 2 23.6 5.01 7 13.63 10.36 22.07 8.61 12.02-3.38 19.06-15.86 15.68-27.89-1.2-4.21-3.6-8.03-6.88-10.91-13.6-11.06-20.43-28.44-18-45.81 2.33-9.2 7.42-17.52 14.61-23.8-5.4 14.4 9.83 28.61 20.05 35.6 18.14 10.88 35.6 22.84 52.32 35.81 18.27 14.4 28.23 36.94 26.67 60-4.11 24.54-21.47 44.8-45.13 52.4 47.33-10.53 96.13-48.13 97.06-101.46-.93-42.67-26.4-80.96-65.33-98.4h-1.73c.86 2.09 1.28 4.34 1.2 6.61.13-1.47.13-2.93 0-4.4.21 1.73.21 3.47 0 5.2-2.96 12.13-15.2 19.6-27.36 16.64-4.86-1.2-9.2-3.93-12.32-7.87-15.6-20 0-42.76 2.61-64.76 1.6-28.13-11.25-55.02-34.05-71.46 11.41 19.02-3.79 44-14.84 58.21-11.07 14.21-27.07 24.8-40.11 37.2-14.05 13.07-26.93 27.44-38.49 42.8-24.99 30.53-34.8 70.8-26.67 109.4 11.15 37.2 42.07 65.15 80.2 72.4h.21l-.13-.12Zm324.56-159.8q0-17.92 6.16-35.56 6.44-17.92 18.48-31.92t29.68-22.68q17.64-8.96 40.04-8.96 26.6 0 45.36 12.04 19.04 12.04 28 31.36l-15.4 9.52q-4.76-9.8-11.76-16.52-6.72-6.72-14.56-10.92-7.84-4.2-16.24-5.88-8.4-1.96-16.52-1.96-17.92 0-31.64 7.28-13.72 7.28-23.24 19.04-9.24 11.76-14 26.6-4.76 14.56-4.76 29.68 0 16.52 5.6 31.64 5.88 15.12 15.68 26.88 10.08 11.48 23.52 18.48 13.72 6.72 29.68 6.72 8.4 0 17.08-1.96 8.96-2.24 17.08-6.72 8.4-4.76 15.4-11.48 7-7 11.76-16.8l16.24 8.4q-4.76 11.2-13.44 19.88-8.68 8.4-19.32 14.28-10.64 5.88-22.68 8.96-11.76 3.08-23.24 3.08-20.44 0-37.52-8.96-17.08-8.96-29.4-23.24-12.32-14.56-19.32-32.76-6.72-18.48-6.72-37.52Zm263.48 103.6q-15.96 0-29.12-5.88-13.16-6.16-22.96-16.52-9.52-10.36-14.84-24.08Q664 294.6 664 279.48q0-15.4 5.32-29.12 5.6-13.72 15.12-24.08 9.8-10.36 22.96-16.52t28.84-6.16q15.68 0 28.84 6.16 13.44 6.16 22.96 16.52 9.8 10.36 15.12 24.08 5.6 13.72 5.6 29.12 0 15.12-5.32 28.84t-15.12 24.08q-9.52 10.36-22.96 16.52-13.16 5.88-29.12 5.88Zm-52.92-75.04q0 12.32 4.2 22.96 4.2 10.36 11.2 18.48 7.28 7.84 16.8 12.32 9.8 4.48 20.72 4.48 10.92 0 20.44-4.48 9.8-4.76 17.08-12.6 7.28-8.12 11.48-18.76 4.2-10.64 4.2-22.96 0-12.04-4.2-22.68-4.2-10.92-11.48-18.76-7.28-8.12-17.08-12.6-9.52-4.76-20.44-4.76-10.92 0-20.44 4.76-9.52 4.48-16.8 12.6-7.28 8.12-11.48 19.04-4.2 10.64-4.2 22.96ZM900.6 354.8q-15.12 0-28-6.16-12.88-6.44-22.12-16.8t-14.56-23.8q-5.04-13.72-5.04-28.56 0-15.4 5.04-29.12 5.04-14 13.72-24.36 8.96-10.36 21-16.24 12.32-6.16 26.88-6.16 18.48 0 32.76 9.8 14.28 9.52 22.4 23.24V147.6h19.04v179.76q0 7.84 6.72 7.84V352q-4.2.84-6.72.84-6.72 0-11.76-4.2-5.04-4.48-5.04-10.64v-14.28Q946.24 338 931.4 346.4t-30.8 8.4Zm4.2-16.8q7 0 14.84-2.8 8.12-2.8 15.12-7.56 7-5.04 11.76-11.48 5.04-6.72 6.16-14.28V256.8q-2.8-7.56-8.12-14-5.32-6.72-12.32-11.76-6.72-5.04-14.56-7.84-7.84-2.8-15.4-2.8-11.76 0-21.28 5.04-9.52 5.04-16.52 13.44-6.72 8.12-10.36 18.76-3.64 10.64-3.64 21.84 0 11.76 4.2 22.4 4.2 10.64 11.48 18.76 7.28 7.84 17.08 12.6Q893.32 338 904.8 338Zm173.04 16.8q-15.96 0-29.4-5.88-13.16-6.16-22.96-16.52-9.8-10.64-15.4-24.36-5.32-13.72-5.32-29.4 0-15.4 5.32-28.84 5.6-13.72 15.12-23.8 9.8-10.36 23.24-16.24 13.44-6.16 29.12-6.16 15.96 0 29.12 6.16 13.44 5.88 22.96 16.24 9.52 10.36 14.84 23.8 5.32 13.44 5.32 28.56v4.48q0 2.24-.28 3.08h-124.88q.84 11.76 5.32 21.84 4.76 9.8 12.04 17.08 7.28 7.28 16.52 11.48 9.52 3.92 20.16 3.92 7 0 14-1.96t12.88-5.32q5.88-3.36 10.64-8.12 4.76-5.04 7.28-10.92l16.52 4.48q-3.36 8.12-9.52 14.84-6.16 6.44-14.28 11.48-8.12 4.76-17.92 7.56-9.8 2.52-20.44 2.52Zm-53.48-83.44h107.24q-.84-11.76-5.6-21.28-4.48-9.8-11.76-16.8-7-7-16.52-10.92-9.24-3.92-19.88-3.92-10.64 0-20.16 3.92t-16.8 10.92q-7 7-11.48 16.8-4.2 9.8-5.04 21.28Zm193.2 80.64h-38.64V153.2h38.64V352Zm93.52.84q-14.84 0-26.88-5.88t-21-15.96q-8.68-10.36-13.44-23.8-4.76-13.44-4.76-28.56 0-15.96 5.04-29.68 5.04-13.72 14-24.08 8.96-10.36 21.56-16.24 12.6-5.88 27.72-5.88 17.08 0 29.96 7.84 12.88 7.56 21.28 20.44v-25.76h32.76V345q0 16.24-6.16 29.12-6.16 12.88-17.08 21.84-10.64 8.96-25.76 13.72-14.84 4.76-32.48 4.76-24.08 0-40.6-7.84-16.24-8.12-28-22.68l20.44-19.88q8.4 10.36 21 16.24 12.88 5.88 27.16 5.88 8.68 0 16.52-2.24 8.12-2.52 14.28-7.56 6.16-5.04 9.52-12.88 3.64-7.84 3.64-18.48v-18.48q-7.28 12.6-20.44 19.6-13.16 6.72-28.28 6.72Zm12.6-29.96q6.16 0 11.76-1.96t10.36-5.32q4.76-3.36 8.4-7.84 3.64-4.48 5.6-9.52v-35q-5.04-12.88-15.96-20.72-10.64-7.84-22.4-7.84-8.68 0-15.68 3.92-7 3.64-12.04 10.08-5.04 6.16-7.84 14.28-2.52 8.12-2.52 16.8 0 8.96 3.08 16.8t8.4 13.72q5.6 5.88 12.88 9.24 7.28 3.36 15.96 3.36Zm243.88-62.44V352h-37.52v-82.32q0-17.64-6.16-25.76-6.16-8.12-17.08-8.12-5.6 0-11.48 2.24-5.88 2.24-11.2 6.44-5.04 3.92-9.24 9.52t-6.16 12.32V352h-37.52V205.28h33.88v27.16q8.12-14 23.52-21.84t34.72-7.84q13.72 0 22.4 5.04 8.68 5.04 13.44 13.16 4.76 8.12 6.44 18.48 1.96 10.36 1.96 21Zm70.28 91.56h-37.52V205.28h37.52V352Zm0-167.16h-37.52V147.6h37.52v37.24Zm114.24 129.92 7.56 29.68q-7.56 3.36-18.48 6.72-10.92 3.36-22.96 3.36-7.84 0-14.84-1.96-6.72-1.96-12.04-6.16-5.04-4.48-8.12-11.2-3.08-7-3.08-16.8v-84.28h-19.32v-28.84h19.32v-47.6h37.52v47.6h30.8v28.84h-30.8v71.68q0 7.84 3.92 11.2 4.2 3.08 10.08 3.08t11.48-1.96q5.6-1.96 8.96-3.36Zm91.56 40.04q-17.64 0-31.92-5.88-14.28-6.16-24.36-16.52t-15.68-24.08q-5.32-13.72-5.32-28.84 0-15.68 5.32-29.4 5.32-14 15.4-24.36 10.08-10.64 24.36-16.8 14.56-6.16 32.48-6.16 17.92 0 31.92 6.16 14.28 6.16 24.08 16.52 10.08 10.36 15.12 24.08 5.32 13.72 5.32 28.56 0 3.64-.28 7 0 3.36-.56 5.6h-113.4q.84 8.68 4.2 15.4 3.36 6.72 8.68 11.48 5.32 4.76 12.04 7.28 6.72 2.52 14 2.52 11.2 0 21-5.32 10.08-5.6 13.72-14.56l32.2 8.96q-8.12 16.8-26.04 27.72-17.64 10.64-42.28 10.64Zm-38.08-88.48h76.16q-1.4-16.52-12.32-26.32-10.64-10.08-26.04-10.08-7.56 0-14.28 2.8-6.44 2.52-11.48 7.28t-8.4 11.48q-3.08 6.72-3.64 14.84Zm225.12-62.72v34.16q-17.08.28-30.52 6.72-13.44 6.16-19.32 18.76V352h-37.52V205.28h34.44v31.36q3.92-7.56 9.24-13.44 5.32-6.16 11.48-10.64t12.32-6.72q6.44-2.52 12.32-2.52h4.48q1.68 0 3.08.28Z"/></svg>
                <h1>Portal del Desarrollador</h1>
            </div>
            <p class="tagline">Guía rápida de archivos y rutas para comenzar tu proyecto en CodeIgniter 4</p>
            
            <div class="search-box">
                <svg class="search-icon" viewBox="0 0 24 24"><path d="M9.5 3A6.5 6.5 0 0116 9.5c0 1.61-.59 3.09-1.56 4.23l.27.27h.79l5 5-1.5 1.5-5-5v-.79l-.27-.27A6.516 6.516 0 019.5 16 6.5 6.5 0 013 9.5 6.5 6.5 0 019.5 3m0 2C7 5 5 7 5 9.5S7 14 9.5 14 14 12 14 9.5 12 5 9.5 5z"/></svg>
                <input type="text" id="filterInput" placeholder="Buscar rutas, controladores o vistas...">
            </div>
        </div>
    </header>

    <!-- CONTENT -->
    <div class="container">
        
        <!-- SYSTEM METRICS -->
        <div class="info-pills">
            <div class="pill">Versión: <span>v<?= CodeIgniter\CodeIgniter::CI_VERSION ?></span></div>
            <div class="pill">Entorno: <span><?= ENVIRONMENT ?></span></div>
            <div class="pill">Tiempo de Carga: <span>{elapsed_time} s</span></div>
            <div class="pill">Memoria: <span>{memory_usage} MB</span></div>
        </div>

        <!-- ACCORDIONS / ARCHIVOS -->
        <h3 class="section-title">Estructura Base</h3>
        <div class="accordion">
            <div class="accordion-item">
                <button class="accordion-header">
                    <span>📄 Vista de Bienvenida</span>
                    <small>app/Views/welcome_message.php</small>
                </button>
                <div class="accordion-content">
                    Este archivo genera la interfaz visual que estás viendo. Puedes editarlo o crear nuevas vistas dentro de la carpeta <code>app/Views/</code>.
                    <div class="code-block">&lt;?=$this-&gt;extend('layout/main')?&gt;</div>
                </div>
            </div>

            <div class="accordion-item">
                <button class="accordion-header">
                    <span>🎮 Controlador Principal</span>
                    <small>app/Controllers/Home.php</small>
                </button>
                <div class="accordion-content">
                    Gestiona la lógica que carga esta página. Es la clase PHP encargada de procesar las peticiones HTTP y retornar la vista correspondiente.
                    <div class="code-block">return view('welcome_message');</div>
                </div>
            </div>

            <div class="accordion-item">
                <button class="accordion-header">
                    <span>🗺️ Configuración de Rutas</span>
                    <small>app/Config/Routes.php</small>
                </button>
                <div class="accordion-content">
                    Define las URLs públicas de tu aplicación y qué controlador debe responder a cada endpoint.
                    <div class="code-block">$routes->get('/', 'Home::index');</div>
                </div>
            </div>
        </div>

        <!-- EXTERNAL RESOURCES -->
        <h3 class="section-title">Recursos Oficiales</h3>
        <div class="resources-grid">
            <a href="https://codeigniter.com/user_guide/" target="_blank" class="resource-card">
                <h4>Documentación Oficial</h4>
                <p>Manual completo con ejemplos de bases de datos, validaciones y migraciones.</p>
            </a>
            <a href="https://forum.codeigniter.com/" target="_blank" class="resource-card">
                <h4>Foro de la Comunidad</h4>
                <p>Espacio para hacer preguntas, compartir código y colaborar con otros desarrolladores.</p>
            </a>
            <a href="https://codeigniter.com/contribute" target="_blank" class="resource-card">
                <h4>Contribuir en GitHub</h4>
                <p>Reporta fallos o aporta mejoras directamente al repositorio oficial del framework.</p>
            </a>
        </div>

    </div>

    <!-- FOOTER -->
    <footer>
        <p>&copy; <?= date('Y') ?> CodeIgniter Foundation. Proyecto Open Source bajo licencia MIT.</p>
    </footer>

    <!-- SCRIPT INTERACTIVO -->
    <script>
        // JS para los acordeones
        document.querySelectorAll('.accordion-header').forEach(button => {
            button.addEventListener('click', () => {
                const content = button.nextElementSibling;
                content.classList.toggle('show');
            });
        });

        // JS para filtrar elementos
        document.getElementById('filterInput').addEventListener('keyup', function() {
            let filter = this.value.toLowerCase();
            let items = document.querySelectorAll('.accordion-item, .resource-card');

            items.forEach(item => {
                let text = item.textContent.toLowerCase();
                item.style.display = text.includes(filter) ? '' : 'none';
            });
        });
    </script>
</body>
</html>
