<script lang="ts">
  import '../app.css';
  import { siteConfig, links } from '../constants';
  
  let { children } = $props();
</script>

<svelte:head>
  <!-- Primary Meta Tags -->
  <title>{siteConfig.title}</title>
  <meta name="title" content={siteConfig.title} />
  <meta name="description" content={siteConfig.description} />
  <meta name="keywords" content={siteConfig.keywords} />
  <meta name="author" content={siteConfig.name} />
  <meta name="robots" content="index, follow" />
  
  <!-- Open Graph / Facebook -->
  <meta property="og:type" content="website" />
  <meta property="og:locale" content="en_US" />
  <meta property="og:url" content={siteConfig.url} />
  <meta property="og:site_name" content={siteConfig.name} />
  <meta property="og:title" content={siteConfig.title} />
  <meta property="og:description" content={siteConfig.description} />
  <meta property="og:image" content={siteConfig.ogImage} />
  <meta property="og:image:secure_url" content={siteConfig.ogImage} />
  <meta property="og:image:type" content="image/png" />
  <meta property="og:image:width" content="1200" />
  <meta property="og:image:height" content="630" />
  <meta property="og:image:alt" content={siteConfig.title} />
  
  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:site" content={links.twitterMinibaseHandle} />
  <meta name="twitter:creator" content={links.twitterHandle} />
  <meta name="twitter:title" content={siteConfig.title} />
  <meta name="twitter:description" content={siteConfig.description} />
  <meta name="twitter:image" content={siteConfig.ogImage} />
  <meta name="twitter:image:alt" content={siteConfig.title} />
  
  <!-- Canonical -->
  <link rel="canonical" href={siteConfig.url} />
  
  <!-- Structured Data -->
  {@html `<script type="application/ld+json">${JSON.stringify({
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": siteConfig.name,
    "applicationCategory": "DeveloperApplication",
    "operatingSystem": "Web",
    "description": siteConfig.description,
    "url": siteConfig.url,
    "image": siteConfig.ogImage,
    "offers": {
      "@type": "Offer",
      "price": "0",
      "priceCurrency": "USD"
    },
    "creator": {
      "@type": "Organization",
      "name": siteConfig.name,
      "url": siteConfig.url
    }
  })}</script>`}
</svelte:head>

{@render children()}
