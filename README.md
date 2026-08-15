<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK CREATIVE AGENCY | CYBER PRO</title>
    <style>
        :root { 
            --bg-dark: #030712; 
            --accent: #3b82f6; 
            --glass: rgba(255, 255, 255, 0.03); 
        }
        
        body { 
            background: radial-gradient(circle at top right, #1e1b4b, #030712); 
            background-attachment: fixed;
            color: white; 
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

        /* Hero Section */
        .hero { padding: 120px 20px; text-align: center; }
        h1 { font-size: 4.5rem; margin: 0; background: linear-gradient(to right, #60a5fa, #3b82f6); -webkit-background-clip: text; -webkit-text-fill-color: transparent; text-transform: uppercase; }
        
        .container { max-width: 1000px; margin: auto; padding: 40px 20px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        
        .card { 
            background: var(--glass); padding: 30px; border-radius: 20px; 
            border: 1px solid rgba(255,255,255,0.1); backdrop-filter: blur(15px);
            transition: 0.4s; cursor: pointer;
        }
        .card:hover { transform: translateY(-15px); border-color: var(--accent); box-shadow: 0 0 40px rgba(59, 130, 246, 0.4); }

        .cta { 
            display: block; width: fit-content; margin: 60px auto; padding: 20px 50px; 
            background: var(--accent); color: white; text-decoration: none; border-radius: 50px; 
            font-weight: 800; text-transform: uppercase; transition: 0.3s;
        }
        .cta:hover { transform: scale(1.1); box-shadow: 0 0 40px var(--accent); }

        /* Dark Mode Toggle */
        #theme-toggle { position: fixed; top: 20px; right: 20px; cursor: pointer; padding: 10px; background: var(--accent); border-radius: 50%; border: none; }
    </style>
</head>
<body>

<div id="loader"><h1>LOADING...</h1></div>

<button id="theme-toggle" onclick="toggleTheme()">☀️</button>

<div class="hero">
    <h1>MK CREATIVE AGENCY</h1>
    <p>Engineering High-Retention Digital Ecosystems.</p>
</div>

<div class="container">
    <h2>OUR POWERHOUSE</h2>
    <div class="grid">
        <div class="card"><h3>Future Mall</h3><p>Full-stack retail application with role-based access.</p></div>
        <div class="card"><h3>Viral Media</h3><p>40M+ views generated through high-retention editing.</p></div>
        <div class="card"><h3>Automation</h3><p>Python-based smart workflows for maximum efficiency.</p></div>
    </div>
</div>

<div class="container">
    <h2>TESTIMONIALS</h2>
    <div class="grid">
        <div class="card">"Mohamed's technical insight is unmatched. He engineered solutions that actually scale."</div>
        <div class="card">"The creative agency approach combined with coding expertise is exactly what we needed."</div>
    </div>
</div>

<a href="mailto:moamedantar8@gmail.com" class="cta">Request Partnership</a>

<script>
    window.onload = () => document.getElementById('loader').style.opacity = '0';
    setTimeout(() => document.getElementById('loader').style.display = 'none', 500);

    function toggleTheme() {
        document.body.style.filter = document.body.style.filter === 'invert(1)' ? 'none' : 'invert(1)';
    }
</script>

</body>
</html> 
