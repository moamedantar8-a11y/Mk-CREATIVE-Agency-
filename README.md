<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MK AI Tools</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Cairo:wght@300;400;600;700&family=Rajdhani:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --neon-blue: #00d4ff;
  --neon-purple: #b14aed;
  --neon-pink: #ff2d78;
  --dark-bg: #050a14;
  --dark-surface: #0a1628;
  --dark-card: #0d1f3c;
  --dark-border: #1a3a5c;
  --text-primary: #e8f4ff;
  --text-secondary: #7aa8d0;
  --text-muted: #3d6080;
  --glow-blue: 0 0 20px rgba(0,212,255,0.4), 0 0 60px rgba(0,212,255,0.1);
  --glow-purple: 0 0 20px rgba(177,74,237,0.4), 0 0 60px rgba(177,74,237,0.1);
  --grid-color: rgba(0,212,255,0.03);
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: 'Cairo', sans-serif;
  background: var(--dark-bg);
  color: var(--text-primary);
  min-height: 100vh;
  overflow-x: hidden;
}

/* Animated grid background */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    linear-gradient(rgba(0,212,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,212,255,0.04) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: gridMove 20s linear infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes gridMove {
  0% { transform: translateY(0); }
  100% { transform: translateY(50px); }
}

/* Floating orbs */
.orb {
  position: fixed;
  border-radius: 50%;
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
  animation: orbFloat 8s ease-in-out infinite;
}
.orb-1 { width: 400px; height: 400px; background: rgba(0,212,255,0.06); top: -100px; left: -100px; animation-delay: 0s; }
.orb-2 { width: 350px; height: 350px; background: rgba(177,74,237,0.06); bottom: -100px; right: -100px; animation-delay: -4s; }
.orb-3 { width: 250px; height: 250px; background: rgba(255,45,120,0.04); top: 50%; left: 50%; animation-delay: -2s; }

@keyframes orbFloat {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(30px, -30px); }
}

/* HEADER */
header {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 16px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(5,10,20,0.85);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(0,212,255,0.1);
}

.logo {
  font-family: 'Orbitron', monospace;
  font-size: 22px;
  font-weight: 900;
  background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  letter-spacing: 2px;
}

.logo span { color: var(--neon-pink); -webkit-text-fill-color: var(--neon-pink); }

nav { display: flex; gap: 8px; }

nav button {
  background: transparent;
  border: 1px solid var(--dark-border);
  color: var(--text-secondary);
  padding: 8px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-family: 'Cairo', sans-serif;
  font-size: 14px;
  transition: all 0.3s;
}

nav button:hover, nav button.active {
  border-color: var(--neon-blue);
  color: var(--neon-blue);
  background: rgba(0,212,255,0.07);
  box-shadow: 0 0 15px rgba(0,212,255,0.2);
}

/* SECTIONS */
section { display: none; position: relative; z-index: 1; }
section.active { display: block; }

/* HERO */
#hero {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 100px 40px 60px;
}

.hero-badge {
  font-family: 'Orbitron', monospace;
  font-size: 11px;
  letter-spacing: 4px;
  color: var(--neon-blue);
  border: 1px solid rgba(0,212,255,0.3);
  padding: 6px 20px;
  border-radius: 20px;
  margin-bottom: 30px;
  background: rgba(0,212,255,0.05);
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 10px rgba(0,212,255,0.2); }
  50% { box-shadow: 0 0 25px rgba(0,212,255,0.5); }
}

h1.hero-title {
  font-family: 'Orbitron', monospace;
  font-size: clamp(40px, 7vw, 80px);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 20px;
}

h1.hero-title .mk { background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
h1.hero-title .ai { color: var(--neon-pink); }

.hero-sub {
  font-size: 18px;
  color: var(--text-secondary);
  max-width: 600px;
  line-height: 1.8;
  margin-bottom: 50px;
}

.hero-cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  max-width: 900px;
  width: 100%;
  margin-bottom: 50px;
}

.hero-card {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 12px;
  padding: 30px 24px;
  cursor: pointer;
  transition: all 0.4s;
  text-align: right;
  position: relative;
  overflow: hidden;
}

.hero-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--card-color), transparent);
  opacity: 0;
  transition: opacity 0.3s;
}

.hero-card:hover::before { opacity: 1; }
.hero-card:hover { transform: translateY(-6px); border-color: var(--card-color); box-shadow: 0 10px 40px rgba(0,0,0,0.4), 0 0 20px rgba(0,212,255,0.1); }

.hero-card.blue { --card-color: var(--neon-blue); }
.hero-card.purple { --card-color: var(--neon-purple); }
.hero-card.pink { --card-color: var(--neon-pink); }

.card-icon {
  font-size: 36px;
  margin-bottom: 16px;
}

.card-title {
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 8px;
  color: var(--text-primary);
}

.card-desc {
  font-size: 13px;
  color: var(--text-secondary);
  line-height: 1.7;
}

.cta-btn {
  font-family: 'Orbitron', monospace;
  font-size: 14px;
  letter-spacing: 2px;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  color: #fff;
  border: none;
  padding: 16px 48px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
  text-transform: uppercase;
}

.cta-btn:hover {
  transform: translateY(-2px);
  box-shadow: var(--glow-blue);
}

/* SECTION WRAPPER */
.section-wrap {
  min-height: 100vh;
  padding: 100px 40px 60px;
  max-width: 1000px;
  margin: 0 auto;
}

.section-header {
  margin-bottom: 40px;
}

.section-tag {
  font-family: 'Orbitron', monospace;
  font-size: 11px;
  letter-spacing: 3px;
  color: var(--neon-blue);
  margin-bottom: 12px;
}

.section-title {
  font-family: 'Orbitron', monospace;
  font-size: 28px;
  font-weight: 700;
  color: var(--text-primary);
}

/* CHAT UI */
.chat-layout {
  display: grid;
  grid-template-columns: 220px 1fr;
  gap: 20px;
  height: 82vh;
}

.chat-sidebar {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.mode-btn {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  color: var(--text-secondary);
  padding: 12px 16px;
  border-radius: 8px;
  cursor: pointer;
  text-align: right;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  transition: all 0.3s;
  display: flex;
  align-items: center;
  gap: 10px;
}

.mode-btn.active, .mode-btn:hover {
  border-color: var(--neon-blue);
  color: var(--neon-blue);
  background: rgba(0,212,255,0.07);
}

.mode-icon { font-size: 18px; }

.chat-main {
  display: flex;
  flex-direction: column;
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 12px;
  overflow: hidden;
}

.chat-header {
  padding: 16px 20px;
  border-bottom: 1px solid var(--dark-border);
  display: flex;
  align-items: center;
  gap: 12px;
  background: rgba(0,212,255,0.03);
}

.status-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: #00ff88;
  box-shadow: 0 0 8px #00ff88;
  animation: blink 2s ease-in-out infinite;
}

@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.4} }

.chat-title { font-size: 14px; color: var(--text-primary); font-weight: 600; }
.chat-sub { font-size: 11px; color: var(--text-muted); }

.messages {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  scrollbar-width: thin;
  scrollbar-color: var(--dark-border) transparent;
}

.msg {
  max-width: 80%;
  animation: msgIn 0.3s ease;
}

@keyframes msgIn { from { opacity:0; transform: translateY(10px); } to { opacity:1; transform:none; } }

.msg.user { align-self: flex-end; }
.msg.ai { align-self: flex-start; }

.msg-bubble {
  padding: 12px 16px;
  border-radius: 12px;
  font-size: 14px;
  line-height: 1.7;
  white-space: pre-wrap;
}

.msg.user .msg-bubble {
  background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(177,74,237,0.2));
  border: 1px solid rgba(0,212,255,0.3);
  color: var(--text-primary);
  border-radius: 12px 12px 4px 12px;
}

.msg.ai .msg-bubble {
  background: var(--dark-surface);
  border: 1px solid var(--dark-border);
  color: var(--text-secondary);
  border-radius: 12px 12px 12px 4px;
  position: relative;
}

