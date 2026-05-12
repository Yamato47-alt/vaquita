<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Una preguntita importante 🐄</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Nunito:wght@400;700;900&display=swap');

  :root {
    --green-grass: #5d9e3a;
    --green-dark: #3a7a1e;
    --sky: #a8d8f0;
    --cow-black: #2a2a2a;
    --dirt: #8b6340;
    --dirt-dark: #6b4a28;
    --yes-green: #4caf50;
    --yes-dark: #388e3c;
    --no-red: #f44336;
    --no-dark: #c62828;
    --heart: #ff4d6d;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--sky);
    font-family: 'Nunito', sans-serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    position: relative;
  }

  /* Clouds */
  .cloud { position: absolute; background: white; opacity: 0.9; image-rendering: pixelated; }
  .cloud::before, .cloud::after { content: ''; position: absolute; background: white; }
  .cloud1 { width: 80px; height: 24px; top: 8%; left: 10%; animation: floatCloud 18s linear infinite; }
  .cloud1::before { width: 40px; height: 24px; top: -16px; left: 8px; }
  .cloud1::after  { width: 24px; height: 16px; top: -8px; right: 8px; }
  .cloud2 { width: 64px; height: 20px; top: 15%; right: 15%; animation: floatCloud 24s linear infinite reverse; }
  .cloud2::before { width: 32px; height: 20px; top: -14px; left: 6px; }
  .cloud2::after  { width: 20px; height: 12px; top: -6px; right: 6px; }
  .cloud3 { width: 96px; height: 28px; top: 5%; left: 50%; animation: floatCloud 20s linear infinite; animation-delay: -8s; }
  .cloud3::before { width: 48px; height: 28px; top: -20px; left: 12px; }
  .cloud3::after  { width: 28px; height: 18px; top: -10px; right: 10px; }
  @keyframes floatCloud { from { transform: translateX(-200px); } to { transform: translateX(110vw); } }

  /* Ground */
  .ground { position: fixed; bottom: 0; left: 0; width: 100%; height: 80px; background: var(--green-grass); border-top: 8px solid var(--green-dark); z-index: 0; }
  .ground::before { content: ''; position: absolute; top: 8px; left: 0; width: 100%; height: 24px; background: var(--dirt); border-bottom: 4px solid var(--dirt-dark); }

  /* Card */
  .card {
    position: relative;
    z-index: 10;
    background: rgba(255,255,255,0.92);
    border: 6px solid var(--cow-black);
    box-shadow: 8px 8px 0 var(--cow-black);
    padding: 36px 40px 32px;
    max-width: 480px;
    width: 92vw;
    text-align: center;
    animation: popIn 0.6s cubic-bezier(0.34,1.56,0.64,1) both;
  }
  @keyframes popIn {
    from { transform: scale(0.5) translateY(60px); opacity: 0; }
    to   { transform: scale(1) translateY(0); opacity: 1; }
  }

  /* Cow */
  .cow-wrapper {
    display: flex;
    justify-content: center;
    margin-bottom: 18px;
    animation: cowBounce 1.8s ease-in-out infinite;
  }
  @keyframes cowBounce { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
  .pixel-cow { width: 160px; height: 160px; image-rendering: pixelated; }

  /* Title */
  .title {
    font-family: 'Press Start 2P', monospace;
    font-size: 11px;
    color: var(--cow-black);
    line-height: 1.8;
    margin-bottom: 14px;
  }

  /* Message */
  .message {
    font-size: 17px;
    font-weight: 700;
    color: #3a3a3a;
    line-height: 1.6;
    margin-bottom: 28px;
    padding: 0 4px;
  }
  .heart { color: var(--heart); display: inline-block; animation: heartbeat 1s ease-in-out infinite; }
  @keyframes heartbeat { 0%,100% { transform: scale(1); } 50% { transform: scale(1.3); } }

  /* Buttons container — relative so No can move inside it */
  .buttons {
    position: relative;
    height: 70px;
    width: 100%;
  }

  .btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 10px;
    padding: 14px 24px;
    border: 4px solid var(--cow-black);
    cursor: pointer;
    box-shadow: 4px 4px 0 var(--cow-black);
    letter-spacing: 0.5px;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    white-space: nowrap;
  }

  /* YES — anchored left-center */
  .btn-yes {
    background: var(--yes-green);
    color: white;
    left: calc(50% - 130px);
  }
  .btn-yes:hover { background: var(--yes-dark); }
  .btn-yes:active { transform: translateY(calc(-50% + 4px)); box-shadow: 0 0 0 var(--cow-black); }

  /* NO — starts right-center, moves on hover */
  .btn-no {
    background: var(--no-red);
    color: white;
    left: calc(50% + 10px);
    transition: left 0.12s ease, top 0.12s ease;
  }
  .btn-no:hover { background: var(--no-dark); }

  /* Success */
  .success { display: none; flex-direction: column; align-items: center; gap: 12px; }
  .success.show { display: flex; }
  .success-text {
    font-family: 'Press Start 2P', monospace;
    font-size: 12px;
    color: var(--yes-dark);
    line-height: 2;
    animation: popIn 0.5s cubic-bezier(0.34,1.56,0.64,1);
  }
  .confetti-row { font-size: 28px; animation: spin 1s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }
  .main-content.hide { display: none; }

  /* Floating hearts */
  .hearts-bg span {
    position: fixed;
    font-size: 20px;
    opacity: 0;
    animation: floatHeart 4s ease-in infinite;
    pointer-events: none;
    z-index: 1;
  }
  @keyframes floatHeart {
    0%   { transform: translateY(0) scale(0.5); opacity: 0.8; }
    100% { transform: translateY(-100vh) scale(1.2); opacity: 0; }
  }
