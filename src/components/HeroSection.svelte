<script>
  import { onMount } from 'svelte';
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
      videoElement.src = "/videohd.mp4";
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
    style="width: 100%; height: 100%; object-fit: cover;"
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
    <div class="container">
      <a href="/" class="logo">
        <span class="logo-container">
            <img src="/images/logo-short.png" alt="Predators Logo" class="logo-image">
            <div class="logo-text">
              <p class="logo-title">Predators</p>
              <p class="logo-subtitle">twbd</p>
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
    </div>
  </nav>

  <div class="hero-content">
    <h1>
      <span class="fade-in glow-text" style="animation-delay: 0.2s;">Entfessle</span>
      <span class="fade-in glow-text" style="animation-delay: 0.4s;">Deinen inneren</span>
      <span class="fade-in glow-text" style="animation-delay: 0.6s;">Krieger</span>
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

<style>


  a {
    text-decoration: none;
    color: #fff;
  }

  .hero {
    height: 100svh;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    overflow: hidden;
    box-sizing: border-box;
  }

  .hero-content {
    text-align: left;
    z-index: 10;
    max-width: 1200px;
    width: 100%;
    padding: 0 2rem;
    box-sizing: border-box;
  }

  .glow-text {
    text-shadow: 0 0 1px rgba(255, 255, 255, 0.7), 0 0 20px rgba(255, 255, 255, 0.5), 0 0 30px rgba(255, 255, 255, 0.3);
  }

  .glow-button {
    box-shadow: 0 0 10x rgba(255, 255, 255, 0.7), 0 0 20px rgba(255, 255, 255, 0.5);
  }

  .navbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    padding: 1rem 0;
    transition: all 0.5s ease;
    backdrop-filter: blur(2px);
  }

  .navbar.scrolled {
    background-color: rgba(0, 0, 0, 0.8);
    padding: 0.5rem 0;
  }

  .navbar .container {
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 2rem;
  }

  .logo-container {
    display: flex;
    align-items: center;
  }

  .logo-image {
    height: 30px;
    width: auto;
    margin-right: 10px;
  }

  .logo-text {
    display: flex;
    flex-direction: column;
  }

  .logo-title {
    margin: 0;
    font-size: 1.2rem;
    font-weight: bold;
    color: #ffffff;
    letter-spacing: 1px;
    text-transform: uppercase;
    line-height: 1;
  }

  .logo-subtitle {
    margin: 0;
    font-size: 0.6rem;
    color: #ffffff;
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  .nav-links {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .nav-links li {
    margin-left: 2rem;
  }

  .nav-links a {
    color: #ffffff;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
    font-size: 1rem;
    position: relative;
    padding: 0.5rem 0;
  }

  .nav-links a::after {
    content: '';
    position: absolute;
    width: 0;
    height: 2px;
    bottom: 0;
    left: 0;
    background-color: #ffffff;
    transition: width 0.3s ease;
  }

  .nav-links a:hover::after {
    width: 100%;
  }

  .menu-toggle {
    display: none;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    z-index: 1001;
  }

  .menu-toggle span {
    display: block;
    width: 25px;
    height: 3px;
    margin: 5px 0;
    position: relative;
    background: #ffffff;
    border-radius: 3px;
    z-index: 1;
    transform-origin: 4px 0px;
    transition: transform 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
                background 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
                opacity 0.55s ease;
  }

  .menu-toggle.open span:first-child {
    transform: rotate(45deg) translate(5px, -5px);
  }

  .menu-toggle.open span:nth-child(2) {
    opacity: 0;
  }

  .menu-toggle.open span:last-child {
    transform: rotate(-45deg) translate(7px, -6px);
  }

  video {
    position: absolute;
    top: 50%;
    left: 50%;
    min-width: 100%;
    min-height: 100%;
    width: auto;
    height: auto;
    transform: translateX(-50%) translateY(-50%);
    z-index: -2;
    object-fit: cover;
  }

  .overlay {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
    z-index: -1;
  }

  h1 {
    font-size: 6rem;
    font-weight: 800;
    line-height: 1.1;
    margin-bottom: 1rem;
    color: #ffffff;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    letter-spacing: -1px;
  }

  h1 span {
    display: block;
  }

  p {
    font-size: 1.8rem;
    margin-bottom: 2rem;
    color: #ffffff;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
    font-weight: 300;
    line-height: 1.5;
    max-width: 600px;
  }

  .button-group {
    display: flex;
    gap: 1rem;
  }

  .btn {
    display: inline-block;
    padding: 1rem 2rem;
    text-decoration: none;
    font-weight: 600;
    font-size: 1.1rem;
    border-radius: 50px;
    transition: all 0.3s ease;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  .btn-primary {
    background-color: #ffffff;
    color: #000000;
  }

  .btn-secondary {
    background-color: transparent;
    color: #ffffff;
    border: 2px solid #ffffff;
  }

  .btn-primary:hover {
    background-color: rgba(255, 255, 255, 0.8);
    transform: translateY(-3px);
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2), 0 0 15px rgba(255, 255, 255, 0.8), 0 0 30px rgba(255, 255, 255, 0.6);
  }

  .btn-secondary:hover {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateY(-3px);
  }

  .social-icons-container {
    position: absolute;
    bottom: 2rem;
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    max-width: 1200px;
    width: 100%;
    margin: 0 auto;
    padding: 0 2rem;
    box-sizing: border-box;
    z-index: 10;
  }

  .social-icons {
    display: flex;
    gap: 1.5rem;
  }

  .social-icons a {
    color: #ffffff;
    font-size: 1.5rem;
    transition: all 0.3s ease;
  }

  .social-icons a:hover {
    color: #f0f0f0;
    transform: translateY(-3px);
  }

  .fade-in {
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.8s ease forwards;
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @media (max-width: 768px) {
    .hero-content {
      padding: 0 1rem;
    }

    .navbar .container {
      padding: 1rem;
    }

    .menu-toggle {
      display: block;
      position: relative;
      z-index: 1001;
      padding: 0.5rem;
      border-radius: 5px;
    }

    .nav-links {
      position: fixed;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100vh;
      flex-direction: column;
      background-color: rgba(0, 0, 0, 0.95);
      transition: left 0.3s ease;
      justify-content: center;
      align-items: center;
    }

    .nav-links.open {
      left: 0;
    }

    .nav-links li {
      margin: 1.5rem 0;
    }

    .nav-links a {
      font-size: 1.4rem;
    }

    h1 {
      font-size: 4.5rem;
    }

    p {
      font-size: 1.5rem;
    }

    .btn {
      font-size: 1rem;
      padding: 0.8rem 1.6rem;
    }

    .button-group {
      flex-direction: column;
      align-items: flex-start;
    }

    .logo-image {
      height: 30px;
    }

    .logo-title {
      font-size: 1.4rem;
    }

    .logo-subtitle {
      font-size: 0.7rem;
    }
  }

  @media (max-width: 480px) {
    .hero-content {
      padding: 0 1rem;
    }

    .navbar .container {
      padding: 1rem;
    }
    
    h1 {
      font-size: 3.5rem;
    }

    p {
      font-size: 1.3rem;
    }

    .social-icons-container {
      bottom: 1rem;
      padding: 0 1rem;
    }

    .social-icons a {
      font-size: 1.2rem;
    }

    .logo-image {
      height: 25px;
    }

    .logo-title {
      font-size: 1.2rem;
    }

    .logo-subtitle {
      font-size: 0.6rem;
    }
  }
</style>