.msg.ai .msg-bubble::before {
  content: '⬡ MK AI';
  display: block;
  font-family: 'Orbitron', monospace;
  font-size: 10px;
  color: var(--neon-blue);
  margin-bottom: 8px;
  letter-spacing: 1px;
}

.typing-dots {
  display: flex;
  gap: 4px;
  padding: 4px 0;
}
.typing-dots span {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: var(--neon-blue);
  animation: dot 1.2s ease-in-out infinite;
}
.typing-dots span:nth-child(2) { animation-delay: 0.2s; }
.typing-dots span:nth-child(3) { animation-delay: 0.4s; }
@keyframes dot { 0%,80%,100%{transform:scale(0.8);opacity:0.4} 40%{transform:scale(1.2);opacity:1} }

.chat-input-area {
  padding: 16px;
  border-top: 1px solid var(--dark-border);
  display: flex;
  gap: 10px;
  align-items: flex-end;
}

.chat-input {
  flex: 1;
  background: var(--dark-surface);
  border: 1px solid var(--dark-border);
  border-radius: 8px;
  color: var(--text-primary);
  font-family: 'Cairo', sans-serif;
  font-size: 14px;
  padding: 12px 16px;
  resize: none;
  min-height: 48px;
  max-height: 120px;
  transition: border-color 0.3s;
  outline: none;
}

.chat-input:focus { border-color: var(--neon-blue); box-shadow: 0 0 10px rgba(0,212,255,0.15); }

.send-btn {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  border: none;
  border-radius: 8px;
  color: white;
  width: 48px; height: 48px;
  cursor: pointer;
  font-size: 20px;
  transition: all 0.3s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.send-btn:hover { transform: scale(1.05); box-shadow: var(--glow-blue); }
.send-btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }

/* CONTENT SECTION */
.content-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 24px; }

.content-type-btn {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 20px;
  cursor: pointer;
  transition: all 0.3s;
  text-align: right;
  font-family: 'Cairo', sans-serif;
}

.content-type-btn:hover, .content-type-btn.selected {
  border-color: var(--neon-purple);
  background: rgba(177,74,237,0.08);
}

.content-type-btn .ct-icon { font-size: 28px; margin-bottom: 8px; }
.content-type-btn .ct-name { font-size: 14px; font-weight: 700; color: var(--text-primary); }
.content-type-btn .ct-desc { font-size: 12px; color: var(--text-muted); margin-top: 4px; }

.content-form {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 12px;
  padding: 24px;
}

.form-group { margin-bottom: 18px; }
.form-label { display: block; font-size: 13px; color: var(--text-secondary); margin-bottom: 8px; font-weight: 600; }

.form-input, .form-textarea, .form-select {
  width: 100%;
  background: var(--dark-surface);
  border: 1px solid var(--dark-border);
  border-radius: 8px;
  color: var(--text-primary);
  font-family: 'Cairo', sans-serif;
  font-size: 14px;
  padding: 11px 14px;
  outline: none;
  transition: border-color 0.3s;
}

.form-input:focus, .form-textarea:focus, .form-select:focus {
  border-color: var(--neon-purple);
  box-shadow: 0 0 10px rgba(177,74,237,0.15);
}

.form-textarea { resize: vertical; min-height: 100px; }
.form-select option { background: var(--dark-surface); }

.generate-btn {
  width: 100%;
  background: linear-gradient(135deg, var(--neon-purple), var(--neon-blue));
  border: none;
  border-radius: 8px;
  color: white;
  padding: 14px;
  font-family: 'Orbitron', monospace;
  font-size: 13px;
  letter-spacing: 2px;
  cursor: pointer;
  transition: all 0.3s;
}

.generate-btn:hover { transform: translateY(-2px); box-shadow: var(--glow-purple); }

.output-box {
  background: var(--dark-surface);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 20px;
  margin-top: 20px;
  min-height: 120px;
  font-size: 14px;
  line-height: 1.8;
  color: var(--text-secondary);
  white-space: pre-wrap;
  position: relative;
}

.output-box::before {
  content: 'OUTPUT';
  font-family: 'Orbitron', monospace;
  font-size: 10px;
  letter-spacing: 2px;
  color: var(--neon-purple);
  display: block;
  margin-bottom: 12px;
}

.copy-btn {
  position: absolute;
  top: 14px;
  left: 14px;
  background: rgba(177,74,237,0.15);
  border: 1px solid rgba(177,74,237,0.3);
  color: var(--neon-purple);
  padding: 4px 12px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 12px;
  font-family: 'Cairo', sans-serif;
}

/* TASKS SECTION */
.tasks-wrap { max-width: 1000px; }

.tasks-header-row {
  display: flex;
  gap: 12px;
  margin-bottom: 24px;
  align-items: center;
}

.task-input-row {
  display: flex;
  gap: 10px;
  flex: 1;
}

.add-task-btn {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  border: none;
  border-radius: 8px;
  color: white;
  padding: 11px 24px;
  font-family: 'Cairo', sans-serif;
  font-size: 14px;
  cursor: pointer;
  white-space: nowrap;
  transition: all 0.3s;
}

.add-task-btn:hover { box-shadow: var(--glow-blue); }

.tasks-stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-bottom: 24px;
}

.stat-card {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 16px;
  text-align: center;
}

.stat-num {
  font-family: 'Orbitron', monospace;
  font-size: 28px;
  font-weight: 700;
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.stat-label { font-size: 12px; color: var(--text-muted); margin-top: 4px; }

.filter-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}

.filter-tab {
  background: transparent;
  border: 1px solid var(--dark-border);
  color: var(--text-muted);
  padding: 6px 16px;
  border-radius: 20px;
  cursor: pointer;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  transition: all 0.3s;
}

.filter-tab.active {
  border-color: var(--neon-blue);
  color: var(--neon-blue);
  background: rgba(0,212,255,0.07);
}

.task-list { display: flex; flex-direction: column; gap: 10px; }

.task-item {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 16px 20px;
  display: flex;
  align-items: center;
  gap: 14px;
  transition: all 0.3s;
  animation: msgIn 0.3s ease;
}

.task-item:hover { border-color: rgba(0,212,255,0.3); }
.task-item.done { opacity: 0.5; }

.task-check {
  width: 22px; height: 22px;
  border-radius: 6px;
  border: 2px solid var(--dark-border);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s;
  flex-shrink: 0;
  font-size: 13px;
  background: transparent;
}

.task-item.done .task-check {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  border-color: transparent;
}

.task-text {
  flex: 1;
  font-size: 14px;
  color: var(--text-primary);
}

.task-item.done .task-text { text-decoration: line-through; color: var(--text-muted); }

.task-priority {
  font-size: 11px;
  padding: 3px 10px;
  border-radius: 12px;
}

.task-priority.high { background: rgba(255,45,120,0.15); color: var(--neon-pink); border: 1px solid rgba(255,45,120,0.3); }
.task-priority.med { background: rgba(177,74,237,0.15); color: var(--neon-purple); border: 1px solid rgba(177,74,237,0.3); }
.task-priority.low { background: rgba(0,212,255,0.1); color: var(--neon-blue); border: 1px solid rgba(0,212,255,0.2); }

.task-del {
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  font-size: 16px;
  transition: color 0.2s;
  padding: 4px;
}

.task-del:hover { color: var(--neon-pink); }

.ai-suggest-btn {
  background: rgba(177,74,237,0.1);
  border: 1px solid rgba(177,74,237,0.3);
  color: var(--neon-purple);
  border-radius: 8px;
  padding: 10px 20px;
  cursor: pointer;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  margin-top: 16px;
  width: 100%;
  transition: all 0.3s;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.ai-suggest-btn:hover { background: rgba(177,74,237,0.2); box-shadow: var(--glow-purple); }

/* Loading */
.loading-overlay {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(5,10,20,0.85);
  z-index: 200;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 20px;
  backdrop-filter: blur(10px);
}

.loading-overlay.show { display: flex; }

.loader-ring {
  width: 60px; height: 60px;
  border: 3px solid var(--dark-border);
  border-top-color: var(--neon-blue);
  border-right-color: var(--neon-purple);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin { to { transform: rotate(360deg); } }

.loader-text {
  font-family: 'Orbitron', monospace;
  font-size: 12px;
  letter-spacing: 3px;
  color: var(--neon-blue);
}

/* Scrollbar */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--dark-border); border-radius: 2px; }

