<!-- src/routes/privacy/+page.svelte -->

<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Privacy Policy | BIP39 Validator Insights</title>
  <meta name="description" content="Our strict no-data-collection policy ensures complete privacy when validating BIP39 seed phrase words." />
  <meta property="og:title" content="Privacy Policy | BIP39 Validator Insights" />
  <meta property="og:description" content="Our strict no-data-collection policy ensures complete privacy when validating BIP39 seed phrase words." />
  <meta property="og:url" content="{base}/privacy" />
  <meta property="og:type" content="article" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a>
    <span>/</span>
    <p>Privacy Policy</p>
  </div>

  <article class="prose">
    <h1>Privacy Policy</h1>
    <p class="post-meta">Effective Date: December 30, 2025</p>

    <h2>1. Introduction</h2>
    <p>Welcome to the <strong>BIP39 Seed Phrase Validator</strong>, a fully client-side web utility ("we," "us," or "our"). This Privacy Policy explains our approach to user privacy when you use our tool to validate individual words against the official BIP39 English wordlist. We prioritize <strong>absolute privacy</strong> and have designed the application to ensure that <strong>no personal data or seed phrase information is ever collected, stored, or transmitted</strong>. All validation occurs locally in your browser, giving you complete control over your sensitive data.</p>

    <h2>2. Information We Do Not Collect</h2>
    <p>The validator operates without gathering any information whatsoever. Specifically, we do not collect:</p>
    <ul>
      <li><strong>Seed Phrase Data</strong>: Any words you enter are processed exclusively on your device and are never sent anywhere.</li>
      <li><strong>Personal Information</strong>: No names, email addresses, IP addresses, or device identifiers are recorded.</li>
      <li><strong>Usage Analytics</strong>: We do not track page views, session duration, clicks, or any behavioral data.</li>
      <li><strong>Technical Metadata</strong>: No browser fingerprints, location data, or referrer information is captured.</li>
    </ul>
    <p>Because the tool is <strong>stateless and purely client-side</strong>, your interactions leave no trace on our end.</p>

    <h2>3. How the Tool Works</h2>
    <p>When you use the validator:</p>
    <ul>
      <li><strong>Local Processing Only</strong>: Input is split, normalized, and checked against an embedded copy of the official 2048-word BIP39 English list using JavaScript running in your browser.</li>
      <li><strong>No Network Requests</strong>: The wordlist is bundled with the application; no external fetches occur during validation.</li>
      <li><strong>Ephemeral Data</strong>: Any text you enter exists only in browser memory for the duration of your session and is cleared on page reload or closure.</li>
    </ul>
    <p>This architecture guarantees <strong>zero data exposure</strong>, making it safe for verifying even real seed phrases.</p>

    <h2>4. Third-Party Services</h2>
    <p>We do not integrate any third-party analytics, advertising, or tracking services. The application uses only standard web technologies and Bootstrap via CDN for styling, with no tracking capabilities enabled.</p>

    <h2>5. Cookies and Tracking</h2>
    <p>The validator <strong>does not use cookies</strong>, localStorage for persistence, sessionStorage, or any tracking technologies. Your visit is completely anonymous.</p>

    <h2>6. Data Security</h2>
    <p>Since no data leaves your device, security relies on your local environment. We recommend using the tool on trusted, up-to-date devices and avoiding public or shared computers for sensitive validations.</p>

    <h2>7. Children's Privacy</h2>
    <p>Our tool is not directed at children under 13. We do not knowingly process data from children.</p>

    <h2>8. Changes to This Policy</h2>
    <p>We may update this policy occasionally. Changes will be reflected here with a new effective date.</p>

    <h2>9. Contact</h2>
    <p>For questions about this policy, please open an issue on our public GitHub repository.</p>

    <p class="italic-note">Your privacy is our highest priority—<strong>no data means no risk</strong>.</p>
  </article>
</div>

<!-- Updated <style> tag for blog posts, privacy, and terms pages -->
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

  .prose .italic-note {
    font-style: italic;
    color: var(--color-text-muted);
    text-align: center;
    margin-top: 3rem;
    padding: 1.5rem;
    background: var(--glass-bg);
    border-radius: var(--radius-lg);
    border: 1px solid var(--glass-border);
  }

</style>