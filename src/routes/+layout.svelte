<script lang="ts">
  import '../app.css';
  import { base } from '$app/paths';
  import { slide, fly } from 'svelte/transition';
  import { onMount } from 'svelte';

  let isDropdownOpen = false;
  let isDark = false;

  function toggleTheme() {
    isDark = !isDark;
    document.body.dataset.bsTheme = isDark ? 'dark' : 'light';
  }

  const toggleDropdown = () => (isDropdownOpen = !isDropdownOpen);
  const closeDropdown = () => (isDropdownOpen = false);

  function clickOutside(node: HTMLElement) {
    const handleClick = (event: MouseEvent) => {
      if (node && !node.contains(event.target as Node)) {
        node.dispatchEvent(new CustomEvent('click_outside'));
      }
    };
    document.addEventListener('click', handleClick, true);
    return {
      destroy() {
        document.removeEventListener('click', handleClick, true);
      }
    };
  }
</script>

<header class="fixed-top p-3 w-100" style="z-index: 1050;">
  <nav
    class="container glass-card rounded-pill px-4 py-2 d-flex justify-content-between align-items-center shadow-sm"
    style="max-width: 1100px;"
  >
    <div class="d-flex align-items-center gap-3">
      <a href="{base}/" class="d-flex align-items-center gap-2 text-decoration-none">
        <img src="{base}/AxelLab-Logo.ico" alt="Logo" class="nav-logo" />
        <span class="fw-bold fs-5 brand-text">AxelBase</span>
      </a>

      <!-- Buy Me a Coffee + Bitcoin Dropdown -->
      <div class="position-relative ms-2" use:clickOutside on:click_outside={closeDropdown}>
        <button
          class="btn btn-coffee d-flex align-items-center gap-2 px-3 py-2"
          on:click={toggleDropdown}
          aria-label="Support AxelBase"
        >
          <i class="bi bi-cup-hot-fill"></i>
          <span class="d-none d-md-inline fw-semibold">Support</span>
        </button>

        {#if isDropdownOpen}
          <div
            class="bmac-dropdown glass-card p-2 shadow-lg"
            transition:fly={{ y: -10, duration: 220 }}
          >
            <a
              href="https://buymeacoffee.com/axelbase"
              target="_blank"
              rel="noopener"
              on:click={closeDropdown}
              class="donation-link amount-item"
            >
              <span class="amount">$3</span> One Coffee
            </a>

            <a
              href="https://buymeacoffee.com/axelbase"
              target="_blank"
              rel="noopener"
              on:click={closeDropdown}
              class="donation-link amount-item"
            >
              <span class="amount">$5</span> Two Coffees
            </a>

            <a
              href="https://buymeacoffee.com/axelbase"
              target="_blank"
              rel="noopener"
              on:click={closeDropdown}
              class="donation-link amount-item"
            >
              <span class="amount">$10</span> Three Coffees
            </a>

            <a
              href="https://buymeacoffee.com/axelbase"
              target="_blank"
              rel="noopener"
              on:click={closeDropdown}
              class="donation-link custom-amount"
            >
              Custom Amount
            </a>

            <a
              href="bitcoin:bc1q3p0e6vt492m4w4fpz5m2cl4zcfuqqkgaj6myc9?label=AxelBase&message=Buy%20me%20a%20coffee"
              target="_blank"
              rel="noopener"
              on:click={closeDropdown}
              class="donation-link custom-amount bitcoin-option"
            >
              Buy via Crypto (Bitcoin)
            </a>
          </div>
        {/if}
      </div>
    </div>

    <div class="d-flex align-items-center gap-3">
      <ul class="nav d-none d-lg-flex gap-2 m-0">
        <li><a class="nav-link-custom" href="{base}/">Home</a></li>
        <li><a class="nav-link-custom" href="{base}/#about">About</a></li>
        <li><a class="nav-link-custom" href="{base}/#how-to">How to use</a></li>
        <li><a class="nav-link-custom" href="{base}/#faq">FAQ</a></li>
        <li><a class="nav-link-custom" href="{base}/wordlist">Wordlist</a></li>
        <li>
          <a class="btn btn-primary btn-sm px-3" href="{base}/blog">Blog</a>
        </li>
      </ul>

      <div class="vr d-none d-lg-block mx-2"></div>

<button
  class="btn-theme-toggle"
  on:click={toggleTheme}
  aria-label="Toggle theme"
  title={isDark ? "Switch to light mode" : "Switch to dark mode"}
>
  {#if isDark}
    <i class="bi bi-sun-fill"></i>
  {:else}
    <i class="bi bi-moon-stars-fill"></i>
  {/if}
</button>    </div>
  </nav>
</header>

<main style="padding-top: 100px; padding-bottom: 80px;">
  <slot />
</main>

<footer
  class="releative glass-card border-0 rounded-0 py-3 shadow-lg"
  style="border-top: 1px solid var(--glass-border) !important;"
>
  <div
    class="container d-flex flex-column flex-sm-row justify-content-between align-items-center small text-muted"
  >
    <span class="fw-medium"
      >© {new Date().getFullYear()} AxelBase BIP39 Seed Phrase Validator</span
    >
    <div class="d-flex gap-4">
      <a href="{base}/privacy" class="footer-link">Privacy</a>
      <a href="{base}/terms" class="footer-link">Terms</a>
    </div>
  </div>
</footer>

<style>
  .nav-logo {
    height: 35px;
    transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  .nav-logo:hover {
    transform: rotate(15deg) scale(1.2);
  }

  .brand-text {
    color: var(--color-text-main);
    font-family: 'Quicksand', sans-serif;
  }

  .nav-link-custom {
    text-decoration: none;
    color: var(--color-text-muted);
    font-weight: 600;
    padding: 8px 15px;
    transition: color 0.3s;
  }
  .nav-link-custom:hover {
    color: var(--color-accent);
  }

  /* Support Button (blending both styles) */
  .btn-coffee {
    background: #ffdd00;
    color: #4a4532;
    border: none;
    font-size: 0.9rem;
    font-weight: 600;
    padding: 8px 16px;
    border-radius: 50px;
    transition: all 0.3s ease;
  }

  .btn-coffee:hover {
    background: #ffe54c;
    box-shadow: 0 5px 15px rgba(255, 221, 0, 0.35);
    transform: translateY(-1px);
  }

  .btn-theme-toggle {
    background: var(--input-bg);
    border: 1px solid var(--glass-border);
    color: var(--color-text-main);
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .btn-theme-toggle:hover {
    transform: rotate(45deg) scale(1.1);
    background: var(--color-accent);
  }

  /* Dropdown - improved version with glass style */
  .bmac-dropdown {
    position: absolute;
    top: 110%;
    left: 50%;
    transform: translateX(-50%);
    width: 240px;
    background: var(--glass-bg);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid var(--glass-border);
    border-radius: 16px;
    box-shadow: var(--glass-shadow);
    overflow: hidden;
    z-index: 1000;
  }

  .donation-link {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 11px 18px;
    color: var(--color-text-main);
    text-decoration: none;
    font-size: 0.95rem;
    transition: all 0.2s ease;
  }

  .donation-link:hover {
    background: var(--color-accent);
    color: #4a4532;
    padding-left: 24px;
  }

  .amount {
    font-weight: 800;
    color: #e6d690;
    font-size: 1.15rem;
    min-width: 38px;
  }

  .amount-item {
    justify-content: flex-start;
    gap: 12px;
  }

  .custom-amount {
    font-weight: 700;
    color: var(--color-accent);
    border-top: 1px solid var(--glass-border);
    justify-content: center !important;
    padding: 14px !important;
  }

  .bitcoin-option {
    color: #f7931a !important;
    font-weight: 700;
  }

  .bitcoin-option:hover {
    background: #f7931a !important;
    color: white !important;
  }

  .footer-link {
    color: var(--color-text-muted);
    text-decoration: none;
    font-weight: 600;
  }

  .footer-link:hover {
    color: var(--color-accent);
  }
</style>