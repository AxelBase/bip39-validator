<script>
  import { wordlist } from '$lib/wordlist';
  import { fade, fly, scale } from 'svelte/transition';

  let searchQuery = '';

  // Reactive filtering logic
  $: filteredList = wordlist
    .map((word, index) => ({ word, index: index + 1 }))
    .filter(item => item.word.toLowerCase().includes(searchQuery.toLowerCase()));
</script>

<div class="container wordlist-container" in:fade={{ duration: 600 }}>
  
  <div class="header-section text-center mb-5" in:fly={{ y: -20, duration: 800 }}>
    <h1 class="display-4 fw-bold text-gradient">BIP39 English Wordlist</h1>
    <div class="accent-line"></div>
    <p class="text-muted mt-3 mx-auto" style="max-width: 600px;">
      The official <strong>2048-word</strong> list used for generating secure seed phrases. 
      All words are curated to be easily distinguishable.
    </p>
  </div>

  <div class="search-wrapper mx-auto mb-5" in:scale={{ duration: 500, delay: 200 }}>
    <div class="glass-card search-bar-inner d-flex align-items-center px-4">
      <i class="bi bi-search text-muted me-3" aria-hidden="true"></i>
      <input 
        id="word-search"
        type="text" 
        class="form-control bg-transparent border-0 shadow-none" 
        placeholder="Search for a word (e.g. 'abandon')..." 
        aria-label="Search BIP39 wordlist"
        bind:value={searchQuery}
      />
      {#if searchQuery}
        <button 
          class="btn btn-sm btn-clear" 
          on:click={() => searchQuery = ''}
          aria-label="Clear search"
          title="Clear search"
        >
          <i class="bi bi-x-circle-fill" aria-hidden="true"></i>
        </button>
      {/if}
    </div>
    <div class="text-center mt-3">
      <span class="badge rounded-pill bg-ivory text-dark">
        Showing {filteredList.length} of 2048 words
      </span>
    </div>
  </div>

  <div class="word-grid">
    {#each filteredList as { word, index } (index)}
      <div 
        class="word-pill-wrapper" 
        in:scale={{ duration: 300 }}
      >
        <div class="word-pill glass-card">
          <span class="word-index">{index}</span>
          <span class="word-text">{word}</span>
        </div>
      </div>
    {/each}
  </div>

  {#if filteredList.length === 0}
    <div class="text-center py-5" in:fade>
      <i class="bi bi-emoji-frown display-1 text-muted" aria-hidden="true"></i>
      <p class="mt-3 fs-5 text-muted">No words match your search.</p>
    </div>
  {/if}
</div>

<style>
  .wordlist-container {
    padding-top: 2rem;
    padding-bottom: 150px;
  }

  .header-section h1 {
    font-family: 'Quicksand', sans-serif;
  }

  .accent-line {
    width: 80px;
    height: 4px;
    background: var(--color-accent);
    margin: 0.5rem auto;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(230, 214, 144, 0.4);
  }

  .search-wrapper {
    max-width: 500px;
  }

  .search-bar-inner {
    height: 60px;
    border-radius: 50px !important;
    border: 2px solid var(--glass-border) !important;
  }

  .search-bar-inner input {
    color: var(--color-text-main) !important;
    font-weight: 600;
  }

  .bg-ivory {
    background-color: var(--color-accent);
    font-weight: 700;
  }

  .btn-clear {
    color: var(--color-text-muted);
    transition: color 0.2s;
    border: none;
    background: transparent;
  }
  .btn-clear:hover {
    color: var(--color-accent-hover);
  }

  .word-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 1.5rem;
    padding: 10px;
  }

  .word-pill {
    padding: 12px 20px;
    border-radius: 50px !important;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    gap: 15px;
    transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    cursor: default;
    border: 1px solid var(--glass-border) !important;
  }

  .word-pill:hover {
    transform: translateY(-8px) scale(1.05);
    background: var(--color-accent);
    border-color: var(--color-accent) !important;
  }

  .word-pill:hover .word-text {
    color: #4a4532;
  }

  .word-pill:hover .word-index {
    background: rgba(255, 255, 255, 0.5);
    color: #4a4532;
  }

  .word-index {
    background: var(--input-bg);
    color: var(--color-text-muted);
    font-size: 0.7rem;
    font-weight: 800;
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    flex-shrink: 0;
    transition: all 0.3s;
  }

  .word-text {
    font-weight: 600;
    color: var(--color-text-main);
    letter-spacing: 0.5px;
    transition: color 0.3s;
  }

  @media (max-width: 768px) {
    .word-grid {
      grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
      gap: 1rem;
    }
  }

  @media (max-width: 480px) {
    .word-grid {
      grid-template-columns: 1fr 1fr;
    }
  }
</style>