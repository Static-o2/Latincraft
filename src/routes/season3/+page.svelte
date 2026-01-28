<script>
  import { onMount } from 'svelte';
  
  let formUrl = 'https://forms.gle/1E98v6ZpWoKRsv6E8';
  let bgTextElement;
  
  function openForm() {
    window.open(formUrl, '_blank');
  }
  
  onMount(() => {
    // Load confetti library dynamically
    const script = document.createElement('script');
    script.src = 'https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.2/dist/confetti.browser.min.js';
    script.onload = () => {
      startConfetti();
    };
    document.head.appendChild(script);
    
    // Animate background text position
    const bgInterval = setInterval(() => {
      if (bgTextElement) {
        bgTextElement.style.top = Math.random() * 100 + '%';
      }
    }, 5000);
    
    return () => {
      clearInterval(bgInterval);
    };
  });
  
  function startConfetti() {
    setInterval(() => {
      if (window.confetti) {
        window.confetti({
          particleCount: 3,
          angle: 90,
          spread: 45,
          origin: { x: Math.random(), y: 0 },
          colors: ['#ff1493', '#00ff00', '#ffff00', '#ff6600', '#00ffff', '#ff0000', '#9400d3', '#0000ff', '#ff69b4', '#7fff00'],
          gravity: 1,
          scalar: 1.2,
          drift: 0,
          ticks: 300,
          zIndex: 999
        });
      }
    }, 100);
  }
</script>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&family=Permanent+Marker&display=swap" rel="stylesheet">
</svelte:head>

<div class="starfield"></div>
<div class="bg-text" bind:this={bgTextElement}>LATIN CRAFT LATIN CRAFT LATIN CRAFT</div>

