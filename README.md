# Brithday-Tamanna
<!DOCTYPE html><html lang="bn">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Happy Birthday Tamanna 🎉</title>
  <style>
    :root{
      --bg1: #ff9a9e;
      --bg2: #fad0c4;
      --card: rgba(255,255,255,0.15);
      --glass: rgba(255,255,255,0.25);
    }
    *{box-sizing: border-box}
    html,body{height:100%;margin:0;font-family: 'Poppins', Arial, sans-serif}
    body{
      background: linear-gradient(135deg,var(--bg1),var(--bg2));
      display:flex;align-items:center;justify-content:center;padding:20px;overflow:hidden;
    }
    .stage{
      width:100%;max-width:900px;background:linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0.03));
      border-radius:18px;padding:28px;backdrop-filter: blur(6px);box-shadow:0 12px 40px rgba(0,0,0,0.18);position:relative;
      color:#fff;text-align:center;
    }
    h1{font-size:46px;margin:8px 0 4px;text-shadow:0 6px 20px rgba(0,0,0,0.25)}
    p.lead{margin:0 0 18px;font-size:18px;opacity:0.95}
    .cake{font-size:110px;display:inline-block;transform-origin:center;animation:bounce 1.6s infinite}
    @keyframes bounce{0%,100%{transform:translateY(0)}50%{transform:translateY(-18px)}}.controls{display:flex;gap:10px;flex-wrap:wrap;justify-content:center;margin-top:18px}
.btn{background:var(--glass);border:1px solid rgba(255,255,255,0.12);padding:10px 16px;border-radius:12px;color:#fff;font-weight:600;cursor:pointer}
.btn:active{transform:translateY(1px)}

/* confetti pieces container */
.confetti-wrap{pointer-events:none;position:absolute;inset:0;overflow:hidden}
.confetti{
  position:absolute;top:-10vh;will-change:transform,opacity;opacity:0.95;border-radius:2px;
  animation:fall linear forwards;transform-origin:center;
}
@keyframes fall{to{transform:translateY(120vh) rotate(720deg);opacity:0.95}}

/* message card */
.card{margin-top:18px;background:rgba(255,255,255,0.06);padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.06)}
.from{font-size:14px;opacity:0.95}

/* mobile tweaks */
@media (max-width:480px){h1{font-size:30px}.cake{font-size:72px}}

  </style>
</head>
<body>
  <div class="stage" role="main">
    <div style="display:flex;align-items:center;justify-content:center;gap:18px;flex-wrap:wrap">
      <div class="cake" aria-hidden>🎂</div>
      <div style="text-align:left;min-width:260px">
        <h1>শুভ জন্মদিন, Tamanna! 🎉</h1>
        <p class="lead">তোমার জন্য রইলো অনেক ভালোবাসা, হাসি আর সফলতার শুভকামনা।</p>
      </div>
    </div><div class="controls">
  <button class="btn" id="surpriseBtn">Surprise দেখাও ✨</button>
  <button class="btn" id="musicToggle">মিউজিক চালাও ▶️</button>
  <button class="btn" id="shareBtn">লিংক কপি করো 🔗</button>
</div>

<div class="card" id="wishCard">
  <div style="font-size:16px;margin-bottom:8px">Dear Tamanna,</div>
  <div style="font-size:15px;opacity:0.95">আজকের দিনটা তোমার জন্য একদম স্পেশাল হওয়া উচিত — তুমি হাসিখুশি থেকো, সবদিন ভালো থাকবে এমনই কামনা করছি।</div>
  <div class="from" style="margin-top:10px">— তোমার বন্ধু</div>
</div>

<div class="confetti-wrap" id="confettiWrap" aria-hidden></div>

<audio id="bgAudio" loop src=""></audio>

  </div>  <script>
    // --- small config ---
    const confettiColors = ['#FFD700','#FF6B6B','#6BCB77','#4D96FF','#C77DFF','#FF9F1C'];
    const confettiWrap = document.getElementById('confettiWrap');
    const surpriseBtn = document.getElementById('surpriseBtn');
    const musicToggle = document.getElementById('musicToggle');
    const shareBtn = document.getElementById('shareBtn');
    const audio = document.getElementById('bgAudio');

    // Optional: Small happy tune (data URI base64 small beep melody) - left empty so file stays offline-friendly.
    // If you want a music file, replace audio.src = 'path/to/music.mp3';

    function makeConfettiPiece(){
      const el = document.createElement('div');
      el.className = 'confetti';
      const size = Math.floor(Math.random()*12)+6; 
      el.style.width = size+'px'; el.style.height = size+'px';
      el.style.left = Math.random()*100 + '%';
      el.style.background = confettiColors[Math.floor(Math.random()*confettiColors.length)];
      el.style.transform = 'rotate('+ (Math.random()*360) +'deg)';
      el.style.animationDuration = (Math.random()*2 + 3) + 's';
      el.style.borderRadius = Math.random()>0.6? '4px':'0px';
      confettiWrap.appendChild(el);
      setTimeout(()=> el.remove(), 5000);
    }

    let confettiInterval = null;
    function startConfetti(){ if(confettiInterval) return; confettiInterval = setInterval(makeConfettiPiece, 80); }
    function stopConfetti(){ clearInterval(confettiInterval); confettiInterval=null }

    surpriseBtn.addEventListener('click', ()=>{
      // show confetti + small animation on card
      startConfetti();
      const card = document.getElementById('wishCard');
      card.animate([{transform:'scale(1)'},{transform:'scale(1.02)'},{transform:'scale(1)'}],{duration:600,iterations:1});
      // stop after 6 seconds
      setTimeout(stopConfetti,6000);
    });

    // simple audio toggle (user can add an mp3 by editing the file)
    let playing = false;
    musicToggle.addEventListener('click', ()=>{
      if(!audio.src){
        alert('মিউজিক ফাইল যোগ করতে চাইলে HTML ফাইলের audio src এ mp3 link বসিয়ে দিন।')
        return;
      }
      if(playing){ audio.pause(); musicToggle.textContent='মিউজিক চালাও ▶️'; }
      else { audio.play(); musicToggle.textContent='মিউজিক বন্ধ করো ⏸️'; }
      playing = !playing;
    });

    // share: copy current page URL (works when hosted). If opened locally, copies file path.
    shareBtn.addEventListener('click', async ()=>{
      const text = window.location.href;
      try{ await navigator.clipboard.writeText(text); alert('লিংক কপি করা হয়েছে — এখন আপনি পাঠাতে পারবেন।'); }
      catch(e){ prompt('Copy this link:', text); }
    });

    // Accessibility: allow Enter key to trigger surprise
    surpriseBtn.addEventListener('keyup', (e)=>{ if(e.key==='Enter') surpriseBtn.click(); });

    // Auto small initial confetti for charm
    setTimeout(()=>{ makeConfettiPiece(); makeConfettiPiece(); }, 600);
  </script></body>
</html>
