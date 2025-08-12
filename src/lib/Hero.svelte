<script lang="ts">
  import { onMount } from 'svelte';
  
  let mounted = false;
  let currentRole = "Web Developer";
  let roleIndex = 0;
  
  const roles = [
    "Web Developer",
    "App Developer", 
    "DevOps Engineer"
  ];
  
  onMount(() => {
    mounted = true;
    
    // Start the auto-changing text
    const interval = setInterval(() => {
      roleIndex = (roleIndex + 1) % roles.length;
      currentRole = roles[roleIndex];
    }, 4000); // Change every 4 seconds
    
    // Cleanup interval on component destroy
    return () => clearInterval(interval);
  });
  
  const scrollToSection = (sectionId: string) => {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  };
</script>

<section id="hero" class="min-h-screen flex items-center justify-center bg-gradient-to-br from-gray-50 via-white to-blue-50 dark:from-gray-900 dark:via-gray-800 dark:to-gray-900">
  <div class="container-custom text-center">
    <div class={`transition-all duration-1000 ${mounted ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <!-- Profile Image -->
      <div class="mb-8">
        <div class="w-32 h-32 mx-auto rounded-full bg-gradient-to-r from-primary-500 to-purple-500 p-1">
          <div class="w-full h-full rounded-full overflow-hidden">
            <img 
              src="/profile.jpg" 
              alt="Samarth Patel"
              class="w-full h-full object-cover"
              loading="eager"
            />
          </div>
        </div>
      </div>
      
      <!-- Main Heading -->
      <h1 class="text-5xl md:text-7xl font-bold mb-6 leading-tight">
        Hi, I'm <span class="text-gradient">Samarth Patel</span>
      </h1>
      
    <!-- Subtitle with auto-changing text -->
    <h2 class="text-2xl md:text-3xl font-medium text-gray-600 dark:text-gray-300 mb-8">
      <span class="transition-opacity duration-500">{currentRole}</span>
    </h2>
      
      <!-- Description -->
      <p class="text-lg md:text-xl text-gray-600 dark:text-gray-400 mb-12 max-w-3xl mx-auto leading-relaxed">
        I craft digital experiences that bridge the gap between design and functionality. 
        Passionate about building scalable applications and solving complex problems with clean, efficient code.
      </p>
      
      <!-- CTA Buttons -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center items-center">
        <button 
          on:click={() => scrollToSection('expertise')}
          class="btn-primary group"
          aria-label="View my work and expertise"
        >
          View My Work
          <svg class="ml-2 w-5 h-5 transition-transform group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
          </svg>
        </button>
        
        <a 
          href="/Samarth_Patel_Resume.docx" 
          download="Samarth_Patel_Resume.docx"
          class="btn-secondary group"
          aria-label="Download my resume"
        >
          Download Resume
          <svg class="ml-2 w-5 h-5 transition-transform group-hover:translate-y-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
        </a>
      </div>
      
      <!-- Scroll Indicator -->
      <div class="mt-12 flex justify-center animate-bounce">
        <button 
          on:click={() => scrollToSection('expertise')}
          class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-300 transition-colors"
          aria-label="Scroll to next section"
        >
          <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
          </svg>
        </button>
      </div>
    </div>
  </div>
</section>

<style>
  /* Custom animation delays for staggered effect */
  :global(.animate-fade-in-1) {
    animation: fadeIn 0.6s ease-out 0.2s both;
  }
  
  :global(.animate-fade-in-2) {
    animation: fadeIn 0.6s ease-out 0.4s both;
  }
  
  :global(.animate-fade-in-3) {
    animation: fadeIn 0.6s ease-out 0.6s both;
  }
</style>
