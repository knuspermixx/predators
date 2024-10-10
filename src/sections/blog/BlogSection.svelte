<script>
  import { onMount } from 'svelte';
  import './BlogSection.css';
  
  let blogPosts = [
    { 
      title: 'Predators Fight Night 2024', 
      date: '2024-03-15', 
      excerpt: 'Join us for an unforgettable night of action-packed fights!',
      image: 'https://picsum.photos/seed/fight-night/600/400'
    },
    { 
      title: 'Regular CrossFit Sessions at CleverFit', 
      date: '2024-02-01', 
      excerpt: 'Enhance your training with our new partnership with CleverFit.',
      image: 'https://picsum.photos/seed/crossfit/600/400'
    },
    { 
      title: 'New Youth Program Launching', 
      date: '2024-01-15', 
      excerpt: 'Introducing our specialized program for young martial artists aged 8-12.',
      image: 'https://picsum.photos/seed/youth-program/600/400'
    },
    { 
      title: 'New Youth Program Launching', 
      date: '2024-01-15', 
      excerpt: 'Introducing our specialized program for young martial artists aged 8-12.',
      image: 'https://picsum.photos/seed/youth-program/600/400'
    }
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

    const section = document.querySelector('.blog');
    observer.observe(section);

    return () => observer.disconnect();
  });
</script>

<section class="blog" class:visible>
  <div class="container">
    <h2 class="slide-in">Latest News</h2>
    <div class="blog-grid">
      {#each blogPosts as post, index}
        <article class="blog-card fade-in" style="animation-delay: {index * 0.2}s">
          <div class="blog-image">
            <img src={post.image} alt={post.title} />
          </div>
          <div class="blog-content">
            <h3>{post.title}</h3>
            <p class="date">{post.date}</p>
            <p class="excerpt">{post.excerpt}</p>
            <a href="#" class="read-more">Read More</a>
          </div>
        </article>
      {/each}
    </div>
  </div>
</section>
