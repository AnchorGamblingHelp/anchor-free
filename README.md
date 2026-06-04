<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ANCHOR · A free chat for when the gambling urge hits</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,500;0,9..144,600;1,9..144,400&family=Hanken+Grotesk:wght@400;500;600;700&family=Space+Mono:wght@400&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#F3EEE4; --bg-2:#ECE5D6; --surface:#FCFAF4; --surface-2:#EEE7D9;
    --ink:#232E27; --muted:#5A675E; --faint:#8C978D;
    --line:rgba(35,46,39,0.10); --line-strong:rgba(35,46,39,0.17);
    --sage:#4F7D5E; --sage-deep:#3C6349; --sage-soft:rgba(79,125,94,0.13);
    --blue:#4E7C99; --blue-soft:rgba(78,124,153,0.13);
    --clay:#BC6A45; --clay-soft:rgba(188,106,69,0.12);
    --radius:18px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  html{scroll-behavior:smooth}
  body{background:var(--bg);color:var(--ink);font-family:'Hanken Grotesk',sans-serif;line-height:1.6;-webkit-font-smoothing:antialiased;overflow-x:hidden}
  body::before{content:"";position:fixed;inset:0;pointer-events:none;z-index:0;
    background:radial-gradient(900px 620px at 84% -12%, rgba(79,125,94,0.10), transparent 60%),radial-gradient(720px 660px at 4% 2%, rgba(78,124,153,0.07), transparent 55%)}
  .wrap{position:relative;z-index:1;max-width:1000px;margin:0 auto;padding:0 24px}
  .display{font-family:'Fraunces',serif;font-weight:600;letter-spacing:-0.015em;line-height:1.08}
  .eyebrow{font-family:'Space Mono',monospace;font-size:12px;letter-spacing:0.2em;text-transform:uppercase;color:var(--sage)}
  em.serif{font-style:italic;font-weight:400;color:var(--clay)}

  nav{position:sticky;top:0;z-index:50;backdrop-filter:blur(12px);background:linear-gradient(to bottom,rgba(243,238,228,0.95),rgba(243,238,228,0.66));border-bottom:1px solid var(--line)}
  .nav-inner{max-width:1000px;margin:0 auto;padding:14px 24px;display:flex;align-items:center;justify-content:space-between}
  .logo{font-family:'Fraunces',serif;font-weight:600;font-size:20px;letter-spacing:0.03em;display:flex;align-items:center;gap:10px}
  .logo .dot{width:9px;height:9px;border-radius:50%;background:var(--sage);box-shadow:0 0 12px rgba(79,125,94,0.6);animation:breathe 3.6s ease-in-out infinite}
  @keyframes breathe{0%,100%{transform:scale(1);opacity:1}50%{transform:scale(.7);opacity:.5}}
  .nav-links{display:flex;gap:22px;align-items:center}
  .nav-links a{color:var(--muted);text-decoration:none;font-size:14px;transition:color .2s}
  .nav-links a:hover{color:var(--ink)}
  .nav-links a.help{color:var(--clay);font-weight:600}
  @media(max-width:640px){.nav-links a.q{display:none}}

  header{padding:54px 0 26px;text-align:center}
  h1.hero{font-size:clamp(36px,5.4vw,58px);margin-top:14px}
  .hero-sub{font-size:18px;color:var(--muted);max-width:560px;margin:18px auto 22px}
  .badges{display:flex;gap:10px;justify-content:center;flex-wrap:wrap;margin-bottom:6px}
  .pill{font-family:'Space Mono';font-size:12px;letter-spacing:.04em;color:var(--muted);background:var(--surface);border:1px solid var(--line);padding:7px 13px;border-radius:100px;display:inline-flex;align-items:center;gap:7px}
  .pill .d{width:6px;height:6px;border-radius:50%;background:var(--sage)}
  .reveal{opacity:0;transform:translateY(18px);animation:rise .8s cubic-bezier(.16,.8,.3,1) forwards}
  .d1{animation-delay:.04s}.d2{animation-delay:.14s}.d3{animation-delay:.24s}.d4{animation-delay:.34s}
  @keyframes rise{to{opacity:1;transform:none}}

  /* CHAT */
  .chat-section{padding:14px 0 30px}
  .chat-card{max-width:720px;margin:0 auto;background:var(--surface);border:1px solid var(--line-strong);border-radius:22px;overflow:hidden;box-shadow:0 26px 70px rgba(35,46,39,0.14)}
  .chat-head{padding:15px 20px;border-bottom:1px solid var(--line);display:flex;align-items:center;gap:13px;background:var(--bg-2)}
  .chat-head .av{width:42px;height:42px;border-radius:50%;background:linear-gradient(150deg,#6fa07e,var(--sage));display:grid;place-items:center;font-size:20px;flex-shrink:0;box-shadow:0 4px 14px rgba(79,125,94,0.3)}
  .chat-head .name{font-family:'Fraunces';font-weight:600;font-size:17px;line-height:1.2}
  .chat-head .sub{font-size:12px;color:var(--faint);display:flex;align-items:center;gap:6px;margin-top:1px}
  .chat-head .sub .on{width:7px;height:7px;border-radius:50%;background:var(--sage);box-shadow:0 0 8px rgba(79,125,94,0.7)}
  .chat-body{height:470px;overflow-y:auto;padding:22px 20px;display:flex;flex-direction:column;gap:11px;scroll-behavior:smooth}
  .chat-body::-webkit-scrollbar{width:8px}
  .chat-body::-webkit-scrollbar-thumb{background:var(--line-strong);border-radius:8px}
  .msg{max-width:85%;padding:12px 15px;font-size:15px;line-height:1.55;opacity:0;transform:translateY(8px);animation:rise .4s forwards}
  .msg.bot{align-self:flex-start;background:var(--bg-2);border:1px solid var(--line);border-radius:16px;border-bottom-left-radius:5px;color:var(--ink)}
  .msg.bot b{color:var(--sage-deep)}
  .msg.user{align-self:flex-end;background:var(--sage-deep);color:#F4F1E8;border-radius:16px;border-bottom-right-radius:5px;font-weight:500}
  .typing{align-self:flex-start;background:var(--bg-2);border:1px solid var(--line);border-radius:16px;border-bottom-left-radius:5px;padding:14px 16px;display:flex;gap:5px}
  .typing span{width:7px;height:7px;border-radius:50%;background:var(--faint);animation:blink 1.2s infinite}
  .typing span:nth-child(2){animation-delay:.2s}.typing span:nth-child(3){animation-delay:.4s}
  @keyframes blink{0%,60%,100%{opacity:.3;transform:translateY(0)}30%{opacity:1;transform:translateY(-3px)}}
  .replies{align-self:stretch;display:flex;flex-wrap:wrap;gap:8px;margin-top:3px}
  .chip{background:var(--surface);border:1px solid var(--sage);color:var(--sage-deep);border-radius:100px;padding:9px 15px;font-size:14px;font-weight:600;cursor:pointer;transition:.15s;font-family:inherit}
  .chip:hover{background:var(--sage-soft);transform:translateY(-1px)}
  .chip.warm{border-color:var(--clay);color:var(--clay)}
  .chip.warm:hover{background:var(--clay-soft)}
  .breathe-box{align-self:center;display:flex;flex-direction:column;align-items:center;gap:16px;padding:20px 0 6px}
  .bcircle{width:96px;height:96px;border-radius:50%;background:radial-gradient(circle at 35% 30%, #7da98b, var(--sage));box-shadow:0 0 44px rgba(79,125,94,0.4);transition:transform 3.6s ease-in-out;transform:scale(.8)}
  .bcap{font-family:'Fraunces';font-size:19px;color:var(--sage-deep);min-height:24px}
  .chat-foot{border-top:1px solid var(--line);padding:11px 12px;display:flex;gap:9px;background:var(--bg-2)}
  .chat-foot input{flex:1;border:1px solid var(--line-strong);border-radius:100px;padding:11px 16px;background:var(--surface);font-family:inherit;font-size:14.5px;color:var(--ink);outline:none;transition:border-color .2s}
  .chat-foot input:focus{border-color:var(--sage)}
  .chat-foot button{width:44px;height:44px;border-radius:50%;border:none;background:var(--sage-deep);color:#F4F1E8;font-size:18px;cursor:pointer;flex-shrink:0;transition:.18s}
  .chat-foot button:hover{transform:translateY(-1px);box-shadow:0 6px 16px rgba(60,99,73,0.3)}
  .chat-note{text-align:center;font-size:12.5px;color:var(--faint);margin:16px auto 0;max-width:520px;line-height:1.5}

  /* FEELINGS strip */
  .feelings-sec{padding:64px 0}
  .sec-head{text-align:center;max-width:620px;margin:0 auto 38px}
  .sec-head h2{font-size:clamp(27px,3.8vw,38px);margin-top:12px}
  .sec-head p{color:var(--muted);font-size:16px;margin-top:14px}
  .feelings{display:grid;grid-template-columns:repeat(5,1fr);gap:14px}
  @media(max-width:900px){.feelings{grid-template-columns:repeat(2,1fr)}}
  @media(max-width:520px){.feelings{grid-template-columns:1fr}}
  .feel{background:var(--surface);border:1px solid var(--line);border-radius:var(--radius);padding:22px 18px;cursor:pointer;transition:.2s;text-align:left}
  .feel:hover{border-color:var(--sage);transform:translateY(-4px);box-shadow:0 14px 34px rgba(35,46,39,0.1)}
  .feel .e{font-size:26px;display:block;margin-bottom:12px}
  .feel h4{font-family:'Fraunces';font-size:17px;font-weight:600;margin-bottom:5px}
  .feel p{font-size:13.5px;color:var(--muted);font-style:italic}
  .feel .go{margin-top:12px;font-size:13px;font-weight:600;color:var(--sage-deep)}

  /* reassurance */
  .reassure-sec{padding:10px 0 50px;text-align:center}
  .reassure-card{max-width:680px;margin:0 auto;background:var(--surface);border:1px solid var(--line);border-radius:var(--radius);padding:34px 30px}
  .reassure-card h3{font-family:'Fraunces';font-size:24px;font-weight:600;margin-bottom:12px}
  .reassure-card p{color:var(--muted);font-size:16px}

  /* finder */
  .finder-sec{padding:20px 0 64px}
  .finder-card{max-width:720px;margin:0 auto;background:var(--surface);border:1px solid var(--line-strong);border-radius:22px;padding:34px 30px;box-shadow:0 22px 60px rgba(35,46,39,0.12)}
  @media(max-width:560px){.finder-card{padding:26px 20px}}
  .finder-card h2{font-size:clamp(25px,3.4vw,34px);margin:10px 0 8px}
  .finder-card .lead{color:var(--muted);font-size:15.5px;margin-bottom:22px}
  .finder-card label{display:block;font-size:12px;font-family:'Space Mono';letter-spacing:.1em;text-transform:uppercase;color:var(--faint);margin-bottom:8px}
  .csel{position:relative}
  .csel select{width:100%;appearance:none;background:var(--bg);border:1px solid var(--line-strong);border-radius:12px;
    padding:14px 44px 14px 16px;font-family:inherit;font-size:16px;color:var(--ink);cursor:pointer;outline:none;transition:border-color .2s}
  .csel select:focus{border-color:var(--sage)}
  .csel::after{content:"▾";position:absolute;right:18px;top:50%;transform:translateY(-50%);color:var(--sage);pointer-events:none;font-size:14px}
  .cresult{margin-top:22px;border:1px solid var(--line);border-radius:16px;padding:24px;background:linear-gradient(170deg,var(--sage-soft),var(--bg-2));display:none;animation:rise .45s ease}
  .cresult.show{display:block}
  .cresult .cflag{font-family:'Space Mono';font-size:12px;letter-spacing:.12em;text-transform:uppercase;color:var(--sage-deep)}
  .cresult .corg{font-size:14px;color:var(--muted);margin:4px 0 14px}
  .cnum{display:inline-flex;align-items:center;gap:10px;font-family:'Fraunces';font-weight:600;font-size:clamp(26px,4.4vw,36px);color:var(--ink);text-decoration:none;line-height:1.1}
  .cnum:hover{color:var(--sage-deep)}
  .cnum .call{font-size:14px;font-weight:600;font-family:'Hanken Grotesk';background:var(--sage-deep);color:#F4F1E8;padding:8px 16px;border-radius:100px;white-space:nowrap}
  .chours{font-size:14px;color:var(--muted);margin-top:10px}
  .cextra{list-style:none;margin-top:14px;display:flex;flex-direction:column;gap:8px}
  .cextra li{font-size:14px;color:var(--ink);display:flex;gap:9px;align-items:flex-start}
  .cextra li::before{content:"›";color:var(--sage);font-weight:700;flex-shrink:0}
  .cnote{font-size:14px;color:var(--ink);margin-bottom:8px}
  .ccrisis{margin-top:16px;padding-top:14px;border-top:1px dashed var(--line-strong);font-size:13px;color:var(--muted)}
  .cverify{font-size:11.5px;color:var(--faint);text-align:center;margin-top:16px;line-height:1.5}

  /* resources */
  #resources{background:var(--surface);border-top:1px solid var(--line);padding:46px 0 12px}
  .res-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px}
  @media(max-width:760px){.res-grid{grid-template-columns:1fr}}
  .res h5{font-weight:700;font-size:15px;margin-bottom:8px}
  .res p{font-size:14px;color:var(--muted);line-height:1.6}
  .res p b{color:var(--ink)}
  footer{border-top:1px solid var(--line);margin-top:30px;padding:24px 0;color:var(--faint);font-size:12.5px}
  .foot-inner{max-width:1000px;margin:0 auto;padding:0 24px;display:flex;justify-content:space-between;flex-wrap:wrap;gap:12px;align-items:center}
  .donate{max-width:1000px;margin:18px auto 0;padding:18px 24px 0;border-top:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:14px}
  .donate-line{font-size:12.5px;color:var(--muted);max-width:640px;line-height:1.5}
  .donate-btn{flex-shrink:0;background:var(--clay);color:#FFF6F0;text-decoration:none;font-family:'Hanken Grotesk';font-weight:600;font-size:14px;padding:11px 22px;border-radius:100px;transition:transform .18s ease,box-shadow .25s ease;white-space:nowrap}
  .donate-btn:hover{transform:translateY(-2px);box-shadow:0 8px 22px rgba(188,106,69,0.35)}
  .disclaimer{font-size:11.5px;color:var(--faint);max-width:1000px;margin:14px auto 0;padding:0 24px;line-height:1.55}

  .scroll-reveal{opacity:0;transform:translateY(22px);transition:opacity .8s cubic-bezier(.16,.8,.3,1),transform .8s cubic-bezier(.16,.8,.3,1)}
  .scroll-reveal.in{opacity:1;transform:none}
</style>
</head>
<body>

<nav>
  <div class="nav-inner">
    <div class="logo"><span class="dot"></span>ANCHOR</div>
    <div class="nav-links">
      <a href="#chat" class="q">Talk now</a>
      <a href="#feelings" class="q">The 5 feelings</a>
      <a href="#finder" class="q">Find my helpline</a>
      <a href="#resources" class="help">Get help now</a>
    </div>
  </div>
</nav>

<header class="wrap">
  <div class="eyebrow reveal d1">Free · No sign-up · Private</div>
  <h1 class="hero display reveal d2">When the urge hits,<br>start <em class="serif">here.</em></h1>
  <p class="hero-sub reveal d3">A free, friendly chat for the moment a gambling urge shows up. Tell it what you are feeling, and it will sit with you and help you ride it out. No account, no cost, nothing saved.</p>
  <div class="badges reveal d4">
    <span class="pill"><span class="d"></span>100% free, forever</span>
    <span class="pill"><span class="d"></span>No sign-up</span>
    <span class="pill"><span class="d"></span>Private, runs on your device</span>
    <span class="pill"><span class="d"></span>Here any time</span>
  </div>
</header>

<!-- CHAT -->
<section id="chat" class="chat-section wrap">
  <div class="chat-card reveal d4">
    <div class="chat-head">
      <div class="av">🤍</div>
      <div>
        <div class="name">Anchor</div>
        <div class="sub"><span class="on"></span>here with you · free · private</div>
      </div>
    </div>
    <div class="chat-body" id="chatBody"></div>
    <div class="chat-foot">
      <input type="text" id="chatInput" placeholder="Type how you feel, or tap a button above" autocomplete="off">
      <button id="sendBtn" aria-label="Send">↑</button>
    </div>
  </div>
  <p class="chat-note">Anchor is a supportive companion, not a counselor or a crisis service. Nothing you type is saved or sent anywhere. If you are in danger, call your local emergency number.</p>
</section>

<!-- 5 FEELINGS -->
<section id="feelings" class="feelings-sec wrap">
  <div class="sec-head scroll-reveal">
    <div class="eyebrow">What it is built for</div>
    <h2 class="display">The 5 feelings behind most urges.</h2>
    <p>Urges rarely come from nowhere. They ride in on a feeling. Tap the one that fits and the chat will start right there.</p>
  </div>
  <div class="feelings">
    <div class="feel scroll-reveal" data-node="bored"><span class="e">🌊</span><h4>Bored and restless</h4><p>"I just need something to happen."</p><div class="go">Start here ›</div></div>
    <div class="feel scroll-reveal" data-node="stressed"><span class="e">🌫️</span><h4>Stressed and overwhelmed</h4><p>"I want to switch my brain off."</p><div class="go">Start here ›</div></div>
    <div class="feel scroll-reveal" data-node="chasing"><span class="e">🔁</span><h4>Chasing a loss</h4><p>"I need to win it back."</p><div class="go">Start here ›</div></div>
    <div class="feel scroll-reveal" data-node="lonely"><span class="e">🕳️</span><h4>Lonely or low</h4><p>"There is an emptiness to fill."</p><div class="go">Start here ›</div></div>
    <div class="feel scroll-reveal" data-node="lucky"><span class="e">✨</span><h4>Riding a high</h4><p>"This time, I can feel it."</p><div class="go">Start here ›</div></div>
  </div>
</section>

<!-- REASSURANCE -->
<section class="reassure-sec wrap">
  <div class="reassure-card scroll-reveal">
    <h3 class="display">An urge is a wave, not a command.</h3>
    <p>It rises, it peaks, and it always comes back down, usually within twenty to thirty minutes. You do not have to fight it. You just have to not act while it passes. That is the whole job, and you do not have to do it alone.</p>
  </div>
</section>

<!-- COUNTRY HELPLINE FINDER -->
<section id="finder" class="finder-sec wrap">
  <div class="finder-card scroll-reveal">
    <div class="eyebrow">Find your helpline</div>
    <h2 class="display">Where are you?</h2>
    <p class="lead">Choose your country and I will show you the national gambling help number for where you are. It is free and confidential to call.</p>
    <label for="countrySelect">Your country</label>
    <div class="csel">
      <select id="countrySelect">
        <option value="">Select your country...</option>
        <option value="au">Australia</option>
        <option value="ca">Canada</option>
        <option value="ie">Ireland</option>
        <option value="nz">New Zealand</option>
        <option value="ph">Philippines</option>
        <option value="sg">Singapore</option>
        <option value="za">South Africa</option>
        <option value="uk">United Kingdom</option>
        <option value="us">United States</option>
        <option value="other">My country is not listed</option>
      </select>
    </div>
    <div class="cresult" id="cresult"></div>
    <div class="cverify">Helpline details verified June 2026. Numbers can change. If one does not connect, search "gambling helpline" plus your country, or use findahelpline.com.</div>
  </div>
</section>

<!-- RESOURCES -->
<section id="resources">
  <div class="wrap">
    <div class="eyebrow" style="margin-bottom:22px">Real help, available today</div>
    <div class="res-grid">
      <div class="res scroll-reveal"><h5>Your national helpline</h5><p>Use the <b><a href="#finder" style="color:var(--sage-deep)">helpline finder</a></b> above to get the free, confidential gambling help number for your country, from the Philippines and US to the UK, Australia, and more.</p></div>
      <div class="res scroll-reveal"><h5>Peer support that works</h5><p><b>Gamblers Anonymous</b> runs free meetings, in person and online, around the world. <b>Gam-Anon</b> supports affected family and friends.</p></div>
      <div class="res scroll-reveal"><h5>If you are in crisis</h5><p>If you are thinking about harming yourself, please reach out now. In the US, call or text <b>988</b>. Elsewhere, contact your local emergency number or crisis line.</p></div>
    </div>
  </div>
  <footer>
    <div class="foot-inner">
      <div class="logo" style="font-size:17px"><span class="dot"></span>ANCHOR</div>
      <div>A free chat for gambling urges. No cost, no account, no judgment.</div>
    </div>
    <div class="donate">
      <span class="donate-line">Anchor is free and always will be. If it helped and you are able, a small gift keeps it running. Please never give at the expense of your own bills or recovery.</span>
      <a class="donate-btn" href="https://paypal.me/JKRyan95" target="_blank" rel="noopener noreferrer">🤍 Support Anchor</a>
    </div>
    <div class="disclaimer">Anchor is a free supportive tool and a concept design. It is not a treatment provider, a counselor, or a crisis service, and it is not a substitute for professional care. If you or someone you love is struggling with gambling, please reach out to a qualified service using the resources above. Recovery is possible, and support is real.</div>
  </footer>
</section>

<script>
/* ================= conversation graph ================= */
const nodes = {
  start:{ bot:[
    `Hey. I am Anchor, and I am really glad you are here.`,
    `You do not have to do anything hard right now. Just tell me what this moment feels like, and we will take it from there together.`],
    replies:[
      {label:`I am bored and restless`, to:'bored'},
      {label:`I am stressed and want to escape`, to:'stressed'},
      {label:`I am trying to win back a loss`, to:'chasing'},
      {label:`I feel lonely or low`, to:'lonely'},
      {label:`I feel lucky, like this is the one`, to:'lucky'},
      {label:`I just need to talk to someone`, to:'person', warm:true} ]},

  bored:{ bot:[
    `That restless, itchy boredom is one of the most common reasons an urge shows up. It is not a flaw in you. Your brain is just reaching for the fastest jolt of something.`,
    `Here is the thing: the bet is not really about money right now. It is about filling a gap. And there are ways to fill it that will not cost you tomorrow.`],
    replies:[
      {label:`Help me ride this out`, to:'ride'},
      {label:`Give me something to do instead`, to:'bored_do'},
      {label:`Why does boredom do this?`, to:'bored_why'},
      {label:`Talk to a person`, to:'person', warm:true} ]},
  bored_do:{ bot:[
    `Let us give your brain a different signal. Pick one tiny thing, just for the next ten minutes.`,
    `Walk to the end of the street and back. Or put on one loud song and move. Or text a friend something random. The point is not the activity, it is breaking the loop.`],
    replies:[{label:`Okay, I will try one`, to:'after_action'},{label:`Ride the urge first`, to:'ride'},{label:`Talk to a person`, to:'person', warm:true}]},
  bored_why:{ bot:[
    `Boredom feels uncomfortable because your brain craves stimulation, and gambling offers a fast, unpredictable reward. That is exactly the kind your brain finds hardest to resist.`,
    `Knowing that is power. The craving is a predictable response, not an order. It will pass whether or not you feed it.`],
    replies:[{label:`Help me ride it out`, to:'ride'},{label:`Something to do instead`, to:'bored_do'},{label:`Talk to a person`, to:'person', warm:true}]},

  stressed:{ bot:[
    `When everything feels like too much, an urge can feel like a release valve, a way to make your mind go quiet for a while. That makes complete sense.`,
    `But that relief is a loan with brutal interest. The stress comes back bigger afterwards. Let us find you some real quiet instead, right now.`],
    replies:[{label:`Breathe with me`, to:'breathe'},{label:`Help me ride this out`, to:'ride'},{label:`Why do I want to escape?`, to:'stressed_why'},{label:`Talk to a person`, to:'person', warm:true}]},
  stressed_why:{ bot:[
    `Gambling can flood your system with dopamine and adrenaline, which briefly drowns out stress. Your brain learns that shortcut and offers it up whenever you are overwhelmed.`,
    `The good news is that slower, steadier things calm the same system without the crash. Breathing is the simplest one there is.`],
    replies:[{label:`Breathe with me`, to:'breathe'},{label:`Ride it out`, to:'ride'},{label:`Talk to a person`, to:'person', warm:true}]},

  chasing:{ bot:[
    `I hear you. Wanting to win it back is one of the strongest pulls there is, and one of the most dangerous, because it feels so logical. It is not your fault that it feels this way.`,
    `Here is the hard truth, said gently: the odds do not remember your losses. Chasing almost always deepens the hole instead of filling it. The bravest move right now is to stop the bleeding, not double down.`,
    `The money already gone is already gone. What you can still protect is everything you have not lost yet.`],
    replies:[{label:`Help me not chase right now`, to:'chasing_stop'},{label:`Help me ride this out`, to:'ride'},{label:`I am scared about money`, to:'money'},{label:`Talk to a person`, to:'person', warm:true}]},
  chasing_stop:{ bot:[
    `Let us make it harder to act, just for tonight. Close the app or the tab. Put your phone or your card in another room. Send one honest text to one person about what is happening.`,
    `You do not have to feel calm to do those things. You just have to do them. Future-you will be so relieved that you did.`],
    replies:[{label:`Okay, done`, to:'after_action'},{label:`Breathe with me`, to:'breathe'},{label:`Talk to a person`, to:'person', warm:true}]},
  money:{ bot:[
    `Money fear is heavy, and it makes the urge to chase even louder. But free help exists, and it is not a lecture.`,
    `Nonprofit debt advisers help people through exactly this, confidentially and at no cost. A helpline can point you to one near you tonight.`],
    replies:[{label:`Show me who to call`, to:'person', warm:true},{label:`Ride the urge first`, to:'ride'},{label:`Go back`, to:'chasing'}]},

  lonely:{ bot:[
    `Feeling lonely or low can leave a kind of emptiness, and the urge promises to fill it, even just for a while. Reaching for something in that ache is deeply human.`,
    `But gambling tends to pull you further from people, not closer. Let us reach toward connection instead, even a small bit of it.`],
    replies:[{label:`Help me reach someone`, to:'lonely_reach'},{label:`Help me ride this out`, to:'ride'},{label:`Why does low mood do this?`, to:'lonely_why'},{label:`Talk to a person`, to:'person', warm:true}]},
  lonely_reach:{ bot:[
    `You do not need the perfect person or the perfect words. Pick one name. Send something tiny: "hey, thinking of you," or "rough night, can we talk?"`,
    `If no one feels right, a helpline is a real person who will simply be with you. That counts as connection too.`],
    replies:[{label:`Okay, I will reach out`, to:'after_action'},{label:`Show me the helpline`, to:'person', warm:true},{label:`Ride it out with me`, to:'ride'}]},
  lonely_why:{ bot:[
    `When your mood is low, the brain gets hungry for anything that lifts it, and gambling offers a fast, false lift. It is a trap dressed up as comfort.`,
    `Real lifts are slower: a voice, daylight, movement, being heard. They last longer, and they do not take anything from you.`],
    replies:[{label:`Help me reach someone`, to:'lonely_reach'},{label:`Ride it out`, to:'ride'},{label:`Talk to a person`, to:'person', warm:true}]},

  lucky:{ bot:[
    `That electric, certain feeling, the sense that this time is different, is one of the most convincing tricks the mind plays. I am really glad you stopped to check in instead of acting on it.`,
    `Here is the truth: the lucky feeling has no connection to the outcome. It feels like a signal, but it is just a mood. Every single time, the odds stay exactly the same.`,
    `Riding a high is exactly when people lose the most, because the brakes feel unnecessary. Let us keep your brakes on.`],
    replies:[{label:`Help me let the feeling pass`, to:'ride'},{label:`Why does "lucky" feel so real?`, to:'lucky_why'},{label:`Remind me what is at stake`, to:'lucky_stake'},{label:`Talk to a person`, to:'person', warm:true}]},
  lucky_why:{ bot:[
    `Wins, near-misses, and even the anticipation flood your brain with dopamine, which creates a powerful sense of certainty and momentum. It is chemistry, not insight.`,
    `Some people call it being "in the zone." It is the most expensive feeling there is. Naming it as a chemical high takes away a lot of its power.`],
    replies:[{label:`Help me let it pass`, to:'ride'},{label:`What is at stake`, to:'lucky_stake'},{label:`Talk to a person`, to:'person', warm:true}]},
  lucky_stake:{ bot:[
    `Take ten seconds. Picture tomorrow morning if you do not bet tonight: the relief, the money still there, the streak of clean days you are protecting.`,
    `You do not have to win anything tonight. You already did, just by stopping here.`],
    replies:[{label:`That helps`, to:'after_action'},{label:`Help me ride it out`, to:'ride'},{label:`Talk to a person`, to:'person', warm:true}]},

  ride:{ bot:[
    `Okay. Let us ride this out together. Hold onto one thing: an urge is a wave. It rises, it peaks, and it always comes back down, usually within twenty to thirty minutes, often less.`,
    `You do not have to fight it or push it away. You only have to not act while it passes. I will stay right here. Want a tool to make the waiting easier?`],
    replies:[{label:`Breathe with me`, to:'breathe'},{label:`Do a grounding exercise`, to:'ground'},{label:`I can wait it out`, to:'after_action'},{label:`It is too strong, I need a person`, to:'person', warm:true}]},

  breathe:{ bot:[`Let us breathe together. Follow the circle: in as it grows, hold, out as it shrinks. Just a few slow rounds.`], widget:'breathe' },
  breathe_after:{ bot:[`Nicely done. Even a little slower is a real win. How is the urge now?`],
    replies:[{label:`A bit softer`, to:'softer'},{label:`Still strong`, to:'still_strong'},{label:`Let us do grounding too`, to:'ground'}]},

  ground:{ bot:[`Let us anchor you in the room you are in. We will go one step at a time.`,`Look around and name, out loud or in your head, five things you can see.`],
    replies:[{label:`Done, that is five`, to:'ground4'}]},
  ground4:{ bot:[`Good. Now four things you can physically feel. The chair, your feet on the floor, the air, your own hands.`], replies:[{label:`Done`, to:'ground3'}]},
  ground3:{ bot:[`Three things you can hear, even faint ones.`], replies:[{label:`Done`, to:'ground2'}]},
  ground2:{ bot:[`Two things you can smell, or two smells you like.`], replies:[{label:`Done`, to:'ground1'}]},
  ground1:{ bot:[`One slow breath, all the way out. You are here, in this room, and the urge is already a little further away.`], replies:[{label:`How am I doing?`, to:'grounded_after'}]},
  grounded_after:{ bot:[`You just rode a big part of the wave. How is the urge now?`],
    replies:[{label:`A bit softer`, to:'softer'},{label:`Still strong`, to:'still_strong'},{label:`Breathe too`, to:'breathe'}]},

  softer:{ bot:[
    `That is huge. You felt an urge and you did not let it drive. That is exactly how recovery gets built, one passed urge at a time.`,
    `Be gentle with yourself tonight. If it rises again, come right back here. I am always on, free, and not going anywhere.`],
    replies:[{label:`Start over`, to:'start'},{label:`Show me human support`, to:'person', warm:true},{label:`I am okay for now`, to:'end'}]},
  still_strong:{ bot:[
    `Thank you for being honest, and for still being here instead of acting. That takes real strength.`,
    `When an urge stays loud, the strongest move is a human voice. A free, confidential helpline has people who do exactly this, right now. Let me put it in front of you.`],
    replies:[{label:`Show me the helpline`, to:'person', warm:true},{label:`Try breathing again`, to:'breathe'},{label:`Try grounding`, to:'ground'}]},

  after_action:{ bot:[
    `That is a real step, and it matters more than it feels like right now.`,
    `Want to ride out whatever is left of the urge with me, or are you steadier?`],
    replies:[{label:`Ride it out`, to:'ride'},{label:`I am a bit steadier`, to:'softer'},{label:`Talk to a person`, to:'person', warm:true}]},

  person:{ bot:[
    `Talking to a real person is one of the strongest things you can do right now, and it is free.`,
    `In the US, you can call or text <b>1-800-GAMBLER</b> any time, day or night. It is free, confidential, and judgment-free.`,
    `<b>Gamblers Anonymous</b> holds free meetings, in person and online, in many countries. And if there is someone you trust, one honest text to them can change the whole night.`,
    `If you are outside the US, searching "gambling helpline" with your country will find your local line.`],
    replies:[{label:`That helps, thank you`, to:'softer'},{label:`Back to the start`, to:'start'},{label:`Stay and breathe with me`, to:'breathe'}]},

  crisis:{ bot:[
    `I am really glad you told me. You matter, and you do not have to carry this alone.`,
    `If any part of you is thinking about harming yourself, please reach out to a real person right now. In the US, call or text <b>988</b>, any time. Outside the US, your local emergency number or a crisis line can help.`,
    `I am still right here with you. Would it help to breathe together for a moment, or to see who you can call?`],
    replies:[{label:`Breathe with me`, to:'breathe'},{label:`Who can I call?`, to:'person', warm:true},{label:`Take me back`, to:'start'}]},

  end:{ bot:[
    `I am glad you stopped here. Whatever happens next, this moment, where you chose to pause, is yours to keep.`,
    `Come back any time. I am free, private, and always on. Take care of yourself. 🤍`],
    replies:[{label:`Start again`, to:'start'}]}
};

/* ================= engine ================= */
const body=document.getElementById('chatBody');
const input=document.getElementById('chatInput');
const sendBtn=document.getElementById('sendBtn');
let currentReplies=[]; let busy=false;
const crisisRe=/(suicide|suicidal|kill myself|killing myself|end my life|end it all|don'?t want to (live|be here|exist)|want to die|better off dead|hurt myself|harm myself|hurting myself)/i;

function scrollDown(){ body.scrollTop=body.scrollHeight; }
function bubble(cls, html){ const d=document.createElement('div'); d.className='msg '+cls; d.innerHTML=html; body.appendChild(d); scrollDown(); return d; }
function userSay(t){ bubble('user', escapeHtml(t)); }
function escapeHtml(s){ return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

let typingEl=null;
function showTyping(){ typingEl=document.createElement('div'); typingEl.className='typing'; typingEl.innerHTML='<span></span><span></span><span></span>'; body.appendChild(typingEl); scrollDown(); }
function hideTyping(){ if(typingEl){ typingEl.remove(); typingEl=null; } }
function typingTime(line){ return Math.min(1500, Math.max(650, 480 + line.length*11)); }

function clearReplies(){ const r=body.querySelector('.replies'); if(r) r.remove(); }
function showReplies(items){
  clearReplies();
  currentReplies=items;
  const row=document.createElement('div'); row.className='replies';
  items.forEach(it=>{
    const b=document.createElement('button'); b.className='chip'+(it.warm?' warm':''); b.textContent=it.label;
    b.addEventListener('click', ()=>{ if(busy) return; clearReplies(); userSay(it.label); if(it.fn){ it.fn(); } else { go(it.to); } });
    row.appendChild(b);
  });
  body.appendChild(row); scrollDown();
}

function botSequence(lines, done){
  busy=true; input.disabled=true;
  let i=0;
  (function next(){
    if(i>=lines.length){ busy=false; input.disabled=false; if(done) done(); return; }
    showTyping();
    const line=lines[i++];
    setTimeout(()=>{ hideTyping(); bubble('bot', line); setTimeout(next, 340); }, typingTime(line));
  })();
}

function go(id){
  const n=nodes[id];
  if(!n) return;
  botSequence(n.bot, ()=>{
    if(n.widget==='breathe'){ runBreathing(()=>go('breathe_after')); }
    else if(n.replies){ showReplies(n.replies); }
  });
}

/* breathing widget */
function runBreathing(onDone){
  const box=document.createElement('div'); box.className='breathe-box';
  const circle=document.createElement('div'); circle.className='bcircle';
  const cap=document.createElement('div'); cap.className='bcap'; cap.textContent='Get ready...';
  box.appendChild(circle); box.appendChild(cap); body.appendChild(box); scrollDown();
  const phases=[['Breathe in','grow'],['Hold','hold'],['Breathe out','shrink'],['Hold','hold']];
  let k=0;
  function step(){
    const ph=phases[k%4]; cap.textContent=ph[0];
    if(ph[1]==='grow') circle.style.transform='scale(1.65)';
    else if(ph[1]==='shrink') circle.style.transform='scale(0.8)';
    k++;
  }
  step(); const iv=setInterval(step,4000);
  currentReplies=[];
  const row=document.createElement('div'); row.className='replies';
  const done=document.createElement('button'); done.className='chip'; done.textContent='I am done breathing';
  done.addEventListener('click', ()=>{ clearInterval(iv); row.remove(); cap.textContent='Well done.'; circle.style.transform='scale(1)'; onDone(); });
  row.appendChild(done); body.appendChild(row); scrollDown();
}

/* free-text input */
function handleInput(){
  const val=input.value.trim(); if(!val || busy) return;
  input.value=''; userSay(val);
  if(crisisRe.test(val)){ clearReplies(); go('crisis'); return; }
  clearReplies();
  botSequence([`I hear you, and I am glad you said it out loud. I might not catch every word just right, but I am here with you. Tap whichever of these fits, and we will go from there.`], ()=>{
    if(currentReplies && currentReplies.length){ showReplies(currentReplies); }
    else { showReplies(nodes.start.replies); }
  });
}
sendBtn.addEventListener('click', handleInput);
input.addEventListener('keydown', e=>{ if(e.key==='Enter'){ e.preventDefault(); handleInput(); } });

/* feeling cards jump into chat */
document.querySelectorAll('.feel').forEach(card=>card.addEventListener('click', ()=>{
  document.getElementById('chat').scrollIntoView({behavior:'smooth', block:'start'});
  body.innerHTML=''; clearReplies();
  setTimeout(()=>go(card.dataset.node), 450);
}));

/* scroll reveal */
const io=new IntersectionObserver(es=>es.forEach(e=>{ if(e.isIntersecting){ e.target.classList.add('in'); io.unobserve(e.target); } }),{threshold:.14});
document.querySelectorAll('.scroll-reveal').forEach(el=>io.observe(el));

/* ================= country helpline finder ================= */
const HELPLINES={
  us:{country:'United States',org:'National Problem Gambling Helpline (NCPG)',num:'1-800-GAMBLER',tel:'18004262537',hours:'24/7, free and confidential',extra:['Call or text the same number','Live chat at ncpg.org']},
  uk:{country:'United Kingdom',org:'National Gambling Helpline (GamCare)',num:'0808 8020 133',tel:'08088020133',hours:'24/7, free',extra:['Call, WhatsApp, or live chat at gamcare.org.uk']},
  ie:{country:'Ireland',org:'National Gambling Helpline (Gamblingcare.ie)',num:'1800 936 725',tel:'1800936725',hours:'9am to 11pm daily, free',extra:['Gamblers Anonymous Ireland: 01 872 1133']},
  au:{country:'Australia',org:'National Gambling Helpline (Gambling Help Online)',num:'1800 858 858',tel:'1800858858',hours:'24/7, free',extra:['Live chat at gamblinghelponline.org.au']},
  nz:{country:'New Zealand',org:'Gambling Helpline',num:'0800 654 655',tel:'0800654655',hours:'24/7, free',extra:['Free text 8006','Live chat at gamblinghelpline.co.nz']},
  sg:{country:'Singapore',org:'National Problem Gambling Helpline (NCPG)',num:'1800-6-668-668',tel:'18006668668',hours:'Daily 8am to 11pm, free',extra:['Webchat at ncpg.org.sg']},
  ph:{country:'Philippines',org:'National Problem Gambling Helpline (PAGCOR)',num:'(02) 8248-9568',tel:'+63282489568',hours:'24/7, free and confidential',extra:['Gamblers Anonymous Philippines: info@gaphilippines.org','Gam-Anon Philippines: gam-anonphilippines.org']},
  za:{country:'South Africa',org:'National Responsible Gambling Programme (SARGF)',num:'0800 006 008',tel:'0800006008',hours:'24/7, free',extra:['WhatsApp or SMS "HELP" to 076 675 0710']},
  ca:{country:'Canada',org:'Support is organised by province, all free and confidential',list:[
    'Ontario (ConnexOntario): 1-866-531-2600, 24/7, text 247247',
    'British Columbia: 1-888-795-6111, 24/7',
    'Quebec (Aide aux joueurs): 1-800-461-0140, 24/7',
    'Other provinces: visit ccsa.ca to find your local line']},
  other:{country:'Your country',org:'Help exists almost everywhere, even if it is not listed here',list:[
    'Gamblers Anonymous holds free meetings worldwide: gamblersanonymous.org',
    'Find your local helpline at findahelpline.com (search the "gambling" topic)',
    'Or search "gambling helpline" plus your country name']}
};
const sel=document.getElementById('countrySelect');
const cres=document.getElementById('cresult');
function renderHelpline(code){
  const h=HELPLINES[code];
  if(!h){ cres.classList.remove('show'); cres.innerHTML=''; return; }
  let html='<div class="cflag">'+h.country+'</div><div class="corg">'+h.org+'</div>';
  if(h.num){
    html+='<a class="cnum" href="tel:'+h.tel+'">'+h.num+'<span class="call">Tap to call</span></a>';
    html+='<div class="chours">'+h.hours+'</div>';
  }
  const items=h.extra||h.list||[];
  if(items.length){
    html+='<ul class="cextra">'+items.map(x=>'<li>'+x+'</li>').join('')+'</ul>';
  }
  html+='<div class="ccrisis">If you are in immediate danger or thinking about harming yourself, contact your local emergency number right now.</div>';
  cres.innerHTML=html; cres.classList.add('show');
}
sel.addEventListener('change', e=>renderHelpline(e.target.value));

/* boot */
setTimeout(()=>go('start'), 500);
</script>
</body>
</html>
