<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Rafi — Android Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#050810;
  --bg2:#080d1a;
  --bg3:#0d1526;
  --cyan:#00e5ff;
  --cyan2:#00b4d8;
  --purple:#7b2fff;
  --pink:#ff2d78;
  --text:#e8eaf6;
  --muted:#8892b0;
  --border:rgba(0,229,255,0.12);
  --glow:0 0 40px rgba(0,229,255,0.15);
}
html{scroll-behavior:smooth}
body{
  background:var(--bg);
  color:var(--text);
  font-family:'DM Mono',monospace;
  overflow-x:hidden;
  cursor:none;
}

/* CUSTOM CURSOR */
.cursor{position:fixed;width:8px;height:8px;background:var(--cyan);border-radius:50%;pointer-events:none;z-index:9999;transition:transform 0.1s;mix-blend-mode:difference}
.cursor-ring{position:fixed;width:36px;height:36px;border:1px solid rgba(0,229,255,0.5);border-radius:50%;pointer-events:none;z-index:9998;transition:transform 0.15s,width 0.2s,height 0.2s}

/* NOISE TEXTURE */
body::before{
  content:'';position:fixed;inset:0;
  background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
  pointer-events:none;z-index:0;opacity:0.4;
}

/* GRID LINES */
body::after{
  content:'';position:fixed;inset:0;
  background-image:linear-gradient(rgba(0,229,255,0.03) 1px,transparent 1px),linear-gradient(90deg,rgba(0,229,255,0.03) 1px,transparent 1px);
  background-size:60px 60px;
  pointer-events:none;z-index:0;
}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:100;
  display:flex;align-items:center;justify-content:space-between;
  padding:20px 60px;
  background:rgba(5,8,16,0.85);
  backdrop-filter:blur(20px);
  border-bottom:1px solid var(--border);
}
.nav-logo{
  font-family:'Syne',sans-serif;
  font-size:22px;font-weight:800;
  background:linear-gradient(135deg,var(--cyan),var(--purple));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  letter-spacing:-0.5px;
}
.nav-links{display:flex;gap:36px;list-style:none}
.nav-links a{
  color:var(--muted);text-decoration:none;
  font-size:12px;letter-spacing:2px;text-transform:uppercase;
  transition:color 0.3s;position:relative;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;
  background:var(--cyan);transition:width 0.3s;
}
.nav-links a:hover{color:var(--cyan)}
.nav-links a:hover::after{width:100%}

