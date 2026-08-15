<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MK CREATIVE AGENCY | CYBER EDITION</title>
    <style>
        :root { 
            --bg-grad: linear-gradient(135deg, #0f172a, #1e1b4b, #030712); 
            --accent: #3b82f6; 
            --glass: rgba(255, 255, 255, 0.05); 
        }
        
        body { 
            background: var(--bg-grad); 
            background-attachment: fixed;
            color: white; 
            font-family: 'Segoe UI', sans-serif; 
            margin: 0; 
        }

        .hero { padding: 120px 20px; text-align: center; }
        h1 { font-size: 4rem; margin: 0; background: linear-gradient(to right, #60a5fa, #3b82f6); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        .container { max-width: 1000px; margin: auto; padding: 40px 20px; }
        
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 30px; }
        
        .card { 
            background: var(--glass); 
            padding: 30px; 
            border-radius: 20px; 
            border: 1px solid rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            transition: 0.4s;
        }
        .card:hover { transform: translateY(-10px); border-color: var(--accent); box-shadow: 0 0 30px rgba(59, 130, 246, 0.3); }

        .cta { 
            display: block; width: fit-content; margin: 60px auto; padding: 20px 50px; 
            background: var(--accent); color: white; text-decoration: none; border-radius: 50px; 
            font-weight: 800; text-transform: uppercase; transition: 0.3s;
        }
        .cta:hover { transform: scale(1.1); box-shadow: 0 0 30px var(--accent); }
    </style>
</head>
<body>

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

</body>
</html>