/* Notification */
.notif {
  position: fixed;
  bottom: 30px;
  right: 30px;
  background: var(--dark-card);
  border: 1px solid var(--neon-blue);
  border-radius: 10px;
  padding: 14px 20px;
  font-size: 13px;
  color: var(--neon-blue);
  box-shadow: var(--glow-blue);
  transform: translateX(200%);
  transition: transform 0.4s ease;
  z-index: 300;
  font-family: 'Orbitron', monospace;
  letter-spacing: 1px;
}

.notif.show { transform: translateX(0); }

/* FLOATING SURVEY CHAT WIDGET STYLES */
.survey-widget-container {
  position: fixed;
  bottom: 25px;
  left: 25px;
  z-index: 1000;
  font-family: 'Cairo', sans-serif;
}

.survey-toggle-btn {
  background: linear-gradient(135deg, var(--neon-blue), var(--neon-purple));
  color: white;
  border: none;
  width: 56px;
  height: 56px;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 0 20px rgba(0,212,255,0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  transition: transform 0.3s, box-shadow 0.3s;
  animation: pulseWidget 2s infinite;
}

.survey-toggle-btn:hover {
  transform: scale(1.1);
  box-shadow: 0 0 30px var(--neon-blue);
}

@keyframes pulseWidget {
  0% { box-shadow: 0 0 0 0 rgba(0,212,255, 0.4); }
  70% { box-shadow: 0 0 0 15px rgba(0,212,255, 0); }
  100% { box-shadow: 0 0 0 0 rgba(0,212,255, 0); }
}

.survey-chat-box {
  position: absolute;
  bottom: 75px;
  left: 0;
  width: 320px;
  background: var(--dark-card);
  border: 1px solid var(--neon-blue);
  border-radius: 16px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.6), var(--glow-blue);
  display: none;
  flex-direction: column;
  overflow: hidden;
  animation: widgetFadeIn 0.3s ease;
}

@keyframes widgetFadeIn {
  from { opacity: 0; transform: translateY(15px); }
  to { opacity: 1; transform: translateY(0); }
}

.survey-chat-box.open { display: flex; }

.survey-header {
  background: rgba(0,212,255,0.08);
  padding: 14px 16px;
  border-bottom: 1px solid var(--dark-border);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.survey-header-title {
  font-family: 'Orbitron', monospace;
  font-size: 13px;
  color: var(--neon-blue);
  letter-spacing: 1px;
}

.survey-close-btn {
  background: transparent;
  border: none;
  color: var(--text-muted);
  cursor: pointer;
  font-size: 16px;
}
.survey-close-btn:hover { color: var(--neon-pink); }

.survey-messages {
  padding: 14px;
  max-height: 250px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
  font-size: 13px;
}

.s-msg {
  padding: 10px 12px;
  border-radius: 10px;
  line-height: 1.5;
  max-width: 85%;
}

.s-msg.ai {
  background: var(--dark-surface);
  border: 1px solid var(--dark-border);
  color: var(--text-secondary);
  align-self: flex-start;
  border-bottom-left-radius: 2px;
}

.s-msg.user {
  background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(177,74,237,0.2));
  border: 1px solid rgba(0,212,255,0.3);
  color: var(--text-primary);
  align-self: flex-end;
  border-bottom-right-radius: 2px;
}

.survey-input-area {
  padding: 10px;
  border-top: 1px solid var(--dark-border);
  display: flex;
  gap: 8px;
  background: var(--dark-surface);
}

.survey-input {
  flex: 1;
  background: var(--dark-bg);
  border: 1px solid var(--dark-border);
  border-radius: 6px;
  color: var(--text-primary);
  padding: 8px 12px;
  font-family: 'Cairo', sans-serif;
  font-size: 13px;
  outline: none;
}
.survey-input:focus { border-color: var(--neon-blue); }

.survey-send-btn {
  background: var(--neon-blue);
  color: var(--dark-bg);
  border: none;
  border-radius: 6px;
  padding: 0 12px;
  cursor: pointer;
  font-weight: 700;
  font-size: 13px;
}

.survey-actions {
  display: flex;
  gap: 6px;
  margin-top: 6px;
}

.survey-option-btn {
  background: rgba(0,212,255,0.1);
  border: 1px solid var(--neon-blue);
  color: var(--neon-blue);
  padding: 6px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 12px;
  font-family: 'Cairo', sans-serif;
  transition: all 0.2s;
}

.survey-option-btn:hover {
  background: var(--neon-blue);
  color: var(--dark-bg);
}

/* FOOTER */
footer {
  position: relative;
  z-index: 1;
  border-top: 1px solid rgba(0,212,255,0.1);
  background: rgba(5,10,20,0.95);
  padding: 40px 40px 24px;
  margin-top: 0;
}

.footer-inner {
  max-width: 1000px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 40px;
  margin-bottom: 32px;
}

.footer-brand .logo { font-size: 20px; margin-bottom: 10px; display: block; }

.footer-brand p {
  font-size: 13px;
  color: var(--text-muted);
  line-height: 1.7;
  max-width: 220px;
}

.footer-col-title {
  font-family: 'Orbitron', monospace;
  font-size: 10px;
  letter-spacing: 3px;
  color: var(--neon-blue);
  margin-bottom: 16px;
}

.footer-dev-card {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 16px;
}

.dev-name {
  font-size: 15px;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 4px;
}

.dev-role {
  font-size: 12px;
  color: var(--neon-purple);
  margin-bottom: 8px;
}

.dev-badge {
  display: inline-block;
  font-size: 11px;
  background: rgba(0,212,255,0.08);
  border: 1px solid rgba(0,212,255,0.2);
  color: var(--neon-blue);
  padding: 3px 10px;
  border-radius: 12px;
  font-family: 'Orbitron', monospace;
  letter-spacing: 1px;
}

.company-card {
  background: var(--dark-card);
  border: 1px solid var(--dark-border);
  border-radius: 10px;
  padding: 16px;
}

.company-name {
  font-family: 'Orbitron', monospace;
  font-size: 16px;
  font-weight: 900;
  background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  margin-bottom: 4px;
}

.company-tm {
  font-size: 11px;
  color: var(--text-muted);
  margin-bottom: 8px;
}

.company-desc {
  font-size: 12px;
  color: var(--text-secondary);
  line-height: 1.6;
}

.footer-bottom {
  border-top: 1px solid rgba(0,212,255,0.07);
  padding-top: 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1000px;
  margin: 0 auto;
}

.footer-copy {
  font-size: 12px;
  color: var(--text-muted);
}

.footer-copy span { color: var(--neon-blue); }

.footer-made {
  font-family: 'Orbitron', monospace;
  font-size: 10px;
  letter-spacing: 2px;
  color: var(--text-muted);
}

/* Responsive */
@media (max-width: 768px) {
  .footer-inner { grid-template-columns: 1fr; gap: 20px; }
  .footer-bottom { flex-direction: column; gap: 8px; text-align: center; }

  header { padding: 12px 20px; }
  .logo { font-size: 16px; }
  nav button { padding: 7px 12px; font-size: 12px; }
  .hero-cards { grid-template-columns: 1fr; }
  .chat-layout { grid-template-columns: 1fr; }
  .chat-sidebar { flex-direction: row; overflow-x: auto; }
  .content-grid { grid-template-columns: 1fr 1fr; }
  .tasks-stats { grid-template-columns: repeat(2, 1fr); }
  .section-wrap { padding: 90px 20px 40px; }
}
</style>
</head>
<body>

<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>

<!-- HEADER -->
<header>
  <div class="logo">MK<span>.</span>AI&nbsp;TOOLS</div>
  <nav>
    <button class="active" onclick="showSection('hero')">الرئيسية</button>
    <button onclick="showSection('assistant')">المساعد</button>
    <button onclick="showSection('content')">المحتوى</button>
    <button onclick="showSection('tasks')">المهام</button>
    <button onclick="showSection('developer')">المطوّر</button>
    <button onclick="showSection('focus')">التركيز</button>
  </nav>
