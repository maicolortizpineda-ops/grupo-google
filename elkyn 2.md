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
            gap: 0.5rem;
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
            font-weight: 60
