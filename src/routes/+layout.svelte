<script lang="ts">
  import '../app.css';
  
  let { children } = $props();
</script>

<svelte:head>
  <meta name="robots" content="index, follow" />
</svelte:head>

{@render children()}
