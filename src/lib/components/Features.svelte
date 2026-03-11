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
      { threshold: 0.1 }
    );
    observer.observe(sectionRef);
    return () => observer.disconnect();
  });
  
  const features = [
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4m0 5c0 2.21-3.582 4-8 4s-8-1.79-8-4" /></svg>`,
      title: "Postgres Database",
      description: "Full Postgres on shared clusters. Always on, zero cold starts, no pausing. The world's most trusted database.",
      visual: "database"
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>`,
      title: "Instant REST API",
      description: "Your schema becomes a RESTful API via PostgREST. CRUD, filtering, pagination — zero config required.",
      visual: "api"
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" /></svg>`,
      title: "Authentication",
      description: "Email/password and OAuth out of the box. Scoped per project, managed from one dashboard.",
      visual: "auth"
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12" /></svg>`,
      title: "File Storage",
      description: "S3-compatible storage powered by Tigris. Scoped per project with pre-signed URLs.",
      visual: "storage"
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" /></svg>`,
      title: "TypeScript SDK",
      description: "Type-safe client for auth, CRUD, and file uploads. Install and start building in 30 seconds.",
      visual: "sdk"
    },
    {
      icon: `<svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z" /></svg>`,
      title: "AI-Native",
      description: "Connect Cursor or Windsurf via MCP. Your AI agent can provision databases directly from your IDE.",
      visual: "ai"
    }
  ];
</script>

<section bind:this={sectionRef} id="features" class="py-24 md:py-32 relative">
  <div class="max-w-5xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-16"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Everything you need</h2>
      <p class="section-subheading mx-auto">
        A complete backend stack that grows with your portfolio.
      </p>
    </div>
    
    <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-5">
      {#each features as feature, i}
        <div 
          class="card group p-6 hover:border-primary/30 transition-colors"
          class:opacity-0={!visible}
          class:animate-fade-in-up={visible}
          style="animation-delay: {(i + 1) * 60}ms"
        >
          <div class="w-11 h-11 rounded-lg bg-primary/10 flex items-center justify-center text-primary mb-4">
            {@html feature.icon}
          </div>
          
          <h3 class="text-lg font-medium text-white mb-2">{feature.title}</h3>
          <p class="text-muted text-sm leading-relaxed mb-5">{feature.description}</p>
          
          <div class="mt-auto">
            {#if feature.visual === 'database'}
              <div class="bg-background rounded-lg border border-card-border p-3 text-xs font-mono">
                <div class="flex items-center gap-2 text-muted mb-2">
                  <span class="text-primary">TABLE</span> products
                </div>
                <div class="space-y-1 text-muted/60">
                  <div class="flex gap-4"><span class="text-blue-400">id</span><span>uuid</span></div>
                  <div class="flex gap-4"><span class="text-blue-400">name</span><span>text</span></div>
                  <div class="flex gap-4"><span class="text-blue-400">price</span><span>int4</span></div>
                </div>
              </div>
            {:else if feature.visual === 'api'}
              <div class="bg-background rounded-lg border border-card-border p-3 text-xs font-mono">
                <div class="text-primary">GET</div>
                <div class="text-muted/60 break-all">/rest/v1/products?status=eq.active</div>
              </div>
            {:else if feature.visual === 'auth'}
              <div class="bg-background rounded-lg border border-card-border p-3 space-y-2">
                <div class="h-6 bg-card-border rounded flex items-center px-2 text-xs text-muted/60">user@example.com</div>
                <div class="h-6 bg-card-border rounded flex items-center px-2 text-xs text-muted/60">••••••••</div>
                <div class="h-6 bg-primary rounded flex items-center justify-center text-xs text-white font-medium">Sign In</div>
              </div>
            {:else if feature.visual === 'storage'}
              <div class="bg-background rounded-lg border border-card-border p-3 text-xs">
                <div class="flex items-center gap-2 text-muted mb-2">
                  <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z" /></svg>
                  <span>uploads/</span>
                </div>
                <div class="pl-6 space-y-1 text-muted/60">
                  <div>avatar.png</div>
                  <div>logo.svg</div>
                </div>
              </div>
            {:else if feature.visual === 'sdk'}
              <div class="bg-background rounded-lg border border-card-border p-3 font-mono text-xs">
                <span class="text-muted/60">$</span> <span class="text-primary">npm install minibase-js</span>
              </div>
            {:else if feature.visual === 'ai'}
              <div class="bg-background rounded-lg border border-card-border p-3 text-xs">
                <div class="flex items-center gap-2 text-primary mb-1">
                  <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 9l3 3-3 3m5 0h3M5 20h14a2 2 0 002-2V6a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" /></svg>
                  MCP Server
                </div>
                <div class="text-muted/60">"Create a users table with email"</div>
              </div>
            {/if}
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>
