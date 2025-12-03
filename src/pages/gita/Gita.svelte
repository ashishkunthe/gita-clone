<script>
    let modalOpen = false;
    let selectedVerse = null;
  
    const verses = Array.from({ length: 47 }, (_, i) => i + 1);
  
    // Dummy data — will be replaced by API later
    const verseData = {
      sanskrit: `धृतराष्ट्र उवाच |
  धर्मक्षेत्रे कुरुक्षेत्रे समवेता युयुत्सवः ||`,
  
      transliteration: `dhṛtarāṣṭra uvāca |
  dharma-kṣetre kuru-kṣetre samavetā yuyutsavaḥ ||`,
  
      translation: `Dhritarashtra said: In the holy field of Kurukshetra, gathered together eager for battle...`,
  
      wordByWord: [
        { word: "धृतराष्ट्र", meaning: "Dhritarashtra" },
        { word: "उवाच", meaning: "said" },
        { word: "धर्मक्षेत्रे", meaning: "in the holy field" },
        { word: "कुरुक्षेत्रे", meaning: "Kuru field" }
      ],
  
      commentary: [
        {
          author: "Ādi Śaṅkarāchārya",
          text: "This verse describes Dhritarashtra expressing his curiosity..."
        },
        {
          author: "Rāmānuja",
          text: "According to Ramanuja, Kurukshetra is also a symbolic field..."
        }
      ],
  
      audio: "/audio/demo.mp3"
    };
  
    let activeTab = "sanskrit";
    let expandedCommentary = null;
  
    const openModal = (v) => {
      selectedVerse = v;
      modalOpen = true;
      document.body.style.overflow = "hidden"; // stop background scroll
    };
  
    const closeModal = () => {
      modalOpen = false;
      document.body.style.overflow = "auto"; // resume scroll
    };
  </script>
  
  <style>
    /* ======================================
       PAGE BACKGROUND
    ====================================== */
    .page-bg {
      min-height: 100vh;
      background: repeating-linear-gradient(
        90deg,
        #faf4e6,
        #faf4e6 12px,
        #f4ead6 12px,
        #f4ead6 24px
      );
      padding-bottom: 60px;
    }
  
    .container {
      max-width: 1300px;
      margin: auto;
    }
  
    /* ======================================
       NAVBAR
    ====================================== */
    nav {
      display: flex;
      justify-content: space-between;
      padding: 20px 40px;
      align-items: center;
      font-family: "Times New Roman", serif;
    }
  
    nav ul {
      display: flex;
      gap: 35px;
      list-style: none;
    }
  
    nav li {
      position: relative;
      font-size: 15px;
      cursor: pointer;
    }
  
    nav li::after {
      content: "";
      position: absolute;
      width: 0%;
      height: 2px;
      left: 0;
      bottom: -3px;
      background: #c23030;
      transition: 0.25s;
    }
  
    nav li:hover::after {
      width: 100%;
    }
  
    /* ======================================
       BACK BUTTON
    ====================================== */
    .back-btn {
      margin: 20px 40px;
      font-family: serif;
      font-size: 16px;
      color: #8b2f2f;
      cursor: pointer;
      transition: 0.2s;
    }
  
    .back-btn:hover {
      transform: translateX(-4px);
      color: #c23030;
    }
  
    /* ======================================
       HERO
    ====================================== */
    .hero {
      background: url('/gita_banner.png') center top/cover no-repeat;
      height: 330px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  
    .hero h1 {
      font-size: 72px;
      background: rgba(255, 255, 255, 0.45);
      padding: 18px 45px;
      border-radius: 10px;
      color: #3e4a3d;
      text-shadow: 1px 1px 2px #00000055;
      font-family: Georgia, serif;
    }
  
    /* ======================================
       CHAPTER TITLE
    ====================================== */
    .chapter-title {
      text-align: center;
      margin-top: 40px;
      font-size: 30px;
      color: #c23030;
      font-weight: bold;
    }
  
    /* ======================================
       VERSE GRID
    ====================================== */
    .verse-grid {
      margin-top: 30px;
      padding: 40px 30px;
      border-top: 3px solid #b92d2d;
      border-radius: 10px;
      background: rgba(255, 255, 255, 0.6);
  
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      gap: 25px;
    }
  
    .verse-card {
      background: url('/scroll-bg.png') center/cover no-repeat;
      height: 170px;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      padding-bottom: 20px;
      font-size: 22px;
      color: #fff;
      text-shadow: 2px 2px 3px black;
      cursor: pointer;
      user-select: none;
      transition: transform 0.2s;
    }
  
    .verse-card:hover {
      transform: scale(1.07);
    }
  
    /* ======================================
       MODAL OVERLAY
    ====================================== */
    .modal-overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 20;
    }
  
    /* ======================================
       MODAL
    ====================================== */
    .modal {
      background: #ffe7cf;
      width: 85%;
      max-width: 820px;
      max-height: 85%;
      border-radius: 20px;
      padding: 0 0 30px;
      overflow-y: auto;
      position: relative;
      box-shadow: 0 0 15px #00000055;
    }
  
    .close-btn {
      position: absolute;
      right: 20px;
      top: 14px;
      font-size: 22px;
      font-weight: bold;
      cursor: pointer;
      z-index: 30;
    }
  
    /* ======================================
       MODAL HEADER (STICKY)
    ====================================== */
    .modal-header {
      position: sticky;
      top: 0;
      background: #b92d2d;
      color: white;
      padding: 12px;
      border-radius: 20px 20px 0 0;
      text-align: center;
      font-size: 18px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 10;
    }
  
    .nav-arrow {
      background: transparent;
      border: none;
      color: white;
      font-size: 26px;
      cursor: pointer;
    }
  
    /* ======================================
       TABS
    ====================================== */
    .tabs {
      display: flex;
      flex-wrap: wrap;
      gap: 12px;
      margin: 20px;
    }
  
    .tab {
      padding: 10px 18px;
      background: #f5d8b8;
      border-radius: 8px;
      cursor: pointer;
      font-family: serif;
      font-size: 15px;
      transition: 0.2s;
    }
  
    .tab.active {
      background: #b92d2d;
      color: white;
    }
  
    /* ======================================
       TAB CONTENT
    ====================================== */
    .tab-content {
      padding: 0 25px;
      margin-top: 15px;
      line-height: 1.7;
    }
  
    .sanskrit-block {
      white-space: pre-wrap;
      font-size: 28px;
      text-align: center;
      color: #5a2b2b;
      margin-bottom: 25px;
    }
  
    .translit {
      font-style: italic;
      font-size: 20px;
      color: #444;
    }
  
    .translation {
      font-size: 20px;
      text-align: justify;
      color: #333;
    }
  
    /* WORD GRID */
    .word-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
      gap: 15px;
    }
  
    .word-item {
      background: #fff6ea;
      border-left: 4px solid #b92d2d;
      padding: 12px;
      border-radius: 6px;
    }
  
    /* COMMENTARY */
    .commentary-title {
      background: #f3d1af;
      padding: 12px;
      border-radius: 6px;
      cursor: pointer;
      margin-bottom: 8px;
      font-weight: bold;
    }
  
    .commentary-text {
      background: #fff3e2;
      padding: 12px;
      border-radius: 6px;
      margin-bottom: 15px;
    }
  
    /* SCROLL TO TOP */
    .scroll-top {
      position: fixed;
      bottom: 30px;
      right: 30px;
      background: #b92d2d;
      color: #fff;
      width: 45px;
      height: 45px;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      border: none;
      transition: 0.2s;
    }
  
    .scroll-top:hover {
      transform: scale(1.1);
    }
  
    /* FOOTER */
    .footer {
      text-align: center;
      margin-top: 50px;
      padding-bottom: 40px;
      font-family: serif;
      color: #444;
    }
  </style>
  
  <!-- ======================================
       PAGE CONTENT
  ====================================== -->
  <div class="page-bg">
    <div class="container">
  
      <!-- NAVBAR -->
      <nav>
        <div class="logo">LOGO</div>
        <ul>
          <li>ĀYURVEDA</li>
          <li>YOGA SŪTRAS</li>
          <li>BHAGAVAD GĪTĀ</li>
          <li>UPANIṢADS</li>
          <li>SANSKRIT</li>
          <li>CONTACT US</li>
        </ul>
      </nav>
  
      <!-- Back button -->
      <div class="back-btn">&lt; BACK</div>
  
      <!-- HERO -->
      <section class="hero">
        <h1>BHAGAVAD GITA</h1>
      </section>
  
      <!-- CHAPTER TITLE -->
      <div class="chapter-title">CHAPTER 1</div>
  
      <!-- VERSE GRID -->
      <div class="verse-grid">
  
        <div class="verse-card" on:click={() => openModal("whole")}>
          Whole<br>Chapter
        </div>
  
        {#each verses as v}
          <div class="verse-card" on:click={() => openModal(v)}>
            {v}
          </div>
        {/each}
  
        <div class="verse-card">End<br>of<br>Chapter</div>
      </div>
  
      <!-- MODAL -->
      {#if modalOpen}
        <div class="modal-overlay">
          <div class="modal">
  
            <div class="close-btn" on:click={closeModal}>X</div>
  
            <div class="modal-header">
              <button class="nav-arrow">⟨</button>
              <div>Chapter 1 — Verse {selectedVerse}</div>
              <button class="nav-arrow">⟩</button>
            </div>
  
            <!-- Tabs -->
            <div class="tabs">
              <div class="tab {activeTab === 'sanskrit' ? 'active' : ''}" on:click={() => activeTab = 'sanskrit'}>Sanskrit</div>
              <div class="tab {activeTab === 'transliteration' ? 'active' : ''}" on:click={() => activeTab = 'transliteration'}>Transliteration</div>
              <div class="tab {activeTab === 'translation' ? 'active' : ''}" on:click={() => activeTab = 'translation'}>Translation</div>
              <div class="tab {activeTab === 'word' ? 'active' : ''}" on:click={() => activeTab = 'word'}>Word-by-word</div>
              <div class="tab {activeTab === 'commentary' ? 'active' : ''}" on:click={() => activeTab = 'commentary'}>Commentary</div>
            </div>
  
            <!-- Tab Content -->
            <div class="tab-content">
  
              {#if activeTab === 'sanskrit'}
                <pre class="sanskrit-block">{verseData.sanskrit}</pre>
  
                <audio controls style="width: 100%; margin-bottom:20px;">
                  <source src={verseData.audio} />
                </audio>
              {/if}
  
              {#if activeTab === 'transliteration'}
                <p class="translit">{verseData.transliteration}</p>
              {/if}
  
              {#if activeTab === 'translation'}
                <p class="translation">{verseData.translation}</p>
              {/if}
  
              {#if activeTab === 'word'}
                <div class="word-grid">
                  {#each verseData.wordByWord as item}
                    <div class="word-item">
                      <strong>{item.word}</strong><br />
                      <span>{item.meaning}</span>
                    </div>
                  {/each}
                </div>
              {/if}
  
              {#if activeTab === 'commentary'}
                {#each verseData.commentary as c, i}
                  <div>
                    <div class="commentary-title" on:click={() => expandedCommentary === i ? expandedCommentary = null : expandedCommentary = i}>
                      {c.author}
                    </div>
                    {#if expandedCommentary === i}
                      <div class="commentary-text">{c.text}</div>
                    {/if}
                  </div>
                {/each}
              {/if}
  
            </div>
          </div>
        </div>
      {/if}
  
      <!-- Scroll to top -->
      <button class="scroll-top" on:click={() => window.scrollTo({ top: 0, behavior: 'smooth' })}>↑</button>
  
    </div>
  
    <footer class="footer">
      <p>© 2025 Sanskrit.ie | All Rights Reserved</p>
      <p>info@sanskrit.ie</p>
    </footer>
  </div>
  