</header>

<!-- LOADING -->
<div class="loading-overlay" id="loading">
  <div class="loader-ring"></div>
  <div class="loader-text">PROCESSING...</div>
</div>

<div class="notif" id="notif"></div>

<!-- HERO -->
<section id="hero" class="active">
  <div class="hero-badge">■ POWERED BY AI ■</div>
  <h1 class="hero-title">
    <span class="mk">MK</span> <span class="ai">AI</span><br>TOOLS
  </h1>
  <p class="hero-sub">منصة ذكاء اصطناعي متكاملة لصناع المحتوى والمبدعين — أدوات قوية في مكان واحد</p>

  <div class="hero-cards">
    <div class="hero-card blue" onclick="showSection('assistant')">
      <div class="card-icon">🤖</div>
      <div class="card-title">المساعد الذكي</div>
      <div class="card-desc">أجب على أسئلتك، تعلّم، استفسر وتحدث مع الذكاء الاصطناعي بالعربية</div>
    </div>
    <div class="hero-card purple" onclick="showSection('content')">
      <div class="card-icon">🎬</div>
      <div class="card-title">صناعة المحتوى</div>
      <div class="card-desc">سكريبتات، أفكار إبداعية، أوصاف فيديو، عناوين جذابة وأكثر</div>
    </div>
    <div class="hero-card pink" onclick="showSection('tasks')">
      <div class="card-icon">⚡</div>
      <div class="card-title">إدارة المهام</div>
      <div class="card-desc">نظّم يومك، تتبع مهامك واحصل على اقتراحات ذكية لإنجازها</div>
    </div>
  </div>

  <button class="cta-btn" onclick="showSection('assistant')">ابدأ الآن ←</button>
</section>

<!-- ASSISTANT SECTION -->
<section id="assistant">
  <div class="section-wrap">
    <div class="section-header">
      <div class="section-tag">■ AI ASSISTANT</div>
      <div class="section-title">المساعد الذكي</div>
    </div>

    <div class="chat-layout">
      <div class="chat-sidebar">
        <button class="mode-btn active" onclick="setMode(this,'general')">
          <span class="mode-icon">🧠</span> عام
        </button>
        <button class="mode-btn" onclick="setMode(this,'creative')">
          <span class="mode-icon">✨</span> إبداعي
        </button>
        <button class="mode-btn" onclick="setMode(this,'technical')">
          <span class="mode-icon">💻</span> تقني
        </button>
        <button class="mode-btn" onclick="setMode(this,'analysis')">
          <span class="mode-icon">📊</span> تحليل
        </button>
        <button class="mode-btn" onclick="setMode(this,'arabic')">
          <span class="mode-icon">📝</span> لغة عربية
        </button>
        <button class="mode-btn" style="margin-top:auto;border-color:rgba(255,45,120,0.3);color:var(--neon-pink)" onclick="clearChat()">
          <span class="mode-icon">🗑️</span> مسح
        </button>
      </div>

      <div class="chat-main">
        <div class="chat-header">
          <div class="status-dot"></div>
          <div>
            <div class="chat-title" id="chatTitle">المساعد العام</div>
            <div class="chat-sub">MK AI — متصل</div>
          </div>
        </div>

        <div class="messages" id="messages">
          <div class="msg ai">
            <div class="msg-bubble">مرحباً! أنا MK AI، مساعدك الذكي. كيف يمكنني مساعدتك اليوم؟ 🚀</div>
          </div>
        </div>

        <div class="chat-input-area">
          <textarea class="chat-input" id="chatInput" placeholder="اكتب رسالتك هنا..." rows="1"
            onkeydown="handleKey(event)" oninput="autoResize(this)"></textarea>
          <button class="send-btn" id="sendBtn" onclick="sendMessage()">➤</button>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CONTENT SECTION -->
<section id="content">
  <div class="section-wrap">
    <div class="section-header">
      <div class="section-tag">■ CONTENT CREATION</div>
      <div class="section-title">صناعة المحتوى</div>
    </div>

    <div class="content-grid">
      <div class="content-type-btn selected" onclick="selectContentType(this,'script')">
        <div class="ct-icon">🎬</div>
        <div class="ct-name">سكريبت فيديو</div>
        <div class="ct-desc">اكتب سكريبت فيديو احترافي</div>
      </div>
      <div class="content-type-btn" onclick="selectContentType(this,'ideas')">
        <div class="ct-icon">💡</div>
        <div class="ct-name">أفكار إبداعية</div>
        <div class="ct-desc">توليد أفكار مبتكرة</div>
      </div>
      <div class="content-type-btn" onclick="selectContentType(this,'description')">
        <div class="ct-icon">📋</div>
        <div class="ct-name">وصف المقطع</div>
        <div class="ct-desc">وصف SEO لليوتيوب</div>
      </div>
      <div class="content-type-btn" onclick="selectContentType(this,'title')">
        <div class="ct-icon">🔥</div>
        <div class="ct-name">عناوين جذابة</div>
        <div class="ct-desc">عناوين تجذب المشاهدين</div>
      </div>
      <div class="content-type-btn" onclick="selectContentType(this,'hook')">
        <div class="ct-icon">⚡</div>
        <div class="ct-name">Hook افتتاحي</div>
        <div class="ct-desc">مقدمة تشدّ الانتباه</div>
      </div>
      <div class="content-type-btn" onclick="selectContentType(this,'hashtags')">
        <div class="ct-icon">🏷️</div>
        <div class="ct-name">هاشتاقات</div>
        <div class="ct-desc">هاشتاقات للسوشيال ميديا</div>
      </div>
    </div>

    <div class="content-form">
      <div class="form-group">
        <label class="form-label">موضوع المحتوى</label>
        <input class="form-input" id="contentTopic" placeholder="مثال: كيفية تعلم البرمجة في 30 يوم" />
      </div>
      <div class="form-group">
        <label class="form-label">الجمهور المستهدف</label>
        <select class="form-select" id="contentAudience">
          <option value="عام">جمهور عام</option>
          <option value="شباب">شباب (18-25)</option>
          <option value="مهنيون">مهنيون</option>
          <option value="طلاب">طلاب</option>
          <option value="رواد أعمال">رواد أعمال</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">النبرة والأسلوب</label>
        <select class="form-select" id="contentTone">
          <option value="محفّز وحماسي">محفّز وحماسي</option>
          <option value="تعليمي وبسيط">تعليمي وبسيط</option>
          <option value="ترفيهي وفكاهي">ترفيهي وفكاهي</option>
          <option value="احترافي وجدي">احترافي وجدي</option>
          <option value="قصصي وإنساني">قصصي وإنساني</option>
        </select>
      </div>
      <div class="form-group">
        <label class="form-label">تفاصيل إضافية (اختياري)</label>
        <textarea class="form-textarea" id="contentExtra" placeholder="أي معلومات إضافية تريد تضمينها..."></textarea>
      </div>
      <button class="generate-btn" onclick="generateContent()">⚡ توليد المحتوى</button>
    </div>

    <div class="output-box" id="contentOutput" style="display:none">
      <button class="copy-btn" onclick="copyOutput()">نسخ</button>
      <span id="contentText"></span>
    </div>
  </div>
</section>

