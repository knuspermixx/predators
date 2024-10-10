<script>
  import { onMount } from 'svelte';
  import { fade, fly } from 'svelte/transition';
  import './FAQSection.css';
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
