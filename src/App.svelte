<script lang="ts">
  import Achievements from './lib/Achievements.svelte';
  import CallToAction from './lib/CallToAction.svelte';
  import Expertise from './lib/Expertise.svelte';
  import Footer from './lib/Footer.svelte';
  import Hero from './lib/Hero.svelte';
  import Navigation from './lib/Navigation.svelte';
  import Projects from './lib/Projects.svelte';
  import TechStack from './lib/TechStack.svelte';
</script>

<svelte:head>
  <!-- Dark mode initialization script - runs before page renders -->
  <script>
    (function() {
      const savedMode = localStorage.getItem('darkMode');
      const darkMode = savedMode !== null ? savedMode === 'true' : true; // Default to dark
      if (darkMode) {
        document.documentElement.classList.add('dark');
      } else {
        document.documentElement.classList.remove('dark');
      }
    })();
  </script>
  
  <title>Samarth Patel - Software Engineer | Portfolio</title>
  <meta name="description" content="Samarth Patel - Software Engineer specializing in full-stack development, cloud architecture, and modern web technologies. Building scalable applications with React, SvelteKit, Node.js, and more." />
  <meta name="keywords" content="software engineer, full-stack developer, web development, React, Svelte, Node.js, TypeScript, cloud architecture" />
  <meta name="author" content="Samarth Patel" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  
  <!-- Open Graph / Facebook -->
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://yourdomain.com/" />
  <meta property="og:title" content="Samarth Patel - Software Engineer" />
  <meta property="og:description" content="Software Engineer specializing in full-stack development and cloud architecture" />
  
  <!-- Twitter -->
  <meta property="twitter:card" content="summary_large_image" />
  <meta property="twitter:url" content="https://yourdomain.com/" />
  <meta property="twitter:title" content="Samarth Patel - Software Engineer" />
  <meta property="twitter:description" content="Software Engineer specializing in full-stack development and cloud architecture" />
</svelte:head>

<Navigation />

<main class="overflow-x-hidden">
  <Hero />
  <Expertise />
  <Projects />
  <TechStack />
  <Achievements />
  <CallToAction />
</main>

<Footer />

<!-- Skip to main content link for accessibility -->
<a href="#hero" class="sr-only focus:not-sr-only focus:absolute focus:top-4 focus:left-4 bg-primary-600 text-white px-4 py-2 rounded-lg z-50">
  Skip to main content
</a>

<style>
  :global(.sr-only) {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
  }
  
  :global(.focus\:not-sr-only:focus) {
    position: static;
    width: auto;
    height: auto;
    padding: 0.5rem 1rem;
    margin: 0;
    overflow: visible;
    clip: auto;
    white-space: normal;
  }
</style>
