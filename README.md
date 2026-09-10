<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Saccharum | The Sugarcane Project</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-dark: #070d0a;
      --bg-card: rgba(14, 25, 20, 0.7);
      --border-glow: rgba(52, 211, 153, 0.25);
      --cane-green: #10b981;
      --cane-glow: #34d399;
      --accent-gold: #f59e0b;
      --text-main: #f3f4f6;
      --text-muted: #9ca3af;
      --font-serif: 'Cinzel', serif;
      --font-sans: 'Plus Jakarta Sans', sans-serif;
      --transition-smooth: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      scroll-behavior: smooth;
    }

    body {
      background-color: var(--bg-dark);
      color: var(--text-main);
      font-family: var(--font-sans);
      overflow-x: hidden;
      line-height: 1.6;
    }

    /* Ambient Background Glow */
    .ambient-glow {
      position: fixed;
      top: -20%;
      left: 50%;
      transform: translateX(-50%);
      width: 80vw;
      height: 60vh;
      background: radial-gradient(circle, rgba(16, 185, 129, 0.12) 0%, rgba(5, 150, 105, 0.04) 40%, transparent 70%);
      pointer-events: none;
      z-index: 0;
    }

    /* Navigation */
    header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      z-index: 100;
      backdrop-filter: blur(16px);
      background: rgba(7, 13, 10, 0.75);
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 1rem 3rem;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      font-family: var(--font-serif);
      font-size: 1.3rem;
      font-weight: 700;
      letter-spacing: 2px;
      color: #fff;
    }

    .brand span {
      color: var(--cane-glow);
    }

    .nav-links {
      display: flex;
      gap: 2rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--text-muted);
      text-decoration: none;
      font-size: 0.9rem;
      font-weight: 500;
      letter-spacing: 1px;
      text-transform: uppercase;
      transition: var(--transition-smooth);
    }

    .nav-links a:hover {
      color: var(--cane-glow);
    }

    .badge-btn {
      background: linear-gradient(135deg, rgba(16, 185, 129, 0.2), rgba(5, 150, 105, 0.4));
      border: 1px solid var(--cane-glow);
      color: #fff;
      padding: 0.5rem 1.25rem;
      border-radius: 9999px;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      transition: var(--transition-smooth);
    }

    .badge-btn:hover {
      box-shadow: 0 0 20px rgba(52, 211, 153, 0.4);
      transform: translateY(-2px);
    }

    /* Hero Carousel */
    .hero-carousel {
      position: relative;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 7rem 2rem 3rem;
      text-align: center;
      z-index: 10;
    }

    .carousel-stage {
      position: relative;
      width: 100%;
      max-width: 1200px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 1.5rem 0;
    }

    /* Flanking Cards */
    .flank-card {
      background: rgba(14, 25, 20, 0.4);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 20px;
      padding: 1.5rem;
      width: 200px;
      cursor: pointer;
      opacity: 0.45;
      transition: var(--transition-smooth);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.75rem;
      user-select: none;
    }

    .flank-card:hover {
      opacity: 0.85;
      transform: scale(1.05);
      border-color: var(--cane-glow);
    }

    .flank-card.left {
      transform: perspective(600px) rotateY(15deg);
    }

    .flank-card.right {
      transform: perspective(600px) rotateY(-15deg);
    }

    .flank-card .flank-icon {
      width: 60px;
      height: 60px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(52, 211, 153, 0.2), rgba(0, 0, 0, 0.8));
      display: flex;
      align-items: center;
      justify-content: center;
      border: 1px solid rgba(52, 211, 153, 0.3);
    }

    .flank-card span {
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    /* Center Featured Variety */
    .featured-stalk-container {
      position: relative;
      flex: 1;
      max-width: 650px;
      padding: 2rem;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .halo-effect {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 420px;
      height: 420px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(16, 185, 129, 0.22) 0%, rgba(16, 185, 129, 0.05) 50%, transparent 70%);
      filter: blur(30px);
      z-index: -1;
      animation: pulseHalo 6s ease-in-out infinite alternate;
    }

    @keyframes pulseHalo {
      0% { transform: translate(-50%, -50%) scale(0.9); opacity: 0.6; }
      100% { transform: translate(-50%, -50%) scale(1.15); opacity: 1; }
    }

    .stalk-visual {
      position: relative;
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 1.5rem;
      filter: drop-shadow(0 10px 25px rgba(16, 185, 129, 0.3));
      transition: transform 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
    }

    .stalk-visual:hover {
      transform: scale(1.06) rotate(-2deg);
    }

    .variety-subtitle {
      font-size: 0.85rem;
      letter-spacing: 3px;
      color: var(--cane-glow);
      text-transform: uppercase;
      font-weight: 600;
      margin-bottom: 0.5rem;
    }

    .variety-title {
      font-family: var(--font-serif);
      font-size: 3.2rem;
      font-weight: 900;
      letter-spacing: 2px;
      color: #fff;
      line-height: 1.1;
      margin-bottom: 0.5rem;
    }

    .variety-botanical {
      font-style: italic;
      color: #a7f3d0;
      font-size: 1.1rem;
      margin-bottom: 1.25rem;
    }

    .variety-desc {
      max-width: 540px;
      color: var(--text-muted);
      font-size: 1rem;
      line-height: 1.7;
      margin-bottom: 2rem;
    }

    /* Specs Pill Bar */
    .specs-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      justify-content: center;
      margin-bottom: 2rem;
    }

    .spec-pill {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 9999px;
      padding: 0.5rem 1.25rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.85rem;
    }

    .spec-pill .pill-val {
      color: var(--cane-glow);
      font-weight: 700;
    }

    /* Buttons */
    .cta-group {
      display: flex;
      align-items: center;
      gap: 1.5rem;
    }

    .learn-btn {
      display: inline-flex;
      align-items: center;
      gap: 0.75rem;
      background: linear-gradient(135deg, #10b981, #059669);
      color: #fff;
      padding: 0.9rem 2rem;
      border-radius: 9999px;
      border: none;
      font-size: 0.95rem;
      font-weight: 700;
      letter-spacing: 1px;
      cursor: pointer;
      box-shadow: 0 4px 20px rgba(16, 185, 129, 0.4);
      transition: var(--transition-smooth);
    }

    .learn-btn:hover {
      box-shadow: 0 6px 30px rgba(52, 211, 153, 0.6);
      transform: translateY(-3px);
    }

    .audio-btn {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.15);
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: var(--transition-smooth);
    }

    .audio-btn:hover {
      border-color: var(--cane-glow);
      background: rgba(52, 211, 153, 0.15);
      transform: scale(1.1);
    }

    /* Dots */
    .dots-nav {
      display: flex;
      gap: 0.75rem;
      margin-top: 2rem;
    }

    .dot {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.2);
      cursor: pointer;
      transition: var(--transition-smooth);
    }

    .dot.active {
      width: 32px;
      border-radius: 9999px;
      background: var(--cane-glow);
      box-shadow: 0 0 12px var(--cane-glow);
    }

    /* Modal */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0, 0, 0, 0.85);
      backdrop-filter: blur(10px);
      z-index: 200;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 1.5rem;
    }

    .modal-overlay.active {
      opacity: 1;
      pointer-events: all;
    }

    .modal-content {
      background: #0d1612;
      border: 1px solid rgba(52, 211, 153, 0.3);
      border-radius: 24px;
      max-width: 750px;
      width: 100%;
      max-height: 90vh;
      overflow-y: auto;
      padding: 2.5rem;
      position: relative;
      transform: scale(0.92) translateY(20px);
      transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .modal-overlay.active .modal-content {
      transform: scale(1) translateY(0);
    }

    .close-modal {
      position: absolute;
      top: 1.5rem;
      right: 1.5rem;
      background: rgba(255, 255, 255, 0.08);
      border: none;
      color: #fff;
      width: 36px;
      height: 36px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
      transition: var(--transition-smooth);
    }

    .close-modal:hover {
      background: rgba(239, 68, 68, 0.6);
    }

    /* Sections */
    section {
      position: relative;
      z-index: 10;
      padding: 6rem 2rem;
      max-width: 1200px;
      margin: 0 auto;
    }

    .section-header {
      text-align: center;
      margin-bottom: 3.5rem;
    }

    .section-eyebrow {
      color: var(--cane-glow);
      font-size: 0.85rem;
      text-transform: uppercase;
      letter-spacing: 3px;
      font-weight: 700;
      margin-bottom: 0.5rem;
    }

    .section-title {
      font-family: var(--font-serif);
      font-size: 2.6rem;
      letter-spacing: 1px;
      color: #fff;
    }

    /* Climate Grid */
    .climate-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.5rem;
    }

    .climate-card {
      background: var(--bg-card);
      border: 1px solid rgba(255, 255, 255, 0.07);
      border-radius: 20px;
      padding: 2rem;
      transition: var(--transition-smooth);
      position: relative;
      overflow: hidden;
    }

    .climate-card:hover {
      transform: translateY(-6px);
      border-color: var(--cane-glow);
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5), 0 0 20px rgba(16, 185, 129, 0.15);
    }

    .climate-card .card-icon {
      width: 52px;
      height: 52px;
      border-radius: 14px;
      background: rgba(16, 185, 129, 0.15);
      border: 1px solid rgba(52, 211, 153, 0.3);
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 1.25rem;
      color: var(--cane-glow);
    }

    .climate-card h3 {
      font-size: 1.2rem;
      margin-bottom: 0.75rem;
      color: #fff;
    }

    .climate-card p {
      color: var(--text-muted);
      font-size: 0.95rem;
      line-height: 1.6;
    }

    .climate-card .exam-tip {
      margin-top: 1rem;
      padding-top: 0.75rem;
      border-top: 1px dashed rgba(255, 255, 255, 0.1);
      font-size: 0.8rem;
      color: #fbbf24;
    }

    /* Comparison Table */
    .compare-container {
      background: var(--bg-card);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 24px;
      overflow: hidden;
      box-shadow: 0 20px 40px rgba(0,0,0,0.6);
    }

    .compare-table {
      width: 100%;
      border-collapse: collapse;
      text-align: left;
    }

    .compare-table th, .compare-table td {
      padding: 1.25rem 1.5rem;
      border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    }

    .compare-table th {
      background: rgba(16, 185, 129, 0.12);
      font-family: var(--font-serif);
      font-size: 1.1rem;
      color: #fff;
    }

    .compare-table tr:hover {
      background: rgba(255, 255, 255, 0.02);
    }

    .factor-col {
      font-weight: 600;
      color: var(--cane-glow);
      width: 25%;
    }

    /* Process Flow */
    .process-flow {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 1.5rem;
      position: relative;
    }

    .step-card {
      background: rgba(14, 25, 20, 0.6);
      border: 1px solid rgba(255, 255, 255, 0.06);
      border-radius: 18px;
      padding: 1.75rem;
      position: relative;
      transition: var(--transition-smooth);
    }

    .step-card:hover {
      border-color: var(--cane-glow);
      transform: translateY(-4px);
    }

    .step-num {
      font-family: var(--font-serif);
      font-size: 1.8rem;
      font-weight: 700;
      color: rgba(52, 211, 153, 0.3);
      position: absolute;
      top: 1rem;
      right: 1.25rem;
    }

    .byproduct-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.25rem;
      margin-top: 3rem;
    }

    .byproduct-card {
      background: linear-gradient(145deg, rgba(20, 35, 28, 0.7), rgba(10, 18, 14, 0.9));
      border: 1px solid rgba(52, 211, 153, 0.2);
      border-radius: 16px;
      padding: 1.5rem;
    }

    .byproduct-card h4 {
      color: var(--accent-gold);
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    /* Quiz Box */
    .quiz-box {
      background: var(--bg-card);
      border: 1px solid rgba(52, 211, 153, 0.3);
      border-radius: 24px;
      padding: 2.5rem;
      max-width: 800px;
      margin: 0 auto;
    }

    .quiz-question {
      font-size: 1.25rem;
      font-weight: 600;
      margin-bottom: 1.5rem;
      color: #fff;
    }

    .quiz-options {
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
      margin-bottom: 1.5rem;
    }

    .option-btn {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 12px;
      padding: 1rem 1.25rem;
      color: var(--text-main);
      text-align: left;
      font-size: 0.95rem;
      cursor: pointer;
      transition: var(--transition-smooth);
    }

    .option-btn:hover {
      background: rgba(16, 185, 129, 0.15);
      border-color: var(--cane-glow);
    }

    .option-btn.correct {
      background: rgba(16, 185, 129, 0.3) !important;
      border-color: #10b981 !important;
      color: #a7f3d0;
    }

    .option-btn.wrong {
      background: rgba(239, 68, 68, 0.3) !important;
      border-color: #ef4444 !important;
      color: #fca5a5;
    }

    .quiz-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-top: 1px solid rgba(255, 255, 255, 0.08);
      padding-top: 1rem;
    }

    .next-quiz-btn {
      background: var(--cane-green);
      color: #fff;
      border: none;
      padding: 0.6rem 1.5rem;
      border-radius: 9999px;
      font-weight: 600;
      cursor: pointer;
    }

    /* Footer */
    footer {
      text-align: center;
      padding: 4rem 2rem 2rem;
      border-top: 1px solid rgba(255, 255, 255, 0.08);
      color: var(--text-muted);
      font-size: 0.85rem;
    }

    /* Responsive */
    @media (max-width: 900px) {
      header {
        padding: 1rem 1.5rem;
      }
      .nav-links {
        display: none;
      }
      .carousel-stage {
        flex-direction: column;
      }
      .flank-card {
        display: none;
      }
      .variety-title {
        font-size: 2.3rem;
      }
      .featured-stalk-container {
        padding: 1rem 0;
      }
    }
  </style>