<!-- TASKS SECTION -->
<section id="tasks">
  <div class="section-wrap tasks-wrap">
    <div class="section-header">
      <div class="section-tag">■ TASK MANAGER</div>
      <div class="section-title">إدارة المهام</div>
    </div>

    <div class="tasks-stats">
      <div class="stat-card">
        <div class="stat-num" id="statTotal">0</div>
        <div class="stat-label">إجمالي المهام</div>
      </div>
      <div class="stat-card">
        <div class="stat-num" id="statDone">0</div>
        <div class="stat-label">مكتملة</div>
      </div>
      <div class="stat-card">
        <div class="stat-num" id="statPending">0</div>
        <div class="stat-label">قيد التنفيذ</div>
      </div>
      <div class="stat-card">
        <div class="stat-num" id="statProgress">0%</div>
        <div class="stat-label">نسبة الإنجاز</div>
      </div>
    </div>

    <div class="tasks-header-row">
      <div class="task-input-row">
        <input class="form-input" id="taskInput" placeholder="أضف مهمة جديدة..." onkeydown="if(event.key==='Enter') addTask()" style="flex:1" />
        <select class="form-select" id="taskPriority" style="width:140px">
          <option value="high">عالية 🔴</option>
          <option value="med" selected>متوسطة 🟣</option>
          <option value="low">منخفضة 🔵</option>
        </select>
      </div>
      <button class="add-task-btn" onclick="addTask()">+ إضافة</button>
    </div>

    <div class="filter-tabs">
      <button class="filter-tab active" onclick="filterTasks(this,'all')">الكل</button>
      <button class="filter-tab" onclick="filterTasks(this,'pending')">قيد التنفيذ</button>
      <button class="filter-tab" onclick="filterTasks(this,'done')">مكتملة</button>
      <button class="filter-tab" onclick="filterTasks(this,'high')">عالية الأولوية</button>
    </div>

    <div class="task-list" id="taskList"></div>

    <button class="ai-suggest-btn" onclick="aiSuggestTasks()">
      🤖 اقتراح مهام ذكية بالذكاء الاصطناعي
    </button>
    <div class="form-group" style="margin-top:30px;">
      <label class="form-label" style="color:var(--neon-blue); font-size:14px;">💻 محرر ومُنظّم أكواد Python السريع</label>
      <textarea class="form-textarea" id="codeEditor" style="font-family:monospace;background:#02060c;border-color:var(--dark-border);color:#a5d6ff;min-height:140px;" placeholder="# اكتب أو الصق كود الـ Python هنا..."></textarea>
      <button class="generate-btn" style="background:linear-gradient(135deg,var(--neon-blue),#1a3a5c);margin-top:10px;" onclick="formatPythonCode()">⚡ تنظيم الكود</button>
    </div>
  </div>
</section>

<!-- DEVELOPER SECTION -->
<section id="developer">
  <div class="section-wrap">
    <div class="section-header">
      <div class="section-tag">■ THE FOUNDER</div>
      <div class="section-title">عن المطور والشركة</div>
    </div>

    <div class="hero-card blue" style="text-align:right; margin-bottom:24px; cursor:default; padding:30px;">
      <div style="display:flex; align-items:center; gap:20px; margin-bottom:16px; flex-wrap:wrap;">
        <div style="width:72px;height:72px;border-radius:50%;background:linear-gradient(135deg,var(--neon-blue),var(--neon-purple));display:flex;align-items:center;justify-content:center;font-family:'Orbitron',monospace;font-size:22px;font-weight:900;color:#fff;flex-shrink:0;">MA</div>
        <div>
          <h3 style="font-family:'Orbitron',monospace;color:var(--neon-blue);font-size:22px;margin-bottom:6px;letter-spacing:2px;">MOHAMED ANTAR</h3>
          <span style="font-family:'Orbitron',monospace;font-size:10px;letter-spacing:3px;background:rgba(0,212,255,0.1);border:1px solid rgba(0,212,255,0.3);color:var(--neon-blue);padding:4px 14px;border-radius:12px;">CEO &amp; FOUNDER — MK COMPANY ™</span>
        </div>
      </div>
      <p style="color:var(--text-secondary);font-size:14px;line-height:1.9;">
        الرئيس التنفيذي ومؤسس براند <strong style="color:var(--neon-blue)">MK</strong>. صانع محتوى رقمي، ومطور حلول أتمتة ذكية، ومتخصص في تكييف التقنيات الحديثة والذكاء الاصطناعي لخدمة مجتمعات الجيمرز والمبدعين.
      </p>
    </div>

    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(250px,1fr));gap:16px;margin-bottom:24px;">

      <div class="stat-card" style="border:1px solid var(--neon-purple);padding:24px;text-align:right;">
        <div style="font-size:32px;margin-bottom:12px;">🎬</div>
        <div style="font-size:15px;font-weight:700;color:var(--neon-purple);margin-bottom:8px;">صناعة المحتوى والمونتاج</div>
        <div style="font-size:13px;color:var(--text-secondary);line-height:1.7;">خبرة طويلة في إدارة قنوات الألعاب وصناعة الفيديوهات الاحترافية.</div>
      </div>

      <div class="stat-card" style="border:1px solid var(--neon-pink);padding:24px;text-align:right;">
        <div style="font-size:32px;margin-bottom:12px;">⚡</div>
        <div style="font-size:15px;font-weight:700;color:var(--neon-pink);margin-bottom:8px;">خبير الأتمتة والبرمجة</div>
        <div style="font-size:13px;color:var(--text-secondary);line-height:1.7;">تطوير سكربتات وأنظمة أتمتة متكاملة للهواتف والويب باستخدام Python و MacroDroid.</div>
      </div>

      <div class="stat-card" style="border:1px solid var(--neon-blue);padding:24px;text-align:right;">
        <div style="font-size:32px;margin-bottom:12px;">🤖</div>
        <div style="font-size:15px;font-weight:700;color:var(--neon-blue);margin-bottom:8px;">تطوير الذكاء الاصطناعي</div>
        <div style="font-size:13px;color:var(--text-secondary);line-height:1.7;">بناء منصات وأدوات ذكاء اصطناعي متكاملة موجّهة للمستخدم العربي والمبدع.</div>
      </div>

    </div>

    <div class="hero-card purple" style="text-align:right; cursor:default; padding:28px;">
      <div style="display:flex;align-items:center;gap:16px;margin-bottom:14px;">
        <div style="font-family:'Orbitron',monospace;font-size:20px;font-weight:900;background:linear-gradient(90deg,var(--neon-blue),var(--neon-purple));-webkit-background-clip:text;-webkit-text-fill-color:transparent;">MK COMPANY ™</div>
        <span style="font-family:'Orbitron',monospace;font-size:9px;letter-spacing:2px;background:rgba(177,74,237,0.15);border:1px solid rgba(177,74,237,0.3);color:var(--neon-purple);padding:4px 12px;border-radius:12px;">TECH COMPANY</span>
      </div>
      <p style="color:var(--text-secondary);font-size:14px;line-height:1.9;">شركة رائدة في تطوير حلول الذكاء الاصطناعي والتقنية المتقدمة، تهدف إلى تمكين المبدعين والمطورين العرب بأدوات ذكية وسهلة الاستخدام. جميع الحقوق محفوظة لشركة MK Company ™.</p>
    </div>

  </div>
</section>

