<script>
  import { onMount } from 'svelte';

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

<style>
  .blog {
    padding: 8rem 0;
    background-color: var(--background-color);
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  h2 {
    text-align: center;
    margin-bottom: 4rem;
    color: var(--primary-color);
    font-size: 3.5rem;
    font-weight: 700;
    letter-spacing: -0.02em;
  }

  .blog-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 3rem;
  }

  .blog-card {
    background-color: var(--secondary-background);
    border-radius: 20px;
    overflow: hidden;
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .blog-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 30px 60px rgba(0, 0, 0, 0.2);
  }

  .blog-image {
    height: 250px;
    overflow: hidden;
  }

  .blog-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .blog-card:hover .blog-image img {
    transform: scale(1.05);
  }

  .blog-content {
    padding: 2rem;
  }

  h3 {
    font-size: 1.8rem;
    margin-bottom: 0.5rem;
    color: var(--primary-color);
    font-weight: 600;
  }

  .date {
    font-size: 1rem;
    color: var(--accent-color);
    margin-bottom: 1rem;
    font-weight: 500;
  }

  .excerpt {
    font-size: 1.1rem;
    line-height: 1.6;
    margin-bottom: 1.5rem;
    color: var(--secondary-text-color);
  }

  .read-more {
    display: inline-block;
    color: var(--accent-color);
    text-decoration: none;
    font-weight: 600;
    font-size: 1.1rem;
    transition: color 0.3s ease;
    position: relative;
  }

  .read-more::after {
    content: '';
    position: absolute;
    width: 100%;
    height: 2px;
    bottom: -4px;
    left: 0;
    background-color: var(--accent-color);
    transform: scaleX(0);
    transform-origin: bottom right;
    transition: transform 0.3s ease;
  }

  .read-more:hover::after {
    transform: scaleX(1);
    transform-origin: bottom left;
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
    .blog {
      padding: 6rem 0;
    }

    h2 {
      font-size: 3rem;
      margin-bottom: 3rem;
    }

    .blog-grid {
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    }
  }

  @media (max-width: 768px) {
    .blog {
      padding: 4rem 0;
    }

    h2 {
      font-size: 2.5rem;
      margin-bottom: 2rem;
    }

    .blog-grid {
      grid-template-columns: 1fr;
    }

    .blog-image {
      height: 200px;
    }

    h3 {
      font-size: 1.6rem;
    }

    .excerpt {
      font-size: 1rem;
    }
  }

  @media (max-width: 480px) {
    h2 {
      font-size: 2rem;
    }

    h3 {
      font-size: 1.4rem;
    }

    .blog-content {
      padding: 1.5rem;
    }
  }
</style>