<div class="container">
  <div class="header">
    <div class="marquee-container">
      <div class="marquee">★☆★ LIFESTEAL EDITION  ★☆★</div>
    </div>
    
    <h1 class="title">LATIN CRAFT</h1>
    <div class="subtitle">✧･ﾟ: *✧･ﾟ:* SEASON 3 *:･ﾟ✧*:･ﾟ✧</div>
    
    <div class="gifs-container">
      <div class="rotating-gif">⚔️</div>
      <div class="rotating-gif">🎮</div>
      <div class="rotating-gif">💎</div>
      <div class="rotating-gif">🔥</div>
    </div>
  </div>
  
  <div class="button-container">
    <div class="sparkles">
      <div class="sparkle">✨</div>
      <div class="sparkle">✨</div>
      <div class="sparkle">✨</div>
      <div class="sparkle">✨</div>
    </div>
    <button class="submit-button" onclick={openForm}>
      ★ CLICK HERE ★<br>TO SIGN UP!
    </button>
  </div>
  
  <div class="under-construction">
    <span class="construction-icon">🚧</span>
    <span>UNDER CONSTRUCTION</span>
    <span class="construction-icon">🚧</span>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  :global(*) {
    box-sizing: border-box;
  }
  
  :global(body) {
    background: #000;
    overflow-x: hidden;
    cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="20" height="20"><circle cx="10" cy="10" r="8" fill="%23ff00ff"/></svg>'), auto;
  }
  
  .starfield {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: 
      radial-gradient(2px 2px at 20% 30%, white, transparent),
      radial-gradient(2px 2px at 60% 70%, white, transparent),
      radial-gradient(1px 1px at 50% 50%, white, transparent),
      radial-gradient(1px 1px at 80% 10%, white, transparent),
      radial-gradient(2px 2px at 90% 60%, white, transparent),
      radial-gradient(1px 1px at 33% 85%, white, transparent),
      radial-gradient(2px 2px at 75% 25%, white, transparent),
      radial-gradient(1px 1px at 15% 65%, white, transparent);
    background-size: 200% 200%;
    animation: twinkle 4s ease-in-out infinite;
    z-index: 0;
  }
  
  @keyframes twinkle {
    0%, 100% { opacity: 0.3; }
    50% { opacity: 1; }
  }
  
  .container {
    position: relative;
    z-index: 1;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
  }
  
  .header {
    text-align: center;
    margin-bottom: 50px;
    position: relative;
  }
  
  .marquee-container {
    background: linear-gradient(90deg, #ff1493, #00ff00, #ff6600, #ffff00, #ff1493);
    background-size: 200% 100%;
    border: 5px ridge gold;
    padding: 10px;
    margin-bottom: 30px;
    box-shadow: 0 0 20px #ff1493, 0 0 40px #00ff00;
    animation: marquee-shift 3s linear infinite;
    overflow: hidden;
  }
  
  @keyframes marquee-shift {
    0% { background-position: 0% 50%; }
    100% { background-position: 100% 50%; }
  }
  
  .marquee {
    font-family: 'Comic Neue', cursive;
    font-size: 24px;
    font-weight: bold;
    color: #ffff00;
    text-shadow: 
      2px 2px #ff0000,
      -2px -2px #00ff00,
      2px -2px #0000ff,
      -2px 2px #ff00ff;
    letter-spacing: 3px;
    animation: marquee-scroll 15s linear infinite;
    white-space: nowrap;
    display: inline-block;
  }
  
  @keyframes marquee-scroll {
    0% { transform: translateX(100%); }
    100% { transform: translateX(-100%); }
  }
  
  .title {
    font-family: 'Permanent Marker', cursive;
    font-size: clamp(60px, 15vw, 150px);
    background: linear-gradient(45deg, 
      #ff0000, #ff7700, #ffdd00, #00ff00, 
      #0099ff, #6600ff, #ff00ff);
    background-size: 400% 400%;
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: rainbow 3s ease infinite, pulse 1s ease-in-out infinite;
    text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
    letter-spacing: 5px;
    transform: rotate(-2deg);
    margin: 20px 0;
  }
  
  @keyframes rainbow {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  @keyframes pulse {
    0%, 100% { transform: rotate(-2deg) scale(1); }
    50% { transform: rotate(-2deg) scale(1.05); }
  }
  
  .subtitle {
    font-family: 'Comic Neue', cursive;
    font-size: clamp(24px, 5vw, 48px);
    color: #00ffff;
    text-shadow: 
      0 0 10px #00ffff,
      0 0 20px #ff00ff,
      2px 2px 0 #ff0000;
    animation: blink 1s step-start infinite;
    letter-spacing: 2px;
  }
  
  @keyframes blink {
    50% { opacity: 0.5; }
  }
  
  .gifs-container {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 30px 0;
    flex-wrap: wrap;
  }
  
  .rotating-gif {
    width: 100px;
    height: 100px;
    border: 3px solid #ffff00;
    border-radius: 50%;
    animation: spin 2s linear infinite;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 50px;
    box-shadow: 0 0 20px rgba(255, 255, 0, 0.5);
  }
  
  .rotating-gif:nth-child(1) {
    background: linear-gradient(45deg, #ff1493, #ff69b4);
    border-color: #00ff00;
  }
  
  .rotating-gif:nth-child(2) {
    background: linear-gradient(45deg, #00ff00, #7fff00);
    border-color: #ff0000;
  }
  
  .rotating-gif:nth-child(3) {
    background: linear-gradient(45deg, #ff6600, #ffaa00);
    border-color: #0000ff;
  }
  
  .rotating-gif:nth-child(4) {
    background: linear-gradient(45deg, #00ffff, #0099ff);
    border-color: #ff00ff;
  }
  
  @keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  
  .button-container {
    position: relative;
    margin: 40px 0;
  }
  
  .sparkles {
    position: absolute;
    width: 100%;
    height: 100%;
    pointer-events: none;
  }
  
  .sparkle {
    position: absolute;
    font-size: 30px;
    animation: sparkle-float 2s ease-in-out infinite;
  }
  
  .sparkle:nth-child(1) {
    top: -20px;
    left: -20px;
    animation-delay: 0s;
  }
  
  .sparkle:nth-child(2) {
    top: -20px;
    right: -20px;
    animation-delay: 0.5s;
  }
  
  .sparkle:nth-child(3) {
    bottom: -20px;
    left: -20px;
    animation-delay: 1s;
  }
  
  .sparkle:nth-child(4) {
    bottom: -20px;
    right: -20px;
    animation-delay: 1.5s;
  }
  
  @keyframes sparkle-float {
    0%, 100% { transform: translateY(0px) scale(1); opacity: 1; }
    50% { transform: translateY(-10px) scale(1.2); opacity: 0.7; }
  }
  
  .submit-button {
    font-family: 'Comic Neue', cursive;
    font-size: 36px;
    font-weight: bold;
    padding: 20px 60px;
    background: linear-gradient(45deg, #ff0000, #ff00ff, #0000ff, #00ffff, #00ff00, #ffff00, #ff0000);
    background-size: 400% 400%;
    border: 5px outset #ffff00;
    color: #ffffff;
    text-shadow: 
      2px 2px 0 #000000,
      -2px -2px 0 #000000,
      2px -2px 0 #000000,
      -2px 2px 0 #000000;
    cursor: pointer;
    animation: button-rainbow 2s ease infinite, bounce 0.5s ease-in-out infinite;
    box-shadow: 
      0 0 20px #ff00ff,
      0 0 40px #00ffff,
      inset 0 0 10px rgba(255, 255, 255, 0.5);
    transform: rotate(-1deg);
    transition: all 0.3s ease;
  }
  
  @keyframes button-rainbow {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  @keyframes bounce {
    0%, 100% { transform: rotate(-1deg) translateY(0px); }
    50% { transform: rotate(-1deg) translateY(-5px); }
  }
  
  .submit-button:hover {
    transform: rotate(-1deg) scale(1.1);
    border-style: inset;
    animation: button-rainbow 0.5s ease infinite, crazy-bounce 0.2s ease-in-out infinite;
  }
  
  @keyframes crazy-bounce {
    0%, 100% { transform: rotate(-1deg) scale(1.1) translateY(0px); }
    25% { transform: rotate(2deg) scale(1.15) translateY(-8px); }
    75% { transform: rotate(-3deg) scale(1.12) translateY(-4px); }
  }
  
  .submit-button:active {
    transform: rotate(-1deg) scale(0.95);
  }
  
  .under-construction {
    margin-top: 50px;
    display: flex;
    align-items: center;
    gap: 15px;
    font-family: 'Comic Neue', cursive;
    font-size: 24px;
    color: #ffff00;
    text-shadow: 2px 2px #000000;
  }
  
  .construction-icon {
    font-size: 40px;
    animation: swing 1s ease-in-out infinite;
  }
  
  @keyframes swing {
    0%, 100% { transform: rotate(0deg); }
    25% { transform: rotate(10deg); }
    75% { transform: rotate(-10deg); }
  }
  
  .bg-text {
    position: fixed;
    top: 50%;
    left: 0;
    width: 100%;
    font-size: 100px;
    color: rgba(255, 0, 255, 0.1);
    font-family: 'Permanent Marker', cursive;
    white-space: nowrap;
    animation: scroll-left 20s linear infinite;
    z-index: 0;
    pointer-events: none;
  }
  
  @keyframes scroll-left {
    from { transform: translateX(100%); }
    to { transform: translateX(-100%); }
  }
</style>