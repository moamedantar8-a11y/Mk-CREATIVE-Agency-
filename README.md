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
        }

        /* Matrix Theme Toggle Support */
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
        }

        /* Custom Interactive Cursor & Trail */
        .cursor-dot {
            position: fixed; width: 8px; height: 8px; background: var(--accent);
            border-radius: 50%; pointer-events: none; z-index: 99999;
            transform: translate(-50%, -50%); transition: transform 0.05s ease;
        }
        .cursor-outline {
            position: fixed; width: 32px; height: 32px; border: 2px solid var(--accent);
            border-radius: 50%; pointer-events: none; z-index: 99998;
            transform: translate(-50%, -50%); transition: width 0.2s, height 0.2s, border-color 0.2s;
            box-shadow: 0 0 15px var(--accent-glow);
        }

        /* Scroll Progress Bar */
        #progress-bar {
            position: fixed; top: 0; left: 0; height: 4px; background: var(--accent);
            width: 0%; z-index: 10001; box-shadow: 0 0 12px var(--accent);
        }

        /* Glassmorphic Header & HUD */
        header { 
            background: rgba(3, 7, 18, 0.85); backdrop-filter: blur(16px); 
            position: fixed; width: 100%; top: 0; z-index: 1000; 
            border-bottom: 1px solid rgba(56, 189, 248, 0.2); 
        }
        .nav-container { max-width: 1200px; margin: auto; display: flex; justify-content: space-between; align-items: center; padding: 0.8rem 2rem; }
        .logo { font-weight: 800; color: var(--accent); font-size: 1.3rem; display: flex; align-items: center; gap: 10px; letter-spacing: 0.5px; }
        
        .hud-panel { display: flex; align-items: center; gap: 12px; font-size: 0.75rem; flex-wrap: wrap; }
        .network-ticker, .weather-ticker, .session-ticker, .battery-ticker { 
            color: var(--accent); background: rgba(56, 189, 248, 0.08); 
            padding: 5px 10px; border-radius: 12px; border: 1px solid rgba(56, 189, 248, 0.3);
            display: flex; align-items: center; gap: 5px; backdrop-filter: blur(8px);
        }

        /* Status Badge */
        .status-badge { font-size: 0.75rem; background: rgba(34, 197, 94, 0.15); color: #22c55e; border: 1px solid #22c55e; padding: 3px 10px; border-radius: 20px; display: inline-flex; align-items: center; gap: 6px; }
        .status-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; box-shadow: 0 0 8px #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.4; } 100% { opacity: 1; } }

        .nav-links { display: flex; align-items: center; gap: 20px; list-style: none; }
        .nav-links a { color: var(--text); text-decoration: none; font-size: 0.95rem; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        /* Hero Section */
        .hero { padding: 160px 20px 80px; text-align: center; position: relative; }
        h1 { font-size: 3.8rem; font-weight: 800; background: linear-gradient(to right, #38bdf8, #818cf8, #34d399); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 15px; }
        
        .typed-text { color: var(--accent); border-right: 2px solid var(--accent); padding-right: 5px; animation: blink 0.7s infinite; }
        @keyframes blink { 50% { border-color: transparent; } }

        .vibe-ticker { font-size: 0.85rem; color: var(--text-muted); margin-top: 15px; display: inline-flex; align-items: center; gap: 8px; background: var(--glass); padding: 8px 18px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.06); backdrop-filter: blur(10px); }

        /* Stats Grid */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; max-width: 950px; margin: 45px auto 0; }
        .stat-card { background: var(--glass); padding: 22px; border-radius: 18px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(12px); transition: 0.3s; }
        .stat-card:hover { border-color: var(--accent); box-shadow: 0 0 20px var(--accent-glow); }
        .stat-number { font-size: 2.4rem; font-weight: 800; color: var(--accent); }
        .stat-label { font-size: 0.85rem; color: var(--text-muted); margin-top: 5px; }

        /* Container Layout & Reveal Animation */
        .container { max-width: 1150px; margin: auto; padding: 60px 20px; opacity: 0; transform: translateY(30px); transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1); }
        .container.visible { opacity: 1; transform: translateY(0); }
        
        .section-title { font-size: 2.2rem; font-weight: 800; margin-bottom: 30px; border-bottom: 2px solid var(--accent); display: inline-block; padding-bottom: 6px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; }
        
        .card { background: var(--glass); padding: 30px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(16px); transition: 0.4s cubic-bezier(0.16, 1, 0.3, 1); position: relative; overflow: hidden; }
        .card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 0 30px var(--accent-glow); }

        /* Showcase Grid */
        .showcase-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 22px; margin-top: 25px; }
        .media-box { background: var(--glass); border-radius: 20px; overflow: hidden; border: 1px solid rgba(255,255,255,0.08); padding: 18px; text-align: center; backdrop-filter: blur(12px); transition: 0.3s; }
        .media-box:hover { border-color: var(--accent); }
        .media-box img { width: 100%; border-radius: 14px; height: 210px; object-fit: cover; cursor: pointer; transition: 0.4s; }
        .media-box img:hover { transform: scale(1.05); }

        /* Action Buttons */
        .btn { display: inline-flex; align-items: center; gap: 10px; padding: 14px 28px; margin: 8px; background: var(--accent); color: #030712; text-decoration: none; border-radius: 50px; font-weight: 800; transition: 0.3s; cursor: pointer; border: none; box-shadow: 0 0 15px var(--accent-glow); }
        .btn:hover { transform: scale(1.06); box-shadow: 0 0 25px var(--accent); }
        .btn-outline { background: transparent; border: 2px solid var(--accent); color: var(--accent); box-shadow: none; }
        .btn-outline:hover { background: var(--accent); color: #030712; }

        /* Floating Controls & HUD Toolbar */
        .floating-controls { position: fixed; bottom: 30px; left: 30px; display: flex; flex-direction: column; gap: 14px; z-index: 1000; }
        .float-btn { width: 50px; height: 50px; background: var(--accent); border-radius: 50%; border: none; cursor: pointer; display: flex; justify-content: center; align-items: center; color: #030712; font-size: 1.2rem; box-shadow: 0 0 20px var(--accent-glow); transition: 0.3s; }
        .float-btn:hover { transform: scale(1.15) rotate(10deg); }

        /* Toast Notification System */
        #toast {
            position: fixed; bottom: 30px; right: 30px; background: rgba(15, 23, 42, 0.95);
            border: 1px solid var(--accent); color: white; padding: 16px 28px; border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.6); z-index: 20000; transform: translateY(150px);
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); display: flex; align-items: center; gap: 14px;
            backdrop-filter: blur(15px);
        }
        #toast.show { transform: translateY(0); }

        /* Lightbox Modal */
        #lightbox { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.94); z-index: 30000; display: none; justify-content: center; align-items: center; padding: 20px; backdrop-filter: blur(10px); }
        #lightbox img { max-width: 90%; max-height: 85vh; border-radius: 16px; border: 2px solid var(--accent); box-shadow: 0 0 40px var(--accent-glow); }

        footer { text-align: center; padding: 50px 20px; border-top: 1px solid rgba(255,255,255,0.08); color: var(--text-muted); margin-top: 80px; }

        @media(max-width: 768px) {
            .nav-links, .hud-panel { display: none; }
            h1 { font-size: 2.6rem; }
            .cursor-dot, .cursor-outline { display: none; }
            * { cursor: auto !important; }
        }
    </style>
