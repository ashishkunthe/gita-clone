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

<!-- HERO SECTION -->
<div class="hero-wrapper">

  <!-- Title banner overlaps hero -->
  <div class="title-banner">
    <h1>BHAGAVAD GITA</h1>
  </div>

  <!-- Main background image -->
  <div class="hero-image"></div>

  <!-- Book Overlapping Bottom -->
  <img src="/gita_open.png" class="book-img" />

</div>

<!-- BACK BUTTON -->
<div class="back-btn">
  &lt; Back
</div>

<!-- CHAPTER TITLE -->
<div class="chapter-title">
  CHAPTER 1
</div>


<!-- Verse Label -->
<div class="verse-label">Verse</div>

<!-- VERSE GRID -->
<div class="verse-grid">
  <div class="scroll-card">
    <div class="scroll-label">Whole<br>Chapter</div>
  
    <button class="play-btn">
      <img src="/play.png" alt="play" />
    </button>
  </div>
  

  {#each Array.from({ length: 47 }, (_, i) => i + 1) as v}
  <div class="scroll-card">
    <div class="verse-number">{v}</div>
  
    <button class="play-btn">
      <img src="/play.png" alt="play" />
    </button>
  </div>
  
  {/each}

  <div class="scroll-card">
  <div class="scroll-label">End<br>of<br>Chapter</div>
  <button class="play-btn">
    <img src="/play.png" alt="play" />
  </button>
</div>

</div>

<footer class="footer-section">
  
  <!-- Connect + Social Icons -->
  <div class="connect-box">
    <span class="connect-title">Connect</span>

    <div class="social-icons">
      <div class="icon-circle">f</div>
      <div class="icon-circle">t</div>
      <div class="icon-circle">▶</div>
      <div class="icon-circle">✉</div>
    </div>
  </div>

  <!-- CENTER LOGO -->
  <img src="/footer.png" alt="footer-logo" class="footer-logo" />

  <!-- TITLE -->
  <div class="footer-title">WELLBEING~SVASTI</div>

  <!-- COPYRIGHT -->
  <div class="footer-copy">
    © 2025 Rutger Kortenhorst. All Rights Reserved | Design and Developed by
  </div>

  <!-- LINK -->
  <a class="footer-link" href="#">Burning Desire Inclusive</a>

  <!-- SCROLL TO TOP BUTTON -->
  <button class="scroll-up-btn" on:click={() => window.scrollTo({ top: 0, behavior: 'smooth' })}>
    ↑
  </button>

</footer>
