<script lang="ts">
  import { onMount } from 'svelte';
  import DiscordModal from './DiscordModal.svelte';
  
  let visible = $state(false);
  let showModal = $state(false);
  
  onMount(() => {
    visible = true;
  });
  
  const codeExample = `import { createClient } from 'minibase-js'

const mb = createClient('your-project-url', 'your-api-key')

// Query your database
const { data, error } = await mb
  .from('products')
  .select('*')
  .eq('status', 'active')

// Authenticate users
const { user } = await mb.auth.signIn({
  email: 'you@startup.io',
  password: '••••••••'
})

// Upload files
const { url } = await mb.storage
  .upload('assets/logo.png', file)`;
</script>

<DiscordModal bind:isOpen={showModal} />

<section class="relative min-h-screen pt-40 md:pt-48 pb-20 overflow-hidden">
  <div class="absolute inset-0 bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))] from-primary/5 via-transparent to-transparent"></div>
  
  <div class="relative max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center max-w-3xl mx-auto">
      <h1 
        class="text-4xl sm:text-5xl md:text-6xl font-semibold tracking-tight leading-[1.1] mb-6"
        class:opacity-0={!visible}
        class:animate-fade-in-up={visible}
      >
        <span class="text-primary">Ship every idea.</span>
        <span class="">Not just the ones you can afford.</span>
      </h1>
      
      <p 
        class="text-lg text-muted max-w-xl mx-auto mb-10 leading-relaxed"
        class:opacity-0={!visible}
        class:animate-fade-in-up={visible}
        class:animate-delay-100={visible}
      >
        Postgres databases, REST APIs, auth, and file storage for all your projects. One subscription. No database pausing.
      </p>
      
      <div 
        class="flex flex-col sm:flex-row gap-4 justify-center mb-8"
        class:opacity-0={!visible}
        class:animate-fade-in-up={visible}
        class:animate-delay-200={visible}
      >
        <button onclick={() => showModal = true} class="btn-primary text-base px-8 py-4">
          Get Early Access
        </button>
        <a href="https://github.com/NormalGuy42/minibase" target="_blank" rel="noopener" class="btn-secondary text-base px-8 py-4">
          View on GitHub
        </a>
      </div>
      
      <p 
        class="text-sm text-muted/60 mb-20"
        class:opacity-0={!visible}
        class:animate-fade-in={visible}
        class:animate-delay-300={visible}
      >
        Currently in development · Join the Discord for updates
      </p>
    </div>
    
    <div 
      class="max-w-2xl mx-auto"
      class:opacity-0={!visible}
      class:animate-slide-up={visible}
      class:animate-delay-400={visible}
    >
      <div class="relative">
        <!-- Glow effect behind code block -->
        <div class="absolute -inset-4 bg-primary/20 rounded-3xl blur-2xl"></div>
        
        <div class="relative card overflow-hidden">
        <div class="flex items-center gap-2 px-4 py-3 border-b border-card-border">
          <div class="flex gap-1.5">
            <div class="w-2.5 h-2.5 rounded-full bg-[#333]"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-[#333]"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-[#333]"></div>
          </div>
          <span class="text-xs text-muted/60 ml-2 font-mono">app.ts</span>
        </div>
        
        <div class="p-5 overflow-x-auto">
          <pre class="font-mono text-sm leading-relaxed"><code class="text-muted">{@html highlightCode(codeExample)}</code></pre>
        </div>
        </div>
      </div>
    </div>
  </div>
</section>

<script context="module" lang="ts">
  function highlightCode(code: string): string {
    return code
      .replace(/import|from|const|await|async/g, '<span class="text-purple-400">$&</span>')
      .replace(/'[^']*'/g, '<span class="text-green-400">$&</span>')
      .replace(/\/\/.*/g, '<span class="text-muted/50">$&</span>')
      .replace(/\.(from|select|eq|auth|signIn|storage|upload|createClient)\b/g, '.<span class="text-blue-400">$1</span>')
      .replace(/\b(data|error|user|url|mb)\b/g, '<span class="text-orange-300">$1</span>')
      .replace(/[{}[\]()]/g, '<span class="text-muted/70">$&</span>');
  }
</script>
