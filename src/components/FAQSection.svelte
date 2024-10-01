<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';

  let faqs = [
    { 
      question: 'Brauche ich Vorkenntnisse, um mitzumachen?', 
      answer: 'Nein, wir begrüßen Anfänger und bieten Kurse für alle Leistungsstufen an. Unsere erfahrenen Trainer führen Sie durch die Grundlagen und helfen Ihnen, in Ihrem eigenen Tempo Fortschritte zu machen.'
    },
    { 
      question: 'Was sollte ich zu meiner ersten Stunde mitbringen?', 
      answer: 'Für Ihre erste Stunde bringen Sie bequeme Sportkleidung, eine Wasserflasche und eine positive Einstellung mit. Wir stellen alle notwendigen Geräte für den Kurs zur Verfügung. Es ist auch ratsam, etwa 15 Minuten früher zu kommen, um eventuelle Formulare auszufüllen.'
    },
    { 
      question: 'Gibt es eine Altersgrenze für die Kurse?', 
      answer: 'Wir haben Programme für alle Altersgruppen, einschließlich spezieller Kinderkurse und Erwachsenentraining. Unsere Jugendprogramme beginnen in der Regel ab 6 Jahren, aber wir empfehlen, uns für spezifische Informationen zu Altersgruppen zu kontaktieren.'
    },
    { 
      question: 'Wie oft sollte ich trainieren?', 
      answer: 'Die Trainingshäufigkeit hängt von Ihren Zielen und Ihrem Zeitplan ab. Für Anfänger empfehlen wir 2-3 Einheiten pro Woche. Mit zunehmender Erfahrung können Sie dies auf 3-5 Einheiten pro Woche erhöhen. Hören Sie auf Ihren Körper und übertreiben Sie es nicht, besonders am Anfang.'
    },
    { 
      question: 'Bieten Sie Einzelunterricht an?', 
      answer: 'Ja, wir bieten Einzelunterricht für diejenigen an, die eine individuellere Anleitung wünschen. Diese können je nach Verfügbarkeit mit jedem unserer Trainer vereinbart werden. Kontaktieren Sie uns für weitere Informationen zu Preisen und Terminplanung.'
    }
  ];

  let activeIndex = null;
  let visible = false;

  function toggleFAQ(index) {
    activeIndex = activeIndex === index ? null : index;
  }

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          visible = true;
        }
      });
    }, { threshold: 0.1 });

    const section = document.querySelector('.faq');
    observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section class="faq" class:visible>
  <div class="container">
    <h2 class="slide-in gradient-text">Häufig gestellte Fragen</h2>
    <div class="faq-list">
      {#each faqs as faq, index}
        <div class="faq-item fade-in" style="animation-delay: {index * 0.1}s">
          <button 
            class="faq-question" 
            class:active={activeIndex === index} 
            on:click={() => toggleFAQ(index)}
          >
            {faq.question}
            <div class="icon-container">
              <svg class="icon plus" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="12" y1="5" x2="12" y2="19"></line>
                <line x1="5" y1="12" x2="19" y2="12"></line>
              </svg>
              <svg class="icon minus" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <line x1="5" y1="12" x2="19" y2="12"></line>
              </svg>
            </div>
          </button>
          {#if activeIndex === index}
            <div class="faq-answer" transition:fly="{{ y: -20, duration: 300 }}">
              <p>{faq.answer}</p>
            </div>
          {/if}
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .faq {
    padding: 8rem 0;
    background-color: #111;
    color: #fff;
  }

  .container {
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

  .faq-list {
    /* max-width: 800px; */
    margin: 0 auto;
  }

  .faq-item {
    margin-bottom: 1.5rem;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.3s ease;
  }

  .faq-item:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .faq-question {
    width: 100%;
    text-align: left;
    background: none;
    border: none;
    padding: 1.5rem;
    color: #fff;
    font-size: 1.25rem;
    font-weight: 600;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: all 0.3s ease;
  }

  .faq-question:hover {
    background-color: rgba(255, 255, 255, 0.1);
  }

  .faq-question.active {
    background-color: rgba(255, 255, 255, 0.15);
  }

  .icon-container {
    position: relative;
    width: 24px;
    height: 24px;
  }

  .icon {
    position: absolute;
    top: 0;
    left: 0;
    width: 24px;
    height: 24px;
    transition: opacity 0.3s ease, transform 0.3s ease;
  }

  .icon.minus {
    opacity: 0;
    transform: rotate(-90deg);
  }

  .faq-question.active .icon.plus {
    opacity: 0;
    transform: rotate(90deg);
  }

  .faq-question.active .icon.minus {
    opacity: 1;
    transform: rotate(0);
  }

  .faq-answer {
    padding: 0 1.5rem 1.5rem;
  }

  .faq-answer p {
    margin: 0;
    line-height: 1.8;
    font-size: 1.1rem;
    color: #e0e0e0;
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
    .faq {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 3rem;
    }
  }

  @media (max-width: 768px) {
    .faq {
      padding: 4rem 0;
    }

    h2 {
      font-size: 2.5rem;
      margin-bottom: 2rem;
    }

    .faq-question {
      font-size: 1.1rem;
    }

    .faq-answer p {
      font-size: 1rem;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2rem;
    }

    .faq-question {
      font-size: 1rem;
      padding: 1.25rem;
    }

    .faq-answer {
      padding: 0 1.25rem 1.25rem;
    }
  }
</style>