/* HERO */
.hero{
  min-height:100vh;display:flex;align-items:center;
  padding:0 60px;position:relative;z-index:1;
}
.hero-content{max-width:700px}
.hero-tag{
  display:inline-flex;align-items:center;gap:8px;
  background:rgba(0,229,255,0.06);
  border:1px solid rgba(0,229,255,0.2);
  border-radius:100px;padding:6px 16px;
  font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--cyan);
  margin-bottom:32px;
  animation:fadeUp 0.8s ease both;
}
.hero-tag span{width:6px;height:6px;background:var(--cyan);border-radius:50%;animation:pulse 2s infinite}
.hero-name{
  font-family:'Syne',sans-serif;
  font-size:clamp(52px,8vw,96px);
  font-weight:800;line-height:0.95;
  letter-spacing:-3px;
  animation:fadeUp 0.8s 0.1s ease both;
}
.hero-name .line1{display:block;color:var(--text)}
.hero-name .line2{
  display:block;
  background:linear-gradient(135deg,var(--cyan) 0%,var(--purple) 60%,var(--pink) 100%);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.hero-role{
  margin-top:24px;font-size:14px;color:var(--muted);
  letter-spacing:1px;line-height:1.8;
  animation:fadeUp 0.8s 0.2s ease both;
}
.hero-role .highlight{color:var(--cyan)}
.hero-cta{
  display:flex;gap:16px;margin-top:48px;flex-wrap:wrap;
  animation:fadeUp 0.8s 0.3s ease both;
}
.btn-primary{
  display:inline-flex;align-items:center;gap:10px;
  background:var(--cyan);color:var(--bg);
  padding:14px 32px;border-radius:4px;
  font-family:'DM Mono',monospace;font-size:13px;font-weight:500;
  text-decoration:none;letter-spacing:1px;
  transition:all 0.3s;border:none;cursor:none;
}
.btn-primary:hover{background:var(--cyan2);transform:translateY(-2px);box-shadow:0 12px 40px rgba(0,229,255,0.3)}
.btn-outline{
  display:inline-flex;align-items:center;gap:10px;
  border:1px solid var(--border);color:var(--text);
  padding:14px 32px;border-radius:4px;
  font-family:'DM Mono',monospace;font-size:13px;
  text-decoration:none;letter-spacing:1px;
  transition:all 0.3s;
}
.btn-outline:hover{border-color:var(--cyan);color:var(--cyan);transform:translateY(-2px)}

/* FLOATING ORB */
.orb{
  position:absolute;right:8%;top:50%;transform:translateY(-50%);
  width:420px;height:420px;border-radius:50%;
  background:radial-gradient(circle at 40% 40%,rgba(123,47,255,0.3),rgba(0,229,255,0.1),transparent 70%);
  animation:float 8s ease-in-out infinite;
  pointer-events:none;
}
.orb::after{
  content:'';position:absolute;inset:20px;border-radius:50%;
  border:1px solid rgba(0,229,255,0.1);
  animation:spin 20s linear infinite;
}
.orb::before{
  content:'';position:absolute;inset:60px;border-radius:50%;
  border:1px dashed rgba(123,47,255,0.2);
  animation:spin 14s linear infinite reverse;
}

/* SECTION */
section{padding:120px 60px;position:relative;z-index:1}
.section-label{
  font-size:11px;letter-spacing:4px;text-transform:uppercase;
  color:var(--cyan);margin-bottom:16px;
  display:flex;align-items:center;gap:12px;
}
.section-label::before{content:'';width:40px;height:1px;background:var(--cyan)}
.section-title{
  font-family:'Syne',sans-serif;
  font-size:clamp(32px,4vw,52px);font-weight:800;
  letter-spacing:-1.5px;line-height:1.1;
  margin-bottom:60px;
}

/* ABOUT */
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:80px;align-items:center}
.about-text p{color:var(--muted);line-height:1.9;font-size:14px;margin-bottom:20px}
.about-text p strong{color:var(--text)}
.about-stats{display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-top:40px}
.stat-card{
  background:var(--bg3);border:1px solid var(--border);
  border-radius:8px;padding:24px;
  transition:border-color 0.3s,transform 0.3s;
}
.stat-card:hover{border-color:rgba(0,229,255,0.4);transform:translateY(-4px)}
.stat-num{
  font-family:'Syne',sans-serif;font-size:36px;font-weight:800;
  background:linear-gradient(135deg,var(--cyan),var(--purple));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.stat-label{font-size:11px;color:var(--muted);letter-spacing:2px;text-transform:uppercase;margin-top:4px}
.code-card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:12px;overflow:hidden;
}
.code-header{
  display:flex;align-items:center;gap:8px;
  padding:14px 20px;background:var(--bg3);border-bottom:1px solid var(--border);
}
.dot{width:12px;height:12px;border-radius:50%}
.dot.red{background:#ff5f57}.dot.yellow{background:#ffbd2e}.dot.green{background:#28ca41}
.code-filename{font-size:12px;color:var(--muted);margin-left:8px;letter-spacing:1px}
.code-body{padding:28px;font-size:13px;line-height:2}
.kw{color:#c678dd}.fn{color:#61afef}.str{color:#98c379}
.cm{color:#5c6370;font-style:italic}.num{color:#d19a66}
.cls{color:#e5c07b}.var{color:#e06c75}

/* SKILLS */
.skills-bg{background:var(--bg2)}
.skills-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(300px,1fr));gap:24px}
.skill-group{
  background:var(--bg);border:1px solid var(--border);
  border-radius:12px;padding:32px;
  transition:border-color 0.3s,transform 0.3s;
  position:relative;overflow:hidden;
}
.skill-group::before{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--purple));
  transform:scaleX(0);transform-origin:left;transition:transform 0.4s;
}
.skill-group:hover::before{transform:scaleX(1)}
.skill-group:hover{border-color:rgba(0,229,255,0.25);transform:translateY(-4px)}
.skill-icon{font-size:28px;margin-bottom:16px}
.skill-group h3{
  font-family:'Syne',sans-serif;font-size:16px;font-weight:700;
  margin-bottom:20px;color:var(--text);letter-spacing:-0.3px;
}
.skill-tags{display:flex;flex-wrap:wrap;gap:8px}
.tag{
  background:rgba(0,229,255,0.06);
  border:1px solid rgba(0,229,255,0.15);
  color:var(--cyan);
  padding:5px 12px;border-radius:4px;
  font-size:11px;letter-spacing:1px;
  transition:all 0.2s;
}
.tag:hover{background:rgba(0,229,255,0.12);border-color:var(--cyan)}
.tag.purple{
  background:rgba(123,47,255,0.08);
  border-color:rgba(123,47,255,0.2);color:#a855f7;
}
.tag.pink{
  background:rgba(255,45,120,0.08);
  border-color:rgba(255,45,120,0.2);color:#f472b6;
}