</style>
</head>
<body>

<div class="cloud cloud1"></div>
<div class="cloud cloud2"></div>
<div class="cloud cloud3"></div>
<div class="ground"></div>
<div class="hearts-bg" id="hearts"></div>

<div class="card" id="mainCard">

  <div class="main-content" id="mainContent">

    <div class="cow-wrapper">
      <svg class="pixel-cow" viewBox="0 0 48 48" xmlns="http://www.w3.org/2000/svg" style="image-rendering:pixelated">
        <!-- CUERPO -->
        <rect x="12" y="20" width="24" height="16" fill="#f0ece0"/>
        <rect x="13" y="21" width="6" height="5" fill="#2a2a2a"/>
        <rect x="22" y="23" width="5" height="6" fill="#2a2a2a"/>
        <rect x="14" y="29" width="4" height="4" fill="#2a2a2a"/>
        <rect x="30" y="22" width="4" height="3" fill="#2a2a2a"/>
        <rect x="27" y="32" width="5" height="3" fill="#2a2a2a"/>
        <!-- PATAS delanteras -->
        <rect x="14" y="36" width="5" height="8" fill="#f0ece0"/>
        <rect x="14" y="41" width="5" height="3" fill="#d0cbb8"/>
        <rect x="14" y="43" width="5" height="1" fill="#2a2a2a"/>
        <rect x="21" y="36" width="5" height="8" fill="#f0ece0"/>
        <rect x="21" y="41" width="5" height="3" fill="#d0cbb8"/>
        <rect x="21" y="43" width="5" height="1" fill="#2a2a2a"/>
        <!-- PATAS traseras -->
        <rect x="28" y="36" width="5" height="8" fill="#f0ece0"/>
        <rect x="28" y="41" width="5" height="3" fill="#d0cbb8"/>
        <rect x="28" y="43" width="5" height="1" fill="#2a2a2a"/>
        <rect x="33" y="36" width="5" height="8" fill="#f0ece0"/>
        <rect x="33" y="41" width="5" height="3" fill="#d0cbb8"/>
        <rect x="33" y="43" width="5" height="1" fill="#2a2a2a"/>
        <!-- CABEZA -->
        <rect x="15" y="7" width="16" height="15" fill="#f0ece0"/>
        <rect x="16" y="8" width="5" height="4" fill="#2a2a2a"/>
        <rect x="25" y="11" width="4" height="5" fill="#2a2a2a"/>
        <rect x="17" y="15" width="3" height="3" fill="#2a2a2a"/>
        <!-- OREJAS -->
        <rect x="11" y="9" width="4" height="5" fill="#f0ece0"/>
        <rect x="11" y="10" width="3" height="3" fill="#f4a0b0"/>
        <rect x="31" y="9" width="4" height="5" fill="#f0ece0"/>
        <rect x="32" y="10" width="3" height="3" fill="#f4a0b0"/>
        <!-- CUERNOS -->
        <rect x="18" y="4" width="3" height="4" fill="#c8b460"/>
        <rect x="17" y="3" width="2" height="2" fill="#c8b460"/>
        <rect x="25" y="4" width="3" height="4" fill="#c8b460"/>
        <rect x="27" y="3" width="2" height="2" fill="#c8b460"/>
        <!-- OJOS -->
        <rect x="18" y="14" width="3" height="3" fill="#2a2a2a"/>
        <rect x="25" y="14" width="3" height="3" fill="#2a2a2a"/>
        <rect x="20" y="14" width="1" height="1" fill="white"/>
        <rect x="27" y="14" width="1" height="1" fill="white"/>
        <!-- HOCICO -->
        <rect x="17" y="19" width="12" height="6" fill="#f4b8c0"/>
        <rect x="19" y="21" width="2" height="2" fill="#c06080"/>
        <rect x="25" y="21" width="2" height="2" fill="#c06080"/>
        <rect x="19" y="23" width="1" height="1" fill="#c06080"/>
        <rect x="26" y="23" width="1" height="1" fill="#c06080"/>
        <rect x="20" y="24" width="6" height="1" fill="#c06080"/>
        <!-- CUELLO -->
        <rect x="19" y="17" width="8" height="4" fill="#f0ece0"/>
        <rect x="19" y="17" width="3" height="3" fill="#2a2a2a"/>
        <!-- COLA -->
        <rect x="36" y="20" width="3" height="6" fill="#f0ece0"/>
        <rect x="36" y="26" width="4" height="3" fill="#d0cbb8"/>
        <rect x="36" y="29" width="5" height="2" fill="#2a2a2a"/>
        <!-- UBRE -->
        <rect x="19" y="33" width="9" height="5" fill="#f4b8c0"/>
        <rect x="20" y="37" width="2" height="2" fill="#e08898"/>
        <rect x="23" y="37" width="2" height="2" fill="#e08898"/>
        <rect x="26" y="37" width="2" height="2" fill="#e08898"/>
      </svg>
    </div>

    <div class="title">🌸 Hola, mi amor 🌸</div>

    <div class="message">
      Igual que esta vaquita,<br>
      yo sin vos me siento perdido.<br>
      <span class="heart">♥</span> ¿Me harías el honor de<br>
      salir a una cita conmigo? <span class="heart">♥</span><br>
      <br>
      <span style="font-size:14px;color:#888;">Te prometo que va a ser especial 🌙✨</span>
    </div>

    <div class="buttons" id="btnContainer">
      <button class="btn btn-yes" onclick="yesClicked()">¡SÍ! 🐄💕</button>
      <button class="btn btn-no" id="noBtn" onmouseover="moveNo()" ontouchstart="moveNo(event)">No...</button>
    </div>

  </div>

  <div class="success" id="successScreen">
    <div class="confetti-row">🎉🐄💕🎉</div>
    <div class="success-text">¡SABÍA QUE<br>DIRÍAS QUE SÍ!</div>
    <div style="font-family:'Nunito',sans-serif;font-size:18px;font-weight:900;color:#1a6fad;margin:4px 0 8px;line-height:1.7;animation:popIn 0.6s cubic-bezier(0.34,1.56,0.64,1) 0.3s both;">
      ¡Te invito una salida al pool! 💕<br>
      <span style="font-size:15px;color:#666;">Va a ser el mejor día 🌸</span>
    </div>
    <div style="font-size:32px; animation: cowBounce 1s ease-in-out infinite;">🐄🌸💕</div>
  </div>

