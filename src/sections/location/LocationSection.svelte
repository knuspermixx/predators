<script lang="ts">
  import { onMount } from 'svelte';
  import './LocationSection.css';

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

<section class="location" class:visible>
  <div class="container">
    <h2 class="slide-in gradient-text">Unser Standort</h2>
    <div class="location-content">
      <div class="map-container fade-in">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2702.3985346774936!2d8.536190315641454!3d47.37659997916941!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47900a08cc0e6e41%3A0x9d56e9a7e0aeaab9!2zWsO8cmljaCwgU2Nod2Vpeg!5e0!3m2!1sde!2sde!4v1623338982913!5m2!1sde!2sde"
          width="100%"
          height="100%"
          style="border:0;"
          allowfullscreen
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
    <div class="contact-form fade-in">
      <h3>Kontaktieren Sie uns</h3>
      <form>
        <div class="form-group">
          <input type="text" id="name" name="name" required placeholder="Name">
        </div>
        <div class="form-group">
          <input type="email" id="email" name="email" required placeholder="E-Mail">
        </div>
        <div class="form-group">
          <textarea id="message" name="message" required placeholder="Ihre Nachricht"></textarea>
        </div>
        <button type="submit" class="btn glow-button">Nachricht senden</button>
      </form>
    </div>
  </div>
</section>
