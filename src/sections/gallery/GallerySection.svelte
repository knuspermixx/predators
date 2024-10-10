<script>
  import { onMount } from 'svelte';
  import './GallerySection.css';
  let images = [
    { src: 'https://picsum.photos/600/400?random=1', alt: 'Trainingsszene 1', size: 'large' },
    { src: 'https://picsum.photos/300/200?random=2', alt: 'Trainingsszene 2', size: 'small' },
    { src: 'https://picsum.photos/300/200?random=3', alt: 'Trainingsszene 3', size: 'small' },
    { src: 'https://picsum.photos/450/300?random=4', alt: 'Trainingsszene 4', size: 'medium' },
    { src: 'https://picsum.photos/450/300?random=5', alt: 'Trainingsszene 5', size: 'medium' },
    { src: 'https://picsum.photos/600/400?random=6', alt: 'Trainingsszene 6', size: 'large' },
    { src: 'https://picsum.photos/300/200?random=7', alt: 'Trainingsszene 7', size: 'small' },
    { src: 'https://picsum.photos/300/200?random=8', alt: 'Trainingsszene 8', size: 'small' },
  ];

  let lightboxOpen = false;
  let currentImage = null;
  let visible = false;

  function openLightbox(image) {
    currentImage = image;
    lightboxOpen = true;
    document.body.style.overflow = 'hidden';
  }

  function closeLightbox() {
    lightboxOpen = false;
    currentImage = null;
    document.body.style.overflow = '';
  }

  onMount(() => {
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && lightboxOpen) {
        closeLightbox();
      }
    });

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.gallery');
    observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section class="gallery" class:visible>
  <div class="container">
    <h2 class="slide-in">Predators in Aktion</h2>
    <div class="image-grid">
      {#each images as image, index}
        <div class="image-item fade-in {image.size}" on:click={() => openLightbox(image)} style="animation-delay: {index * 0.1}s">
          <img src={image.src} alt={image.alt} />
        </div>
      {/each}
    </div>
  </div>
</section>

{#if lightboxOpen}
  <div class="lightbox" on:click={closeLightbox}>
    <img src={currentImage.src} alt={currentImage.alt} />
    <button class="close-button" on:click|stopPropagation={closeLightbox}>
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <line x1="18" y1="6" x2="6" y2="18"></line>
        <line x1="6" y1="6" x2="18" y2="18"></line>
      </svg>
    </button>
  </div>
{/if}

