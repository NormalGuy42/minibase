<script lang="ts">
  import { onMount } from 'svelte';
  import DiscordModal from './DiscordModal.svelte';
  
  let scrolled = $state(false);
  let mobileMenuOpen = $state(false);
  let showModal = $state(false);
  
  onMount(() => {
    const handleScroll = () => {
      scrolled = window.scrollY > 20;
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  });
  
  function closeMobileMenu() {
    mobileMenuOpen = false;
  }
</script>

<DiscordModal bind:isOpen={showModal} />

<nav 
  class="fixed top-0 left-0 right-0 z-50 transition-all duration-200 border-b {scrolled ? 'bg-background/90 backdrop-blur-lg border-card-border' : 'bg-transparent border-transparent'}"
>
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex items-center justify-between h-16">
      <a href="/" class="flex items-center gap-2 shrink-0">
        <img src="/minibase-logo-transparent-2.png" alt="Minibase" class="h-3" />
        <span class="text-white text-xl font-bold">minibase</span>
      </a>
      
      <div class="hidden md:flex items-center gap-6">
        <a href="#features" class="text-muted hover:text-white transition-colors text-sm">Features</a>
        <a href="#pricing" class="text-muted hover:text-white transition-colors text-sm">Pricing</a>
        <a href="https://github.com/NormalGuy42/minibase" target="_blank" rel="noopener" class="text-muted hover:text-white transition-colors text-sm">GitHub</a>
      </div>
      
      <div class="hidden md:flex items-center gap-3">
        <button onclick={() => showModal = true} class="btn-primary text-sm py-2 px-4">
          Get Early Access
        </button>
      </div>
      
      <button 
        onclick={() => mobileMenuOpen = !mobileMenuOpen}
        class="md:hidden p-2 text-muted hover:text-white transition-colors"
        aria-label="Toggle menu"
      >
        {#if mobileMenuOpen}
          <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        {:else}
          <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>
        {/if}
      </button>
    </div>
  </div>
  
  {#if mobileMenuOpen}
    <div class="md:hidden bg-background/95 backdrop-blur-lg border-b border-card-border">
      <div class="px-4 py-4 space-y-3">
        <a href="#features" onclick={closeMobileMenu} class="block text-muted hover:text-white transition-colors py-2 text-sm">Features</a>
        <a href="#pricing" onclick={closeMobileMenu} class="block text-muted hover:text-white transition-colors py-2 text-sm">Pricing</a>
        <a href="https://github.com/NormalGuy42/minibase" target="_blank" rel="noopener" class="block text-muted hover:text-white transition-colors py-2 text-sm">GitHub</a>
        <hr class="border-card-border" />
        <button onclick={() => { closeMobileMenu(); showModal = true; }} class="btn-primary text-center block w-full py-2.5 text-sm">
          Get Early Access
        </button>
      </div>
    </div>
  {/if}
</nav>
