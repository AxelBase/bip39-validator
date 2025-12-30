<script>
  import { base } from '$app/paths';
  import { validateWords } from '$lib/wordlist';
  import { fade, fly, scale } from 'svelte/transition';

  let phrase = '';
  let results = [];
  let summary = '';

  function validate() {
    if (!phrase.trim()) {
      results = [];
      summary = 'Please enter a seed phrase.';
      return;
    }
    results = validateWords(phrase);
    const invalidCount = results.filter(r => !r.valid).length;
    summary = invalidCount === 0 ? 'All words are valid.' : `${invalidCount} invalid words found.`;
  }
</script>

<svelte:head>
  <title>BIP39 Seed Phrase Validator | Client-Side Wordlist Checker</title>
  <meta name="description" content="Free, privacy-focused tool to validate individual words in BIP39 seed phrases against the official English wordlist. Instant client-side checking with no data transmission." />
  <meta property="og:title" content="BIP39 Seed Phrase Validator | Client-Side Wordlist Checker" />
  <meta property="og:description" content="Free, privacy-focused tool to validate individual words in BIP39 seed phrases against the official English wordlist. Instant client-side checking with no data transmission." />
  <meta property="og:url" content="{base}/" />
  <meta property="og:type" content="website" />
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="BIP39 Seed Phrase Validator | Client-Side Wordlist Checker" />
  <meta name="twitter:description" content="Free, privacy-focused tool to validate individual words in BIP39 seed phrases against the official English wordlist. Instant client-side checking with no data transmission." />
</svelte:head>

