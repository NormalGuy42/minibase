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
  
  const steps = [
    {
      number: '01',
      title: 'Create a project',
      description: 'Sign up, click "New Project", your database is live in seconds.'
    },
    {
      number: '02',
      title: 'Install the SDK',
      description: 'npm install minibase-js and connect with one line of code.'
    },
    {
      number: '03',
      title: 'Ship your product',
      description: 'Query data, auth users, upload files. Focus on your product.'
    }
  ];
</script>

<section bind:this={sectionRef} class="py-24 md:py-32 relative">
  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
    <div 
      class="text-center mb-16"
      class:opacity-0={!visible}
      class:animate-fade-in-up={visible}
    >
      <h2 class="section-heading mb-4">Up and running in minutes</h2>
      <p class="section-subheading mx-auto">
        Three steps from sign-up to shipping.
      </p>
    </div>
    
    <div class="grid md:grid-cols-3 gap-8">
      {#each steps as step, i}
        <div 
          class="text-center"
          class:opacity-0={!visible}
          class:animate-fade-in-up={visible}
          style="animation-delay: {(i + 1) * 100}ms"
        >
          <div class="text-4xl font-semibold text-primary/60 mb-4">{step.number}</div>
          <h3 class="text-lg font-medium text-white mb-2">{step.title}</h3>
          <p class="text-muted text-sm leading-relaxed">{step.description}</p>
        </div>
      {/each}
    </div>
  </div>
</section>
