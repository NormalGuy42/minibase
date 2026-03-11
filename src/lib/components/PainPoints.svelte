<script lang="ts">
  import { onMount } from 'svelte';
  
  let visible = $state(false);
  let sectionRef: HTMLElement;
  
  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      },
      { threshold: 0.2 }
    );
    observer.observe(sectionRef);
    return () => observer.disconnect();
  });
  
  const painPoints = [
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M10 9v6m4-6v6m7-3a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>`,
      title: "Databases that pause",
      text: "Supabase pauses your database after 7 days of inactivity. Your side project breaks when someone finally visits."
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>`,
      title: "$25 per project",
      text: "One project on Supabase Pro costs $25/month. Five projects? That's $125/month just for backends."
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" /></svg>`,
      title: "Ideas limited by cost",
      text: "You have 10 ideas this month. You shouldn't need to pick which 2 get a real backend."
    }
  ];
</script>

<section bind:this={sectionRef} class="py-24 md:py-32 relative">
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-16"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Built for people who ship</h2>
      <p class="section-subheading mx-auto">
        Most backend platforms punish you for having ideas. We reward it.
      </p>
    </div>
    
    <div class="grid md:grid-cols-3 gap-6">
      {#each painPoints as point, i}
        <div 
          class="card p-6 group hover:border-primary/30 transition-colors"
          class:opacity-0={!visible}
          class:animate-fade-in-up={visible}
          style="animation-delay: {(i + 1) * 100}ms"
        >
          <div class="w-10 h-10 rounded-lg bg-primary/10 flex items-center justify-center text-primary mb-4">
            {@html point.icon}
          </div>
          <h3 class="text-white font-medium mb-2">{point.title}</h3>
          <p class="text-muted text-sm leading-relaxed">
            {point.text}
          </p>
        </div>
      {/each}
    </div>
  </div>
</section>
