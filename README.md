<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>Hanane Saharaoui — Software Engineer × AI</title>
    <link rel="preconnect" href="https://fonts.googleapis.com"/>
    <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@300;400;500;600;700;800;900&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet"/>
    <style>
        *,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
        :root{
            --bg-primary:#0a0a12;--bg-secondary:#0f0c29;--bg-card:#12101f;
            --purple-100:#e0aaff;--purple-200:#c77dff;--purple-300:#9d4edd;
            --purple-400:#7b2d8b;--purple-500:#302b63;--purple-600:#24243e;
            --text-primary:#e8e6f0;--text-secondary:#a09cb5;--text-muted:#6b6780;
            --glow:rgba(199,125,255,.15);--glow-strong:rgba(199,125,255,.35);
        }
        html{scroll-behavior:smooth;scrollbar-width:thin;scrollbar-color:var(--purple-300) var(--bg-primary)}
        ::-webkit-scrollbar{width:6px}
        ::-webkit-scrollbar-track{background:var(--bg-primary)}
        ::-webkit-scrollbar-thumb{background:var(--purple-300);border-radius:3px}
        body{font-family:'Inter',sans-serif;background:var(--bg-primary);color:var(--text-primary);overflow-x:hidden;line-height:1.7}

        /* === PARTICLE CANVAS === */
        #particles{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;pointer-events:none}

        /* === CURSOR GLOW === */
        .cursor-glow{position:fixed;width:400px;height:400px;border-radius:50%;pointer-events:none;z-index:1;background:radial-gradient(circle,rgba(157,78,221,.08),transparent 70%);transform:translate(-50%,-50%);transition:opacity .3s}

        /* === NAV === */
        nav{position:fixed;top:0;left:0;right:0;z-index:100;padding:1rem 2rem;backdrop-filter:blur(20px);background:rgba(10,10,18,.7);border-bottom:1px solid rgba(199,125,255,.08);transition:all .3s}
        nav.scrolled{background:rgba(10,10,18,.92);box-shadow:0 4px 30px rgba(0,0,0,.4)}
        .nav-inner{max-width:1200px;margin:0 auto;display:flex;justify-content:space-between;align-items:center}
        .nav-logo{font-family:'Space Grotesk',sans-serif;font-weight:700;font-size:1.2rem;color:var(--purple-200);text-decoration:none;letter-spacing:-0.5px}
        .nav-logo span{color:var(--purple-300);opacity:.6}
        .nav-links{display:flex;gap:2rem;list-style:none}
        .nav-links a{color:var(--text-secondary);text-decoration:none;font-size:.85rem;font-weight:500;letter-spacing:.5px;text-transform:uppercase;transition:color .3s;position:relative}
        .nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:2px;background:var(--purple-200);transition:width .3s;border-radius:1px}
        .nav-links a:hover{color:var(--purple-200)}
        .nav-links a:hover::after{width:100%}
        .nav-toggle{display:none;background:none;border:none;color:var(--purple-200);font-size:1.5rem;cursor:pointer}

        /* === HERO === */
        .hero{position:relative;min-height:100vh;display:flex;align-items:center;justify-content:center;text-align:center;padding:6rem 2rem 4rem;overflow:hidden}
        .hero::before{content:'';position:absolute;top:-50%;left:-50%;width:200%;height:200%;background:radial-gradient(ellipse at 30% 50%,rgba(48,43,99,.4),transparent 50%),radial-gradient(ellipse at 70% 50%,rgba(123,45,139,.3),transparent 50%);animation:heroGlow 8s ease-in-out infinite alternate}
        @keyframes heroGlow{0%{transform:translate(0,0) scale(1)}100%{transform:translate(-2%,2%) scale(1.05)}}
        .hero-content{position:relative;z-index:2;max-width:800px}
        .hero-badge{display:inline-flex;align-items:center;gap:.5rem;padding:.4rem 1.2rem;border:1px solid rgba(199,125,255,.25);border-radius:50px;font-size:.75rem;font-family:'JetBrains Mono',monospace;color:var(--purple-200);margin-bottom:2rem;backdrop-filter:blur(10px);background:rgba(199,125,255,.05)}
        .hero-badge .dot{width:6px;height:6px;border-radius:50%;background:var(--purple-200);animation:pulse 2s ease-in-out infinite}
        @keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.4;transform:scale(.8)}}
        .hero h1{font-family:'Space Grotesk',sans-serif;font-size:clamp(2.5rem,6vw,4.5rem);font-weight:800;letter-spacing:-2px;line-height:1.1;margin-bottom:1rem;background:linear-gradient(135deg,#e0aaff 0%,#c77dff 40%,#9d4edd 80%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
        .hero-subtitle{font-size:clamp(1rem,2vw,1.3rem);color:var(--text-secondary);font-weight:300;margin-bottom:2.5rem;letter-spacing:.5px}
        .hero-subtitle strong{color:var(--purple-200);font-weight:600}
        .hero-typing{font-family:'JetBrains Mono',monospace;font-size:.9rem;color:var(--purple-300);min-height:1.5em;margin-bottom:2.5rem}
        .hero-typing .cursor{animation:blink 1s step-end infinite;color:var(--purple-200)}
        @keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
        .hero-actions{display:flex;gap:1rem;justify-content:center;flex-wrap:wrap}
        .btn{padding:.8rem 2rem;border-radius:8px;font-size:.9rem;font-weight:600;text-decoration:none;transition:all .3s;cursor:pointer;display:inline-flex;align-items:center;gap:.5rem;border:none;font-family:'Inter',sans-serif}
        .btn-primary{background:linear-gradient(135deg,var(--purple-300),var(--purple-400));color:#fff;box-shadow:0 4px 20px rgba(157,78,221,.3)}
        .btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 30px rgba(157,78,221,.5)}
        .btn-secondary{background:transparent;color:var(--purple-200);border:1px solid rgba(199,125,255,.3)}
        .btn-secondary:hover{background:rgba(199,125,255,.08);border-color:var(--purple-200);transform:translateY(-2px)}
        .hero-stats{display:flex;gap:3rem;justify-content:center;margin-top:3rem;padding-top:2rem;border-top:1px solid rgba(199,125,255,.1)}
        .stat{text-align:center}
        .stat-number{font-family:'Space Grotesk',sans-serif;font-size:1.8rem;font-weight:700;color:var(--purple-200)}
        .stat-label{font-size:.75rem;color:var(--text-muted);text-transform:uppercase;letter-spacing:1px;margin-top:.2rem}
        .scroll-indicator{position:absolute;bottom:2rem;left:50%;transform:translateX(-50%);display:flex;flex-direction:column;align-items:center;gap:.5rem;color:var(--text-muted);font-size:.7rem;letter-spacing:2px;text-transform:uppercase;animation:float 3s ease-in-out infinite}
        @keyframes float{0%,100%{transform:translateX(-50%) translateY(0)}50%{transform:translateX(-50%) translateY(-8px)}}
        .scroll-indicator .line{width:1px;height:30px;background:linear-gradient(to bottom,var(--purple-300),transparent)}

        /* === SECTIONS === */
        section{position:relative;z-index:2;padding:6rem 2rem}
        .section-inner{max-width:1100px;margin:0 auto}
        .section-header{text-align:center;margin-bottom:4rem}
        .section-tag{font-family:'JetBrains Mono',monospace;font-size:.75rem;color:var(--purple-300);text-transform:uppercase;letter-spacing:3px;margin-bottom:.8rem;display:block}
        .section-title{font-family:'Space Grotesk',sans-serif;font-size:clamp(1.8rem,4vw,2.8rem);font-weight:700;letter-spacing:-1px;margin-bottom:1rem;background:linear-gradient(135deg,var(--purple-100),var(--purple-200));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
        .section-desc{color:var(--text-secondary);max-width:600px;margin:0 auto;font-size:.95rem}
        .divider{height:1px;background:linear-gradient(to right,transparent,var(--purple-500),transparent);margin:0 auto;max-width:800px}

        /* === ABOUT === */
        .about-grid{display:grid;grid-template-columns:1fr 1fr;gap:3rem;align-items:start}
        .about-terminal{background:var(--bg-card);border:1px solid rgba(199,125,255,.1);border-radius:12px;overflow:hidden;box-shadow:0 20px 60px rgba(0,0,0,.3)}
        .terminal-header{display:flex;align-items:center;gap:.5rem;padding:.8rem 1.2rem;background:rgba(199,125,255,.05);border-bottom:1px solid rgba(199,125,255,.08)}
        .terminal-dot{width:10px;height:10px;border-radius:50%}
        .terminal-dot.r{background:#ff5f56}.terminal-dot.y{background:#ffbd2e}.terminal-dot.g{background:#27c93f}
        .terminal-title{font-family:'JetBrains Mono',monospace;font-size:.7rem;color:var(--text-muted);margin-left:auto}
        .terminal-body{padding:1.5rem;font-family:'JetBrains Mono',monospace;font-size:.8rem;line-height:2}
        .terminal-body .key{color:var(--purple-200)}
        .terminal-body .val{color:var(--text-secondary)}
        .terminal-body .comment{color:var(--text-muted);font-style:italic}
        .about-text{display:flex;flex-direction:column;gap:1.5rem}
        .about-text p{color:var(--text-secondary);font-size:.95rem;line-height:1.8}
        .about-text p strong{color:var(--purple-200);font-weight:600}
        .about-highlight{padding:1.5rem;border-left:3px solid var(--purple-300);background:rgba(199,125,255,.03);border-radius:0 8px 8px 0}
        .about-highlight p{font-style:italic;color:var(--text-secondary);font-size:.9rem}
        .about-langs{display:flex;gap:1rem;flex-wrap:wrap;margin-top:.5rem}
        .lang-badge{padding:.3rem .8rem;border-radius:6px;font-size:.75rem;font-weight:500;background:rgba(199,125,255,.08);color:var(--purple-200);border:1px solid rgba(199,125,255,.15)}

        /* === TECH STACK === */
        .tech-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:1.5rem}
        .tech-card{background:var(--bg-card);border:1px solid rgba(199,125,255,.08);border-radius:12px;padding:2rem 1.5rem;text-align:center;transition:all .4s;position:relative;overflow:hidden}
        .tech-card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:linear-gradient(90deg,transparent,var(--purple-300),transparent);opacity:0;transition:opacity .4s}
        .tech-card:hover{transform:translateY(-5px);border-color:rgba(199,125,255,.2);box-shadow:0 10px 40px rgba(0,0,0,.3)}
        .tech-card:hover::before{opacity:1}
        .tech-icon{font-size:2rem;margin-bottom:1rem}
        .tech-card h4{font-family:'Space Grotesk',sans-serif;font-weight:600;color:var(--purple-200);margin-bottom:.8rem;font-size:.95rem}
        .tech-tags{display:flex;flex-wrap:wrap;gap:.4rem;justify-content:center}
        .tech-tag{padding:.2rem .6rem;border-radius:4px;font-size:.7rem;font-family:'JetBrains Mono',monospace;background:rgba(199,125,255,.06);color:var(--text-secondary)}

        /* === PROJECTS === */
        .project-card{background:var(--bg-card);border:1px solid rgba(199,125,255,.08);border-radius:16px;padding:2.5rem;margin-bottom:2rem;transition:all .4s;position:relative;overflow:hidden}
        .project-card::after{content:'';position:absolute;top:0;left:0;right:0;bottom:0;background:linear-gradient(135deg,rgba(199,125,255,.02),transparent);pointer-events:none}
        .project-card:hover{border-color:rgba(199,125,255,.2);box-shadow:0 20px 60px rgba(0,0,0,.3);transform:translateY(-3px)}
        .project-meta{display:flex;align-items:center;gap:1rem;margin-bottom:1rem;flex-wrap:wrap}
        .project-org{font-family:'JetBrains Mono',monospace;font-size:.75rem;padding:.3rem .8rem;border-radius:6px;background:rgba(199,125,255,.1);color:var(--purple-200)}
        .project-type{font-size:.75rem;color:var(--text-muted)}
        .project-card h3{font-family:'Space Grotesk',sans-serif;font-size:1.4rem;font-weight:700;color:var(--purple-100);margin-bottom:.8rem;letter-spacing:-.5px}
        .project-card>p{color:var(--text-secondary);font-size:.9rem;margin-bottom:1.5rem;position:relative;z-index:1}
        .project-features{display:grid;grid-template-columns:1fr 1fr;gap:.8rem;margin-bottom:1.5rem}
        .feature{display:flex;align-items:center;gap:.6rem;padding:.6rem .8rem;border-radius:8px;background:rgba(199,125,255,.03);font-size:.8rem;color:var(--text-secondary);border:1px solid rgba(199,125,255,.05)}
        .feature-icon{font-size:1rem}
        .project-stack{display:flex;flex-wrap:wrap;gap:.5rem}
        .stack-tag{padding:.3rem .7rem;border-radius:6px;font-size:.7rem;font-family:'JetBrains Mono',monospace;background:rgba(157,78,221,.1);color:var(--purple-200);border:1px solid rgba(157,78,221,.15)}

        /* === EXPERIENCE MINI === */
        .exp-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;margin-top:1rem}
        .exp-card{background:var(--bg-card);border:1px solid rgba(199,125,255,.08);border-radius:12px;padding:1.8rem;transition:all .3s}
        .exp-card:hover{border-color:rgba(199,125,255,.2);transform:translateY(-3px)}
        .exp-card h4{font-family:'Space Grotesk',sans-serif;color:var(--purple-200);font-weight:600;margin-bottom:.3rem}
        .exp-card .exp-org{font-size:.8rem;color:var(--purple-300);font-weight:500;margin-bottom:.8rem}
        .exp-card p{font-size:.85rem;color:var(--text-secondary);line-height:1.7}

        /* === EDUCATION === */
        .edu-timeline{position:relative;display:flex;gap:3rem;justify-content:center;flex-wrap:wrap}
        .edu-card{flex:1;min-width:280px;max-width:400px;background:var(--bg-card);border:1px solid rgba(199,125,255,.1);border-radius:16px;padding:2rem;position:relative;transition:all .4s}
        .edu-card:hover{transform:translateY(-5px);border-color:rgba(199,125,255,.25);box-shadow:0 15px 50px rgba(0,0,0,.3)}
        .edu-icon{width:50px;height:50px;border-radius:12px;background:linear-gradient(135deg,var(--purple-300),var(--purple-400));display:flex;align-items:center;justify-content:center;font-size:1.5rem;margin-bottom:1.2rem}
        .edu-card h4{font-family:'Space Grotesk',sans-serif;font-weight:700;color:var(--purple-100);font-size:1.1rem;margin-bottom:.3rem}
        .edu-card .edu-degree{color:var(--purple-200);font-size:.85rem;font-weight:500;margin-bottom:.8rem}
        .edu-card .edu-date{font-family:'JetBrains Mono',monospace;font-size:.75rem;color:var(--text-muted);margin-bottom:1rem;display:flex;align-items:center;gap:.5rem}
        .edu-card .edu-date .check{color:#27c93f}
        .edu-topics{display:flex;flex-wrap:wrap;gap:.4rem}
        .edu-topic{padding:.2rem .6rem;border-radius:4px;font-size:.7rem;background:rgba(199,125,255,.06);color:var(--text-secondary)}
        .edu-university{text-align:center;margin-bottom:2.5rem;padding:1.5rem;border:1px solid rgba(199,125,255,.08);border-radius:12px;background:rgba(199,125,255,.02)}
        .edu-university h3{font-family:'Space Grotesk',sans-serif;color:var(--purple-200);font-size:1.1rem;margin-bottom:.2rem}
        .edu-university p{font-size:.85rem;color:var(--text-muted)}

        /* === CERTS === */
        .cert-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem}
        .cert-card{display:flex;align-items:center;gap:1.2rem;background:var(--bg-card);border:1px solid rgba(199,125,255,.08);border-radius:12px;padding:1.5rem;transition:all .3s}
        .cert-card:hover{border-color:rgba(199,125,255,.2);transform:translateY(-2px)}
        .cert-icon{width:48px;height:48px;border-radius:10px;background:rgba(199,125,255,.08);display:flex;align-items:center;justify-content:center;font-size:1.4rem;flex-shrink:0}
        .cert-info h4{font-size:.9rem;font-weight:600;color:var(--purple-200);margin-bottom:.2rem}
        .cert-info p{font-size:.8rem;color:var(--text-muted)}
        .cert-check{margin-left:auto;color:#27c93f;font-size:1.2rem}

        /* === GITHUB STATS === */
        .stats-grid{display:grid;grid-template-columns:1fr 1fr;gap:1.5rem}
        .stats-grid img{width:100%;border-radius:12px;border:1px solid rgba(199,125,255,.08);transition:transform .3s}
        .stats-grid img:hover{transform:scale(1.02)}
        .stats-full{grid-column:1/-1}
        .stats-full img{width:100%}

        /* === CONTACT === */
        .contact-section{background:linear-gradient(180deg,var(--bg-primary),rgba(48,43,99,.15),var(--bg-primary))}
        .contact-inner{text-align:center}
        .contact-inner>p{color:var(--text-secondary);max-width:550px;margin:0 auto 2.5rem;font-size:.95rem}
        .contact-btns{display:flex;gap:1rem;justify-content:center;flex-wrap:wrap;margin-bottom:3rem}
        .contact-quote{font-style:italic;color:var(--text-muted);font-size:.9rem;margin-top:2rem;padding-top:2rem;border-top:1px solid rgba(199,125,255,.08)}

        /* === FOOTER === */
        footer{text-align:center;padding:2rem;color:var(--text-muted);font-size:.8rem;position:relative;z-index:2;border-top:1px solid rgba(199,125,255,.05)}
        footer a{color:var(--purple-300);text-decoration:none}

        /* === ANIMATIONS === */
        .reveal{opacity:0;transform:translateY(40px);transition:all .8s cubic-bezier(.16,1,.3,1)}
        .reveal.visible{opacity:1;transform:translateY(0)}
        .reveal-delay-1{transition-delay:.1s}
        .reveal-delay-2{transition-delay:.2s}
        .reveal-delay-3{transition-delay:.3s}
        .reveal-delay-4{transition-delay:.4s}

        /* === RESPONSIVE === */
        @media(max-width:768px){
            .nav-links{display:none;position:fixed;top:60px;left:0;right:0;background:rgba(10,10,18,.97);flex-direction:column;padding:2rem;gap:1.5rem;border-bottom:1px solid rgba(199,125,255,.1)}
            .nav-links.open{display:flex}
            .nav-toggle{display:block}
            .about-grid{grid-template-columns:1fr}
            .project-features{grid-template-columns:1fr}
            .exp-grid,.cert-grid,.stats-grid{grid-template-columns:1fr}
            .hero-stats{gap:1.5rem}
            .hero h1{font-size:2.2rem}
        }

        /* Glitch effect for name on hover */
        .glitch:hover{animation:glitch .3s infinite}
        @keyframes glitch{
            0%{text-shadow:2px 0 var(--purple-300),-2px 0 var(--purple-400)}
            25%{text-shadow:-2px -1px var(--purple-300),2px 1px var(--purple-400)}
            50%{text-shadow:1px 2px var(--purple-300),-1px -2px var(--purple-400)}
            75%{text-shadow:-1px 1px var(--purple-300),1px -1px var(--purple-400)}
            100%{text-shadow:2px -2px var(--purple-300),-2px 2px var(--purple-400)}
        }

        /* Floating orbs background */
        .orb{position:absolute;border-radius:50%;filter:blur(80px);opacity:.12;pointer-events:none;z-index:0}
        .orb-1{width:500px;height:500px;background:var(--purple-300);top:10%;left:-10%;animation:orbMove1 20s ease-in-out infinite}
        .orb-2{width:400px;height:400px;background:var(--purple-400);bottom:10%;right:-10%;animation:orbMove2 25s ease-in-out infinite}
        .orb-3{width:300px;height:300px;background:var(--purple-500);top:50%;left:50%;animation:orbMove3 18s ease-in-out infinite}
        @keyframes orbMove1{0%,100%{transform:translate(0,0)}50%{transform:translate(100px,50px)}}
        @keyframes orbMove2{0%,100%{transform:translate(0,0)}50%{transform:translate(-80px,-60px)}}
        @keyframes orbMove3{0%,100%{transform:translate(-50%,-50%)}50%{transform:translate(-30%,-60%)}}
    </style>

</head>
<body>

<!-- Particle Canvas -->

<canvas id="particles"></canvas>

<!-- Cursor Glow -->
<div class="cursor-glow" id="cursorGlow"></div>

<!-- Floating Orbs -->
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>
<div class="orb orb-3"></div>

<!-- Navigation -->
<nav id="navbar">
    <div class="nav-inner">
        <a href="#" class="nav-logo">HS<span>.</span>dev</a>
        <button class="nav-toggle" id="navToggle" aria-label="Toggle menu">☰</button>
        <ul class="nav-links" id="navLinks">
            <li><a href="#about">About</a></li>
            <li><a href="#arsenal">Arsenal</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#education">Education</a></li>
            <li><a href="#stats">Stats</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </div>
</nav>

<!-- ===================== HERO ===================== -->
<section class="hero" id="hero">
    <div class="hero-content">
        <div class="hero-badge reveal">
            <span class="dot"></span>
            Open to Opportunities
        </div>
        <h1 class="glitch reveal reveal-delay-1">Hanane Saharaoui</h1>
        <p class="hero-subtitle reveal reveal-delay-2">
            <strong>Software Engineer</strong> — Full-Stack × Artificial Intelligence
        </p>
        <div class="hero-typing reveal reveal-delay-3">
            <span id="typewriter"></span><span class="cursor">|</span>
        </div>
        <div class="hero-actions reveal reveal-delay-4">
            <a href="#projects" class="btn btn-primary">⚡ View My Work</a>
            <a href="mailto:hanane.sahraoui20@gmail.com" class="btn btn-secondary">✉ Get In Touch</a>
        </div>
        <div class="hero-stats reveal reveal-delay-4">
            <div class="stat">
                <div class="stat-number" data-count="5">0</div>
                <div class="stat-label">Years Studying</div>
            </div>
            <div class="stat">
                <div class="stat-number" data-count="3">0</div>
                <div class="stat-label">Major Projects</div>
            </div>
            <div class="stat">
                <div class="stat-number" data-count="3">0</div>
                <div class="stat-label">Languages Spoken</div>
            </div>
        </div>
    </div>
    <div class="scroll-indicator">
        <span>scroll</span>
        <div class="line"></div>
    </div>
</section>

<div class="divider"></div>

<!-- ===================== ABOUT ===================== -->
<section id="about">
    <div class="section-inner">
        <div class="section-header">
            <span class="section-tag reveal">// about me</span>
            <h2 class="section-title reveal">whoami</h2>
        </div>
        <div class="about-grid">
            <div class="about-terminal reveal">
                <div class="terminal-header">
                    <span class="terminal-dot r"></span>
                    <span class="terminal-dot y"></span>
                    <span class="terminal-dot g"></span>
                    <span class="terminal-title">hanane@portfolio:~$</span>
                </div>
                <div class="terminal-body">
                    <span class="comment"># Personal config</span><br/>
                    <span class="key">Name</span>        <span class="val">: Hanane Saharaoui</span><br/>
                    <span class="key">Role</span>        <span class="val">: Software Engineer</span><br/>
                    <span class="key">Degree</span>      <span class="val">: M.Sc. Software Engineering</span><br/>
                    <span class="key">University</span>  <span class="val">: USTHB '25</span><br/>
                    <span class="key">Location</span>    <span class="val">: Boumerdes, Algeria 🇩🇿</span><br/>
                    <span class="key">Focus</span>       <span class="val">: Full-Stack · AI · Data</span><br/>
                    <span class="key">Status</span>      <span class="val">: Open to opportunities</span><br/>
                    <br/>
                    <span class="comment"># Languages</span><br/>
                    <span class="key">Arabic</span>      <span class="val">: ████████████ native</span><br/>
                    <span class="key">French</span>      <span class="val">: ██████████░░ fluent</span><br/>
                    <span class="key">English</span>     <span class="val">: ██████████░░ fluent</span><br/>
                    <br/>
                    <span class="comment"># Superpower</span><br/>
                    <span class="val">Turning complex problems</span><br/>
                    <span class="val">into elegant systems ✨</span>
                </div>
            </div>
            <div class="about-text reveal reveal-delay-1">
                <p>
                    I build at the intersection of <strong>intelligent systems</strong> and <strong>great user experiences</strong> — from architecting real-time AI pipelines to writing the frontend layer people actually love to use.
                </p>
                <div class="about-highlight">
                    <p>
                        "Calm under pressure, obsessive about quality, and deeply motivated by impact. The best engineers don't just solve problems — they reframe them."
                    </p>
                </div>
                <p>
                    With a Master's from <strong>USTHB</strong> in Software Engineering, I specialize in building end-to-end systems that combine <strong>machine learning</strong>, <strong>data engineering</strong>, and <strong>modern web technologies</strong>.
                </p>
                <div class="about-langs">
                    <span class="lang-badge">🇩🇿 Arabic (native)</span>
                    <span class="lang-badge">🇫🇷 French (fluent)</span>
                    <span class="lang-badge">🇬🇧 English (fluent)</span>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="divider"></div>

<!-- ===================== TECH STACK ===================== -->
<section id="arsenal">
    <div class="section-inner">
        <div class="section-header">
            <span class="section-tag reveal">// tech stack</span>
            <h2 class="section-title reveal">⚡ Arsenal</h2>
            <p class="section-desc reveal">The tools and technologies I wield to build impactful solutions</p>
        </div>
        <div class="tech-grid">
            <div class="tech-card reveal">
                <div class="tech-icon">🎨</div>
                <h4>Frontend</h4>
                <div class="tech-tags">
                    <span class="tech-tag">HTML5</span>
                    <span class="tech-tag">CSS3</span>
                    <span class="tech-tag">JavaScript</span>
                    <span class="tech-tag">React</span>
                </div>
            </div>
            <div class="tech-card reveal reveal-delay-1">
                <div class="tech-icon">⚙️</div>
                <h4>Backend</h4>
                <div class="tech-tags">
                    <span class="tech-tag">Python</span>
                    <span class="tech-tag">Flask</span>
                    <span class="tech-tag">Laravel</span>
                    <span class="tech-tag">REST APIs</span>
                </div>
            </div>
            <div class="tech-card reveal reveal-delay-2">
                <div class="tech-icon">🗄️</div>
                <h4>Databases</h4>
                <div class="tech-tags">
                    <span class="tech-tag">MySQL</span>
                    <span class="tech-tag">PostgreSQL</span>
                    <span class="tech-tag">SQL Server</span>
                </div>
            </div>
            <div class="tech-card reveal reveal-delay-3">
                <div class="tech-icon">🧠</div>
                <h4>AI & Data</h4>
                <div class="tech-tags">
                    <span class="tech-tag">Scikit-learn</span>
                    <span class="tech-tag">Pandas</span>
                    <span class="tech-tag">Graphviz</span>
                    <span class="tech-tag">NiFi</span>
                </div>
            </div>
            <div class="tech-card reveal reveal-delay-4">
                <div class="tech-icon">🛠️</div>
                <h4>Tooling</h4>
                <div class="tech-tags">
                    <span class="tech-tag">Git</span>
                    <span class="tech-tag">GitHub</span>
                    <span class="tech-tag">VS Code</span>
                    <span class="tech-tag">Postman</span>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="divider"></div>

<!-- ===================== PROJECTS ===================== -->
<section id="projects">
    <div class="section-inner">
        <div class="section-header">
            <span class="section-tag reveal">// portfolio</span>
            <h2 class="section-title reveal">🔭 Work That Matters</h2>
            <p class="section-desc reveal">Systems designed for real-world impact at scale</p>
        </div>

        <!-- Project 1 -->
        <div class="project-card reveal">
            <div class="project-meta">
                <span class="project-org">🏭 GCB</span>
                <span class="project-type">Master's Thesis</span>
            </div>
            <h3>AI-Powered Incident Management System</h3>
            <p>The most complex system I've built — and the one I'm most proud of. An end-to-end intelligent platform for <strong style="color:var(--purple-200)">industrial incident prevention, detection, and response</strong> — designed for real-world critical environments.</p>
            <div class="project-features">
                <div class="feature"><span class="feature-icon">📡</span> Real-time alert system — WebSocket-powered</div>
                <div class="feature"><span class="feature-icon">🤖</span> ML prediction engine — Scikit-learn models</div>
                <div class="feature"><span class="feature-icon">📊</span> Smart dashboards — React + Chart.js</div>
                <div class="feature"><span class="feature-icon">🔐</span> Role-based access — Secure API layer</div>
            </div>
            <div class="project-stack">
                <span class="stack-tag">Python</span>
                <span class="stack-tag">Flask</span>
                <span class="stack-tag">React</span>
                <span class="stack-tag">Scikit-learn</span>
                <span class="stack-tag">PostgreSQL</span>
                <span class="stack-tag">Chart.js</span>
            </div>
        </div>

        <!-- Project 2 -->
        <div class="project-card reveal">
            <div class="project-meta">
                <span class="project-org">📡 Djezzy</span>
                <span class="project-type">Bachelor's Thesis</span>
            </div>
            <h3>Big Data NPS Analytics Platform</h3>
            <p>Built for one of Algeria's largest telecom operators. A large-scale <strong style="color:var(--purple-200)">Big Data architecture</strong> to measure and visualize Net Promoter Score in near-real-time — helping a national operator understand its customers at scale.</p>
            <div class="project-features">
                <div class="feature"><span class="feature-icon">🔄</span> Apache NiFi pipeline — data ingestion</div>
                <div class="feature"><span class="feature-icon">📦</span> Data warehouse design — SQL Server</div>
                <div class="feature"><span class="feature-icon">📈</span> Analytics dashboards — Pandas + Chart.js</div>
                <div class="feature"><span class="feature-icon">💡</span> Customer insight layer — segmentation models</div>
            </div>
            <div class="project-stack">
                <span class="stack-tag">Apache NiFi</span>
                <span class="stack-tag">Python</span>
                <span class="stack-tag">Pandas</span>
                <span class="stack-tag">SQL Server</span>
                <span class="stack-tag">Chart.js</span>
            </div>
        </div>

        <!-- Experience Mini Cards -->
        <div class="exp-grid">
            <div class="exp-card reveal">
                <h4>🏛️ IT Infrastructure</h4>
                <div class="exp-org">Algeria Poste</div>
                <p>Network configuration, IT maintenance, payment systems & infrastructure support across a national financial institution.</p>
            </div>
            <div class="exp-card reveal reveal-delay-1">
                <h4>🎓 Educator</h4>
                <div class="exp-org">NG School</div>
                <p>Teaching Python, AI fundamentals, and IT basics to young learners. Running Canva design workshops and building interactive educational content.</p>
            </div>
        </div>
    </div>

</section>

<div class="divider"></div>

<!-- ===================== EDUCATION ===================== -->
<section id="education">
    <div class="section-inner">
        <div class="section-header">
            <span class="section-tag reveal">// academic path</span>
            <h2 class="section-title reveal">🎓 Education</h2>
        </div>

        <div class="edu-university reveal">
            <h3>USTHB — University of Science and Technology Houari Boumediene</h3>
            <p>Algiers, Algeria 🇩🇿</p>
        </div>

        <div class="edu-timeline">
            <div class="edu-card reveal">
                <div class="edu-icon">🎓</div>
                <h4>Master of Science</h4>
                <div class="edu-degree">Software Engineering</div>
                <div class="edu-date">Sept 2023 → June 2025 <span class="check">✅</span></div>
                <div class="edu-topics">
                    <span class="edu-topic">AI Systems</span>
                    <span class="edu-topic">Full-Stack</span>
                    <span class="edu-topic">Architecture</span>
                    <span class="edu-topic">Research</span>
                </div>
            </div>
            <div class="edu-card reveal reveal-delay-1">
                <div class="edu-icon">🎓</div>
                <h4>Bachelor of Science</h4>
                <div class="edu-degree">Computer Science</div>
                <div class="edu-date">Sept 2019 → June 2023 <span class="check">✅</span></div>
                <div class="edu-topics">
                    <span class="edu-topic">Algorithms</span>
                    <span class="edu-topic">Networks</span>
                    <span class="edu-topic">Databases</span>
                    <span class="edu-topic">OOP</span>
                </div>
            </div>
        </div>

        <!-- Certifications -->
        <div style="margin-top:4rem">
            <h3 style="font-family:'Space Grotesk',sans-serif;color:var(--purple-200);text-align:center;margin-bottom:1.5rem;font-size:1.2rem" class="reveal">🏅 Certifications</h3>
            <div class="cert-grid">
                <div class="cert-card reveal">
                    <div class="cert-icon">🌐</div>
                    <div class="cert-info">
                        <h4>CCNA 1 — Cisco Networking Academy</h4>
                        <p>Network fundamentals, IP, routing protocols</p>
                    </div>
                    <span class="cert-check">✅</span>
                </div>
                <div class="cert-card reveal reveal-delay-1">
                    <div class="cert-icon">🚑</div>
                    <div class="cert-info">
                        <h4>First Aid & Emergency Response</h4>
                        <p>Algerian Civil Protection — Emergency protocols</p>
                    </div>
                    <span class="cert-check">✅</span>
                </div>
            </div>
        </div>
    </div>

</section>

<div class="divider"></div>

<!-- ===================== GITHUB STATS ===================== -->
<section id="stats">
    <div class="section-inner">
        <div class="section-header">
            <span class="section-tag reveal">// metrics</span>
            <h2 class="section-title reveal">📊 GitHub Activity</h2>
        </div>
        <div class="stats-grid">
            <div class="reveal">
                <img src="https://github-readme-stats.vercel.app/api?username=HananShr&show_icons=true&theme=midnight-purple&include_all_commits=true&count_private=true&hide_border=true&bg_color=12101f&title_color=c77dff&icon_color=c77dff&text_color=e0aaff&ring_color=9d4edd" alt="GitHub Stats"/>
            </div>
            <div class="reveal reveal-delay-1">
                <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=HananShr&layout=compact&langs_count=8&theme=midnight-purple&hide_border=true&bg_color=12101f&title_color=c77dff&text_color=e0aaff" alt="Top Languages"/>
            </div>
            <div class="stats-full reveal reveal-delay-2">
                <img src="https://streak-stats.demolab.com?user=HananShr&theme=midnight-purple&hide_border=true&background=12101f&ring=c77dff&fire=e0aaff&currStreakLabel=c77dff&dates=9d4edd&stroke=12101f" alt="Streak Stats"/>
            </div>
            <div class="stats-full reveal reveal-delay-3">
                <img src="https://github-readme-activity-graph.vercel.app/graph?username=HananShr&bg_color=12101f&color=c77dff&line=9d4edd&point=e0aaff&area=true&hide_border=true&area_color=302b63" alt="Activity Graph"/>
            </div>
        </div>
    </div>
</section>

<div class="divider"></div>

<!-- ===================== CONTACT ===================== -->
<section id="contact" class="contact-section">
    <div class="section-inner contact-inner">
        <div class="section-header">
            <span class="section-tag reveal">// let's connect</span>
            <h2 class="section-title reveal">💬 Get In Touch</h2>
        </div>
        <p class="reveal">
            I'm actively looking for roles in <strong style="color:var(--purple-200)">software engineering</strong>, <strong style="color:var(--purple-200)">AI development</strong>, or <strong style="color:var(--purple-200)">full-stack</strong> — remote or Algeria-based.
            If you're building something impactful, I'd love to be part of it.
        </p>
        <div class="contact-btns reveal">
            <a href="mailto:hanane.sahraoui20@gmail.com" class="btn btn-primary">✉ Send an Email</a>
            <a href="https://www.linkedin.com/in/hanane-sahraoui" target="_blank" class="btn btn-secondary">💼 Connect on LinkedIn</a>
            <a href="https://github.com/HananShr" target="_blank" class="btn btn-secondary">🐙 Browse My Work</a>
        </div>
        <div class="contact-quote reveal">
            "The best engineers don't just solve problems — they reframe them."
        </div>
    </div>
</section>

<!-- Footer -->
<footer>
    <p>Crafted with 💜 by <a href="https://github.com/HananShr">Hanane Saharaoui</a> · Boumerdes, Algeria 🇩🇿</p>
</footer>

<script>
// ==================== PARTICLE SYSTEM ====================
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let particles = [];
let mouse = { x: 0, y: 0 };

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

class Particle {
    constructor() {
        this.reset();
    }
    reset() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.size = Math.random() * 2 + 0.5;
        this.speedX = (Math.random() - 0.5) * 0.5;
        this.speedY = (Math.random() - 0.5) * 0.5;
        this.opacity = Math.random() * 0.5 + 0.1;
        this.color = Math.random() > 0.5 ? '199,125,255' : '157,78,221';
    }
    update() {
        this.x += this.speedX;
        this.y += this.speedY;
        if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) {
            this.reset();
        }
        // Mouse interaction
        const dx = mouse.x - this.x;
        const dy = mouse.y - this.y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 120) {
            this.x -= dx * 0.01;
            this.y -= dy * 0.01;
            this.opacity = Math.min(0.8, this.opacity + 0.02);
        }
    }
    draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(${this.color},${this.opacity})`;
        ctx.fill();
    }
}

// Create particles
const particleCount = Math.min(80, Math.floor(window.innerWidth / 15));
for (let i = 0; i < particleCount; i++) {
    particles.push(new Particle());
}

function connectParticles() {
    for (let i = 0; i < particles.length; i++) {
        for (let j = i + 1; j < particles.length; j++) {
            const dx = particles[i].x - particles[j].x;
            const dy = particles[i].y - particles[j].y;
            const dist = Math.sqrt(dx * dx + dy * dy);
            if (dist < 150) {
                ctx.beginPath();
                ctx.moveTo(particles[i].x, particles[i].y);
                ctx.lineTo(particles[j].x, particles[j].y);
                ctx.strokeStyle = `rgba(157,78,221,${0.08 * (1 - dist / 150)})`;
                ctx.lineWidth = 0.5;
                ctx.stroke();
            }
        }
    }
}

function animateParticles() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => { p.update(); p.draw(); });
    connectParticles();
    requestAnimationFrame(animateParticles);
}
animateParticles();

// ==================== CURSOR GLOW ====================
const cursorGlow = document.getElementById('cursorGlow');
document.addEventListener('mousemove', (e) => {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
    cursorGlow.style.left = e.clientX + 'px';
    cursorGlow.style.top = e.clientY + 'px';
});

// ==================== TYPEWRITER ====================
const phrases = [
    '⚡ Building AI-powered systems that actually ship',
    '🧠 Where clean architecture meets machine intelligence',
    '🌍 From Algeria — building for the world',
    '💜 Code with purpose, ship with precision'
];
let phraseIndex = 0, charIndex = 0, isDeleting = false;
const typeEl = document.getElementById('typewriter');

function typewrite() {
    const current = phrases[phraseIndex];
    if (!isDeleting) {
        typeEl.textContent = current.substring(0, charIndex + 1);
        charIndex++;
        if (charIndex === current.length) {
            setTimeout(() => { isDeleting = true; typewrite(); }, 2000);
            return;
        }
        setTimeout(typewrite, 50);
    } else {
        typeEl.textContent = current.substring(0, charIndex - 1);
        charIndex--;
        if (charIndex === 0) {
            isDeleting = false;
            phraseIndex = (phraseIndex + 1) % phrases.length;
            setTimeout(typewrite, 500);
            return;
        }
        setTimeout(typewrite, 30);
    }
}
typewrite();

// ==================== SCROLL REVEAL ====================
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
reveals.forEach(el => observer.observe(el));

// ==================== NAV SCROLL ====================
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 50);
});

// ==================== MOBILE NAV ====================
const navToggle = document.getElementById('navToggle');
const navLinks = document.getElementById('navLinks');
navToggle.addEventListener('click', () => {
    navLinks.classList.toggle('open');
    navToggle.textContent = navLinks.classList.contains('open') ? '✕' : '☰';
});
navLinks.querySelectorAll('a').forEach(a => {
    a.addEventListener('click', () => {
        navLinks.classList.remove('open');
        navToggle.textContent = '☰';
    });
});

// ==================== COUNTER ANIMATION ====================
const counters = document.querySelectorAll('.stat-number');
const counterObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            const el = entry.target;
            const target = parseInt(el.dataset.count);
            let current = 0;
            const inc = target / 40;
            const timer = setInterval(() => {
                current += inc;
                if (current >= target) {
                    el.textContent = target + '+';
                    clearInterval(timer);
                } else {
                    el.textContent = Math.ceil(current);
                }
            }, 40);
            counterObserver.unobserve(el);
        }
    });
}, { threshold: 0.5 });
counters.forEach(c => counterObserver.observe(c));

// ==================== SMOOTH SCROLL ====================
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }
    });
});

// ==================== TECH CARD TILT ====================
document.querySelectorAll('.tech-card, .project-card, .edu-card').forEach(card => {
    card.addEventListener('mousemove', (e) => {
        const rect = card.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const centerX = rect.width / 2;
        const centerY = rect.height / 2;
        const rotateX = (y - centerY) / 20;
        const rotateY = (centerX - x) / 20;
        card.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateY(-5px)`;
    });
    card.addEventListener('mouseleave', () => {
        card.style.transform = '';
    });
});
</script>

</body>
</html>
