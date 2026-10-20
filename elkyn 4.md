<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>CodeIgniter 4 | Sci-Fi Dev Console</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="shortcut icon" type="image/x-icon" href="/favicon.ico">

    <style>
        :root {
            --bg-deep: #090d16;
            --accent-cyan: #00f2fe;
            --accent-purple: #7928ca;
            --accent-pink: #ff0080;
            --accent-green: #00ff87;
            --glass-bg: rgba(15, 23, 42, 0.65);
            --glass-border: rgba(255, 255, 255, 0.12);
            --glass-glow: rgba(0, 242, 254, 0.15);
            --text-primary: #f8fafc;
            --text-secondary: #94a3b8;
            --font-mono: "Fira Code", Monaco, Consolas, "Courier New", monospace;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
        }

        body {
            background-color: var(--bg-deep);
            color: var(--text-primary);
            font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 2rem 1rem;
            position: relative;
            overflow-x: hidden;
        }

        /* Luces de fondo (Aura Orbs) */
        .orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(100px);
            opacity: 0.35;
            z-index: 0;
            pointer-events: none;
        }
        .orb-1 { width: 400px; height: 400px; background: var(--accent-purple); top: -100px; left: -100px; }
        .orb-2 { width: 450px; height: 450px; background: var(--accent-cyan); bottom: -150px; right: -100px; }
        .orb-3 { width: 300px; height: 300px; background: var(--accent-pink); top: 40%; left: 60%; }

        /* Contenedor Glassmorphic */
        .hud-container {
            position: relative;
            z-index: 10;
            width: 100%;
            max-width: 950px;
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 2.5rem;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6), 0 0 30px var(--glass-glow);
        }

        /* Header */
        .hud-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 1.5rem;
            padding-bottom: 2rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .brand-group {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .brand-logo {
            width: 48px;
            height: 48px;
            background: linear-gradient(135deg, var(--accent-pink), var(--accent-purple));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 20px rgba(255, 0, 128, 0.4);
        }

        .brand-logo svg {
            width: 28px;
            height: 28px;
            fill: #fff;
        }

        .brand-title h1 {
            font-size: 1.6rem;
            font-weight: 800;
            background: linear-gradient(90deg, #fff, var(--accent-cyan));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            letter-spacing: -0.02em;
        }

        .brand-title p {
            font-size: 0.85rem;
            color: var(--text-secondary);
        }

        .status-pill {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            background: rgba(0, 255, 135, 0.1);
            border: 1px solid rgba(0, 255, 135, 0.3);
            color: var(--accent-green);
            padding: 0.5rem 1rem;
            border-radius: 999px;
            font-size: 0.8rem;
            font-weight: 600;
            letter-spacing: 0.05em;
            text-transform: uppercase;
        }

        .pulse-dot {
            width: 8px;
            height: 8px;
            background-color: var(--accent-green);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--accent-green);
            animation: pulse 1.8s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(0, 255, 135, 0.7); }
            70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(0, 255, 135, 0); }
            100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(0, 255, 135, 0); }
        }

        /* Metrics HUD Grid */
        .hud-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1.25rem;
            margin: 2rem 0;
        }

        .metric-tile {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 16px;
            padding: 1.25rem;
            position: relative;
            overflow: hidden;
        }

        .metric-tile::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--accent-cyan), transparent);
        }

        .metric-tile label {
            display: block;
            font-size: 0.75rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.08em;
            margin-bottom: 0.4rem;
        }

        .metric-tile val {
            display: block;
            font-size: 1.4rem;
            font-weight: 700;
            font-family: var(--font-mono);
            color: var(--text-primary);
        }

        /* File Cards Section */
        .section-title {
            font-size: 0.95rem;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            color: var(--accent-cyan);
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .section-title .badge-count {
            font-size: 0.75rem;
            background: rgba(0, 242, 254, 0.1);
            border: 1px solid rgba(0, 242, 254, 0.3);
            color: var(--accent-cyan);
            padding: 0.2rem 0.6rem;
            border-radius: 6px;
        }

        .file-list {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .file-item {
            background: rgba(15, 23, 42, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 12px;
            padding: 1rem 1.25rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 0.75rem;
        }

        .file-info {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .file-tag {
            background: rgba(0, 242, 254, 0.15);
            color: var(--accent-cyan);
            font-size: 0.75rem;
            font-weight: 700;
            padding: 0.25rem 0.6rem;
            border-radius: 6px;
            text-transform: uppercase;
        }

        .file-tag.model {
            background: rgba(255, 0, 128, 0.15);
            color: var(--accent-pink);
        }

        .file-path {
            font-family: var(--font-mono);
            font-size: 0.875rem;
            color: #e2e8f0;
        }

        .copy-btn {
            background: transparent;
            border: 1px solid rgba(255, 255, 255, 0.15);
            color: var(--text-secondary);
            padding: 0.4rem 0.8rem;
            border-radius: 8px;
            font-size: 0.75rem;
            cursor: pointer;
            font-weight: 600;
        }

        .copy-btn:hover {
            background: var(--accent-cyan);
            border-color: var(--accent-cyan);
            color: #000;
            box-shadow: 0 0 15px rgba(0, 242, 254, 0.4);
        }

        /* Quick Action Bar */
        .action-bar {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1rem;
        }

        .action-card {
            background: linear-gradient(135deg, rgba(255,255,255,0.05) 0%, rgba(255,255,255,0.01) 100%);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 14px;
            padding: 1.25rem;
            text-decoration: none;
            color: var(--text-primary);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }

        .action-card:hover {
            transform: translateY(-3px);
            border-color: var(--accent-purple);
            box-shadow: 0 10px 25px rgba(121, 40, 202, 0.3);
        }

        .action-card h4 {
            font-size: 0.95rem;
            font-weight: 700;
            margin-bottom: 0.4rem;
        }

        .action-card p {
            font-size: 0.8rem;
            color: var(--text-secondary);
        }

        /* Footer */
        footer {
            margin-top: 2.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center;
            font-size: 0.8rem;
            color: var(--text-secondary);
        }
    </style>
</head>
<body>

    <!-- Luces de fondo -->
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>

    <div class="hud-container">
        <!-- HEADER -->
        <header class="hud-header">
            <div class="brand-group">
                <div class="brand-logo">
                    <svg viewBox="0 0 24 24"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>
                </div>
                <div class="brand-title">
                    <h1>CodeIgniter 4</h1>
                    <p>Sci-Fi Glassmorphism HUD Interface</p>
                </div>
            </div>
            <div class="status-pill">
                <span class="pulse-dot"></span>
                <?= ENVIRONMENT ?> MODE
            </div>
        </header>

        <!-- METRICAS EN TIEMPO REAL -->
        <div class="hud-grid">
            <div class="metric-tile">
                <label>Versión CI</label>
                <val>v<?= CodeIgniter\CodeIgniter::CI_VERSION ?></val>
            </div>
            <div class="metric-tile">
                <label>Tiempo Render</label>
                <val>{elapsed_time} s</val>
            </div>
            <div class="metric-tile">
                <label>Uso Memoria</label>
                <val>{memory_usage} MB</val>
            </div>
            <div class="metric-tile">
                <label>Motor PHP</label>
                <val>v<?= PHP_VERSION ?></val>
            </div>
        </div>

        <!-- LISTA DE ARCHIVOS DEL SISTEMA -->
        <div class="section-title">
            <span>⚡ Arquitectura de Archivos Activa</span>
            <span class="badge-count">4 Archivos</span>
        </div>

        <div class="file-list">
            <div class="file-item">
                <div class="file-info">
                    <span class="file-tag">View</span>
                    <span class="file-path" id="p1">app/Views/welcome_message.php</span>
                </div>
                <button class="copy-btn" onclick="copyText('p1', this)">Copiar Ruta</button>
            </div>

            <div class="file-item">
                <div class="file-info">
                    <span class="file-tag">Controller</span>
                    <span class="file-path" id="p2">app/Controllers/Home.php</span>
                </div>
                <button class="copy-btn" onclick="copyText('p2', this)">Copiar Ruta</button>
            </div>

            <div class="file-item">
                <div class="file-info">
                    <span class="file-tag model">Model</span>
                    <span class="file-path" id="p4">app/Models/UserModel.php</span>
                </div>
                <button class="copy-btn" onclick="copyText('p4', this)">Copiar Ruta</button>
            </div>

            <div class="file-item">
                <div class="file-info">
                    <span class="file-tag">Routes</span>
                    <span class="file-path" id="p3">app/Config/Routes.php</span>
                </div>
                <button class="copy-btn" onclick="copyText('p3', this)">Copiar Ruta</button>
            </div>
        </div>

        <!-- ACCIONES RÁPIDAS -->
        <div class="action-bar">
            <a href="https://codeigniter.com/user_guide/" target="_blank" class="action-card">
                <h4>📖 User Guide</h4>
                <p>Explora la documentación oficial y tutoriales de desarrollo.</p>
            </a>
            <a href="https://forum.codeigniter.com/" target="_blank" class="action-card">
                <h4>💬 Comunidad</h4>
                <p>Resuelve dudas e interactúa en los foros oficiales.</p>
            </a>
            <a href="https://github.com/codeigniter4/CodeIgniter4" target="_blank" class="action-card">
                <h4>🐙 Repositorio</h4>
                <p>Accede al código fuente y reporta issues en GitHub.</p>
            </a>
            <a href="http://localhost:8080/debugger" target="_blank" class="action-card" style="border-color: rgba(0, 242, 254, 0.3);">
                <h4>⚡ Debug Toolbar</h4>
                <p>Monitorea consultas SQL, logs y rendimiento en vivo.</p>
            </a>
        </div>

        <!-- FOOTER -->
        <footer>
            <p>&copy; <?= date('Y') ?> CodeIgniter Foundation. Renderizado dinámico en {elapsed_time} segundos.</p>
        </footer>
    </div>

    <script>
        function copyText(elementId, btn) {
            const text = document.getElementById(elementId).innerText;
            navigator.clipboard.writeText(text).then(() => {
                const originalText = btn.innerText;
                btn.innerText = '¡Copiado!';
                btn.style.background = 'var(--accent-green)';
                btn.style.color = '#000';
                setTimeout(() => {
                    btn.innerText = originalText;
                    btn.style.background = 'transparent';
                    btn.style.color = 'var(--text-secondary)';
                }, 1800);
            });
        }
    </script>

</body>
</html>
