<script>
  import { onMount } from 'svelte';
  import './OpeningHoursSection.css';

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
                  <div class="time-name-container">
                    <span class="time">{time}</span>
                    <span class="class-name">{name}</span>
                  </div>
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