</head>
<body>

  <div class="ambient-glow"></div>

  <!-- Top Navbar -->
  <header>
    <div class="brand">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <path d="M12 2v20M8 5h8M7 10h10M8 15h8M9 19h6" stroke="#34d399"/>
      </svg>
      SACCHARUM <span>EDU</span>
    </div>
    <ul class="nav-links">
      <li><a href="#varieties">Varieties</a></li>
      <li><a href="#climate">Climate & Soil</a></li>
      <li><a href="#comparison">North vs South</a></li>
      <li><a href="#byproducts">By-Products</a></li>
      <li><a href="#quiz">Class 10 Quiz</a></li>
    </ul>
    <button class="badge-btn" onclick="document.getElementById('quiz').scrollIntoView();">Test Your Knowledge</button>
  </header>

  <!-- Hero Carousel (UI/UX Spaceedu Adaptation) -->
  <div class="hero-carousel" id="varieties">
    <div class="carousel-stage">
      
      <!-- Left Thumbnail Preview -->
      <div class="flank-card left" id="leftFlank" onclick="prevVariety()">
        <div class="flank-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#34d399" stroke-width="2">
            <polyline points="15 18 9 12 15 6"></polyline>
          </svg>
        </div>
        <span id="leftFlankName">Wild Cane</span>
        <small style="color:#6b7280; font-size:0.75rem;">Previous</small>
      </div>

      <!-- Main Central Feature -->
      <div class="featured-stalk-container">
        <div class="halo-effect"></div>

        <!-- Animated Sugarcane Stalk Graphic -->
        <div class="stalk-visual" id="stalkVisual">
          <svg width="120" height="260" viewBox="0 0 120 260" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="48" y="30" width="24" height="42" rx="4" fill="url(#caneGrad)" stroke="#059669" stroke-width="2"/>
            <rect x="47" y="74" width="26" height="42" rx="4" fill="url(#caneGrad)" stroke="#059669" stroke-width="2"/>
            <rect x="46" y="118" width="28" height="42" rx="4" fill="url(#caneGrad)" stroke="#059669" stroke-width="2"/>
            <rect x="45" y="162" width="30" height="44" rx="4" fill="url(#caneGrad)" stroke="#059669" stroke-width="2"/>
            <rect x="44" y="208" width="32" height="42" rx="4" fill="url(#caneGrad)" stroke="#059669" stroke-width="2"/>
            
            <ellipse cx="60" cy="73" rx="15" ry="3.5" fill="#f59e0b" opacity="0.9"/>
            <ellipse cx="60" cy="117" rx="16" ry="3.5" fill="#f59e0b" opacity="0.9"/>
            <ellipse cx="60" cy="161" rx="17" ry="4" fill="#f59e0b" opacity="0.9"/>
            <ellipse cx="60" cy="207" rx="18" ry="4" fill="#f59e0b" opacity="0.9"/>

            <path d="M50 34 C20 10 5 -5 0 -20 C20 -5 45 15 52 30" fill="#10b981" opacity="0.85"/>
            <path d="M70 34 C100 10 115 -5 120 -20 C100 -5 75 15 68 30" fill="#34d399" opacity="0.85"/>
            <path d="M60 20 C60 -10 65 -30 60 -40 C55 -30 55 -10 60 20" fill="#059669" opacity="0.9"/>

            <defs>
              <linearGradient id="caneGrad" x1="48" y1="30" x2="72" y2="250" gradientUnits="userSpaceOnUse">
                <stop stop-color="#34d399"/>
                <stop offset="0.5" stop-color="#10b981"/>
                <stop offset="1" stop-color="#047857"/>
              </linearGradient>
            </defs>
          </svg>
        </div>

        <div class="variety-subtitle" id="varietySubtitle">CANES OF THE WORLD</div>
        <h1 class="variety-title" id="varietyTitle">NOBLE CANE</h1>
        <div class="variety-botanical" id="varietyBotanical">Saccharum officinarum</div>
        <p class="variety-desc" id="varietyDesc">
          Known as the true tropical cane with thick, succulent stalks and very high sucrose concentration. The bedrock of modern commercial sugar manufacturing in Peninsular India.
        </p>

        <!-- Dynamic Key Stats Pills -->
        <div class="specs-grid" id="specsGrid">
          <div class="spec-pill"><span>Sucrose:</span> <span class="pill-val" id="specSucrose">14% – 17%</span></div>
          <div class="spec-pill"><span>Primary Belt:</span> <span class="pill-val" id="specBelt">Peninsular India</span></div>
          <div class="spec-pill"><span>Stalk Thickness:</span> <span class="pill-val" id="specThickness">Thick (3–5 cm)</span></div>
          <div class="spec-pill"><span>Frost Tolerance:</span> <span class="pill-val" id="specFrost">Low (Tropical)</span></div>
        </div>

        <!-- Buttons -->
        <div class="cta-group">
          <button class="learn-btn" onclick="openDetailsModal()">
            <span>LEARN MORE</span>
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5">
              <line x1="5" y1="12" x2="19" y2="12"></line>
              <polyline points="12 5 19 12 12 19"></polyline>
            </svg>
          </button>
          <button class="audio-btn" title="Pronounce Botanical Name" onclick="speakBotanicalName()">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>
              <path d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"></path>
            </svg>
          </button>
        </div>

      </div>

      <!-- Right Thumbnail Preview -->
      <div class="flank-card right" id="rightFlank" onclick="nextVariety()">
        <div class="flank-icon">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#34d399" stroke-width="2">
            <polyline points="9 18 15 12 9 6"></polyline>
          </svg>
        </div>
        <span id="rightFlankName">North Indian Cane</span>
        <small style="color:#6b7280; font-size:0.75rem;">Next</small>
      </div>

    </div>

    <!-- Navigation Dots -->
    <div class="dots-nav" id="dotsContainer"></div>
  </div>

  <!-- Deep Dive Interactive Modal -->
  <div class="modal-overlay" id="detailsModal">
    <div class="modal-content">
      <button class="close-modal" onclick="closeDetailsModal()">&times;</button>
      <div class="section-eyebrow" id="modalTag">BOTANICAL & AGRONOMIC DOSSIER</div>
      <h2 style="font-family: var(--font-serif); font-size: 2rem; margin-bottom: 0.5rem; color:#fff;" id="modalTitle">Noble Cane</h2>
      <p style="color: #a7f3d0; font-style:italic; margin-bottom: 1.5rem;" id="modalBotanical">Saccharum officinarum</p>
      
      <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem; margin-bottom: 1.5rem;">
        <div style="background: rgba(255,255,255,0.03); padding: 1rem; border-radius: 12px; border: 1px solid rgba(255,255,255,0.08);">
          <div style="color: var(--text-muted); font-size: 0.8rem;">Average Stalk Yield</div>
          <div style="color: var(--cane-glow); font-size: 1.3rem; font-weight:700;" id="modalYield">85 - 110 tonnes/ha</div>
        </div>
        <div style="background: rgba(255,255,255,0.03); padding: 1rem; border-radius: 12px; border: 1px solid rgba(255,255,255,0.08);">
          <div style="color: var(--text-muted); font-size: 0.8rem;">Crushing Recovery</div>
          <div style="color: var(--cane-glow); font-size: 1.3rem; font-weight:700;" id="modalRecovery">11.5% - 13.0%</div>
        </div>
        <div style="background: rgba(255,255,255,0.03); padding: 1rem; border-radius: 12px; border: 1px solid rgba(255,255,255,0.08);">
          <div style="color: var(--text-muted); font-size: 0.8rem;">Fibre Content</div>
          <div style="color: var(--accent-gold); font-size: 1.3rem; font-weight:700;" id="modalFibre">10% - 12% (Low/Soft)</div>
        </div>
      </div>

      <div style="margin-bottom: 1.5rem;">
        <h4 style="color:#fff; margin-bottom: 0.5rem;">Origin & Historical Significance</h4>
        <p style="color: var(--text-muted); font-size: 0.95rem; line-height: 1.6;" id="modalOrigin">
          Native to New Guinea and Southeast Asia, *S. officinarum* was historically called 'Noble' due to its thick stalks, high juice volume, and rich sweet taste.
        </p>
      </div>

      <div>
        <h4 style="color:#fff; margin-bottom: 0.5rem;">Relevance in Class 10 Board Examinations</h4>
        <p style="color: #cbd5e1; font-size: 0.95rem; line-height: 1.6; background: rgba(16, 185, 129, 0.1); border-left: 3px solid var(--cane-green); padding: 0.75rem 1rem; border-radius: 0 8px 8px 0;" id="modalClass10Note">
          Directly explains why sugar mills flourish in Maharashtra and Tamil Nadu: this tropical variety gives far superior sucrose yields compared to northern sub-tropical strains.
        </p>
      </div>
    </div>
  </div>

  <!-- Section 1: Climatic Requirements -->
  <section id="climate">
    <div class="section-header">
      <div class="section-eyebrow">GEOGRAPHICAL CRITERIA</div>
      <h2 class="section-title">Ideal Growing Conditions</h2>
      <p style="color: var(--text-muted); max-width:600px; margin: 0.5rem auto 0;">Sugarcane is a tropical as well as a sub-tropical crop that takes 10 to 18 months to mature depending on regional weather patterns.</p>
    </div>

    <div class="climate-grid">
      <div class="climate-card">
        <div class="card-icon">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M14 14.76V3.5a2.5 2.5 0 0 0-5 0v11.26a4.5 4.5 0 1 0 5 0z"/>
          </svg>
        </div>
        <h3>Temperature</h3>
        <p>Thrives in a hot and humid climate with a temperature range between <strong>21°C and 27°C</strong>.</p>
        <div class="exam-tip">Exam Alert: Temperatures below 20°C retard growth; severe winter frost destroys the crop completely.</div>
      </div>

      <div class="climate-card">
        <div class="card-icon">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M20 16.2A4.5 4.5 0 0 0 17.5 8h-1.8A7 7 0 1 0 4 14.9"/>
            <path d="M16 14v6M8 14v6M12 16v6"/>
          </svg>
        </div>
        <h3>Annual Rainfall</h3>
        <p>Requires an annual rainfall of <strong>75 cm to 100 cm</strong> evenly distributed over the growth period.</p>
        <div class="exam-tip">Exam Alert: In regions with low rainfall (like parts of Punjab & Haryana), extensive canal or tubewell irrigation is mandatory.</div>
      </div>

      <div class="climate-card">
        <div class="card-icon">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M3 21h18M3 10h18M3 7l9-4 9 4M4 10v11M20 10v11M8 14v7M12 14v7M16 14v7"/>
          </svg>
        </div>
        <h3>Soil Types</h3>
        <p>Needs deep, rich, well-drained loamy, alluvial, or black lava soils that retain moisture without becoming waterlogged.</p>
        <div class="exam-tip">Exam Alert: Heavy fertilizer application (Nitrogen, Potash, Phosphorus) is required as sugarcane severely exhausts soil nutrients.</div>
      </div>

      <div class="climate-card">
        <div class="card-icon">
          <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="5"/>
            <line x1="12" y1="1" x2="12" y2="3"/>
            <line x1="12" y1="21" x2="12" y2="23"/>
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"/>
            <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"/>
          </svg>
        </div>
        <h3>Sunlight & Ripening</h3>
        <p>Short cool nights with bright sunny days during the ripening period are critical for maximum sucrose concentration in the stalks.</p>
        <div class="exam-tip">Exam Alert: High humidity during vegetative growth followed by dry, sunny weather before harvest produces the sweetest juice.</div>
      </div>
    </div>
  </section>

  <!-- Section 2: North vs South Comparison -->
  <section id="comparison">
    <div class="section-header">
      <div class="section-eyebrow">REGIONAL DYNAMICS</div>
      <h2 class="section-title">The Sugar Industry Shift: North vs South</h2>
      <p style="color: var(--text-muted); max-width:650px; margin: 0.5rem auto 0;">In recent decades, there has been a distinct southward shift of the Indian sugar industry into the Peninsular belt. Here is the comparative breakdown.</p>
    </div>

    <div class="compare-container">
      <table class="compare-table">
        <thead>
          <tr>
            <th>Factor</th>
            <th>Northern Belt (UP, Bihar, Punjab)</th>
            <th>Southern Belt (Maharashtra, TN, Karnataka)</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="factor-col">Climate & Weather</td>
            <td>Sub-tropical climate; severe winter cold and frost retard growth and lower juice quality.</td>
            <td>Maritime tropical climate with no frost; warm temperatures throughout the year.</td>
          </tr>
          <tr>
            <td class="factor-col">Sucrose Content</td>
            <td>Lower sucrose percentage due to extreme seasonal swings and dry summer winds (Loo).</td>
            <td>Higher sucrose concentration due to maritime humidity and steady sunshine.</td>
          </tr>
          <tr>
            <td class="factor-col">Crushing Season</td>
            <td>Short crushing window: typically only <strong>4 to 5 months</strong> (November to March).</td>
            <td>Long crushing window: lasts <strong>7 to 8 months</strong> (October to May/June).</td>
          </tr>
          <tr>
            <td class="factor-col">Average Yield</td>
            <td>Moderate yield per hectare (approx. 60–70 tonnes/ha).</td>
            <td>High yield per hectare (exceeding 85–100 tonnes/ha in canal-irrigated zones).</td>
          </tr>
          <tr>
            <td class="factor-col">Mill Management</td>
            <td>Predominantly older, privately owned mills with higher transportation lag.</td>
            <td>Modern mills predominantly organized under successful farmer-run <strong>cooperatives</strong>.</td>
          </tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- Section 3: By-Products & Processing -->
  <section id="byproducts">
    <div class="section-header">
      <div class="section-eyebrow">CIRCULAR BIO-ECONOMY</div>
      <h2 class="section-title">Zero-Waste By-Products</h2>
      <p style="color: var(--text-muted); max-width:600px; margin: 0.5rem auto 0;">Sugarcane is one of the most efficient industrial crops where almost nothing goes to waste.</p>
    </div>

    <div class="process-flow">
      <div class="step-card">
        <span class="step-num">01</span>
        <h3 style="color:#fff; margin-bottom: 0.5rem;">Sett Planting</h3>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Cuttings of mature stalks (setts) with 2–3 buds are planted in furrows with organic manure.</p>
      </div>
      <div class="step-card">
        <span class="step-num">02</span>
        <h3 style="color:#fff; margin-bottom: 0.5rem;">Ratooning</h3>
        <p style="color: var(--text-muted); font-size: 0.9rem;">After cutting the first crop, the root system sprouts a second (ratoon) crop, saving seed and labor costs.</p>
      </div>
      <div class="step-card">
        <span class="step-num">03</span>
        <h3 style="color:#fff; margin-bottom: 0.5rem;">Rapid Crushing</h3>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Canes must reach mills within <strong>24–48 hours</strong>; delay leads to rapid sucrose inversion into glucose.</p>
      </div>
      <div class="step-card">
        <span class="step-num">04</span>
        <h3 style="color:#fff; margin-bottom: 0.5rem;">Extraction & Boiling</h3>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Juice is clarified with lime, concentrated in vacuum evaporators, and crystallized into white sugar or jaggery.</p>
      </div>
    </div>

    <div class="byproduct-grid">
      <div class="byproduct-card">
        <h4>
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/>
          </svg>
          Molasses
        </h4>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Thick dark residual syrup. Fermented into industrial alcohol, potable rum, and <strong>bioethanol for India's 20% ethanol petrol blending (E20)</strong> mandate.</p>
      </div>

      <div class="byproduct-card">
        <h4>
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M13 2L3 14h9l-1 8 10-12h-9l1-8z"/>
          </svg>
          Bagasse
        </h4>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Dry fibrous residue after juice extraction. Used as captive fuel in sugar mill boilers for <strong>green cogeneration electricity</strong> and eco-friendly paper production.</p>
      </div>

      <div class="byproduct-card">
        <h4>
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M12 3a9 9 0 0 0 9 9 9 9 0 1 1-9-9Z"/>
          </svg>
          Press Mud
        </h4>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Organic filtration residue containing phosphorus and calcium. Restores fertility to fields as compost and yields sugarcane wax for polishes.</p>
      </div>

      <div class="byproduct-card">
        <h4>
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="10"/>
            <path d="M8 14s1.5 2 4 2 4-2 4-2"/>
          </svg>
          Jaggery (Gur) & Khandsari
        </h4>
        <p style="color: var(--text-muted); font-size: 0.9rem;">Traditional cottage sweeteners rich in natural iron, potassium, and mineral salts, widely consumed across rural and semi-urban India.</p>
      </div>
    </div>
  </section>

  <!-- Section 4: Class 10 Revision Quiz -->
  <section id="quiz">
    <div class="section-header">
      <div class="section-eyebrow">TEST YOUR UNDERSTANDING</div>
      <h2 class="section-title">Class 10 Agriculture Quiz</h2>
      <p style="color: var(--text-muted);">Quick check on key points often asked in Social Science exams.</p>
    </div>

    <div class="quiz-box">
      <div class="quiz-question" id="quizQuestion">Loading question...</div>
      <div class="quiz-options" id="quizOptions"></div>
      <div class="quiz-footer">
        <span style="color: var(--text-muted); font-size: 0.85rem;" id="quizCounter">Question 1 of 4</span>
        <button class="next-quiz-btn" id="nextQuizBtn" onclick="nextQuestion()" style="display:none;">Next Question</button>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <p style="font-weight: 600; color: #fff; margin-bottom: 0.5rem;">SACCHARUM EDU &bull; CLASS 10 SOCIAL SCIENCE PROJECT</p>
    <p>Curriculum: Agriculture (Sugarcane) &bull; Designed with UI/UX Carousel Animation &bull; Ready for GitHub Pages</p>
  </footer>

  <script>
    // Data for Sugarcane Varieties
    const varieties = [
      {
        name: "NOBLE CANE",
        botanical: "Saccharum officinarum",
        subtitle: "TROPICAL SWEET GIANT",
        desc: "The true tropical cane possessing thick, soft, juicy stalks with exceptionally high sucrose content. Native to the South Pacific and cultivated extensively in Peninsular India.",
        sucrose: "14% – 17%",
        belt: "Peninsular India (Maha / TN)",
        thickness: "Thick (3.5 – 5 cm)",
        frost: "Vulnerable to Frost",
        yield: "90 – 120 tonnes/ha",
        recovery: "11.5% – 13.0%",
        fibre: "10% – 12% (Soft Cane)",
        origin: "Originated in New Guinea; domesticated thousands of years ago. Spread across India and the Americas as the premier commercial sugar source.",
        class10Note: "Explains why Maharashtra and Tamil Nadu have higher sugar recovery rates and why mills migrated southwards from UP/Bihar."
      },
      {
        name: "NORTH INDIAN CANE",
        botanical: "Saccharum barberi",
        subtitle: "SUBTROPICAL HARDY SPECIES",
        desc: "Adapted to the harsher climate of the Indo-Gangetic plains. Has slender stalks and comparatively lower sugar yield, but offers exceptional resistance to frost, drought, and waterlogging.",
        sucrose: "10% – 12%",
        belt: "Northern Plains (UP / Bihar / Punjab)",
        thickness: "Slender (1.5 – 2.5 cm)",
        frost: "High Frost Tolerance",
        yield: "55 – 70 tonnes/ha",
        recovery: "8.5% – 9.8%",
        fibre: "15% – 17% (Fibrous)",
        origin: "Indigenous to northern India; named after botanist C.A. Barber who systematically cataloged indigenous Indian canes at the Sugarcane Breeding Institute in Coimbatore.",
        class10Note: "Historic mainstay of Uttar Pradesh's sugar belt. Its frost tolerance allowed commercial cultivation despite bitter northern winters."
      },
      {
        name: "CHINESE CANE",
        botanical: "Saccharum sinense",
        subtitle: "HARDY TEMPERATE STRAIN",
        desc: "A vigorously tillering, slender cane cultivated across central and southern China and Northeast India. Highly fibrous with remarkable hardiness against soil salinity.",
        sucrose: "11% – 13%",
        belt: "Northeast India & East Asia",
        thickness: "Slender / Medium (2 cm)",
        frost: "Moderate Tolerance",
        yield: "60 – 75 tonnes/ha",
        recovery: "9.0% – 10.2%",
        fibre: "14% – 16%",
        origin: "Historically cultivated along the Yangtze and Pearl River basins in China; used in early inter-species breeding programs for cold tolerance.",
        class10Note: "Demonstrates how botanical diversity enables sugarcane to grow outside strict tropical rainforest borders."
      },
      {
        name: "WONDER HYBRID Co 0238",
        botanical: "Saccharum Hybrid (Karan 4)",
        subtitle: "INDIA'S REVOLUTIONARY CANE",
        desc: "Developed by ICAR-Sugarcane Breeding Institute Regional Centre (Karnal), this super-variety revolutionized sugar production in North India, doubling sucrose recovery.",
        sucrose: "14.5% – 18%",
        belt: "Entire Northern & Central Belt",
        thickness: "Medium Thick (3 cm)",
        frost: "High Tolerance",
        yield: "80 – 105 tonnes/ha",
        recovery: "11.8% – 12.5%",
        fibre: "12% – 13.5%",
        origin: "Bred by Dr. Bakshi Ram at ICAR-SBI. A milestone in Indian agricultural biotechnology combining northern frost resilience with tropical sucrose density.",
        class10Note: "Often cited in modern agriculture case studies as the primary reason for Uttar Pradesh regaining top position in sugar output."
      },
      {
        name: "WILD KANS CANE",
        botanical: "Saccharum spontaneum",
        subtitle: "THE IMMORTAL ANCESTOR",
        desc: "A wild perennial grass with nearly zero commercial sugar, but immune to red rot disease, pests, and drought. Used as a genetic donor in cane hybridization.",
        sucrose: "2% – 4% (Non-commercial)",
        belt: "Wild riverbeds across India",
        thickness: "Very Thin (<1.5 cm)",
        frost: "Extreme Tolerance",
        yield: "30 – 40 tonnes/ha",
        recovery: "Negligible",
        fibre: "Above 25%",
        origin: "Native across the Indian subcontinent and Himalayas. Used at SBI Coimbatore to create the world's first inter-specific noble x wild hybrids in 1918.",
        class10Note: "Signifies the importance of wild biodiversity in preserving agriculture against climate change and crop epidemics."
      }
    ];

    let currentIndex = 0;

    // Elements
    const titleEl = document.getElementById("varietyTitle");
    const botanicalEl = document.getElementById("varietyBotanical");
    const subtitleEl = document.getElementById("varietySubtitle");
    const descEl = document.getElementById("varietyDesc");
    const sucroseEl = document.getElementById("specSucrose");
    const beltEl = document.getElementById("specBelt");
    const thicknessEl = document.getElementById("specThickness");
    const frostEl = document.getElementById("specFrost");
    const leftFlankName = document.getElementById("leftFlankName");
    const rightFlankName = document.getElementById("rightFlankName");
    const stalkVisual = document.getElementById("stalkVisual");
    const dotsContainer = document.getElementById("dotsContainer");

    // Initialize Dots
    function initDots() {
      dotsContainer.innerHTML = "";
      varieties.forEach((_, idx) => {
        const dot = document.createElement("div");
        dot.className = `dot ${idx === currentIndex ? "active" : ""}`;
        dot.onclick = () => selectVariety(idx);
        dotsContainer.appendChild(dot);
      });
    }

    function renderVariety(index) {
      const v = varieties[index];
      
      stalkVisual.style.transform = "scale(0.85) rotate(-10deg)";
      stalkVisual.style.opacity = "0.3";

      setTimeout(() => {
        titleEl.textContent = v.name;
        botanicalEl.textContent = v.botanical;
        subtitleEl.textContent = v.subtitle;
        descEl.textContent = v.desc;
        sucroseEl.textContent = v.sucrose;
        beltEl.textContent = v.belt;
        thicknessEl.textContent = v.thickness;
        frostEl.textContent = v.frost;

        const prevIdx = (index - 1 + varieties.length) % varieties.length;
        const nextIdx = (index + 1) % varieties.length;
        leftFlankName.textContent = varieties[prevIdx].name;
        rightFlankName.textContent = varieties[nextIdx].name;

        stalkVisual.style.transform = "scale(1) rotate(0deg)";
        stalkVisual.style.opacity = "1";

        initDots();
      }, 200);
    }

    function nextVariety() {
      currentIndex = (currentIndex + 1) % varieties.length;
      renderVariety(currentIndex);
    }

    function prevVariety() {
      currentIndex = (currentIndex - 1 + varieties.length) % varieties.length;
      renderVariety(currentIndex);
    }

    function selectVariety(idx) {
      currentIndex = idx;
      renderVariety(currentIndex);
    }

    // Modal Drawer
    function openDetailsModal() {
      const v = varieties[currentIndex];
      document.getElementById("modalTitle").textContent = v.name;
      document.getElementById("modalBotanical").textContent = v.botanical;
      document.getElementById("modalYield").textContent = v.yield;
      document.getElementById("modalRecovery").textContent = v.recovery;
      document.getElementById("modalFibre").textContent = v.fibre;
      document.getElementById("modalOrigin").textContent = v.origin;
      document.getElementById("modalClass10Note").textContent = v.class10Note;
      document.getElementById("detailsModal").classList.add("active");
    }

    function closeDetailsModal() {
      document.getElementById("detailsModal").classList.remove("active");
    }

    // Pronunciation Speech
    function speakBotanicalName() {
      const v = varieties[currentIndex];
      if ('speechSynthesis' in window) {
        const utterance = new SpeechSynthesisUtterance(v.botanical);
        utterance.rate = 0.85;
        window.speechSynthesis.speak(utterance);
      } else {
        alert(v.botanical);
      }
    }

    // Keyboard navigation
    window.addEventListener("keydown", (e) => {
      if (e.key === "ArrowRight") nextVariety();
      if (e.key === "ArrowLeft") prevVariety();
      if (e.key === "Escape") closeDetailsModal();
    });

    // Quiz Implementation
    const quizData = [
      {
        question: "What is the ideal temperature range required for sugarcane cultivation?",
        options: ["10°C to 15°C", "21°C to 27°C", "35°C to 45°C", "15°C to 18°C"],
        answer: 1,
        explanation: "Sugarcane requires a hot and humid climate with a temperature of 21°C to 27°C."
      },
      {
        question: "Why is the sugar industry increasingly shifting towards Peninsular India (South)?",
        options: [
          "Labor is much cheaper than in Uttar Pradesh",
          "Maritime climate offers frost-free days, higher sucrose, and a longer crushing season",
          "There is no canal irrigation in North India",
          "Sugarcane cannot grow in alluvial soil"
        ],
        answer: 1,
        explanation: "Peninsular India's tropical maritime climate prevents frost, offers higher sucrose recovery, and extends the crushing season to 7-8 months."
      },
      {
        question: "Why must freshly harvested sugarcane stalks be crushed within 24 to 48 hours?",
        options: [
          "To stop roots from sprouting in storage",
          "To prevent sucrose from inverting into glucose and fructose, which decreases sugar yield",
          "To avoid bacterial fungal rot in transport trucks",
          "To reduce the weight of bagasse"
        ],
        answer: 1,
        explanation: "Delays in crushing cause sucrose inversion, drastically reducing crystal sugar recovery."
      },
      {
        question: "What is 'Bagasse' primarily utilized for in modern sugar mills?",
        options: [
          "Direct chemical fertilizer in wheat fields",
          "Captive boiler biofuel for electricity cogeneration and eco-paper production",
          "Distillation into edible vinegar",
          "Animal feed for sheep"
        ],
        answer: 1,
        explanation: "Bagasse is burned in boilers for green cogeneration power and used as raw pulp for paper."
      }
    ];

    let currentQ = 0;
    let score = 0;

    function loadQuiz() {
      const q = quizData[currentQ];
      document.getElementById("quizQuestion").textContent = `${currentQ + 1}.${q.question}`;
      document.getElementById("quizCounter").textContent = `Question ${currentQ + 1} of${quizData.length}`;
      const optsContainer = document.getElementById("quizOptions");
      optsContainer.innerHTML = "";
      document.getElementById("nextQuizBtn").style.display = "none";

      q.options.forEach((opt, idx) => {
        const btn = document.createElement("button");
        btn.className = "option-btn";
        btn.textContent = opt;
        btn.onclick = () => checkAnswer(idx, btn);
        optsContainer.appendChild(btn);
      });
    }

    function checkAnswer(selectedIdx, btnElement) {
      const q = quizData[currentQ];
      const allBtns = document.querySelectorAll(".option-btn");
      allBtns.forEach(b => b.style.pointerEvents = "none");

      if (selectedIdx === q.answer) {
        btnElement.classList.add("correct");
        score++;
      } else {
        btnElement.classList.add("wrong");
        allBtns[q.answer].classList.add("correct");
      }

      document.getElementById("nextQuizBtn").style.display = "inline-block";
    }

    function nextQuestion() {
      currentQ++;
      if (currentQ < quizData.length) {
        loadQuiz();
      } else {
        showResults();
      }
    }

    function showResults() {
      document.getElementById("quizQuestion").textContent = `Quiz Completed! Your Score: ${score} /${quizData.length}`;
      document.getElementById("quizOptions").innerHTML = `
        <p style="color: var(--cane-glow); font-size: 1.1rem; padding: 1rem 0;">
          ${score === quizData.length ? "Outstanding! You have mastered the Class 10 Sugarcane Agriculture topic." : "Good effort! Review the North vs South comparison and climatic criteria sections above for full marks."}
        </p>
      `;
      document.getElementById("quizCounter").textContent = "Completed";
      const nextBtn = document.getElementById("nextQuizBtn");
      nextBtn.textContent = "Restart Quiz";
      nextBtn.onclick = () => {
        currentQ = 0;
        score = 0;
        nextBtn.textContent = "Next Question";
        loadQuiz();
      };
      nextBtn.style.display = "inline-block";
    }

    // Initialize Page
    initDots();
    renderVariety(0);
    loadQuiz();
  </script>
</body>
</html>
