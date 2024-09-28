<script>
  import { onMount } from 'svelte';

  const trainers = [
    {
      name: 'Thomas Kipfer',
      role: 'Gründer und Leiter des Gyms, Erwachsenentrainer',
      image: 'https://picsum.photos/200/200?random=1',
      bio: 'Mit über 20 Jahren Erfahrung in Kampfsportarten bringt Thomas Leidenschaft und Expertise in jede Klasse. Seine Hingabe zum Sport und zu seinen Schülern hat Predators zu einem führenden Namen im Kampfsporttraining gemacht. Als Gründer und Leiter des Gyms setzt er kontinuierlich neue Maßstäbe für Qualität und Innovation.'
    },
    {
      name: 'Lena',
      role: 'Kindertrainerin',
      image: 'https://picsum.photos/200/200?random=2',
      bio: 'Lena hat sich auf die Arbeit mit jungen Athleten spezialisiert und fördert von klein auf Disziplin, Selbstvertrauen und die Liebe zu Kampfkünsten. Ihr engagierter Lehrstil macht jede Klasse zu einem Abenteuer für unsere jüngsten Predators.'
    },
    {
      name: 'Annali Brugger',
      role: 'Fitness-Boxen Trainerin',
      image: 'https://picsum.photos/200/200?random=3',
      bio: 'Annali Brugger ist unsere Expertin für Fitness-Boxen. Als erfahrene und aktive Kämpferin bringt sie eine einzigartige Perspektive in ihre Kurse ein. Ihr Training kombiniert effektive Boxtechniken mit intensivem Konditionstraining, um Körper und Geist gleichermaßen herauszufordern.'
    }
  ];

  let visible = false;
  let activeTrainer = trainers[0];

  function setActiveTrainer(trainer) {
    activeTrainer = trainer;
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

    return () => observer.disconnect();
  });
</script>

<section class="trainers" class:visible>
  <div class="container">
    <h2 class="slide-in gradient-text">Unsere Experten-Trainer</h2>
    <div class="trainer-showcase">
      <div class="trainer-list">
        {#each trainers as trainer, index}
          <div 
            class="trainer-item fade-in" 
            class:active={trainer === activeTrainer}
            on:click={() => setActiveTrainer(trainer)}
            on:keydown={(e) => e.key === 'Enter' && setActiveTrainer(trainer)}
            style="animation-delay: {index * 0.2}s"
            tabindex="0"
          >
            <img src={trainer.image} alt={trainer.name} />
            <h3>{trainer.name}</h3>
            <h4>{trainer.role}</h4>
          </div>
        {/each}
      </div>
      <div class="trainer-details fade-in">
        <img src={activeTrainer.image} alt={activeTrainer.name} />
        <div class="trainer-info">
          <h3>{activeTrainer.name}</h3>
          <h4>{activeTrainer.role}</h4>
          <p>{activeTrainer.bio}</p>
        </div>
      </div>
    </div>
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

  .trainer-showcase {
    display: flex;
    gap: 2rem;
  }

  .trainer-list {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .trainer-item {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1rem;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .trainer-item:hover, .trainer-item.active {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateX(10px);
  }

  .trainer-item img {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    object-fit: cover;
  }

  .trainer-item h3 {
    font-size: 1.2rem;
    margin: 0;
  }

  .trainer-item h4 {
    font-size: 0.9rem;
    margin: 0;
    color: var(--secondary-text-color);
  }

  .trainer-details {
    flex: 2;
    display: flex;
    gap: 2rem;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 20px;
    padding: 2rem;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
    transition: all 0.3s ease;
  }

  .trainer-details:hover {
    transform: translateY(-5px);
    box-shadow: 0 30px 60px rgba(0, 0, 0, 0.4);
  }

  .trainer-details img {
    width: 200px;
    height: 200px;
    border-radius: 50%;
    object-fit: cover;
  }

  .trainer-info {
    flex: 1;
  }

  .trainer-info h3 {
    font-size: 2rem;
    margin-bottom: 0.5rem;
  }

  .trainer-info h4 {
    font-size: 1.2rem;
    margin-bottom: 1rem;
    color: var(--accent-color);
  }

  .trainer-info p {
    font-size: 1.1rem;
    line-height: 1.6;
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

  @media (max-width: 1024px) {
    .trainers {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 3rem;
    }

    .trainer-showcase {
      flex-direction: column;
    }

    .trainer-list {
      flex-direction: row;
      overflow-x: auto;
      padding-bottom: 1rem;
    }

    .trainer-item {
      flex: 0 0 auto;
      width: 200px;
      flex-direction: column;
      text-align: center;
    }

    .trainer-item img {
      width: 100px;
      height: 100px;
    }
  }

  @media (max-width: 768px) {
    .trainers {
      padding: 4rem 0;
    }

    h2 {
      font-size: 2.5rem;
      margin-bottom: 2rem;
    }

    .trainer-details {
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .trainer-details img {
      width: 150px;
      height: 150px;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2rem;
    }

    .trainer-info h3 {
      font-size: 1.6rem;
    }

    .trainer-info h4 {
      font-size: 1.1rem;
    }

    .trainer-info p {
      font-size: 1rem;
    }
  }
</style>