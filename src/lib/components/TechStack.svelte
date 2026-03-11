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
  
  const technologies = [
    { name: 'PostgreSQL', role: 'Database', icon: '/icons/postgresql-transparent.png' },
    { name: 'PostgREST', role: 'REST API', icon: '/icons/postgrest-transparent.png' },
    { name: 'Tigris', role: 'Storage', icon: '/icons/tigris-transparent.png' },
    { name: 'Fly.io', role: 'Compute', icon: '/icons/flyio-transparent.png' },
    { name: 'Cloudflare', role: 'Edge', icon: '/icons/cloudflare-transparent.png' }
  ];
</script>

<section bind:this={sectionRef} class="py-16 border-t border-card-border">
  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-10"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <p class="text-sm text-muted">
        Built with open-source tools you trust
      </p>
    </div>
    
    <div 
      class="flex flex-wrap items-center justify-center gap-10 md:gap-14"
      class:opacity-0={!visible}
      class:animate-fade-in={visible}
      class:animate-delay-200={visible}
    >
      {#each technologies as tech}
        <div class="flex flex-col items-center gap-3 group">
          <div class="w-12 h-12 rounded-lg bg-white/5 border border-card-border flex items-center justify-center group-hover:border-primary/30 transition-colors">
            <!-- Placeholder icon - replace with actual icon -->
            <img 
              src={tech.icon} 
              alt={tech.name} 
              class="h-7 opacity-60 group-hover:opacity-100 transition-opacity"
            />
          </div>
          <div class="text-center">
            <div class="text-sm font-medium text-white/70 group-hover:text-white transition-colors">{tech.name}</div>
            <div class="text-xs text-muted">{tech.role}</div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
