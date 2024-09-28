<script>
  import { onMount } from 'svelte';

  let visible = false;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.location');
    observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section class="location" class:visible>
  <div class="container">
    <h2 class="slide-in gradient-text">Unser Standort</h2>
    <div class="location-content">
      <div class="map-container fade-in">
        <img src="https://picsum.photos/600/400" alt="Karte des Predators Gym Standorts" class="static-map" />
      </div>
      <div class="contact-info fade-in">
        <h3>Predators Gym</h3>
        <p><strong>Adresse:</strong> Kämpferstraße 123, 8000 Zürich</p>
        <p><strong>Telefon:</strong> 044 123 45 67</p>
        <p><strong>E-Mail:</strong> info@predatorsgym.ch</p>
        <h4>Öffnungszeiten</h4>
        <p>Montag - Freitag: 06:00 - 22:00 Uhr</p>
        <p>Samstag: 08:00 - 20:00 Uhr</p>
        <p>Sonntag: 10:00 - 18:00 Uhr</p>
        <a href="https://goo.gl/maps/EXAMPLE" target="_blank" rel="noopener noreferrer" class="btn glow-button">Route planen</a>
      </div>
    </div>
  </div>
</section>

<style>
  .location {
    padding: 8rem 0;
    background-color: #111;
    color: #fff;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  h2 {
    text-align: center;
    margin-bottom: 4rem;
    font-size: 3.5rem;
    font-weight: 700;
    letter-spacing: -0.02em;
  }

  .location-content {
    display: flex;
    gap: 4rem;
    align-items: stretch;
  }

  .map-container {
    flex: 1;
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  }

  .static-map {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .map-container:hover .static-map {
    transform: scale(1.05);
  }

  .contact-info {
    flex: 1;
    background-color: rgba(255, 255, 255, 0.05);
    padding: 3rem;
    border-radius: 20px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  h3 {
    color: #fff;
    font-size: 2rem;
    margin-bottom: 1.5rem;
    font-weight: 600;
  }

  h4 {
    color: #fff;
    font-size: 1.5rem;
    margin-top: 2rem;
    margin-bottom: 1rem;
    font-weight: 600;
  }

  p {
    margin-bottom: 0.75rem;
    font-size: 1.1rem;
    color: #e0e0e0;
  }

  .btn {
    display: inline-block;
    background-color: #fff;
    color: #000;
    padding: 1rem 2rem;
    border-radius: 30px;
    text-decoration: none;
    font-weight: 600;
    font-size: 1.1rem;
    margin-top: 2rem;
    transition: all 0.3s ease;
    text-align: center;
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

  @media (max-width: 1024px) {
    .location {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 3rem;
    }

    .location-content {
      flex-direction: column;
    }

    .map-container, .contact-info {
      width: 100%;
    }

    .map-container {
      height: 400px;
    }
  }

  @media (max-width: 768px) {
    .location {
      padding: 4rem 0;
    }

    h2 {
      font-size: 2.5rem;
      margin-bottom: 2rem;
    }

    .map-container {
      height: 300px;
    }

    .contact-info {
      padding: 2rem;
    }

    h3 {
      font-size: 1.75rem;
    }

    h4 {
      font-size: 1.3rem;
    }

    p {
      font-size: 1rem;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2rem;
    }

    h3 {
      font-size: 1.5rem;
    }

    h4 {
      font-size: 1.2rem;
    }

    .btn {
      width: 100%;
    }
  }
</style>