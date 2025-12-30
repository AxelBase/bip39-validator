<script lang="ts">
  import '../app.css';
  import { base } from '$app/paths';
  import { slide, fade } from 'svelte/transition';
  import { onMount } from 'svelte';

  const paypalUsername = 'AxelLab427'; 
  const donationAmounts = [1, 3, 5, 10];
  let isDropdownOpen = false;
  let isDark = false;

  function toggleTheme() {
    isDark = !isDark;
    document.body.dataset.bsTheme = isDark ? 'dark' : 'light';
  }

  const toggleDropdown = () => isDropdownOpen = !isDropdownOpen;
  const closeDropdown = () => isDropdownOpen = false;

  function clickOutside(node: HTMLElement) {
    const handleClick = (event: MouseEvent) => {
      if (node && !node.contains(event.target as Node)) {
        node.dispatchEvent(new CustomEvent('click_outside'));
      }
    };
    document.addEventListener('click', handleClick, true);
    return {
      destroy() { document.removeEventListener('click', handleClick, true); }
    };
  }
</script>

<header class="fixed-top p-3 w-100" style="z-index: 1050;">
  <nav class="container glass-card rounded-pill px-4 py-2 d-flex justify-content-between align-items-center shadow-sm" style="max-width: 1100px;">
    
    <div class="d-flex align-items-center gap-2">
      <a href="{base}/" class="d-flex align-items-center gap-2 text-decoration-none">
        <img src="{base}/AxelLab-Logo.ico" alt="Logo" class="nav-logo" />
        <span class="fw-bold fs-5 brand-text">AxelBase</span>
      </a>

      <div class="position-relative ms-3" use:clickOutside on:click_outside={closeDropdown}>
        <button class="btn btn-coffee d-flex align-items-center gap-2" on:click={toggleDropdown}>
          <i class="bi bi-cup-hot-fill"></i>
          <span class="d-none d-md-inline">Support</span>
        </button>

        {#if isDropdownOpen}
          <div class="dropdown-menu-custom glass-card p-2" transition:slide>
            {#each donationAmounts as amount}
              <a href="https://paypal.me/{paypalUsername}/{amount}" target="_blank" class="donation-link" on:click={closeDropdown}>
                ${amount}
              </a>
            {/each}
          </div>
        {/if}
      </div>
    </div>

    <div class="d-flex align-items-center gap-3">
      <ul class="nav d-none d-lg-flex gap-2">
        <li><a class="nav-link-custom" href="{base}/">Home</a></li>
        <li><a class="nav-link-custom" href="{base}/#about">About</a></li>
        <li><a class="nav-link-custom" href="{base}/#how-to">How to use</a></li>
        <li><a class="nav-link-custom" href="{base}/#faq">FAQ</a></li>
        <li><a class="nav-link-custom" href="{base}/wordlist">Wordlist</a></li>
        <li><a class="btn btn-primary btn-sm px-3" href="{base}/blog">Blog</a></li>
      </ul>

      <div class="vr d-none d-lg-block mx-2"></div>

      <button class="btn-theme-toggle" on:click={toggleTheme} aria-label="Toggle Theme">
        <i class="bi {isDark ? 'bi-sun-fill' : 'bi-moon-stars-fill'}"></i>
      </button>
    </div>
  </nav>
</header>

<main style="padding-top: 100px; padding-bottom: 80px;">
  <slot />
</main>

<footer class="releative glass-card border-0 rounded-0 py-3 shadow-lg" style="border-top: 1px solid var(--glass-border) !important;">
  <div class="container d-flex flex-column flex-sm-row justify-content-between align-items-center small text-muted">
    <span class="fw-medium">&copy; {new Date().getFullYear()} AxelBase BIP39 Seed Phrase Validator</span>
    <div class="d-flex gap-4">
      <a href="{base}/privacy" class="footer-link">Privacy</a>
      <a href="{base}/terms" class="footer-link">Terms</a>
    </div>
  </div>
</footer>

<style>
  .nav-logo { height: 35px; transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
  .nav-logo:hover { transform: rotate(15deg) scale(1.2); }
  
  .brand-text { color: var(--color-text-main); font-family: 'Quicksand', sans-serif; }
  
  .nav-link-custom { 
    text-decoration: none; 
    color: var(--color-text-muted); 
    font-weight: 600; 
    padding: 8px 15px;
    transition: color 0.3s;
  }
  .nav-link-custom:hover { color: var(--color-accent); }

  .btn-coffee { background: #ffdd00; color: #4a4532; border: none; font-size: 0.85rem; padding: 6px 15px; }
  .btn-coffee:hover { background: #ffe54c; box-shadow: 0 5px 15px rgba(255, 221, 0, 0.3) !important; }

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
  .btn-theme-toggle:hover { transform: rotate(45deg) scale(1.1); background: var(--color-accent); }

  .dropdown-menu-custom {
    position: absolute;
    top: 120%;
    left: 0;
    min-width: 100px;
    z-index: 1000;
  }

  .donation-link {
    display: block;
    padding: 8px;
    text-align: center;
    text-decoration: none;
    color: var(--color-text-main);
    font-weight: bold;
    border-radius: 12px;
  }
  .donation-link:hover { background: var(--color-accent); color: #4a4532; }

  .footer-link { color: var(--color-text-muted); text-decoration: none; font-weight: 600; }
  .footer-link:hover { color: var(--color-accent); }
</style>