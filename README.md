<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="color-scheme" content="only dark">
    <title id="page-title">MK CREATIVE AGENCY Web 2 | AI Assistant & Solutions</title>
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #38bdf8; 
            --accent-glow: rgba(56, 189, 248, 0.4);
            --glass: rgba(255, 255, 255, 0.03); 
            --text: #f8fafc;
            --text-muted: #94a3b8;
            --neon-blue: #00d4ff;
            --neon-purple: #b14aed;
        }

        body.matrix-mode {
            --bg-dark: #020d05;
            --accent: #22c55e;
            --accent-glow: rgba(34, 197, 94, 0.5);
            background: radial-gradient(circle at top right, #052e16, #020d05) !important;
        }

        body.amber-mode {
            --bg-dark: #120803;
            --accent: #f59e0b;
            --accent-glow: rgba(245, 158, 11, 0.5);
            background: radial-gradient(circle at top right, #2e1a05, #120803) !important;
        }
        
        * { box-sizing: border-box; margin: 0; padding: 0; scroll-behavior: smooth; color-scheme: dark; cursor: none; }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, var(--bg-dark)); 
            background-attachment: fixed;
            color: var(--text); 
            font-family: 'Cairo', 'Inter', sans-serif; 
            overflow-x: hidden;
            transition: background 0.5s ease;
            position: relative;
        }

        #particle-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        header, .hero, .container, footer, .floating-controls, .rocket-top-btn, .mobile-search-float, #search-modal { position: relative; z-index: 2; }

        .cursor-dot { position: fixed; width: 8px; height: 8px; background: var(--accent); border-radius: 50%; pointer-events: none; z-index: 99999; transform: translate(-50%, -50%); transition: transform 0.05s ease; }
        .cursor-outline { position: fixed; width: 32px; height: 32px; border: 2px solid var(--accent); border-radius: 50%; pointer-events: none; z-index: 99998; transform: translate(-50%, -50%); transition: width 0.2s, height 0.2s, border-color 0.2s; box-shadow: 0 0 15px var(--accent-glow); }

        #progress-bar { position: fixed; top: 0; left: 0; height: 4px; background: var(--accent); width: 0%; z-index: 1001; box-shadow: 0 0 12px var(--accent); }

        header { background: rgba(3, 7, 18, 0.85); backdrop-filter: blur(16px); position: fixed; width: 100%; top: 0; z-index: 1000; border-bottom: 1px solid rgba(56, 189, 248, 0.2); }
        .nav-container { max-width: 1200px; margin: auto; display: flex; justify-content: space-between; align-items: center; padding: 0.8rem 2rem; }
        .logo { font-weight: 800; color: var(--accent); font-size: 1.1rem; display: flex; align-items: center; gap: 10px; letter-spacing: 0.5px; }
        
        .hud-panel { display: flex; align-items: center; gap: 10px; font-size: 0.75rem; flex-wrap: wrap; }
        .network-ticker, .weather-ticker, .session-ticker { color: var(--accent); background: rgba(56, 189, 248, 0.08); padding: 5px 10px; border-radius: 12px; border: 1px solid rgba(56, 189, 248, 0.3); display: flex; align-items: center; gap: 5px; backdrop-filter: blur(8px); }

        .lang-select {
            background: rgba(56, 189, 248, 0.08);
            color: var(--accent);
            border: 1px solid rgba(56, 189, 248, 0.3);
            padding: 5px 10px;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.75rem;
            outline: none;
            transition: 0.3s;
            font-family: 'Cairo', sans-serif;
        }
        .lang-select option { background: #030712; color: #fff; }
        .lang-select:hover { background: rgba(56, 189, 248, 0.2); border-color: var(--accent); }

        .status-badge { font-size: 0.75rem; background: rgba(34, 197, 94, 0.15); color: #22c55e; border: 1px solid #22c55e; padding: 3px 10px; border-radius: 20px; display: inline-flex; align-items: center; gap: 6px; }
        .status-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; box-shadow: 0 0 8px #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.4; } 100% { opacity: 1; } }

        .nav-links { display: flex; align-items: center; gap: 15px; list-style: none; }
        .nav-links a { color: var(--text); text-decoration: none; font-size: 0.85rem; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        .activity-ticker-bar { background: rgba(56, 189, 248, 0.06); border-bottom: 1px solid rgba(56, 189, 248, 0.15); padding: 8px 0; font-size: 0.82rem; color: var(--accent); overflow: hidden; white-space: nowrap; margin-top: 65px; }
        .ticker-content { display: inline-block; animation: tickerScroll 30s linear infinite; }
        @keyframes tickerScroll { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        .hero { padding: 90px 20px 50px; text-align: center; position: relative; }
        h1 { font-size: 3.2rem; font-weight: 800; background: linear-gradient(to right, #38bdf8, #818cf8, #34d399); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 15px; }
        
        .typed-text { color: var(--accent); border-right: 2px solid var(--accent); padding-right: 5px; animation: blink 0.7s infinite; }
        @keyframes blink { 50% { border-color: transparent; } }

        .vibe-ticker { font-size: 0.85rem; color: var(--text-muted); margin-top: 15px; display: inline-flex; align-items: center; gap: 8px; background: var(--glass); padding: 8px 18px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.06); backdrop-filter: blur(10px); }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; max-width: 950px; margin: 40px auto 0; }
        .stat-card { background: var(--glass); padding: 22px; border-radius: 18px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(12px); transition: 0.3s; }
        .stat-card:hover { border-color: var(--accent); box-shadow: 0 0 20px var(--accent-glow); }
        .stat-number { font-size: 2.4rem; font-weight: 800; color: var(--accent); }
        .stat-label { font-size: 0.85rem; color: var(--text-muted); margin-top: 5px; }

        .container { max-width: 1150px; margin: auto; padding: 60px 20px; opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
        .container.visible { opacity: 1; transform: translateY(0); }
        
        .section-title { font-size: 2.2rem; font-weight: 800; margin-bottom: 25px; border-bottom: 2px solid var(--accent); display: inline-block; padding-bottom: 6px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
        
        .card { background: var(--glass); padding: 30px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(16px); transition: 0.4s cubic-bezier(0.16, 1, 0.3, 1); position: relative; overflow: hidden; cursor: pointer; }
        .card:hover { transform: translateY(-8px); border-color: var(--accent); box-shadow: 0 0 30px var(--accent-glow); }

        .cert-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 25px; margin-top: 25px; }
        .cert-card { background: var(--glass); border-radius: 20px; overflow: hidden; border: 1px solid rgba(255,255,255,0.08); padding: 20px; backdrop-filter: blur(12px); transition: 0.3s; text-align: center; display: flex; flex-direction: column; justify-content: space-between; }
        .cert-card:hover { border-color: var(--accent); box-shadow: 0 0 25px var(--accent-glow); transform: translateY(-5px); }
        .cert-card img { width: 100%; height: 210px; object-fit: cover; border-radius: 12px; cursor: pointer; border: 1px solid rgba(255,255,255,0.1); transition: 0.3s; }
        .cert-card img:hover { transform: scale(1.03); }

        /* تصميم المساعد الذكي MK Assistant Bot المتطور والمطابق لصورتك */
        .assistant-section-container {
            max-width: 900px;
            margin: auto;
            background: linear-gradient(135deg, rgba(15, 23, 42, 0.95), rgba(3, 7, 18, 0.98));
            border: 2px solid var(--accent);
            border-radius: 28px;
            padding: 30px;
            box-shadow: 0 0 40px var(--accent-glow);
            backdrop-filter: blur(20px);
        }
        .assistant-box-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid rgba(56, 189, 248, 0.2);
            padding-bottom: 15px;
            margin-bottom: 20px;
        }
        .chat-messages-area {
            height: 380px;
            overflow-y: auto;
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid rgba(56, 189, 248, 0.2);
            border-radius: 18px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 20px;
            scroll-behavior: smooth;
        }
        .chat-msg {
            max-width: 80%;
            padding: 12px 18px;
            border-radius: 16px;
            font-size: 0.95rem;
            line-height: 1.6;
        }
        .chat-msg.bot {
            background: rgba(56, 189, 248, 0.1);
            border: 1px solid rgba(56, 189, 248, 0.3);
            color: var(--text);
            align-self: flex-start;
            border-top-left-radius: 4px;
        }
        .chat-msg.user {
            background: var(--accent);
            color: #030712;
            align-self: flex-end;
            font-weight: 600;
            border-top-right-radius: 4px;
        }
        .chat-input-row {
            display: flex;
            gap: 12px;
        }
        .chat-input {
            flex: 1;
            padding: 14px 20px;
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-radius: 14px;
            color: white;
            outline: none;
            font-size: 0.95rem;
            font-family: 'Cairo', sans-serif;
        }
        .chat-input:focus {
            border-color: var(--accent);
            box-shadow: 0 0 15px var(--accent-glow);
        }
        .chat-quick-chips {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }
        .chip-btn {
            background: rgba(56, 189, 248, 0.08);
            border: 1px solid rgba(56, 189, 248, 0.3);
            color: var(--accent);
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 0.8rem;
            cursor: pointer;
            transition: 0.3s;
        }
        .chip-btn:hover {
            background: var(--accent);
            color: #030712;
        }

        .btn { display: inline-flex; align-items: center; gap: 10px; padding: 12px 24px; margin: 6px; background: var(--accent); color: #030712; text-decoration: none; border-radius: 50px; font-weight: 800; transition: 0.3s; cursor: pointer; border: none; box-shadow: 0 0 15px var(--accent-glow); font-size: 0.9rem; }
        .btn:hover { transform: scale(1.06); box-shadow: 0 0 25px var(--accent); }
        .btn-outline { background: transparent; border: 2px solid var(--accent); color: var(--accent); box-shadow: none; }
        .btn-outline:hover { background: var(--accent); color: #030712; }

        .floating-controls { position: fixed; bottom: 30px; left: 30px; display: flex; flex-direction: column; gap: 14px; z-index: 1000; }
        .float-btn { width: 50px; height: 50px; background: var(--accent); border-radius: 50%; border: none; cursor: pointer; display: flex; justify-content: center; align-items: center; color: #030712; font-size: 1.2rem; box-shadow: 0 0 20px var(--accent-glow); transition: 0.3s; }
        .float-btn:hover { transform: scale(1.15) rotate(10deg); }

        .rocket-top-btn {
            position: fixed; bottom: 30px; left: 95px;
            background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
            color: white; border: none; width: 50px; height: 50px; border-radius: 50%;
            cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 22px;
            box-shadow: 0 0 20px rgba(0,212,255,0.4); z-index: 1000;
            opacity: 0; visibility: hidden; transition: all 0.3s ease;
        }
        .rocket-top-btn.show { opacity: 1; visibility: visible; }
        .rocket-top-btn:hover { transform: scale(1.15); }

        .mobile-search-float {
            position: fixed; bottom: 30px; left: 160px;
            background: var(--accent); color: #030712; border: none; width: 50px; height: 50px; border-radius: 50%;
            cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 20px;
            box-shadow: 0 0 20px var(--accent-glow); z-index: 1000; transition: 0.3s;
        }
        .mobile-search-float:hover { transform: scale(1.15); }

        @keyframes launchRocket {
            0% { transform: translateY(0) scale(1); }
            30% { transform: translateY(10px) scale(0.9); filter: brightness(1.5); }
            100% { transform: translateY(-800px) scale(0.5); opacity: 0; }
        }
        .rocket-top-btn.launching { animation: launchRocket 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards; }

        #search-modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85);
            z-index: 50000; display: none; justify-content: center; align-items: flex-start; padding-top: 120px; backdrop-filter: blur(12px);
        }
        .search-box-wrap { background: #0f172a; border: 2px solid var(--accent); width: 90%; max-width: 600px; border-radius: 20px; overflow: hidden; box-shadow: 0 0 40px var(--accent-glow); }
        .search-input { width: 100%; padding: 20px; background: transparent; border: none; color: white; font-size: 1.2rem; outline: none; border-bottom: 1px solid rgba(255,255,255,0.1); }
        .search-results-list { max-height: 300px; overflow-y: auto; padding: 10px; list-style: none; }
        .search-results-list li { padding: 12px 18px; border-radius: 12px; margin-bottom: 5px; cursor: pointer; transition: 0.2s; display: flex; align-items: center; gap: 10px; }
        .search-results-list li:hover { background: rgba(56, 189, 248, 0.15); color: var(--accent); }

        #project-modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.88);
            z-index: 40000; display: none; justify-content: center; align-items: center; padding: 20px; backdrop-filter: blur(15px);
        }
        .modal-content { background: #0f172a; border: 2px solid var(--accent); width: 100%; max-width: 650px; padding: 35px; border-radius: 24px; position: relative; box-shadow: 0 0 50px var(--accent-glow); }
        .close-modal { position: absolute; top: 20px; right: 20px; background: rgba(255,255,255,0.1); border: none; color: white; width: 35px; height: 35px; border-radius: 50%; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 1.1rem; transition: 0.3s; }
        .close-modal:hover { background: var(--accent); color: #030712; }

        #toast {
            position: fixed; bottom: 30px; right: 30px; background: rgba(15, 23, 42, 0.95);
            border: 1px solid var(--accent); color: white; padding: 16px 28px; border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.6); z-index: 20000; transform: translateY(150px);
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); display: flex; align-items: center; gap: 14px;
            backdrop-filter: blur(15px);
        }
        #toast.show { transform: translateY(0); }

        #lightbox { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.94); z-index: 30000; display: none; justify-content: center; align-items: center; padding: 20px; backdrop-filter: blur(10px); }
        #lightbox img { max-width: 90%; max-height: 85vh; border-radius: 16px; border: 2px solid var(--accent); box-shadow: 0 0 40px var(--accent-glow); }

        footer { text-align: center; padding: 50px 20px; border-top: 1px solid rgba(255,255,255,0.08); color: var(--text-muted); margin-top: 80px; }

        @media(max-width: 768px) {
            .nav-links, .hud-panel { display: none; }
            h1 { font-size: 2.2rem; }
            .cursor-dot, .cursor-outline, #particle-canvas { display: none; }
            * { cursor: auto !important; }
        }
    </style>
</head>
<body>

<canvas id="particle-canvas"></canvas>
<div class="cursor-dot" id="cursor-dot"></div>
<div class="cursor-outline" id="cursor-outline"></div>
<div id="progress-bar"></div>

<div id="toast">
    <i class="fa-solid fa-shield-halved" style="color: var(--accent); font-size: 1.4rem;"></i>
    <div>
        <div style="font-weight: 800;">MK CREATIVE AGENCY Web 2 Active</div>
        <div style="font-size: 0.85rem; color: var(--text-muted);">Systems online under Mohamed Antar's governance.</div>
    </div>
</div>

<div id="lightbox" onclick="closeLightbox()">
    <img id="lightbox-img" src="" alt="Expanded View">
</div>

<!-- Quick Search Modal -->
<div id="search-modal" onclick="closeSearchModal(event)">
    <div class="search-box-wrap" onclick="event.stopPropagation()">
        <input type="text" class="search-input" id="search-input-box" placeholder="Search agency systems, Assistant or team..." oninput="filterSearch()">
        <ul class="search-results-list" id="search-results">
            <li onclick="scrollToSection('about')"><i class="fa-solid fa-building"></i> <span data-translate="s_about">About MK CREATIVE Agency</span></li>
            <li onclick="scrollToSection('assistant-bot')"><i class="fa-solid fa-robot"></i> <span data-translate="s_ai">MK Assistant Bot (المساعد الذكي)</span></li>
            <li onclick="scrollToSection('ceo')"><i class="fa-solid fa-user-tie"></i> <span data-translate="s_ceo">CEO & Founder: Mohamed Antar</span></li>
            <li onclick="scrollToSection('team')"><i class="fa-solid fa-users"></i> <span data-translate="s_team">Motion Graphics Lead: Malek Mohamed</span></li>
            <li onclick="scrollToSection('certifications')"><i class="fa-solid fa-award"></i> <span data-translate="s_certs">Verified Google Cloud Certifications</span></li>
            <li onclick="scrollToSection('projects')"><i class="fa-solid fa-store"></i> <span data-translate="s_proj">Future Mall POS System & AI Tools</span></li>
            <li onclick="scrollToSection('contact')"><i class="fa-solid fa-envelope"></i> <span data-translate="s_contact">Secure Corporate Contact</span></li>
        </ul>
    </div>
</div>

<!-- Detailed Project Modal -->
<div id="project-modal" onclick="closeProjectModal()">
    <div class="modal-content" onclick="event.stopPropagation()">
        <button class="close-modal" onclick="closeProjectModal()"><i class="fa-solid fa-xmark"></i></button>
        <h2 id="modal-title" style="color: var(--accent); margin-bottom: 15px;">Project Title</h2>
        <p id="modal-desc" style="color: var(--text-muted); line-height: 1.7; margin-bottom: 20px;"></p>
        <div id="modal-tech" style="display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 25px;"></div>
        <a href="#" id="modal-link" class="btn" target="_blank"><i class="fa-solid fa-external-link"></i> <span data-translate="launch_demo">Launch Agency Demo</span></a>
    </div>
</div>

<header>
    <div class="nav-container">
        <div class="logo">
            <i class="fa-solid fa-cube"></i> MK CREATIVE AGENCY Web 2
            <span class="status-badge"><span class="status-dot"></span> <span data-translate="secure_node">Active Node</span></span>
        </div>
        
        <div class="hud-panel">
            <div class="network-ticker"><i class="fa-solid fa-wifi"></i> <span id="ping-val">19</span>ms</div>
            <div class="weather-ticker"><i class="fa-solid fa-cloud-sun"></i> <span data-translate="dakahlia">Dakahlia: 32°C</span></div>
            <div class="session-ticker"><i class="fa-solid fa-clock"></i> <span id="session-time">00:00</span></div>
            <select id="langSwitch" class="lang-select" onchange="changeLanguage(this.value)">
                <option value="ar">العربية</option>
                <option value="en">English</option>
                <option value="fr">Français</option>
            </select>
        </div>

        <nav class="nav-links">
            <a href="#about"><i class="fa-solid fa-building"></i> <span data-translate="nav_agency">Agency</span></a>
            <a href="#assistant-bot"><i class="fa-solid fa-robot"></i> <span data-translate="nav_ai">Assistant Bot</span></a>
            <a href="#ceo"><i class="fa-solid fa-user-tie"></i> <span data-translate="nav_ceo">CEO</span></a>
            <a href="#team"><i class="fa-solid fa-users"></i> <span data-translate="nav_team">Team</span></a>
            <a href="#certifications"><i class="fa-solid fa-award"></i> <span data-translate="nav_certs">Certifications</span></a>
            <a href="#projects"><i class="fa-solid fa-layer-group"></i> <span data-translate="nav_solutions">Solutions</span></a>
            <a href="#contact"><i class="fa-solid fa-envelope"></i> <span data-translate="nav_contact">Contact</span></a>
        </nav>
    </div>
</header>

<div class="activity-ticker-bar">
    <div class="ticker-content">
        🏢 <b data-translate="ticker_title">MK CREATIVE AGENCY Web 2:</b> <span data-translate="ticker_desc">High-Performance Cloud Architecture & AI Assistant Integration</span> &nbsp;&bull;&nbsp; ♟️ <span data-translate="ticker_ceo">Directed by Mohamed Antar (CEO, 14y)</span> &nbsp;&bull;&nbsp; <span data-translate="ticker_search">Press Ctrl + K for Agency Quick Search!</span>
    </div>
</div>

<section class="hero" id="about">
    <div class="container visible">
        <h1>MK CREATIVE AGENCY Web 2</h1>
        <p style="font-size: 1.3rem; color: var(--text-muted);">
            <span data-translate="hero_subtitle">Empowering Global Business with</span> <span class="typed-text" id="typed"></span>
        </p>
        
        <div class="vibe-ticker">
            <i class="fa-solid fa-microchip fa-spin" style="color: var(--accent);"></i> 
            <span><span data-translate="agency_status">Agency Status:</span> <b><span data-translate="agency_status_val">Next-Gen Cloud & Assistant Frameworks Active</span></b></span>
        </div>

        <p style="max-width: 750px; margin: 25px auto; color: #cbd5e1; line-height: 1.8;" data-translate="hero_desc">
            MK CREATIVE AGENCY Web 2 is a forward-thinking technology corporation specializing in automated retail POS systems, high-retention digital media pipelines, and intelligent assistant solutions.
        </p>
        
        <div style="margin-top: 30px;">
            <a href="#assistant-bot" class="btn"><i class="fa-solid fa-robot"></i> <span data-translate="btn_ai">Open MK Assistant Bot</span></a>
            <a href="#projects" class="btn btn-outline"><i class="fa-solid fa-rocket"></i> <span data-translate="btn_explore">Explore Solutions</span></a>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" data-target="10">0</div>
                <div class="stat-label" data-translate="stat_certs">Verified Google Cloud Certs</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="40">0</div>
                <div class="stat-label" data-translate="stat_views">Million+ Global Views</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="14">0</div>
                <div class="stat-label" data-translate="stat_age">Years Young Innovator CEO</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="100">0</div>
                <div class="stat-label" data-translate="stat_secure">% Secure Infrastructure</div>
            </div>
        </div>
    </div>
</section>

<!-- MK ASSISTANT BOT (المساعد الذكي المدرب خصيصاً للشغل) -->
<div class="container" id="assistant-bot">
    <h2 class="section-title" data-translate="sec_bot">MK ASSISTANT BOT (المساعد الذكي للوكالة)</h2>
    <p style="color: var(--text-muted); margin-bottom: 25px;" data-translate="bot_subtitle">اسأل المساعد عن خدمات الوكالة، تفاصيل المشاريع، انضمام فريق العمل، أو تقديم استمارة التقديم والتنفيذ.</p>
    
    <div class="assistant-section-container">
        <div class="assistant-box-header">
            <div style="display: flex; align-items: center; gap: 12px;">
                <div style="width: 42px; height: 42px; background: rgba(56, 189, 248, 0.15); border: 2px solid var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; color: var(--accent); font-size: 1.2rem;">
                    <i class="fa-solid fa-robot"></i>
                </div>
                <div>
                    <h3 style="color: var(--accent); font-size: 1.1rem;"><span data-translate="bot_name">MK Assistant Bot v2.0</span></h3>
                    <p style="color: #22c55e; font-size: 0.75rem;"><i class="fa-solid fa-circle" style="font-size: 6px;"></i> <span data-translate="bot_online">مستعد للإجابة عن أسئلة الشغل والخدمات</span></p>
                </div>
            </div>
            <button class="btn btn-outline" style="padding: 6px 12px; font-size: 0.75rem;" onclick="clearChat()"><i class="fa-solid fa-rotate-right"></i> <span data-translate="clear_chat">إعادة المحادثة</span></button>
        </div>

        <!-- أسئلة سريعة مقترحة (Chips) -->
        <div class="chat-quick-chips">
            <button class="chip-btn" onclick="sendQuickQuery('من هو مؤسس الشركة وما هي خدماتها؟')">🏢 من هو المؤسس والخدمات؟</button>
            <button class="chip-btn" onclick="sendQuickQuery('كيف أنضم لفريق العمل في MK Creative؟')">🤝 كيف أنضم للعمل؟</button>
            <button class="chip-btn" onclick="sendQuickQuery('ما هو نظام Future Mall POS؟')">🛒 نظام Future Mall POS</button>
            <button class="chip-btn" onclick="sendQuickQuery('ما هي مشاريع الموشن جرافيك ومالك محمد؟')">🎬 مشاريع الموشن جرافيك</button>
        </div>

        <div class="chat-messages-area" id="chat-messages">
            <div class="chat-msg bot">
                أهلاً بك في منصة <b>MK CREATIVE AGENCY Web 2</b>! أنا المساعد الذكي للوكالة. هل أنت مهتم بالانضمام للعمل معنا في فريق MK، أو ترغب في معرفة تفاصيل مشاريعنا وبرمجياتنا؟ اطرح سؤالك أو اختر من الأزرار السريعة بالأعلى! 🚀
            </div>
        </div>

        <div class="chat-input-row">
            <input type="text" id="chat-input-box" class="chat-input" placeholder="اكتب سؤالك عن الشغل، الخدمات، أو التقديم..." onkeypress="handleChatKeyPress(event)">
            <button class="btn" onclick="sendUserMessage()"><i class="fa-solid fa-paper-plane"></i> <span data-translate="btn_send">إرسال</span></button>
        </div>
    </div>
</div>

<!-- CEO PROFILE SECTION -->
<div class="container" id="ceo">
    <h2 class="section-title" data-translate="sec_exec">EXECUTIVE LEADERSHIP</h2>
    <div class="card" style="max-width: 900px; margin: auto; display: flex; flex-direction: column; gap: 20px;">
        <div style="display: flex; align-items: center; gap: 20px; flex-wrap: wrap;">
            <div style="width: 80px; height: 80px; background: rgba(56, 189, 248, 0.1); border: 2px solid var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 2.2rem; color: var(--accent);">
                <i class="fa-solid fa-user-tie"></i>
            </div>
            <div>
                <h3 style="font-size: 1.6rem; color: var(--accent);">Mohamed Antar (محمد عنتر)</h3>
                <p style="color: var(--text-muted); font-size: 0.95rem;" data-translate="ceo_role">Founder & Chief Executive Officer (CEO) • Age 14 • Dakahlia, Egypt</p>
            </div>
        </div>
        <p style="color: #cbd5e1; line-height: 1.8;" data-translate="ceo_desc">
            As the 14-year-old visionary behind MK CREATIVE AGENCY Web 2, Mohamed oversees technical architecture, AI assistant integrations, and high-level software engineering. Holding 10 official certifications from Udacity and Google Cloud, he bridges the gap between advanced cloud operations, automated commercial applications, and viral digital media solutions. He also actively administers the EGYPT CHESS CLUB.
        </p>
    </div>
</div>

<!-- AGENCY TEAM & COLLABORATORS SECTION -->
<div class="container" id="team">
    <h2 class="section-title" data-translate="sec_team">AGENCY TEAM & COLLABORATORS</h2>
    <p style="color: var(--text-muted); margin-bottom: 25px;" data-translate="team_subtitle">Key talent who contributed creative excellence to MK CREATIVE AGENCY Web 2 projects.</p>
    
    <div class="grid" style="max-width: 900px; margin: auto;">
        <div class="card" style="display: flex; flex-direction: column; gap: 15px;">
            <div style="display: flex; align-items: center; gap: 15px;">
                <div style="width: 65px; height: 65px; background: rgba(56, 189, 248, 0.1); border: 2px solid var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1.8rem; color: var(--accent);">
                    <i class="fa-solid fa-video"></i>
                </div>
                <div>
                    <h3 style="font-size: 1.3rem; color: var(--accent);">Malek Mohamed</h3>
                    <p style="color: var(--text-muted); font-size: 0.85rem;" data-translate="malek_role">Motion Graphic Designer & Video Editor (Summer Launch)</p>
                </div>
            </div>
            <p style="color: #cbd5e1; font-size: 0.95rem; line-height: 1.6;" data-translate="malek_desc">
                Served as the lead Motion Graphic Designer for MK CREATIVE Agency's Summer Launch. Demonstrated exemplary commitment, visual creativity, and professional execution across brand video production and dynamic logo animations.
            </p>
            
            <div style="margin-top: 15px; background: rgba(0,0,0,0.3); padding: 15px; border-radius: 16px; border: 1px solid rgba(56, 189, 248, 0.2);">
                <h4 style="color: var(--accent); font-size: 1rem; margin-bottom: 10px;"><i class="fa-solid fa-play-circle"></i> <span data-translate="asmaa_title">Asmaa Centre Collaboration Project</span></h4>
                <video controls autoplay muted loop playsinline style="width: 100%; border-radius: 12px; border: 1px solid rgba(255,255,255,0.1); max-height: 450px; object-fit: cover;">
                    <source src="Asmaa Centre collaboration project .mov" type="video/quicktime">
                    <source src="Asmaa Centre collaboration project .mov" type="video/mp4">
                    Your browser does not support the video tag.
                </video>
            </div>

            <div style="margin-top: 10px;">
                <button class="btn btn-outline" onclick="openLightbox('Screenshot_20260815_210636.jpg')" style="width: 100%; justify-content: center;"><i class="fa-solid fa-award"></i> <span data-translate="btn_cert">View Official Internship Certificate (June 29, 2026)</span></button>
            </div>
        </div>
    </div>
</div>

<!-- CERTIFICATIONS SECTION -->
<div class="container" id="certifications">
    <h2 class="section-title" data-translate="sec_certs">VERIFIED AGENCY CERTIFICATIONS</h2>
    <p style="color: var(--text-muted); margin-bottom: 20px;" data-translate="certs_subtitle">Official credentials awarded by Udacity in collaboration with Google Cloud and Accenture.</p>
    
    <div class="cert-grid">
        <div class="cert-card">
            <img src="IMG_20251221_133154.jpg" alt="Gemini in Google Sheets" onclick="openLightbox(this.src)">
            <h3 style="color: var(--accent); margin: 15px 0 8px; font-size: 1.1rem;">Gemini in Google Sheets</h3>
            <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 15px;">Google Cloud & Udacity</p>
            <button class="btn btn-outline" onclick="openLightbox('IMG_20251221_133154.jpg')" style="width: 100%; justify-content: center;"><i class="fa-solid fa-eye"></i> <span data-translate="view_cred">View Credential</span></button>
        </div>

        <div class="cert-card">
            <img src="IMG_20251221_133952_edit_1294679129859207.jpg" alt="Gemini in Gmail" onclick="openLightbox(this.src)">
            <h3 style="color: var(--accent); margin: 15px 0 8px; font-size: 1.1rem;">Gemini in Gmail</h3>
            <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 15px;">Google Cloud & Udacity</p>
            <button class="btn btn-outline" onclick="openLightbox('IMG_20251221_133952_edit_1294679129859207.jpg')" style="width: 100%; justify-content: center;"><i class="fa-solid fa-eye"></i> <span data-translate="view_cred">View Credential</span></button>
        </div>

        <div class="cert-card">
            <img src="IMG_20251221_134712.jpg" alt="Trust and Security with Google Cloud" onclick="openLightbox(this.src)">
            <h3 style="color: var(--accent); margin: 15px 0 8px; font-size: 1.1rem;">Trust & Security with Google Cloud</h3>
            <p style="color: var(--text-muted); font-size: 0.85rem; margin-bottom: 15px;">Google Cloud & Udacity</p>
            <button class="btn btn-outline" onclick="openLightbox('IMG_20251221_134712.jpg')" style="width: 100%; justify-content: center;"><i class="fa-solid fa-eye"></i> <span data-translate="view_cred">View Credential</span></button>
        </div>
    </div>
</div>

<div class="container" id="projects">
    <h2 class="section-title" data-translate="sec_solutions">AGENCY SOLUTIONS & AI TOOLS</h2>
    <div class="grid">
        <div class="card" onclick="openProjectModal('Future Mall POS', 'Advanced enterprise retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, multi-currency frameworks, and automated inventory management.', ['Python', 'HTML/JS', 'AI Frameworks'], 'https://github.com')">
            <h3><i class="fa-solid fa-store" style="color: var(--accent);"></i> Future Mall POS</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-translate="proj1_desc">Full-stack retail web application featuring role-based access control, AI product classification, and multi-currency frameworks.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);" data-translate="view_specs">View System Specs &rarr;</span>
        </div>
        <div class="card" onclick="openProjectModal('Viral Media Engine', 'Corporate media distribution engine generating over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines.', ['Video Production', 'Analytics', 'Media Scaling'], 'https://youtube.com/@mo7amed_5272')">
            <h3><i class="fa-solid fa-video" style="color: var(--accent);"></i> Viral Media Engine</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-translate="proj2_desc">Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);" data-translate="view_specs">View System Specs &rarr;</span>
        </div>
        <div class="card" onclick="openProjectModal('EGYPT CHESS CLUB', 'Strategic community management ecosystem and automated tactical club frameworks hosted on Chess.com to foster high-level analytical thinking and local talent.', ['Strategy', 'Community Engine'], 'https://chess.com')">
            <h3><i class="fa-solid fa-chess-board" style="color: var(--accent);"></i> EGYPT CHESS CLUB (Admin)</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-translate="proj3_desc">Active administration and tactical management within digital strategy communities and club workflows.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);" data-translate="view_specs">View System Specs &rarr;</span>
        </div>
    </div>
</div>

<div class="container" id="contact">
    <h2 class="section-title" data-translate="sec_comm">SECURE AGENCY COMMUNICATIONS</h2>
    <div class="card" style="max-width: 650px; margin: auto; text-align: center; cursor: default;">
        <p style="margin: 12px 0;"><i class="fa-solid fa-envelope" style="color: var(--accent);"></i> <span data-translate="agency_email">Agency Email:</span> <span>moamedantar8@gmail.com</span></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-whatsapp" style="color: #22c55e;"></i> <span data-translate="agency_whatsapp">Direct Line / WhatsApp:</span> <a href="https://wa.me/201559719175" target="_blank" style="color:var(--accent); text-decoration: none;">+20 155 971 9175</a></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-linkedin" style="color: var(--accent);"></i> <span data-translate="agency_linkedin">Executive LinkedIn:</span> <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent); text-decoration: none;" target="_blank">mohamed-antar-522201406</a></p>
        <button class="btn" style="margin-top: 20px;" onclick="copyEmail()"><i class="fa-solid fa-copy"></i> <span data-translate="btn_copy">Copy Agency Email</span></button>
    </div>
</div>

<div class="floating-controls">
    <button class="float-btn" onclick="toggleMatrixMode()" title="Toggle Matrix Secure Mode"><i class="fa-solid fa-code"></i></button>
    <button class="float-btn" onclick="toggleAmberMode()" title="Toggle Amber E-Ink Mode"><i class="fa-solid fa-moon"></i></button>
    <button class="float-btn" id="audio-toggle-btn" onclick="toggleAudioFX()" title="Toggle Audio Sound FX"><i class="fa-solid fa-volume-high"></i></button>
</div>

<button class="rocket-top-btn" id="rocketBtn" onclick="launchToTop()" title="Scroll to Top">🚀</button>
<button class="mobile-search-float" onclick="openSearchModalMobile()" title="Quick Search"><i class="fa-solid fa-magnifying-glass"></i></button>

<footer>
    <p data-translate="footer_text">&copy; 2026 MK CREATIVE AGENCY Web 2. Founded and Directed by Mohamed Antar. All Rights Reserved.</p>
</footer>

<script>
    // --- نظام MK Assistant Bot المدرب خصيصاً للشغل والخدمات ---
    const agencyKnowledgeBase = [
        {
            keywords: ["مؤسس", "من أنت", "محمد عنتر", "الceo", "صاحب الشركة", "عمرك"],
            response: "مؤسس ومدير شركة MK CREATIVE AGENCY Web 2 هو المبتكر الشاب **محمد عنتر** (عمره ١٤ عاماً من الدقهلية، مصر). وهو حاصل على 10 شهادات معتمدة من Google Cloud و Udacity في مجالات السحابة والذكاء الاصطناعي[cite: 4, 5]."
        },
        {
            keywords: ["انضمام", "عمل", "وظيفة", "شغل", "فريق", "استمارة", "تقديم"],
            response: "أهلاً بك! للانضمام والعمل معنا في فريق MK CREATIVE AGENCY Web 2، يسعدنا استقبال طلباتك عبر استمارة التقديم الرسمية أو التواصل المباشر عبر البريد (moamedantar8@gmail.com) أو الواتساب (+201559719175)[cite: 4]."
        },
        {
            keywords: ["future mall", "pos", "نظام نقاط البيع", "متجر"],
            response: "نظام **Future Mall POS** هو تطبيق ويب متطور لقطاع التجزئة تم تطويره بواسطة الوكالة باستخدام Python وتقنيات الويب، ويتميز بتحكم في الصلاحيات، وتصنيف ذكي للمنتجات، وأنظمة عملات متعددة[cite: 4, 5]."
        },
        {
            keywords: ["مالك", "موشن", "جرافيك", "فيديو", "مونتاج", "أسماء"],
            response: "تعاونت الوكالة مع مصمم الموشن جرافيك المبدع **مالك محمد** في مشاريع الصيف وإطلاق فيديوهات لعلامات تجارية مثل 'مشروع مركز أسماء' (Asmaa Centre collaboration project)[cite: 4]."
        },
        {
            keywords: ["شطرنج", "chess", "egypt chess club"],
            response: "يقوم المدير التنفيذي محمد عنتر بإدارة وتنسيق الأنشطة التكتيكية والمجتمعية في مجموعة **EGYPT CHESS CLUB** على منصة Chess.com[cite: 4]."
        },
        {
            keywords: ["شهادات", "google cloud", "udacity", "اعتماد"],
            response: "تمتلك الوكالة سجل موثوق من شهادات Google Cloud في مجالات الأمان، وتحليلات البيانات، وتكامل أدوات Gemini Workspace[cite: 4, 5]."
        },
        {
            keywords: ["التواصل", "ايميل", "رقم", "واتساب", "اتصل"],
            response: "يمكنك التواصل معنا مباشرة عبر البريد الإلكتروني: moamedantar8@gmail.com أو عبر رقم الواتساب: +201559719175[cite: 4]."
        }
    ];

    function getBotResponse(userMsg) {
        const lowerMsg = userMsg.toLowerCase();
        for (let item of agencyKnowledgeBase) {
            for (let kw of item.keywords) {
                if (lowerMsg.includes(kw)) {
                    return item.response;
                }
            }
        }
        return "سؤال ممتاز حول العمل في MK CREATIVE AGENCY Web 2! نحن نركز على تطوير الحلول التقنية المتقدمة، أنظمة الـ POS، وإنتاج المحتوى الرقمي. هل ترغب في معرفة المزيد عن خدماتنا أو التقديم للانضمام لفريقنا؟ يمكنك مراسلتنا عبر الواتساب أو الايميل الظاهر أسفل الموقع[cite: 4, 5].";
    }

    function appendMessage(sender, text) {
        const chatContainer = document.getElementById('chat-messages');
        if (!chatContainer) return;
        const msgDiv = document.createElement('div');
        msgDiv.className = `chat-msg ${sender}`;
        msgDiv.innerHTML = text;
        chatContainer.appendChild(msgDiv);
        chatContainer.scrollTop = chatContainer.scrollHeight;
    }

    function sendUserMessage() {
        const input = document.getElementById('chat-input-box');
        const text = input.value.trim();
        if (!text) return;
        
        appendMessage('user', text);
        input.value = '';

        // محاكاة تفكير المساعد الذكي
        setTimeout(() => {
            const reply = getBotResponse(text);
            appendMessage('bot', reply);
        }, 500);
    }

    function sendQuickQuery(queryText) {
        document.getElementById('chat-input-box').value = queryText;
        sendUserMessage();
    }

    function handleChatKeyPress(e) {
        if (e.key === 'Enter') {
            sendUserMessage();
        }
    }

    function clearChat() {
        const chatContainer = document.getElementById('chat-messages');
        chatContainer.innerHTML = `
            <div class="chat-msg bot">
                تم مسح المحادثة. كيف يمكنني مساعدتك اليوم في أعمال وخدمات MK CREATIVE AGENCY Web 2؟ 🚀
            </div>
        `;
        showToast("✓ تمت إعادة تعيين المحادثة");
    }

    // قاموس الترجمات الشامل
    const translations = {
        ar: {
            dir: "rtl",
            secure_node: "Active Node",
            dakahlia: "الدقهلية: 32°م",
            nav_agency: "الوكالة",
            nav_ai: "المساعد الذكي",
            nav_ceo: "المؤسس",
            nav_team: "الفريق",
            nav_certs: "الشهادات",
            nav_solutions: "الحلول",
            nav_contact: "تواصل معنا",
            ticker_title: "MK CREATIVE AGENCY Web 2:",
            ticker_desc: "هندسة السحابة عالية الأداء وتكامل المساعد الذكي",
            ticker_ceo: "بإدارة محمد عنتر (المدير التنفيذي، 14 سنة)",
            ticker_search: "اضغط Ctrl + K للبحث السريع داخل الموقع!",
            hero_subtitle: "تمكين الأعمال العالمية باستخدام",
            agency_status: "حالة الوكالة:",
            agency_status_val: "أنظمة السحابة والمساعد الذكي من الجيل التالي نشطة",
            hero_desc: "MK CREATIVE AGENCY Web 2 هي شركة تقنية مستقبلية تخصصت في أنظمة نقاط البيع الآلية للتجزئة، خطوط الإنتاج الإعلامي الرقمي، وحلول المساعد الذكي.",
            btn_ai: "فتح المساعد الذكي",
            btn_explore: "استكشف الحلول",
            stat_certs: "شهادات Google Cloud معتمدة",
            stat_views: "أكثر من مليون مشاهدة عالمية",
            stat_age: "سنوات عمر المدير التنفيذي المبتكر",
            stat_secure: "% البنية التحتية الآمنة",
            sec_bot: "MK ASSISTANT BOT (المساعد الذكي للوكالة)",
            bot_subtitle: "اسأل المساعد عن خدمات الوكالة، تفاصيل المشاريع، انضمام فريق العمل، أو تقديم استمارة التقديم والتنفيذ.",
            bot_name: "MK Assistant Bot v2.0",
            bot_online: "مستعد للإجابة عن أسئلة الشغل والخدمات",
            clear_chat: "إعادة المحادثة",
            btn_send: "إرسال",
            sec_exec: "القيادة التنفيذية",
            ceo_role: "المؤسس والرئيس التنفيذي (CEO) • العمر 14 سنة • الدقهلية، مصر",
            ceo_desc: "بصفته العقل المبتكر البالغ من العمر 14 عاماً خلف MK CREATIVE AGENCY Web 2، يشرف محمد على الهندسة المعمارية التقنية، وتكامل المساعد الذكي، وهندسة البرمجيات عالية المستوى.",
            sec_team: "فريق الوكالة والمبدعون",
            team_subtitle: "المواهب الرئيسية التي ساهمت بالتميز الإبداعي في مشاريع MK CREATIVE AGENCY Web 2.",
            malek_role: "مصمم جرافيك ومونتير فيديو (إطلاق الصيف)",
            malek_desc: "عمل كمصمم رئيسي للرسومات المتحركة لإطلاق صيف الوكالة، وأظهر التزاماً استثنائياً وإبداعاً بصرياً وتنفيذاً احترافياً.",
            asmaa_title: "مشروع التعاون مع مركز أسماء",
            btn_cert: "عرض شهادة التدريب الرسمية (29 يونيو 2026)",
            sec_certs: "شهادات الوكالة المعتمدة",
            certs_subtitle: "أوراق الاعتماد الرسمية المقدمة من Udacity بالتعاون مع Google Cloud و Accenture.",
            view_cred: "عرض الاعتماد",
            sec_solutions: "حلول الوكالة وأدوات الذكاء الاصطناعي",
            proj1_desc: "تطبيق ويب متكامل لقطاع التجزئة يتميز بالتحكم في الصلاحيات، التصنيف الآلي للمنتجات عبر الذكاء الاصطناعي، وأنظمة العملات المتعددة.",
            proj2_desc: "حقق أكثر من 40 مليون مشاهدة من خلال التوازن الصوتي البصري الدقيق، والتحسين المتقدم للفيديوهات القصيرة.",
            proj3_desc: "الإدارة النشطة والإدارة التكتيكية داخل مجتمعات الاستراتيجيات الرقمية وسير عمل الأندية.",
            view_specs: "عرض تفاصيل النظام ←",
            sec_comm: "اتصالات الوكالة الآمنة",
            agency_email: "بريد الوكالة:",
            agency_whatsapp: "الخط المباشر / واتساب:",
            agency_linkedin: "لينكد إن التنفيذي:",
            btn_copy: "نسخ بريد الوكالة",
            footer_text: "© 2026 MK CREATIVE AGENCY Web 2. مؤسسة ومُدارة بواسطة محمد عنتر. جميع الحقوق محفوظة.",
            launch_demo: "تشغيل العرض التوضيحي",
            s_about: "حول MK CREATIVE AGENCY Web 2",
            s_ai: "المساعد الذكي MK Assistant Bot",
            s_ceo: "المؤسس والرئيس التنفيذي: محمد عنتر",
            s_team: "مسؤول الموشن جرافيك: مالك محمد",
            s_certs: "شهادات Google Cloud المعتمدة",
            s_proj: "نظام نقاط البيع Future Mall POS وأدوات الذكاء الاصطناعي",
            s_contact: "التواصل المؤسسي الآمن"
        },
        en: {
            dir: "ltr",
            secure_node: "Active Node",
            dakahlia: "Dakahlia: 32°C",
            nav_agency: "Agency",
            nav_ai: "Assistant Bot",
            nav_ceo: "CEO",
            nav_team: "Team",
            nav_certs: "Certifications",
            nav_solutions: "Solutions",
            nav_contact: "Contact",
            ticker_title: "MK CREATIVE AGENCY Web 2:",
            ticker_desc: "High-Performance Cloud Architecture & Assistant Integration",
            ticker_ceo: "Directed by Mohamed Antar (CEO, 14y)",
            ticker_search: "Press Ctrl + K for Agency Quick Search!",
            hero_subtitle: "Empowering Global Business with",
            agency_status: "Agency Status:",
            agency_status_val: "Next-Gen Cloud & Assistant Frameworks Active",
            hero_desc: "MK CREATIVE AGENCY Web 2 is a forward-thinking technology corporation specializing in automated retail POS systems, high-retention digital media pipelines, and smart assistant solutions.",
            btn_ai: "Open MK Assistant Bot",
            btn_explore: "Explore Solutions",
            stat_certs: "Verified Google Cloud Certs",
            stat_views: "Million+ Global Views",
            stat_age: "Years Young Innovator CEO",
            stat_secure: "% Secure Infrastructure",
            sec_bot: "MK ASSISTANT BOT",
            bot_subtitle: "Ask the assistant about agency services, project details, team recruitment, or application submissions.",
            bot_name: "MK Assistant Bot v2.0",
            bot_online: "Ready to answer work and service questions",
            clear_chat: "Reset Chat",
            btn_send: "Send",
            sec_exec: "EXECUTIVE LEADERSHIP",
            ceo_role: "Founder & Chief Executive Officer (CEO) • Age 14 • Dakahlia, Egypt",
            ceo_desc: "As the 14-year-old visionary behind MK CREATIVE AGENCY Web 2, Mohamed oversees technical architecture, AI assistant integrations, and high-level software engineering.",
            sec_team: "AGENCY TEAM & COLLABORATORS",
            team_subtitle: "Key talent who contributed creative excellence to MK CREATIVE AGENCY Web 2 projects.",
            malek_role: "Motion Graphic Designer & Video Editor (Summer Launch)",
            malek_desc: "Served as the lead Motion Graphic Designer for MK CREATIVE Agency's Summer Launch. Demonstrated exemplary commitment and visual creativity.",
            asmaa_title: "Asmaa Centre Collaboration Project",
            btn_cert: "View Official Internship Certificate (June 29, 2026)",
            sec_certs: "VERIFIED AGENCY CERTIFICATIONS",
            certs_subtitle: "Official credentials awarded by Udacity in collaboration with Google Cloud and Accenture.",
            view_cred: "View Credential",
            sec_solutions: "AGENCY SOLUTIONS & AI TOOLS",
            proj1_desc: "Full-stack retail web application featuring role-based access control, AI product classification, and multi-currency frameworks.",
            proj2_desc: "Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing.",
            proj3_desc: "Active administration and tactical management within digital strategy communities and club workflows.",
            view_specs: "View System Specs →",
            sec_comm: "SECURE AGENCY COMMUNICATIONS",
            agency_email: "Agency Email:",
            agency_whatsapp: "Direct Line / WhatsApp:",
            agency_linkedin: "Executive LinkedIn:",
            btn_copy: "Copy Agency Email",
            footer_text: "© 2026 MK CREATIVE AGENCY Web 2. Founded and Directed by Mohamed Antar. All Rights Reserved.",
            launch_demo: "Launch Agency Demo",
            s_about: "About MK CREATIVE AGENCY Web 2",
            s_ai: "MK Assistant Bot",
            s_ceo: "CEO & Founder: Mohamed Antar",
            s_team: "Motion Graphics Lead: Malek Mohamed",
            s_certs: "Verified Google Cloud Certifications",
            s_proj: "Future Mall POS System & AI Tools",
            s_contact: "Secure Corporate Contact"
        },
        fr: {
            dir: "ltr",
            secure_node: "Nœud Actif",
            dakahlia: "Dakahlia: 32°C",
            nav_agency: "Agence",
            nav_ai: "Assistant Bot",
            nav_ceo: "PDG",
            nav_team: "Équipe",
            nav_certs: "Certifications",
            nav_solutions: "Solutions",
            nav_contact: "Contact",
            ticker_title: "MK CREATIVE AGENCY Web 2:",
            ticker_desc: "Architecture Cloud Haute Performance & Assistant IA",
            ticker_ceo: "Dirigé par Mohamed Antar (PDG, 14 ans)",
            ticker_search: "Appuyez sur Ctrl + K pour la recherche rapide !",
            hero_subtitle: "Autonomiser les entreprises mondiales avec",
            agency_status: "Statut de l'Agence:",
            agency_status_val: "Cadres Cloud & Assistant de Nouvelle Génération Actifs",
            hero_desc: "MK CREATIVE AGENCY Web 2 est une entreprise technologique innovante spécialisée dans les systèmes POS automatisés.",
            btn_ai: "Ouvrir MK Assistant Bot",
            btn_explore: "Explorer les Solutions",
            stat_certs: "Certifications Google Cloud Vérifiées",
            stat_views: "Millions de Vues Mondiales",
            stat_age: "Ans du PDG Innovateur",
            stat_secure: "% Infrastructure Sécurisée",
            sec_bot: "MK ASSISTANT BOT",
            bot_subtitle: "Posez vos questions à l'assistant concernant les services, les projets et le recrutement.",
            bot_name: "MK Assistant Bot v2.0",
            bot_online: "Prêt à répondre aux questions",
            clear_chat: "Réinitialiser",
            btn_send: "Envoyer",
            sec_exec: "LEADERSHIP EXÉCUTIF",
            ceo_role: "Fondateur & Directeur Général (PDG) • 14 ans • Dakahlia, Égypte",
            ceo_desc: "En tant que visionnaire de 14 ans derrière MK CREATIVE AGENCY Web 2, Mohamed supervise l'architecture technique.",
            sec_team: "ÉQUIPE DE L'AGENCE & COLLABORATEURS",
            team_subtitle: "Talents clés ayant contribué à l'excellence créative des projets.",
            malek_role: "Designer Motion Graphics & Monteur Vidéo",
            malek_desc: "A servi en tant que Motion Designer principal pour le lancement estival.",
            asmaa_title: "Projet de Collaboration Asmaa Centre",
            btn_cert: "Voir le Certificat de Stage Officiel (29 Juin 2026)",
            sec_certs: "CERTIFICATIONS OFFICIELLES DE L'AGENCE",
            certs_subtitle: "Titres officiels décernés par Udacity en collaboration avec Google Cloud.",
            view_cred: "Voir le Certificat",
            sec_solutions: "SOLUTIONS DE L'AGENCE & OUTILS IA",
            proj1_desc: "Application Web e-commerce complète avec contrôle d'accès basé sur les rôles.",
            proj2_desc: "Généré plus de 40 millions de vues grâce à un équilibre audiovisuel précis.",
            proj3_desc: "Administration active et gestion tactique au sein des communautés de stratégie.",
            view_specs: "Voir les Spécifications →",
            sec_comm: "COMMUNICATIONS SÉCURISÉES DE L'AGENCE",
            agency_email: "Email de l'Agence:",
            agency_whatsapp: "Ligne Directe / WhatsApp:",
            agency_linkedin: "LinkedIn Exécutif:",
            btn_copy: "Copier l'Email",
            footer_text: "© 2026 MK CREATIVE AGENCY Web 2. Fondé et Dirigé par Mohamed Antar. Tous droits réservés.",
            launch_demo: "Lancer la Démo",
            s_about: "À propos de MK CREATIVE AGENCY Web 2",
            s_ai: "MK Assistant Bot",
            s_ceo: "PDG & Fondateur : Mohamed Antar",
            s_team: "Responsable Motion Design : Malek Mohamed",
            s_certs: "Certifications Google Cloud Vérifiées",
            s_proj: "Système POS Future Mall & Outils IA",
            s_contact: "Contact Professionnel Sécurisé"
        }
    };

    function changeLanguage(lang) {
        const t = translations[lang];
        if (!t) return;
        document.documentElement.lang = lang;
        document.documentElement.dir = t.dir;

        document.querySelectorAll('[data-translate]').forEach(el => {
            const key = el.getAttribute('data-translate');
            if (t[key]) el.textContent = t[key];
        });
        showToast(lang === 'ar' ? "تم تغيير اللغة إلى العربية" : (lang === 'en' ? "Language changed to English" : "Langue changée en Français"));
    }

    let audioEnabled = true;
    function playClickSound() {
        if (!audioEnabled) return;
        try {
            const ctx = new (window.AudioContext || window.webkitAudioContext)();
            const osc = ctx.createOscillator();
            const gain = ctx.createGain();
            osc.type = 'sine';
            osc.frequency.setValueAtTime(800, ctx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(400, ctx.currentTime + 0.05);
            gain.gain.setValueAtTime(0.05, ctx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + 0.05);
            osc.connect(gain);
            gain.connect(ctx.destination);
            osc.start();
            osc.stop(ctx.currentTime + 0.05);
        } catch(e) {}
    }
    function toggleAudioFX() {
        audioEnabled = !audioEnabled;
        let btn = document.getElementById('audio-toggle-btn');
        btn.innerHTML = audioEnabled ? '<i class="fa-solid fa-volume-high"></i>' : '<i class="fa-solid fa-volume-xmark"></i>';
        showToast(audioEnabled ? "Audio FX Enabled" : "Audio FX Muted");
    }

    document.addEventListener('click', () => { playClickSound(); });

    const canvas = document.getElementById('particle-canvas');
    const ctx = canvas.getContext('2d');
    let particlesArray = [];
    function resizeCanvas() {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class Particle {
        constructor() {
            this.x = Math.random() * canvas.width;
            this.y = Math.random() * canvas.height;
            this.vx = (Math.random() - 0.5) * 0.8;
            this.vy = (Math.random() - 0.5) * 0.8;
            this.size = Math.random() * 2 + 1;
        }
        update() {
            this.x += this.vx;
            this.y += this.vy;
            if (this.x < 0 || this.x > canvas.width) this.vx = -this.vx;
            if (this.y < 0 || this.y > canvas.height) this.vy = -this.vy;
        }
        draw() {
            ctx.fillStyle = getComputedStyle(document.body).getPropertyValue('--accent').trim();
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
            ctx.fill();
        }
    }
    function initParticles() {
        particlesArray = [];
        let count = window.innerWidth > 768 ? 45 : 0;
        for (let i = 0; i < count; i++) particlesArray.push(new Particle());
    }
    initParticles();

    function animateParticles() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let i = 0; i < particlesArray.length; i++) {
            particlesArray[i].update();
            particlesArray[i].draw();
            for (let j = i + 1; j < particlesArray.length; j++) {
                let dx = particlesArray[i].x - particlesArray[j].x;
                let dy = particlesArray[i].y - particlesArray[j].y;
                let dist = Math.sqrt(dx * dx + dy * dy);
                if (dist < 120) {
                    ctx.strokeStyle = getComputedStyle(document.body).getPropertyValue('--accent').trim();
                    ctx.globalAlpha = (1 - (dist / 120)) * 0.2;
                    ctx.beginPath();
                    ctx.moveTo(particlesArray[i].x, particlesArray[i].y);
                    ctx.lineTo(particlesArray[j].x, particlesArray[j].y);
                    ctx.stroke();
                    ctx.globalAlpha = 1.0;
                }
            }
        }
        requestAnimationFrame(animateParticles);
    }
    animateParticles();

    const dot = document.getElementById('cursor-dot');
    const outline = document.getElementById('cursor-outline');
    window.addEventListener('mousemove', (e) => {
        dot.style.left = e.clientX + 'px';
        dot.style.top = e.clientY + 'px';
        outline.style.left = e.clientX + 'px';
        outline.style.top = e.clientY + 'px';
    });

    const rocketBtn = document.getElementById('rocketBtn');

    window.onscroll = () => {
        let winScroll = document.documentElement.scrollTop || document.body.scrollTop;
        let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        let scrolled = (winScroll / height) * 100;
        document.getElementById("progress-bar").style.width = scrolled + "%";
        
        if (winScroll > 300) {
            rocketBtn.classList.add('show');
        } else {
            rocketBtn.classList.remove('show');
        }

        document.querySelectorAll('.container').forEach(el => {
            let rect = el.getBoundingClientRect();
            if(rect.top < window.innerHeight - 80) el.classList.add('visible');
        });
    };

    window.addEventListener('keydown', (e) => {
        if ((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 'k') {
            e.preventDefault();
            openSearchModalMobile();
        }
        if (e.key === 'Escape') {
            document.getElementById('search-modal').style.display = 'none';
            document.getElementById('project-modal').style.display = 'none';
        }
    });

    function openSearchModalMobile() {
        document.getElementById('search-modal').style.display = 'flex';
        document.getElementById('search-input-box').focus();
    }

    function closeSearchModal(e) {
        if (e.target.id === 'search-modal') document.getElementById('search-modal').style.display = 'none';
    }

    function scrollToSection(id) {
        document.getElementById('search-modal').style.display = 'none';
        document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
    }

    function filterSearch() {
        let query = document.getElementById('search-input-box').value.toLowerCase();
        let items = document.getElementById('search-results').getElementsByTagName('li');
        for (let item of items) {
            let text = item.textContent.toLowerCase();
            item.style.display = text.includes(query) ? 'flex' : 'none';
        }
    }

    function openProjectModal(title, desc, techArray, link) {
        document.getElementById('modal-title').textContent = title;
        document.getElementById('modal-desc').textContent = desc;
        let techDiv = document.getElementById('modal-tech');
        techDiv.innerHTML = '';
        techArray.forEach(t => {
            let span = document.createElement('span');
            span.style.cssText = 'background: rgba(56, 189, 248, 0.1); color: var(--accent); padding: 5px 12px; border-radius: 10px; font-size: 0.8rem; border: 1px solid rgba(56, 189, 248, 0.3);';
            span.textContent = t;
            techDiv.appendChild(span);
        });
        document.getElementById('modal-link').href = link;
        document.getElementById('project-modal').style.display = 'flex';
    }
    function closeProjectModal() {
        document.getElementById('project-modal').style.display = 'none';
    }

    setInterval(() => {
        let randomPing = Math.floor(Math.random() * 5) + 17;
        document.getElementById('ping-val').textContent = randomPing;
    }, 3500);

    let totalSeconds = 0;
    setInterval(() => {
        totalSeconds++;
        let mins = Math.floor(totalSeconds / 60).toString().padStart(2, '0');
        let secs = (totalSeconds % 60).toString().padStart(2, '0');
        document.getElementById('session-time').textContent = `${mins}:${secs}`;
    }, 1000);

    window.onload = () => {
        setTimeout(() => {
            showToast("MK CREATIVE AGENCY Web 2 Online");
        }, 1000);
        startCounters();
    };

    function showToast(msg) {
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-shield-halved" style="color: var(--accent); font-size: 1.4rem;"></i><div><div style="font-weight: 800;">${msg}</div><div style="font-size: 0.85rem; color: var(--text-muted);">Managed by Mohamed Antar (CEO).</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 4000);
    }

    const words = ["Cloud Infrastructure & AI.", "Automated Retail Solutions.", "Next-Gen Assistant Frameworks."];
    let wordIdx = 0, charIdx = 0, currentWord = "", isDeletingState = false;
    function typeEffectEngine() {
        currentWord = words[wordIdx];
        if (isDeletingState) {
            document.getElementById("typed").textContent = currentWord.substring(0, charIdx - 1);
            charIdx--;
            if (charIdx == 0) { isDeletingState = false; wordIdx = (wordIdx + 1) % words.length; }
        } else {
            document.getElementById("typed").textContent = currentWord.substring(0, charIdx + 1);
            charIdx++;
            if (charIdx == currentWord.length) { isDeletingState = true; setTimeout(typeEffectEngine, 2200); return; }
        }
        setTimeout(typeEffectEngine, isDeletingState ? 35 : 80);
    }
    typeEffectEngine();

    function startCounters() {
        const counters = document.querySelectorAll('.stat-number');
        counters.forEach(counter => {
            const target = +counter.getAttribute('data-target');
            let count = 0;
            const speed = target / 40;
            const updateCount = () => {
                count += speed;
                if (count < target) {
                    counter.innerText = Math.ceil(count) + (target === 40 ? "M+" : "+");
                    setTimeout(updateCount, 30);
                } else {
                    counter.innerText = target + (target === 40 ? "M+" : "+");
                }
            };
            updateCount();
        });
    }

    function openLightbox(src) {
        document.getElementById('lightbox-img').src = src;
        document.getElementById('lightbox').style.display = 'flex';
    }
    function closeLightbox() {
        document.getElementById('lightbox').style.display = 'none';
    }

    function toggleMatrixMode() {
        document.body.classList.remove('amber-mode');
        document.body.classList.toggle('matrix-mode');
        initParticles();
        showToast(document.body.classList.contains('matrix-mode') ? "Matrix Secure Mode Active" : "Default Mode Restored");
    }

    function toggleAmberMode() {
        document.body.classList.remove('matrix-mode');
        document.body.classList.toggle('amber-mode');
        initParticles();
        showToast(document.body.classList.contains('amber-mode') ? "Amber E-Ink Mode Active" : "Default Mode Restored");
    }

    function copyEmail() {
        navigator.clipboard.writeText("moamedantar8@gmail.com");
        showToast("Agency Email Copied to Clipboard!");
    }

    function launchToTop() {
        rocketBtn.classList.add('launching');
        window.scrollTo({ top: 0, behavior: 'smooth' });
        setTimeout(() => {
            rocketBtn.classList.remove('launching');
            rocketBtn.classList.remove('show');
        }, 600);
    }
</script>

</body>
</html>
