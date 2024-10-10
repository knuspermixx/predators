<script>
  import { onMount } from 'svelte';

  const trainers = [
    {
      name: 'Thomas Kipfer',
      role: 'Gründer & Erwachsenentrainer',
      image: 'https://picsum.photos/200/200?random=1',
      bio: 'Mit über 20 Jahren Erfahrung bringt Thomas Leidenschaft und Expertise in jede Klasse. Seine Hingabe hat Predators zu einem führenden Namen im Kampfsporttraining gemacht.'
    },
    {
      name: 'Lena',
      role: 'Kindertrainerin',
      image: 'https://picsum.photos/200/200?random=2',
      bio: 'Lena fördert von klein auf Disziplin, Selbstvertrauen und die Liebe zu Kampfkünsten. Ihr engagierter Lehrstil macht jede Klasse zu einem Abenteuer für unsere jüngsten Predators.'
    },
    {
      name: 'Annali Brugger',
      role: 'Fitness-Boxen Trainerin',
      image: 'https://picsum.photos/200/200?random=3',
      bio: 'Als erfahrene Kämpferin kombiniert Annali effektive Boxtechniken mit intensivem Konditionstraining, um Körper und Geist gleichermaßen herauszufordern.'
    }
  ];

  let visible = false;
  let currentTrainer = 0;
  let isMobile = false;
  let startX;

  function nextTrainer() {
    currentTrainer = (currentTrainer + 1) % trainers.length;
  }

  function prevTrainer() {
    currentTrainer = (currentTrainer - 1 + trainers.length) % trainers.length;
  }

  function handleTouchStart(event) {
    startX = event.touches[0].clientX;
  }

  function handleTouchEnd(event) {
    const endX = event.changedTouches[0].clientX;
    const diff = startX - endX;
    if (Math.abs(diff) > 50) {
      if (diff > 0) {
        nextTrainer();
      } else {
        prevTrainer();
      }
    }
  }

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.trainers');
    observer.observe(section);

    const checkMobile = () => {
      isMobile = window.innerWidth <= 768;
    };

    checkMobile();
    window.addEventListener('resize', checkMobile);

    return () => {
      observer.disconnect();
      window.removeEventListener('resize', checkMobile);
    };
  });
</script>

<section class="trainers" class:visible>
  <div class="container">
    <h2 class="slide-in gradient-text">Unsere Experten-Trainer</h2>
    
    {#if isMobile}
      <div class="trainer-mobile-container" 
           on:touchstart={handleTouchStart} 
           on:touchend={handleTouchEnd}>
        {#each trainers as trainer, index}
          <div class="trainer-slide" class:active={index === currentTrainer}>
            <img src={trainer.image} alt={trainer.name} />
            <div class="trainer-info">
              <h3>{trainer.name}</h3>
              <h4>{trainer.role}</h4>
              <p>{trainer.bio}</p>
            </div>
          </div>
        {/each}
        <div class="mobile-navigation">
          <button on:click={prevTrainer}>&lt;</button>
          <span>{currentTrainer + 1} / {trainers.length}</span>
          <button on:click={nextTrainer}>&gt;</button>
        </div>
      </div>
    {:else}
      <div class="trainer-grid">
        {#each trainers as trainer, index}
          <div class="trainer-item fade-in" style="animation-delay: {index * 0.2}s">
            <div class="trainer-image">
              <img src={trainer.image} alt={trainer.name} />
            </div>
            <div class="trainer-info">
              <h3>{trainer.name}</h3>
              <h4>{trainer.role}</h4>
              <p>{trainer.bio}</p>
            </div>
          </div>
        {/each}
      </div>
    {/if}
  </div>
</section>

<style>
  .trainers {
    padding: 8rem 0;
    background-color: var(--background-color);
    color: var(--text-color);
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

  .trainer-grid {
    display: flex;
    justify-content: space-between;
    gap: 2rem;
  }

  .trainer-item {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .trainer-image {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    overflow: hidden;
    margin-bottom: 1rem;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .trainer-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .trainer-info h3 {
    font-size: 1.8rem;
    margin-bottom: 0.5rem;
    color: var(--primary-color);
  }

  .trainer-info h4 {
    font-size: 1.2rem;
    margin-bottom: 1rem;
    color: var(--accent-color);
  }

  .trainer-info p {
    font-size: 1rem;
    line-height: 1.6;
    color: var(--secondary-text-color);
  }

  .trainer-mobile-container {
    position: relative;
    overflow: hidden;
  }

  .trainer-slide {
    display: none;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .trainer-slide.active {
    display: flex;
  }

  .mobile-navigation {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1rem;
  }

  .mobile-navigation button {
    background: none;
    border: none;
    font-size: 1.5rem;
    color: var(--accent-color);
    cursor: pointer;
  }

  .mobile-navigation span {
    margin: 0 1rem;
    color: var(--secondary-text-color);
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
    .trainers {
      padding: 4rem 0;
    }

    h2 {
      font-size: 2.5rem;
      margin-bottom: 2rem;
    }

    .trainer-image {
      width: 150px;
      height: 150px;
    }

    .trainer-info h3 {
      font-size: 1.5rem;
    }

    .trainer-info h4 {
      font-size: 1rem;
    }

    .trainer-info p {
      font-size: 0.9rem;
    }
  }
</style>