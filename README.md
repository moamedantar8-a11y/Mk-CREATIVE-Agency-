<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mohamed Antar | Ultimate Cyber Portfolio</title>
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #38bdf8; 
            --glass: rgba(255, 255, 255, 0.05); 
            --text: #f8fafc;
        }
        
        * { box-sizing: border-box; margin: 0; padding: 0; scroll-behavior: smooth; }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, #030712); 
            background-attachment: fixed;
            color: var(--text); 
            font-family: 'Segoe UI', sans-serif; 
            overflow-x: hidden;
        }

        /* Navbar */
        header { background: rgba(3, 7, 18, 0.85); backdrop-filter: blur(10px); position: fixed; width: 100%; top: 0; z-index: 1000; border-bottom: 1px solid rgba(56, 189, 248, 0.2); }
        .nav-container { max-width: 1200px; margin: auto; display: flex; justify-content: space-between; align-items: center; padding: 1rem 2rem; }
        .logo { font-weight: bold; color: var(--accent); font-size: 1.5rem; }
        .nav-links a { color: white; text-decoration: none; margin-left: 20px; font-size: 0.95rem; transition: 0.3s; }
        .nav-links a:hover { color: var(--accent); }

        /* Hero */
        .hero { padding: 150px 20px 80px; text-align: center; }
        h1 { font-size: 3.5rem; background: linear-gradient(to right, #38bdf8, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 20px; }
        
        /* Container & Cards */
        .container { max-width: 1000px; margin: auto; padding: 60px 20px; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        .card { background: var(--glass); padding: 30px; border-radius: 20px; border: 1px solid rgba(255,255,255,0.1); backdrop-filter: blur(10px); transition: 0.4s; }
        .card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 0 25px rgba(56, 189, 248, 0.3); }

        /* Gallery / Showcase */
        .showcase-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
        .media-box { background: var(--glass); border-radius: 15px; overflow: hidden; border: 1px solid rgba(255,255,255,0.1); text-align: center; padding: 15px; }
        .media-box img, .media-box video { width: 100%; border-radius: 10px; max-height: 400px; object-fit: cover; }

        /* Buttons */
        .btn { display: inline-block; padding: 12px 25px; margin: 10px; background: var(--accent); color: #030712; text-decoration: none; border-radius: 50px; font-weight: bold; transition: 0.3s; }
        .btn:hover { transform: scale(1.05); box-shadow: 0 0 15px var(--accent); }

        #theme-toggle { position: fixed; bottom: 20px; left: 20px; cursor: pointer; padding: 12px; background: var(--accent); border-radius: 50%; border: none; z-index: 1000; box-shadow: 0 0 10px rgba(0,0,0,0.5); }
    </style>
</head>
<body>

<header>
    <div class="nav-container">
        <div class="logo">Mohamed Antar</div>
        <nav class="nav-links">
            <a href="#about">About</a>
            <a href="#projects">Projects</a>
            <a href="#gallery">Showcase</a>
            <a href="#contact">Contact</a>
        </nav>
    </div>
</header>

<section class="hero" id="about">
    <h1>Mohamed Antar</h1>
    <p>Video Editor | Content Architect | Aspiring Software Engineer</p>
    <div style="margin-top: 30px;">
        <a href="https://youtube.com/@mo7amed_5272" class="btn" target="_blank">MK GAMES PRO</a>
        <a href="https://youtube.com/@mo7amed_5277" class="btn" target="_blank">MK QURAN</a>
    </div>
</section>

<div class="container" id="projects">
    <h2>OUR POWERHOUSE</h2>
    <div class="grid" style="margin-top: 20px;">
        <div class="card"><h3>Future Mall</h3><p>Full-stack retail application with role-based access.</p></div>
        <div class="card"><h3>Viral Media</h3><p>40M+ views generated through high-retention editing.</p></div>
        <div class="card"><h3>Automation</h3><p>Python-based smart workflows for maximum efficiency.</p></div>
    </div>
</div>

<div class="container" id="gallery">
    <h2>CREATIVE SHOWCASE & WORKS</h2>
    <div class="showcase-grid">
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 10px;">Asmaa Clinic Design</h3>
            <img src="IMG-20260630-WA0006.jpg" alt="Asmaa Clinic Skin Care Preview">
        </div>
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 10px;">High-Retention Reel</h3>
            <video controls poster="IMG-20260630-WA0006.jpg">
                <source src="input_file_0.mp4" type="video/mp4">
                Your browser does not support the video tag.
            </video>
        </div>
    </div>
</div>

<div class="container" id="contact">
    <h2>CONTACT INFO</h2>
    <div class="card" style="margin-top: 20px;">
        <p>📧 Email: moamedantar8@gmail.com</p>
        <p>💬 WhatsApp: +20 155 971 9175</p>
        <p>🔗 LinkedIn: <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent)" target="_blank">Profile Link</a></p>
    </div>
</div>

<button id="theme-toggle" onclick="document.body.style.filter = document.body.style.filter ? '' : 'invert(1)'">☀️</button>

</body>
</html>
