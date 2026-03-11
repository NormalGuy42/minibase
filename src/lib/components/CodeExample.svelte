<script lang="ts">
  import { onMount } from 'svelte';
  
  let visible = $state(false);
  let sectionRef: HTMLElement;
  let activeTab = $state('database');
  
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
  
  const tabs = [
    { id: 'database', label: 'Database' },
    { id: 'auth', label: 'Auth' },
    { id: 'storage', label: 'Storage' }
  ];
  
  const codeExamples: Record<string, { code: string; description: string }> = {
    database: {
      code: `import { createClient } from 'minibase-js'

const mb = createClient(PROJECT_URL, API_KEY)

// Fetch all active products
const { data: products } = await mb
  .from('products')
  .select('id, name, price')
  .eq('status', 'active')
  .order('created_at', { ascending: false })

// Insert a new product
const { data: newProduct } = await mb
  .from('products')
  .insert({ name: 'Widget Pro', price: 29 })
  .select()
  .single()`,
      description: "Query your Postgres database with a clean, chainable API. Filter, sort, and paginate with type-safe methods."
    },
    auth: {
      code: `import { createClient } from 'minibase-js'

const mb = createClient(PROJECT_URL, API_KEY)

// Sign up a new user
const { user, error } = await mb.auth.signUp({
  email: 'you@startup.io',
  password: 'secure-password'
})

// Sign in with OAuth
await mb.auth.signInWithOAuth({
  provider: 'github',
  redirectTo: 'https://myapp.com/callback'
})`,
      description: "Add authentication in minutes. Email/password, magic links, and OAuth providers like Google and GitHub."
    },
    storage: {
      code: `import { createClient } from 'minibase-js'

const mb = createClient(PROJECT_URL, API_KEY)

// Upload a file
const { data } = await mb.storage
  .from('avatars')
  .upload('users/123/avatar.png', file)

// Get a public URL
const { publicUrl } = mb.storage
  .from('avatars')
  .getPublicUrl('users/123/avatar.png')`,
      description: "Upload and serve files with S3-compatible storage. Generate signed URLs for secure, time-limited access."
    }
  };
  
  function highlightCode(code: string): string {
    return code
      .replace(/\b(import|from|const|await|async)\b/g, '<span class="text-purple-400">$&</span>')
      .replace(/'[^']*'/g, '<span class="text-green-400">$&</span>')
      .replace(/\/\/.*/g, '<span class="text-muted/50">$&</span>')
      .replace(/\.(from|select|eq|order|insert|single|auth|signUp|signInWithOAuth|storage|upload|getPublicUrl)\b/g, '.<span class="text-blue-400">$1</span>')
      .replace(/\b(data|error|user|publicUrl|products|newProduct|mb)\b/g, '<span class="text-orange-300">$1</span>')
      .replace(/\b(PROJECT_URL|API_KEY)\b/g, '<span class="text-cyan-400">$1</span>');
  }
</script>

<section bind:this={sectionRef} class="py-24 md:py-32 relative">
  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-12"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Simple, powerful SDK</h2>
      <p class="section-subheading mx-auto">
        One client library for everything. Type-safe and intuitive.
      </p>
    </div>
    
    <div 
      class="card overflow-hidden"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
      class:animate-delay-200={visible}
    >
      <div class="flex border-b border-card-border">
        {#each tabs as tab}
          <button
            onclick={() => activeTab = tab.id}
            class="px-5 py-3 text-sm transition-colors relative {activeTab === tab.id ? 'text-white' : 'text-muted hover:text-white'}"
          >
            {tab.label}
            {#if activeTab === tab.id}
              <div class="absolute bottom-0 left-0 right-0 h-px bg-primary"></div>
            {/if}
          </button>
        {/each}
      </div>
      
      <div class="p-5 overflow-x-auto">
        <pre class="font-mono text-sm leading-relaxed"><code>{@html highlightCode(codeExamples[activeTab].code)}</code></pre>
      </div>
      
      <div class="px-5 pb-5">
        <p class="text-sm text-muted">
          {codeExamples[activeTab].description}
        </p>
      </div>
    </div>
  </div>
</section>