<!-- FOCUS MODE SECTION -->
<section id="focus">
  <div class="section-wrap" style="text-align:center;">
    <div class="section-header" style="text-align:right;">
      <div class="section-tag">■ PRODUCTIVITY</div>
      <div class="section-title">وضع التركيز للمذاكرة والعمل</div>
    </div>

    <div style="font-family:'Orbitron',monospace;font-size:clamp(60px,12vw,100px);color:var(--neon-pink);margin:40px 0;text-shadow:0 0 30px rgba(255,45,120,0.5),0 0 60px rgba(255,45,120,0.2);letter-spacing:4px;">
      <span id="timerDisplay">25:00</span>
    </div>

    <div style="display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-bottom:40px;">
      <button class="cta-btn" id="timerBtn" style="background:linear-gradient(135deg,var(--neon-pink),var(--neon-purple));" onclick="toggleTimer()">▶ ابدأ الجلسة</button>
      <button class="mode-btn" onclick="resetTimer()">↺ إعادة تعيين</button>
    </div>

    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px;max-width:600px;margin:0 auto 40px;">
      <button class="content-type-btn" onclick="setTimerPreset(25,0)" style="text-align:center;padding:16px;">
        <div style="font-family:'Orbitron',monospace;font-size:20px;color:var(--neon-pink);margin-bottom:6px;">25</div>
        <div style="font-size:12px;color:var(--text-muted);">Pomodoro</div>
      </button>
      <button class="content-type-btn" onclick="setTimerPreset(15,0)" style="text-align:center;padding:16px;">
        <div style="font-family:'Orbitron',monospace;font-size:20px;color:var(--neon-purple);margin-bottom:6px;">15</div>
        <div style="font-size:12px;color:var(--text-muted);">جلسة قصيرة</div>
      </button>
      <button class="content-type-btn" onclick="setTimerPreset(50,0)" style="text-align:center;padding:16px;">
        <div style="font-family:'Orbitron',monospace;font-size:20px;color:var(--neon-blue);margin-bottom:6px;">50</div>
        <div style="font-size:12px;color:var(--text-muted);">جلسة عميقة</div>
      </button>
      <button class="content-type-btn" onclick="setTimerPreset(5,0)" style="text-align:center;padding:16px;">
        <div style="font-family:'Orbitron',monospace;font-size:20px;color:#00ff88;margin-bottom:6px;">5</div>
        <div style="font-size:12px;color:var(--text-muted);">استراحة</div>
      </button>
    </div>

    <div style="max-width:500px;margin:0 auto;">
      <div style="background:var(--dark-card);border:1px solid var(--dark-border);border-radius:12px;padding:24px;">
        <div style="font-family:'Orbitron',monospace;font-size:10px;letter-spacing:3px;color:var(--neon-purple);margin-bottom:16px;">■ إحصائيات الجلسات</div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;">
          <div class="stat-card">
            <div class="stat-num" id="focusSessions" style="font-size:22px;">0</div>
            <div class="stat-label">جلسات مكتملة</div>
          </div>
          <div class="stat-card">
            <div class="stat-num" id="focusMinutes" style="font-size:22px;">0</div>
            <div class="stat-label">دقيقة تركيز</div>
          </div>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- INTERACTIVE SURVEY / HIRING BOT WIDGET -->
<div class="survey-widget-container">
  <div class="survey-chat-box" id="surveyChatBox">
    <div class="survey-header">
      <span class="survey-header-title">MK ASSISTANT BOT</span>
      <button class="survey-close-btn" onclick="toggleSurveyChat()">✕</button>
    </div>
    <div class="survey-messages" id="surveyMessages">
      <div class="s-msg ai">أهلاً بك في موقع MK! أنا مساعد الوكالة الذكي. ما هو اسمك الكريم؟ (اكتب اسمك الأول والأخير)</div>
    </div>
    <div class="survey-input-area" id="surveyInputArea">
      <input type="text" class="survey-input" id="surveyInput" placeholder="اكتب هنا..." onkeydown="if(event.key==='Enter') handleSurveyInput()">
      <button class="survey-send-btn" onclick="handleSurveyInput()">➤</button>
    </div>
  </div>
  <button class="survey-toggle-btn" onclick="toggleSurveyChat()" title="انضم إلينا أو قيّم الموقع">🤖</button>
</div>

<script>
const API_URL = "https://api.anthropic.com/v1/messages";
const MODEL = "claude-sonnet-4-20250514";

let chatHistory = [];
let currentMode = 'general';
let selectedContentType = 'script';
let tasks = [
  { id: 1, text: 'مراجعة محتوى القناة الأسبوعي', priority: 'high', done: false },
  { id: 2, text: 'التخطيط لمقاطع الشهر القادم', priority: 'med', done: false },
  { id: 3, text: 'الرد على تعليقات المتابعين', priority: 'low', done: true }
];
if(localStorage.getItem('mk_tasks')) {
  tasks = JSON.parse(localStorage.getItem('mk_tasks'));
}
let currentFilter = 'all';

function saveTasksToStorage() {
  localStorage.setItem('mk_tasks', JSON.stringify(tasks));
}

const MK_IDENTITY = `
معلوماتك الأساسية التي يجب أن تعرفها دائماً:
- اسمك: MK AI — المساعد الذكي الرسمي لمنصة MK AI Tools.
- الشركة المطوّرة لك: شركة MK Company ™ — شركة رائدة في تطوير حلول الذكاء الاصطناعي والتقنية المتقدمة.
- المطوّر والمؤسس: المهندس محمد عنتر محمد عوض — مطوّر الموقع والمنصة بالكامل.
- المنصة: MK AI Tools — منصة ذكاء اصطناعي متكاملة تضم ثلاثة أقسام رئيسية: المساعد الذكي، صناعة المحتوى، وإدارة المهام.
- رسالتك: مساعدة المستخدمين العرب وصناع المحتوى بأدوات ذكاء اصطناعي قوية وسهلة الاستخدام.
- إذا سُئلت عن مطوّرك أو شركتك أو هويتك، أجب بثقة ووضوح بالمعلومات أعلاه.
- لا تقل أبداً أنك ChatGPT أو Gemini أو أي نموذج آخر — أنت MK AI من MK Company ™.
`;

const modePrompts = {
  general: MK_IDENTITY + 'أنت مساعد ذكاء اصطناعي متعدد الأغراض. أجب بالعربية بشكل واضح ومفيد وموجز.',
  creative: MK_IDENTITY + 'أنت مساعد إبداعي. أجب بالعربية بطريقة إبداعية ومبتكرة، وقدّم أفكاراً غير تقليدية.',
  technical: MK_IDENTITY + 'أنت مساعد تقني متخصص. أجب بالعربية بدقة تقنية عالية مع شرح واضح للمفاهيم.',
  analysis: MK_IDENTITY + 'أنت محلل بيانات وخبير استراتيجي. قدّم تحليلات عميقة ومنظمة باللغة العربية.',
  arabic: MK_IDENTITY + 'أنت خبير في اللغة العربية وآدابها. ساعد في الكتابة والنحو والصرف والأسلوب الأدبي.'
};

const modeTitles = {
  general: 'المساعد العام', creative: 'المساعد الإبداعي',
  technical: 'المساعد التقني', analysis: 'محلل البيانات', arabic: 'خبير اللغة العربية'
};

function showSection(id) {
  document.querySelectorAll('section').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  document.querySelectorAll('nav button').forEach((b, i) => {
    b.classList.toggle('active', ['hero','assistant','content','tasks','developer','focus'][i] === id);
  });
  if (id === 'tasks') renderTasks();
}

function setMode(btn, mode) {
  document.querySelectorAll('.mode-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  currentMode = mode;
  document.getElementById('chatTitle').textContent = modeTitles[mode];
  chatHistory = [];
  const msgs = document.getElementById('messages');
  msgs.innerHTML = `<div class="msg ai"><div class="msg-bubble">تم تغيير الوضع إلى: ${modeTitles[mode]} ✨ كيف أساعدك؟</div></div>`;
}

function clearChat() {
  chatHistory = [];
  document.getElementById('messages').innerHTML = `<div class="msg ai"><div class="msg-bubble">تم مسح المحادثة. كيف يمكنني مساعدتك؟ 🚀</div></div>`;
}

function autoResize(el) {
  el.style.height = 'auto';
  el.style.height = Math.min(el.scrollHeight, 120) + 'px';
}

function handleKey(e) {
  if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendMessage(); }
}

function addMessage(role, text) {
  const msgs = document.getElementById('messages');
  const div = document.createElement('div');
  div.className = `msg ${role}`;
  div.innerHTML = `<div class="msg-bubble">${text}</div>`;
  msgs.appendChild(div);
  msgs.scrollTop = msgs.scrollHeight;
}

function addTyping() {
  const msgs = document.getElementById('messages');
  const div = document.createElement('div');
  div.className = 'msg ai'; div.id = 'typing';
  div.innerHTML = `<div class="msg-bubble" style="padding:16px 20px"><div class="typing-dots"><span></span><span></span><span></span></div></div>`;
  msgs.appendChild(div);
  msgs.scrollTop = msgs.scrollHeight;
}

