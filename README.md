<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mohamed Antar | Cyber Pro Portfolio</title>
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #38bdf8; 
            --glass: rgba(255, 255, 255, 0.05); 
            --text: #f8fafc;
        }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, #030712); 
            background-attachment: fixed;
            color: var(--text); 
            font-family: 'Segoe UI', sans-serif; 
            margin: 0; 
            overflow-x: hidden;
        }

        /* Loading Screen */
        #loader {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #030712; z-index: 9999; display: flex; justify-content: center; align-items: center;
            transition: opacity 0.5s;
        }

        /* Elements */
        .container { max-width: 1000px; margin: auto; padding: 80px 20px; }
        h1 { font-size: 3.5rem; margin: 0; background: linear-gradient(to right, #38bdf8, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-transform: uppercase; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        
        .card { 
            background: var(--glass); padding: 30px; border-radius: 20px; 
            border: 1px solid rgba(255,255,255,0.1); backdrop-filter: blur(15px);
            transition: 0.4s;
        }
        .card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 0 30px rgba(56, 189, 248, 0.3); }

        .btn { 
            display: inline-block; padding: 15px 30px; margin: 10px;
            background: var(--accent); color: white; text-decoration: none; border-radius: 50px; 
            font-weight: bold; transition: 0.3s;
        }
        .btn:hover { transform: scale(1.05); box-shadow: 0 0 20px var(--accent); }

        #theme-toggle { position: fixed; top: 20px; right: 20px; cursor: pointer; padding: 10px; background: var(--accent); border-radius: 50%; border: none; }
    </style>
</head>
<body>

<div id="loader"><h1>LOADING CYBER PORTFOLIO...</h1></div>

<button id="theme-toggle" onclick="toggleTheme()">☀️</button>

<div class="container" style="text-align: center;">
    <h1>Mohamed Antar</h1>
    <p>Video Editor | Content Architect | Aspiring Software Engineer</p>
    <div style="margin-top: 30px;">
        <a href="https://youtube.com/@mo7amed_5272" class="btn">MK GAMES PRO</a>
        <a href="https://youtube.com/@mo7amed_5277" class="btn">MK QURAN</a>
        <a href="mailto:moamedantar8@gmail.com" class="btn">Email Me</a>
    </div>
</div>

<div class="container">
    <h2>OUR POWERHOUSE</h2>
    <div class="grid">
        <div class="card"><h3>Future Mall</h3><p>Full-stack retail application with role-based access.</p></div>
        <div class="card"><h3>Content Growth</h3><p>40M+ views generated through high-retention editing.</p></div>
        <div class="card"><h3>Automation</h3><p>Python-based smart workflows for maximum efficiency.</p></div>
    </div>
</div>

<div class="container">
    <h2>EXPERIENCE</h2>
    <div class="grid">
        <div class="card"><h3>Lead Media Engineer</h3><p>MK GAMES PRO (450+ videos published).</p></div>
        <div class="card"><h3>Software Developer</h3><p>Building scalable systems using Python, HTML, CSS.</p></div>
    </div>
</div>

<script>
    window.onload = () => document.getElementById('loader').style.opacity = '0';
    setTimeout(() => document.getElementById('loader').style.display = 'none', 500);

    function toggleTheme() {
        document.body.style.filter = document.body.style.filter === 'invert(1)' ? 'none' : 'invert(1)';
    }
</script>

</body>
</html>
