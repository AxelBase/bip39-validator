<!-- src/routes/blog/posts/post2/+page.svelte -->

<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>How the Validator Checks Words | BIP39 Validator Insights</title>
  <meta name="description" content="A technical explanation of the case-insensitive validation process using the embedded official BIP39 2048-word English list." />
  <meta property="og:title" content="How the Validator Checks Words | BIP39 Validator Insights" />
  <meta property="og:description" content="A technical explanation of the case-insensitive validation process using the embedded official BIP39 2048-word English list." />
  <meta property="og:url" content="{base}/blog/posts/post2" />
  <meta property="og:type" content="article" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/blog">Blog</a>
    <span>/</span>
    <p>How the Validator Checks Words</p>
  </div>

  <article class="prose">
    <h1>How the Validator Checks Words</h1>
    <p class="post-meta">Published: December 30, 2025</p>

    <p>The core function of this validator is simple yet precise: determine whether each word entered belongs to the official BIP39 English wordlist. The process is designed for accuracy, speed, and complete privacy, with every step occurring locally in your browser.</p>

    <p>When you enter a seed phrase, the tool first normalizes the input by converting all text to lowercase and splitting it on whitespace. This handles common formatting variations such as extra spaces, line breaks, or inconsistent capitalization that might occur during manual entry.</p>

    <p>Each resulting word is then compared against the complete 2048-word BIP39 English dictionary, which is embedded directly in the application. This eliminates any need for external requests and ensures the tool works offline.</p>

    <h2>The Validation Process Step by Step</h2>

    <p>First, the input string is trimmed of leading and trailing whitespace. It is then split using a regular expression that treats any sequence of spaces, tabs, or newlines as delimiters. Empty strings resulting from multiple consecutive delimiters are automatically filtered out.</p>

    <p>Next, every word is converted to lowercase. The BIP39 standard is case-insensitive for human readability, though the official list is presented in lowercase. This normalization ensures words like Abandon, ABANDON, or abandon are all treated identically.</p>

    <p>The normalized word is checked for exact membership in the wordlist array. If found, it is marked as valid. If not found, it is flagged as invalid. The comparison is strict: partial matches or similar-looking words are not accepted.</p>

    <h3>Why Case-Insensitive Matching</h3>

    <ul>
      <li>Users often write seed phrases in mixed case for readability</li>
      <li>Some wallets display words capitalized</li>
      <li>Prevents false negatives from formatting differences</li>
      <li>Maintains consistency with how humans perceive the phrases</li>
    </ul>

    <h3>Performance Considerations</h3>

    <p>With only 2048 words to check against and typical seed phrases containing at most 24 words, validation is instantaneous. The embedded list ensures no network latency, and the simple array lookup provides excellent performance even on low-powered devices.</p>

    <h2>FAQ</h2>

    <details>
      <summary>What happens with punctuation or special characters?</summary>
      <p>Any word containing punctuation or symbols will not match entries in the official list, which contains only lowercase letters. Such words will be correctly flagged as invalid.</p>
    </details>

    <details>
      <summary>Are near-matches accepted?</summary>
      <p>No. Only exact matches from the official list are considered valid. This prevents acceptance of common misspellings or similar-looking words.</p>
    </details>

    <details>
      <summary>Why embed the wordlist instead of fetching it?</summary>
      <p>Embedding ensures offline functionality, eliminates privacy risks from external requests, and guarantees the correct official list is always used.</p>
    </details>

    <p class="italic-note">Precise, private word validation forms the foundation of reliable seed phrase verification.</p>
  </article>

  <footer class="mt-5 pt-4 border-top text-center">
    <a href="{base}/blog" class="btn btn-outline-primary">&larr; Back to Blog Index</a>
  </footer>
</div>

<style>
  .post-layout {
    max-width: 800px;
    padding-top: 2rem;
    padding-bottom: 4rem;
  }

  .breadcrumbs {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
    font-size: 0.9rem;
    color: var(--color-text-muted);
  }
  .breadcrumbs a {
    color: var(--color-accent);
    text-decoration: none;
  }
  .breadcrumbs a:hover {
    text-decoration: underline;
    color: var(--color-accent-hover);
  }
  .breadcrumbs p {
    margin: 0;
    color: var(--color-text-main);
  }

  .prose {
    line-height: 1.8;
    color: var(--color-text-main);
  }

  .prose .post-meta {
    color: var(--color-text-muted);
    font-size: 0.9rem;
    margin-bottom: 2rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 1rem;
  }

  .prose h1, 
  .prose h2 {
    color: var(--color-accent);
    background: linear-gradient(135deg, var(--color-accent), #b8a655);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .prose h1 {
    font-size: 2.5rem;
    margin-bottom: 0.5rem;
  }

  .prose h2 {
    margin-top: 2.5rem;
    border-bottom: 1px solid var(--glass-border);
    padding-bottom: 0.5rem;
  }

  .prose p {
    color: var(--color-text-main);
    margin-bottom: 1.2rem;
  }

  .prose ul {
    list-style-type: '→ ';
    padding-left: 1.5rem;
    color: var(--color-text-main);
  }
  .prose ul li::marker {
    color: var(--color-accent);
  }
  .prose ul li {
    padding-left: 0.5rem;
    margin-bottom: 0.75rem;
  }

  .prose details {
    background: var(--glass-bg);
    border: 1px solid var(--glass-border);
    border-radius: var(--radius-lg);
    padding: 1.2rem;
    margin-bottom: 1.5rem;
    transition: all 0.3s ease;
  }

  .prose details[open] {
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  }

  .prose summary {
    cursor: pointer;
    font-weight: 600;
    color: var(--color-accent);
    list-style: none;
    padding: 0.5rem 0;
  }

  .prose summary::-webkit-details-marker {
    display: none;
  }

  .prose summary::before {
    content: '+';
    margin-right: 0.75rem;
    color: var(--color-accent);
    font-weight: bold;
    display: inline-block;
    width: 1.2em;
    transition: transform 0.2s ease;
  }

  .prose details[open] summary::before {
    transform: rotate(45deg);
  }

  .prose details p {
    margin-top: 1rem;
    padding-left: 1.5rem;
    border-left: 2px solid var(--color-accent);
    color: var(--color-text-muted);
  }

  .prose .italic-note {
    font-style: italic;
    color: var(--color-text-muted);
    text-align: center;
    margin-top: 3rem;
    padding: 1.5rem;
    background: var(--glass-bg);
    border-radius: var(--radius-lg);
  }

</style>