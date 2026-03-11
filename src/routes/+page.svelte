<script lang="ts">
  import Navbar from '$lib/components/Navbar.svelte';
  import Hero from '$lib/components/Hero.svelte';
  import PainPoints from '$lib/components/PainPoints.svelte';
  import Features from '$lib/components/Features.svelte';
  import CodeExample from '$lib/components/CodeExample.svelte';
  import Pricing from '$lib/components/Pricing.svelte';
  import Comparison from '$lib/components/Comparison.svelte';
  import HowItWorks from '$lib/components/HowItWorks.svelte';
  import TechStack from '$lib/components/TechStack.svelte';
  import FinalCTA from '$lib/components/FinalCTA.svelte';
  import Footer from '$lib/components/Footer.svelte';
</script>

<svelte:head>
  <title>Minibase — Ship ten products. Pay for one backend.</title>
  <meta name="description" content="Minibase gives you Postgres databases, auto-generated REST APIs, auth, and file storage for all your projects. The Supabase alternative for indie hackers who ship a lot. Starting at $0/month." />
</svelte:head>

<div class="min-h-screen bg-background">
  <Navbar />
  
  <main>
    <Hero />
    <PainPoints />
    <Features />
    <CodeExample />
    <Pricing />
    <Comparison />
    <HowItWorks />
    <TechStack />
    <FinalCTA />
  </main>
  
  <Footer />
</div>
