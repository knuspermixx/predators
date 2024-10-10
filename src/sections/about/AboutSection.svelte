<script>
  import { onMount } from 'svelte';
  import './AboutSection.css';

  let visible = false;
  let currentImageIndex = 0;
  let manuallyChanged = false;
  let interval;

  const images = [
    'https://picsum.photos/id/1018/1000/800',
    'https://picsum.photos/id/1025/1000/800',
    'https://picsum.photos/id/1035/1000/800',
    'https://picsum.photos/id/1043/1000/800'
  ];

  function nextImage() {
    currentImageIndex = (currentImageIndex + 1) % images.length;
    manuallyChanged = true;
    clearInterval(interval);
  }

  function prevImage() {
    currentImageIndex = (currentImageIndex - 1 + images.length) % images.length;
    manuallyChanged = true;
    clearInterval(interval);
  }

  function setImage(index) {
    currentImageIndex = index;
    manuallyChanged = true;
    clearInterval(interval);
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

    interval = setInterval(() => {
      if (!manuallyChanged) {
        currentImageIndex = (currentImageIndex + 1) % images.length;
      }
    }, 5000);

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
          <button class="nav-button prev" on:click={prevImage}>&#10094;</button>
          <button class="nav-button next" on:click={nextImage}>&#10095;</button>
          <div class="pagination-dots">
            {#each images as _, index}
              <span 
                class="dot" 
                class:active={index === currentImageIndex} 
                on:click={() => setImage(index)}
              ></span>
            {/each}
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
