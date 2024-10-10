<script>
  import { onMount } from 'svelte';
  import './HeroSection.css';

  let videoElement;
  let visible = false;
  let menuOpen = false;
  let scrolled = false;
  let videoLoaded = false;

  function toggleMenu() {
    menuOpen = !menuOpen;
  }

  function loadVideo() {
    if (videoElement && !videoLoaded) {
      videoElement.src = "/video.mp4";
      videoElement.load();
      videoLoaded = true;
    }
  }

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
          loadVideo();
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.hero');
    observer.observe(section);

    window.addEventListener('scroll', () => {
      scrolled = window.scrollY > 50;
    });

    return () => {
      observer.disconnect();
      window.removeEventListener('scroll', () => {});
    };
  });
</script>

<div class="video-container">
  <video 
    bind:this={videoElement}
    autoplay 
    muted 
    loop 
    playsinline
  >
    <source type="video/mp4">
    Ihr Browser unterstützt das Video-Tag nicht.
  </video>
  {#if !videoLoaded}
    <div class="video-placeholder"></div>
  {/if}
</div>

<div class="overlay"></div>

<section class="hero" class:visible>
  <nav class="navbar" class:scrolled class:open={menuOpen}>
      <a href="/" class="logo">
        <span class="logo-container">
            <img src="/images/logo-short.png" alt="Predators Logo" class="logo-image ">
            <div class="logo-text">
              <p class="logo-title">Predators</p>
              <p class="logo-subtitle ">==twbd==</p>
            </div>
        </span>
      </a>
      <button class="menu-toggle" on:click={toggleMenu} aria-label="Menü umschalten">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <ul class="nav-links" class:open={menuOpen}>
        <li><a href="#about" on:click={toggleMenu}>Über uns</a></li>
        <li><a href="#classes" on:click={toggleMenu}>Kurse</a></li>
        <li><a href="#trainers" on:click={toggleMenu}>Trainer</a></li>
        <li><a href="#pricing" on:click={toggleMenu}>Preise</a></li>
      </ul>
  </nav>

  <div class="hero-content">
    <h1>
      <span class="fade-in glow-text" style="animation-delay: 0.2s;">Entfessle Deinen inneren</span>
      <span class="fade-in glow-text" style="animation-delay: 0.4s;">Krieger</span>
      <!-- <span class="fade-in glow-text" style="animation-delay: 0.6s;">Krieger</span> -->
    </h1>
    <p class="fade-in" style="animation-delay: 0.8s;">Erlebe die nächste Stufe des Kampfsporttrainings.</p>
    <div class="button-group fade-in" style="animation-delay: 1s;">
      <a href="#schedule" class="btn btn-secondary">Traingsplan</a>
      <a href="#pricing" class="btn btn-primary glow-button">Jetzt beitreten</a>
    </div>
  </div>
  <div class="social-icons-container fade-in" style="animation-delay: 1.2s;">
    <div class="social-icons left">
      <a href="#" aria-label="Facebook"><i class="fab fa-facebook"></i></a>
      <a href="#" aria-label="Instagram"><i class="fab fa-instagram"></i></a>
    </div>
    <div class="social-icons right">
      <a href="#" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
      <a href="#" aria-label="YouTube"><i class="fab fa-youtube"></i></a>
    </div>
  </div>
</section>