/* PROJECTS */
.projects-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(340px,1fr));gap:28px}
.project-card{
  background:var(--bg2);border:1px solid var(--border);
  border-radius:12px;padding:36px;
  transition:all 0.3s;position:relative;overflow:hidden;
  group:hover;
}
.project-card::after{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,rgba(0,229,255,0.03),rgba(123,47,255,0.03));
  opacity:0;transition:opacity 0.3s;
}
.project-card:hover{border-color:rgba(0,229,255,0.3);transform:translateY(-6px);box-shadow:var(--glow)}
.project-card:hover::after{opacity:1}
.project-num{
  font-family:'Syne',sans-serif;font-size:48px;font-weight:800;
  color:rgba(0,229,255,0.06);position:absolute;top:20px;right:28px;
  line-height:1;
}
.project-icon{font-size:32px;margin-bottom:20px}
.project-card h3{
  font-family:'Syne',sans-serif;font-size:20px;font-weight:700;
  margin-bottom:12px;letter-spacing:-0.3px;
}
.project-card p{color:var(--muted);font-size:13px;line-height:1.8;margin-bottom:24px}
.project-stack{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px}
.project-link{
  display:inline-flex;align-items:center;gap:8px;
  color:var(--cyan);font-size:12px;letter-spacing:1px;
  text-decoration:none;
  transition:gap 0.2s;
}
.project-link:hover{gap:14px}

/* CONTACT */
.contact-bg{background:var(--bg2)}
.contact-wrapper{max-width:680px;margin:0 auto;text-align:center}
.contact-wrapper .section-label{justify-content:center}
.contact-wrapper .section-label::before{display:none}
.contact-desc{color:var(--muted);font-size:14px;line-height:1.9;margin-bottom:48px}
.contact-links{display:flex;flex-wrap:wrap;justify-content:center;gap:16px}
.contact-link{
  display:inline-flex;align-items:center;gap:10px;
  background:var(--bg);border:1px solid var(--border);
  color:var(--text);padding:14px 24px;border-radius:8px;
  text-decoration:none;font-size:12px;letter-spacing:1px;
  transition:all 0.3s;
}
.contact-link:hover{border-color:var(--cyan);color:var(--cyan);transform:translateY(-3px);box-shadow:0 8px 30px rgba(0,229,255,0.15)}
.contact-link .icon{font-size:18px}