<div class="container py-4">
  <div class="text-center mb-5" in:fade={{ duration: 1000 }}>
    <h1 class="display-4 fw-bold text-gradient mb-2">Secure Validator</h1>
    <p class="lead text-muted">Verify your BIP39 mnemonic phrases locally & safely.</p>
  </div>

  <section class="glass-card p-4 p-md-5 mb-5 mx-auto" style="max-width: 800px;" in:fly={{ y: 50, duration: 800 }}>
    <div class="mb-4">
      <label for="phrase" class="form-label fw-bold ps-2">Recovery Phrase</label>
      <textarea 
        id="phrase" 
        class="form-control bubbly-input" 
        rows="4" 
        placeholder="Enter your 12 or 24 words separated by spaces..."
        bind:value={phrase}>
      </textarea>
    </div>

    <div class="text-center">
      <button class="btn btn-primary btn-lg px-5 shadow" on:click={validate}>
        Validate Words
      </button>
    </div>

    {#if results.length > 0}
      <div class="mt-5" transition:fade>
        <div class="alert glass-card border-0 mb-4 text-center fw-bold" style="background: rgba(230, 214, 144, 0.1);">
          {summary}
        </div>
        
        <div class="word-grid">
          {#each results as { word, valid }, i}
            <div class="word-badge {valid ? 'valid' : 'invalid'}" in:scale={{ delay: i * 30 }}>
              <span class="index">{i + 1}</span>
              <span class="text">{word}</span>
            </div>
          {/each}
        </div>
      </div>
    {/if}
  </section>

  <div class="row g-4 mt-4">
<!-- src/routes/+page.svelte (updated sections) -->

<!-- About Section -->
<section id="about" class="col-md-6" in:fade={{ delay: 400 }}>
  <div class="glass-card p-4 h-100">
    <h3 class="h4 mb-3 text-gradient">About the BIP39 Seed Phrase Validator</h3>
    <p class="text-muted">
      The BIP39 Seed Phrase Validator is a lightweight, fully client-side web utility designed to help cryptocurrency users verify the accuracy of individual words in their recovery phrases against the official BIP39 English wordlist. Built with privacy and simplicity at its core, this tool addresses a common pain point in wallet management: catching transcription errors before they become irreversible problems.
    </p>
    <p class="text-muted">
      BIP39, introduced as Bitcoin Improvement Proposal 39, standardized the use of mnemonic phrases—typically 12, 18, or 24 words—as a human-readable method for backing up private keys. The standard defines a fixed list of exactly 2048 English words, each uniquely identifiable by its first four letters. These words are carefully chosen to minimize confusion and errors during manual entry or transcription.
    </p>
    <p class="text-muted">
      Unlike comprehensive BIP39 implementations that derive seeds and validate checksums, this validator intentionally limits its scope to wordlist membership only. This focused approach eliminates any need to process the full phrase as entropy, ensuring that no cryptographic operations occur and no sensitive data is exposed—even theoretically—during validation.
    </p>
    <p class="text-muted">
      All processing happens exclusively in your browser. The complete official wordlist is embedded directly in the application, requiring no network requests. Input is normalized for case and whitespace, then each word is checked with instant color-coded feedback: green for valid entries from the official list, red for anything else.
    </p>
    <p class="text-muted">
      This design makes the tool ideal for quick sanity checks when writing down a new seed phrase, transcribing an existing backup, or verifying suspicious words during recovery attempts. By catching typos, autocorrect changes, or non-standard words early, users can correct issues while the original phrase is still accessible, preventing potential lockouts.
    </p>
    <p class="text-muted">
      The validator supports best security practices by encouraging immediate verification and reducing reliance on memory. It serves as a complementary tool alongside official wallet software, which should always be used for final recovery and full checksum validation.
    </p>
    <p class="text-muted">
      Whether you are a new user setting up your first hardware wallet or an experienced holder reviewing backups, this utility provides a fast, private, and reliable way to ensure every word in your seed phrase belongs to the standard dictionary—helping maintain control over your digital assets with greater confidence.
    </p>
  </div>
</section>

<!-- How to Use Section -->
<section id="how-to" class="col-md-6" in:fade={{ delay: 600 }}>
  <div class="glass-card p-4 h-100">
    <h3 class="h4 mb-3 text-gradient">How to Use the Validator</h3>
    <p class="text-muted">
      Using the BIP39 Seed Phrase Validator is straightforward and requires no technical knowledge. The interface is intentionally minimal, allowing you to focus entirely on verifying your recovery phrase words quickly and securely.
    </p>
    <p class="text-muted">
      Start by locating the large text area on the main page, labeled for entering space-separated words. Paste your entire seed phrase directly into this field, or type it manually. The tool accepts phrases in any common format: words separated by single spaces, multiple spaces, tabs, or even each word on its own line.
    </p>
    <p class="text-muted">
      Capitalization does not matter—the validator automatically converts all input to lowercase for comparison against the official list. Extra whitespace is ignored during processing, so you do not need to worry about perfect formatting. Simply enter the phrase as it appears most convenient.
    </p>
    <p class="text-muted">
      Once your words are in the text area, click the "Validate" button or wait briefly—the tool processes input continuously. Results appear immediately below the input field. Each word is listed individually with clear visual indicators: valid words from the official BIP39 English wordlist appear in green, while any word not found in the standard dictionary is highlighted in red.
    </p>
    <p class="text-muted">
      A summary message at the top of the results section provides an overview: "All words are valid" when everything checks out, or a count of how many invalid words were detected. This makes it easy to see at a glance whether your phrase uses only standard BIP39 words.
    </p>
    <p class="text-muted">
      If invalid words are flagged, compare them carefully against your original written backup. Common issues include typos, autocorrect changes, added plurals, or confusion between similar-looking words. Correct the flagged entries directly in the text area and validate again until all words show as valid.
    </p>
    <p class="text-muted">
      For best results, perform validation immediately after receiving a new seed phrase from your wallet, while the original display is still visible. This is the safest time to catch and correct any transcription errors. You can also use the tool anytime you access or rewrite a backup to ensure ongoing accuracy.
    </p>
    <p class="text-muted">
      The validator works with any number of words, so you can check partial phrases or individual suspicious words if needed. Remember that order does not matter for wordlist validation—the tool checks each word independently.
    </p>
    <p class="text-muted">
      Following these simple steps helps build confidence that your recovery phrase contains only correct, standard BIP39 words—reducing the risk of issues during future wallet recovery procedures.
    </p>
  </div>
</section>

<!-- FAQ Section -->
<section id="faq" class="col-12" in:fade={{ delay: 800 }}>
  <div class="glass-card p-4">
    <h3 class="h4 mb-3 text-gradient text-center">Frequently Asked Questions</h3>
    <div class="row pt-2">
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Is my seed phrase safe to enter here?</h5>
        <p class="small text-muted">Yes, absolutely. The validator runs entirely in your browser—no data is sent to any server, stored, or transmitted. The official wordlist is embedded locally, and all processing occurs on your device only.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Does this tool validate the BIP39 checksum?</h5>
        <p class="small text-muted">No. It checks only that each word belongs to the official 2048-word English list. Full checksum validation requires seed derivation, which this tool intentionally avoids for maximum privacy.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Why focus only on wordlist validation?</h5>
        <p class="small text-muted">Most recovery issues stem from simple transcription errors. Checking individual words catches these early without exposing the full phrase to unnecessary processing, even client-side.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">What if a word is flagged as invalid?</h5>
        <p class="small text-muted">Double-check your original backup. Common causes include typos, autocorrect changes, added plurals, or handwriting misreads. Correct and re-validate until all words are green.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Can I use this offline?</h5>
        <p class="small text-muted">Once loaded, yes—the tool works without internet access since the wordlist is embedded and no external requests are made.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Are other languages supported?</h5>
        <p class="small text-muted">Currently only the standard English BIP39 wordlist is supported, as it is used by the vast majority of hardware and software wallets.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Should I still use my wallet's recovery process?</h5>
        <p class="small text-muted">Yes, always. This tool is for preliminary word checks only. Final recovery and checksum verification must be done through your official wallet software.</p>
      </div>
      <div class="col-md-6 mb-4">
        <h5 class="fw-bold">Is it safe on public computers?</h5>
        <p class="small text-muted">No. For real seed phrases, use only trusted, private devices to avoid risks from keyloggers or residual data.</p>
      </div>
    </div>
  </div>
</section>  </div>
</div>

<style>
  .bubbly-input {
    border-radius: 20px;
    padding: 1.2rem;
    border: 2px solid var(--glass-border) !important;
    background: var(--input-bg) !important;
    font-size: 1.1rem;
    color: var(--color-text-main) !important;
  }

  .word-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 12px;
  }

  .word-badge {
    padding: 10px 15px;
    border-radius: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
    font-weight: 600;
    background: var(--glass-bg);
    border: 1px solid var(--glass-border);
  }

  .word-badge .index { font-size: 0.7rem; opacity: 0.5; }
  
  .word-badge.valid { border-left: 4px solid #4ade80; }
  .word-badge.invalid { border-left: 4px solid #f87171; background: rgba(248, 113, 113, 0.05); }

  :global(html) { scroll-behavior: smooth; }
</style>