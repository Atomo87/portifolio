<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="author" content="Leandro Ramos">
  <meta name="description" content="Portfólio 3D moderno desenvolvido por Leandro Ramos">
  <title>Leandro Ramos · Portfólio 3D</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* ========= RESET & VARIÁVEIS ========= */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    :root {
      --bg-0: #03030a;
      --bg-1: #0a0a18;
      --bg-2: #12122a;
      --primary: #7c5cff;
      --primary-2: #a78bfa;
      --secondary: #00e5ff;
      --accent: #ff3d71;
      --green: #25d366;
      --green-dark: #128c7e;
      --text: #f5f5ff;
      --text-dim: #8b8bb0;
      --glass: rgba(255, 255, 255, 0.03);
      --glass-border: rgba(255, 255, 255, 0.08);
      --glow-primary: 0 0 40px rgba(124, 92, 255, 0.5);
      --glow-secondary: 0 0 40px rgba(0, 229, 255, 0.4);
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Inter', sans-serif;
      background: var(--bg-0);
      color: var(--text);
      overflow-x: hidden;
      line-height: 1.5;
      cursor: none;
    }

    /* ========= CURSOR CUSTOMIZADO ========= */
    .cursor-dot {
      position: fixed;
      width: 8px;
      height: 8px;
      background: var(--secondary);
      border-radius: 50%;
      pointer-events: none;
      z-index: 99999;
      transform: translate(-50%, -50%);
      transition: width 0.2s, height 0.2s, background 0.2s;
      mix-blend-mode: difference;
    }

    .cursor-ring {
      position: fixed;
      width: 40px;
      height: 40px;
      border: 1.5px solid rgba(124, 92, 255, 0.6);
      border-radius: 50%;
      pointer-events: none;
      z-index: 99998;
      transform: translate(-50%, -50%);
      transition: width 0.3s, height 0.3s, border-color 0.3s, background 0.3s;
      backdrop-filter: blur(2px);
    }

    .cursor-ring.hover {
      width: 70px;
      height: 70px;
      background: rgba(124, 92, 255, 0.15);
      border-color: var(--secondary);
    }

    .cursor-dot.hover {
      width: 12px;
      height: 12px;
      background: var(--primary);
    }

    @media (max-width: 768px) {
      body { cursor: auto; }
      .cursor-dot, .cursor-ring { display: none; }
    }

    /* ========= LOADER ========= */
    .loader {
      position: fixed;
      inset: 0;
      background: var(--bg-0);
      z-index: 100000;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 30px;
      transition: opacity 0.8s ease, visibility 0.8s;
    }

    .loader.hidden {
      opacity: 0;
      visibility: hidden;
    }

    .loader-logo {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 2.5rem;
      font-weight: 700;
      letter-spacing: -0.03em;
      background: linear-gradient(135deg, #fff, var(--primary-2), var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      animation: pulse 1.5s ease-in-out infinite;
    }

    .loader-author {
      font-size: 0.85rem;
      color: var(--text-dim);
      letter-spacing: 0.3em;
      text-transform: uppercase;
      font-weight: 400;
      margin-top: -15px;
    }

    .loader-author span {
      color: var(--primary-2);
      font-weight: 600;
    }

    .loader-bar {
      width: 200px;
      height: 2px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 100px;
      overflow: hidden;
    }

    .loader-bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      animation: loadBar 1.8s ease-in-out forwards;
    }

    @keyframes loadBar {
      0% { width: 0%; }
      100% { width: 100%; }
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.6; }
    }

    /* ========= FUNDO ANIMADO ========= */
    .bg-container {
      position: fixed;
      inset: 0;
      z-index: 0;
      overflow: hidden;
      pointer-events: none;
    }

    .bg-gradient {
      position: absolute;
      inset: 0;
      background: 
        radial-gradient(circle at 15% 20%, rgba(124, 92, 255, 0.18) 0%, transparent 45%),
        radial-gradient(circle at 85% 75%, rgba(0, 229, 255, 0.12) 0%, transparent 50%),
        radial-gradient(circle at 50% 50%, rgba(255, 61, 113, 0.06) 0%, transparent 60%);
      animation: gradientShift 15s ease-in-out infinite;
    }

    @keyframes gradientShift {
      0%, 100% { transform: scale(1) rotate(0deg); }
      50% { transform: scale(1.1) rotate(5deg); }
    }

    .bg-grid {
      position: absolute;
      inset: -50%;
      background-image: 
        linear-gradient(rgba(124, 92, 255, 0.06) 1px, transparent 1px),
        linear-gradient(90deg, rgba(124, 92, 255, 0.06) 1px, transparent 1px);
      background-size: 60px 60px;
      transform: perspective(600px) rotateX(60deg) translateZ(-200px);
      transform-origin: center;
      animation: gridMove 20s linear infinite;
      mask-image: radial-gradient(ellipse at center, black 20%, transparent 70%);
      -webkit-mask-image: radial-gradient(ellipse at center, black 20%, transparent 70%);
    }

    @keyframes gridMove {
      0% { background-position: 0 0; }
      100% { background-position: 60px 60px; }
    }

    .particles {
      position: absolute;
      inset: 0;
    }

    .particle {
      position: absolute;
      border-radius: 50%;
      opacity: 0.6;
      animation: floatParticle linear infinite;
    }

    @keyframes floatParticle {
      0% {
        transform: translateY(100vh) translateX(0) scale(0);
        opacity: 0;
      }
      10% { opacity: 0.6; }
      90% { opacity: 0.6; }
      100% {
        transform: translateY(-100px) translateX(50px) scale(1);
        opacity: 0;
      }
    }

    /* ========= CONTAINER ========= */
    .container {
      max-width: 1400px;
      margin: 0 auto;
      padding: 0 32px;
      position: relative;
      z-index: 2;
    }

    /* ========= NAVBAR ========= */
    .navbar {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      width: calc(100% - 64px);
      max-width: 1300px;
      padding: 16px 32px;
      background: rgba(10, 10, 24, 0.6);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid var(--glass-border);
      border-radius: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 1000;
      transition: all 0.4s ease;
    }

    .navbar.scrolled {
      padding: 12px 32px;
      background: rgba(10, 10, 24, 0.85);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4), var(--glow-primary);
    }

    .logo {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.5rem;
      font-weight: 700;
      letter-spacing: -0.03em;
      background: linear-gradient(135deg, #fff, var(--primary-2));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      display: flex;
      align-items: center;
      gap: 8px;
      text-decoration: none;
    }

    .logo-dot {
      width: 8px;
      height: 8px;
      background: var(--secondary);
      border-radius: 50%;
      box-shadow: 0 0 12px var(--secondary);
      animation: pulse 2s ease-in-out infinite;
    }

    .nav-links {
      display: flex;
      gap: 36px;
      list-style: none;
    }

    .nav-links a {
      color: var(--text-dim);
      text-decoration: none;
      font-size: 0.9rem;
      font-weight: 500;
      letter-spacing: 0.02em;
      position: relative;
      padding: 6px 0;
      transition: color 0.3s;
    }

    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 1.5px;
      background: linear-gradient(90deg, var(--primary), var(--secondary));
      transition: width 0.4s cubic-bezier(0.23, 1, 0.32, 1);
    }

    .nav-links a:hover { color: var(--text); }
    .nav-links a:hover::after { width: 100%; }

    .nav-cta {
      padding: 10px 22px;
      background: linear-gradient(135deg, var(--primary), var(--primary-2));
      border-radius: 12px;
      color: white;
      text-decoration: none;
      font-weight: 600;
      font-size: 0.85rem;
      letter-spacing: 0.02em;
      transition: all 0.3s cubic-bezier(0.23, 1, 0.32, 1);
      box-shadow: 0 10px 25px -10px rgba(124, 92, 255, 0.6);
      position: relative;
      overflow: hidden;
    }

    .nav-cta::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, var(--secondary), var(--primary));
      opacity: 0;
      transition: opacity 0.3s;
    }

    .nav-cta span { position: relative; z-index: 1; }

    .nav-cta:hover {
      transform: translateY(-2px);
      box-shadow: 0 15px 35px -10px rgba(124, 92, 255, 0.8);
    }

    .nav-cta:hover::before { opacity: 1; }

    /* ========= HERO ========= */
    .hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      padding: 140px 0 80px;
      position: relative;
      perspective: 1500px;
    }

    .hero-grid {
      display: grid;
      grid-template-columns: 1.1fr 1fr;
      gap: 80px;
      align-items: center;
      width: 100%;
    }

    .hero-left { transform-style: preserve-3d; }

    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      background: rgba(124, 92, 255, 0.1);
      border: 1px solid rgba(124, 92, 255, 0.3);
      padding: 8px 18px;
      border-radius: 100px;
      font-size: 0.8rem;
      font-weight: 500;
      letter-spacing: 0.08em;
      color: var(--primary-2);
      margin-bottom: 32px;
      backdrop-filter: blur(10px);
      text-transform: uppercase;
    }

    .status-dot {
      width: 8px;
      height: 8px;
      background: var(--green);
      border-radius: 50%;
      box-shadow: 0 0 10px var(--green);
      animation: pulse 2s ease-in-out infinite;
    }

    .hero-title {
      font-family: 'Space Grotesk', sans-serif;
      font-size: clamp(2.8rem, 6vw, 5rem);
      font-weight: 700;
      line-height: 1.02;
      letter-spacing: -0.04em;
      margin-bottom: 28px;
    }

    .hero-title .line { display: block; overflow: hidden; }

    .hero-title .gradient {
      background: linear-gradient(135deg, var(--primary-2) 0%, var(--secondary) 50%, var(--accent) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      background-size: 200% 200%;
      animation: gradientText 5s ease infinite;
    }

    @keyframes gradientText {
      0%, 100% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
    }

    .hero-desc {
      font-size: 1.1rem;
      color: var(--text-dim);
      margin-bottom: 40px;
      max-width: 520px;
      line-height: 1.7;
      font-weight: 300;
    }

    .hero-desc strong { color: var(--text); font-weight: 500; }

    .hero-cta {
      display: flex;
      gap: 16px;
      flex-wrap: wrap;
      margin-bottom: 48px;
    }

    .btn {
      padding: 16px 32px;
      border-radius: 14px;
      font-weight: 600;
      text-decoration: none;
      font-size: 0.95rem;
      transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      cursor: none;
      border: none;
      font-family: 'Inter', sans-serif;
      letter-spacing: 0.01em;
      position: relative;
      overflow: hidden;
    }

    .btn-primary {
      background: linear-gradient(135deg, var(--primary), var(--primary-2));
      color: white;
      box-shadow: 0 15px 35px -10px rgba(124, 92, 255, 0.6);
    }

    .btn-primary::before {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, var(--secondary), var(--primary));
      opacity: 0;
      transition: opacity 0.4s;
    }

    .btn-primary span {
      position: relative;
      z-index: 1;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .btn-primary:hover {
      transform: translateY(-3px);
      box-shadow: 0 25px 45px -10px rgba(124, 92, 255, 0.9);
    }

    .btn-primary:hover::before { opacity: 1; }

    .btn-outline {
      background: rgba(255, 255, 255, 0.02);
      color: var(--text);
      border: 1px solid var(--glass-border);
      backdrop-filter: blur(10px);
    }

    .btn-outline:hover {
      background: rgba(255, 255, 255, 0.06);
      border-color: var(--secondary);
      transform: translateY(-3px);
      box-shadow: 0 15px 30px -10px rgba(0, 229, 255, 0.3);
    }

    .hero-stats {
      display: flex;
      gap: 40px;
    }

    .stat { display: flex; flex-direction: column; }

    .stat-num {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.8rem;
      font-weight: 700;
      background: linear-gradient(135deg, #fff, var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .stat-label {
      font-size: 0.8rem;
      color: var(--text-dim);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      margin-top: 4px;
    }

    /* ========= CARD 3D HERO ========= */
    .hero-right {
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      perspective: 1500px;
      transform-style: preserve-3d;
    }

    .card-wrapper {
      position: relative;
      transform-style: preserve-3d;
      transition: transform 0.15s ease-out;
    }

    .card-3d {
      width: 380px;
      height: 500px;
      background: linear-gradient(135deg, rgba(20, 20, 45, 0.9), rgba(10, 10, 24, 0.7));
      backdrop-filter: blur(30px);
      border-radius: 32px;
      border: 1px solid var(--glass-border);
      padding: 36px;
      display: flex;
      flex-direction: column;
      position: relative;
      overflow: hidden;
      box-shadow: 
        0 40px 80px -20px rgba(0, 0, 0, 0.8),
        0 0 0 1px rgba(255, 255, 255, 0.05) inset,
        0 0 80px rgba(124, 92, 255, 0.15);
      transform-style: preserve-3d;
    }

    .card-3d::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: conic-gradient(from 0deg, transparent, rgba(124, 92, 255, 0.1), transparent 30%);
      animation: rotate 8s linear infinite;
      pointer-events: none;
    }

    @keyframes rotate {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .card-content {
      position: relative;
      z-index: 2;
      display: flex;
      flex-direction: column;
      height: 100%;
      transform-style: preserve-3d;
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 30px;
      transform: translateZ(40px);
    }

    .avatar {
      width: 90px;
      height: 90px;
      border-radius: 24px;
      background: linear-gradient(135deg, var(--primary), var(--secondary));
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Space Grotesk', sans-serif;
      font-size: 2.4rem;
      font-weight: 700;
      color: white;
      box-shadow: 0 15px 30px -5px rgba(124, 92, 255, 0.6);
      border: 2px solid rgba(255, 255, 255, 0.15);
    }

    .card-status {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 6px 14px;
      background: rgba(37, 211, 102, 0.1);
      border: 1px solid rgba(37, 211, 102, 0.3);
      border-radius: 100px;
      font-size: 0.7rem;
      color: var(--green);
      font-weight: 600;
      letter-spacing: 0.05em;
      text-transform: uppercase;
    }

    .card-name {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.9rem;
      font-weight: 700;
      margin-bottom: 6px;
      letter-spacing: -0.02em;
      transform: translateZ(35px);
    }

    .card-role {
      color: var(--secondary);
      font-weight: 500;
      letter-spacing: 0.1em;
      font-size: 0.8rem;
      text-transform: uppercase;
      margin-bottom: 30px;
      transform: translateZ(30px);
    }

    .card-divider {
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
      margin-bottom: 24px;
      transform: translateZ(25px);
    }

    .card-skills {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-bottom: 24px;
      transform: translateZ(20px);
    }

    .skill-tag {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.08);
      padding: 6px 14px;
      border-radius: 100px;
      font-size: 0.75rem;
      color: var(--text-dim);
      transition: all 0.3s;
    }

    .skill-tag:hover {
      border-color: var(--primary);
      color: var(--primary-2);
      transform: translateY(-2px);
    }

    .card-footer {
      margin-top: auto;
      display: flex;
      justify-content: space-between;
      transform: translateZ(15px);
      padding-top: 20px;
      border-top: 1px solid rgba(255, 255, 255, 0.06);
    }

    .card-stat-num {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.4rem;
      font-weight: 700;
      background: linear-gradient(135deg, #fff, var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .card-stat-label {
      font-size: 0.65rem;
      color: var(--text-dim);
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    .card-glow {
      position: absolute;
      bottom: -60px;
      left: 50%;
      transform: translateX(-50%);
      width: 300px;
      height: 100px;
      background: radial-gradient(ellipse, rgba(124, 92, 255, 0.5), transparent 70%);
      filter: blur(30px);
      z-index: -1;
      animation: pulse 4s ease-in-out infinite;
    }

    /* ========= SEÇÕES ========= */
    section {
      padding: 120px 0;
      position: relative;
    }

    .section-header {
      text-align: center;
      margin-bottom: 80px;
    }

    .section-tag {
      display: inline-block;
      font-size: 0.8rem;
      font-weight: 600;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--primary-2);
      margin-bottom: 16px;
      padding: 6px 18px;
      background: rgba(124, 92, 255, 0.1);
      border-radius: 100px;
      border: 1px solid rgba(124, 92, 255, 0.2);
    }

    .section-title {
      font-family: 'Space Grotesk', sans-serif;
      font-size: clamp(2rem, 4.5vw, 3.5rem);
      font-weight: 700;
      letter-spacing: -0.03em;
      margin-bottom: 16px;
      line-height: 1.1;
    }

    .section-title .gradient {
      background: linear-gradient(135deg, var(--primary-2), var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .section-sub {
      color: var(--text-dim);
      font-size: 1.05rem;
      max-width: 620px;
      margin: 0 auto;
      font-weight: 300;
    }

    /* ========= PROJETOS ========= */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
      gap: 28px;
      perspective: 2000px;
    }

    .project-card {
      background: linear-gradient(135deg, rgba(20, 20, 45, 0.7), rgba(10, 10, 24, 0.5));
      backdrop-filter: blur(20px);
      border-radius: 24px;
      border: 1px solid var(--glass-border);
      padding: 32px;
      position: relative;
      overflow: hidden;
      transition: all 0.5s cubic-bezier(0.23, 1, 0.32, 1);
      transform-style: preserve-3d;
      min-height: 380px;
      display: flex;
      flex-direction: column;
      cursor: none;
    }

    .project-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at var(--mx, 50%) var(--my, 50%), rgba(124, 92, 255, 0.15), transparent 50%);
      opacity: 0;
      transition: opacity 0.5s;
      pointer-events: none;
    }

    .project-card:hover::before { opacity: 1; }

    .project-card:hover {
      border-color: rgba(124, 92, 255, 0.4);
      box-shadow: 
        0 40px 60px -20px rgba(0, 0, 0, 0.8),
        0 0 60px -10px rgba(124, 92, 255, 0.3);
      transform: translateY(-8px);
    }

    .project-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 24px;
    }

    .project-icon {
      width: 64px;
      height: 64px;
      border-radius: 18px;
      background: linear-gradient(135deg, rgba(124, 92, 255, 0.25), rgba(0, 229, 255, 0.15));
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.8rem;
      border: 1px solid rgba(255, 255, 255, 0.1);
      box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.4);
    }

    .project-year {
      font-size: 0.75rem;
      color: var(--text-dim);
      font-weight: 500;
      letter-spacing: 0.05em;
      padding: 4px 12px;
      background: rgba(255, 255, 255, 0.03);
      border-radius: 100px;
      border: 1px solid rgba(255, 255, 255, 0.06);
    }

    .project-title {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 1.5rem;
      font-weight: 700;
      margin-bottom: 12px;
      letter-spacing: -0.02em;
    }

    .project-desc {
      color: var(--text-dim);
      font-size: 0.92rem;
      line-height: 1.65;
      margin-bottom: 24px;
      flex-grow: 1;
      font-weight: 300;
    }

    .project-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: auto;
    }

    .project-tag {
      background: rgba(255, 255, 255, 0.03);
      padding: 5px 12px;
      border-radius: 100px;
      font-size: 0.7rem;
      color: var(--text-dim);
      border: 1px solid rgba(255, 255, 255, 0.06);
      font-weight: 500;
      letter-spacing: 0.02em;
    }

    .project-arrow {
      position: absolute;
      bottom: 32px;
      right: 32px;
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: rgba(124, 92, 255, 0.15);
      border: 1px solid rgba(124, 92, 255, 0.3);
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--primary-2);
      transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      transform: translate(-4px, 4px);
      opacity: 0;
    }

    .project-card:hover .project-arrow {
      opacity: 1;
      transform: translate(0, 0);
      background: var(--primary);
      color: white;
    }

    /* ========= CTA WHATSAPP SECTION ========= */
    .cta-section { padding: 100px 0; }

    .cta-box {
      background: linear-gradient(135deg, rgba(20, 20, 45, 0.8), rgba(10, 10, 24, 0.6));
      backdrop-filter: blur(30px);
      border-radius: 40px;
      border: 1px solid var(--glass-border);
      padding: 80px 60px;
      text-align: center;
      position: relative;
      overflow: hidden;
      box-shadow: 0 40px 80px -30px rgba(0, 0, 0, 0.8);
    }

    .cta-box::before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: conic-gradient(from 0deg, transparent, rgba(37, 211, 102, 0.08), transparent 30%);
      animation: rotate 12s linear infinite;
      pointer-events: none;
    }

    .cta-content { position: relative; z-index: 2; }

    .cta-title {
      font-family: 'Space Grotesk', sans-serif;
      font-size: clamp(2rem, 4vw, 3rem);
      font-weight: 700;
      letter-spacing: -0.03em;
      margin-bottom: 20px;
      line-height: 1.15;
    }

    .cta-title .gradient {
      background: linear-gradient(135deg, var(--green), var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .cta-desc {
      color: var(--text-dim);
      font-size: 1.05rem;
      max-width: 540px;
      margin: 0 auto 40px;
      font-weight: 300;
    }

    /* ========= BOTÃO WHATSAPP FLUTUANTE ========= */
    .whatsapp-float {
      position: fixed;
      bottom: 32px;
      right: 32px;
      z-index: 9999;
      display: flex;
      align-items: center;
      gap: 12px;
      text-decoration: none;
      cursor: none;
    }

    .whatsapp-btn {
      width: 64px;
      height: 64px;
      background: linear-gradient(135deg, var(--green), var(--green-dark));
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 
        0 10px 30px -5px rgba(37, 211, 102, 0.5),
        0 0 0 0 rgba(37, 211, 102, 0.6);
      position: relative;
      transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      animation: whatsappPulse 2.5s ease-in-out infinite;
    }

    @keyframes whatsappPulse {
      0% {
        box-shadow: 
          0 10px 30px -5px rgba(37, 211, 102, 0.5),
          0 0 0 0 rgba(37, 211, 102, 0.6);
      }
      70% {
        box-shadow: 
          0 10px 30px -5px rgba(37, 211, 102, 0.5),
          0 0 0 20px rgba(37, 211, 102, 0);
      }
      100% {
        box-shadow: 
          0 10px 30px -5px rgba(37, 211, 102, 0.5),
          0 0 0 0 rgba(37, 211, 102, 0);
      }
    }

    .whatsapp-btn svg {
      width: 32px;
      height: 32px;
      fill: white;
      transition: transform 0.4s;
    }

    .whatsapp-btn:hover {
      transform: scale(1.1) rotate(8deg);
      box-shadow: 0 15px 40px -5px rgba(37, 211, 102, 0.7);
    }

    .whatsapp-btn:hover svg { transform: scale(1.1); }

    .whatsapp-tooltip {
      background: rgba(10, 10, 24, 0.95);
      backdrop-filter: blur(20px);
      border: 1px solid rgba(37, 211, 102, 0.3);
      padding: 12px 18px;
      border-radius: 14px;
      color: white;
      font-size: 0.85rem;
      font-weight: 500;
      white-space: nowrap;
      opacity: 0;
      transform: translateX(20px);
      transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
      pointer-events: none;
      position: relative;
      box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.6);
    }

    .whatsapp-tooltip::after {
      content: '';
      position: absolute;
      right: -6px;
      top: 50%;
      transform: translateY(-50%) rotate(45deg);
      width: 12px;
      height: 12px;
      background: rgba(10, 10, 24, 0.95);
      border-right: 1px solid rgba(37, 211, 102, 0.3);
      border-top: 1px solid rgba(37, 211, 102, 0.3);
    }

    .whatsapp-tooltip small {
      display: block;
      color: var(--text-dim);
      font-size: 0.7rem;
      margin-top: 2px;
      font-weight: 400;
    }

    .whatsapp-float:hover .whatsapp-tooltip {
      opacity: 1;
      transform: translateX(0);
    }

    .whatsapp-badge {
      position: absolute;
      top: -4px;
      right: -4px;
      width: 20px;
      height: 20px;
      background: var(--accent);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.7rem;
      font-weight: 700;
      color: white;
      border: 2px solid var(--bg-0);
      animation: pulse 2s ease-in-out infinite;
    }

    /* ========= FOOTER ========= */
    footer {
      padding: 60px 0 40px;
      border-top: 1px solid rgba(255, 255, 255, 0.05);
      position: relative;
      z-index: 2;
    }

    .footer-content {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 24px;
    }

    .footer-brand {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .footer-copy {
      color: var(--text-dim);
      font-size: 0.88rem;
      font-weight: 300;
    }

    .footer-credit {
      font-family: 'Space Grotesk', sans-serif;
      font-size: 0.95rem;
      font-weight: 500;
      color: var(--text-dim);
      display: flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .footer-credit strong {
      background: linear-gradient(135deg, var(--primary-2), var(--secondary));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      font-weight: 700;
      font-size: 1.05rem;
      letter-spacing: -0.01em;
    }

    .footer-credit .heart {
      color: var(--accent);
      animation: pulse 1.5s ease-in-out infinite;
      display: inline-block;
    }

    .footer-social {
      display: flex;
      gap: 12px;
    }

    .social-link {
      width: 44px;
      height: 44px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 12px;
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid var(--glass-border);
      color: var(--text-dim);
      text-decoration: none;
      transition: all 0.3s;
      cursor: none;
    }

    .social-link:hover {
      background: rgba(124, 92, 255, 0.15);
      border-color: var(--primary);
      color: var(--primary-2);
      transform: translateY(-4px);
    }

    .social-link svg {
      width: 20px;
      height: 20px;
      fill: currentColor;
    }

    /* ========= SCROLL REVEAL ========= */
    .reveal {
      opacity: 0;
      transform: translateY(40px);
      transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.23, 1, 0.32, 1);
    }

    .reveal.active {
      opacity: 1;
      transform: translateY(0);
    }

    /* ========= RESPONSIVO ========= */
    @media (max-width: 1024px) {
      .hero-grid {
        grid-template-columns: 1fr;
        gap: 60px;
        text-align: center;
      }

      .hero-left {
        display: flex;
        flex-direction: column;
        align-items: center;
      }

      .hero-desc { max-width: 100%; }
      .hero-cta { justify-content: center; }
      .hero-stats { justify-content: center; }

      .card-3d {
        width: 340px;
        height: 460px;
        padding: 30px;
      }

      .nav-links { display: none; }
    }

    @media (max-width: 768px) {
      .container { padding: 0 20px; }

      .navbar {
        width: calc(100% - 32px);
        padding: 14px 20px;
      }

      .hero { padding: 120px 0 60px; }
      .hero-stats { gap: 24px; }
      .stat-num { font-size: 1.4rem; }
      .section-header { margin-bottom: 50px; }
      section { padding: 80px 0; }

      .cta-box {
        padding: 60px 30px;
        border-radius: 28px;
      }

      .whatsapp-float {
        bottom: 20px;
        right: 20px;
      }

      .whatsapp-btn {
        width: 56px;
        height: 56px;
      }

      .whatsapp-btn svg {
        width: 28px;
        height: 28px;
      }

      .whatsapp-tooltip { display: none; }

      .projects-grid { grid-template-columns: 1fr; }

      .footer-content {
        flex-direction: column;
        text-align: center;
      }

      .footer-credit {
        justify-content: center;
      }
    }

    @media (max-width: 480px) {
      .hero-cta {
        flex-direction: column;
        width: 100%;
      }

      .btn { width: 100%; }

      .hero-stats {
        flex-wrap: wrap;
        justify-content: center;
      }

      .card-3d {
        width: 100%;
        max-width: 320px;
        height: 440px;
      }
    }
  </style>
</head>
<body>

  <!-- LOADER -->
  <div class="loader" id="loader">
    <div class="loader-logo">PORTFOLIO·3D</div>
    <div class="loader-author">Desenvolvido por <span>Leandro Ramos</span></div>
    <div class="loader-bar">
      <div class="loader-bar-fill"></div>
    </div>
  </div>

  <!-- CURSOR CUSTOMIZADO -->
  <div class="cursor-dot" id="cursorDot"></div>
  <div class="cursor-ring" id="cursorRing"></div>

  <!-- FUNDO ANIMADO -->
  <div class="bg-container">
    <div class="bg-gradient"></div>
    <div class="bg-grid"></div>
    <div class="particles" id="particles"></div>
  </div>

  <!-- NAVBAR -->
  <nav class="navbar" id="navbar">
    <a href="#" class="logo">
      <span class="logo-dot"></span>
      LR·3D
    </a>
    <ul class="nav-links">
      <li><a href="#home">Início</a></li>
      <li><a href="#projects">Projetos</a></li>
      <li><a href="#about">Sobre</a></li>
      <li><a href="#contact">Contato</a></li>
    </ul>
    <a href="https://wa.me/5511999999999" target="_blank" class="nav-cta">
      <span>Vamos Conversar →</span>
    </a>
  </nav>

  <div class="container">

    <!-- HERO -->
    <section class="hero" id="home">
      <div class="hero-grid">
        <div class="hero-left">
          <div class="hero-badge reveal">
            <span class="status-dot"></span>
            Disponível para novos projetos
          </div>
          <h1 class="hero-title reveal">
            <span class="line">Design que</span>
            <span class="line gradient">ganha vida</span>
            <span class="line">em 3D.</span>
          </h1>
          <p class="hero-desc reveal">
            Sou <strong>Leandro Ramos</strong>, designer e desenvolvedor front-end especializado em criar 
            <strong>experiências digitais imersivas</strong> que combinam estética tridimensional, 
            movimento e interfaces modernas.
          </p>
          <div class="hero-cta reveal">
            <a href="#projects" class="btn btn-primary">
              <span>
                Ver Projetos
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                  <path d="M5 12h14M12 5l7 7-7 7"/>
                </svg>
              </span>
            </a>
            <a href="https://wa.me/5511999999999" target="_blank" class="btn btn-outline">
              Falar no WhatsApp
            </a>
          </div>
          <div class="hero-stats reveal">
            <div class="stat">
              <div class="stat-num">48+</div>
              <div class="stat-label">Projetos</div>
            </div>
            <div class="stat">
              <div class="stat-num">7</div>
              <div class="stat-label">Anos Exp</div>
            </div>
            <div class="stat">
              <div class="stat-num">32</div>
              <div class="stat-label">Clientes</div>
            </div>
          </div>
        </div>

        <div class="hero-right">
          <div class="card-wrapper" id="cardWrapper">
            <div class="card-3d">
              <div class="card-content">
                <div class="card-header">
                  <div class="avatar">LR</div>
                  <div class="card-status">
                    <span class="status-dot"></span>
                    Online
                  </div>
                </div>
                <h3 class="card-name">Leandro Ramos</h3>
                <div class="card-role">Creative Developer</div>
                <div class="card-divider"></div>
                <div class="card-skills">
                  <span class="skill-tag">Three.js</span>
                  <span class="skill-tag">React</span>
                  <span class="skill-tag">WebGL</span>
                  <span class="skill-tag">Motion</span>
                  <span class="skill-tag">UI/UX</span>
                </div>
                <div class="card-footer">
                  <div>
                    <div class="card-stat-num">48+</div>
                    <div class="card-stat-label">Projetos</div>
                  </div>
                  <div>
                    <div class="card-stat-num">7</div>
                    <div class="card-stat-label">Anos</div>
                  </div>
                  <div>
                    <div class="card-stat-num">32</div>
                    <div class="card-stat-label">Clientes</div>
                  </div>
                </div>
              </div>
            </div>
            <div class="card-glow"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- PROJETOS -->
    <section id="projects">
      <div class="section-header">
        <div class="section-tag reveal">Portfólio</div>
        <h2 class="section-title reveal">
          Projetos <span class="gradient">em destaque</span>
        </h2>
        <p class="section-sub reveal">
          Uma seleção de trabalhos que exploram o melhor do design 3D, 
          interação e performance.
        </p>
      </div>

      <div class="projects-grid">
        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">🧊</div>
            <div class="project-year">2025</div>
          </div>
          <h3 class="project-title">Neon Dashboard</h3>
          <p class="project-desc">
            Interface 3D para visualização de dados com elementos flutuantes, 
            efeitos de profundidade e animações reativas em tempo real.
          </p>
          <div class="project-tags">
            <span class="project-tag">Three.js</span>
            <span class="project-tag">WebGL</span>
            <span class="project-tag">D3.js</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">🪐</div>
            <div class="project-year">2025</div>
          </div>
          <h3 class="project-title">Cosmic Store</h3>
          <p class="project-desc">
            E-commerce com visualização 3D de produtos, animações de gravidade 
            zero e checkout ultra-rápido.
          </p>
          <div class="project-tags">
            <span class="project-tag">React</span>
            <span class="project-tag">R3F</span>
            <span class="project-tag">GSAP</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">🔮</div>
            <div class="project-year">2024</div>
          </div>
          <h3 class="project-title">Aura Brand</h3>
          <p class="project-desc">
            Identidade visual interativa com elementos 3D que reagem ao 
            movimento do mouse e criam uma experiência sensorial única.
          </p>
          <div class="project-tags">
            <span class="project-tag">Branding</span>
            <span class="project-tag">Canvas</span>
            <span class="project-tag">GLSL</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">🌌</div>
            <div class="project-year">2024</div>
          </div>
          <h3 class="project-title">Galaxy Portfolio</h3>
          <p class="project-desc">
            Portfólio imersivo com navegação espacial, cards flutuantes e 
            ambientação estelar gerada proceduralmente.
          </p>
          <div class="project-tags">
            <span class="project-tag">Three.js</span>
            <span class="project-tag">GLSL</span>
            <span class="project-tag">Svelte</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">🧬</div>
            <div class="project-year">2024</div>
          </div>
          <h3 class="project-title">Bio Interface</h3>
          <p class="project-desc">
            Dashboard médico com representações 3D de dados biológicos, 
            animações orgânicas e foco em acessibilidade.
          </p>
          <div class="project-tags">
            <span class="project-tag">Vue</span>
            <span class="project-tag">WebGL</span>
            <span class="project-tag">D3.js</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>

        <div class="project-card reveal tilt-card">
          <div class="project-header">
            <div class="project-icon">⚡</div>
            <div class="project-year">2023</div>
          </div>
          <h3 class="project-title">Volt Agency</h3>
          <p class="project-desc">
            Site institucional com efeitos 3D em cada seção, transições 
            cinematográficas e performance otimizada.
          </p>
          <div class="project-tags">
            <span class="project-tag">Next.js</span>
            <span class="project-tag">Framer</span>
            <span class="project-tag">Tailwind</span>
          </div>
          <div class="project-arrow">↗</div>
        </div>
      </div>
    </section>

    <!-- CTA WHATSAPP -->
    <section id="contact" class="cta-section">
      <div class="cta-box reveal">
        <div class="cta-content">
          <h2 class="cta-title">
            Pronto para criar algo<br>
            <span class="gradient">extraordinário juntos?</span>
          </h2>
          <p class="cta-desc">
            Estou sempre aberto a novos projetos, colaborações e ideias ousadas. 
            Me chame no WhatsApp e vamos conversar.
          </p>
          <a href="https://wa.me/5511999999999?text=Olá%20Leandro!%20Vi%20seu%20portfólio%20e%20gostaria%20de%20conversar%20sobre%20um%20projeto." 
             target="_blank" 
             class="btn btn-primary" 
             style="padding: 18px 40px; font-size: 1rem;">
            <span>
              <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor" style="margin-right: 4px;">
                <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
              </svg>
              Conversar no WhatsApp
            </span>
          </a>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer>
      <div class="footer-content">
        <div class="footer-brand">
          <div class="footer-copy">
            © 2025 <strong style="color: var(--text);">PORTF·3D</strong> — Todos os direitos reservados.
          </div>
          <div class="footer-credit">
            <span class="heart">♥</span>
            Desenvolvido por <strong>Leandro Ramos</strong>
          </div>
        </div>
        <div class="footer-social">
          <a href="#" class="social-link" aria-label="GitHub">
            <svg viewBox="0 0 24 24"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
          </a>
          <a href="#" class="social-link" aria-label="LinkedIn">
            <svg viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          </a>
          <a href="#" class="social-link" aria-label="Dribbble">
            <svg viewBox="0 0 24 24"><path d="M12 24C5.385 24 0 18.615 0 12S5.385 0 12 0s12 5.385 12 12-5.385 12-12 12zm10.12-10.358c-.35-.11-3.17-.953-6.384-.438 1.34 3.684 1.887 6.684 1.992 7.308 2.3-1.555 3.936-4.02 4.395-6.87zm-6.115 7.808c-.153-.9-.75-4.032-2.19-7.77l-.066.02c-5.79 2.015-7.86 6.025-8.04 6.4 1.73 1.358 3.92 2.166 6.29 2.166 1.42 0 2.77-.29 4-.814zm-11.62-2.58c.232-.4 3.045-5.055 8.332-6.765.135-.045.27-.084.405-.12-.26-.585-.54-1.167-.832-1.74C7.17 11.775 2.206 11.71 1.756 11.7l-.004.312c0 2.633.998 5.037 2.634 6.855zm-2.42-8.955c.46.008 4.683.026 9.477-1.248-1.698-3.018-3.53-5.558-3.8-5.928-2.868 1.35-5.01 3.99-5.676 7.17zM9.6 2.052c.282.38 2.145 2.914 3.822 6 3.645-1.365 5.19-3.44 5.373-3.702-1.81-1.61-4.19-2.586-6.795-2.586-.825 0-1.63.1-2.4.285zm10.335 3.483c-.218.29-1.935 2.493-5.724 4.04.24.49.47.985.68 1.486.08.18.15.36.22.53 3.41-.43 6.8.26 7.14.33-.02-2.42-.88-4.64-2.31-6.38z"/></svg>
          </a>
          <a href="#" class="social-link" aria-label="Behance">
            <svg viewBox="0 0 24 24"><path d="M22 7h-7V5h7v2zm1.726 10c-.442 1.297-2.029 3-5.101 3-3.074 0-5.564-1.729-5.564-5.675 0-3.91 2.325-5.92 5.466-5.92 3.082 0 4.964 1.782 5.375 4.426.078.506.109 1.188.095 2.14H15.97c.13 3.211 3.483 3.312 4.588 2.029h3.168zm-7.686-4h4.965c-.105-1.547-1.136-2.219-2.477-2.219-1.466 0-2.277.768-2.488 2.219zm-9.574 6.988H0V5.021h6.953c5.476.081 5.58 5.444 2.72 6.906 3.461 1.26 3.577 8.061-3.207 8.061zM3 11h3.584c2.508 0 2.906-3-.312-3H3v3zm3.391 3H3v3.016h3.341c3.055 0 2.868-3.016.05-3.016z"/></svg>
          </a>
        </div>
      </div>
    </footer>
  </div>

  <!-- BOTÃO WHATSAPP FLUTUANTE -->
  <a href="https://wa.me/5511999999999?text=Olá%20Leandro!%20Vim%20do%20seu%20portfólio%203D%20e%20gostaria%20de%20conversar." 
     target="_blank" 
     class="whatsapp-float"
     aria-label="Falar no WhatsApp">
    <div class="whatsapp-tooltip">
      Vamos conversar? 💬
      <small>Resposta em minutos</small>
    </div>
    <div class="whatsapp-btn">
      <span class="whatsapp-badge">1</span>
      <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
      </svg>
    </div>
  </a>

  <script>
    /* ============================================
       PORTFÓLIO 3D · Desenvolvido por Leandro Ramos
       ============================================ */

    /* ========= LOADER ========= */
    window.addEventListener('load', () => {
      setTimeout(() => {
        document.getElementById('loader').classList.add('hidden');
      }, 1900);
    });

    /* ========= CURSOR CUSTOMIZADO ========= */
    const cursorDot = document.getElementById('cursorDot');
    const cursorRing = document.getElementById('cursorRing');
    let mouseX = 0, mouseY = 0;
    let ringX = 0, ringY = 0;

    document.addEventListener('mousemove', (e) => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      cursorDot.style.left = mouseX + 'px';
      cursorDot.style.top = mouseY + 'px';
    });

    function animateRing() {
      ringX += (mouseX - ringX) * 0.15;
      ringY += (mouseY - ringY) * 0.15;
      cursorRing.style.left = ringX + 'px';
      cursorRing.style.top = ringY + 'px';
      requestAnimationFrame(animateRing);
    }
    animateRing();

    const hoverElements = document.querySelectorAll('a, button, .project-card, .skill-tag, .social-link, .btn');
    hoverElements.forEach(el => {
      el.addEventListener('mouseenter', () => {
        cursorDot.classList.add('hover');
        cursorRing.classList.add('hover');
      });
      el.addEventListener('mouseleave', () => {
        cursorDot.classList.remove('hover');
        cursorRing.classList.remove('hover');
      });
    });

    /* ========= PARTÍCULAS ========= */
    const particlesContainer = document.getElementById('particles');
    const particleCount = 30;

    for (let i = 0; i < particleCount; i++) {
      const particle = document.createElement('div');
      particle.className = 'particle';
      const size = Math.random() * 3 + 1;
      particle.style.width = size + 'px';
      particle.style.height = size + 'px';
      particle.style.left = Math.random() * 100 + '%';
      particle.style.animationDuration = (Math.random() * 15 + 10) + 's';
      particle.style.animationDelay = (Math.random() * 15) + 's';
      
      const colors = ['#00e5ff', '#7c5cff', '#ff3d71'];
      const color = colors[Math.floor(Math.random() * colors.length)];
      particle.style.background = color;
      particle.style.boxShadow = `0 0 10px ${color}`;
      
      particlesContainer.appendChild(particle);
    }

    /* ========= NAVBAR SCROLL ========= */
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      if (window.scrollY > 50) {
        navbar.classList.add('scrolled');
      } else {
        navbar.classList.remove('scrolled');
      }
    });

    /* ========= SCROLL REVEAL ========= */
    const revealElements = document.querySelectorAll('.reveal');
    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach((entry, index) => {
        if (entry.isIntersecting) {
          setTimeout(() => {
            entry.target.classList.add('active');
          }, index * 100);
          revealObserver.unobserve(entry.target);
        }
      });
    }, {
      threshold: 0.15,
      rootMargin: '0px 0px -50px 0px'
    });

    revealElements.forEach(el => revealObserver.observe(el));

    /* ========= TILT 3D NO CARD PRINCIPAL ========= */
    const cardWrapper = document.getElementById('cardWrapper');
    const heroRight = document.querySelector('.hero-right');

    if (heroRight && cardWrapper && window.innerWidth > 1024) {
      heroRight.addEventListener('mousemove', (e) => {
        const rect = heroRight.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const centerX = rect.width / 2;
        const centerY = rect.height / 2;
        
        const rotateY = ((x - centerX) / centerX) * 12;
        const rotateX = ((y - centerY) / centerY) * -12;
        
        cardWrapper.style.transform = `rotateY(${rotateY}deg) rotateX(${rotateX}deg)`;
      });

      heroRight.addEventListener('mouseleave', () => {
        cardWrapper.style.transform = 'rotateY(0deg) rotateX(0deg)';
      });
    }

    /* ========= TILT 3D NOS CARDS DE PROJETO ========= */
    const tiltCards = document.querySelectorAll('.tilt-card');
    
    tiltCards.forEach(card => {
      card.addEventListener('mousemove', (e) => {
        const rect = card.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const centerX = rect.width / 2;
        const centerY = rect.height / 2;
        
        const rotateY = ((x - centerX) / centerX) * 8;
        const rotateX = ((y - centerY) / centerY) * -8;
        
        card.style.transform = `perspective(1000px) rotateY(${rotateY}deg) rotateX(${rotateX}deg) translateY(-8px)`;
        card.style.setProperty('--mx', x + 'px');
        card.style.setProperty('--my', y + 'px');
      });

      card.addEventListener('mouseleave', () => {
        card.style.transform = '';
      });
    });

    /* ========= SMOOTH SCROLL ========= */
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function(e) {
        const href = this.getAttribute('href');
        if (href === '#') return;
        
        e.preventDefault();
        const target = document.querySelector(href);
        if (target) {
          target.scrollIntoView({
            behavior: 'smooth',
            block: 'start'
          });
        }
      });
    });

    /* ========= PARALLAX NO SCROLL ========= */
    let ticking = false;
    window.addEventListener('scroll', () => {
      if (!ticking) {
        window.requestAnimationFrame(() => {
          const scrolled = window.pageYOffset;
          const bgGrid = document.querySelector('.bg-grid');
          if (bgGrid) {
            bgGrid.style.transform = `perspective(600px) rotateX(60deg) translateZ(-200px) translateY(${scrolled * 0.3}px)`;
          }
          ticking = false;
        });
        ticking = true;
      }
    });

    /* ========= EFEITO MAGNÉTICO NOS BOTÕES ========= */
    const magneticButtons = document.querySelectorAll('.btn-primary, .nav-cta');
    
    magneticButtons.forEach(btn => {
      btn.addEventListener('mousemove', (e) => {
        const rect = btn.getBoundingClientRect();
        const x = e.clientX - rect.left - rect.width / 2;
        const y = e.clientY - rect.top - rect.height / 2;
        
        btn.style.transform = `translate(${x * 0.15}px, ${y * 0.15}px) translateY(-3px)`;
      });
      
      btn.addEventListener('mouseleave', () => {
        btn.style.transform = '';
      });
    });

    /* ========= CONSOLE CREDIT ========= */
    console.log(
      '%c PORTFÓLIO 3D %c Desenvolvido por Leandro Ramos ',
      'background: linear-gradient(135deg, #7c5cff, #00e5ff); color: white; padding: 8px 16px; border-radius: 8px 0 0 8px; font-weight: 700; font-size: 14px;',
      'background: #0a0a18; color: #a78bfa; padding: 8px 16px; border-radius: 0 8px 8px 0; font-weight: 600; font-size: 14px;'
    );
  </script>
</body>
</html>
