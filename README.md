<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mohamed Antar | Ultimate Cyber Portfolio</title>
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #38bdf8; 
            --accent-glow: rgba(56, 189, 248, 0.4);
            --glass: rgba(255, 255, 255, 0.04); 
            --text: #f8fafc;
            --text-muted: #94a3b8;
        }
        
        * { box-sizing: border-box; margin: 0; padding: 0; scroll-behavior: smooth; }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, #030712); 
            background-attachment: fixed;
            color: var(--text); 
            font-family: 'Segoe UI', sans-serif; 
            overflow-x: hidden;
            transition: filter 0.3s ease;
        }

        /* 1. Scroll Progress Bar */
        #progress-bar {
            position: fixed; top: 0; left: 0; height: 4px; background: var(--accent);
            width: 0%; z-index: 1001; box-shadow: 0 0 10px var(--accent);
        }

        /* Navbar */
        header { background: rgba(3, 7, 18, 0.85); backdrop-filter: blur(12px); position: fixed; width: 100%; top: 0; z-index: 1000; border-bottom: 1px solid rgba(56, 189, 248, 0.2); }
        .nav-container { max-width: 1200px; margin: auto; display: flex; justify-content: space-between; align-items: center; padding: 1rem 2rem; }
        .logo { font-weight: bold; color: var(--accent); font-size: 1.5rem; display: flex; align-items: center; gap: 10px; }
        
        /* Freelance Status Badge */
        .status-badge { font-size: 0.75rem; background: rgba(34, 197, 94, 0.15); color: #22c55e; border: 1px solid #22c55e; padding: 3px 10px; border-radius: 20px; display: inline-flex; align-items: center; gap: 6px; }
        .status-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; box-shadow: 0 0 8px #22c55e; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.4; } 100% { opacity: 1; } }

        .nav-links { display: flex; align-items: center; gap: 20px; list-style: none; }
        .nav-links a { color: var(--text); text-decoration: none; font-size: 0.95rem; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        /* Hero */
        .hero { padding: 160px 20px 80px; text-align: center; position: relative; }
        h1 { font-size: 3.8rem; background: linear-gradient(to right, #38bdf8, #818cf8, #34d399); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 15px; }
        .typed-text { color: var(--accent); border-right: 2px solid var(--accent); padding-right: 5px; animation: blink 0.7s infinite; }
        @keyframes blink { 50% { border-color: transparent; } }

        /* Animated Stats Counter */
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; max-width: 900px; margin: 40px auto 0; }
        .stat-card { background: var(--glass); padding: 20px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(10px); }
        .stat-number { font-size: 2.2rem; font-weight: bold; color: var(--accent); }
        .stat-label { font-size: 0.9rem; color: var(--text-muted); }

        /* Container & Cards */
        .container { max-width: 1100px; margin: auto; padding: 60px 20px; }
        .section-title { font-size: 2.2rem; margin-bottom: 30px; border-bottom: 2px solid var(--accent); display: inline-block; padding-bottom: 5px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        .card { background: var(--glass); padding: 30px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.08); backdrop-filter: blur(12px); transition: 0.4s; position: relative; overflow: hidden; }
        .card:hover { transform: translateY(-8px); border-color: var(--accent); box-shadow: 0 0 30px var(--accent-glow); }

        /* Gallery / Showcase */
        .showcase-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 25px; margin-top: 20px; }
        .media-box { background: var(--glass); border-radius: 20px; overflow: hidden; border: 1px solid rgba(255,255,255,0.08); padding: 20px; text-align: center; }
        .media-box img, .media-box video { width: 100%; border-radius: 12px; height: 220px; object-fit: cover; cursor: pointer; transition: 0.3s; }
        .media-box img:hover, .media-box video:hover { transform: scale(1.03); }

        /* Buttons & Actions */
        .btn { display: inline-flex; align-items: center; gap: 10px; padding: 12px 28px; margin: 8px; background: var(--accent); color: #030712; text-decoration: none; border-radius: 50px; font-weight: bold; transition: 0.3s; cursor: pointer; border: none; }
        .btn:hover { transform: scale(1.05); box-shadow: 0 0 20px var(--accent); }
        .btn-outline { background: transparent; border: 2px solid var(--accent); color: var(--accent); }
        .btn-outline:hover { background: var(--accent); color: #030712; }

        /* Toast Notification */
        #toast {
            position: fixed; bottom: 30px; right: 30px; background: rgba(15, 23, 42, 0.95);
            border: 1px solid var(--accent); color: white; padding: 15px 25px; border-radius: 12px;
            box-shadow: 0 5px 25px rgba(0,0,0,0.5); z-index: 10000; transform: translateY(150px);
            transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); display: flex; align-items: center; gap: 12px;
        }
        #toast.show { transform: translateY(0); }

        /* Floating Utilities */
        .floating-controls { position: fixed; bottom: 25px; left: 25px; display: flex; flex-direction: column; gap: 12px; z-index: 1000; }
        .float-btn { width: 45px; height: 45px; background: var(--accent); border-radius: 50%; border: none; cursor: pointer; display: flex; justify-content: center; align-items: center; color: #030712; font-size: 1.1rem; box-shadow: 0 0 15px var(--accent-glow); transition: 0.3s; }
        .float-btn:hover { transform: scale(1.15); }

        /* Lightbox Modal */
        #lightbox { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.92); z-index: 20000; display: none; justify-content: center; align-items: center; padding: 20px; }
        #lightbox img { max-width: 90%; max-height: 90vh; border-radius: 10px; border: 2px solid var(--accent); box-shadow: 0 0 30px var(--accent-glow); }

        footer { text-align: center; padding: 40px 20px; border-top: 1px solid rgba(255,255,255,0.08); color: var(--text-muted); margin-top: 60px; }

        @media(max-width: 768px) {
            .nav-links { display: none; }
            h1 { font-size: 2.5rem; }
        }
    </style>
</head>
<body>

<!-- Scroll Progress Bar -->
<div id="progress-bar"></div>

<!-- Welcome Toast Notification -->
<div id="toast">
    <i class="fa-solid fa-rocket" style="color: var(--accent); font-size: 1.3rem;"></i>
    <div>
        <div style="font-weight: bold;">Welcome to the 40-Feature Elite Site!</div>
        <div style="font-size: 0.85rem; color: var(--text-muted);">Explore Mohamed Antar's Ultimate Cyber Portfolio.</div>
    </div>
</div>

<!-- Lightbox Container -->
<div id="lightbox" onclick="closeLightbox()">
    <img id="lightbox-img" src="" alt="Zoomed View">
</div>

<!-- Header / Navbar -->
<header>
    <div class="nav-container">
        <div class="logo">
            <i class="fa-solid fa-code"></i> Mohamed Antar
            <span class="status-badge"><span class="status-dot"></span> Available for Work</span>
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
    <div class="container">
        <h1>Mohamed Antar</h1>
        <p style="font-size: 1.3rem; color: var(--text-muted);">
            Architecting <span class="typed-text" id="typed"></span>
        </p>
        <p style="max-width: 700px; margin: 20px auto; color: #cbd5e1; line-height: 1.7;">
            A 14-year-old tech builder, video editor, and software engineer merging high-retention digital media pipelines with robust web architectures.
        </p>
        
        <div style="margin-top: 30px;">
            <a href="https://youtube.com/@mo7amed_5272" class="btn" target="_blank"><i class="fa-brands fa-youtube"></i> MK GAMES PRO</a>
            <a href="https://youtube.com/@mo7amed_5277" class="btn btn-outline" target="_blank"><i class="fa-brands fa-youtube"></i> MK QURAN</a>
        </div>

        <!-- Animated Stats Counter -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" data-target="40">0</div>
                <div class="stat-label">Million+ Views & Remixes</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="450">0</div>
                <div class="stat-label">Published Videos</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="14">0</div>
                <div class="stat-label">Years Old Developer</div>
            </div>
        </div>
    </div>
</section>

<!-- Projects Powerhouse -->
<div class="container" id="projects">
    <h2 class="section-title">OUR POWERHOUSE</h2>
    <div class="grid" style="margin-top: 20px;">
        <div class="card">
            <h3><i class="fa-solid fa-store" style="color: var(--accent);"></i> Future Mall</h3>
            <p style="color: var(--text-muted); margin-top: 10px;">Full-stack retail web application featuring role-based access control, AI product classification, and multi-currency support.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-video" style="color: var(--accent);"></i> Viral Media Engine</h3>
            <p style="color: var(--text-muted); margin-top: 10px;">Generated over 40M+ views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-terminal" style="color: var(--accent);"></i> Python Automation</h3>
            <p style="color: var(--text-muted); margin-top: 10px;">Custom backend scripts and smart automation workflows built for maximum production efficiency and AI model integrations.</p>
        </div>
    </div>
</div>

<!-- Creative Showcase Gallery (Including Minecraft & Islam designs) -->
<div class="container" id="gallery">
    <h2 class="section-title">CREATIVE SHOWCASE & WORKS</h2>
    <div class="showcase-grid">
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1.1rem;">Asmaa Clinic Design</h3>
            <img src="IMG-20260630-WA0006.jpg" alt="Asmaa Clinic" onclick="openLightbox(this.src)">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1.1rem;">Minecraft Thumbnail</h3>
            <img src="Screenshot_20260815_093326.jpg" alt="Minecraft Thumbnail" onclick="openLightbox(this.src)">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1.1rem;">Islam: A Way of Life (1)</h3>
            <img src="Screenshot_20260815_093338.jpg" alt="Islam Way of Life 1" onclick="openLightbox(this.src)">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1.1rem;">Islam: A Way of Life (2)</h3>
            <img src="Screenshot_20260815_093346.jpg" alt="Islam Way of Life 2" onclick="openLightbox(this.src)">
        </div>
    </div>
</div>

<!-- Contact Section -->
<div class="container" id="contact">
    <h2 class="section-title">CONTACT INFO</h2>
    <div class="card" style="margin-top: 20px; max-width: 600px; margin-left: auto; margin-right: auto; text-align: center;">
        <p style="margin: 10px 0;"><i class="fa-solid fa-envelope" style="color: var(--accent);"></i> Email: <span id="email-text">moamedantar8@gmail.com</span></p>
        <p style="margin: 10px 0;"><i class="fa-brands fa-whatsapp" style="color: #22c55e;"></i> WhatsApp: <a href="https://wa.me/201559719175" target="_blank" style="color:var(--accent); text-decoration: none;">+20 155 971 9175</a></p>
        <p style="margin: 10px 0;"><i class="fa-brands fa-linkedin" style="color: var(--accent);"></i> LinkedIn: <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent); text-decoration: none;" target="_blank">mohamed-antar-522201406</a></p>
        <button class="btn" style="margin-top: 20px;" onclick="copyEmail()"><i class="fa-solid fa-copy"></i> Copy Email Address</button>
    </div>
</div>

<!-- Floating Controls -->
<div class="floating-controls">
    <button class="float-btn" onclick="toggleTheme()" title="Toggle Light/Dark Theme"><i class="fa-solid fa-circle-half-stroke"></i></button>
    <button class="float-btn" onclick="scrollToTop()" title="Back to Top"><i class="fa-solid fa-arrow-up"></i></button>
</div>

<footer>
    <p>&copy; 2026 Mohamed Antar. Built with absolute precision, code, and passion.</p>
</footer>

<!-- JavaScript Enhancements -->
<script>
    window.onscroll = () => {
        let winScroll = document.documentElement.scrollTop || document.body.scrollTop;
        let height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
        let scrolled = (winScroll / height) * 100;
        document.getElementById("progress-bar").style.width = scrolled + "%";
    };

    window.onload = () => {
        setTimeout(() => {
            document.getElementById("toast").classList.add("show");
            setTimeout(() => {
                document.getElementById("toast").classList.remove("show");
            }, 4000);
        }, 1000);
        
        startCounters();
    };

    const words = ["High-Retention Digital Ecosystems.", "Scalable Software Solutions.", "Cinematic Video Productions."];
    let i = 0, j = 0, currentWord = "", isDeleting = false;
    function typeEffect() {
        currentWord = words[i];
        if (isDeleting) {
            document.getElementById("typed").textContent = currentWord.substring(0, j-1);
            j--;
            if (j == 0) { isDeleting = false; i = (i + 1) % words.length; }
        } else {
            document.getElementById("typed").textContent = currentWord.substring(0, j+1);
            j++;
            if (j == currentWord.length) { isDeleting = true; setTimeout(typeEffect, 2000); return; }
        }
        setTimeout(typeEffect, isDeleting ? 50 : 100);
    }
    typeEffect();

    function startCounters() {
        const counters = document.querySelectorAll('.stat-number');
        counters.forEach(counter => {
            const target = +counter.getAttribute('data-target');
            let count = 0;
            const speed = target / 50;
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

    function copyEmail() {
        navigator.clipboard.writeText("moamedantar8@gmail.com");
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-check-circle" style="color: #22c55e; font-size: 1.3rem;"></i><div><div style="font-weight: bold;">Copied!</div><div style="font-size: 0.85rem; color: var(--text-muted);">Email copied to clipboard successfully.</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 3000);
    }

    function toggleTheme() {
        document.body.style.filter = document.body.style.filter === 'invert(1) hue-rotate(180deg)' ? 'none' : 'invert(1) hue-rotate(180deg)';
    }

    function scrollToTop() {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }
</script>

</body>
</html> 
