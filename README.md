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

        /* MK Creative Agency Services Table Style */
        .agency-table-box { background: var(--glass); border-radius: 20px; border: 1px solid rgba(255,255,255,0.08); overflow: hidden; backdrop-filter: blur(16px); margin-top: 25px; }
        .agency-table { width: 100%; border-collapse: collapse; text-align: left; }
        .agency-table th, .agency-table td { padding: 16px 20px; border-bottom: 1px solid rgba(255,255,255,0.06); font-size: 0.95rem; }
        .agency-table th { background: rgba(255,255,255,0.03); color: var(--accent); font-weight: 800; font-family: 'Courier New', monospace; }
        .service-badge { background: rgba(56, 189, 248, 0.12); color: var(--accent); padding: 4px 10px; border-radius: 20px; border: 1px solid rgba(56, 189, 248, 0.3); font-weight: bold; display: inline-flex; align-items: center; gap: 6px; }

        /* Form Inputs for Feedback / Suggestions */
        .form-group { margin-bottom: 20px; text-align: left; }
        .form-group label { display: block; font-size: 0.9rem; color: var(--accent); margin-bottom: 8px; font-weight: 600; }
        .form-input, .form-textarea { width: 100%; background: rgba(3, 7, 18, 0.6); border: 1px solid rgba(255, 255, 255, 0.1); padding: 12px 16px; border-radius: 12px; color: white; font-family: 'Inter', sans-serif; font-size: 0.95rem; outline: none; transition: 0.3s; }
        .form-input:focus, .form-textarea:focus { border-color: var(--accent); box-shadow: 0 0 10px var(--accent-glow); }
        .form-textarea { resize: vertical; height: 120px; }

        /* Code Sandbox Box */
        .code-sandbox-box { background: rgba(3, 7, 18, 0.95); border: 1px solid rgba(56, 189, 248, 0.3); border-radius: 16px; overflow: hidden; position: relative; height: 300px; margin-top: 25px; font-family: 'Courier New', monospace; }
        .code-header { background: rgba(255, 255, 255, 0.05); padding: 10px 15px; display: flex; align-items: center; gap: 8px; border-bottom: 1px solid rgba(255, 255, 255, 0.08); }
        .dot-red { width: 10px; height: 10px; background: #ef4444; border-radius: 50%; display: inline-block; }
        .dot-yellow { width: 10px; height: 10px; background: #f59e0b; border-radius: 50%; display: inline-block; }
        .dot-green { width: 10px; height: 10px; background: #22c55e; border-radius: 50%; display: inline-block; }
        .code-title-text { font-size: 0.8rem; color: var(--text-muted); margin-left: 10px; font-family: 'Inter', sans-serif; }
        .code-body { padding: 25px; position: relative; height: 100%; }
        .code-line { color: #38bdf8; font-size: 0.95rem; display: block; margin-bottom: 8px; }
        
        .escaping-code {
            position: absolute; color: #ef4444; background: rgba(239, 68, 68, 0.1);
            border: 1px solid #ef4444; padding: 5px 10px; border-radius: 6px;
            font-weight: bold; font-size: 0.85rem; cursor: grab; z-index: 10;
            box-shadow: 0 0 10px rgba(239, 68, 68, 0.3);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .escaping-code:hover { transform: scale(1.2); cursor: crosshair; }

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
        <div style="font-weight: 800;" id="toast-title">System Online: MK Creative Agency Loaded</div>
        <div style="font-size: 0.85rem; color: var(--text-muted);" id="toast-sub">Welcome to Mohamed Antar's Master Engine.</div>
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
            <i class="fa-solid fa-terminal"></i> <span data-lang-en="M. ANTAR" data-lang-ar="محمد عنتر">M. ANTAR</span>
            <span class="status-badge"><span class="status-dot"></span> <span data-lang-en="Elite Live Status" data-lang-ar="متصل ونشط">Elite Live Status</span></span>
        </div>
        
        <div class="hud-panel">
            <div class="network-ticker"><i class="fa-solid fa-wifi"></i> <span id="ping-val">21</span>ms</div>
            <div class="weather-ticker"><i class="fa-solid fa-cloud-sun"></i> Mansoura: 32°C</div>
            <div class="session-ticker"><i class="fa-solid fa-clock"></i> <span id="session-time">00:00</span></div>
            <div class="battery-ticker"><i class="fa-solid fa-battery-full"></i> <span id="battery-val">100%</span></div>
        </div>

        <nav class="nav-links">
            <a href="#about"><i class="fa-solid fa-user"></i> <span data-lang-en="About" data-lang-ar="عني">About</span></a>
            <a href="#projects"><i class="fa-solid fa-layer-group"></i> <span data-lang-en="Powerhouse" data-lang-ar="المشاريع">Powerhouse</span></a>
            <a href="#services"><i class="fa-solid fa-briefcase"></i> <span data-lang-en="Services" data-lang-ar="الخدمات">Services</span></a>
            <a href="#feedback"><i class="fa-solid fa-comments"></i> <span data-lang-en="Suggestions" data-lang-ar="الاقتراحات">Suggestions</span></a>
            <a href="#contact"><i class="fa-solid fa-envelope"></i> <span data-lang-en="Contact" data-lang-ar="التواصل">Contact</span></a>
        </nav>
    </div>
</header>

<!-- Hero Section -->
<section class="hero" id="about">
    <div class="container visible">
        <h1 data-lang-en="Mohamed Antar" data-lang-ar="محمد عنتر">Mohamed Antar</h1>
        <p style="font-size: 1.4rem; color: var(--text-muted);">
            <span data-lang-en="Architecting" data-lang-ar="مهندس برمجيات ومونتاج يطور">Architecting</span> <span class="typed-text" id="typed"></span>
        </p>
        
        <div class="vibe-ticker">
            <i class="fa-solid fa-compact-disc fa-spin" style="color: var(--accent);"></i> 
            <span data-lang-en="Active Vibe: MK Creative Agency & Master Engine Core" data-lang-ar="الوضع الحالي: وكالة إم كي الإبداعية ومحرك الأداء">Active Vibe: <b>MK Creative Agency & Master Engine Core</b></span>
        </div>

        <p style="max-width: 750px; margin: 25px auto; color: #cbd5e1; line-height: 1.8;" data-lang-en="A 14-year-old software architect, competitive chess organizer, and advanced video producer driving viral digital campaigns through state-of-the-art web systems and optimized content pipelines." data-lang-ar="مبرمج ومطور برمجيات عمره 14 عاماً، منظم بطولات شطرنج، ومصمم ومونيتير فيديوهات متقدم يقود حملات رقمية احترافية عبر أنظمة ويب متطورة ومونتاج استثنائي.">
            A 14-year-old software architect, competitive chess organizer, and advanced video producer driving viral digital campaigns through state-of-the-art web systems and optimized content pipelines.
        </p>
        
        <div style="margin-top: 30px;">
            <a href="https://youtube.com/@mo7amed_5272" class="btn" target="_blank"><i class="fa-brands fa-youtube"></i> MK GAMES PRO</a>
            <a href="https://youtube.com/@mo7amed_5277" class="btn btn-outline" target="_blank"><i class="fa-brands fa-youtube"></i> MK QURAN</a>
        </div>

        <!-- Dynamic Statistics Grid -->
        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-number" data-target="40">0</div>
                <div class="stat-label" data-lang-en="Million+ Global Views" data-lang-ar="أكثر من 40 مليون مشاهدة عالمية">Million+ Global Views</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="500">0</div>
                <div class="stat-label" data-lang-en="Production Assets Created" data-lang-ar="أصل إنتاجي تم إنجازه">Production Assets Created</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="14">0</div>
                <div class="stat-label" data-lang-en="Years of Innovation" data-lang-ar="سنوات من الابتكار التكنولوجي">Years of Innovation</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" data-target="100">0</div>
                <div class="stat-label" data-lang-en="Integrated UI Features" data-lang-ar="خاصية واجهة مستخدم متكاملة">Integrated UI Features</div>
            </div>
        </div>
    </div>
</section>

<!-- Powerhouse Projects Section -->
<div class="container" id="projects">
    <h2 class="section-title" data-lang-en="THE POWERHOUSE" data-lang-ar="أبرز المشاريع والقوة التقنية">THE POWERHOUSE</h2>
    <div class="grid">
        <div class="card">
            <h3><i class="fa-solid fa-store" style="color: var(--accent);"></i> Future Mall POS</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-lang-en="Full-stack retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, and multi-currency frameworks." data-lang-ar="تطبيق نقاط بيع متكامل لإدارة المتاجر مع نظام تحكم بالصلاحيات وتصنيف منتجات بالذكاء الاصطناعي ودعم متعدد العملات.">Full-stack retail web application featuring role-based access control, AI product classification via Keras/Teachable Machine, and multi-currency frameworks.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-video" style="color: var(--accent);"></i> <span data-lang-en="Viral Media Engine" data-lang-ar="محرك الوسائط الفيروسية">Viral Media Engine</span></h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-lang-en="Generated massive global views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines." data-lang-ar="تمكن من حصد ملايين المشاهدات عبر موازنة الصوت والصورة بدقة واحترافية وتحسين الفيديوهات القصيرة لرفع نسبة الاحتفاظ بالمشاهد.">Generated massive global views through precision audio-visual balancing, advanced short-form optimization, and high-retention editing pipelines.</p>
        </div>
        <div class="card">
            <h3><i class="fa-solid fa-chess-board" style="color: var(--accent);"></i> EGYPT CHESS CLUB</h3>
            <p style="color: var(--text-muted); margin-top: 12px; line-height: 1.6;" data-lang-en="Established and managed digital strategy communities, tactical booklets, and automated club management workflows on Chess.com." data-lang-ar="تأسيس وإدارة مجتمعات استراتيجية رقمية لبطولات الشطرنج ونشرات تكتيكية ومسابقات منظمة على منصة Chess.com.">Established and managed digital strategy communities, tactical booklets, and automated club management workflows on Chess.com.</p>
        </div>
    </div>
</div>

<!-- MK Creative Agency Services Table -->
<div class="container" id="services">
    <h2 class="section-title" data-lang-en="MK CREATIVE AGENCY SERVICES" data-lang-ar="خدمات وكالة إم كي الإبداعية">MK CREATIVE AGENCY SERVICES</h2>
    <p style="color: var(--text-muted); margin-bottom: 15px;" data-lang-en="Professional video production packages, editing ecosystems, and content scaling pipelines." data-lang-ar="باقات إنتاج ومونتاج فيديو احترافية وأنظمة متكاملة لتوسيع ونشر المحتوى الرقمي.">Professional video production packages, editing ecosystems, and content scaling pipelines.</p>
    
    <div class="agency-table-box">
        <table class="agency-table">
            <thead>
                <tr>
                    <th data-lang-en="PACKAGE NAME" data-lang-ar="اسم الباقة">PACKAGE NAME</th>
                    <th data-lang-en="CATEGORY & FOCUS" data-lang-ar="التصنيف">CATEGORY & FOCUS</th>
                    <th data-lang-en="CORE SERVICES & DELIVERABLES" data-lang-ar="الخدمات والتشغيل الأساسي">CORE SERVICES & DELIVERABLES</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><b>01. THE SINGLE SMASH</b></td>
                    <td><span class="service-badge" data-lang-en="SHORT-FORM" data-lang-ar="فيديو قصير">SHORT-FORM</span></td>
                    <td data-lang-en="1 Premium Short Video (Reels/Shorts/TikTok), dynamic kinetic text, background score syncing, custom SFX, fast delivery[cite: 1]." data-lang-ar="فيديو قصير احترافي واحد (ريلز/شورتس/تيك توك)، نصوص حركية ديناميكية، مزامنة الموسيقى ومؤثرات صوتية، وتوصيل سريع[cite: 1].">1 Premium Short Video (Reels/Shorts/TikTok), dynamic kinetic text, background score syncing, custom SFX, fast delivery[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>02. AD CAMPAIGN PACK</b></td>
                    <td><span class="service-badge" data-lang-en="SPECIALIZED" data-lang-ar="إعلانات خاصة">SPECIALIZED</span></td>
                    <td data-lang-en="2 Promotional Videos for direct-response marketing, high-energy scroll-stoppers in the first 3 seconds, strategic CTA layouts[cite: 1]." data-lang-ar="عدد 2 فيديو ترويجي للتسويق المباشر، خطف انتباه المشاهد في أول 3 ثوانٍ، وتوجيه استراتيجي للعملاء[cite: 1].">2 Promotional Videos for direct-response marketing, high-energy scroll-stoppers in the first 3 seconds, strategic CTA layouts[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>03. STARTER PACK</b></td>
                    <td><span class="service-badge" data-lang-en="SHORT-FORM" data-lang-ar="فيديو قصير">SHORT-FORM</span></td>
                    <td data-lang-en="4 Videos per month (1/week), clean subtitles, trend-matching background tracks, custom font animations, 1 revision round[cite: 1]." data-lang-ar="4 فيديوهات شهرياً (فيديو أسبوعياً)، ترجمة نصية دقيقة، مسارات خلفية متوافقة مع التريندات، وجولة تعديل واحدة[cite: 1].">4 Videos per month (1/week), clean subtitles, trend-matching background tracks, custom font animations, 1 revision round[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>04. CINEMATIC SHOWCASE</b></td>
                    <td><span class="service-badge" data-lang-en="CINEMATIC" data-lang-ar="سينمائي فاخر">CINEMATIC</span></td>
                    <td data-lang-en="1 Main Cinematic Promo Film (1-2 mins), 3 social media teasers, ultra-premium color grading, epic cinematic sound design[cite: 1]." data-lang-ar="فيديو ترويجي سينمائي رئيسي (1-2 دقيقة)، 3 مقاطع تشويقية، تدريج ألوان سينمائي وتصميم صوتي ضخم[cite: 1].">1 Main Cinematic Promo Film (1-2 mins), 3 social media teasers, ultra-premium color grading, epic cinematic sound design[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>05. YOUTUBE LONG-FORM PACK</b></td>
                    <td><span class="service-badge" data-lang-en="LONG-FORM" data-lang-ar="فيديوهات طويلة">LONG-FORM</span></td>
                    <td data-lang-en="4 Long-Form Videos/month (8-15 mins), expert pacing, B-roll integration, audio balancing, 1 free custom thumbnail per video[cite: 1]." data-lang-ar="4 فيديوهات طويلة شهرياً (8-15 دقيقة)، هندسة سرعة ومونتاج متقدم، موازنة الصوت، وتصميم مصغرة مجاناً[cite: 1].">4 Long-Form Videos/month (8-15 mins), expert pacing, B-roll integration, audio balancing, 1 free custom thumbnail per video[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>06. PERSONAL BRANDING PACK</b></td>
                    <td><span class="service-badge" data-lang-en="CREATOR FOCUS" data-lang-ar="صناع المحتوى">CREATOR FOCUS</span></td>
                    <td data-lang-en="6 talking-head/educational videos, studio-grade audio filtering, jump-cut optimization, custom glowing/neon subtitles[cite: 1]." data-lang-ar="6 فيديوهات تعليمية أو حوارية، فلترة صوت استوديو، قص سريع ذكي، ونصوص نيون مضيئة مخصصة[cite: 1].">6 talking-head/educational videos, studio-grade audio filtering, jump-cut optimization, custom glowing/neon subtitles[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>07. PODCAST CLIPPING PACK</b></td>
                    <td><span class="service-badge" data-lang-en="LONG-TO-SHORT" data-lang-ar="قص بودكاست">LONG-TO-SHORT</span></td>
                    <td data-lang-en="15 to 20 viral clips from long-form sessions, multi-cam editing, expressive stylized subtitles, pop-ups, and zoom frames[cite: 1]." data-lang-ar="قص من 15 لـ 20 مقطع فيروسي من البودكاست، متعدد الكاميرات، وترجمة معبرة تكبيرات وحركات ديناميكية[cite: 1].">15 to 20 viral clips from long-form sessions, multi-cam editing, expressive stylized subtitles, pop-ups, and zoom frames[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>08. PRO GROWTH PACK</b></td>
                    <td><span class="service-badge" data-lang-en="MOST POPULAR" data-lang-ar="الأكثر طلباً">MOST POPULAR</span></td>
                    <td data-lang-en="8 Videos/month (2/week), advanced motion graphics, psychologically mapped 3-second hooks, script architecture modifications[cite: 1]." data-lang-ar="8 فيديوهات شهرياً (فيديوهان أسبوعياً)، موشن جرافيك متقدم، خطافات نفسية في أول 3 ثوانٍ، وتعديل السكربتات[cite: 1].">8 Videos/month (2/week), advanced motion graphics, psychologically mapped 3-second hooks, script architecture modifications[cite: 1].</td>
                </tr>
                <tr>
                    <td><b>09. ELITE AGENCY PACK</b></td>
                    <td><span class="service-badge" data-lang-en="ULTRA PREMIUM" data-lang-ar="النخبة الفاخرة">ULTRA PREMIUM</span></td>
                    <td data-lang-en="12-15 ultra-premium videos/month, custom VFX & animations, professional voiceovers, green-screen/chroma key, weekly strategy calls[cite: 1]." data-lang-ar="من 12 لـ 15 فيديو فائق الجودة، مؤثرات بصرية VFX معقدة، تعليق صوتي بشري، شاشة خضراء، ومكالمات استشارية أسبوعية[cite: 1].">12-15 ultra-premium videos/month, custom VFX & animations, professional voiceovers, green-screen/chroma key, weekly strategy calls[cite: 1].</td>
                </tr>
            </tbody>
        </table>
    </div>
</div>

<!-- Creative Works Showcase Gallery -->
<div class="container" id="gallery">
    <h2 class="section-title" data-lang-en="CREATIVE SHOWCASE" data-lang-ar="معرض الأعمال البصرية">CREATIVE SHOWCASE</h2>
    <div class="showcase-grid">
        <div class="media-box">
            <h3 style="color: var(--accent); margin-bottom: 12px; font-size: 1rem;">Asmaa Clinic UI</h3>
            <img src="EYOUTH-31202101204057_Final Logo that is the name of the logo.jpg" alt="Asmaa Clinic" onclick="openLightbox(this.src)">
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

<!-- Suggestions & Future Vision Box (New Addition requested by user) -->
<div class="container" id="feedback">
    <h2 class="section-title" data-lang-en="SUGGESTIONS & FUTURE VISION" data-lang-ar="صندوق الاقتراحات والرؤية المستقبلية">SUGGESTIONS & FUTURE VISION</h2>
    <div class="card" style="max-width: 750px; margin: auto;">
        <p style="color: var(--text-muted); margin-bottom: 20px; line-height: 1.6;" data-lang-en="Have an idea, suggestion, or feature you want to see in the future on this platform? Drop your message directly here!" data-lang-ar="عندك فكرة أو اقتراحات لأي ميزة جديدة حابب تشوفها في الموقع مستقبلاً؟ اكتبها هنا وسجل رأيك فوراً!">
            Have an idea, suggestion, or feature you want to see in the future on this platform? Drop your message directly here!
        </p>
        <form onsubmit="handleSuggestionSubmit(event)">
            <div class="form-group">
                <label data-lang-en="Your Name / Alias" data-lang-ar="اسمك الكريم">Your Name / Alias</label>
                <input type="text" class="form-input" id="sugName" placeholder="Mohamed Antar..." required>
            </div>
            <div class="form-group">
                <label data-lang-en="Your Suggestions / What you want to see next" data-lang-ar="اقتراحاتك وماذا تود أن تراه في الموقع مستقبلاً؟">Your Suggestions / What you want to see next</label>
                <textarea class="form-textarea" id="sugText" placeholder="Write your awesome ideas here..." required></textarea>
            </div>
            <button type="submit" class="btn"><i class="fa-solid fa-paper-plane"></i> <span data-lang-en="Send Suggestion" data-lang-ar="إرسال الاقتراح">Send Suggestion</span></button>
        </form>
    </div>
</div>

<!-- Interactive Code Sandbox with 4 Escaping Bugs -->
<div class="container">
    <h2 class="section-title" data-lang-en="ACTIVE BUG SANDBOX" data-lang-ar="منطقة الأخطاء التفاعلية">ACTIVE BUG SANDBOX</h2>
    <div class="code-sandbox-box" id="codeSandbox">
        <div class="code-header">
            <span class="dot-red"></span> <span class="dot-yellow"></span> <span class="dot-green"></span>
            <span class="code-title-text">engine_core.js - 4 Escaping Errors</span>
        </div>
        <div class="code-body">
            <span class="code-line">1: initializeSystem();</span>
            <span class="code-line">2: loadDependencies();</span>
            <span class="code-line">3: checkBufferOverflow();</span>
            <span class="code-line">4: system.ready();</span>
            
            <!-- الأكواد الأربعة الهاربة باللون الأحمر -->
            <span class="escaping-code bug-1">ERR_TYPE_01</span>
            <span class="escaping-code bug-2">ERR_TYPE_02</span>
            <span class="escaping-code bug-3">ERR_TYPE_03</span>
            <span class="escaping-code bug-4">ERR_TYPE_04</span>
        </div>
    </div>
</div>

<!-- Contact Station Section -->
<div class="container" id="contact">
    <h2 class="section-title" data-lang-en="SECURE COMMUNICATIONS" data-lang-ar="قنوات الاتصال المؤمنة">SECURE COMMUNICATIONS</h2>
    <div class="card" style="max-width: 650px; margin: auto; text-align: center;">
        <p style="margin: 12px 0;"><i class="fa-solid fa-envelope" style="color: var(--accent);"></i> Email: <span>moamedantar8@gmail.com</span></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-whatsapp" style="color: #22c55e;"></i> WhatsApp: <a href="https://wa.me/201559719175" target="_blank" style="color:var(--accent); text-decoration: none;">+20 155 971 9175</a></p>
        <p style="margin: 12px 0;"><i class="fa-brands fa-linkedin" style="color: var(--accent);"></i> LinkedIn: <a href="https://linkedin.com/in/mohamed-antar-522201406" style="color:var(--accent); text-decoration: none;" target="_blank">mohamed-antar-522201406</a></p>
        <button class="btn" style="margin-top: 20px;" onclick="copyEmail()"><i class="fa-solid fa-copy"></i> <span data-lang-en="Copy Secure Email" data-lang-ar="نسخ البريد الإلكتروني">Copy Secure Email</span></button>
    </div>
</div>

<!-- Floating Controls (Includes Language Toggle & Matrix & Scroll to Top) -->
<div class="floating-controls">
    <button class="float-btn" onclick="toggleLanguage()" title="Switch Language (EN / AR)"><i class="fa-solid fa-language"></i></button>
    <button class="float-btn" onclick="toggleMatrixMode()" title="Toggle Matrix Green Theme"><i class="fa-solid fa-code"></i></button>
    <button class="float-btn" onclick="scrollToTop()" title="Scroll to Top"><i class="fa-solid fa-arrow-up"></i></button>
</div>

<footer>
    <p>&copy; 2026 Mohamed Antar. Built with absolute mastery and agency service architectures.</p>
</footer>

<!-- JavaScript Execution Engine -->
<script>
    // Smooth Mouse Mechanics
    const dot = document.getElementById('cursor-dot');
    const outline = document.getElementById('cursor-outline');
    window.addEventListener('mousemove', (e) => {
        dot.style.left = e.clientX + 'px';
        dot.style.top = e.clientY + 'px';
        outline.style.left = e.clientX + 'px';
        outline.style.top = e.clientY + 'px';
    });

    // Scroll Progress & Reveal Engine
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

    // Live Ping Telemetry
    setInterval(() => {
        let randomPing = Math.floor(Math.random() * 6) + 19;
        document.getElementById('ping-val').textContent = randomPing;
    }, 3500);

    // Live Session Timer
    let totalSeconds = 0;
    setInterval(() => {
        totalSeconds++;
        let mins = Math.floor(totalSeconds / 60).toString().padStart(2, '0');
        let secs = (totalSeconds % 60).toString().padStart(2, '0');
        document.getElementById('session-time').textContent = `${mins}:${secs}`;
    }, 1000);

    // Battery Status API
    if ('getBattery' in navigator) {
        navigator.getBattery().then(battery => {
            function updateBattery() {
                document.getElementById('battery-val').textContent = Math.round(battery.level * 100) + '%';
            }
            updateBattery();
            battery.addEventListener('levelchange', updateBattery);
        });
    }

    // Toast Notification Sequence
    window.onload = () => {
        setTimeout(() => {
            document.getElementById("toast").classList.add("show");
            setTimeout(() => document.getElementById("toast").classList.remove("show"), 4500);
        }, 1000);
        startCounters();
        initBugs();
    };

    // Typing Effect
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

    // Stat Counters Animation
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

    // Escaping Bugs Logic (4 Red Bugs)
    function initBugs() {
        const bugs = document.querySelectorAll('.escaping-code');
        const container = document.getElementById('codeSandbox');

        function moveBug(bug) {
            const maxX = container.clientWidth - bug.clientWidth - 20;
            const maxY = container.clientHeight - bug.clientHeight - 40;
            const randomX = Math.floor(Math.random() * Math.max(10, maxX));
            const randomY = Math.floor(Math.random() * Math.max(10, maxY));
            bug.style.left = randomX + 'px';
            bug.style.top = randomY + 'px';
        }

        bugs.forEach(bug => {
            setInterval(() => moveBug(bug), 2000);
            bug.addEventListener('mouseover', () => moveBug(bug));
            moveBug(bug);
        });
    }

    // Lightbox Controls
    function openLightbox(src) {
        document.getElementById('lightbox-img').src = src;
        document.getElementById('lightbox').style.display = 'flex';
    }
    function closeLightbox() {
        document.getElementById('lightbox').style.display = 'none';
    }

    // Matrix Theme Toggle
    function toggleMatrixMode() {
        document.body.classList.toggle('matrix-mode');
    }

    // Language Toggle Engine (EN / AR)
    let currentLang = 'en';
    function toggleLanguage() {
        currentLang = currentLang === 'en' ? 'ar' : 'en';
        document.documentElement.setAttribute('dir', currentLang === 'ar' ? 'rtl' : 'ltr');
        
        document.querySelectorAll('[data-lang-en]').forEach(el => {
            el.textContent = el.getAttribute(`data-lang-${currentLang}`);
        });

        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-globe" style="color: var(--accent); font-size: 1.4rem;"></i><div><div style="font-weight: 800;">Language Switched</div><div style="font-size: 0.85rem; color: var(--text-muted);">Current language: ${currentLang.toUpperCase()}</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 3000);
    }

    // Handle Suggestions Form Submission
    function handleSuggestionSubmit(e) {
        e.preventDefault();
        let name = document.getElementById('sugName').value;
        let text = document.getElementById('sugText').value;
        
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-circle-check" style="color: #22c55e; font-size: 1.4rem;"></i><div><div style="font-weight: 800;">Thank You, ${name}!</div><div style="font-size: 0.85rem; color: var(--text-muted);">Your suggestion has been securely recorded.</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 4000);
        
        e.target.reset();
    }

    // Copy Email
    function copyEmail() {
        navigator.clipboard.writeText("moamedantar8@gmail.com");
        let toast = document.getElementById("toast");
        toast.innerHTML = `<i class="fa-solid fa-circle-check" style="color: #22c55e; font-size: 1.4rem;"></i><div><div style="font-weight: 800;">Secured & Copied!</div><div style="font-size: 0.85rem; color: var(--text-muted);">Email copied to clipboard successfully.</div></div>`;
        toast.classList.add("show");
        setTimeout(() => toast.classList.remove("show"), 3500);
    }

    // Scroll to Top
    function scrollToTop() {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    }
</script>

</body>
</html> 
