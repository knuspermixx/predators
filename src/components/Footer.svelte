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

<style>
  .footer {
    padding: 4rem 0 2rem;
    color: #fff;
    background-color: #111;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  .footer-content {
    display: flex;
    justify-content: space-between;
    gap: 2rem;
    margin-bottom: 2rem;
  }

  .footer-info, .footer-links, .footer-social {
    flex: 1;
  }

  h3 {
    font-size: 2rem;
    margin-bottom: 1rem;
    font-weight: 700;
  }

  h4 {
    color: #fff;
    font-size: 1.5rem;
    margin-bottom: 1rem;
    font-weight: 600;
  }

  p {
    margin-bottom: 0.5rem;
    font-size: 1rem;
    color: #e0e0e0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    margin-bottom: 0.5rem;
  }

  a {
    color: #e0e0e0;
    text-decoration: none;
    transition: color 0.3s ease;
  }

  a:hover {
    color: #fff;
  }

  .social-icons {
    display: flex;
    gap: 1rem;
  }

  .social-icons a {
    display: inline-block;
    width: 40px;
    height: 40px;
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 50%;
    text-align: center;
    line-height: 40px;
    transition: background-color 0.3s ease;
  }

  .social-icons a:hover {
    background-color: rgba(255, 255, 255, 0.2);
  }

  .copyright {
    text-align: center;
    margin-top: 2rem;
    padding-top: 2rem;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
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
    .footer-content {
      flex-direction: column;
    }

    .footer-info, .footer-links, .footer-social {
      text-align: center;
    }

    .social-icons {
      justify-content: center;
    }
  }
</style>