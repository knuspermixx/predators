<script>
  import { onMount } from 'svelte';
  import './Footer.css';
  
  let visible = false;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const footer = document.querySelector('.footer');
    observer.observe(footer);

    return () => observer.disconnect();
  });
</script>

<footer class="footer" class:visible>
  <div class="container">
    <div class="footer-content">
      <div class="footer-info fade-in">
        <h3 class="gradient-text">Predators Gym</h3>
        <p><strong>Adresse:</strong> Kämpferstraße 123, 8000 Zürich</p>
        <p><strong>Telefon:</strong> 044 123 45 67</p>
        <p><strong>E-Mail:</strong> info@predatorsgym.ch</p>
      </div>
      <div class="footer-links fade-in">
        <h4>Quick Links</h4>
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#about">Über uns</a></li>
          <li><a href="#trainers">Trainer</a></li>
          <li><a href="#gallery">Galerie</a></li>
          <li><a href="#contact">Kontakt</a></li>
        </ul>
      </div>
      <div class="footer-social fade-in">
        <h4>Folge uns</h4>
        <div class="social-icons">
          <a href="#" target="_blank" rel="noopener noreferrer" aria-label="Facebook">
            <i class="fab fa-facebook-f"></i>
          </a>
          <a href="#" target="_blank" rel="noopener noreferrer" aria-label="Instagram">
            <i class="fab fa-instagram"></i>
          </a>
          <a href="#" target="_blank" rel="noopener noreferrer" aria-label="Twitter">
            <i class="fab fa-twitter"></i>
          </a>
        </div>
      </div>
    </div>
    <div class="copyright slide-in">
      <p>&copy; 2023 Predators Gym. Alle Rechte vorbehalten.</p>
    </div>
  </div>
</footer>