</div>

<script>
  // Floating hearts
  const heartsContainer = document.getElementById('hearts');
  const heartEmojis = ['💕','🌸','💖','🐄','✨','💗'];
  for (let i = 0; i < 12; i++) {
    const h = document.createElement('span');
    h.textContent = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
    h.style.left = Math.random() * 100 + 'vw';
    h.style.bottom = '-40px';
    h.style.animationDelay = Math.random() * 6 + 's';
    h.style.animationDuration = (3 + Math.random() * 4) + 's';
    heartsContainer.appendChild(h);
    setInterval(() => { h.style.left = Math.random() * 100 + 'vw'; }, (3 + Math.random() * 4) * 1000);
  }

  // Move No button — stays inside the card, never overlaps the Yes button
  function moveNo(e) {
    if (e && e.cancelable) e.preventDefault();
    const btn = document.getElementById('noBtn');
    const card = document.getElementById('mainCard');
    const cardRect = card.getBoundingClientRect();
    const btnW = btn.offsetWidth;
    const btnH = btn.offsetHeight;

    // Safe area: 12px padding from card edges
    const pad = 12;
    const maxLeft = cardRect.width - btnW - pad;
    const maxTop  = cardRect.height - btnH - pad;

    // Keep away from Yes button zone (left half roughly)
    const minLeft = Math.floor(cardRect.width / 2) - btnW / 2 + 10;

    let newLeft, newTop;
    // Alternate between left and right halves to avoid Yes overlap
    const goLeft = Math.random() < 0.3; // 30% chance left side (but far from Yes center)
    if (goLeft) {
      newLeft = pad + Math.random() * (Math.floor(cardRect.width * 0.35) - pad - btnW);
    } else {
      newLeft = minLeft + Math.random() * (maxLeft - minLeft);
    }
    newTop = pad + Math.random() * (maxTop - pad);

    // Clamp
    newLeft = Math.max(pad, Math.min(newLeft, maxLeft));
    newTop  = Math.max(pad, Math.min(newTop, maxTop));

    btn.style.left = newLeft + 'px';
    btn.style.top  = newTop  + 'px';
    btn.style.transform = 'none';
  }

  function yesClicked() {
    document.getElementById('mainContent').classList.add('hide');
    document.getElementById('successScreen').classList.add('show');
    for (let i = 0; i < 20; i++) {
      const h = document.createElement('span');
      h.textContent = ['💕','🐄','🌸','💖','🎉'][Math.floor(Math.random() * 5)];
      h.style.position = 'fixed';
      h.style.left = Math.random() * 100 + 'vw';
      h.style.bottom = '0';
      h.style.fontSize = (16 + Math.random() * 20) + 'px';
      h.style.opacity = '0';
      h.style.animation = `floatHeart ${1.5 + Math.random() * 2}s ease-in forwards`;
      h.style.animationDelay = Math.random() * 1.5 + 's';
      h.style.zIndex = '999';
      h.style.pointerEvents = 'none';
      document.body.appendChild(h);
    }
  }
</script>
</body>
</html>