/* FOOTER */
footer{
  padding:40px 60px;
  border-top:1px solid var(--border);
  display:flex;justify-content:space-between;align-items:center;
  position:relative;z-index:1;
}
.footer-logo{
  font-family:'Syne',sans-serif;font-weight:800;
  background:linear-gradient(135deg,var(--cyan),var(--purple));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.footer-copy{font-size:12px;color:var(--muted);letter-spacing:1px}

/* ANIMATIONS */
@keyframes fadeUp{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:translateY(0)}}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:0.5;transform:scale(0.8)}}
@keyframes float{0%,100%{transform:translateY(-50%) translateX(0)}50%{transform:translateY(calc(-50% - 20px)) translateX(10px)}}
@keyframes spin{from{transform:rotate(0deg)}to{transform:rotate(360deg)}}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}

.typed::after{content:'|';color:var(--cyan);animation:blink 1s infinite}

/* SCROLL REVEAL */
.reveal{opacity:0;transform:translateY(30px);transition:opacity 0.7s ease,transform 0.7s ease}
.reveal.visible{opacity:1;transform:translateY(0)}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--cyan);border-radius:2px}

@media(max-width:900px){
  nav{padding:16px 24px}
  .hero{padding:0 24px}
  .orb{display:none}
  section{padding:80px 24px}
  .about-grid{grid-template-columns:1fr}
  footer{padding:32px 24px;flex-direction:column;gap:12px;text-align:center}
}
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">RAFI.</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-content">
    <div class="hero-tag">
      <span></span>
      Available for work
    </div>
    <h1 class="hero-name">
      <span class="line1">Hi, I'm</span>
      <span class="line2">Rafi.</span>
    </h1>
    <p class="hero-role">
      Android Developer based in <span class="highlight">Bangladesh 🇧🇩</span><br/>
      Building apps with <span class="highlight">Java · Firebase · RESTful APIs</span><br/>
      <span class="typed" id="typed"></span>
    </p>
    <div class="hero-cta">
      <a href="#projects" class="btn-primary">View Projects →</a>
      <a href="#contact" class="btn-outline">Get in Touch</a>
    </div>
  </div>
  <div class="orb"></div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-grid">
    <div class="about-text reveal">
      <div class="section-label">About Me</div>
      <h2 class="section-title" style="margin-bottom:28px">Crafting apps<br/>people <em>love</em>.</h2>
      <p>I'm a passionate <strong>Android App Developer</strong> with deep expertise in Java and Android Studio. I specialize in building efficient, robust, and beautiful mobile applications that deliver seamless user experiences.</p>
      <p>From architecting <strong>RESTful API integrations</strong> to designing intuitive UIs with Figma — I handle the full development lifecycle. I take pride in clean code, thoughtful UX, and shipping products that actually work.</p>
      <div class="about-stats">
        <div class="stat-card">
          <div class="stat-num">3+</div>
          <div class="stat-label">Years Experience</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">20+</div>
          <div class="stat-label">Apps Built</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">100%</div>
          <div class="stat-label">Client Satisfaction</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">∞</div>
          <div class="stat-label">Cups of Coffee</div>
        </div>
      </div>
    </div>
    <div class="reveal" style="transition-delay:0.15s">
      <div class="code-card">
        <div class="code-header">
          <div class="dot red"></div>
          <div class="dot yellow"></div>
          <div class="dot green"></div>
          <span class="code-filename">Developer.java</span>
        </div>
        <div class="code-body">
