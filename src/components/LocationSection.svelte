<script lang="ts">
  import { onMount } from 'svelte';

  let visible: boolean = false;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.location');
    if (section) {
      observer.observe(section);
    }

    return () => observer.disconnect();
  });
</script>

<section class="location" class:visible={visible}>
  <div class="container">
    <h2 class="slide-in gradient-text">Unser Standort</h2>
    <div class="location-content">
      <div class="map-container fade-in">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2702.3985346774936!2d8.536190315641454!3d47.37659997916941!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47900a08cc0e6e41%3A0x9d56e9a7e0aeaab9!2zWsO8cmljaCwgU2Nod2Vpeg!5e0!3m2!1sde!2sde!4v1623338982913!5m2!1sde!2sde"
          width="100%"
          height="100%"
          style="border:0;"
          allowfullscreen=""
          loading="lazy"
          title="Standort von Predators Gym"
        ></iframe>
      </div>
      <div class="contact-info fade-in">
        <h3>Predators Gym</h3>
        <div class="contact-info-text">
          <p><strong>Adresse:</strong> Kämpferstraße 123, 8000 Zürich</p>
          <p><strong>Telefon:</strong> 044 123 45 67</p>
          <p><strong>E-Mail:</strong> info@predatorsgym.ch</p>
        </div>
        <a href="https://goo.gl/maps/EXAMPLE" target="_blank" rel="noopener noreferrer" class="btn glow-button">Route planen</a>
      </div>
    </div>
  </div>
</section>

<style>
  .location {
    padding: 4rem 0;
    color: #fff;
    background-color: #111;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  h2 {
    text-align: center;
    margin-bottom: 3rem;
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 700;
    letter-spacing: -0.02em;
  }

  .location-content {
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
  }

  .map-container, .contact-info {
    flex: 1 1 500px;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  }

  .map-container {
    aspect-ratio: 16 / 9;
  }

  .map-container iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }

  .contact-info {
    background-color: rgba(255, 255, 255, 0.05);
    padding: 2rem;
    display: flex;
    flex-direction: column;
    gap:1.5rem;

  
  }



  h3 {
    color: #fff;
    font-size: clamp(1.5rem, 4vw, 2rem);
    font-weight: 600;
  }

  p {
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    color: #e0e0e0;
    margin: 0.2rem;
  }

  .btn {
    display: inline-block;
    background-color: #fff;
    color: #000;
    padding: 0.8rem 1.5rem;
    border-radius: 30px;
    text-decoration: none;
    font-weight: 600;
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    margin-top: auto;
    transition: all 0.3s ease;
    text-align: center;
    align-self: flex-start;
  }

  .btn:hover {
    background-color: rgba(255, 255, 255, 0.9);
    transform: translateY(-3px);
  }

  .slide-in {
    opacity: 0;
    transform: translateY(50px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .fade-in {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .visible .slide-in,
  .visible .fade-in {
    opacity: 1;
    transform: translateY(0);
  }

  @media (max-width: 768px) {
    .location {
      padding: 3rem 0;
    }

    .map-container {
      aspect-ratio: 4 / 3;
    }

    .btn {
      align-self: stretch;
      text-align: center;
    }
  }
</style>