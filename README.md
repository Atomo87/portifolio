<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta name="author" content="Leandro Ramos">
<title>Leandro Ramos · Retro Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700;900&family=Rajdhani:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#0a0320;
  --purple:#b537f2;
  --pink:#ff2e97;
  --cyan:#00f5ff;
  --orange:#ff7b00;
  --yellow:#ffd60a;
  --text:#fff;
  --dim:rgba(255,255,255,.6);
}
html{scroll-behavior:smooth}
body{font-family:'Rajdhani',sans-serif;background:var(--bg);color:var(--text);overflow-x:hidden;line-height:1.6}
/* Synthwave bg */
.synth-bg{position:fixed;inset:0;z-index:0;overflow:hidden}
.synth-bg::before{content:'';position:absolute;inset:0;background:linear-gradient(180deg,#0a0320 0%,#1a0a3a 40%,#2d1155 70%,#0a0320 100%)}
.sun{position:absolute;bottom:0;left:50%;transform:translateX(-50%);width:600px;height:600px;background:linear-gradient(180deg,var(--yellow) 0%,var(--orange) 40%,var(--pink) 80%,transparent 100%);border-radius:50%;filter:blur(2px);opacity:.5;mask-image:repeating-linear-gradient(180deg,#000 0px,#000 4px,transparent 4px,transparent 12px)}
.grid-floor{position:absolute;bottom:0;left:-50%;right:-50%;height:50%;background-image:linear-gradient(var(--cyan) 1px,transparent 1px),linear-gradient(90deg,var(--cyan) 1px,transparent 1px);background-size:60px 60px;transform:perspective(400px) rotateX(70deg);transform-origin:bottom;opacity:.4;animation:gridScroll 3s linear infinite}
@keyframes gridScroll{0%{background-position:0 0}100%{background-position:0 60px}}
.stars{position:absolute;inset:0;background-image:radial-gradient(1px 1px at 20% 30%,#fff,transparent),radial-gradient(1px 1px at 80% 20%,#fff,transparent),radial-gradient(1px 1px at 40% 60%,#fff,transparent),radial-gradient(1px 1px at 70% 80%,#fff,transparent),radial-gradient(2px 2px at 10% 70%,#fff,transparent),radial-gradient(1px 1px at 90% 40%,#fff,transparent);animation:twinkle 3s ease-in-out infinite}
@keyframes twinkle{0%,100%{opacity:.6}50%{opacity:1}}
.container{max-width:1300px;margin:0 auto;padding:0 40px;position:relative;z-index:2}
/* Nav */
nav{position:fixed;top:20px;left:50%;transform:translateX(-50%);z-index:100;padding:16px 32px;background:rgba(10,3,32,.7);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);border:1px solid rgba(181,55,242,.4);border-radius:12px;display:flex;gap:32px;align-items:center;justify-content:space-between;width:calc(100% - 80px);max-width:1150px;box-shadow:0 0 40px rgba(181,55,242,.3)}
.brand{font-family:'Orbitron',sans-serif;font-weight:900;font-size:1.2rem;letter-spacing:.05em;background:linear-gradient(90deg,var(--cyan),var(--pink),var(--yellow));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;background-size:200% auto;animation:shine 3s linear infinite}
@keyframes shine{to{background-position:200% center}}
.nav-menu{display:flex;gap:30px;list-style:none}
.nav-menu a{color:var(--dim);text-decoration:none;font-size:.85rem;font-weight:500;letter-spacing:.15em;text-transform:uppercase;transition:all .3s;position:relative}
.nav-menu a:hover{color:var(--cyan);text-shadow:0 0 15px var(--cyan)}
.nav-btn{padding:11px 24px;background:linear-gradient(135deg,var(--pink),var(--purple));color:white;text-decoration:none;border-radius:8px;font-size:.8rem;font-weight:600;letter-spacing:.1em;text-transform:uppercase;transition:all .4s;box-shadow:0 0 25px rgba(255,46,151,.5)}
.nav-btn:hover{box-shadow:0 0 40px rgba(255,46,151,.9);transform:translateY(-2px)}
/* Hero */
.hero{min-height:100vh;display:flex;align-items:center;padding:140px 0 80px}
.hero-grid{display:grid;grid-template-columns:1.2fr 1fr;gap:60px;align-items:center;width:100%}
.hero-tag{display:inline-flex;align-items:center;gap:10px;padding:8px 18px;background:rgba(181,55,242,.15);border:1px solid var(--purple);border-radius:100px;font-size:.75rem;color:var(--cyan);margin-bottom:32px;letter-spacing:.15em;text-transform:uppercase;font-weight:500;box-shadow:0 0 20px rgba(181,55,242,.3)}
.hero-tag .dot{width:8px;height:8px;border-radius:50%;background:var(--cyan);box-shadow:0 0 12px var(--cyan);animation:pulse 1.5s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
.hero-title{font-family:'Orbitron',sans-serif;font-weight:900;font-size:clamp(2.8rem,7vw,6rem);line-height:.95;letter-spacing:-.02em;margin-bottom:32px;text-transform:uppercase}
.hero-title .line1{color:var(--text);text-shadow:0 0 20px rgba(255,255,255,.5)}
.hero-title .line2{background:linear-gradient(90deg,var(--cyan),var(--pink));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;filter:drop-shadow(0 0 20px var(--cyan))}
.hero-title .line3{color:var(--yellow);text-shadow:0 0 20px var(--yellow),0 0 40px var(--orange)}
.hero-desc{font-size:1.1rem;color:var(--dim);max-width:520px;margin-bottom:44px;font-weight:400;line-height:1.7;letter-spacing:.02em}
.hero-desc strong{color:var(--text);font-weight:600}
.hero-cta{display:flex;gap:14px;flex-wrap:wrap}
.btn{padding:16px 32px;border-radius:8px;text-decoration:none;font-size:.9rem;font-weight:600;letter-spacing:.1em;text-transform:uppercase;display:inline-flex;align-items:center;gap:10px;transition:all .4s cubic-bezier(.23,1,.32,1);cursor:pointer;border:1px solid;font-family:inherit}
.btn-primary{background:linear-gradient(135deg,var(--pink),var(--purple));color:white;border-color:var(--pink);box-shadow:0 0 25px rgba(255,46,151,.5)}
.btn-primary:hover{transform:translateY(-3px);box-shadow:0 0 50px rgba(255,46,151,.9)}
.btn-outline{background:transparent;color:var(--cyan);border-color:var(--cyan);box-shadow:inset 0 0 20px rgba(0,245,255,.1)}
.btn-outline:hover{background:var(--cyan);color:var(--bg);box-shadow:0 0 40px rgba(0,245,255,.9)}
/* Hero Card - Retro */
.hero-card{position:relative;padding:40px;background:linear-gradient(135deg,rgba(10,3,32,.9),rgba(45,17,85,.6));border:2px solid var(--pink);border-radius:16px;box-shadow:0 0 40px rgba(255,46,151,.4),inset 0 0 40px rgba(181,55,242,.1);backdrop-filter:blur(20px)}
.hero-card::before{content:'';position:absolute;top:-2px;left:-2px;right:-2px;height:6px;background:linear-gradient(90deg,var(--cyan),var(--pink),var(--yellow),var(--cyan));background-size:200% auto;animation:shine 3s linear infinite;border-radius:16px 16px 0 0}
.hc-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:28px}
.hc-avatar{width:80px;height:80px;border-radius:50%;background:linear-gradient(135deg,var(--pink),var(--purple));display:flex;align-items:center;justify-content:center;font-family:'Orbitron',sans-serif;font-size:1.8rem;font-weight:900;color:white;box-shadow:0 0 30px rgba(255,46,151,.6);border:2px solid var(--cyan)}
.hc-online{display:flex;align-items:center;gap:6px;padding:6px 14px;background:rgba(0,245,255,.1);border:1px solid var(--cyan);border-radius:100px;font-size:.7rem;color:var(--cyan);letter-spacing:.15em;text-transform:uppercase}
.hc-name{font-family:'Orbitron',sans-serif;font-size:1.8rem;font-weight:700;letter-spacing:-.02em;margin-bottom:6px;color:var(--text);text-shadow:0 0 15px rgba(255,255,255,.3)}
.hc-role{color:var(--cyan);font-size:.85rem;letter-spacing:.15em;text-transform:uppercase;margin-bottom:24px;font-weight:500}
.hc-stats{display:flex;justify-content:space-between;padding-top:24px;border-top:1px solid rgba(181,55,242,.3)}
.hc-stat-num{font-family:'Orbitron',sans-serif;font-size:1.5rem;font-weight:700;background:linear-gradient(135deg,var(--cyan),var(--pink));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent}
.hc-stat-lbl{font-size:.7rem;color:var(--dim);letter-spacing:.15em;text-transform:uppercase;margin-top:4px}
/* Sections */
section{padding:120px 0;position:relative;z-index:2}
.section-head{text-align:center;margin-bottom:80px}
.section-label{display:inline-block;padding:6px 18px;background:rgba(181,55,242,.15);border:1px solid var(--purple);border-radius:100px;font-size:.75rem;color:var(--cyan);letter-spacing:.2em;text-transform:uppercase;margin-bottom:20px;font-weight:500}
.section-title{font-family:'Orbitron',sans-serif;font-size:clamp(2rem,5.5vw,4rem);font-weight:700;letter-spacing:-.02em;line-height:1;text-transform:uppercase}
.section-title .grad{background:linear-gradient(90deg,var(--cyan),var(--pink),var(--yellow));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;background-size:200% auto;animation:shine 4s linear infinite}
/* Projects */
.projects{display:grid;grid-template-columns:repeat(auto-fit,minmax(340px,1fr));gap:24px}
.proj{position:relative;padding:32px;background:linear-gradient(135deg,rgba(10,3,32,.8),rgba(45,17,85,.4));border:1px solid rgba(181,55,242,.4);border-radius:12px;transition:all .5s cubic-bezier(.23,1,.32,1);min-height:360px;display:flex;flex-direction:column;overflow:hidden;backdrop-filter:blur(10px)}
.proj::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--cyan),var(--pink));transform:scaleX(0);transform-origin:left;transition:transform .5s}
.proj:hover::before{transform:scaleX(1)}
.proj:hover{transform:translateY(-8px);border-color:var(--pink);box-shadow:0 0 40px rgba(255,46,151,.4),0 30px 60px -20px rgba(0,0,0,.6)}
.proj-num{font-family:'Orbitron',sans-serif;font-size:.8rem;color:var(--cyan);letter-spacing:.15em;margin-bottom:20px;font-weight:500}
.proj-icon{font-size:2.4rem;margin-bottom:20px;filter:drop-shadow(0 0 15px var(--pink))}
.proj h3{font-family:'Orbitron',sans-serif;font-size:1.4rem;font-weight:700;margin-bottom:12px;letter-spacing:-.01em;text-transform:uppercase}
.proj p{color:var(--dim);font-size:.92rem;line-height:1.65;flex-grow:1;margin-bottom:24px}
.proj-tags{display:flex;gap:8px;flex-wrap:wrap;margin-top:auto}
.proj-tags span{padding:4px 12px;background:rgba(0,245,255,.08);border:1px solid rgba(0,245,255,.4);border-radius:100px;font-size:.7rem;color:var(--cyan);letter-spacing:.1em;text-transform:uppercase;font-weight:500}
/* CTA */
.retro-cta{padding:80px 40px;text-align:center;background:linear-gradient(135deg,rgba(10,3,32,.9),rgba(45,17,85,.6));border:2px solid var(--pink);border-radius:20px;position:relative;overflow:hidden;box-shadow:0 0 60px rgba(255,46,151,.3)}
.retro-cta::before{content:'';position:absolute;inset:0;background:radial-gradient(circle at 50% 100%,var(--pink),transparent 60%);opacity:.15;pointer-events:none}
.retro-cta-content{position:relative;z-index:2}
.retro-cta h2{font-family:'Orbitron',sans-serif;font-size:clamp(2rem,5vw,3.5rem);font-weight:900;text-transform:uppercase;letter-spacing:-.02em;line-height:1.05;margin-bottom:24px}
.retro-cta h2 .grad{background:linear-gradient(90deg,var(--cyan),var(--pink));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;filter:drop-shadow(0 0 20px var(--cyan))}
.retro-cta p{color:var(--dim);font-size:1.05rem;max-width:520px;margin:0 auto 44px;line-height:1.7}
.btn-whats{padding:22px 44px;border-radius:12px;background:linear-gradient(135deg,#25d366,#128c7e);color:white;text-decoration:none;font-size:1rem;font-weight:600;letter-spacing:.05em;display:inline-flex;align-items:center;gap:12px;transition:all .4s cubic-bezier(.23,1,.32,1);box-shadow:0 0 30px rgba(37,211,102,.5)}
.btn-whats:hover{transform:translateY(-4px) scale(1.02);box-shadow:0 0 60px rgba(37,211,102,.9)}
/* Footer */
footer{padding:60px 0 40px;border-top:1px solid rgba(181,55,242,.3);text-align:center;position:relative;z-index:2}
.footer-credit{color:var(--dim);font-size:.95rem;letter-spacing:.05em;margin-bottom:10px;font-weight:400}
.footer-credit strong{font-family:'Orbitron',sans-serif;background:linear-gradient(90deg,var(--cyan),var(--pink));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;font-weight:700;letter-spacing:0}
.footer-copy{color:var(--dim);font-size:.75rem;letter-spacing:.2em;text-transform:uppercase}
/* Whats */
.whats-float{position:fixed;bottom:28px;right:28px;z-index:999;text-decoration:none}
.whats-btn{width:64px;height:64px;border-radius:50%;background:linear-gradient(135deg,#25d366,#128c7e);display:flex;align-items:center;justify-content:center;box-shadow:0 0 30px rgba(37,211,102,.6),0 0 0 0 rgba(37,211,102,.6);position:relative;transition:transform .4s;animation:wpulse 2s infinite}
@keyframes wpulse{0%,100%{box-shadow:0 0 30px rgba(37,211,102,.6),0 0 0 0 rgba(37,211,102,.6)}70%{box-shadow:0 0 30px rgba(37,211,102,.6),0 0 0 22px rgba(37,211,102,0)}}
.whats-btn:hover{transform:scale(1.1)}
.whats-btn svg{width:30px;height:30px;fill:white}
.reveal{opacity:0;transform:translateY(40px);transition:all .9s cubic-bezier(.23,1,.32,1)}
.reveal.active{opacity:1;transform:translateY(0)}
@media(max-width:900px){
  .container{padding:0 20px}
  .hero-grid{grid-template-columns:1fr;gap:60px}
  .nav-menu{display:none}
  nav{width:calc(100% - 40px);padding:12px 20px}
  section{padding:80px 0}
  .retro-cta{padding:60px 24px}
  .sun{width:400px;height:400px}
}
</style>
</head>
<body>
<div class="synth-bg">
  <div class="stars"></div>
  <div class="sun"></div>
  <div class="grid-floor"></div>
</div>

<nav>
  <div class="brand">◢ LEANDRO RAMOS ◣</div>
  <ul class="nav-menu">
    <li><a href="#home">Home</a></li>
    <li><a href="#work">Work</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="https://wa.me/5511999999999" class="nav-btn" target="_blank">Connect</a>
</nav>

<div class="container">
  <section class="hero" id="home">
    <div class="hero-grid">
      <div>
        <div class="hero-tag reveal"><span class="dot"></span>System Online · 2025</div>
        <h1 class="hero-title reveal">
          <span class="line1">Digital</span><br>
          <span class="line2">Dreams</span><br>
          <span class="line3">& Code.</span>
        </h1>
        <p class="hero-desc reveal">
          Sou <strong>Leandro Ramos</strong> — designer e desenvolvedor criando 
          <strong>experiências digitais com alma retrô</strong> e tecnologia de ponta. 
          Design que viaja no tempo, do passado ao futuro.
        </p>
        <div class="hero-cta reveal">
          <a href="#work" class="btn btn-primary">Ver Projetos →</a>
          <a href="https://wa.me/5511999999999" class="btn btn-outline" target="_blank">Contato</a>
        </div>
      </div>
      <div class="reveal">
        <div class="hero-card">
          <div class="hc-header">
            <div class="hc-avatar">LR</div>
            <div class="hc-online"><span class="dot" style="width:6px;height:6px;background:var(--cyan);border-radius:50%;box-shadow:0 0 10px var(--cyan);"></span>Online</div>
          </div>
          <div class="hc-name">Leandro Ramos</div>
          <div class="hc-role">Creative Developer</div>
          <div class="hc-stats">
            <div><div class="hc-stat-num">48+</div><div class="hc-stat-lbl">Projects</div></div>
            <div><div class="hc-stat-num">07</div><div class="hc-stat-lbl">Years</div></div>
            <div><div class="hc-stat-num">32</div><div class="hc-stat-lbl">Clients</div></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section id="work">
    <div class="section-head">
      <div class="section-label reveal">// Portfolio</div>
      <h2 class="section-title reveal">Featured <span class="grad">Work</span></h2>
    </div>
    <div class="projects">
      <div class="proj reveal">
        <div class="proj-num">01 / PROJECT</div>
        <div class="proj-icon">🕹️</div>
        <h3>Neon Runner</h3>
        <p>Jogo interativo em 3D com estética synthwave e trilha sonora retrô original.</p>
        <div class="proj-tags"><span>Three.js</span><span>WebAudio</span></div>
      </div>
      <div class="proj reveal">
        <div class="proj-num">02 / PROJECT</div>
        <div class="proj-icon">📼</div>
        <h3>VHS Store</h3>
        <p>E-commerce nostálgico com animações de fita cassete e efeitos analógicos.</p>
        <div class="proj-tags"><span>React</span><span>GSAP</span></div>
      </div>
      <div class="proj reveal">
        <div class="proj-num">03 / PROJECT</div>
        <div class="proj-icon">🌆</div>
        <h3>Miami Nights</h3>
        <p>Portfólio visual com paisagens neon geradas proceduralmente em WebGL.</p>
        <div class="proj-tags"><span>WebGL</span><span>GLSL</span></div>
      </div>
      <div class="proj reveal">
        <div class="proj-num">04 / PROJECT</div>
        <div class="proj-icon">🎸</div>
        <h3>Synthwave FM</h3>
        <p>Rádio online com visualizador 3D de áudio e interface inspirada nos anos 80.</p>
        <div class="proj-tags"><span>Canvas</span><span>Audio API</span></div>
      </div>
    </div>
  </section>

  <section id="contact">
    <div class="retro-cta reveal">
      <div class="retro-cta-content">
        <h2>Let's build the <span class="grad">future</span></h2>
        <p>Transforme sua ideia em uma experiência digital inesquecível. Estou pronto para o próximo desafio.</p>
        <a href="https://wa.me/5511999999999?text=Olá%20Leandro!" target="_blank" class="btn-whats">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
          </svg>
          Conversar no WhatsApp
        </a>
      </div>
    </div>
  </section>

  <footer>
    <div class="footer-credit">Desenvolvido por <strong>Leandro Ramos</strong></div>
    <div class="footer-copy">© 2025 · All rights reserved</div>
  </footer>
</div>

<a href="https://wa.me/5511999999999" target="_blank" class="whats-float">
  <div class="whats-btn">
    <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
  </div>
</a>

<script>
const obs=new IntersectionObserver(e=>{e.forEach((x,i)=>{if(x.isIntersecting){setTimeout(()=>x.target.classList.add('active'),i*100);obs.unobserve(x.target)}})},{threshold:.15});
document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));
document.querySelectorAll('a[href^="#"]').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();const t=document.querySelector(a.getAttribute('href'));if(t)t.scrollIntoView({behavior:'smooth'})}));
console.log('%c RETRO PORTFOLIO %c Leandro Ramos ','background:linear-gradient(135deg,#00f5ff,#ff2e97,#ffd60a);color:white;padding:8px 16px;border-radius:8px 0 0 8px;font-weight:900;font-family:monospace;','background:#0a0320;color:#00f5ff;padding:8px 16px;border-radius:0 8px 8px 0;font-weight:700;font-family:monospace;');
</script>
</body>
</html>
