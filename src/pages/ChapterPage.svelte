<script>
  const chapters = Array.from({ length: 18 }, (_, i) => i + 1);

  function goToChapter(n) {
    window.location.hash = `/chapter/${n}`;
  }
</script>

<!-- NAVBAR -->
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

<!-- PIXEL STRIP -->
<div class="pixel-strip"></div>

<!-- HERO SECTION -->
<div class="hero-wrapper">
  <div class="title-banner">
    <h1>BHAGAVAD GITA</h1>
  </div>

  <div class="hero-image"></div>
  <img src="/gita_open.png" class="book-img" />
</div>

<!-- PAGE TITLE -->
<div class="chapters-title">GITA CHAPTERS</div>

<!-- CHAPTER GRID -->
<div class="chapters-grid">
  {#each chapters as c}
    <div class="chapter-card" on:click={() => goToChapter(c)}>
      <img src="/chapter-img.jpg" class="chapter-img" />
      <div class="chapter-overlay">
        <span>{c}</span>
      </div>
    </div>
  {/each}
</div>

<!-- FOOTER -->
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

  <button class="scroll-up-btn" on:click={() => window.scrollTo({ top: 0, behavior: 'smooth' })}>
    ↑
  </button>
</footer>

<style>
  /* ———————————— Existing global styles apply from app.css ———————————— */

  /* Page title */
  .chapters-title {
    text-align: center;
    font-size: 34px;
    font-family: Georgia, serif;
    color: #b92d2d;
    margin-top: 200px;
    font-weight: bold;
  }

  .chapters-title::after {
    content: "";
    display: block;
    width: 220px;
    height: 2px;
    background: #b92d2d;
    margin: 10px auto 0;
  }

  /* Chapter grid (5 per row like original site) */
  .chapters-grid {
    width: 90%;
    margin: 50px auto;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 55px 25px;
    justify-items: center;
  }

  /* Diamond card */
  .chapter-card {
    width: 180px;
    height: 180px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transform: rotate(45deg);
    transition: 0.25s ease;
  }

  .chapter-card:hover {
    transform: rotate(45deg) scale(1.07);
  }

  /* Background image inside diamond */
  .chapter-img {
    width: 230px;
    height: 230px;
    object-fit: cover;
    transform: rotate(-45deg);
    position: absolute;
    top: -25px;
    left: -25px;
  }

  /* Overlay + number */
  .chapter-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.45);
    display: flex;
    justify-content: center;
    align-items: center;
    transform: rotate(-45deg);
  }

  .chapter-overlay span {
    color: white;
    font-family: Georgia, serif;
    font-size: 32px;
  }
</style>
