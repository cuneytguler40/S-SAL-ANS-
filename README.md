<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <title>SİSAL ŞANS</title>
  <link href="https://fonts.googleapis.com/css2?family=Roboto+Condensed:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background: #e0e0e0;
      font-family: 'Roboto Condensed', sans-serif;
      overflow-x: hidden;
      width: 100vw;
      height: 100vh;
      -webkit-text-size-adjust: 100%;
      touch-action: manipulation;
      font-size: calc(14px + 0.5vw); /* Mobil için dinamik font boyutu */
    }
    .container {
      width: 100vw;
      height: 100vh;
      background: #fff;
      border: none;
      border-radius: 0;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
      display: flex;
      flex-direction: column;
      align-items: center;
      overflow-y: auto;
      -webkit-overflow-scrolling: touch;
    }
    .header {
      width: 100%;
      background: #424242;
      color: #fff;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem 1rem;
      font-size: calc(12px + 0.5vw);
      border-bottom: 2px solid #0288d1;
      position: sticky;
      top: 0;
      z-index: 10;
    }
    .header .title {
      font-size: calc(14px + 0.5vw);
      font-weight: bold;
      text-align: center;
      flex-grow: 1;
    }
    .header .info {
      font-size: calc(10px + 0.5vw);
      color: #b0bec5;
    }
    .bottom-section {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); /* Mobil için daha esnek grid */
      gap: 0.5rem;
      padding: 0.5rem;
      background: #f5f5f5;
      width: 100%;
    }
    .game-btn {
      padding: 0.75rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      border: 2px solid;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3), 0 0 5px inset;
      touch-action: manipulation;
      min-height: 48px; /* Mobil için dokunma alanı */
    }
    .game-btn:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5), 0 0 10px inset;
    }
    .game-btn:active {
      transform: translateY(1px) scale(0.97);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2), 0 0 3px inset;
    }
    .sayisal { background: #d32f2f; border-color: #ef5350; box-shadow: 0 3px 10px rgba(211, 47, 47, 0.5), 0 0 5px #ef5350 inset; }
    .super { background: #f57c00; border-color: #ff9800; box-shadow: 0 3px 10px rgba(245, 124, 0, 0.5), 0 0 5px #ff9800 inset; }
    .sans { background: #0288d1; border-color: #42a5f5; box-shadow: 0 3px 10px rgba(2, 136, 209, 0.5), 0 0 5px #42a5f5 inset; }
    .on { background: #ab47bc; border-color: #ce93d8; box-shadow: 0 3px 10px rgba(171, 71, 188, 0.5), 0 0 5px #ce93d8 inset; }
    .middle-section {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
      gap: 0.5rem;
      padding: 0.5rem;
      background: #fff;
      width: 100%;
    }
    .action-btn {
      padding: 0.75rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      border: 2px solid;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3), 0 0 5px inset;
      touch-action: manipulation;
      min-height: 48px;
    }
    .action-btn:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5), 0 0 10px inset;
    }
    .action-btn:active {
      transform: translateY(1px) scale(0.97);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2), 0 0 3px inset;
    }
    .sen-sec { background: #d32f2f; border-color: #ef5350; box-shadow: 0 3px 10px rgba(211, 47, 47, 0.5), 0 0 5px #ef5350 inset; }
    .ekrandan-oyna { background: #4fc3f7; border-color: #81d4fa; box-shadow: 0 3px 10px rgba(79, 195, 247, 0.5), 0 0 5px #81d4fa inset; }
    .preview-section {
      display: none;
      flex-direction: column;
      align-items: center;
      gap: 0.4rem;
      padding: 0.5rem;
      background: #f8f9fa;
      border: 1px solid #ccc;
      border-radius: 8px;
      margin: 0.5rem 0;
      width: 100%;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }
    .preview-item {
      background: #e9ecef;
      padding: 0.5rem 0.75rem;
      border-radius: 5px;
      font-size: calc(12px + 0.3vw);
      color: #333;
      width: 90%;
      text-align: left;
    }
    .preview-title {
      font-size: calc(14px + 0.3vw);
      font-weight: bold;
      color: #0288d1;
    }
    .other-games {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(90px, 1fr));
      gap: 0.5rem;
      padding: 0.5rem;
      background: #f5f5f5;
      width: 100%;
    }
    .other-btn {
      padding: 0.5rem;
      font-size: calc(10px + 0.3vw);
      color: #fff;
      border: 2px solid;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.3), 0 0 5px inset;
      touch-action: manipulation;
      min-height: 44px;
    }
    .other-btn:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5), 0 0 10px inset;
    }
    .other-btn:active {
      transform: translateY(1px) scale(0.97);
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2), 0 0 3px inset;
    }
    .sayisal-sen-sec { background: #d32f2f; border-color: #ef5350; box-shadow: 0 3px 10px rgba(211, 47, 47, 0.5), 0 0 5px #ef5350 inset; }
    .super-sen-sec { background: #f57c00; border-color: #ff9800; box-shadow: 0 3px 10px rgba(245, 124, 0, 0.5), 0 0 5px #ff9800 inset; }
    .sans-sen-sec { background: #0288d1; border-color: #42a5f5; box-shadow: 0 3px 10px rgba(2, 136, 209, 0.5), 0 0 5px #42a5f5 inset; }
    .on-sen-sec { background: #ab47bc; border-color: #ce93d8; box-shadow: 0 3px 10px rgba(171, 71, 188, 0.5), 0 0 5px #ce93d8 inset; }
    .column-page {
      display: none;
      width: 100%;
      background: #fff;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
      text-align: center;
      overflow-y: auto;
      -webkit-overflow-scrolling: touch;
    }
    .column-options {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
      gap: 0.5rem;
      padding: 0.5rem;
      touch-action: pan-x;
    }
    .column-btn {
      padding: 0.75rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      background: #00bcd4;
      border: 2px solid #00e5ff;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 0 5px #00e5ff, 0 0 10px #00bcd4 inset;
      min-height: 48px;
      user-select: none;
      touch-action: manipulation;
    }
    .column-btn:hover {
      transform: scale(1.05);
      box-shadow: 0 0 10px #00e5ff, 0 0 15px #00bcd4 inset;
    }
    .column-btn:active {
      transform: scale(0.95);
      box-shadow: 0 0 3px #00e5ff, 0 0 5px #00bcd4 inset;
    }
    .column-btn.selected {
      background: #4caf50;
      border-color: #66bb6a;
      box-shadow: 0 0 10px #66bb6a, 0 0 15px #4caf50 inset;
    }
    .number-selection {
      display: none;
      grid-template-columns: repeat(auto-fit, minmax(40px, 1fr));
      gap: 0.3rem;
      padding: 0.5rem;
      touch-action: pan-x;
    }
    .number-btn {
      padding: 0.5rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      background: #0288d1;
      border: 2px solid #42a5f5;
      border-radius: 5px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 0 5px #42a5f5;
      min-height: 40px;
      user-select: none;
      touch-action: manipulation;
    }
    .number-btn:hover {
      transform: scale(1.05);
      box-shadow: 0 0 8px #42a5f5;
    }
    .number-btn:active {
      transform: scale(0.95);
      box-shadow: 0 0 3px #42a5f5;
    }
    .number-btn.selected {
      background: #d32f2f;
      border-color: #ef5350;
      box-shadow: 0 0 8px #ef5350;
    }
    .onayla-btn {
      display: none;
      padding: 0.75rem 1.25rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      background: #4caf50;
      border: 2px solid #66bb6a;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 3px 10px rgba(76, 175, 80, 0.5), 0 0 5px #66bb6a inset;
      margin: 0.5rem auto;
      touch-action: manipulation;
      width: 80%; /* Daha geniş buton */
      max-width: 200px;
    }
    .onayla-btn:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 15px rgba(76, 175, 80, 0.7), 0 0 10px #66bb6a inset;
    }
    .onayla-btn:active {
      transform: translateY(1px) scale(0.97);
      box-shadow: 0 1px 3px rgba(76, 175, 80, 0.3), 0 0 3px #66bb6a inset;
    }
    .footer {
      display: flex;
      justify-content: space-between;
      padding: 0.5rem;
      background: #424242;
      color: #fff;
      font-size: calc(10px + 0.3vw);
      width: 100%;
      border-top: 2px solid #0288d1;
      position: sticky;
      bottom: 0;
      z-index: 10;
    }
    .ticket-section {
      display: none;
      flex-direction: column;
      padding: 1rem;
      width: 100%;
      background: #fff;
      border: 1px dashed #000;
      border-radius: 8px;
      font-family: 'Courier New', monospace;
      text-align: left;
      color: #000;
      line-height: 1.3;
      margin: 0.5rem 0;
    }
    .ticket-header {
      font-size: calc(16px + 0.3vw);
      font-weight: bold;
      padding-bottom: 0.3rem;
      text-align: center;
      border-bottom: 1px dashed #000;
    }
    .ticket-body {
      font-size: calc(12px + 0.3vw);
      padding: 0.5rem 0;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
    }
    .ticket-row {
      display: flex;
      width: 100%;
      justify-content: space-between;
      padding: 0.2rem 0;
    }
    .ticket-number {
      margin-left: 0.5rem;
      min-width: 100px;
      font-size: calc(12px + 0.3vw);
      font-weight: bold;
      color: #0288d1;
    }
    .ticket-footer {
      font-size: calc(10px + 0.3vw);
      padding-top: 0.5rem;
      color: #666;
      border-top: 1px dashed #000;
      text-align: center;
    }
    .back-btn {
      padding: 0.75rem;
      font-size: calc(12px + 0.3vw);
      color: #fff;
      background: #607d8b;
      border: 2px solid #78909c;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      box-shadow: 0 3px 10px rgba(96, 125, 139, 0.5), 0 0 5px #78909c inset;
      margin: 0.5rem auto;
      touch-action: manipulation;
      width: 80%;
      max-width: 200px;
    }
    .back-btn:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 5px 15px rgba(96, 125, 139, 0.7), 0 0 10px #78909c inset;
    }
    .back-btn:active {
      transform: translateY(1px) scale(0.97);
      box-shadow: 0 1px 3px rgba(96, 125, 139, 0.3), 0 0 3px #78909c inset;
    }
    .ticket-output {
      margin-top: 0.5rem;
      background: #e9ecef;
      padding: 0.75rem;
      border: 1px dashed #00aaff;
      color: #000;
      text-align: center;
      animation: blink 1s infinite;
      font-size: calc(12px + 0.3vw);
    }
    @keyframes blink {
      50% { opacity: 0.5; }
    }
    /* Küçük ekranlar için ek optimizasyon */
    @media (max-width: 600px) {
      .game-btn, .action-btn, .other-btn, .column-btn, .number-btn, .onayla-btn, .back-btn {
        font-size: calc(10px + 0.5vw);
        padding: 0.5rem;
        min-height: 44px;
      }
      .header .title {
        font-size: calc(12px + 0.5vw);
      }
      .header .info {
        font-size: calc(8px + 0.5vw);
      }
      .column-options, .number-selection {
        gap: 0.3rem;
      }
    }
  </style>
</head>
<body>
  <div class="container" id="mainPage">
    <div class="header">
      <div>
        <button class="back-btn" onclick="goBack()" style="background: #616161; padding: 0.3rem 0.6rem; font-size: calc(10px + 0.3vw);" aria-label="Geri dön">GERİ</button>
        <span style="margin-left: 0.5rem;">Oyunlar</span>
      </div>
      <div class="title">SİSAL ŞANS <span style="font-size: calc(10px + 0.3vw); color: #b0bec5;">Çekiliş No: 85/2025</span></div>
      <div class="info">07/06/2025 06:17</div>
    </div>
    <div class="bottom-section">
      <button class="game-btn sayisal" id="sayisal" onclick="showColumnPage('sayisal')" aria-label="Sayısal Loto oyununu seç">Sayısal Loto</button>
      <button class="game-btn super" id="super" onclick="showColumnPage('super')" aria-label="Süper Loto oyununu seç">Süper Loto</button>
      <button class="game-btn sans" id="sans" onclick="showColumnPage('sans')" aria-label="Şans Topu oyununu seç">Şans Topu</button>
      <button class="game-btn on" id="on" onclick="showColumnPage('on')" aria-label="On Numara oyununu seç">On Numara</button>
    </div>
    <div class="middle-section">
      <button class="action-btn sen-sec" onclick="autoSelect()" aria-label="Otomatik seçim yap">Sen Seç</button>
      <button class="action-btn ekrandan-oyna" onclick="showNumberSelection()" aria-label="Ekranadan numara seç">Ekranadan Oyna</button>
    </div>
    <div class="preview-section" id="previewSection">
      <div class="preview-title">Seçilen Kolonlar</div>
    </div>
    <div class="column-page" id="gamePage">
      <h2 id="columnTitle">Kolon Seçimi</h2>
      <div class="column-options" id="columnOptions"></div>
      <div class="number-selection" id="numberSelection"></div>
      <button class="onayla-btn" id="onaylaBtn" onclick="generateTicket()" aria-label="Seçimi onayla">ONAYLA</button>
    </div>
    <div class="ticket-section" id="ticketSection">
      <div class="ticket-header" id="ticketHeader">SİSAL ŞANS</div>
      <div class="ticket-body" id="ticketBody"></div>
      <div class="ticket-footer" id="ticketFooter"></div>
      <div class="ticket-output" id="ticketOutput">Bilet Yazdırılıyor...</div>
      <button class="back-btn" onclick="goBack()" aria-label="Ana sayısına dön">GERİ DÖN</button>
    </div>
    <div class="other-games">
      <button class="other-btn sayisal-sen-sec" onclick="autoSelect('sayisal')" aria-label="Sayısal Loto için otomatik seçim">Sayısal Loto Sen Seç</button>
      <button class="other-btn super-sen-sec" onclick="autoSelect('super')" aria-label="Süper Loto için otomatik seçim">Süper Loto Sen Seç</button>
      <button class="other-btn sans-sen-sec" onclick="autoSelect('sans')" aria-label="Şans Topu için otomatik seçim">Şans Topu Sen Seç</button>
      <button class="other-btn on-sen-sec" onclick="autoSelect('on')" aria-label="On Numara için otomatik seçim">On Numara Sen Seç</button>
    </div>
    <div class="footer">
      <span id="totalCost">TOPLAM: 0.00 TL</span>
      <span>SON İŞLEM</span>
    </div>
  </div>

  <script>
    let selectedGame = '';
    let selectedColumns = 0;
    let selectedNumbers = [];
    let manualNumbers = [];
    let isManualMode = false;
    let pastDraws = {
      sayisal: [[3, 12, 23, 34, 45, 67], [5, 14, 25, 36, 47, 68], [7, 16, 27, 38, 49, 69]],
      super: [[2, 13, 24, 35, 46, 58], [4, 15, 26, 37, 48, 59], [6, 17, 28, 39, 50, 60]],
      sans: [[1, 12, 23, 34, 45, 13], [3, 14, 25, 36, 47, 14], [5, 16, 27, 38, 49, 15]],
      on: [[2, 13, 24, 35, 46, 57, 68, 79, 80, 10], [4, 15, 26, 37, 48, 59, 70, 71, 72, 11], [6, 17, 28, 39, 50, 61, 73, 74, 75, 12]]
    };
    const gamePrices = { sayisal: 20, super: 15, sans: 10, on: 5 };

    class LotteryAI {
      constructor(pastDraws) {
        this.pastDraws = pastDraws;
        this.frequencyMap = {};
        this.patternMap = {};
        this.gameDrawCounts = {};
        this.initializeFrequencyAndPatterns();
      }
      initializeFrequencyAndPatterns() {
        Object.keys(this.pastDraws).forEach(game => {
          this.frequencyMap[game] = {};
          this.patternMap[game] = {};
          this.gameDrawCounts[game] = this.pastDraws[game].length;
          if (!this.gameDrawCounts[game]) {
            console.error(`No draws for ${game}`);
            return;
          }
          this.pastDraws[game].forEach(draw => {
            draw.forEach(num => {
              this.frequencyMap[game][num] = (this.frequencyMap[game][num] || 0) + 1;
            });
            for (let i = 0; i < draw.length - 1; i++) {
              let diff = draw[i + 1] - draw[i];
              this.patternMap[game][diff] = (this.patternMap[game][diff] || 0) + 1;
              if (i < draw.length - 2 && draw[i + 2] - draw[i] < 10) {
                this.patternMap[game]['cluster'] = (this.patternMap[game]['cluster'] || 0) + 1;
              }
            }
          });
        });
      }
      calculateWeights(game, maxNum) {
        const freq = this.frequencyMap[game] || {};
        const patterns = this.patternMap[game] || {};
        const totalDraws = this.gameDrawCounts[game] || 1;
        const weights = Array(maxNum).fill(1);
        for (let i = 1; i <= maxNum; i++) {
          const freqCount = freq[i] || 0;
          let freqWeight = 1 + (totalDraws - freqCount) / totalDraws;
          let patternBonus = 0;
          for (let diff in patterns) {
            if (diff !== 'cluster' && patterns[diff] < totalDraws / 10) patternBonus += 0.2;
          }
          if (patterns['cluster'] && patterns['cluster'] / totalDraws < 0.3) patternBonus += 0.1;
          weights[i - 1] = freqWeight + patternBonus;
        }
        return weights;
      }
      weightedRandom(maxNum, weights, count) {
        const numbers = new Set();
        while (numbers.size < count) {
          let sum = weights.reduce((a, b) => a + b, 0);
          let r = Math.random() * sum;
          let i = 0;
          while (r > weights[i]) {
            r -= weights[i];
            i++;
          }
          numbers.add(i + 1);
        }
        return Array.from(numbers).sort((a, b) => a - b);
      }
      predictFutureDraw(game, count, maxNum) {
        const weights = this.calculateWeights(game, maxNum);
        let numbers = this.weightedRandom(maxNum, weights, count);
        let bonus = game === 'sans' ? this.weightedRandom(14, Array(14).fill(1).map((_, i) => 1 + (i + 1) / 14 * 1.5), 1)[0] : null;
        return bonus ? [...numbers, bonus] : numbers;
      }
    }

    const ai = new LotteryAI(pastDraws);

    function showColumnPage(game) {
      selectedGame = game;
      isManualMode = false;
      const elements = {
        gamePage: document.getElementById('gamePage'),
        bottomSection: document.querySelector('.bottom-section'),
        middleSection: document.querySelector('.middle-section'),
        previewSection: document.getElementById('previewSection'),
        otherGames: document.querySelector('.other-games'),
        footer: document.querySelector('.footer'),
        ticketSection: document.getElementById('ticketSection'),
        columnOptions: document.getElementById('columnOptions'),
        numberSelection: document.getElementById('numberSelection'),
        onaylaBtn: document.getElementById('onaylaBtn'),
        columnTitle: document.getElementById('columnTitle')
      };
      if (Object.values(elements).some(el => !el)) {
        alert('Hata: Sayfada bazı öğeler eksik!');
        return;
      }
      elements.columnOptions.innerHTML = '';
      elements.numberSelection.style.display = 'none';
      elements.numberSelection.innerHTML = '';
      elements.columnTitle.textContent = `${game.toUpperCase()} Kolon Seçimi`;
      const columns = game === 'sayisal' ? [1, 2, 3, 4, 5, 6] :
                      game === 'super' ? [1, 2, 3, 4, 5, 6, 7] : [1, 2, 3, 4, 5];
      columns.forEach(col => {
        const btn = document.createElement('button');
        btn.className = 'column-btn';
        btn.textContent = `${col} Kolon`;
        btn.setAttribute('aria-label', `${col} kolon seç`);
        btn.onclick = () => selectColumns(col, btn);
        btn.addEventListener('touchstart', (e) => {
          e.preventDefault();
          selectColumns(col, btn);
        });
        btn.addEventListener('keydown', (e) => {
          if (e.key === 'Enter') selectColumns(col, btn);
        });
        elements.columnOptions.appendChild(btn);
      });
      elements.bottomSection.style.display = 'none';
      elements.middleSection.style.display = 'none';
      elements.previewSection.style.display = 'none';
      elements.otherGames.style.display = 'none';
      elements.footer.style.display = 'none';
      elements.ticketSection.style.display = 'none';
      elements.gamePage.style.display = 'block';
      elements.onaylaBtn.style.display = 'block';
    }

    function selectColumns(col, button) {
      selectedColumns = col;
      document.querySelectorAll('.column-btn').forEach(btn => btn.classList.remove('selected'));
      button.classList.add('selected');
      document.getElementById('numberSelection').style.display = isManualMode ? 'flex' : 'none';
    }

    function showNumberSelection(game = null) {
      if (game) selectedGame = game;
      if (!selectedGame) {
        alert('Lütfen önce bir oyun seçin!');
        return;
      }
      isManualMode = true;
      const elements = {
        gamePage: document.getElementById('gamePage'),
        bottomSection: document.querySelector('.bottom-section'),
        middleSection: document.querySelector('.middle-section'),
        previewSection: document.getElementById('previewSection'),
        otherGames: document.querySelector('.other-games'),
        footer: document.querySelector('.footer'),
        ticketSection: document.getElementById('ticketSection'),
        columnOptions: document.getElementById('columnOptions'),
        numberSelection: document.getElementById('numberSelection'),
        onaylaBtn: document.getElementById('onaylaBtn'),
        columnTitle: document.getElementById('columnTitle')
      };
      if (Object.values(elements).some(el => !el)) {
        alert('Hata: Sayfada bazı öğeler eksik!');
        return;
      }
      elements.columnOptions.innerHTML = '';
      elements.numberSelection.innerHTML = '';
      elements.columnTitle.textContent = `${selectedGame.toUpperCase()} Numara Seçimi`;
      let maxNum = 0, numCount = 0, bonus = false;
      switch (selectedGame) {
        case 'sayisal': maxNum = 90; numCount = 6; break;
        case 'super': maxNum = 60; numCount = 6; break;
        case 'sans': maxNum = 34; numCount = 5; bonus = true; break;
        case 'on': maxNum = 80; numCount = 10; break;
        default: alert('Geçersiz oyun!'); return;
      }
      manualNumbers = [];
      for (let i = 1; i <= maxNum; i++) {
        const btn = document.createElement('button');
        btn.className = 'number-btn';
        btn.textContent = i.toString().padStart(2, '0');
        btn.setAttribute('aria-label', `Numara ${i} seç`);
        btn.onclick = () => toggleNumber(i, btn, numCount);
        btn.addEventListener('touchstart', (e) => {
          e.preventDefault();
          toggleNumber(i, btn, numCount);
        });
        btn.addEventListener('keydown', (e) => {
          if (e.key === 'Enter') toggleNumber(i, btn, numCount);
        });
        elements.numberSelection.appendChild(btn);
      }
      if (bonus) {
        const bonusTitle = document.createElement('div');
        bonusTitle.textContent = 'Bonus Numara (1-14)';
        bonusTitle.style.fontWeight = 'bold';
        bonusTitle.style.color = '#0288d1';
        bonusTitle.style.marginTop = '10px';
        elements.numberSelection.appendChild(bonusTitle);
        for (let i = 1; i <= 14; i++) {
          const btn = document.createElement('button');
          btn.className = 'number-btn';
          btn.textContent = i.toString().padStart(2, '0');
          btn.setAttribute('aria-label', `Bonus numara ${i} seç`);
          btn.onclick = () => toggleNumber(i, btn, 1, true);
          btn.addEventListener('touchstart', (e) => {
            e.preventDefault();
            toggleNumber(i, btn, 1, true);
          });
          btn.addEventListener('keydown', (e) => {
            if (e.key === 'Enter') toggleNumber(i, btn, 1, true);
          });
          elements.numberSelection.appendChild(btn);
        }
      }
      elements.bottomSection.style.display = 'none';
      elements.middleSection.style.display = 'none';
      elements.previewSection.style.display = 'none';
      elements.otherGames.style.display = 'none';
      elements.footer.style.display = 'none';
      elements.ticketSection.style.display = 'none';
      elements.gamePage.style.display = 'block';
      elements.numberSelection.style.display = 'flex';
      elements.onaylaBtn.style.display = 'block';
    }

    function toggleNumber(num, button, limit, isBonus = false) {
      const index = isBonus ? manualNumbers.findIndex(set => set.bonus === num) : manualNumbers.findIndex(set => set.main.includes(num));
      if (index > -1) {
        if (isBonus) manualNumbers[index].bonus = null;
        else manualNumbers[index].main = manualNumbers[index].main.filter(n => n !== num);
        button.classList.remove('selected');
      } else {
        if (manualNumbers.length === 0 || (isBonus && !manualNumbers[0].bonus) || (!isBonus && manualNumbers[0].main.length < limit)) {
          if (manualNumbers.length === 0) manualNumbers.push({ main: [], bonus: null });
          if (isBonus) manualNumbers[0].bonus = num;
          else manualNumbers[0].main.push(num);
          button.classList.add('selected');
        } else {
          alert(`Maksimum ${isBonus ? '1 bonus numara' : limit + ' numara'} seçebilirsiniz!`);
        }
      }
      manualNumbers[0].main.sort((a, b) => a - b);
    }

    function autoSelect(game = null) {
      if (game) selectedGame = game;
      if (!selectedGame) {
        alert('Lütfen önce bir oyun seçin!');
        return;
      }
      isManualMode = false;
      selectedColumns = 1;
      selectedNumbers = [];
      let maxNum = 0, numCount = 0, bonus = false;
      switch (selectedGame) {
        case 'sayisal': maxNum = 90; numCount = 6; break;
        case 'super': maxNum = 60; numCount = 6; break;
        case 'sans': maxNum = 34; numCount = 5; bonus = true; break;
        case 'on': maxNum = 80; numCount = 10; break;
        default: alert('Geçersiz oyun!'); return;
      }
      let numSet = bonus ?
        `${ai.predictFutureDraw(selectedGame, numCount, maxNum).join('-')} + ${ai.predictFutureDraw(selectedGame, 1, 14)[0]}` :
        ai.predictFutureDraw(selectedGame, numCount, maxNum).join('-');
      selectedNumbers.push(numSet);
      const previewSection = document.getElementById('previewSection');
      const totalCost = document.getElementById('totalCost');
      if (!previewSection || !totalCost) {
        alert('Hata: Sayfada bazı öğeler eksik!');
        return;
      }
      previewSection.innerHTML = '<div class="preview-title">Seçilen Kolonlar</div>';
      selectedNumbers.forEach((num, i) => {
        const item = document.createElement('div');
        item.className = 'preview-item';
        item.textContent = `Kolon ${i + 1}: ${num} (Otomatik)`;
        previewSection.appendChild(item);
      });
      previewSection.style.display = 'flex';
      totalCost.textContent = `TOPLAM: ${(selectedColumns * gamePrices[selectedGame]).toFixed(2)} TL`;
    }

    function generateTicket() {
      if (!selectedGame || !selectedColumns) {
        alert('Lütfen bir kolon sayısı seçin!');
        return;
      }
      if (isManualMode && (!manualNumbers.length || manualNumbers[0].main.length < getNumberCount(selectedGame) || (selectedGame === 'sans' && !manualNumbers[0].bonus))) {
        alert('Lütfen tüm numaraları seçin!');
        return;
      }
      const elements = {
        ticketHeader: document.getElementById('ticketHeader'),
        ticketBody: document.getElementById('ticketBody'),
        ticketFooter: document.getElementById('ticketFooter'),
        ticketOutput: document.getElementById('ticketOutput'),
        gamePage: document.getElementById('gamePage'),
        ticketSection: document.getElementById('ticketSection')
      };
      if (Object.values(elements).some(el => !el)) {
        alert('Hata: Sayfada bazı öğeler eksik!');
        return;
      }
      if (!isManualMode) {
        selectedNumbers = [];
        let maxNum = 0, numCount = 0, bonus = false;
        switch (selectedGame) {
          case 'sayisal': maxNum = 90; numCount = 6; break;
          case 'super': maxNum = 60; numCount = 6; break;
          case 'sans': maxNum = 34; numCount = 5; bonus = true; break;
          case 'on': maxNum = 80; numCount = 10; break;
          default: alert('Geçersiz oyun!'); return;
        }
        for (let i = 0; i < selectedColumns; i++) {
          let numSet = bonus ?
            `${ai.predictFutureDraw(selectedGame, numCount, maxNum).join('-')} + ${ai.predictFutureDraw(selectedGame, 1, 14)[0]}` :
            ai.predictFutureDraw(selectedGame, numCount, maxNum).join('-');
          selectedNumbers.push(numSet);
        }
      } else {
        selectedNumbers = [];
        for (let i = 0; i < selectedColumns; i++) {
          let numSet = selectedGame === 'sans' ?
            `${manualNumbers[0].main.join('-')} + ${manualNumbers[0].bonus}` :
            manualNumbers[0].main.join('-');
          selectedNumbers.push(numSet);
        }
      }
      let gameName = '';
      switch (selectedGame) {
        case 'sayisal': gameName = 'SAYISAL LOTO'; break;
        case 'super': gameName = 'SÜPER LOTO'; break;
        case 'sans': gameName = 'ŞANS TOPU'; break;
        case 'on': gameName = 'ON NUMARA'; break;
      }
      elements.ticketBody.innerHTML = '';
      let numbers = '';
      for (let i = 0; i < selectedColumns; i++) {
        numbers += `<div class="ticket-row"><span>0${i + 1}. KOLON (${selectedGame === 'sans' ? '5+1' : selectedGame === 'on' ? '10' : '6'})</span><span class="ticket-number">${selectedNumbers[i]} ${isManualMode ? 'MS' : 'SS'}</span></div>`;
      }
      elements.ticketHeader.textContent = gameName;
      elements.ticketBody.innerHTML = numbers;
      elements.ticketFooter.innerHTML = `
        ÇEKILIŞ NO: 85 ve TARIH: 07/06/2025<br>
        BILET NO: 25000D212763ACA000${Math.floor(Math.random() * 1000000).toString().padStart(6, '0')}<br>
        TOPLAM KOLON SAYISI: ${selectedColumns}<br>
        PLAM: ${(selectedColumns * gamePrices[selectedGame]).toFixed(2)} TL<br>
        BAYI KODU 275BSTA SIRA NO 013032<br>
        07/06/25 06:17 GÜVENLIK KODU ${Math.floor(Math.random() * 1000000).toString().padStart(6, '0')}<br>
        [BARKOD] [DAMGA]
      `;
      elements.gamePage.style.display = 'none';
      elements.ticketSection.style.display = 'flex';
      elements.ticketOutput.textContent = 'Bilet Yazdırılıyor...';
      setTimeout(() => {
        elements.ticketOutput.textContent = 'Bilet Yazdırıldı!';
        elements.ticketOutput.style.animation = 'none';
      }, 2000);
      const totalCost = document.getElementById('totalCost');
      if (totalCost) totalCost.textContent = `TOPLAM: ${(selectedColumns * gamePrices[selectedGame]).toFixed(2)} TL`;
    }

    function getNumberCount(game) {
      switch (game) {
        case 'sayisal': return 6;
        case 'super': return 6;
        case 'sans': return 5;
        case 'on': return 10;
        default: return 0;
      }
    }

    function goBack() {
      const elements = {
        ticketSection: document.getElementById('ticketSection'),
        gamePage: document.getElementById('gamePage'),
        bottomSection: document.querySelector('.bottom-section'),
        middleSection: document.querySelector('.middle-section'),
        previewSection: document.getElementById('previewSection'),
        otherGames: document.querySelector('.other-games'),
        footer: document.querySelector('.footer'),
        ticketOutput: document.getElementById('ticketOutput'),
        onaylaBtn: document.getElementById('onaylaBtn')
      };
      if (Object.values(elements).some(el => !el)) {
        alert('Hata: Sayfada bazı öğeler eksik!');
        return;
      }
      elements.ticketSection.style.display = 'none';
      elements.gamePage.style.display = 'none';
      elements.bottomSection.style.display = 'flex';
      elements.middleSection.style.display = 'flex';
      elements.previewSection.style.display = 'none';
      elements.otherGames.style.display = 'flex';
      elements.footer.style.display = 'flex';
      elements.ticketOutput.textContent = 'Bilet Yazdırılıyor...';
      elements.onaylaBtn.style.display = 'none';
      selectedGame = '';
      selectedColumns = 0;
      selectedNumbers = [];
      manualNumbers = [];
      isManualMode = false;
      const totalCost = document.getElementById('totalCost');
      if (totalCost) totalCost.textContent = 'TOPLAM: 0.00 TL';
    }

    document.addEventListener('DOMContentLoaded', () => {
      console.log('DOM yüklendi');
      document.querySelectorAll('.game-btn').forEach(btn => {
        btn.addEventListener('touchstart', (e) => {
          e.preventDefault();
          showColumnPage(btn.id);
        });
        btn.addEventListener('keydown', (e) => {
          if (e.key === 'Enter') showColumnPage(btn.id);
        });
      });
      document.querySelectorAll('.back-btn').forEach(btn => {
        btn.addEventListener('touchstart', (e) => {
          e.preventDefault();
          goBack();
        });
        btn.addEventListener('keydown', (e) => {
          if (e.key === 'Enter') goBack();
        });
      });
    });
  </script>
</body>
</html>
