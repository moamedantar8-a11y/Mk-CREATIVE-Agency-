<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="color-scheme" content="only dark">
    <title>Mohamed Antar | The Ultimate 100-Feature Master Engine</title>
    
    <!-- External FontAwesome & Google Fonts -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #38bdf8; 
            --accent-glow: rgba(56, 189, 248, 0.4);
            --glass: rgba(255, 255, 255, 0.04); 
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
        
        * { box-sizing: border-box; margin: 0; padding: 0; scroll-behavior: smooth; color-scheme: dark; cursor: none; }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, var(--bg-dark)); 
            background-attachment: fixed;
            color: var(--text); 
            font-family: 'Inter', sans-serif; 
            overflow-x: hidden;
            transition: background 0.5s ease;
            position: relative;
        }

        #particle-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }
        header, .hero, .container, footer, .floating-controls, .rocket-top-btn, .mobile-search-float, #search-modal { position: relative; z-index: 2; }

        .cursor-dot { position: fixed; width: 8px; height: 8px; background: var(--accent); border-radius: 50%; pointer-events: none; z-index: 99999; transform: translate(-50%, -50%); transition: transform 0.05s ease; }
        .cursor-outline { position: fixed; width: 32px; height: 32px; border: 2px solid var(--accent); border-radius: 50%; pointer-events: none; z-index: 99998; transform: translate(-50%, -50%); transition: width 0.2s, height 0.2s, border-color 0.2s; box-shadow: 0 0 15px var(--accent-glow); }

        #progress-bar { position: fixed; top: 0; left: 0; height: 4px; background: var(--accent); width: 0%; z-index: 10001; box-shadow: 0 0 12px var(--accent); }

        header { background: rgba(3, 7, 18, 0.85); backdrop-filter: blur(16px); position: fixed; width: 100%; top: 0; z-index: 1000; border-bottom: 1px solid rgba(56, 189, 248, 0.2); }
        .nav-container { max-width: 1200px; margin: auto; display: flex; justify-content: space-between; align-items: center; padding: 0.8rem 2rem; }
        .logo { font-weight: 800; color: var(--accent); font-size: 1.3rem; display: flex; align-items: center; gap: 10px; letter-spacing: 0.5px; }
        
        .hud-panel { display: flex; align-items: center; gap: 12px; font-size: 0.75rem; flex-wrap: wrap; }
        .network-ticker, .weather-ticker, .session-ticker, .battery-ticker { color: var(--accent); background: rgba(56, 189, 248, 0.08); padding: 5px 10px; border-radius: 12px; border: 1px solid rgba(56, 189, 248, 0.3); display: flex; align-items: center; gap: 5px; backdrop-filter: blur(8px); }

        .status-badge { font-size: 0.75rem; background: rgba(34, 197, 94, 0.15); color: #22c55e; border: 1px solid #22c55e; padding: 3px 10px; border-radius: 20px; display: inline-flex; align-items: center; gap: 6px; }
        .status-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; box-shadow: 0 0 8px #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.4; } 100% { opacity: 1; } }

        .nav-links { display: flex; align-items: center; gap: 20px; list-style: none; }
        .nav-links a { color: var(--text); text-decoration: none; font-size: 0.95rem; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        .activity-ticker-bar { background: rgba(56, 189, 248, 0.06); border-bottom: 1px solid rgba(56, 189, 248, 0.15); padding: 8px 0; font-size: 0.82rem; color: var(--accent); overflow: hidden; white-space: nowrap; margin-top: 65px; }
        .ticker-content { display: inline-block; animation: tickerScroll 25s linear infinite; }
        @keyframes tickerScroll { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        .hero { padding: 100px 20px 60px; text-align: center; position: relative; }
        h1 { font-size: 3.8rem; font-weight: 800; background: linear-gradient(to right, #38bdf8, #818cf8, #34d399); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 15px; }
        
        .typed-text { color: var(--accent); border-right: 2px solid var(--accent); padding-right: 5px; animation: blink 0.7s infinite; }
        @keyframes blink { 50% { border-color: transparent; } }

        .vibe-ticker { font-size: 0.85rem; color: var(--text-muted); margin-top: 15px; display: inline-flex; align-items: center; gap: 8px; background: var(--glass); padding: 8px 18px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.06); backdrop-filter: blur(10px); }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; max-width: 950px; margin: 45px auto 0; }
        .stat-card { background: var(--glass); padding: 22px; border-radius: 18px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(12px); transition: 0.3s; }
        .stat-card:hover { border-color: var(--accent); box-shadow: 0 0 20px var(--accent-glow); }
        .stat-number { font-size: 2.4rem; font-weight: 800; color: var(--accent); }
        .stat-label { font-size: 0.85rem; color: var(--text-muted); margin-top: 5px; }

        .container { max-width: 1150px; margin: auto; padding: 60px 20px; opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
        .container.visible { opacity: 1; transform: translateY(0); }
        
        .section-title { font-size: 2.2rem; font-weight: 800; margin-bottom: 30px; border-bottom: 2px solid var(--accent); display: inline-block; padding-bottom: 6px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
        
        .card { background: var(--glass); padding: 30px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(16px); transition: 0.4s cubic-bezier(0.16, 1, 0.3, 1); position: relative; overflow: hidden; cursor: pointer; }
        .card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 0 30px var(--accent-glow); }

        .skills-container { max-width: 900px; margin: 40px auto 0; background: var(--glass); padding: 35px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(16px); }
        .skill-item { margin-bottom: 20px; }
        .skill-item:last-child { margin-bottom: 0; }
        .skill-info { display: flex; justify-content: space-between; font-size: 0.95rem; margin-bottom: 8px; font-weight: 600; }
        .skill-bar { width: 100%; height: 10px; background: rgba(255,255,255,0.08); border-radius: 5px; overflow: hidden; }
        .skill-progress { height: 100%; background: linear-gradient(to right, var(--accent), var(--neon-purple)); width: 0%; border-radius: 5px; transition: width 1.5s cubic-bezier(0.1, 1, 0.1, 1); box-shadow: 0 0 10px var(--accent-glow); }

        .showcase-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 22px; margin-top: 25px; }
        .media-box { background: var(--glass); border-radius: 20px; overflow: hidden; border: 1px solid rgba(255,255,255,0.08); padding: 18px; text-align: center; backdrop-filter: blur(12px); transition: 0.3s; }
        .media-box:hover { border-color: var(--accent); }
        .media-box img { width: 100%; border-radius: 14px; height: 210px; object-fit: cover; cursor: pointer; transition: 0.4s; }
        .media-box img:hover { transform: scale(1.05); }

        .btn { display: inline-flex; align-items: center; gap: 10px; padding: 14px 28px; margin: 8px; background: var(--accent); color: #030712; text-decoration: none; border-radius: 50px; font-weight: 800; transition: 0.3s; cursor: pointer; border: none; box-shadow: 0 0 15px var(--accent-glow); }
        .btn:hover { transform: scale(1.06); box-shadow: 0 0 25px var(--accent); }
        .btn-outline { background: transparent; border: 2px solid var(--accent); color: var(--accent); box-shadow: none; }
        .btn-outline:hover { background: var(--accent); color: #030712; }

        .floating-controls { position: fixed; bottom: 30px; left: 30px; display: flex; flex-direction: column; gap: 14px; z-index: 1000; }
        .float-btn { width: 50px; height: 50px; background: var(--accent); border-radius: 50%; border: none; cursor: pointer; display: flex; justify-content: center; align-items: center; color: #030712; font-size: 1.2rem; box-shadow: 0 0 20px var(--accent-glow); transition: 0.3s; }
        .float-btn:hover { transform: scale(1.15) rotate(10deg); }

        /* Rocket & Mobile Search Float Buttons */
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

        /* Quick Search Modal */
        #search-modal {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85);
            z-index: 50000; display: none; justify-content: center; align-items: flex-start; padding-top: 120px; backdrop-filter: blur(12px);
        }
        .search-box-wrap { background: #0f172a; border: 2px solid var(--accent); width: 90%; max-width: 600px; border-radius: 20px; overflow: hidden; box-shadow: 0 0 40px var(--accent-glow); }
        .search-input { width: 100%; padding: 20px; background: transparent; border: none; color: white; font-size: 1.2rem; outline: none; border-bottom: 1px solid rgba(255,255,255,0.1); }
        .search-results-list { max-height: 300px; overflow-y: auto; padding: 10px; list-style: none; }
        .search-results-list li { padding: 12px 18px; border-radius: 12px; margin-bottom: 5px; cursor: pointer; transition: 0.2s; display: flex; align-items: center; gap: 10px; }
        .search-results-list li:hover { background: rgba(56, 189, 248, 0.15); color: var(--accent); }

        /* Detailed Project Modal */
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
            h1 { font-size: 2.6rem; }
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
    <i class="fa-solid fa-bolt" style="color: var(--accent); font-size: 1.4rem;"></i>
    <div>
        <div style="font-weight: 800;">System Online: Mobile Search & Features Active</div>
        <div style="font-size: 0.85rem; color: var(--text-muted);">Welcome to Mohamed Antar's Master Engine.</div>
    </div>
</div>

<div id="lightbox" onclick="closeLightbox()">
    <img id="lightbox-img" src="" alt="Expanded Media View">
</div>

<!-- Quick Search Modal -->
<div id="search-modal" onclick="closeSearchModal(event)">
    <div class="search-box-wrap" onclick="event.stopPropagation()">
        <input type="text" class="search-input" id="search-input-box" placeholder="Type to search sections or projects (e.g. POS, Chess, Contact)..." oninput="filterSearch()">
        <ul class="search-results-list" id="search-results">
            <li onclick="scrollToSection('about')"><i class="fa-solid fa-user"></i> About Mohamed Antar</li>
            <li onclick="scrollToSection('projects')"><i class="fa-solid fa-store"></i> Future Mall POS Project</li>
            <li onclick="scrollToSection('projects')"><i class="fa-solid fa-chess-board"></i> EGYPT CHESS CLUB</li>
            <li onclick="scrollToSection('gallery')"><i class="fa-solid fa-photo-film"></i> Creative Works Showcase</li>
            <li onclick="scrollToSection('skills')"><i class="fa-solid fa-code"></i> Technical Skills & Mastery</li>
            <li onclick="scrollToSection('contact')"><i class="fa-solid fa-envelope"></i> Secure Communications & Contact</li>
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
        <a href="#" id="modal-link" class="btn" target="_blank"><i class="fa-solid fa-external-link"></i> Launch Live Preview</a>
    </div>
</div>

<header>
    <div class="nav-container">
        <div class="logo">
            <i class="fa-solid fa-terminal"></i> M. ANTAR
            <span class="status-badge"><span class="status-dot"></span> 100 Elite Status</span>
        </div>
        
        <div class="hud-panel">
            <div class="network-ticker"><i class="fa-solid fa-wifi"></i> <span id="ping-val">21</span>ms</div>
            <div class="weather-ticker"><i class="fa-solid fa-cloud-sun"></i> Mansoura: 32°C</div>
            <div class="session-ticker"><i class="fa-solid fa-clock"></i> <span id="session-time">00:00</span></div>
            <div class="battery-ticker"><i class="fa-solid fa-battery-full"></i> <span id="battery-val">100%</span></div>
        </div>

        <nav class="nav-links">
            <a href="#about"><i class="fa-solid fa-user"></i> About</a>
            <a href="#projects"><i class="fa-solid fa-layer-group"></i> Powerhouse</a>
            <a href="#gallery"><i class="fa-solid fa-photo-film"></i> Showcase</a>
            <a href="#skills"><i class="fa-solid fa-code"></i> Skills</a>
            <a href="#contact"><i class="fa-solid fa-envelope"></i> Contact</a>
        </nav>
    </div>
</header>

<div class="activity-ticker-bar">
    <div class="ticker-content">
        ⚡ <b>LIVE ACTIVITY:</b> Architecting Next-Gen Systems &nbsp;&bull;&nbsp; ♟️ Managing EGYPT CHESS CLUB &nbsp;&bull;&nbsp; 🚀 Pushing 40M+ Video Views &nbsp;&bull;&nbsp; 💻 Building Interactive POS Web Applications &nbsp;&bull;&nbsp; Press <b>Ctrl + K</b> or use mobile search!
    </div>
</div>

<section class="hero" id="about">
    <div class="container visible">
        <h1>Mohamed Antar</h1>
        <p style="font-size: 1.4rem; color: var(--text-muted);">
            Architecting <span class="typed-text" id="typed"></span>
        </p>
        
        <div class="vibe-ticker">
            <i class="fa-solid fa-compact-disc fa-spin" style="color: var(--accent);"></i> 
            <span>Active Vibe: <b>100-Feature Master Engine & Neural Code</b></span>
        </div>

        <p style="max-width: 750px; margin: 25px auto; color: #cbd5e1; line-height: 1.8;">
            A 14-year-old software architect, competitive chess organizer, and advanced video producer driving over 40M+ viral views through state-of-the-art web systems and optimized digital media engines.
        </p>
        
        <div style="margin-top: 30px;">
            <a href="https://youtube.com/@mo7amed_5272" class="btn" target="_blank"><i class="fa-brands fa-youtube"></i> MK GAMES PRO</a>
            <a href="https://youtube.com/@mo7amed_5277" class="btn btn-outline" target="_blank"><i class="fa-brands fa-youtube"></i> MK QURAN</a>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" data-target="40">0</div>
                <div class="stat-label">Million+ Global Views</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="500">0</div>
                <div class="stat-label">Production Assets Created</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="14">0</div>
                <div class="stat-label">Years of Innovation</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="100">0</div>
                <div class="stat-label">Integrated UI Features</div>
            </div>
        </div>
    </div>
</section>

<div class="container" id="projects">
    <h2 class="section-title">THE POWERHOUSE</h2>
    <div class="grid">
        <div class="card" onclick="openProjectModal('Future Mall POS', 'Full-stack retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, and multi-currency frameworks designed for peak retail efficiency.', ['Python', 'HTML/JS', 'AI Models'], 'https://github.com')">
            <h3><i class="fa-solid fa-store" style="color: var(--accent);"></i> Future Mall POS</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Full-stack retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, and multi-currency frameworks.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);">Click for details &rarr;</span>
        </div>
        <div class="card" onclick="openProjectModal('Viral Media Engine', 'Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines across major platforms.', ['Video Editing', 'Analytics', 'Media Pipelines'], 'https://youtube.com/@mo7amed_5272')">
            <h3><i class="fa-solid fa-video" style="color: var(--accent);"></i> Viral Media Engine</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);">Click for details &rarr;</span>
        </div>
        <div class="card" onclick="openProjectModal('EGYPT CHESS CLUB', 'Established and managed digital strategy communities, tactical booklets, and automated club management workflows on Chess.com to foster competitive local talent.', ['Chess Strategy', 'Community Management'], 'https://chess.com')">
            <h3><i class="fa-solid fa-chess-board" style="color: var(--accent);"></i> EGYPT CHESS CLUB</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Established and managed digital strategy communities, tactical booklets, and automated club management workflows on Chess.com.</p>
            <span style="display:inline-block; margin-top: 15px; font-size:0.8rem; color:var(--accent);">Click for details &rarr;</span>
        </div>
    </div>
</div>

<div class="container" id="skills">
    <h2 class="section-title">TECHNICAL MASTERY</h2>
    <div class="skills-container">
        <div class="skill-item">
            <div class="skill-info"><span>Python & Software Logic</span><span>95%</span></div>
            <div class="skill-bar"><div class="skill-progress" data-width="95"></div></div>
        </div>
        <div class="skill-item">
            <div class="skill-info"><span>HTML / CSS / JavaScript</span><span>90%</span></div>
            <div class="skill-bar"><div class="skill-progress" data-width="90"></div></div>
        </div>
        <div class="skill-item">
            <div class="skill-info"><span>Video Editing & Motion Graphics</span><span>96%</span></div>
            <div class="skill-bar"><div class="skill-progress" data-width="96"></div></div>
        </div>
        <div class="skill-item">
            <div class="skill-info"><span>Chess Strategy & Analytics</span><span>88%</span></div>
            <div class="skill-bar"><div class="skill-progress" data-width="88"></div></div>
        </div>
    </div>
</div>

<div class="container" id="gallery">
    <h2 class="section-title">CREATIVE SHOWCASE</h2>
    <div class="showcase-grid">
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1rem;">Asmaa Clinic UI</h3>
            <img src="IMG-20260630-WA0006.jpg" alt="Asmaa Clinic" onclick="openLightbox(this.src)">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1rem;">Minecraft Thumbnail</h3>
            <img src="Screenshot_20260815_093326.jpg" alt="Minecraft Thumbnail" onclick="openLightbox(this.src)">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1rem;">Islam: A Way of Life</h3>
            <img src="Screenshot_20260815_093338.jpg" alt="Islam Way of Life" onclick="openLightbox(this.src)">
        </div>
    </div>
</div>

<div class="container" id="contact">
    <h2 class="section-title">SECURE COMMUNICATIONS</h2>
    <div class="card" style="max-width: 650px; margin: auto; text-align: center; cursor: default;">
        <p style="margin: 12px 0;"><i class="fa-solid fa-envelope" style="color: var(--accent);"></i> Email: <span>moamedantar8@gmail.com</span></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-whatsapp" style="color: #22c55e;"></i> WhatsApp: <a href="https://wa.me/201559719175" target="_blank" style="color:var(--accent); text-decoration: none;">+20 155 971 9175</a></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-linkedin" style="color: var(--accent);"></i> LinkedIn: <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent); text-decoration: none;" target="_blank">mohamed-antar-522201406</a></p>
        <button class="btn" style="margin-top: 20px;" onclick="copyEmail()"><i class="fa-solid fa-copy"></i> Copy Secure Email</button>
    </div>
</div>

<div class="floating-controls">
    <button class="float-btn" onclick="toggleMatrixMode()" title="Toggle Matrix Green Theme"><i class="fa-solid fa-code"></i></button>
    <button class="float-btn" id="audio-toggle-btn" onclick="toggleAudioFX()" title="Toggle Cyber Click FX"><i class="fa-solid fa-volume-high"></i></button>
</div>

<!-- Rocket Top Button -->
<button class="rocket-top-btn" id="rocketBtn" onclick="launchToTop()" title="الرجوع للأعلى">
    🚀
</button>

<!-- Mobile Search Float Button -->
<button class="mobile-search-float" onclick="openSearchModalMobile()" title="بحث سريع">
    <i class="fa-solid fa-magnifying-glass"></i>
</button>

<footer>
    <p>&copy; 2026 Mohamed Antar. Built with absolute mastery, 100 integrated features, and relentless passion.</p>
</footer>

<script>
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
    let skillsAnimated = false;

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

        const skillsSec = document.getElementById('skills');
        if (skillsSec && skillsSec.getBoundingClientRect().top < window.innerHeight - 100 && !skillsAnimated) {
            document.querySelectorAll('.skill-progress').forEach(bar => {
                bar.style.width = bar.getAttribute('data-width') + '%';
            });
            skillsAnimated = true;
        }
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
        let randomPing = Math.floor(Math.random() * 6) + 19;
        document.getElementById('ping-val').textContent = randomPing;
    }, 3500);

    let totalSeconds = 0;
    setInterval(() => {
        totalSeconds++;
        let mins = Math.floor(totalSeconds / 60).toString().padStart(2, '0');
        let secs = (totalSeconds % 60).toString().padStart(2, '0');
        document.getElementById('session-time').textContent = `${mins}:${secs}`;
    }, 1000);

    if ('getBattery' in navigator) {
        navigator.getBattery().then(battery => {
            function updateBattery() {
                document.getElementById('battery-val').textContent = Math.round(battery.level * 100) + '%';
            }
            updateBattery();
            battery.addEventListener('levelchange', updateBattery);
        });
    }

    window.onload = () => {
        setTimeout(() => {
            showToast("System Online: All Features Loaded");
        }, 1000);
        startCounters();
    };

    function showToast(msg) {
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-bolt" style="color: var(--accent); font-size: 1.4rem;"></i><div><div style="font-weight: 800;">${msg}</div><div style="font-size: 0.85rem; color: var(--text-muted);">Mohamed Antar Master Engine v100.</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 4000);
    }

    const words = ["100-Feature Master Engines.", "High-Retention Media Ecosystems.", "Scalable Software Solutions."];
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
        document.body.classList.toggle('matrix-mode');
        initParticles();
    }

    function copyEmail() {
        navigator.clipboard.writeText("moamedantar8@gmail.com");
        showToast("Secured & Copied to Clipboard!");
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
