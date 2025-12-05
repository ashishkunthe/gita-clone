<script>
  // Extract chapter from hash URL: #/chapter/1
  let chapter = window.location.hash.split("/")[2];
  console.log("CHAPTER:", chapter);

  let verses = [];
  let modalOpen = false;
  let selectedVerse = null;
  let verseData = null;

  async function loadVerses() {
    try {
      const url = `/api/geeta.php?q=${chapter}`;
      console.log("FETCH:", url);

      const res = await fetch(url);
      const json = await res.json();

      console.log("API RAW:", json);

      // FIX: real verse array is inside json.data
      verses = json.data;

      console.log("VERSES LOADED:", verses);

    } catch (err) {
      console.error("API ERROR:", err);
    }
  }

  loadVerses();

  function openVerse(v) {
    selectedVerse = v;
    verseData = verses[v - 1];  // correct indexing
    modalOpen = true;
  }

  function closeModal() {
    modalOpen = false;
  }
</script>

<nav class="top-nav">
  <img src="/nav-logo.png" class="nav-logo" />

  <div class="nav-center">
    <span class="search">&#128269;</span>
    <ul>
      <li>ĀYURVEDA ▼</li>
      <li>YOGASŪTRAS ▼</li>
      <li>BHAGAVAD GĪTĀ</li>
      <li>UPANIṢADS ▼</li>
      <li>SANSKRIT ▼</li>
      <li>CONTACT US</li>
    </ul>
  </div>
</nav>

<div class="pixel-strip"></div>

<div class="hero-wrapper">
  <div class="title-banner"><h1>BHAGAVAD GITA</h1></div>
  <div class="hero-image"></div>
  <img src="/gita_open.png" class="book-img" />
</div>

<div class="back-btn" on:click={() => history.back()}>&lt; Back</div>

<div class="chapter-title">CHAPTER {chapter}</div>

<div class="verse-label">Verse</div>

<div class="verse-grid">

  <!-- Whole chapter card -->
  <div class="scroll-card">
    <div class="scroll-label">Whole<br>Chapter</div>
    <button class="play-btn"><img src="/play.png" /></button>
  </div>

  {#each verses as v, i}
    <div class="scroll-card" on:click={() => openVerse(i + 1)}>
      <div class="verse-number">{i + 1}</div>
      <button class="play-btn"><img src="/play.png" /></button>
    </div>
  {/each}

  <div class="scroll-card">
    <div class="scroll-label">End<br>of<br>Chapter</div>
    <button class="play-btn"><img src="/play.png" /></button>
  </div>

</div>

{#if modalOpen}
<div class="modal-overlay">
  <div class="modal">

    <div class="modal-close" on:click={closeModal}>X</div>

    <h2>Verse {selectedVerse}</h2>

    <div class="modal-content">
      {@html verseData.lyrics}
    </div>

    {#if verseData.music}
      <audio controls class="audio-player">
        <source src={`https://sanskrit.ie/${verseData.music}`} />
      </audio>
    {/if}

  </div>
</div>
{/if}

<footer class="footer-section">
  <div class="connect-box">
    <span class="connect-title">Connect</span>

    <div class="social-icons">
      <div class="icon-circle">f</div>
      <div class="icon-circle">t</div>
      <div class="icon-circle">▶</div>
      <div class="icon-circle">✉</div>
    </div>
  </div>

  <img src="/footer.png" class="footer-logo" />
  <div class="footer-title">WELLBEING~SVASTI</div>

  <div class="footer-copy">© 2025 Rutger Kortenhorst. All Rights Reserved</div>
  <a class="footer-link" href="#">Burning Desire Inclusive</a>

  <button class="scroll-up-btn" on:click={() => window.scrollTo({ top: 0, behavior: "smooth" })}>↑</button>
</footer>
