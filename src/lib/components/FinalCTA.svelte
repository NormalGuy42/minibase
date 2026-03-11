<script lang="ts">
  import { onMount } from 'svelte';
  import DiscordModal from './DiscordModal.svelte';
  
  let visible = $state(false);
  let sectionRef: HTMLElement;
  let showModal = $state(false);
  
  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      },
      { threshold: 0.3 }
    );
    observer.observe(sectionRef);
    return () => observer.disconnect();
  });
</script>

<DiscordModal bind:isOpen={showModal} />

<section bind:this={sectionRef} class="py-24 md:py-32 relative">
  <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-primary/5 via-transparent to-transparent"></div>
  
  <div class="relative max-w-2xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
    <div
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="text-3xl md:text-4xl font-semibold text-white mb-4 tracking-tight">
        Stop paying per project.
      </h2>
      
      <p class="text-muted mb-8 max-w-md mx-auto">
        Join the waitlist and be first to try Minibase when we launch.
      </p>
      
      <button onclick={() => showModal = true} class="btn-primary text-base px-8 py-3.5">
        Get Early Access
      </button>
      
      <p class="text-xs text-muted/50 mt-4">
        No spam · Shape the product · Free early access
      </p>
    </div>
  </div>
</section>
