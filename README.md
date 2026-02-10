# my-website
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Ultimate Aero Profile - 2002 Final Fixed</title>
<style>
/* --------------------
   基本デザイン
   -------------------- */
html, body {
  margin: 0; padding: 0; width: 100%; height: 100%; overflow: hidden;
  font-family: 'Segoe UI', 'Meiryo', sans-serif;
  background-color: #000; user-select: none;
}

#main-bg {
  position: absolute; inset: 0;
  background: 
    radial-gradient(circle at 50% 120%, #90EE90 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, #ffffff 0%, transparent 30%),
    linear-gradient(180deg, #00bfff 0%, #e0f7fa 60%, #32cd32 100%);
  z-index: 0; opacity: 0; transition: opacity 1.5s;
}

/* --------------------
   ローディング画面 (強烈ネオン演出)
   -------------------- */
#loading-screen {
  position: fixed; inset: 0; background: #000; z-index: 99999;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
}
.loading-text {
  color: #ffffff; font-size: 32px; font-weight: bold;
  animation: neonPulse 5s infinite ease-in-out; margin-bottom: 25px;
  letter-spacing: 2px;
}
@keyframes neonPulse {
  0%, 100% { text-shadow: 0 0 7px #fff, 0 0 10px #fff, 0 0 21px #00ffff, 0 0 42px #00ffff, 0 0 82px #00ffff, 0 0 92px #00ffff; }
  50% { text-shadow: 0 0 2px #fff, 0 0 5px #fff, 0 0 10px #00ffff, 0 0 15px #00ffff, 0 0 30px #00ffff, 0 0 40px #00ffff; }
}
.kaomoji-container {
  display: flex; gap: 20px; font-size: 24px; font-weight: bold;
  animation: kaomojiGlow 5s infinite ease-in-out;
}
.pink { color: #ff1493; text-shadow: 0 0 10px #ff1493, 0 0 20px #ff1493, 0 0 30px #ff1493; }
.green { color: #00ff00; text-shadow: 0 0 10px #00ff00, 0 0 20px #00ff00, 0 0 30px #00ff00; }
.purple { color: #cc00ff; text-shadow: 0 0 10px #cc00ff, 0 0 20px #cc00ff, 0 0 30px #cc00ff; }
@keyframes kaomojiGlow { 0%, 100% { filter: brightness(1.5) blur(0.5px); } 50% { filter: brightness(0.5) blur(0px); } }

/* --------------------
   テロップ速度
   -------------------- */
.marquee-bar {
  position: fixed; width: 100%; background: rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(8px); border-top: 1px solid rgba(255,255,255,0.6);
  border-bottom: 1px solid rgba(255,255,255,0.6); height: 30px; z-index: 1000;
  display: flex; align-items: center; overflow: hidden; color: #004488;
  font-size: 13px; font-weight: bold;
}
#top-bar { top: 0; }
#bottom-bar { bottom: 0; }
.marquee-content { display: inline-block; white-space: nowrap; padding-left: 100%; }
#top-bar .marquee-content { animation: marquee-top 22s linear infinite; }
#bottom-bar .marquee-content { animation: marquee-bottom 150s linear infinite; }
@keyframes marquee-top { from { transform: translateX(0); } to { transform: translateX(-100%); } }
@keyframes marquee-bottom { from { transform: translateX(0); } to { transform: translateX(-100%); } }

/* --------------------
   掲示板 (BBS)
   -------------------- */
#bbs-sidebar {
  position: fixed; left: 15px; top: 50px; bottom: 50px; width: 210px;
  background: rgba(255, 255, 255, 0.25); backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.5); border-radius: 15px;
  z-index: 10; display: flex; flex-direction: column; box-shadow: 0 4px 15px rgba(0,0,0,0.1);
}
.bbs-header { background: linear-gradient(to bottom, #7abcff, #4096ee); color: white; padding: 10px; font-size: 12px; text-align: center; border-radius: 14px 14px 0 0; font-weight: bold; }
#counter-display { font-size: 16px; color: #ffcc00; text-shadow: 1px 1px 2px #000; margin-top: 5px; display: block; }
.bbs-content { flex: 1; overflow-y: auto; padding: 10px; font-size: 11px; }
.bbs-post { background: rgba(255, 255, 255, 0.5); margin-bottom: 8px; padding: 8px; border-radius: 8px; border-left: 4px solid #00bfff; animation: poyonIn 0.4s ease-out; word-break: break-all; }
@keyframes poyonIn { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }
.bbs-form { padding: 10px; border-top: 1px solid rgba(255,255,255,0.5); }
.bbs-form input, .bbs-form textarea { width: 90%; margin-bottom: 5px; border-radius: 5px; border: 1px solid #ccc; padding: 4px; font-size: 11px; }
.bbs-form button { width: 100%; background: #4096ee; color: white; border: none; padding: 5px; border-radius: 10px; cursor: pointer; font-weight: bold; }

/* --------------------
   XP風ウィンドウ (ドラッグ)
   -------------------- */
.xp-window { position: absolute; width: 220px; background: #f1f1f1; border: 1px solid #0055ea; border-radius: 8px 8px 0 0; box-shadow: 8px 8px 20px rgba(0,0,0,0.2); z-index: 100; overflow: hidden; touch-action: none; }
.title-bar { background: linear-gradient(to bottom, #0058ee 0%, #3593ff 100%); height: 32px; display: flex; align-items: center; justify-content: space-between; padding: 0 10px; color: white; font-size: 13px; font-weight: bold; cursor: move; }
.close-x { width: 22px; height: 22px; background: #e04a3f; border: 1px solid #fff; border-radius: 3px; cursor: pointer; text-align: center; color: white; line-height: 20px; z-index: 101; }

/* --------------------
   全消しシステム
   -------------------- */
#clearBtn { position: fixed; bottom: 40px; right: 20px; background: #ff4444; color: #fff; border: 2px solid #fff; padding: 10px 15px; border-radius: 10px; cursor: pointer; z-index: 1100; font-weight: bold; }
#confirmBox { position: fixed; bottom: 95px; right: 20px; background: rgba(255,255,255,0.95); border: 2px solid #0055ea; padding: 15px; border-radius: 12px; display: none; z-index: 1100; text-align: center; backdrop-filter: blur(5px); box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
#confirmBox button { margin: 5px; padding: 6px 15px; border-radius: 6px; cursor: pointer; font-weight: bold; border: 1px solid #999; }
.btn-yes { background: #ff4444; color: white; }
.btn-no { background: #eee; }
#vn-box { position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 80%; max-width: 400px; background: linear-gradient(rgba(0,100,200,0.9), rgba(0,50,150,0.95)); border: 5px solid #00ffff; border-radius: 30px; padding: 40px 20px; color: #fff; font-weight: bold; font-size: 48px; display: none; z-index: 20000; text-align: center; box-shadow: 0 0 50px rgba(0,255,255,0.8); text-shadow: 0 0 15px #00ffff; }

/* --------------------
   装飾
   -------------------- */
.dolphin { position: absolute; font-size: 80px; z-index: 2; cursor: pointer; transition: transform 0.2s; pointer-events: auto; }
@keyframes swimR { from { left: -150px; } to { left: 115vw; } }
@keyframes swimL { from { left: 115vw; transform: scaleX(-1); } to { left: -150px; transform: scaleX(-1); } }
.bubble { position: absolute; background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.85), rgba(255,255,255,0.1)); border: 1px solid rgba(255,255,255,0.4); border-radius: 50%; pointer-events: none; animation: floatUp linear infinite; z-index: 1; }
@keyframes floatUp { 0% { transform: translateY(110vh) translateX(0); opacity: 0; } 50% { opacity: 0.6; } 100% { transform: translateY(-20vh) translateX(-15px); opacity: 0; } }
.poyon-effect { position: absolute; pointer-events: none; z-index: 9999; animation: poyonAnim 0.7s forwards; font-size: 40px; }
@keyframes poyonAnim { 0% { transform: translate(-50%, -50%) scale(0); opacity: 0; } 50% { transform: translate(-50%, -50%) scale(1.6); opacity: 1; } 100% { transform: translate(-50%, -50%) scale(1.2); opacity: 0; } }
</style>
</head>
<body>

<div id="loading-screen">
  <div class="loading-text">Now Loading...</div>
  <div class="kaomoji-container">
    <span class="pink">(^^)</span>
    <span class="green">(；；)</span>
    <span class="purple">(^_-)-☆</span>
  </div>
</div>

<div id="top-bar" class="marquee-bar">
  <div class="marquee-content">
    ▷▷ Welcome to YUHEI's Website (Ver 2.3 FINAL) ▷▷ 🫧 ぷにぷに ▷▷ 🍣 お寿司は、小宇宙。 ▷▷ 🐬 イルカさんをタップ ▷▷ ニュース：全ての機能を復旧完了！ ▷▷
  </div>
</div>

<div id="bottom-bar" class="marquee-bar">
  <div id="fortune-marquee" class="marquee-content"></div>
</div>

<div id="bbs-sidebar">
  <div class="bbs-header">FOOTPRINTS (BBS)<span id="counter-display">000000 HIT</span></div>
  <div id="bbs-list" class="bbs-content"><div class="bbs-post"><b>管理人</b>いらっしゃい！</div></div>
  <div class="bbs-form">
    <input type="text" id="bbs-name" placeholder="なまえ">
    <textarea id="bbs-msg" rows="2" placeholder="メッセージ"></textarea>
    <button onclick="postBBS()">書き込む</button>
  </div>
</div>

<div id="main-bg"><div id="bg-layer"></div></div>

<div id="profileBox" style="position: absolute; top: 50%; left: 58%; transform: translate(-50%, -50%); width: 300px; background: rgba(255, 255, 255, 0.4); border: 2px solid rgba(255, 255, 255, 0.7); border-radius: 20px; padding: 25px; text-align: center; backdrop-filter: blur(15px); z-index: 5; box-shadow: 0 10px 40px rgba(0,0,0,0.1);">
  <div id="icon-container" style="width:110px; height:110px; margin:0 auto 15px; border-radius:50%; border:5px solid #fff; overflow:hidden; cursor:pointer; background:white; display:flex; align-items:center; justify-content:center; font-size:60px; box-shadow:0 5px 15px rgba(0,0,0,0.1);">
    <span id="user-icon-emoji">🍣</span>
    <img id="user-icon-img" style="display:none; width:100%; height:100%; object-fit:cover;">
  </div>
  <input type="file" id="fileInput" accept="image/*" style="display:none;">
  <div style="font-size:24px; font-weight:bold; color:#004488; margin-bottom:10px; text-shadow:0 1px 2px #fff;">ゆうへい</div>
  <div style="font-size:13px; color:#333; background:rgba(255,255,255,0.4); padding:12px; border-radius:12px; text-align:left; border:1px solid rgba(255,255,255,0.5);">趣味 ▷ すしすきー<br>好き ▷ かにぱん・おすし<br>一言 ▷ へいらっしゃい！</div>
  <button id="centerBtn" style="background:linear-gradient(#7abcff, #4096ee); border:1px solid #1e69de; color:white; padding:10px 25px; border-radius:30px; font-weight:bold; cursor:pointer; margin-top:15px; box-shadow:0 4px 0 #1a5cad; text-shadow:0 1px 2px rgba(0,0,0,0.3);">押してみる？</button>
</div>

<button id="clearBtn">全部消す</button>
<div id="confirmBox"><b>全部けしちゃう？</b><br><button class="btn-yes" onclick="executeClear()">けしちゃえ！</button><button class="btn-no" onclick="closeConfirm()">まだ！</button></div>
<div id="vn-box">まいどあり！</div>

<script>
// 1. カウンター
let hitCount = parseInt(localStorage.getItem('hitCount') || '1555');
hitCount++; localStorage.setItem('hitCount', hitCount);
document.getElementById('counter-display').textContent = hitCount.toString().padStart(6, '0') + " HIT";

// 2. アイコン変更
const iconContainer = document.getElementById('icon-container'), fileInput = document.getElementById('fileInput'), userEmoji = document.getElementById('user-icon-emoji'), userImg = document.getElementById('user-icon-img');
iconContainer.onclick = () => fileInput.click();
fileInput.onchange = (e) => {
  const file = e.target.files[0];
  if (file) {
    const r = new FileReader(); r.onload = (ev) => { userImg.src = ev.target.result; userImg.style.display = 'block'; userEmoji.style.display = 'none'; spawnPoyon(window.innerWidth/2, window.innerHeight/2, "✨"); };
    r.readAsDataURL(file);
  }
};

// 3. 全消し
function executeClear() { document.querySelectorAll('.xp-window').forEach(w => w.remove()); document.getElementById('confirmBox').style.display = 'none'; document.getElementById('vn-box').style.display = 'block'; setTimeout(() => document.getElementById('vn-box').style.display = 'none', 3000); }
document.getElementById('clearBtn').onclick = () => document.getElementById('confirmBox').style.display = 'block';
function closeConfirm() { document.getElementById('confirmBox').style.display = 'none'; }

// 4. 掲示板
function postBBS() { const name = document.getElementById('bbs-name').value || "名無しさん", msg = document.getElementById('bbs-msg').value; if(!msg) return; const post = document.createElement('div'); post.className = 'bbs-post'; post.innerHTML = `<b>${name}</b> ${msg}`; const list = document.getElementById('bbs-list'); list.insertBefore(post, list.firstChild); document.getElementById('bbs-msg').value = ""; spawnPoyon(100, window.innerHeight-100, "📝"); }

// 5. 占い (順位固定)
const zodiacs = ["牡羊座", "牡牛座", "双子座", "蟹座", "獅子座", "乙女座", "天秤座", "蠍座", "射手座", "山羊座", "水瓶座", "魚座"], items = ["アンコリーノ", "ぬあみ(お風呂)", "金色の皿", "透明な消しゴム", "中トロ", "醤油皿", "特大アガリ", "ガリ", "かにぱん", "カリフォルニアロール", "おもちゃの指輪", "ガラスのビー玉", "納豆巻き", "ラベンダーのポプリ", "光るシール", "巻きたての鉄火巻", "お気に入りのCD", "タイの煮付け", "えんがわ", "穴子", "貝殻", "ミントタブレット"], comments = ["おめでとうございます！持ち歩いてみては？", "調子がいいみたい。新チャレンジを！", "絶好調！寿司のように輝く一日に。", "安定した運気。落ち着いて行動を。", "人との繋がりが幸運を運びます。", "一息つくのが大事。特大アガリを。", "努力が認められる予感。信じて！", "小さな幸せ発見。足元に注目。", "焦りは禁物。大トロ級の幸せが。", "整理整頓が吉。運気爆上がり。", "無理禁物。早めにぬあみして休息。", "今日は慎重に。最高のネタを待とう。"];
function generateFortune() { let fText = "▷▷ 今日の運勢占い ▷▷ ", zS = [...zodiacs].sort(() => Math.random() - 0.5), iS = [...items].sort(() => Math.random() - 0.5), cS = [...comments].sort(() => Math.random() - 0.5); for(let i=0; i<12; i++) fText += `${i+1}位は${zS[i]}！ ${cS[i]} ラッキーアイテムは「${iS[i]}」。 ▷▷ `; document.getElementById('fortune-marquee').textContent = fText; }
generateFortune();

// 6. メッセージ窓 (修正版ドラッグ＆閉じる)
const msgList = ["わっ！","ぷにっ","こら！","つんつんすな","エラー：可愛すぎます","へいらっしゃい！","へいおまち！","決済完了 105円(税込)","つんつん料貰っちゃうよ","おすしたべたい","あがり！","もういっちょ！","( ﾟдﾟ)🍣"];
let zIdx = 100;
document.getElementById('centerBtn').onclick = (e) => { 
  e.stopPropagation(); 
  const win = document.createElement('div'); win.className = 'xp-window'; 
  win.style.left = (Math.random()*20 + 20) + 'vw'; win.style.top = (Math.random()*20 + 30) + 'vh'; 
  win.style.zIndex = ++zIdx; 
  win.innerHTML = `<div class="title-bar"><span>Message</span><div class="close-x">×</div></div><div style="padding:25px; background:#fff; text-align:center; font-weight:bold;">${msgList[Math.floor(Math.random()*msgList.length)]}</div>`; 
  document.body.appendChild(win); 
  const closeBtn = win.querySelector('.close-x');
  closeBtn.onclick = (ev) => { ev.stopPropagation(); win.remove(); };
  closeBtn.ontouchstart = (ev) => { ev.stopPropagation(); win.remove(); };
  win.onmousedown = win.ontouchstart = () => win.style.zIndex = ++zIdx; 
  makeDraggable(win); 
};

function makeDraggable(el) { 
  const t = el.querySelector('.title-bar'); 
  let isDragging = false, offsetX, offsetY; 
  const start = (e) => { 
    if (e.target.className === 'close-x') return; 
    isDragging = true; 
    const cX = e.type === 'touchstart' ? e.touches[0].clientX : e.clientX, cY = e.type === 'touchstart' ? e.touches[0].clientY : e.clientY; 
    offsetX = cX - el.getBoundingClientRect().left; offsetY = cY - el.getBoundingClientRect().top; 
    el.style.zIndex = ++zIdx; 
    if (e.type === 'touchstart') e.preventDefault(); 
  }; 
  const move = (e) => { 
    if (!isDragging) return; 
    const cX = e.type === 'touchmove' ? e.touches[0].clientX : e.clientX, cY = e.type === 'touchmove' ? e.touches[0].clientY : e.clientY; 
    el.style.left = (cX - offsetX) + 'px'; el.style.top = (cY - offsetY) + 'px'; 
    if (e.type === 'touchmove') e.preventDefault(); 
  }; 
  const end = () => { isDragging = false; }; 
  t.addEventListener('mousedown', start); document.addEventListener('mousemove', move); document.addEventListener('mouseup', end); 
  t.addEventListener('touchstart', start, { passive: false }); document.addEventListener('touchmove', move, { passive: false }); document.addEventListener('touchend', end); 
}

// 7. 演出
window.onload = () => { setTimeout(() => { document.getElementById('loading-screen').remove(); document.getElementById('main-bg').style.opacity = '1'; }, 5000); };
const bgLayer = document.getElementById('bg-layer');
for(let i=0; i<30; i++) { const b = document.createElement('div'); b.className = 'bubble'; const s = Math.random() * 55 + 10; b.style.width = b.style.height = s + 'px'; b.style.left = Math.random() * 100 + 'vw'; b.style.animationDuration = (Math.random() * 10 + 5) + 's'; bgLayer.appendChild(b); }
document.addEventListener('click', (e) => { if(e.target.closest('button') || e.target.closest('.xp-window') || e.target.closest('#bbs-sidebar') || e.target.closest('.dolphin')) return; spawnPoyon(e.clientX, e.clientY, "🍣"); });

function spawnPoyon(x, y, char) { 
  const p = document.createElement('div'); p.className = 'poyon-effect'; p.textContent = char; 
  p.style.left = x + 'px'; p.style.top = y + 'px'; 
  document.body.appendChild(p); setTimeout(() => p.remove(), 700); 
}

// イルカ生成 (タップ時の挙動を1回に限定 & 絵文字を厳選)
const dolphinEmojis = ["💚","🩵","💞","❗","❔","🍀"];
for(let i=0; i<3; i++) { 
  const d = document.createElement('div'); d.className = 'dolphin'; d.textContent = '🐬'; 
  d.style.top = (Math.random()*60 + 20) + 'vh'; 
  const isR = Math.random() > 0.5; 
  d.style.animation = `${isR ? 'swimL' : 'swimR'} ${Math.random()*12 + 18}s linear infinite`; 
  
  // 重複発火を防ぐためのハンドラ
  const handleDolphin = (e) => {
    e.preventDefault(); // デフォルト挙動と伝播を抑制
    e.stopPropagation();
    const cX = (e.type === 'touchstart') ? e.touches[0].clientX : e.clientX;
    const cY = (e.type === 'touchstart') ? e.touches[0].clientY : e.clientY;
    const randomEmoji = dolphinEmojis[Math.floor(Math.random() * dolphinEmojis.length)];
    spawnPoyon(cX, cY, randomEmoji);
  };
  
  // mouseup/touchend ではなく、一回のアクションで一回だけ呼ぶ
  d.addEventListener('mousedown', (e) => { if(e.button === 0) handleDolphin(e); });
  d.addEventListener('touchstart', handleDolphin, { passive: false });
  
  document.body.appendChild(d);
}
</script>
</body>
</html>