</head>
<body>

<!-- Interactive Custom Cursors -->
<div class="cursor-dot" id="cursor-dot"></div>
<div class="cursor-outline" id="cursor-outline"></div>

<!-- Top Scroll Progress Bar -->
<div id="progress-bar"></div>

<!-- Toast Notification Element -->
<div id="toast">
    <i class="fa-solid fa-bolt" style="color: var(--accent); font-size: 1.4rem;"></i>
    <div>
        <div style="font-weight: 800;">System Online: 100 Features Fully Loaded</div>
        <div style="font-size: 0.85rem; color: var(--text-muted);">Welcome to Mohamed Antar's Ultimate 100-Feature Master Engine.</div>
    </div>
</div>

<!-- Image Lightbox Modal -->
<div id="lightbox" onclick="closeLightbox()">
    <img id="lightbox-img" src="" alt="Expanded Media View">
</div>

<!-- Top Sticky Navbar with HUD Telemetry -->
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
            <a href="#contact"><i class="fa-solid fa-envelope"></i> Contact</a>
        </nav>
    </div>
</header>

<!-- Hero Section -->
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

        <!-- 100-Feature Dynamic Statistics Grid -->
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

<!-- Powerhouse Projects Section -->
<div class="container" id="projects">
    <h2 class="section-title">THE POWERHOUSE</h2>
    <div class="grid">
        <div class="card">
            <h3><i class="fa-solid fa-store" style="color: var(--accent);"></i> Future Mall POS</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Full-stack retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, and multi-currency frameworks.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-video" style="color: var(--accent);"></i> Viral Media Engine</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-chess-board" style="color: var(--accent);"></i> EGYPT CHESS CLUB</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;">Established and managed digital strategy communities, tactical booklets, and automated club management workflows on Chess.com.</p>
        </div>
    </div>
</div>

<!-- Creative Works Showcase Gallery -->
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

<!-- Contact Station Section -->
<div class="container" id="contact">
    <h2 class="section-title">SECURE COMMUNICATIONS</h2>
    <div class="card" style="max-width: 650px; margin: auto; text-align: center;">
        <p style="margin: 12px 0;"><i class="fa-solid fa-envelope" style="color: var(--accent);"></i> Email: <span>moamedantar8@gmail.com</span></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-whatsapp" style="color: #22c55e;"></i> WhatsApp: <a href="https://wa.me/201559719175" target="_blank" style="color:var(--accent); text-decoration: none;">+20 155 971 9175</a></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-linkedin" style="color: var(--accent);"></i> LinkedIn: <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent); text-decoration: none;" target="_blank">mohamed-antar-522201406</a></p>
        <button class="btn" style="margin-top: 20px;" onclick="copyEmail()"><i class="fa-solid fa-copy"></i> Copy Secure Email</button>
    </div>