<span class="kw">public class</span> <span class="cls">Rafi</span> {<br/>
<br/>
&nbsp;&nbsp;<span class="kw">private</span> <span class="cls">String</span> <span class="var">name</span> = <span class="str">"Rafi"</span>;<br/>
&nbsp;&nbsp;<span class="kw">private</span> <span class="cls">String</span> <span class="var">role</span> = <span class="str">"Android Dev"</span>;<br/>
&nbsp;&nbsp;<span class="kw">private</span> <span class="cls">String</span> <span class="var">base</span> = <span class="str">"Bangladesh 🇧🇩"</span>;<br/>
<br/>
&nbsp;&nbsp;<span class="cm">// Core stack</span><br/>
&nbsp;&nbsp;<span class="cls">String</span>[] <span class="var">stack</span> = {<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"Java"</span>, <span class="str">"Firebase"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"REST APIs"</span>, <span class="str">"AWS"</span><br/>
&nbsp;&nbsp;};<br/>
<br/>
&nbsp;&nbsp;<span class="kw">boolean</span> <span class="var">available</span> = <span class="num">true</span>;<br/>
<br/>
&nbsp;&nbsp;<span class="kw">public</span> <span class="cls">String</span> <span class="fn">passion</span>() {<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="kw">return</span> <span class="str">"Solving real problems"</span>;<br/>
&nbsp;&nbsp;}<br/>
}
        </div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills" class="skills-bg">
  <div class="section-label reveal">Skills</div>
  <h2 class="section-title reveal">My Tech Stack</h2>
  <div class="skills-grid">
    <div class="skill-group reveal">
      <div class="skill-icon">📱</div>
      <h3>Mobile Development</h3>
      <div class="skill-tags">
        <span class="tag">Java</span>
        <span class="tag">Android Studio</span>
        <span class="tag">XML Layouts</span>
        <span class="tag">Material Design</span>
        <span class="tag">Jetpack</span>
      </div>
    </div>
    <div class="skill-group reveal" style="transition-delay:0.1s">
      <div class="skill-icon">☁️</div>
      <h3>Cloud & Backend</h3>
      <div class="skill-tags">
        <span class="tag purple">Firebase</span>
        <span class="tag purple">AWS</span>
        <span class="tag purple">Google Cloud</span>
        <span class="tag purple">PHP</span>
        <span class="tag purple">SQL</span>
      </div>
    </div>
    <div class="skill-group reveal" style="transition-delay:0.2s">
      <div class="skill-icon">🌐</div>
      <h3>Web & APIs</h3>
      <div class="skill-tags">
        <span class="tag">RESTful APIs</span>
        <span class="tag">HTML5</span>
        <span class="tag">CSS3</span>
        <span class="tag">JavaScript</span>
      </div>
    </div>
    <div class="skill-group reveal" style="transition-delay:0.3s">
      <div class="skill-icon">🧪</div>
      <h3>Testing & QA</h3>
      <div class="skill-tags">
        <span class="tag pink">JUnit</span>
        <span class="tag pink">Espresso</span>
        <span class="tag pink">Unit Testing</span>
        <span class="tag pink">UI Testing</span>
      </div>
    </div>
    <div class="skill-group reveal" style="transition-delay:0.4s">
      <div class="skill-icon">🛠️</div>
      <h3>Tools & DevOps</h3>
      <div class="skill-tags">
        <span class="tag">Git</span>
        <span class="tag">GitHub</span>
        <span class="tag">VS Code</span>
        <span class="tag">Figma</span>
      </div>
    </div>
    <div class="skill-group reveal" style="transition-delay:0.5s">
      <div class="skill-icon">🎨</div>
      <h3>Design</h3>
      <div class="skill-tags">
        <span class="tag purple">UI/UX Design</span>
        <span class="tag purple">Prototyping</span>
        <span class="tag purple">Wireframing</span>
        <span class="tag purple">Figma</span>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label reveal">Projects</div>
  <h2 class="section-title reveal">What I've Built</h2>
  <div class="projects-grid">
    <div class="project-card reveal">
      <div class="project-num">01</div>
      <div class="project-icon">🛒</div>
      <h3>E-Commerce App</h3>
      <p>Full-featured Android shopping app with real-time inventory, Firebase auth, and payment gateway integration.</p>
      <div class="project-stack">
        <span class="tag">Java</span><span class="tag">Firebase</span><span class="tag">REST API</span>
      </div>
      <a href="#" class="project-link">View Project →</a>
    </div>
    <div class="project-card reveal" style="transition-delay:0.1s">
      <div class="project-num">02</div>
      <div class="project-icon">💬</div>
      <h3>Real-Time Chat App</h3>
      <p>Messaging application with end-to-end encryption, push notifications, and media sharing built on Firebase.</p>
      <div class="project-stack">
        <span class="tag">Java</span><span class="tag">Firebase</span><span class="tag">FCM</span>
      </div>
      <a href="#" class="project-link">View Project →</a>
    </div>
    <div class="project-card reveal" style="transition-delay:0.2s">
      <div class="project-num">03</div>
      <div class="project-icon">📊</div>
      <h3>Task Manager Pro</h3>
      <p>Productivity app with team collaboration, deadline tracking, and SQL-powered local database for offline use.</p>
      <div class="project-stack">
        <span class="tag">Java</span><span class="tag">SQL</span><span class="tag">AWS</span>
      </div>
      <a href="#" class="project-link">View Project →</a>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact" class="contact-bg">
  <div class="contact-wrapper">
    <div class="section-label reveal">Contact</div>
    <h2 class="section-title reveal">Let's Work Together</h2>
    <p class="contact-desc reveal">
      Got a project in mind? I'm always open to discussing new opportunities,<br/>
      creative ideas, or how I can help bring your vision to life.
    </p>
    <div class="contact-links reveal">
      <a href="mailto:your@email.com" class="contact-link">
        <span class="icon">✉️</span> Email Me
      </a>
      <a href="https://linkedin.com" class="contact-link">
        <span class="icon">💼</span> LinkedIn
      </a>
      <a href="https://github.com" class="contact-link">
        <span class="icon">🐙</span> GitHub
      </a>
      <a href="https://t.me" class="contact-link">
        <span class="icon">✈️</span> Telegram
      </a>
      <a href="https://discord.com" class="contact-link">
        <span class="icon">🎮</span> Discord
      </a>
      <a href="https://facebook.com" class="contact-link">
        <span class="icon">📘</span> Facebook
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">RAFI.</div>
  <div class="footer-copy">© 2025 Rafi. Crafted with ☕ & passion.</div>
