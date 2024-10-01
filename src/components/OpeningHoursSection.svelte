<script>
  import { onMount } from 'svelte';

  const schedule = [
    { 
      day: 'Montag', 
      classes: [
        { time: '17:30 - 18:30', name: 'Kindertraining', icon: 'child', instructor: 'Lena' },
        { time: '18:30 - 20:00', name: 'Erwachsenentraining', icon: 'user', description: 'Für Anfänger und Fortgeschrittene', instructor: 'Thomas Kipfer' }
      ]
    },
    { 
      day: 'Mittwoch', 
      classes: [
        { time: '19:30', name: 'Freies Training', icon: 'boxing-glove', description: 'Wettkampfvorbereitung und Sparring für Fortgeschrittene, aber auch für Anfänger', instructor: 'Thomas Kipfer' }
      ]
    },
    { 
      day: 'Donnerstag', 
      classes: [
        { time: '17:30 - 18:30', name: 'Kindertraining', icon: 'child', instructor: 'Lena' },
        { time: '18:30 - 20:00', name: 'Erwachsenentraining', icon: 'user', description: 'Für Anfänger und Fortgeschrittene', instructor: 'Thomas Kipfer' }
      ]
    },
    { 
      day: 'Samstag', 
      classes: [
        { time: '10:00 - 11:00', name: 'Fitness Boxen', icon: 'dumbbell', instructor: 'Annali Brugger' }
      ]
    },
  ];

  let visible = false;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.opening-hours');
    observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section class="opening-hours" class:visible>
  <div class="container">
    <h2 class="slide-in">Trainingsplan</h2>
    <p class="intro-text fade-in">Entdecken Sie unseren abwechslungsreichen Trainingsplan im Predators Gym. Egal ob Anfänger oder Fortgeschrittene – bei uns findet jeder das passende Training. Besuchen Sie uns und erleben Sie Kampfsport hautnah!</p>
    
    <div class="schedule-grid">
      {#each schedule as { day, classes }, index}
        <div class="schedule-item fade-in" style="animation-delay: {index * 0.1}s">
          <h3>{day}</h3>
          <ul>
            {#each classes as { time, name, icon, description, instructor }}
              <li>
                <div class="class-header">
                  <svg class="icon" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    {#if icon === 'child'}
                      <path d="M12 16C14.2091 16 16 14.2091 16 12C16 9.79086 14.2091 8 12 8C9.79086 8 8 9.79086 8 12C8 14.2091 9.79086 16 12 16Z" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M12 2V4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M12 20V22" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M4 12H2" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M22 12H20" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                    {:else if icon === 'user'}
                      <path d="M12 15C15.3137 15 18 12.3137 18 9C18 5.68629 15.3137 3 12 3C8.68629 3 6 5.68629 6 9C6 12.3137 8.68629 15 12 15Z" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M2.90625 20.2491C3.82834 18.6531 5.1542 17.3278 6.75064 16.4064C8.34708 15.485 10.1579 15 12.0011 15C13.8443 15 15.6552 15.4851 17.2516 16.4065C18.848 17.3279 20.1739 18.6533 21.0959 20.2493" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                    {:else if icon === 'boxing-glove'}
                      <path d="M12 6C7.58172 6 4 9.58172 4 14V19C4 20.1046 4.89543 21 6 21H18C19.1046 21 20 20.1046 20 19V14C20 9.58172 16.4183 6 12 6Z" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M12 6V3" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                    {:else if icon === 'dumbbell'}
                      <path d="M6 5V19" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M18 5V19" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M3 8H21" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                      <path d="M3 16H21" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
                    {/if}
                  </svg>
                  <span class="time">{time}</span>
                  <span class="class-name">{name}</span>
                </div>
                <div class="class-details">
                  {#if description}
                    <p class="description">{description}</p>
                  {/if}
                  <p class="instructor">Trainer: {instructor}</p>
                </div>
              </li>
            {/each}
          </ul>
        </div>
      {/each}
    </div>

    <div class="cta-container fade-in">
      <p class="cta-text">Neugierig geworden? Klicke hier, um zu erfahren, wo du uns findest:</p>
      <a href="#location" class="btn btn-primary glow-button">Standort anzeigen</a>
    </div>
  </div>
</section>

<style>
  .opening-hours {
    padding: 8rem 0;
    background-color: #111;
    overflow: hidden;
    color: #fff;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  h2 {
    text-align: center;
    margin-bottom: 2rem;
    font-size: 4rem;
    font-weight: 700;
    letter-spacing: -0.02em;
    background: linear-gradient(45deg, #fff, #f0f0f0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .intro-text {
    text-align: center;
    max-width: 800px;
    margin: 0 auto 4rem;
    font-size: 1.2rem;
    color: #e0e0e0;
    line-height: 1.6;
  }

  .schedule-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
    margin-bottom: 4rem;
  }

  .schedule-item {
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 20px;
    padding: 2rem;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
    transition: all 0.3s ease;
    backdrop-filter: blur(10px);
  }

  .schedule-item:hover {
    transform: translateY(-5px) scale(1.02);
    box-shadow: 0 30px 60px rgba(0, 0, 0, 0.4);
    background-color: rgba(255, 255, 255, 0.08);
  }

  h3 {
    color: #fff;
    margin-bottom: 1.5rem;
    font-size: 1.8rem;
    font-weight: 600;
    border-bottom: 2px solid rgba(255, 255, 255, 0.1);
    padding-bottom: 0.5rem;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  li {
    margin-bottom: 1.5rem;
    font-size: 1.1rem;
    color: #e0e0e0;
    transition: all 0.3s ease;
  }

  li:hover {
    transform: translateX(5px);
  }

  .class-header {
    display: flex;
    align-items: center;
    margin-bottom: 0.5rem;
  }

  .icon {
    margin-right: 1rem;
    color: #fff;
  }

  .time {
    font-weight: 600;
    margin-right: 0.5rem;
    color: #fff;
  }

  .class-name {
    flex-grow: 1;
    font-weight: 600;
  }

  .class-details {
    padding-left: 2.5rem;
  }

  .description {
    margin-bottom: 0.5rem;
    font-size: 0.95rem;
    color: #bbb;
  }

  .instructor {
    font-size: 0.9rem;
    font-style: italic;
    color: #999;
  }

  .cta-container {
    text-align: center;
    margin-top: 4rem;
    padding: 2rem;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 20px;
    backdrop-filter: blur(10px);
  }

  .cta-text {
    font-size: 1.4rem;
    margin-bottom: 1.5rem;
    color: #fff;
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
    transform: translateY(20px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }

  .visible .slide-in,
  .visible .fade-in {
    opacity: 1;
    transform: translateY(0);
  }

  @keyframes float {
    0% {
      transform: translateY(0px);
    }
    50% {
      transform: translateY(-10px);
    }
    100% {
      transform: translateY(0px);
    }
  }

  .schedule-item {
    animation: float 6s ease-in-out infinite;
  }

  .schedule-item:nth-child(odd) {
    animation-delay: -3s;
  }

  .glow-button {
    box-shadow: 0 0 10px rgba(255, 255, 255, 0.7), 0 0 20px rgba(255, 255, 255, 0.5);
  }

  @media (max-width: 1024px) {
    .opening-hours {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3.5rem;
      margin-bottom: 1.5rem;
    }

    .intro-text {
      font-size: 1.1rem;
      margin-bottom: 3rem;
    }

    .schedule-grid {
      grid-template-columns: 1fr;
    }
  }

  @media (max-width: 768px) {
    .opening-hours {
      padding: 4rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 1rem;
    }

    .intro-text {
      font-size: 1rem;
      margin-bottom: 2rem;
    }

    .cta-text {
      font-size: 1.2rem;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2.5rem;
    }

    h3 {
      font-size: 1.5rem;
    }

    .schedule-item {
      padding: 1.5rem;
    }

    li {
      font-size: 1rem;
    }

    .class-details {
      padding-left: 2rem;
    }

    .description {
      font-size: 0.9rem;
    }

    .instructor {
      font-size: 0.85rem;
    }

    .cta-text {
      font-size: 1.1rem;
    }

    .btn {
      font-size: 1rem;
      padding: 0.8rem 1.6rem;
    }
  }
</style>