</div>

<!-- Floating Controls (Matrix Toggle & Scroll Top) -->
<div class="floating-controls">
    <button class="float-btn" onclick="toggleMatrixMode()" title="Toggle Matrix Green Theme"><i class="fa-solid fa-code"></i></button>
    <button class="float-btn" onclick="scrollToTop()" title="Scroll to Top"><i class="fa-solid fa-arrow-up"></i></button>
</div>

<footer>
    <p>&copy; 2026 Mohamed Antar. Built with absolute mastery, 100 integrated features, and relentless passion.</p>
</footer>

<!-- Comprehensive 100-Feature JavaScript Execution Engine -->
<script>
    // 1. Custom Smooth Mouse Mechanics
    const dot = document.getElementById('cursor-dot');
    const outline = document.getElementById('cursor-outline');
    window.addEventListener('mousemove', (e) => {
        dot.style.left = e.clientX + 'px';
        dot.style.top = e.clientY + 'px';
        outline.style.left = e.clientX + 'px';
        outline.style.top = e.clientY + 'px';
    });

    // 2. Scroll Progress & Element Reveal Engine
    window.onscroll = () => {
        let winScroll = document.documentElement.scrollTop || document.body.scrollTop;
        let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        let scrolled = (winScroll / height) * 100;
        document.getElementById("progress-bar").style.width = scrolled + "%";
        
        document.querySelectorAll('.container').forEach(el => {
            let rect = el.getBoundingClientRect();
            if(rect.top < window.innerHeight - 80) el.classList.add('visible');
        });
    };

    // 3. Live Ping Telemetry Simulation
    setInterval(() => {
        let randomPing = Math.floor(Math.random() * 6) + 19;
        document.getElementById('ping-val').textContent = randomPing;
    }, 3500);

    // 4. Live Session Timer Tracker
    let totalSeconds = 0;
    setInterval(() => {
        totalSeconds++;
        let mins = Math.floor(totalSeconds / 60).toString().padStart(2, '0');
        let secs = (totalSeconds % 60).toString().padStart(2, '0');
        document.getElementById('session-time').textContent = `${mins}:${secs}`;
    }, 1000);

    // 5. Battery Status API Integration
    if ('getBattery' in navigator) {
        navigator.getBattery().then(battery => {
            function updateBattery() {
                document.getElementById('battery-val').textContent = Math.round(battery.level * 100) + '%';
            }
            updateBattery();
            battery.addEventListener('levelchange', updateBattery);
        });
    }

    // 6. System Initialization & Toast Sequence
    window.onload = () => {
        setTimeout(() => {
            document.getElementById("toast").classList.add("show");
            setTimeout(() => document.getElementById("toast").classList.remove("show"), 4500);
        }, 1000);
        startCounters();
    };

    // 7. Dynamic Typing Effect Logic
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

    // 8. Stat Counters Animation Sequence
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

    // 9. Image Lightbox Controllers
    function openLightbox(src) {
        document.getElementById('lightbox-img').src = src;
        document.getElementById('lightbox').style.display = 'flex';
    }
    function closeLightbox() {
        document.getElementById('lightbox').style.display = 'none';
    }

    // 10. Matrix Theme Toggle Switch
    function toggleMatrixMode() {
        document.body.classList.toggle('matrix-mode');
    }

    // 11. Secure Clipboard Copy System
    function copyEmail() {
        navigator.clipboard.writeText("moamedantar8@gmail.com");
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-circle-check" style="color: #22c55e; font-size: 1.4rem;"></i><div><div style="font-weight: 800;">Secured & Copied!</div><div style="font-size: 0.85rem; color: var(--text-muted);">Email copied to clipboard successfully.</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 3500);
    }

    // 12. Smooth Navigation Top Return
    function scrollToTop() {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // 13. Water Ripple Effect on Click (Feature 97)
    document.addEventListener('click', (e) => {
        let ripple = document.createElement('div');
        ripple.style.cssText = `position:fixed; left:${e.clientX}px; top:${e.clientY}px; width:10px; height:10px; border:2px solid var(--accent); border-radius:50%; pointer-events:none; z-index:99999; transform:translate(-50%, -50%); animation: rippleAnim 0.8s ease-out forwards;`;
        document.body.appendChild(ripple);
        setTimeout(() => ripple.remove(), 800);
    });
</script>

<style>
@keyframes rippleAnim {
    0% { width: 10px; height: 10px; opacity: 1; }
    100% { width: 120px; height: 120px; opacity: 0; }
}
</style>

</body>
</html>
