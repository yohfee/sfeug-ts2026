---
marp: true
theme: default
paginate: true
style: |
  @import url("https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Mochiy+Pop+One&family=Noto+Sans+JP:wght@400;700;900&display=swap");

  /* ==================== tokens ==================== */
  :root {
    --bg: #0b0d12;
    --surface: #141824;
    --border: #262c3d;
    --bar: #3a4152;
    --fg: #e8eaf0;
    --muted: #8b93a7;
    --code-fg: #d6deeb;

    --red: #ff3d3d;
    --red-soft: rgba(255, 61, 61, .14);
    --red-line: rgba(255, 61, 61, .18);
    --red-text: #ff8080;
    --yellow: #ffd23f;
    --yellow-soft: rgba(255, 210, 63, .14);
    --green: #3ddc84;
    --green-soft: rgba(61, 220, 132, .12);
    --green-border: rgba(61, 220, 132, .5);

    --font-sans: "Noto Sans JP", sans-serif;
    --font-mono: "JetBrains Mono", monospace;

    /* コードブロックの寸法（行に帯を引くときの基準） */
    --pre-top: 56px;
    --pre-line: calc(24px * 1.55);
  }

  /* ==================== base ==================== */
  section {
    background: var(--bg);
    color: var(--fg);
    font-family: var(--font-sans);
    font-size: 28px;
    line-height: 1.6;
    padding: 64px 80px;
    align-content: start;
  }
  section strong { color: var(--yellow); }

  /* ページ番号 */
  section::after {
    color: var(--muted);
    font-family: var(--font-mono);
    font-size: 18px;
  }

  section h1, section h2, section h3 {
    color: var(--fg);
    font-weight: 900;
    border: none;
    margin: 0 0 .5em;
    letter-spacing: .01em;
  }
  section h2 {
    font-size: 44px;
    line-height: 1.3;
    padding-left: 24px;
    border-left: 10px solid var(--bar);
  }

  /* ---------- code ---------- */
  section code {
    font-family: var(--font-mono);
    /* 合字を切る（<= が ≤ に見えないように） */
    font-variant-ligatures: none;
    font-feature-settings: "liga" 0, "calt" 0;
  }
  section :not(pre) > code {
    background: var(--yellow-soft);
    color: var(--yellow);
    font-size: .9em;
    padding: .1em .4em;
    border-radius: 6px;
  }

  /* コードブロック（ターミナル風ウィンドウ） */
  section pre {
    position: relative;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: var(--pre-top) 28px 24px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, .5);
    font-size: 24px;
    line-height: 1.55;
  }
  /* 信号機の 3 つの丸 */
  section pre::before {
    content: "";
    position: absolute;
    top: 20px; left: 24px;
    width: 14px; height: 14px;
    border-radius: 50%;
    background: #ff5f56;
    box-shadow: 24px 0 #ffbd2e, 48px 0 #27c93f;
  }
  section pre code {
    background: none;
    color: var(--code-fg);
  }

  /* シンタックスハイライト */
  section .hljs-keyword, section .hljs-built_in { color: #c792ea; }
  section .hljs-string { color: #ecc48d; }
  section .hljs-number, section .hljs-literal { color: #f78c6c; }
  section .hljs-title { color: #82aaff; }
  section .hljs-comment { color: var(--red); font-style: normal; font-weight: 700; }
  section .hljs-variable, section .hljs-params { color: var(--code-fg); }
  section .hljs-deletion { color: var(--red-text); background: none; }
  section .hljs-addition { color: var(--green); background: none; }

  /* ---------- list ---------- */
  section ul { padding-left: 1.2em; }
  section li::marker { color: var(--red); }
  section li > ul { margin-top: .2em; }
  section li > ul > li { color: var(--muted); font-size: .9em; }
  section li > ul > li::marker { color: var(--muted); }

  /* ---------- blockquote（強調の囲み） ---------- */
  section blockquote {
    margin: 1em 0 0;
    padding: 20px 28px;
    background: var(--red-soft);
    border: none;
    border-left: 8px solid var(--red);
    border-radius: 0 12px 12px 0;
    color: var(--fg);
    font-weight: 700;
  }
  section blockquote p { margin: 0; }

  /* ---------- table（2 列目 = 旧、3 列目 = 新、最終行 = 結果） ---------- */
  section table {
    display: table;
    width: 100%;
    border-collapse: collapse;
    font-size: 26px;
  }
  section table tr { background: transparent !important; }
  section table th, section table td {
    padding: 18px 20px;
    background: transparent;
    border: none;
    border-bottom: 1px solid var(--border);
    color: var(--fg);
  }
  section table th { color: var(--muted); font-size: .85em; text-transform: uppercase; }
  section table th:nth-child(2) { color: #8dd0ff; }
  section table th:nth-child(3) { color: #bd9bff; }
  section table tr:last-child td { border-bottom: none; font-size: 1.1em; font-weight: 900; }
  section table tr:last-child td:nth-child(3) { color: var(--red); }

  /* ---------- 成功 / 失敗のバッジ（quiz・verify で共用） ---------- */
  section.quiz li,
  section.verify pre:nth-of-type(1)::after {
    background: var(--green-soft);
    border: 1px solid var(--green-border);
    border-radius: 999px;
    color: var(--green);
    font-weight: 700;
  }
  section.quiz ul:nth-of-type(2) li:last-child,
  section.verify pre:nth-of-type(2)::after {
    background: var(--red);
    border: 1px solid var(--red);
    border-radius: 999px;
    color: #fff;
    font-weight: 700;
  }

  /* ==================== 中央寄せのスライド ==================== */
  section.profile, section.title, section.impact, section.finale {
    align-content: center;
  }
  section.profile, section.impact, section.finale {
    align-items: center;
    text-align: center;
  }

  /* profile: 自己紹介 */
  section.profile img {
    border: 6px solid var(--red);
    border-radius: 50%;
    box-shadow: 0 0 0 12px rgba(255, 61, 61, .2);
  }
  section.profile h1 { font-size: 64px; margin: .6em 0 .1em; }
  section.profile h3 { color: var(--muted); font-weight: 700; margin: 0 0 1em; }
  section.profile p:last-child { color: var(--yellow); font-weight: 700; }

  /* title: 表紙 */
  section.title { padding: 80px 100px; }
  section.title h1 { font-size: 66px; line-height: 1.25; }
  section.title h1 strong { color: var(--red); font-size: 1.25em; }
  section.title p { color: var(--muted); font-size: 26px; }

  /* impact: 特大文字（h2 = 前置き、h1 = 本題、p = 補足） */
  section.impact h2 {
    padding: 0;
    border: none;
    color: var(--muted);
    font-size: 36px;
  }
  section.impact h1 {
    color: var(--red);
    font-size: 110px;
    line-height: 1.2;
  }
  section.impact p { color: var(--muted); }

  /* impact の色・サイズ違い */
  section.quiet h1 { color: var(--fg); font-size: 96px; }
  /* rant: 集中線の中で叫ぶ（1 行目 = ぼやき、2 行目 = 叫び） */
  section.rant { overflow: hidden; }
  /* 集中線（揺らすために疑似要素に分ける） */
  section.rant::before {
    content: "";
    display: block;
    position: absolute;
    inset: -20%;
    background:
      radial-gradient(ellipse 33% 32% at 50% 50%, var(--bg) 55%, transparent 100%),
      repeating-conic-gradient(from 0deg at 50% 50%, rgba(255, 255, 255, .22) 0 .5deg, transparent .5deg 3.1deg),
      repeating-conic-gradient(from 1deg at 50% 50%, rgba(255, 61, 61, .25) 0 .8deg, transparent .8deg 7.3deg);
    animation: rant-rays .12s steps(1) infinite;
  }
  /* 着地の瞬間に画面を赤く光らせ、画面ごと揺らす */
  section.rant {
    animation:
      rant-flash .5s .45s ease-out both,
      rant-quake .2s .45s linear infinite;
  }
  section.rant h1 {
    position: relative;
    color: var(--red);
    font-size: 74px;
    line-height: 1.5;
    white-space: nowrap;
    transform: rotate(-3deg);
    text-shadow: 0 0 40px rgba(255, 61, 61, .55), 6px 6px 0 #000;
    /* 叩きつけて着地 → 震え続ける＋色ずれ */
    animation:
      rant-slam .45s cubic-bezier(.2, 2, .4, 1) both,
      rant-shake .08s .45s linear infinite,
      rant-glitch .3s .45s steps(1) infinite;
  }
  section.rant h1::first-line {
    color: var(--fg);
    font-size: 50px;
  }
  @keyframes rant-slam {
    from { opacity: 0; transform: rotate(-30deg) scale(6); }
    to   { opacity: 1; transform: rotate(-3deg) scale(1); }
  }
  @keyframes rant-shake {
    0%, 100% { transform: rotate(-3deg) translate(0, 0) scale(1); }
    25% { transform: rotate(-4.5deg) translate(-8px, 5px) scale(1.03); }
    50% { transform: rotate(-1.5deg) translate(7px, -6px) scale(.98); }
    75% { transform: rotate(-3.8deg) translate(-5px, -7px) scale(1.02); }
  }
  @keyframes rant-glitch {
    0%   { text-shadow: 0 0 40px rgba(255, 61, 61, .55), 6px 6px 0 #000; }
    33%  { text-shadow: -6px 0 0 #00e5ff, 6px 0 0 #ff00aa, 6px 6px 0 #000; }
    66%  { text-shadow: 0 0 60px rgba(255, 61, 61, .9), -6px -4px 0 #000; }
  }
  @keyframes rant-rays {
    0%   { transform: rotate(0deg) scale(1); }
    33%  { transform: rotate(3deg) scale(1.08); }
    66%  { transform: rotate(-2deg) scale(1.04); }
  }
  @keyframes rant-flash {
    from { background-color: #ff3d3d; }
    to   { background-color: var(--bg); }
  }
  @keyframes rant-quake {
    0%, 100% { translate: 0 0; }
    25% { translate: -5px 3px; }
    50% { translate: 4px -4px; }
    75% { translate: -3px -2px; }
  }
  /* PDF 書き出しでは止めて、着地した状態にする */
  @media print {
    section.rant, section.rant::before, section.rant h1 { animation: none; }
  }
  section.relief h1 { color: var(--green); font-size: 80px; }
  section.missing h1 { font-size: 92px; line-height: 1.4; }
  section.missing h1 code { font-size: .85em; padding: 0 .25em; }

  section.whiteout { background: #fff; color: #111; }
  section.whiteout h1 { color: #111; }
  section.whiteout h2, section.whiteout p { color: #b0b4bd; }

  /* ==================== quiz: 静的チェック / 実行結果 ==================== */
  section.quiz ul {
    display: flex;
    align-items: center;
    gap: 14px;
    margin: 0 0 14px;
    padding: 0;
    list-style: none;
  }
  section.quiz ul:nth-of-type(1) { margin-top: 12px; }
  section.quiz ul::before {
    width: 150px;
    color: var(--muted);
    font-size: 20px;
    font-weight: 700;
  }
  section.quiz ul:nth-of-type(1)::before { content: "静的チェック"; }
  section.quiz ul:nth-of-type(2)::before { content: "実行結果"; }
  section.quiz li {
    margin: 0;
    padding: 4px 22px;
    font-size: 24px;
  }
  section.quiz li::before { content: "✔ "; }
  section.quiz ul:nth-of-type(2) li:last-child::before { content: "✘ "; }

  /* ==================== console: コンソールのエラー表示 ==================== */
  section.console blockquote {
    position: relative;
    margin-top: 8px;
    padding: 48px 28px 20px 72px;
    background: #2a1215;
    border: 1px solid #5c1f24;
    border-left: 8px solid var(--red);
    border-radius: 12px;
    font-weight: 400;
  }
  section.console blockquote::before {
    content: "Console";
    position: absolute;
    top: 12px; left: 28px;
    color: var(--muted);
    font-size: 18px;
    font-weight: 700;
    letter-spacing: .08em;
  }
  section.console blockquote::after {
    content: "✘";
    position: absolute;
    left: 24px; bottom: 21px;
    width: 32px; height: 32px;
    border-radius: 50%;
    background: var(--red);
    color: #fff;
    font-size: 18px;
    line-height: 32px;
    text-align: center;
  }
  section.console blockquote code {
    padding: 0;
    background: none;
    color: var(--red-text);
    font-size: 26px;
  }

  /* verify: var / const の比較（console と併用） */
  section.verify pre:nth-of-type(1) { margin-bottom: 36px; }
  /* const のコードとエラーを 1 つのまとまりに繋げる */
  section.verify pre:nth-of-type(2) {
    margin-bottom: 0;
    border-bottom: none;
    border-radius: 14px 14px 0 0;
  }
  section.verify blockquote {
    margin-top: 0;
    border-radius: 0 0 12px 12px;
  }
  /* ウィンドウのタイトルバーに結果バッジ */
  section.verify pre::after {
    position: absolute;
    top: 12px; right: 20px;
    padding: 2px 14px;
    font-family: var(--font-sans);
    font-size: 18px;
    line-height: 1.6;
  }
  section.verify pre:nth-of-type(1)::after { content: "✔ var：動く"; }
  section.verify pre:nth-of-type(2)::after { content: "✘ const：ReferenceError"; }

  /* ==================== コードの行に帯を引く ==================== */
  /* answer: 1 つ目のコードの 3 行目（バグの行）を赤く */
  section.answer pre:first-of-type {
    --from: calc(var(--pre-top) + var(--pre-line) * 2);
    --to: calc(var(--pre-top) + var(--pre-line) * 3);
    background:
      linear-gradient(transparent var(--from), var(--red-line) var(--from), var(--red-line) var(--to), transparent var(--to)),
      var(--surface);
  }
  /* answer / aside: 最後のコードは diff（1 行目 = 削除、2 行目 = 追加） */
  section.answer pre:last-of-type,
  section.aside pre:last-of-type {
    --mid: calc(var(--pre-top) + var(--pre-line));
    --end: calc(var(--pre-top) + var(--pre-line) * 2);
    padding-bottom: 12px;
    background:
      linear-gradient(transparent var(--pre-top), var(--red-soft) var(--pre-top), var(--red-soft) var(--mid), var(--green-soft) var(--mid), var(--green-soft) var(--end), transparent var(--end)),
      var(--surface);
  }
  section.aside p:last-of-type { color: var(--muted); font-size: 24px; }

  /* ==================== es5: var の強調と流れ図 ==================== */
  section.es5 pre code > .hljs-keyword:first-child {
    color: var(--yellow);
    background: var(--yellow-soft);
    border-radius: 4px;
    box-shadow: 0 0 0 4px var(--yellow-soft);
  }
  section.es5 ol {
    display: flex;
    align-items: center;
    margin: .4em 0 0;
    padding: 0;
    list-style: none;
  }
  section.es5 ol li {
    position: relative;
    margin: 0;
    padding: 10px 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    font-size: 24px;
  }
  section.es5 ol li + li { margin-left: 48px; }
  section.es5 ol li + li::before {
    content: "→";
    position: absolute;
    left: -38px;
    color: var(--muted);
  }
  section.es5 ol li:last-child { border-color: var(--yellow); }
  section.es5 ol code { padding: 0; background: none; }

  /* ==================== cards: 縦積みカード ==================== */
  section.cards > ul {
    display: flex;
    flex-direction: column;
    gap: 16px;
    margin-top: .2em;
    padding: 0;
    list-style: none;
  }
  section.cards > ul > li {
    margin: 0;
    padding: 14px 28px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-left: 8px solid var(--red);
    border-radius: 12px;
    font-weight: 900;
    line-height: 1.4;
  }
  section.cards > ul > li > ul {
    margin-top: .3em;
    padding: 0;
    list-style: none;
  }
  section.cards > ul > li > ul > li {
    margin: 0;
    font-size: 21px;
    font-weight: 400;
    line-height: 1.5;
  }

  /* suspects: 「容疑者 A/B/C」のラベル付き */
  section.suspects > ul { counter-reset: suspect; }
  section.suspects > ul > li { counter-increment: suspect; }
  section.suspects > ul > li::before {
    content: "容疑者 " counter(suspect, upper-alpha);
    margin-right: 14px;
    padding: 2px 12px;
    border: 1px solid var(--red);
    border-radius: 6px;
    color: var(--red);
    font-size: 18px;
    font-weight: 700;
    vertical-align: middle;
  }
  section.suspects > ul > li > em {
    margin-left: 10px;
    color: var(--yellow);
    font-style: normal;
  }

  /* lessons: 01, 02, ... の番号付き */
  section.lessons > ul { counter-reset: lesson; gap: 20px; }
  section.lessons > ul > li {
    position: relative;
    counter-increment: lesson;
    padding: 18px 28px 18px 112px;
    border-left-color: var(--yellow);
  }
  section.lessons > ul > li::before {
    content: "0" counter(lesson);
    position: absolute;
    left: 28px; top: 50%;
    transform: translateY(-50%);
    color: var(--yellow);
    font-family: var(--font-mono);
    font-size: 48px;
    line-height: 1;
  }

  /* reasons: 一言だけの大きめカード */
  section.reasons > ul { gap: 28px; margin-top: 40px; }
  section.reasons > ul > li { padding: 36px 40px; font-size: 40px; }

  /* ==================== punch: オチの画像 ==================== */
  section.punch { background: #efefef; }

  /* ゴゴゴ…（ジョジョ風の書き文字。1 文字ずつ現れて脈打つ） */
  section.punch ul {
    position: absolute;
    inset: 0;
    margin: 0;
    padding: 0;
    list-style: none;
  }
  section.punch li {
    position: absolute;
    left: var(--x); top: var(--y);
    margin: 0;
    color: #3d1060;
    font-family: var(--font-sans);
    font-size: var(--s);
    font-weight: 900;
    line-height: 1;
    -webkit-text-stroke: 10px #fff;
    paint-order: stroke fill;
    text-shadow: 6px 6px 0 #000;
    transform: rotate(var(--r)) skewX(-10deg);
    animation:
      gogo-in .25s var(--d) cubic-bezier(.2, 2.2, .4, 1) both,
      gogo-pulse .35s calc(var(--d) + .25s) linear infinite;
  }
  /* 左の余白に 2 つ、右下に 5 つ（だんだん大きく斜めに上がる） */
  section.punch li:nth-child(1) { --x: 24px;   --y: 150px; --s: 84px;  --r: -10deg; --d: 0s; }
  section.punch li:nth-child(2) { --x: 34px;   --y: 330px; --s: 92px;  --r: 8deg;   --d: .25s; }
  section.punch li:nth-child(3) { --x: 600px;  --y: 560px; --s: 92px;  --r: -8deg;  --d: .5s; }
  section.punch li:nth-child(4) { --x: 730px;  --y: 470px; --s: 104px; --r: 10deg;  --d: .75s; }
  section.punch li:nth-child(5) { --x: 870px;  --y: 545px; --s: 116px; --r: -6deg;  --d: 1s; }
  section.punch li:nth-child(6) { --x: 1000px; --y: 430px; --s: 128px; --r: 12deg;  --d: 1.25s; }
  section.punch li:nth-child(7) { --x: 1120px; --y: 520px; --s: 140px; --r: -8deg;  --d: 1.5s; }
  @keyframes gogo-in {
    from { opacity: 0; transform: rotate(calc(var(--r) * -4)) skewX(-10deg) scale(5); }
    to   { opacity: 1; transform: rotate(var(--r)) skewX(-10deg) scale(1); }
  }
  /* 脈打ちながらガタガタ震える */
  @keyframes gogo-pulse {
    0%, 100% { transform: translate(0, 0) rotate(var(--r)) skewX(-10deg) scale(1); }
    20% { transform: translate(-5px, 4px) rotate(calc(var(--r) - 3deg)) skewX(-10deg) scale(1.1); }
    40% { transform: translate(6px, -3px) rotate(calc(var(--r) + 3deg)) skewX(-10deg) scale(1.25); }
    60% { transform: translate(-4px, -5px) rotate(calc(var(--r) - 2deg)) skewX(-10deg) scale(1.15); }
    80% { transform: translate(4px, 5px) rotate(calc(var(--r) + 2deg)) skewX(-10deg) scale(1.05); }
  }
  @media print {
    section.punch li { animation: none; }
  }

  /* ==================== finale: 昔のワードアート風（わざとダサく） ==================== */
  section.finale {
    padding: 40px;
    background:
      radial-gradient(circle, rgba(255, 255, 255, .7) 4px, transparent 5px) 0 0 / 48px 48px,
      linear-gradient(135deg, #ff66cc, #ffff66, #66ffff, #ff66cc, #ffff66, #66ffff) 0 0 / 300% 300%;
    /* 背景が流れ続けて、色もぐるぐる変わる */
    animation: finale-bg 1.5s linear infinite;
  }
  /* 散らばる星のクリップアート（1 つの ★ を text-shadow で複製） */
  section.finale::before {
    content: "★";
    position: absolute;
    top: 20px; left: 40px;
    color: #ffff00;
    font-size: 90px;
    line-height: 1;
    text-shadow:
      1080px 10px 0 #ff00ff,
      30px 540px 0 #00ffff,
      1100px 560px 0 #ff3300,
      560px -40px 0 #00ff00,
      300px 600px 0 #ffff00;
    animation:
      finale-blink .4s steps(1) infinite,
      finale-jitter .2s linear infinite;
  }
  section.finale h1 {
    --shadow:
      drop-shadow(0 0 0 #fff) drop-shadow(3px 3px 0 #000080) drop-shadow(3px 3px 0 #000080)
      drop-shadow(3px 3px 0 #000080) drop-shadow(8px 8px 6px rgba(0, 0, 0, .6));
    font-family: "HGS創英角ﾎﾟｯﾌﾟ体", "HG創英角ﾎﾟｯﾌﾟ体", "Mochiy Pop One", sans-serif;
    font-size: 160px;
    font-weight: 400;
    line-height: 1.2;
    letter-spacing: 0;
    white-space: nowrap;
    background: linear-gradient(180deg, #ff0000, #ff9900, #ffff00, #00cc00, #0066ff, #9900ff);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    -webkit-text-stroke: 4px #000080;
    filter: var(--shadow);
    transform: perspective(600px) rotateX(18deg) rotate(-3deg);
    /* 回転しながら飛び込み → 色が高速で回り、ぐわんぐわん揺れる */
    animation:
      finale-in .8s cubic-bezier(.2, 1.8, .4, 1) both,
      finale-rainbow .6s linear infinite,
      finale-wobble 1s .8s ease-in-out infinite;
  }
  @keyframes finale-in {
    from { opacity: 0; transform: perspective(600px) rotateX(18deg) rotate(-723deg) scale(0); }
    to   { opacity: 1; transform: perspective(600px) rotateX(18deg) rotate(-3deg) scale(1); }
  }
  @keyframes finale-rainbow {
    to { filter: var(--shadow) hue-rotate(360deg); }
  }
  @keyframes finale-wobble {
    0%, 100% { transform: perspective(600px) rotateX(18deg) rotateY(0deg) rotate(-3deg) scale(1); }
    25% { transform: perspective(600px) rotateX(24deg) rotateY(-14deg) rotate(-7deg) scale(1.08); }
    50% { transform: perspective(600px) rotateX(10deg) rotateY(0deg) rotate(-3deg) scale(.95); }
    75% { transform: perspective(600px) rotateX(24deg) rotateY(14deg) rotate(1deg) scale(1.08); }
  }
  @keyframes finale-blink {
    50% { opacity: .1; }
  }
  @keyframes finale-jitter {
    0%, 100% { translate: 0 0; }
    25% { translate: -10px 8px; }
    50% { translate: 8px -10px; }
    75% { translate: -6px -6px; }
  }
  @keyframes finale-bg {
    from { background-position: 0 0, 0% 0%; filter: hue-rotate(0deg); }
    to   { background-position: 48px 48px, 100% 100%; filter: hue-rotate(360deg); }
  }
  @media print {
    section.finale, section.finale::before, section.finale h1 { animation: none; }
  }
---

<!-- _class: profile -->
<!-- _paginate: false -->

![w:240 h:240](./images/yohfee.jpg)

# id:yohfee

### はてな | Mackerel CRE

ゆる募：炒飯がおいしいお店

---

<!-- _class: title -->
<!-- _paginate: false -->

# ビルドツールを換えたら<br>**2 年越しのバグが爆発**した

Sendai Frontend Meetup × TSKaigi Sendai

---

<!-- _class: impact -->
<!-- _paginate: false -->

※ 副業で引き継いだ Web サービスの話

---

<!-- _class: impact whiteout -->
<!-- _paginate: false -->

## ビルドツールを Webpack + Babel から Vite に換えたら

# とある画面が<br>真っ白に！

---

<!-- _class: quiz -->

## このコード、何がまずい？

```ts
const plans = useMemo(() => {
  const thePlans = myPlanGroup?.plans || []
  if (plans?.length <= 0) return []
  return [...thePlans.sort((a, b) => a.rank - b.rank)]
}, [myPlanGroup])
```

- TypeScript：エラー無し
- ESLint：エラー無し

+ Webpack + Babel：動作する
+ Vite：動作しない

---

<!-- _class: console -->

## ヒント

```ts
const plans = useMemo(() => {
  const thePlans = myPlanGroup?.plans || []
  if (plans?.length <= 0) return []
  return [...thePlans.sort((a, b) => a.rank - b.rank)]
}, [myPlanGroup])
```

> `ReferenceError: Cannot access 'plans' before initialization`

---

<!-- _class: answer -->

## 答え

```ts
const plans = useMemo(() => {
  const thePlans = myPlanGroup?.plans || []
  if (plans?.length <= 0) return [] // 初期化中の自分を参照
  return [...thePlans.sort((a, b) => a.rank - b.rank)]
}, [myPlanGroup])
```

```diff
- if (plans?.length <= 0) return []
+ if (thePlans?.length <= 0) return []
```

---

<!-- _class: aside -->

## ちなみに：もう 1 つのバグ

`sort` は配列をその場で並べ替える → 元の `myPlanGroup.plans` まで並び替わる

```diff
- return [...thePlans.sort((a, b) => a.rank - b.rank)]
+ return [...thePlans].sort((a, b) => a.rank - b.rank)
```

ES2023 以降なら `thePlans.toSorted(...)` でも OK

---

<!-- _class: es5 -->

## なぜこれまでは動いていたのか

Babel 7 の preset-env は targets 指定なし・browserslist なし → **ES5 まで変換**
`const` が `var` になっていた

```js
var plans = useMemo(() => {
  if (plans?.length <= 0) return []
```

`var` は巻き上げられ、代入前でも `undefined` として読める（TDZ が無い）

1. `plans?.length`
2. `undefined <= 0`
3. `false`
4. 次の行へ進む（**偶然正しい**）

---

<!-- _class: console verify -->

## 確かめる

```js
> var p = (() => { if (p?.length <= 0) return []; return ['sorted'] })()
> p
[ 'sorted' ]
```

```js
> const q = (() => { if (q?.length <= 0) return []; return ['sorted'] })()
```

> `Uncaught ReferenceError: Cannot access 'q' before initialization`

---

## なぜ壊れたのか

|  | Webpack + Babel | Vite |
|-|-|-|
| 出力 | ES5（`const` → `var`） | モダンES（`const` のまま） |
| `plans` の参照 | `undefined` が返る | TDZ で `ReferenceError` |
| 結果 | 偶然動く | 爆発！ |

> コードは同じ。変わったのは**実行時の意味**。

---

<!-- _class: cards suspects -->

## なぜ誰も止めなかったのか

- tsc *「関数の中は管轄外なんで」*
  - `strict` でも、関数の中からの参照は「後で呼ばれるかもしれない」ので検査しない
- ESLint *「名前より後ろだったのでセーフです」*
  - @typescript-eslint/no-use-before-define は error 設定
  - それでも、参照が宣言の名前より後ろの位置にあるので通過する
- `?.` *「ちゃんとチェックしてました」*（してない）
  - チェックをしたように見える
  - 「`undefined` でも大丈夫なように書いてある」と読めてしまい、レビューでも見落としやすい

---

<!-- _class: impact missing -->
<!-- _paginate: false -->

## なぜ画面が真っ白になったのか

# `ErrorBoundary` が無い<br>`errorElement` も無い

だから例外 1 つでアプリ全体が消える

---

<!-- _class: cards lessons -->

## 学び

- ビルドツールの移行は「実行時の意味が変わる変更」
  - トランスパイルが言語本来の挙動を隠していることがある
- 型と lint の守備範囲を知っておく
  - クロージャ越しの TDZ は、どちらも見ていない
- `ErrorBoundary` | `errorElement` を保険として置く
  - 1 画面のバグで、アプリ全体を消さない

---

<!-- _class: impact relief -->
<!-- _paginate: false -->

# めでたしめでたし

---

<!-- _class: impact quiet -->
<!-- _paginate: false -->

# 本当に？

---

<!-- _class: impact -->
<!-- _paginate: false -->

# 大事なことを<br>お忘れでは？

---

<!-- _class: impact rant -->
<!-- _paginate: false -->

# なんでコードにテストが無いんだよ...？<br>教えはどうなってんだ 教えは！

---

<!-- _class: punch -->
<!-- _paginate: false -->

![bg contain](./images/t_wada.webp)

- ゴ
- ゴ
- ゴ
- ゴ
- ゴ
- ゴ
- ゴ

---

<!-- _class: cards reasons -->

## とはいえ 11 万行に対してのテストを一気にはムズイ

- 依存だらけのコードでテストしにくい
- 画面のテストは手間のわりに効果が薄い
- 後付けのテストはバグごと固めてしまう

---

<!-- _class: cards lessons -->

## 安くて効くところからやってるのでお許しください

- 純粋なロジック
  - 計算や判定など、入力と出力だけで確かめられるところ
- ロジックを切り出してテスト
  - 大きなクラスを丸ごとではなく、ルールだけを関数にする
- 主要な流れだけ結合テスト・E2E
  - 全部ではなく、壊れたら困るところを数本

---

<!-- _class: finale -->
<!-- _paginate: false -->

# 明日はTDDBCで <br>t-wadaさんと<br>アクス🪓
