<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>CSS 动画示例</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      min-height: 100vh;
      background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-family: 'Segoe UI', sans-serif;
      gap: 60px;
      padding: 40px;
    }

    h2 {
      color: #fff;
      font-size: 14px;
      letter-spacing: 2px;
      text-transform: uppercase;
      opacity: 0.6;
      margin-bottom: -40px;
    }

    /* ===== 1. 粒子轨道动画 ===== */
    .orbit-scene {
      position: relative;
      width: 200px;
      height: 200px;
    }

    .orbit-core {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: radial-gradient(circle at 35% 35%, #fff8b0, #ffcc00, #ff6600);
      box-shadow: 0 0 20px #ffcc00, 0 0 60px #ff660088;
      animation: pulse 2s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: translate(-50%, -50%) scale(1); box-shadow: 0 0 20px #ffcc00, 0 0 60px #ff660088; }
      50%       { transform: translate(-50%, -50%) scale(1.15); box-shadow: 0 0 40px #ffcc00, 0 0 100px #ff6600cc; }
    }

    .orbit-ring {
      position: absolute;
      top: 50%;
      left: 50%;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.15);
      transform: translate(-50%, -50%);
    }

    .orbit-ring:nth-child(2) { width: 100px; height: 100px; }
    .orbit-ring:nth-child(3) { width: 150px; height: 150px; }
    .orbit-ring:nth-child(4) { width: 200px; height: 200px; }

    .planet {
      position: absolute;
      border-radius: 50%;
      top: 50%;
      left: 50%;
    }

    .planet-1 {
      width: 12px; height: 12px;
      background: radial-gradient(circle at 35% 35%, #a8edea, #42a5f5);
      box-shadow: 0 0 8px #42a5f5;
      margin: -6px;
      animation: orbit1 3s linear infinite;
      transform-origin: 50px 0;
    }

    .planet-2 {
      width: 10px; height: 10px;
      background: radial-gradient(circle at 35% 35%, #fbc2eb, #f857a6);
      box-shadow: 0 0 8px #f857a6;
      margin: -5px;
      animation: orbit2 5s linear infinite;
      transform-origin: 75px 0;
    }

    .planet-3 {
      width: 8px; height: 8px;
      background: radial-gradient(circle at 35% 35%, #d4fc79, #96e6a1);
      box-shadow: 0 0 8px #96e6a1;
      margin: -4px;
      animation: orbit3 8s linear infinite;
      transform-origin: 100px 0;
    }

    @keyframes orbit1 { from { transform: rotate(0deg)   translateX(50px); } to { transform: rotate(360deg) translateX(50px); } }
    @keyframes orbit2 { from { transform: rotate(120deg) translateX(75px); } to { transform: rotate(480deg) translateX(75px); } }
    @keyframes orbit3 { from { transform: rotate(240deg) translateX(100px); } to { transform: rotate(600deg) translateX(100px); } }

    /* ===== 2. 加载动画 ===== */
    .loader-row {
      display: flex;
      gap: 40px;
      align-items: center;
    }

    /* 波浪点 */
    .wave-dots {
      display: flex;
      gap: 8px;
      align-items: flex-end;
    }

    .wave-dots span {
      display: block;
      width: 12px;
      height: 12px;
      border-radius: 50%;
      background: #7c3aed;
      animation: wave-bounce 1.4s ease-in-out infinite;
    }

    .wave-dots span:nth-child(1) { animation-delay: 0s;    background: #f472b6; }
    .wave-dots span:nth-child(2) { animation-delay: 0.2s;  background: #a78bfa; }
    .wave-dots span:nth-child(3) { animation-delay: 0.4s;  background: #60a5fa; }
    .wave-dots span:nth-child(4) { animation-delay: 0.6s;  background: #34d399; }
    .wave-dots span:nth-child(5) { animation-delay: 0.8s;  background: #fbbf24; }

    @keyframes wave-bounce {
      0%, 100% { transform: translateY(0);   opacity: 0.4; }
      50%       { transform: translateY(-20px); opacity: 1; }
    }

    /* 环形进度 */
    .ring-loader {
      width: 60px;
      height: 60px;
      position: relative;
    }

    .ring-loader svg {
      transform: rotate(-90deg);
      animation: ring-spin 2s linear infinite;
    }

    .ring-loader circle {
      fill: none;
      stroke-width: 5;
      stroke-linecap: round;
      stroke-dasharray: 150;
      stroke-dashoffset: 0;
      animation: ring-dash 2s ease-in-out infinite;
    }

    .ring-loader .c1 { stroke: #f472b6; animation-delay: 0s; }
    .ring-loader .c2 { stroke: #60a5fa; stroke-dasharray: 100; animation-delay: -0.5s; }

    @keyframes ring-spin { to { transform: rotate(270deg); } }
    @keyframes ring-dash {
      0%   { stroke-dashoffset: 150; opacity: 1; }
      50%  { stroke-dashoffset: 30;  opacity: 1; }
      100% { stroke-dashoffset: 150; opacity: 0.2; }
    }

    /* ===== 3. 卡片悬浮动画 ===== */
    .cards-row {
      display: flex;
      gap: 24px;
    }

    .flip-card {
      width: 100px;
      height: 130px;
      perspective: 600px;
      cursor: pointer;
    }

    .flip-card-inner {
      position: relative;
      width: 100%;
      height: 100%;
      transform-style: preserve-3d;
      transition: transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
      animation: auto-flip 4s ease-in-out infinite;
    }

    .flip-card:nth-child(2) .flip-card-inner { animation-delay: 1.3s; }
    .flip-card:nth-child(3) .flip-card-inner { animation-delay: 2.6s; }

    @keyframes auto-flip {
      0%, 40%  { transform: rotateY(0deg); }
      50%, 90% { transform: rotateY(180deg); }
      100%     { transform: rotateY(0deg); }
    }

    .flip-card:hover .flip-card-inner {
      animation-play-state: paused;
      transform: rotateY(180deg);
    }

    .flip-front, .flip-back {
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 16px;
      backface-visibility: hidden;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-size: 13px;
      font-weight: 600;
      color: #fff;
      gap: 10px;
    }

    .flip-front { background: linear-gradient(135deg, #667eea, #764ba2); }
    .flip-back  { background: linear-gradient(135deg, #f093fb, #f5576c); transform: rotateY(180deg); }

    .flip-front .icon, .flip-back .icon { font-size: 36px; }

    /* ===== 4. 文字动画 ===== */
    .text-animate {
      font-size: 32px;
      font-weight: 800;
      letter-spacing: 4px;
      display: flex;
      gap: 2px;
    }

    .text-animate span {
      display: inline-block;
      color: transparent;
      background: linear-gradient(90deg, #f472b6, #a78bfa, #60a5fa, #34d399, #fbbf24);
      background-size: 300%;
      -webkit-background-clip: text;
      background-clip: text;
      animation: text-color 3s linear infinite, text-wave 1.8s ease-in-out infinite;
    }

    .text-animate span:nth-child(1)  { animation-delay: 0s,    0s; }
    .text-animate span:nth-child(2)  { animation-delay: 0.1s,  0.1s; }
    .text-animate span:nth-child(3)  { animation-delay: 0.2s,  0.2s; }
    .text-animate span:nth-child(4)  { animation-delay: 0.3s,  0.3s; }
    .text-animate span:nth-child(5)  { animation-delay: 0.4s,  0.4s; }
    .text-animate span:nth-child(6)  { animation-delay: 0.5s,  0.5s; }
    .text-animate span:nth-child(7)  { animation-delay: 0.6s,  0.6s; }
    .text-animate span:nth-child(8)  { animation-delay: 0.7s,  0.7s; }
    .text-animate span:nth-child(9)  { animation-delay: 0.8s,  0.8s; }
    .text-animate span:nth-child(10) { animation-delay: 0.9s,  0.9s; }

    @keyframes text-color {
      0%   { background-position: 0%; }
      100% { background-position: 300%; }
    }

    @keyframes text-wave {
      0%, 100% { transform: translateY(0); }
      50%       { transform: translateY(-10px); }
    }

    /* ===== 5. 粒子爆炸按钮 ===== */
    .btn-wrap {
      position: relative;
    }

    .magic-btn {
      position: relative;
      padding: 14px 40px;
      border: none;
      border-radius: 50px;
      font-size: 16px;
      font-weight: 700;
      color: #fff;
      cursor: pointer;
      background: linear-gradient(90deg, #6366f1, #8b5cf6, #ec4899);
      background-size: 200%;
      letter-spacing: 2px;
      animation: btn-gradient 3s linear infinite;
      transition: transform 0.2s, box-shadow 0.2s;
      overflow: visible;
    }

    .magic-btn::before {
      content: '';
      position: absolute;
      inset: -3px;
      border-radius: 53px;
      background: linear-gradient(90deg, #6366f1, #ec4899, #6366f1);
      background-size: 200%;
      z-index: -1;
      animation: btn-gradient 3s linear infinite;
      filter: blur(8px);
      opacity: 0.8;
    }

    .magic-btn:hover {
      transform: scale(1.06);
      box-shadow: 0 8px 30px rgba(139, 92, 246, 0.5);
    }

    .magic-btn:active { transform: scale(0.97); }

    @keyframes btn-gradient {
      0%   { background-position: 0%; }
      100% { background-position: 200%; }
    }

    /* 粒子 */
    .particles {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 0;
      height: 0;
      pointer-events: none;
    }

    .particle {
      position: absolute;
      width: 6px;
      height: 6px;
      border-radius: 50%;
      opacity: 0;
    }

    .magic-btn.explode ~ .particles .particle {
      animation: explode 0.8s ease-out forwards;
    }

    @keyframes explode {
      0%   { transform: translate(0, 0) scale(1); opacity: 1; }
      100% { transform: var(--tx, 60px) var(--ty, -60px) scale(0); opacity: 0; }
    }

    /* ===== 6. 进度条动画 ===== */
    .progress-list {
      width: 320px;
      display: flex;
      flex-direction: column;
      gap: 16px;
    }

    .progress-item {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .progress-label {
      display: flex;
      justify-content: space-between;
      color: #fff;
      font-size: 13px;
      opacity: 0.8;
    }

    .progress-track {
      height: 8px;
      background: rgba(255,255,255,0.1);
      border-radius: 99px;
      overflow: hidden;
    }

    .progress-fill {
      height: 100%;
      border-radius: 99px;
      animation: fill-in 2s cubic-bezier(0.4, 0, 0.2, 1) forwards;
      width: 0;
    }

    .p1 .progress-fill { background: linear-gradient(90deg, #6366f1, #a78bfa); animation-delay: 0.2s; --w: 82%; }
    .p2 .progress-fill { background: linear-gradient(90deg, #ec4899, #f472b6); animation-delay: 0.4s; --w: 65%; }
    .p3 .progress-fill { background: linear-gradient(90deg, #14b8a6, #34d399); animation-delay: 0.6s; --w: 91%; }
    .p4 .progress-fill { background: linear-gradient(90deg, #f59e0b, #fbbf24); animation-delay: 0.8s; --w: 48%; }

    @keyframes fill-in {
      to { width: var(--w); }
    }
  </style>
</head>
<body>

  <!-- 1. 行星轨道 -->
  <h2>🪐 Orbit</h2>
  <div class="orbit-scene">
    <div class="orbit-ring"></div>
    <div class="orbit-ring"></div>
    <div class="orbit-ring"></div>
    <div class="orbit-core"></div>
    <div class="planet planet-1"></div>
    <div class="planet planet-2"></div>
    <div class="planet planet-3"></div>
  </div>

  <!-- 2. 加载动画 -->
  <h2>⏳ Loader</h2>
  <div class="loader-row">
    <div class="wave-dots">
      <span></span><span></span><span></span><span></span><span></span>
    </div>
    <div class="ring-loader">
      <svg viewBox="0 0 60 60" width="60" height="60">
        <circle class="c1" cx="30" cy="30" r="24"/>
        <circle class="c2" cx="30" cy="30" r="14"/>
      </svg>
    </div>
  </div>

  <!-- 3. 卡片翻转 -->
  <h2>🃏 Flip Card</h2>
  <div class="cards-row">
    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-front"><span class="icon">🚀</span>启动</div>
        <div class="flip-back"><span class="icon">🌌</span>飞翔</div>
      </div>
    </div>
    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-front"><span class="icon">💎</span>价值</div>
        <div class="flip-back"><span class="icon">✨</span>闪耀</div>
      </div>
    </div>
    <div class="flip-card">
      <div class="flip-card-inner">
        <div class="flip-front"><span class="icon">🎯</span>目标</div>
        <div class="flip-back"><span class="icon">🏆</span>成功</div>
      </div>
    </div>
  </div>

  <!-- 4. 文字波浪 -->
  <h2>💬 Text Wave</h2>
  <div class="text-animate">
    <span>H</span><span>e</span><span>l</span><span>l</span><span>o</span>
    <span>&nbsp;</span>
    <span>W</span><span>o</span><span>r</span><span>l</span><span>d</span>
  </div>

  <!-- 5. 魔法按钮 -->
  <h2>✨ Magic Button</h2>
  <div class="btn-wrap">
    <button class="magic-btn" id="magicBtn" onclick="triggerExplode(this)">
      点击爆炸 💥
    </button>
    <div class="particles" id="particles"></div>
  </div>

  <!-- 6. 进度条 -->
  <h2>📊 Progress</h2>
  <div class="progress-list">
    <div class="progress-item p1">
      <div class="progress-label"><span>Vue 3</span><span>82%</span></div>
      <div class="progress-track"><div class="progress-fill"></div></div>
    </div>
    <div class="progress-item p2">
      <div class="progress-label"><span>TypeScript</span><span>65%</span></div>
      <div class="progress-track"><div class="progress-fill"></div></div>
    </div>
    <div class="progress-item p3">
      <div class="progress-label"><span>CSS 动画</span><span>91%</span></div>
      <div class="progress-track"><div class="progress-fill"></div></div>
    </div>
    <div class="progress-item p4">
      <div class="progress-label"><span>Rust</span><span>48%</span></div>
      <div class="progress-track"><div class="progress-fill"></div></div>
    </div>
  </div>

  <script>
    const COLORS = ['#f472b6','#a78bfa','#60a5fa','#34d399','#fbbf24','#fb923c'];

    function triggerExplode(btn) {
      const container = document.getElementById('particles');
      container.innerHTML = '';

      const count = 20;
      for (let i = 0; i < count; i++) {
        const p = document.createElement('div');
        p.className = 'particle';
        const angle = (360 / count) * i;
        const dist = 50 + Math.random() * 60;
        const tx = `translateX(${Math.cos(angle * Math.PI / 180) * dist}px)`;
        const ty = `translateY(${Math.sin(angle * Math.PI / 180) * dist}px)`;
        p.style.cssText = `
          background: ${COLORS[i % COLORS.length]};
          --tx: ${tx};
          --ty: ${ty};
          box-shadow: 0 0 6px ${COLORS[i % COLORS.length]};
          animation: explode 0.8s ease-out forwards;
          animation-delay: ${Math.random() * 0.1}s;
        `;
        container.appendChild(p);
      }

      btn.classList.add('explode');
      setTimeout(() => {
        btn.classList.remove('explode');
        container.innerHTML = '';
      }, 1000);
    }
  </script>
</body>
</html>
