<script lang="ts">
  import { onMount } from 'svelte';
  
  let mounted = false;
  let isMenuOpen = false;
  let scrollY = 0;
  let darkMode = false;
  
  const navItems = [
    { label: 'Home', href: '#hero' },
    { label: 'Expertise', href: '#expertise' },
    { label: 'Projects', href: '#projects' },
    { label: 'Tech Stack', href: '#tech-stack' },
    { label: 'Contact', href: '#cta' }
  ];
  
  onMount(() => {
    mounted = true;
    
    // Check for dark mode preference - default to light mode
    darkMode = localStorage.getItem('darkMode') === 'true';
    
    updateDarkMode();
    
    // Listen for scroll events
    const handleScroll = () => scrollY = window.scrollY;
    window.addEventListener('scroll', handleScroll);
    
    return () => window.removeEventListener('scroll', handleScroll);
  });
  
  const toggleDarkMode = () => {
    darkMode = !darkMode;
    localStorage.setItem('darkMode', darkMode.toString());
    updateDarkMode();
  };
  
  const updateDarkMode = () => {
    if (darkMode) {
      document.documentElement.classList.add('dark');
    } else {
      document.documentElement.classList.remove('dark');
    }
  };
  
  const scrollToSection = (href: string) => {
    const element = document.querySelector(href);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
      isMenuOpen = false;
    }
  };
  
  const handleKeydown = (event: KeyboardEvent, href: string) => {
    if (event.key === 'Enter' || event.key === ' ') {
      event.preventDefault();
      scrollToSection(href);
    }
  };
</script>

<svelte:window bind:scrollY />

<nav class={`fixed top-0 w-full z-50 transition-all duration-300 ${scrollY > 50 ? 'bg-white/95 dark:bg-gray-900/95 backdrop-blur-md shadow-lg' : 'bg-transparent'}`}>
  <div class="container-custom">
    <div class="flex items-center justify-between py-4">
      <!-- Logo -->
      <button 
        on:click={() => scrollToSection('#hero')}
        class="flex items-center hover:opacity-80 transition-opacity"
        aria-label="Go to home section"
      >
        <img src="/Logo1.png" alt="Samarth Patel Logo" class="w-10 h-10" />
      </button>
      
      <!-- Desktop Navigation -->
      <div class="hidden md:flex items-center space-x-8">
        {#each navItems as item}
          <button
            on:click={() => scrollToSection(item.href)}
            on:keydown={(e) => handleKeydown(e, item.href)}
            class="text-gray-700 dark:text-gray-300 hover:text-primary-600 dark:hover:text-primary-400 font-medium transition-colors focus:outline-none focus:ring-2 focus:ring-primary-500 rounded px-2 py-1"
            tabindex="0"
          >
            {item.label}
          </button>
        {/each}
        
        <!-- Dark Mode Toggle -->
        <button
          on:click={toggleDarkMode}
          class="p-2 rounded-lg bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-400 hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors focus:outline-none focus:ring-2 focus:ring-primary-500"
          aria-label={darkMode ? 'Switch to light mode' : 'Switch to dark mode'}
        >
          {#if darkMode}
            <!-- Sun Icon -->
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
          {:else}
            <!-- Moon Icon -->
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
            </svg>
          {/if}
        </button>
      </div>
      
      <!-- Mobile Menu Button -->
      <div class="md:hidden flex items-center space-x-4">
        <!-- Dark Mode Toggle for Mobile -->
        <button
          on:click={toggleDarkMode}
          class="p-2 rounded-lg bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-400 hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors"
          aria-label={darkMode ? 'Switch to light mode' : 'Switch to dark mode'}
        >
          {#if darkMode}
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
          {:else}
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
            </svg>
          {/if}
        </button>
        
        <!-- Hamburger Menu -->
        <button
          on:click={() => isMenuOpen = !isMenuOpen}
          class="p-2 rounded-lg bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-400 hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors"
          aria-label="Toggle navigation menu"
          aria-expanded={isMenuOpen}
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            {#if isMenuOpen}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            {:else}
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            {/if}
          </svg>
        </button>
      </div>
    </div>
    
    <!-- Mobile Menu -->
    {#if isMenuOpen}
      <div class="md:hidden bg-white dark:bg-gray-900 border-t border-gray-200 dark:border-gray-700">
        <div class="py-4 space-y-2">
          {#each navItems as item}
            <button
              on:click={() => scrollToSection(item.href)}
              class="block w-full text-left px-4 py-3 text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-primary-600 dark:hover:text-primary-400 transition-colors"
            >
              {item.label}
            </button>
          {/each}
        </div>
      </div>
    {/if}
  </div>
</nav>
