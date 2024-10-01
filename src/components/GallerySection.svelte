<script>
  import { onMount } from 'svelte';
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

<style>
  .gallery {
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
    font-size: 4rem;
    font-weight: 700;
    letter-spacing: -0.02em;
    background: linear-gradient(45deg, #fff, #f0f0f0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .image-grid {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-auto-rows: 200px;
    gap: 1rem;
  }

  .image-item {
    position: relative;
    overflow: hidden;
    cursor: pointer;
    border-radius: 12px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .image-item.small {
    grid-column: span 2;
    grid-row: span 1;
  }

  .image-item.medium {
    grid-column: span 3;
    grid-row: span 2;
  }

  .image-item.large {
    grid-column: span 4;
    grid-row: span 2;
  }

  .image-item:hover {
    transform: translateY(-5px) scale(1.02);
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
  }

  .image-item img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .image-item:hover img {
    transform: scale(1.05);
  }

  .lightbox {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.9);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
    opacity: 0;
    animation: fadeIn 0.3s ease forwards;
  }

  .lightbox img {
    max-width: 90%;
    max-height: 90%;
    object-fit: contain;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
    opacity: 0;
    transform: scale(0.9);
    animation: zoomIn 0.3s ease 0.1s forwards;
  }

  .close-button {
    position: absolute;
    top: 20px;
    right: 20px;
    width: 40px;
    height: 40px;
    background: rgba(255, 255, 255, 0.1);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: background-color 0.3s ease, transform 0.3s ease;
  }

  .close-button:hover {
    background: rgba(255, 255, 255, 0.2);
    transform: scale(1.1);
  }

  .close-button svg {
    width: 24px;
    height: 24px;
    stroke: #fff;
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

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  @keyframes zoomIn {
    from { opacity: 0; transform: scale(0.9); }
    to { opacity: 1; transform: scale(1); }
  }

  @media (max-width: 1024px) {
    .gallery {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3.5rem;
      margin-bottom: 3rem;
    }

    .container {
      padding: 0 1rem;
    }

    .image-grid {
      gap: 0.5rem;
    }
  }

  @media (max-width: 768px) {
    .gallery {
      padding: 4rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 2rem;
    }

    .image-grid {
      grid-auto-rows: 150px;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2.5rem;
    }

    .image-grid {
      grid-auto-rows: 100px;
    }

    .container {
      padding: 0 0.5rem;
    }
  }
</style>