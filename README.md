<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Besties Scoops — No Lovebirds Allowed 🍦</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  /* ===== TOKENS ===== */
  :root {
    --pink:    #FF6EB4;
    --coral:   #FF4C6A;
    --mint:    #3DDBB8;
    --sky:     #5BC8F5;
    --cream:   #FFF5E6;
    --vanilla: #FFE0B5;
    --choco:   #3B2A1A;
    --purple:  #C47FFF;
    --yellow:  #FFD43B;
    --white:   #FFFFFF;
    --radius:  20px;
    --shadow:  0 6px 24px rgba(59,42,26,.13);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--cream);
    font-family: 'Nunito', sans-serif;
    color: var(--choco);
    overflow-x: hidden;
  }

  /* ===== GATE OVERLAY ===== */
  #gate {
    position: fixed; inset: 0;
    background: linear-gradient(135deg, #FF6EB4 0%, #C47FFF 50%, #5BC8F5 100%);
    display: flex; align-items: center; justify-content: center;
    z-index: 9999;
    padding: 20px;
  }
  .gate-box {
    background: var(--white);
    border-radius: 32px;
    padding: 48px 40px;
    max-width: 480px;
    width: 100%;
    text-align: center;
    box-shadow: 0 20px 60px rgba(0,0,0,.25);
    animation: popIn .5s cubic-bezier(.34,1.56,.64,1) both;
  }
  @keyframes popIn {
    from { transform: scale(.6); opacity: 0; }
    to   { transform: scale(1);  opacity: 1; }
  }
  .gate-emoji { font-size: 72px; line-height: 1; display: block; margin-bottom: 16px; }
  .gate-box h1 {
    font-family: 'Fredoka One', cursive;
    font-size: 2rem;
    color: var(--coral);
    margin-bottom: 8px;
  }
  .gate-box p {
    font-size: 1rem;
    color: #666;
    margin-bottom: 28px;
    line-height: 1.6;
  }
  .gate-question {
    font-family: 'Fredoka One', cursive;
    font-size: 1.3rem;
    color: var(--choco);
    margin-bottom: 20px;
  }
  .gate-btns { display: flex; gap: 14px; justify-content: center; flex-wrap: wrap; }
  .btn-yes, .btn-no {
    padding: 14px 32px;
    border-radius: 50px;
    border: none;
    font-family: 'Fredoka One', cursive;
    font-size: 1.1rem;
    cursor: pointer;
    transition: transform .15s, box-shadow .15s;
  }
  .btn-yes {
    background: var(--mint);
    color: var(--white);
    box-shadow: 0 4px 16px rgba(61,219,184,.4);
  }
  .btn-no {
    background: var(--coral);
    color: var(--white);
    box-shadow: 0 4px 16px rgba(255,76,106,.4);
  }
  .btn-yes:hover { transform: translateY(-3px); box-shadow: 0 8px 24px rgba(61,219,184,.5); }
  .btn-no:hover  { transform: translateY(-3px); box-shadow: 0 8px 24px rgba(255,76,106,.5); }

  /* ===== REJECTED SCREEN ===== */
  #rejected {
    position: fixed; inset: 0;
    background: linear-gradient(135deg, #FF4C6A 0%, #FF6EB4 100%);
    display: none; align-items: center; justify-content: center;
    z-index: 9998;
    padding: 20px;
  }
  .rejected-box {
    background: var(--white);
    border-radius: 32px;
    padding: 48px 40px;
    max-width: 480px;
    width: 100%;
    text-align: center;
    box-shadow: 0 20px 60px rgba(0,0,0,.25);
    animation: shake .4s ease both;
  }
  @keyframes shake {
    0%,100% { transform: translateX(0); }
    20%      { transform: translateX(-12px); }
    40%      { transform: translateX(12px); }
    60%      { transform: translateX(-8px); }
    80%      { transform: translateX(8px); }
  }
  .rejected-box h2 {
    font-family: 'Fredoka One', cursive;
    font-size: 2.2rem;
    color: var(--coral);
    margin: 16px 0 12px;
  }
  .rejected-box p {
    font-size: 1rem; color: #666; line-height: 1.6; margin-bottom: 24px;
  }
  .btn-retry {
    padding: 14px 36px;
    background: var(--sky);
    color: var(--white);
    border: none;
    border-radius: 50px;
    font-family: 'Fredoka One', cursive;
    font-size: 1.1rem;
    cursor: pointer;
    transition: transform .15s;
  }
  .btn-retry:hover { transform: translateY(-3px); }

  /* ===== MAIN SITE ===== */
  #site { display: none; }

  /* NAV */
  nav {
    background: var(--white);
    padding: 16px 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 2px 12px rgba(0,0,0,.07);
    position: sticky; top: 0; z-index: 100;
  }
  .logo {
    font-family: 'Fredoka One', cursive;
    font-size: 1.7rem;
    color: var(--coral);
    text-decoration: none;
  }
  .logo span { color: var(--mint); }
  .nav-links { display: flex; gap: 28px; list-style: none; }
  .nav-links a {
    text-decoration: none;
    font-weight: 700;
    color: var(--choco);
    font-size: .95rem;
    transition: color .2s;
  }
  .nav-links a:hover { color: var(--coral); }
  .no-couples-badge {
    background: var(--coral);
    color: var(--white);
    font-family: 'Fredoka One', cursive;
    font-size: .85rem;
    padding: 6px 16px;
    border-radius: 50px;
  }

  /* HERO */
  .hero {
    background: linear-gradient(160deg, #FF6EB4 0%, #C47FFF 60%, #5BC8F5 100%);
    padding: 80px 40px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '🍦🍧🍨🍡🧁🍦🍧🍨🍡🧁🍦🍧🍨🍡🧁';
    position: absolute; top: -10px; left: 0; right: 0;
    font-size: 2rem; letter-spacing: 8px; opacity: .18;
    white-space: nowrap; overflow: hidden;
  }
  .hero-eyebrow {
    display: inline-block;
    background: var(--yellow);
    color: var(--choco);
    font-family: 'Fredoka One', cursive;
    font-size: .9rem;
    padding: 6px 20px;
    border-radius: 50px;
    margin-bottom: 24px;
    letter-spacing: .5px;
  }
  .hero h1 {
    font-family: 'Fredoka One', cursive;
    font-size: clamp(2.6rem, 6vw, 4.5rem);
    color: var(--white);
    line-height: 1.1;
    margin-bottom: 20px;
    text-shadow: 0 4px 16px rgba(0,0,0,.15);
  }
  .hero h1 .strike {
    text-decoration: line-through;
    color: var(--yellow);
  }
  .hero p {
    font-size: 1.2rem;
    color: rgba(255,255,255,.9);
    max-width: 560px;
    margin: 0 auto 36px;
    line-height: 1.6;
  }
  .hero-cta {
    display: inline-block;
    background: var(--white);
    color: var(--coral);
    font-family: 'Fredoka One', cursive;
    font-size: 1.2rem;
    padding: 16px 48px;
    border-radius: 50px;
    text-decoration: none;
    box-shadow: 0 8px 28px rgba(0,0,0,.2);
    transition: transform .2s, box-shadow .2s;
  }
  .hero-cta:hover { transform: translateY(-4px); box-shadow: 0 14px 36px rgba(0,0,0,.25); }
  .hero-floats {
    display: flex; justify-content: center; gap: 20px;
    margin-top: 48px; font-size: 3.5rem;
    animation: float 3s ease-in-out infinite alternate;
  }
  .hero-floats span:nth-child(2) { animation-delay: .3s; }
  .hero-floats span:nth-child(3) { animation-delay: .6s; }
  @keyframes float {
    from { transform: translateY(0); }
    to   { transform: translateY(-12px); }
  }

  /* RULES BANNER */
  .rules-banner {
    background: var(--coral);
    padding: 18px 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 32px;
    flex-wrap: wrap;
  }
  .rule-pill {
    background: rgba(255,255,255,.18);
    color: var(--white);
    font-family: 'Fredoka One', cursive;
    font-size: 1rem;
    padding: 8px 22px;
    border-radius: 50px;
    display: flex; align-items: center; gap: 8px;
  }

  /* SECTION TITLE */
  .section-title {
    font-family: 'Fredoka One', cursive;
    font-size: 2.2rem;
    color: var(--choco);
    text-align: center;
    margin-bottom: 8px;
  }
  .section-sub {
    text-align: center;
    color: #888;
    font-size: 1rem;
    margin-bottom: 48px;
  }
  section { padding: 72px 40px; max-width: 1100px; margin: 0 auto; }

  /* MENU CARDS */
  .menu-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 24px;
  }
  .menu-card {
    background: var(--white);
    border-radius: var(--radius);
    padding: 28px 24px;
    text-align: center;
    box-shadow: var(--shadow);
    transition: transform .2s, box-shadow .2s;
    position: relative;
    overflow: hidden;
  }
  .menu-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 5px;
    border-radius: 0 0 var(--radius) var(--radius);
  }
  .menu-card.pink::after   { background: var(--pink); }
  .menu-card.mint::after   { background: var(--mint); }
  .menu-card.sky::after    { background: var(--sky); }
  .menu-card.purple::after { background: var(--purple); }
  .menu-card.yellow::after { background: var(--yellow); }
  .menu-card.coral::after  { background: var(--coral); }
  .menu-card:hover { transform: translateY(-8px); box-shadow: 0 16px 40px rgba(59,42,26,.18); }
  .card-emoji { font-size: 52px; display: block; margin-bottom: 14px; }
  .card-name {
    font-family: 'Fredoka One', cursive;
    font-size: 1.3rem;
    color: var(--choco);
    margin-bottom: 8px;
  }
  .card-desc { font-size: .9rem; color: #888; line-height: 1.5; margin-bottom: 16px; }
  .card-price {
    font-family: 'Fredoka One', cursive;
    font-size: 1.4rem;
    color: var(--coral);
  }
  .bestseller-tag {
    position: absolute; top: 16px; right: 16px;
    background: var(--yellow);
    color: var(--choco);
    font-family: 'Fredoka One', cursive;
    font-size: .7rem;
    padding: 4px 10px;
    border-radius: 50px;
  }

  /* RULES SECTION */
  .rules-section {
    background: linear-gradient(135deg, var(--vanilla) 0%, #FFD6E7 100%);
    border-radius: 32px;
    padding: 56px 48px;
    margin: 0 40px;
    max-width: 1020px;
    margin-left: auto; margin-right: auto;
  }
  .rules-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 20px;
    margin-top: 36px;
  }
  .rule-card {
    background: var(--white);
    border-radius: 18px;
    padding: 24px 20px;
    text-align: center;
    box-shadow: 0 4px 16px rgba(0,0,0,.07);
  }
  .rule-card .rule-icon { font-size: 36px; display: block; margin-bottom: 10px; }
  .rule-card h3 {
    font-family: 'Fredoka One', cursive;
    font-size: 1.1rem;
    margin-bottom: 6px;
    color: var(--choco);
  }
  .rule-card p { font-size: .85rem; color: #888; line-height: 1.5; }

  /* VIBES / GALLERY */
  .vibes-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
  }
  .vibe-tile {
    border-radius: 20px;
    padding: 32px 20px;
    text-align: center;
    color: var(--white);
  }
  .vibe-tile:nth-child(1) { background: linear-gradient(135deg, var(--pink), var(--purple)); }
  .vibe-tile:nth-child(2) { background: linear-gradient(135deg, var(--mint), var(--sky)); grid-row: span 2; display: flex; flex-direction: column; justify-content: center; }
  .vibe-tile:nth-child(3) { background: linear-gradient(135deg, var(--yellow), var(--coral)); }
  .vibe-tile:nth-child(4) { background: linear-gradient(135deg, var(--sky), var(--purple)); }
  .vibe-tile:nth-child(5) { background: linear-gradient(135deg, var(--coral), var(--pink)); grid-column: span 2; }
  .vibe-tile .vibe-emoji { font-size: 48px; display: block; margin-bottom: 12px; }
  .vibe-tile h3 { font-family: 'Fredoka One', cursive; font-size: 1.4rem; margin-bottom: 6px; }
  .vibe-tile p { font-size: .9rem; opacity: .85; line-height: 1.4; }

  /* TESTIMONIALS */
  .testi-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
  }
  .testi-card {
    background: var(--white);
    border-radius: 20px;
    padding: 28px;
    box-shadow: var(--shadow);
  }
  .testi-stars { color: var(--yellow); font-size: 1.1rem; margin-bottom: 12px; }
  .testi-text { font-size: .95rem; line-height: 1.6; color: #555; margin-bottom: 16px; }
  .testi-author {
    display: flex; align-items: center; gap: 12px;
  }
  .testi-avatar {
    width: 40px; height: 40px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem;
    flex-shrink: 0;
  }
  .testi-name { font-weight: 800; font-size: .9rem; color: var(--choco); }
  .testi-tag  { font-size: .8rem; color: var(--mint); font-weight: 700; }

  /* FOOTER */
  footer {
    background: var(--choco);
    color: rgba(255,255,255,.7);
    padding: 48px 40px;
    text-align: center;
  }
  footer .footer-logo {
    font-family: 'Fredoka One', cursive;
    font-size: 2rem;
    color: var(--white);
    margin-bottom: 12px;
    display: block;
  }
  footer p { font-size: .9rem; margin-bottom: 8px; line-height: 1.6; }
  .footer-rule {
    display: inline-block;
    background: var(--coral);
    color: var(--white);
    font-family: 'Fredoka One', cursive;
    font-size: .85rem;
    padding: 6px 18px;
    border-radius: 50px;
    margin-top: 16px;
  }

  /* RESPONSIVE */
  @media (max-width: 700px) {
    nav { padding: 14px 20px; }
    .nav-links { display: none; }
    .hero { padding: 56px 20px; }
    section { padding: 48px 20px; }
    .rules-section { margin: 0 16px; padding: 36px 24px; }
    .vibes-grid { grid-template-columns: 1fr 1fr; }
    .vibe-tile:nth-child(2) { grid-row: auto; }
    .vibe-tile:nth-child(5) { grid-column: auto; }
    footer { padding: 36px 20px; }
  }

  /* SCROLL FADE IN */
  .fade-in { opacity: 0; transform: translateY(24px); transition: opacity .5s ease, transform .5s ease; }
  .fade-in.visible { opacity: 1; transform: translateY(0); }
</style>
</head>
<body>

<!-- ===== GATE ===== -->
<div id="gate">
  <div class="gate-box">
    <span class="gate-emoji">🍦</span>
    <h1>Besties Scoops</h1>
    <p>The world's most exclusive ice cream shop — for friends only. No lovebirds. No exceptions.</p>
    <div class="gate-question">Quick question before you enter 👀</div>
    <p style="font-size:1.1rem; font-weight:800; color:#333; margin-bottom:20px;">Are you here with a romantic partner?</p>
    <div class="gate-btns">
      <button class="btn-no"  onclick="enterSite()">Nope! Just friends 🤝</button>
      <button class="btn-yes" onclick="rejectUser()">Yes, it's a date 💑</button>
    </div>
  </div>
</div>

<!-- ===== REJECTED ===== -->
<div id="rejected">
  <div class="rejected-box">
    <span style="font-size:72px; display:block;">🚫💑</span>
    <h2>ABSOLUTELY NOT.</h2>
    <p>We love love… just not in our shop. Come back with your friends, your dog, your mum — anyone who is NOT your significant other.</p>
    <p style="font-size: .85rem; color: #aaa; margin-bottom: 20px;">No kissy faces. No hand-holding. No staring into each other's eyes over a scoop of strawberry.</p>
    <button class="btn-retry" onclick="resetGate()">← Go back (and dump them) 💀</button>
  </div>
</div>

<!-- ===== SITE ===== -->
<div id="site">

  <!-- NAV -->
  <nav>
    <a href="#" class="logo">Besties <span>Scoops</span> 🍦</a>
    <ul class="nav-links">
      <li><a href="#menu">Menu</a></li>
      <li><a href="#rules">The Rules</a></li>
      <li><a href="#vibes">Vibes</a></li>
      <li><a href="#reviews">Reviews</a></li>
    </ul>
    <div class="no-couples-badge">🚫 No Couples</div>
  </nav>

  <!-- HERO -->
  <div class="hero">
    <div class="hero-eyebrow">Est. 2024 — Friends Only Since Day One</div>
    <h1>Ice Cream for Your<br>Besties, Not Your <span class="strike">Boo</span></h1>
    <p>A safe space for squad hangouts, post-breakup healing scoops, and anyone who refuses to share their cone with a romantic partner.</p>
    <a href="#menu" class="hero-cta">See the Menu 👇</a>
    <div class="hero-floats">
      <span>🍦</span><span>🍧</span><span>🍨</span>
    </div>
  </div>

  <!-- RULES BANNER -->
  <div class="rules-banner">
    <div class="rule-pill">🚫 No Couples</div>
    <div class="rule-pill">✅ Solo & Squad Welcome</div>
    <div class="rule-pill">🤝 Friendship Goals Only</div>
    <div class="rule-pill">💅 Single? Extra Sprinkles</div>
  </div>

  <!-- MENU -->
  <section id="menu">
    <h2 class="section-title fade-in">The Bestie Menu 🍨</h2>
    <p class="section-sub fade-in">Sharing is optional. Judging is not.</p>
    <div class="menu-grid">

      <div class="menu-card pink fade-in">
        <div class="bestseller-tag">⭐ Bestseller</div>
        <span class="card-emoji">🍦</span>
        <div class="card-name">Single & Thriving Swirl</div>
        <div class="card-desc">Vanilla & strawberry soft serve, rainbow sprinkles, pride wafer cone</div>
        <div class="card-price">$4.50</div>
      </div>

      <div class="menu-card mint fade-in">
        <span class="card-emoji">🍧</span>
        <div class="card-name">Squad Goals Sorbet</div>
        <div class="card-desc">Mango + passion fruit + lychee trio — one for each bestie in the group</div>
        <div class="card-price">$5.50</div>
      </div>

      <div class="menu-card sky fade-in">
        <span class="card-emoji">🧁</span>
        <div class="card-name">No-Drama Sundae</div>
        <div class="card-desc">3-scoop vanilla, hot fudge, whipped cream, zero emotional baggage</div>
        <div class="card-price">$7.00</div>
      </div>

      <div class="menu-card purple fade-in">
        <div class="bestseller-tag">🔥 Hot</div>
        <span class="card-emoji">🍡</span>
        <div class="card-name">Ex Who? Mochi</div>
        <div class="card-desc">Matcha, taro & ube mochi — best eaten while absolutely not texting your ex</div>
        <div class="card-price">$6.00</div>
      </div>

      <div class="menu-card yellow fade-in">
        <span class="card-emoji">🍨</span>
        <div class="card-name">Chaos Cone Classic</div>
        <div class="card-desc">Pick any 3 flavours that should never go together. Go for it.</div>
        <div class="card-price">$5.00</div>
      </div>

      <div class="menu-card coral fade-in">
        <span class="card-emoji">🫙</span>
        <div class="card-name">Situationship Scoop</div>
        <div class="card-desc">Half chocolate, half vanilla — just like your complicated feelings. Only served to singles.</div>
        <div class="card-price">$4.00</div>
      </div>

    </div>
  </section>

  <!-- THE RULES -->
  <div id="rules" style="padding: 0 0 72px 0;">
    <div class="rules-section fade-in">
      <h2 class="section-title" style="margin-bottom:4px;">The Official Rules 📜</h2>
      <p class="section-sub" style="margin-bottom:0;">We're serious. Well, mostly.</p>
      <div class="rules-grid">
        <div class="rule-card">
          <span class="rule-icon">🚫</span>
          <h3>No Couples</h3>
          <p>Romantic partners are not welcome. Break up outside, then come in.</p>
        </div>
        <div class="rule-card">
          <span class="rule-icon">🤝</span>
          <h3>Friends First</h3>
          <p>Bring your bestie, your crew, or your dog. All are warmly accepted.</p>
        </div>
        <div class="rule-card">
          <span class="rule-icon">🍦</span>
          <h3>Cone Sharing = Crime</h3>
          <p>Everyone gets their own. No reaching for someone else's scoop.</p>
        </div>
        <div class="rule-card">
          <span class="rule-icon">💅</span>
          <h3>Bonus Sprinkles</h3>
          <p>Come in freshly single? Free extra sprinkles. Show us the deleted texts.</p>
        </div>
        <div class="rule-card">
          <span class="rule-icon">🎶</span>
          <h3>Bop-Only Playlist</h3>
          <p>Zero slow songs. Zero. We will not be held responsible for accidental romance.</p>
        </div>
        <div class="rule-card">
          <span class="rule-icon">📸</span>
          <h3>No Couple Photos</h3>
          <p>Group selfies: absolutely. Matching profile photos with bae: take it outside.</p>
        </div>
      </div>
    </div>
  </div>

  <!-- VIBES -->
  <section id="vibes">
    <h2 class="section-title fade-in">The Vibe 🎪</h2>
    <p class="section-sub fade-in">What you can expect when you walk through our (couples-free) door</p>
    <div class="vibes-grid">
      <div class="vibe-tile fade-in">
        <span class="vibe-emoji">🎵</span>
        <h3>Hype Playlist</h3>
        <p>All bops. No ballads. Taylor Swift's angry era only.</p>
      </div>
      <div class="vibe-tile fade-in">
        <span class="vibe-emoji">🌈</span>
        <h3>Chaotic Decor</h3>
        <p>Pink walls, neon signs, bean bags, and 47 flavours of chaos. Welcome home.</p>
      </div>
      <div class="vibe-tile fade-in">
        <span class="vibe-emoji">🛋️</span>
        <h3>Cosy Corners</h3>
        <p>Booths built for 3+ people. No intimate two-seaters anywhere in sight.</p>
      </div>
      <div class="vibe-tile fade-in">
        <span class="vibe-emoji">🎮</span>
        <h3>Games & Giggles</h3>
        <p>Uno, arcade, trivia — because real besties fight over cards, not feelings.</p>
      </div>
      <div class="vibe-tile fade-in">
        <span class="vibe-emoji">✨</span>
        <h3>Zero Romantic Energy</h3>
        <p>Candlelit tables? Never heard of them. We have fairy lights and loud laughter instead.</p>
      </div>
    </div>
  </section>

  <!-- REVIEWS -->
  <section id="reviews" style="background: var(--vanilla); border-radius: 32px; margin: 0 40px 72px; max-width: 1020px; margin-left: auto; margin-right: auto; padding: 56px 48px;">
    <h2 class="section-title fade-in">What Besties Say 💬</h2>
    <p class="section-sub fade-in">Real reviews. No couple wrote these. We checked.</p>
    <div class="testi-grid">
      <div class="testi-card fade-in">
        <div class="testi-stars">★★★★★</div>
        <div class="testi-text">"Came in the day after my breakup with my three besties. Got the Situationship Scoop and cried happy tears. 11/10."</div>
        <div class="testi-author">
          <div class="testi-avatar" style="background: #FFD6E7;">😂</div>
          <div>
            <div class="testi-name">Maya & The Girls</div>
            <div class="testi-tag">Certified Besties ✅</div>
          </div>
        </div>
      </div>
      <div class="testi-card fade-in">
        <div class="testi-stars">★★★★★</div>
        <div class="testi-text">"They actually gave me free sprinkles when I told them I'd just unmatched 47 people on Hinge. Iconic service."</div>
        <div class="testi-author">
          <div class="testi-avatar" style="background: #D6F5EC;">🧃</div>
          <div>
            <div class="testi-name">Jake (Solo Visit)</div>
            <div class="testi-tag">Happily Single 🎉</div>
          </div>
        </div>
      </div>
      <div class="testi-card fade-in">
        <div class="testi-stars">★★★★★</div>
        <div class="testi-text">"Tried to bring my boyfriend. They said no. Dumped him in the car park and came in with my mum. Best decision of my life."</div>
        <div class="testi-author">
          <div class="testi-avatar" style="background: #E0CFFF;">💅</div>
          <div>
            <div class="testi-name">Priya & Mum</div>
            <div class="testi-tag">Mother-Daughter Goals 💜</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <span class="footer-logo">Besties Scoops 🍦</span>
    <p>42 Friend Zone Avenue, No Couples Allowed District</p>
    <p>Open daily 10am – 10pm · Singles & squads only · Dogs welcome</p>
    <div class="footer-rule">🚫 No lovebirds. Ever. Go date somewhere else.</div>
  </footer>

</div><!-- end #site -->

<script>
  function enterSite() {
    document.getElementById('gate').style.display = 'none';
    document.getElementById('site').style.display = 'block';
    initScrollFade();
  }

  function rejectUser() {
    document.getElementById('gate').style.display = 'none';
    const rej = document.getElementById('rejected');
    rej.style.display = 'flex';
  }

  function resetGate() {
    document.getElementById('rejected').style.display = 'none';
    document.getElementById('gate').style.display = 'flex';
  }

  function initScrollFade() {
    const els = document.querySelectorAll('.fade-in');
    const obs = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          obs.unobserve(e.target);
        }
      });
    }, { threshold: 0.12 });
    els.forEach(el => obs.observe(el));
  }

  // Smooth scroll for nav links
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth' }); }
    });
  });
</script>
</body>
</html>

