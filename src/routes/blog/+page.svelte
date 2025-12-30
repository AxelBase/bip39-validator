<!-- src/routes/blog/+page.svelte -->

<script lang="ts">
  import { base } from '$app/paths';

  const posts = [
    { href: '/blog/posts/post1', title: 'Introduction to BIP39 Seed Phrase Validation', description: 'An overview of this client-side utility for checking individual words against the official BIP39 English wordlist.' },
    { href: '/blog/posts/post2', title: 'How the Validator Checks Words', description: 'Explore the case-insensitive validation process using the embedded 2048-word list.' },
    { href: '/blog/posts/post3', title: 'Getting Started with the Validator', description: 'Step-by-step guide to entering and validating your space-separated seed phrase words.' },
    { href: '/blog/posts/post4', title: 'Identifying and Fixing Invalid Words', description: 'Learn to spot common issues like typos or non-wordlist entries and understand the color-coded results.' },
    { href: '/blog/posts/post5', title: 'Why Focus on Wordlist Validation Only', description: 'Explanation of the tool\'s scope: checking words without full checksum or seed derivation for privacy.' },
    { href: '/blog/posts/post6', title: 'Common Mistakes in Seed Phrase Handling', description: 'Tips on avoiding errors like case mix-ups, extra spaces, or using unofficial words.' },
    { href: '/blog/posts/post7', title: 'Security Best Practices for Seed Phrases', description: 'Advice on safe usage of validation tools and protecting your mnemonic in offline environments.' },
  ];
</script>

<svelte:head>
  <title>Blog | BIP39 Validator Insights</title>
  <meta name="description" content="Articles, guides, and tips on using the BIP39 Seed Phrase Wordlist Validator for secure mnemonic verification." />
</svelte:head>

<div class="container fade-in blog-index">
  <header class="blog-header">
    <h1><i class="bi bi-journal-richtext"></i> Blog: BIP39 Validator Insights</h1>
    <p class="subtitle">
      In-depth articles and practical guides on BIP39 seed phrase validation, wordlist accuracy, and best practices for verifying mnemonic words securely.
    </p>
  </header>

  <div class="posts-grid">
    {#each posts as post}
      <a href="{base}{post.href}" class="card post-card">
        <div class="card-body">
          <h2 class="post-title">{post.title}</h2>
          <p class="post-description">{post.description}</p>
          <span class="read-more">Read Article &rarr;</span>
        </div>
      </a>
    {/each}
  </div>
</div>

<!-- Updated <style> tag for src/routes/blog/+page.svelte (Blog Index) -->
<style>
  .blog-index {
    padding-top: 2rem;
    padding-bottom: 4rem;
  }

  .blog-header {
    text-align: center;
    margin-bottom: 3rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 2rem;
  }

  .blog-header h1 {
    font-size: 2.8rem;
    margin-bottom: 1rem;
    background: linear-gradient(135deg, var(--color-accent), #b8a655);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .subtitle {
    font-size: 1.1rem;
    color: var(--color-text-muted);
    max-width: 700px;
    margin: 0 auto;
    line-height: 1.7;
  }

  .posts-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .post-card {
    text-decoration: none;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    background: var(--glass-bg);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid var(--glass-border);
    box-shadow: var(--glass-shadow);
    border-radius: var(--radius-lg);
    transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
  }

  .post-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 45px rgba(184, 166, 85, 0.2);
  }

  .post-card .card-body {
    display: flex;
    flex-direction: column;
    height: 100%;
    padding: 1.5rem;
  }

  .post-title {
    font-size: 1.25rem;
    color: var(--color-accent);
    margin-bottom: 0.75rem;
    background: linear-gradient(135deg, var(--color-accent), #b8a655);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .post-description {
    color: var(--color-text-muted);
    flex-grow: 1;
    margin-bottom: 1rem;
  }

  .read-more {
    color: var(--color-accent);
    font-weight: 600;
    align-self: flex-start;
    transition: all 0.3s ease;
  }

  .post-card:hover .read-more {
    transform: translateX(8px);
    color: var(--color-accent-hover);
  }
</style>