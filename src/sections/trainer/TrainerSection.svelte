<script>
  import { onMount } from 'svelte';
  import './TrainerSection.css';

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
    <h2 class="slide-in">Unsere Experten-Trainer</h2>
    
    {#if isMobile}
      <div class="trainer-mobile-container" 
           on:touchstart={handleTouchStart} 
           on:touchend={handleTouchEnd}>
        {#each trainers as trainer, index}
          <div class="trainer-slide" class:active={index === currentTrainer}>
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
