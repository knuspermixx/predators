<script>
  import { onMount } from 'svelte';
  import HeroSection from './components/HeroSection.svelte';
  import AboutSection from './components/AboutSection.svelte';
  import OpeningHoursSection from './components/OpeningHoursSection.svelte';
  import TrainerSection from './components/TrainerSection.svelte';
  import BlogSection from './components/BlogSection.svelte';
  import GallerySection from './components/GallerySection.svelte';
  import FAQSection from './components/FAQSection.svelte';
  import LocationSection from './components/LocationSection.svelte';
  let scrollY;

  onMount(() => {
    const handleIntersection = (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    };

    const observer = new IntersectionObserver(handleIntersection, {
      root: null,
      rootMargin: '0px',
      threshold: 0.1
    });

    document.querySelectorAll('section').forEach(section => {
      observer.observe(section);
    });

    // Load Font Awesome
    const script = document.createElement('script');
    script.src = 'https://kit.fontawesome.com/your-kit-id.js';
    script.crossOrigin = 'anonymous';
    document.head.appendChild(script);

    return () => observer.disconnect();
  });
</script>

<svelte:head>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" rel="stylesheet">
</svelte:head>

<svelte:window bind:scrollY />

<main>
  <HeroSection />
  <AboutSection />
  <OpeningHoursSection />
  <GallerySection />
  <TrainerSection />
  <BlogSection />
  <FAQSection />
  <LocationSection />
</main>


<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;
    background-color: var(--background-color);
    color: var(--text-color);
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  main {
    width: 100%;
    max-width: 100%;
    overflow-x: hidden;
  }

  :global(.container) {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  :global(section) {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  :global(section.visible) {
    opacity: 1;
    transform: translateY(0);
  }

 
  
</style>
