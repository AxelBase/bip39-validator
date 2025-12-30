<!-- src/routes/terms/+page.svelte -->

<script lang="ts">
  import { base } from '$app/paths';
</script>

<svelte:head>
  <title>Terms and Conditions | BIP39 Validator Insights</title>
  <meta name="description" content="Terms of use for the BIP39 Seed Phrase Validator, a free client-side tool with no warranties." />
  <meta property="og:title" content="Terms and Conditions | BIP39 Validator Insights" />
  <meta property="og:description" content="Terms of use for the BIP39 Seed Phrase Validator, a free client-side tool with no warranties." />
  <meta property="og:url" content="{base}/terms" />
  <meta property="og:type" content="article" />
  <meta name="twitter:card" content="summary_large_image" />
</svelte:head>

<div class="container fade-in post-layout">
  <div class="breadcrumbs">
    <a href="{base}/">Home</a>
    <span>/</span>
    <p>Terms and Conditions</p>
  </div>

  <article class="prose">
    <h1>Terms and Conditions</h1>
    <p class="post-meta">Effective Date: December 30, 2025</p>

    <h2>1. Acceptance of Terms</h2>
    <p>By accessing or using the <strong>BIP39 Seed Phrase Validator</strong> ("the Tool"), you agree to these Terms and Conditions. If you do not agree, please do not use the Tool. We reserve the right to modify these terms at any time, with changes effective upon posting.</p>

    <h2>2. Description of Service</h2>
    <p>The Tool is a free, open-source, client-side web application that validates individual words against the official BIP39 English wordlist. It performs <strong>no checksum validation</strong>, seed derivation, or cryptographic operations. All processing occurs locally in your browser.</p>

    <h2>3. Use of the Tool</h2>
    <p>You may use the Tool for personal, non-commercial purposes. Permitted uses include verifying seed phrase words for personal cryptocurrency wallet backups. You agree not to:</p>
    <ul>
      <li>Use the Tool for illegal purposes</li>
      <li>Attempt to reverse-engineer or interfere with its operation</li>
      <li>Distribute modified versions without clear attribution</li>
      <li>Misrepresent the Tool's capabilities (e.g., claiming full BIP39 validation)</li>
    </ul>

    <h2>4. No Warranties</h2>
    <p>The Tool is provided <strong>"as is"</strong> and <strong>"as available"</strong> without warranties of any kind, express or implied. We do not guarantee:</p>
    <ul>
      <li>Accuracy or completeness of validation results</li>
      <li>Uninterrupted or error-free operation</li>
      <li>Compatibility with all browsers or devices</li>
      <li>Suitability for any particular purpose</li>
    </ul>
    <p>Use at your own risk. Always verify critical seed phrases using official wallet software.</p>

    <h2>5. Limitation of Liability</h2>
    <p>To the fullest extent permitted by law, we shall not be liable for any direct, indirect, incidental, consequential, or punitive damages arising from your use of the Tool, including but not limited to loss of funds due to incorrect validation or user error.</p>

    <h2>6. User Responsibilities</h2>
    <p>You are solely responsible for:</p>
    <ul>
      <li>The security of your device and browser</li>
      <li>Proper backup and verification of seed phrases</li>
      <li>Understanding that the Tool checks only wordlist membership, not full phrase validity</li>
    </ul>
    <p><strong>Never enter real seed phrases on untrusted devices.</strong></p>

    <h2>7. Intellectual Property</h2>
    <p>The Tool is open-source and available under an appropriate license on GitHub. The embedded BIP39 wordlist is public domain.</p>

    <h2>8. Termination</h2>
    <p>We may restrict access to the Tool at any time without notice.</p>

    <h2>9. Governing Law</h2>
    <p>These terms are governed by applicable laws without regard to conflict of law principles.</p>

    <p class="italic-note">Use responsibly—<strong>your security depends on correct practices beyond this Tool</strong>.</p>
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