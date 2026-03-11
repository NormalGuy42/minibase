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
      { threshold: 0.2 }
    );
    observer.observe(sectionRef);
    return () => observer.disconnect();
  });
  
  const comparisonData = [
    { 
      feature: 'Monthly cost (5 projects)', 
      minibase: '$12', 
      supabaseFree: '$0*', 
      supabasePro: '$125',
      note: '*Pauses after 7 days'
    },
    { 
      feature: 'Projects included', 
      minibase: '25', 
      supabaseFree: '2', 
      supabasePro: '1 per $25'
    },
    { 
      feature: 'Database pausing', 
      minibase: 'Never', 
      supabaseFree: 'After 7 days', 
      supabasePro: 'Never'
    },
    { 
      feature: 'Cold starts', 
      minibase: 'None', 
      supabaseFree: 'Yes', 
      supabasePro: 'None'
    },
    { 
      feature: 'Storage per project', 
      minibase: '5GB', 
      supabaseFree: '1GB total', 
      supabasePro: '100GB total'
    },
    { 
      feature: 'REST API', 
      minibase: 'Included', 
      supabaseFree: 'Included', 
      supabasePro: 'Included'
    },
    { 
      feature: 'Auth', 
      minibase: 'Included', 
      supabaseFree: 'Included', 
      supabasePro: 'Included'
    }
  ];
</script>

<DiscordModal bind:isOpen={showModal} />

<section bind:this={sectionRef} class="py-24 md:py-32 relative">
  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-12"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Minibase vs Supabase</h2>
      <p class="section-subheading mx-auto">
        For builders who ship multiple products, the math is simple.
      </p>
    </div>
    
    <div 
      class="card overflow-hidden"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
      class:animate-delay-200={visible}
    >
      <div class="overflow-x-auto">
        <table class="w-full">
          <thead>
            <tr class="border-b border-card-border">
              <th class="text-left p-4 text-sm font-medium text-muted w-1/3"></th>
              <th class="p-4 text-center bg-primary/10 border-x border-primary/20">
                <span class="text-primary font-semibold">Minibase</span>
                <span class="block text-xs text-muted mt-0.5">Indie Plan</span>
              </th>
              <th class="p-4 text-center bg-white/[0.02]">
                <span class="text-white/80 font-medium">Supabase</span>
                <span class="block text-xs text-muted mt-0.5">Free</span>
              </th>
              <th class="p-4 text-center bg-white/[0.02]">
                <span class="text-white/80 font-medium">Supabase</span>
                <span class="block text-xs text-muted mt-0.5">Pro</span>
              </th>
            </tr>
          </thead>
          <tbody>
            {#each comparisonData as row, i}
              <tr class="border-b border-card-border last:border-0">
                <td class="p-4 text-sm text-white/70">{row.feature}</td>
                <td class="p-4 text-center bg-primary/10 border-x border-primary/20">
                  <span class="text-sm font-medium text-white">
                    {row.minibase}
                  </span>
                </td>
                <td class="p-4 text-center text-sm text-white/70 bg-white/[0.02]">
                  {row.supabaseFree}
                  {#if row.note}
                    <span class="block text-xs text-muted mt-0.5">{row.note}</span>
                  {/if}
                </td>
                <td class="p-4 text-center text-sm text-white/70 bg-white/[0.02]">{row.supabasePro}</td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>
    
    <div 
      class="text-center mt-10"
      class:opacity-0={!visible}
      class:animate-fade-in={visible}
      class:animate-delay-400={visible}
    >
      <button onclick={() => showModal = true} class="btn-primary">
        Join the Waitlist
      </button>
    </div>
  </div>
</section>