async function sendMessage() {
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if (!text) return;

  input.value = ''; input.style.height = 'auto';
  document.getElementById('sendBtn').disabled = true;
  playCyberSound('click');
  addMessage('user', text);
  addTyping();

  chatHistory.push({ role: 'user', content: text });

  try {
    const res = await fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: MODEL,
        max_tokens: 1000,
        system: modePrompts[currentMode],
        messages: chatHistory
      })
    });

    const data = await res.json();
    const reply = data.content?.[0]?.text || 'عذراً، حدث خطأ في الاتصال.';
    document.getElementById('typing')?.remove();
    addMessage('ai', reply);
    chatHistory.push({ role: 'assistant', content: reply });
  } catch {
    document.getElementById('typing')?.remove();
    addMessage('ai', '⚠️ خطأ في الاتصال. تحقق من الإنترنت وأعد المحاولة.');
  }

  document.getElementById('sendBtn').disabled = false;
}

function selectContentType(btn, type) {
  document.querySelectorAll('.content-type-btn').forEach(b => b.classList.remove('selected'));
  btn.classList.add('selected');
  selectedContentType = type;
}

const contentPrompts = {
  script: (topic, aud, tone, extra) => `اكتب سكريبت فيديو يوتيوب احترافي ومتكامل بالعربية عن: "${topic}". الجمهور: ${aud}. الأسلوب: ${tone}. ${extra ? 'تفاصيل: ' + extra : ''}\n\nالسكريبت يجب أن يتضمن: مقدمة شيقة، المحتوى الرئيسي منظم في نقاط، خاتمة مع call-to-action.`,
  ideas: (topic, aud, tone, extra) => `أعطني 8 أفكار فيديو إبداعية ومبتكرة بالعربية حول موضوع: "${topic}". الجمهور: ${aud}. ${extra || ''}\n\nلكل فكرة: عنوان جذاب + وصف موجز + سبب نجاحها.`,
  description: (topic, aud, tone, extra) => `اكتب وصف يوتيوب احترافي ومحسّن لـ SEO بالعربية لفيديو عن: "${topic}". الجمهور: ${aud}.\nيجب أن يتضمن: فقرة تعريفية، نقاط ما ستتعلمه، معلومات التواصل، هاشتاقات مناسبة.`,
  title: (topic, aud, tone, extra) => `أعطني 10 عناوين فيديو جذابة ومثيرة للفضول بالعربية حول: "${topic}". الجمهور: ${aud}. الأسلوب: ${tone}.\n\nالعناوين يجب أن تكون مثيرة للنقر (clickbait أخلاقي) ومحسّنة للخوارزميات.`,
  hook: (topic, aud, tone, extra) => `اكتب 5 مقدمات افتتاحية (Hooks) قوية ومشوّقة بالعربية لفيديو عن: "${topic}". الجمهور: ${aud}. الأسلوب: ${tone}.\n\nكل hook لا يتجاوز 30 ثانية حواراً ويجب أن يشدّ المشاهد فوراً.`,
  hashtags: (topic, aud, tone, extra) => `أعطني قائمة هاشتاقات شاملة بالعربية والإنجليزية لمحتوى عن: "${topic}". الجمهور: ${aud}.\n\nصنّف الهاشتاقات: عامة، متخصصة، ترند. أعطِ 30 هاشتاق على الأقل.`
};

async function generateContent() {
  const topic = document.getElementById('contentTopic').value.trim();
  if (!topic) { showNotif('⚠️ أدخل موضوع المحتوى أولاً'); return; }

  const aud = document.getElementById('contentAudience').value;
  const tone = document.getElementById('contentTone').value;
  const extra = document.getElementById('contentExtra').value;

  showLoading(true);

  try {
    const prompt = contentPrompts[selectedContentType](topic, aud, tone, extra);
    const res = await fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: MODEL,
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    const data = await res.json();
    const text = data.content?.[0]?.text || 'حدث خطأ.';
    const box = document.getElementById('contentOutput');
    document.getElementById('contentText').textContent = text;
    box.style.display = 'block';
    box.scrollIntoView({ behavior: 'smooth', block: 'start' });
  } catch {
    showNotif('⚠️ خطأ في الاتصال');
  }

  showLoading(false);
}

function copyOutput() {
  const text = document.getElementById('contentText').textContent;
  navigator.clipboard.writeText(text).then(() => { playCyberSound('success'); showNotif('✓ تم النسخ'); });
}

// TASKS
let nextId = 10;

function addTask() {
  const input = document.getElementById('taskInput');
  const text = input.value.trim();
  if (!text) return;
  const priority = document.getElementById('taskPriority').value;
  tasks.unshift({ id: nextId++, text, priority, done: false });
  input.value = '';
  saveTasksToStorage();
  renderTasks();
  playCyberSound('success');
  showNotif('✓ تمت إضافة المهمة');
}

function toggleTask(id) {
  const task = tasks.find(t => t.id === id);
  if (task) { task.done = !task.done; saveTasksToStorage(); renderTasks(); }
}

function deleteTask(id) {
  tasks = tasks.filter(t => t.id !== id);
  saveTasksToStorage();
  renderTasks();
}

function filterTasks(btn, filter) {
  document.querySelectorAll('.filter-tab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  currentFilter = filter;
  renderTasks();
}

function renderTasks() {
  let filtered = tasks;
  if (currentFilter === 'pending') filtered = tasks.filter(t => !t.done);
  else if (currentFilter === 'done') filtered = tasks.filter(t => t.done);
  else if (currentFilter === 'high') filtered = tasks.filter(t => t.priority === 'high');

  const total = tasks.length;
  const done = tasks.filter(t => t.done).length;
  document.getElementById('statTotal').textContent = total;
  document.getElementById('statDone').textContent = done;
  document.getElementById('statPending').textContent = total - done;
  document.getElementById('statProgress').textContent = total ? Math.round(done / total * 100) + '%' : '0%';

  const pLabels = { high: 'عالية', med: 'متوسطة', low: 'منخفضة' };
  document.getElementById('taskList').innerHTML = filtered.map(t => `
    <div class="task-item ${t.done ? 'done' : ''}">
      <button class="task-check" onclick="toggleTask(${t.id})">${t.done ? '✓' : ''}</button>
      <div class="task-text">${t.text}</div>
      <span class="task-priority ${t.priority}">${pLabels[t.priority]}</span>
      <button class="task-del" onclick="deleteTask(${t.id})">✕</button>
    </div>
  `).join('') || '<div style="color:var(--text-muted);text-align:center;padding:30px">لا توجد مهام في هذا القسم</div>';
}

async function aiSuggestTasks() {
  showLoading(true);
  const existing = tasks.map(t => t.text).join(', ');
  try {
    const res = await fetch(API_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: MODEL,
        max_tokens: 1000,
        messages: [{
          role: 'user',
          content: `أنا صانع محتوى. مهامي الحالية: ${existing || 'لا يوجد'}. اقترح لي 5 مهام جديدة مفيدة وذكية لصانع المحتوى. قدّمها كقائمة مرقمة بسيطة بدون تفاصيل زائدة.`
        }]
      })
    });
    const data = await res.json();
    const text = data.content?.[0]?.text || '';
    const lines = text.split('\n').filter(l => l.match(/^\d+\./));
    lines.forEach(line => {
      const taskText = line.replace(/^\d+\.\s*/, '').trim();
      if (taskText) tasks.unshift({ id: nextId++, text: taskText, priority: 'med', done: false });
    });
    renderTasks();
    showNotif('✓ تم إضافة مهام ذكية');
  } catch {
    showNotif('⚠️ خطأ في الاتصال');
  }
  showLoading(false);
}

function playCyberSound(type) {
  const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  const oscillator = audioCtx.createOscillator();
  const gainNode = audioCtx.createGain();
  oscillator.connect(gainNode);
  gainNode.connect(audioCtx.destination);
  if (type === 'click') {
    oscillator.type = 'sine';
    oscillator.frequency.setValueAtTime(800, audioCtx.currentTime);
    gainNode.gain.setValueAtTime(0.05, audioCtx.currentTime);
    oscillator.start();
    oscillator.stop(audioCtx.currentTime + 0.05);
  } else if (type === 'success') {
    oscillator.type = 'triangle';
    oscillator.frequency.setValueAtTime(600, audioCtx.currentTime);
    oscillator.frequency.exponentialRampToValueAtTime(1200, audioCtx.currentTime + 0.15);
    gainNode.gain.setValueAtTime(0.05, audioCtx.currentTime);
    oscillator.start();
    oscillator.stop(audioCtx.currentTime + 0.15);
  }
}

