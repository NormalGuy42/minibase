<script lang="ts">
  import { onMount } from 'svelte';
  import DiscordModal from './DiscordModal.svelte';
  
  let visible = $state(false);
  let sectionRef: HTMLElement;
  let annual = $state(false);
  let showModal = $state(false);
  
  onMount(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          visible = true;
          observer.disconnect();
        }
      },
      { threshold: 0.1 }
    );
    observer.observe(sectionRef);
    return () => observer.disconnect();
  });
  
  const plans = [
    {
      name: 'Free',
      price: 0,
      annualPrice: 0,
      description: 'Try it out',
      features: [
        '1 project',
        'Postgres (always on)',
        'REST API',
        'Auth',
        '500MB storage'
      ],
      cta: 'Get Started',
      highlighted: false
    },
    {
      name: 'Hobby',
      price: 5,
      annualPrice: 4,
      description: 'Side projects',
      features: [
        '5 projects',
        'Everything in Free',
        '1GB storage / project',
        '500MB database / project'
      ],
      cta: 'Get Started',
      highlighted: false
    },
    {
      name: 'Indie',
      price: 12,
      annualPrice: 10,
      description: 'Prolific builders',
      features: [
        '25 projects',
        'Everything in Hobby',
        '5GB storage / project',
        '1GB database / project',
        'MCP server access'
      ],
      cta: 'Get Started',
      highlighted: true
    },
    {
      name: 'Pro',
      price: 29,
      annualPrice: 21,
      description: 'Teams & agencies',
      features: [
        '100 projects',
        'Everything in Indie',
        '10GB storage / project',
        '5GB database / project',
        'Priority support'
      ],
      cta: 'Get Started',
      highlighted: false
    }
  ];
</script>

<DiscordModal bind:isOpen={showModal} />

<section bind:this={sectionRef} id="pricing" class="py-24 md:py-32 relative">
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-12"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Simple, flat pricing</h2>
      <p class="section-subheading mx-auto">
        No per-project fees. Ship more, pay less.
      </p>
      
      <div class="flex items-center justify-center gap-3 mt-8">
        <span class="text-sm {!annual ? 'text-white' : 'text-muted'}">Monthly</span>
        <button 
          onclick={() => annual = !annual}
          class="relative w-12 h-6 rounded-full transition-colors {annual ? 'bg-primary' : 'bg-card-border'}"
          role="switch"
          aria-checked={annual}
        >
          <span class="absolute top-1 left-1 w-4 h-4 bg-white rounded-full transition-transform {annual ? 'translate-x-6' : ''}"></span>
        </button>
        <span class="text-sm {annual ? 'text-white' : 'text-muted'}">
          Annual <span class="text-primary text-xs ml-1">-20%</span>
        </span>
      </div>
    </div>
    
    <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-5">
      {#each plans as plan, i}
        <div 
          class="card p-5 flex flex-col relative {plan.highlighted ? 'border-primary/50' : ''}"
          class:opacity-0={!visible}
          class:animate-fade-in-up={visible}
          style="animation-delay: {(i + 1) * 80}ms"
        >
          {#if plan.highlighted}
            <div class="absolute -top-2.5 left-1/2 -translate-x-1/2 px-2.5 py-0.5 bg-primary text-xs font-medium rounded-full">
              Recommended
            </div>
          {/if}
          
          <div class="mb-5">
            <h3 class="text-base font-medium text-white mb-0.5">{plan.name}</h3>
            <p class="text-xs text-muted">{plan.description}</p>
          </div>
          
          <div class="mb-5">
            <div class="flex items-baseline gap-0.5">
              <span class="text-3xl font-semibold text-white">${annual ? plan.annualPrice : plan.price}</span>
              <span class="text-muted text-sm">/mo</span>
            </div>
          </div>
          
          <ul class="space-y-2.5 mb-6 flex-grow">
            {#each plan.features as feature}
              <li class="flex items-start gap-2 text-sm text-muted">
                <svg class="h-4 w-4 text-primary shrink-0 mt-0.5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd" />
                </svg>
                {feature}
              </li>
            {/each}
          </ul>
          
          <button 
            onclick={() => showModal = true}
            class="{plan.highlighted ? 'btn-primary' : 'btn-secondary'} text-center w-full text-sm py-2.5"
          >
            {plan.cta}
          </button>
        </div>
      {/each}
    </div>
    
    <p 
      class="text-center text-xs text-muted/60 mt-8"
      class:opacity-0={!visible}
      class:animate-fade-in={visible}
      class:animate-delay-500={visible}
    >
      All plans: No database pausing · Auto REST API · OAuth · File storage
    </p>
  </div>
</section>
