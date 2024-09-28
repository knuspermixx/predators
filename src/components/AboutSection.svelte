<script>
  import { onMount } from 'svelte';
  let visible = false;
  let currentImageIndex = 0;

  const images = [
    'https://picsum.photos/id/1018/1000/800',
    'https://picsum.photos/id/1025/1000/800',
    'https://picsum.photos/id/1035/1000/800',
    'https://picsum.photos/id/1043/1000/800'
  ];

  function nextImage() {
    currentImageIndex = (currentImageIndex + 1) % images.length;
  }

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.about');
    observer.observe(section);

    const interval = setInterval(nextImage, 5000);

    return () => {
      observer.disconnect();
      clearInterval(interval);
    };
  });
</script>

<section class="about" class:visible>
  <div class="container">
    <h2 class="slide-in">Über Predators</h2>
    <div class="about-content">
      <div class="text-content fade-in">
        <p>
          Predators ist mehr als nur ein Fitnessstudio; es ist eine Gemeinschaft, die sich der persönlichen Entwicklung und der Exzellenz in Kampfkünsten verschrieben hat. Gegründet auf den Prinzipien von Disziplin, Respekt und kontinuierlicher Verbesserung bieten wir ein einzigartiges Trainingserlebnis, das Menschen aller Altersgruppen und Fähigkeitsstufen stärkt.
        </p>
        <p>
          Unsere hochmoderne Einrichtung und unsere erfahrenen Trainer schaffen eine Umgebung, in der Sie Ihre Grenzen erweitern, Selbstvertrauen aufbauen und Ihre Fitnessziele erreichen können. Bei Predators bilden wir nicht nur Kämpfer aus; wir formen Krieger fürs Leben.
        </p>
      </div>
      <div class="image-content fade-in">
        <div class="image-carousel">
          {#each images as image, index}
            <img
              src={image}
              alt="Predators Gym"
              class:active={index === currentImageIndex}
            />
          {/each}
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .about {
    padding: 8rem 0;
    background-color: #111;
    position: relative;
    overflow: hidden;
  }

  .about::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, rgba(0,0,0,0.8) 0%, rgba(0,0,0,0.4) 100%);
    z-index: 1;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
    position: relative;
    z-index: 2;
  }

  h2 {
    text-align: center;
    margin-bottom: 4rem;
    font-size: 4rem;
    font-weight: 700;
    letter-spacing: -0.02em;
    background: linear-gradient(45deg, #fff, #f0f0f0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .about-content {
    display: flex;
    gap: 4rem;
    align-items: center;
  }

  .text-content {
    flex: 1;
  }

  .image-content {
    flex: 1;
  }

  .image-carousel {
    position: relative;
    width: 100%;
    height: 400px;
    overflow: hidden;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
  }

  .image-carousel img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0;
    transition: opacity 0.5s ease-in-out;
  }

  .image-carousel img.active {
    opacity: 1;
  }

  p {
    font-size: 1.25rem;
    line-height: 1.8;
    margin-bottom: 1.5rem;
    color: #e0e0e0;
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
    margin-top: 1rem;
  }

  .btn-primary {
    background-color: #fff;
    color: #000;
  }

  .btn-primary:hover {
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
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .visible .slide-in,
  .visible .fade-in {
    opacity: 1;
    transform: translateY(0);
  }

  .glow-button {
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.7), 0 0 20px rgba(255, 255, 255, 0.5);
  }

  @media (max-width: 1024px) {
    .about {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3.5rem;
      margin-bottom: 3rem;
    }

    .about-content {
      flex-direction: column;
      gap: 3rem;
    }

    .text-content,
    .image-content {
      flex: none;
      width: 100%;
    }

    .image-carousel {
      height: 300px;
    }
  }

  @media (max-width: 768px) {
    .about {
      padding: 4rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 2rem;
    }

    p {
      font-size: 1.1rem;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2.5rem;
    }

    p {
      font-size: 1rem;
    }

    .btn {
      font-size: 1rem;
      padding: 0.8rem 1.6rem;
    }

    .image-carousel {
      height: 250px;
    }
  }
</style>