</footer>

<script>
// Cursor
const cursor=document.getElementById('cursor');
const ring=document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX;my=e.clientY;
  cursor.style.left=mx-4+'px';cursor.style.top=my-4+'px';
});
(function animRing(){
  rx+=(mx-rx)*0.12;ry+=(my-ry)*0.12;
  ring.style.left=rx-18+'px';ring.style.top=ry-18+'px';
  requestAnimationFrame(animRing);
})();
document.querySelectorAll('a,button').forEach(el=>{
  el.addEventListener('mouseenter',()=>{ring.style.width='56px';ring.style.height='56px';ring.style.borderColor='rgba(0,229,255,0.8)'});
  el.addEventListener('mouseleave',()=>{ring.style.width='36px';ring.style.height='36px';ring.style.borderColor='rgba(0,229,255,0.5)'});
});

// Typed text
const phrases=["Turning ideas into apps.","Clean code. Great UX.","Firebase & Java expert.","Available for freelance."];
let pi=0,ci=0,deleting=false,wait=0;
const el=document.getElementById('typed');
(function type(){
  if(wait>0){wait--;setTimeout(type,50);return}
  const phrase=phrases[pi];
  if(!deleting){
    el.textContent=phrase.slice(0,++ci);
    if(ci===phrase.length){deleting=true;wait=40}
    setTimeout(type,80);
  } else {
    el.textContent=phrase.slice(0,--ci);
    if(ci===0){deleting=false;pi=(pi+1)%phrases.length;wait=10}
    setTimeout(type,40);
  }
})();

// Scroll reveal
const observer=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible')}});
},{threshold:0.1});
document.querySelectorAll('.reveal').forEach(el=>observer.observe(el));
</script>
</body>
</html>