function formatPythonCode() {
  const editor = document.getElementById('codeEditor');
  let code = editor.value;
  if(!code.trim()) { showNotif('⚠️ المحرر فارغ!'); return; }
  editor.value = code.trim();
  playCyberSound('success');
  showNotif('✓ تم تنظيم وتنسيق الكود بنجاح');
}

// FOCUS TIMER
let timerInterval = null;
let timerRunning = false;
let timerMinutes = 25;
let timerSeconds = 0;
let focusSessionsCount = parseInt(localStorage.getItem('mk_focus_sessions') || '0');
let focusTotalMinutes = parseInt(localStorage.getItem('mk_focus_minutes') || '0');

function updateTimerDisplay() {
  const m = String(timerMinutes).padStart(2,'0');
  const s = String(timerSeconds).padStart(2,'0');
  document.getElementById('timerDisplay').textContent = m + ':' + s;
}

function setTimerPreset(min, sec) {
  if(timerRunning) return;
  timerMinutes = min;
  timerSeconds = sec;
  updateTimerDisplay();
  playCyberSound('click');
}

function toggleTimer() {
  const btn = document.getElementById('timerBtn');
  if (!timerRunning) {
    timerRunning = true;
    btn.textContent = '⏸ إيقاف مؤقت';
    playCyberSound('click');
    timerInterval = setInterval(() => {
      if (timerSeconds === 0) {
        if (timerMinutes === 0) {
          clearInterval(timerInterval);
          timerRunning = false;
          btn.textContent = '▶ ابدأ الجلسة';
          focusSessionsCount++;
          focusTotalMinutes += 25;
          localStorage.setItem('mk_focus_sessions', focusSessionsCount);
          localStorage.setItem('mk_focus_minutes', focusTotalMinutes);
          document.getElementById('focusSessions').textContent = focusSessionsCount;
          document.getElementById('focusMinutes').textContent = focusTotalMinutes;
          playCyberSound('success');
          showNotif('🎉 انتهت الجلسة! أحسنت!');
          return;
        }
        timerMinutes--;
        timerSeconds = 59;
      } else {
        timerSeconds--;
      }
      updateTimerDisplay();
    }, 1000);
  } else {
    clearInterval(timerInterval);
    timerRunning = false;
    btn.textContent = '▶ استمرار';
    playCyberSound('click');
  }
}

function resetTimer() {
  clearInterval(timerInterval);
  timerRunning = false;
  timerMinutes = 25;
  timerSeconds = 0;
  updateTimerDisplay();
  const btn = document.getElementById('timerBtn');
  if(btn) btn.textContent = '▶ ابدأ الجلسة';
  playCyberSound('click');
}

// SURVEY WIDGET LOGIC (CONDITIONAL BOT FLOW)
let surveyStep = 0; // 0: ask name, 1: ask interest
let userName = '';

function toggleSurveyChat() {
  const box = document.getElementById('surveyChatBox');
  box.classList.toggle('open');
}

function appendSurveyMsg(sender, text, htmlExtra = '') {
  const container = document.getElementById('surveyMessages');
  const div = document.createElement('div');
  div.className = `s-msg ${sender}`;
  div.innerHTML = text + htmlExtra;
  container.appendChild(div);
  container.scrollTop = container.scrollHeight;
}

function handleSurveyInput() {
  const input = document.getElementById('surveyInput');
  const val = input.value.trim();
  if(!val) return;

  appendSurveyMsg('user', val);
  input.value = '';

  setTimeout(() => {
    if(surveyStep === 0) {
      userName = val;
      surveyStep = 1;
      appendSurveyMsg('ai', `أهلاً بك يا ${userName}! هل أنت مهتم بالانضمام للعمل معنا في فريق MK (كورك) ولا مجرد زيارة وتقييم الموقع؟`);
      // Add quick choice buttons
      const extraDiv = document.createElement('div');
      extraDiv.className = 'survey-actions';
      extraDiv.innerHTML = `
        <button class="survey-option-btn" onclick="handleSurveyChoice('yes')">مهتم بالعمل والانضمام 💼</button>
        <button class="survey-option-btn" onclick="handleSurveyChoice('no')">تقييم الموقع فقط ⭐</button>
      `;
      document.getElementById('surveyMessages').appendChild(extraDiv);
      document.getElementById('surveyMessages').scrollTop = document.getElementById('surveyMessages').scrollHeight;
      document.getElementById('surveyInputArea').style.display = 'none'; // hide text input during choice
    }
  }, 500);
}

function handleSurveyChoice(choice) {
  // Remove buttons container
  const actions = document.querySelectorAll('.survey-actions');
  actions.forEach(el => el.remove());

  if(choice === 'yes') {
    appendSurveyMsg('user', 'مهتم بالانضمام للعمل والانضمام 💼');
    setTimeout(() => {
      appendSurveyMsg('ai', `رائع جداً يا ${userName}! يسعدنا انضمامك لمجتمع المبدعين. تفضل بالدخول إلى استمارة التقديم الرسمية من هنا: <br><br><a href="https://surveymars.com/q/l0irKxv2M" target="_blank" style="color:var(--neon-blue);text-decoration:underline;font-weight:bold;">اضغط هنا لفتح استمارة التقديم 🚀</a>`);
      document.getElementById('surveyInputArea').style.display = 'flex';
      surveyStep = 0; // reset flow
    }, 600);
  } else {
    appendSurveyMsg('user', 'تقييم الموقع فقط ⭐');
    setTimeout(() => {
      appendSurveyMsg('ai', `شكراً لوقتك يا ${userName}! نتمنى أن يكون الموقع قد نال إعجابك. يسعدنا دائماً رأيك لتطوير أدواتنا.`);
      document.getElementById('surveyInputArea').style.display = 'flex';
      surveyStep = 0; // reset flow
    }, 600);
  }
}

// Init focus stats
document.addEventListener('DOMContentLoaded', () => {
  const fs = document.getElementById('focusSessions');
  const fm = document.getElementById('focusMinutes');
  if(fs) fs.textContent = focusSessionsCount;
  if(fm) fm.textContent = focusTotalMinutes;
});

function showLoading(show) {
  document.getElementById('loading').classList.toggle('show', show);
}

function showNotif(msg) {
  const n = document.getElementById('notif');
  n.textContent = msg;
  n.classList.add('show');
  setTimeout(() => n.classList.remove('show'), 3000);
}

renderTasks();
</script>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-brand">
      <span class="logo">MK<span style="-webkit-text-fill-color:var(--neon-pink);color:var(--neon-pink)">.</span>AI&nbsp;TOOLS</span>
      <p>منصة ذكاء اصطناعي متكاملة لصناع المحتوى والمبدعين — أدوات قوية في مكان واحد.</p>
    </div>
    <div>
      <div class="footer-col-title">■ المطوّر</div>
      <div class="footer-dev-card">
        <div class="dev-name">محمد عنتر محمد عوض</div>
        <div class="dev-role">مطوّر الموقع والمنصة</div>
        <span class="dev-badge">FULL STACK DEV</span>
      </div>
    </div>
    <div>
      <div class="footer-col-title">■ الشركة المطوّرة</div>
      <div class="company-card">
        <div class="company-name">MK CREATIVE Agency </div>
        <div class="company-tm">™ — جميع الحقوق محفوظة</div>
        <div class="company-desc">شركة رائدة في تطوير حلول الذكاء الاصطناعي والتقنية المتقدمة.</div>
      </div>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2025 <span>MK CREATIVE Agency ™</span> — تطوير: محمد عنتر محمد عوض. جميع الحقوق محفوظة.</div>
    <div class="footer-made">BUILT WITH ❤ BY MK CREATIVE Agency </div>
  </div>
</footer>

</body>
</html> 
