<script lang="ts">
  import { onMount } from 'svelte';
  
  let sectionVisible = false;
  let techStackSection: HTMLElement;
  
  const techCategories = [
    {
      category: 'Frontend',
      technologies: [
        { name: 'Svelte', icon: '🔥', color: 'from-orange-500 to-red-500' },
        { name: 'React', icon: '⚛️', color: 'from-blue-500 to-cyan-500' },
        { name: 'TypeScript', icon: '📘', color: 'from-blue-600 to-blue-800' },
        { name: 'Tailwind CSS', icon: '🎨', color: 'from-cyan-500 to-blue-500' },
        { name: 'Next.js', icon: '▲', color: 'from-gray-800 to-gray-600' },
        { name: 'SvelteKit', icon: '🚀', color: 'from-orange-500 to-red-500' }
      ]
    },
    {
      category: 'Backend',
      technologies: [
        { name: 'Node.js', icon: '🟢', color: 'from-green-500 to-green-600' },
        { name: 'Python', icon: '🐍', color: 'from-yellow-500 to-blue-500' },
        { name: 'Express', icon: '⚡', color: 'from-gray-600 to-gray-800' },
        { name: 'FastAPI', icon: '🚀', color: 'from-green-400 to-blue-500' },
        { name: 'REST APIs', icon: '🔗', color: 'from-blue-500 to-purple-500' }
      ]
    },
    {
      category: 'Cloud & DevOps',
      technologies: [
        { name: 'AWS', icon: '☁️', color: 'from-orange-400 to-orange-600' },
        { name: 'Docker', icon: '🐳', color: 'from-blue-400 to-blue-600' },
        { name: 'Kubernetes', icon: '⚙️', color: 'from-blue-600 to-purple-600' },
        { name: 'GitHub Actions', icon: '🔄', color: 'from-gray-700 to-gray-900' }
      ]
    },
    {
      category: 'Database',
      technologies: [
        { name: 'MongoDB', icon: '🍃', color: 'from-green-500 to-green-700' },
        { name: 'Redis', icon: '🔴', color: 'from-red-500 to-red-700' },
        { name: 'Supabase', icon: '⚡', color: 'from-green-400 to-blue-500' },
        { name: 'MySql', icon: '💾', color: 'from-blue-400 to-blue-600' }
      ]
    }
  ];
  
  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            sectionVisible = true;
          }
        });
      },
      { threshold: 0.1 }
    );
    
    if (techStackSection) {
      observer.observe(techStackSection);
    }
    
    return () => observer.disconnect();
  });
</script>

<section id="tech-stack" bind:this={techStackSection} class="section-padding bg-gradient-to-br from-gray-50 to-gray-100 dark:from-gray-900 dark:to-gray-800">
  <div class="container-custom">
    <!-- Section Header -->
    <div class={`text-center mb-20 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-5xl md:text-6xl font-bold mb-6 text-gray-900 dark:text-white">
        Tech <span class="text-gradient bg-gradient-to-r from-primary-600 to-purple-600 bg-clip-text text-transparent">Stack</span>
      </h2>
      <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto leading-relaxed">
        Technologies and tools I use to build amazing digital experiences
      </p>
      <div class="w-24 h-1 bg-gradient-to-r from-primary-500 to-purple-500 mx-auto mt-6 rounded-full"></div>
    </div>
    
    <!-- Tech Categories -->
    <div class="space-y-16">
      {#each techCategories as category, categoryIndex}
        <div 
          class={`transition-all duration-700 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}
          style={`transition-delay: ${categoryIndex * 200}ms`}
        >
          <!-- Category Title -->
          <div class="text-center mb-10">
            <h3 class="text-3xl font-bold text-gray-900 dark:text-white mb-3">
              {category.category}
            </h3>
            <div class="w-16 h-0.5 bg-gradient-to-r from-primary-400 to-purple-400 mx-auto rounded-full"></div>
          </div>
          
          <!-- Technologies Grid -->
          <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-6 justify-items-center">
            {#each category.technologies as tech, techIndex}
              <div 
                class={`tech-card group relative ${sectionVisible ? 'animate-fade-in' : ''}`}
                style={`animation-delay: ${(categoryIndex * 200) + (techIndex * 100)}ms`}
              >
                <!-- Gradient Border Effect -->
                <div class="absolute inset-0 rounded-2xl bg-gradient-to-r from-purple-500 to-blue-500 opacity-0 group-hover:opacity-100 transition-all duration-300 p-0.5 scale-95 group-hover:scale-100">
                  <div class="w-full h-full bg-white dark:bg-gray-800 rounded-2xl"></div>
                </div>
                
                <!-- Card Content -->
                <div class="relative z-10 bg-white dark:bg-gray-800 rounded-2xl p-6 h-full flex flex-col items-center justify-center text-center border border-gray-200 dark:border-gray-700 group-hover:border-transparent transition-all duration-300 shadow-lg dark:shadow-xl group-hover:shadow-xl dark:group-hover:shadow-2xl">
                  <!-- Icon -->
                  <div class="text-5xl mb-4 group-hover:scale-110 transition-transform duration-300 filter group-hover:drop-shadow-lg">
                    {tech.icon}
                  </div>
                  
                  <!-- Tech Name -->
                  <span class="text-sm font-bold text-gray-900 dark:text-white transition-colors duration-300 group-hover:text-primary-600 dark:group-hover:text-primary-400">
                    {tech.name}
                  </span>
                </div>
              </div>
            {/each}
          </div>
        </div>
      {/each}
    </div>
    
    <!-- Additional Skills -->
    <div class={`mt-20 text-center transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style="transition-delay: 1000ms">
      <h4 class="text-2xl font-bold text-gray-900 dark:text-white mb-6">Also Experienced With</h4>
      <div class="flex flex-wrap justify-center gap-4 max-w-4xl mx-auto">
        {#each ['Git', 'Figma', 'VS Code', 'Postman', 'Jira', 'Slack', 'Notion'] as skill}
          <span class="px-6 py-3 bg-white dark:bg-gray-800 text-gray-800 dark:text-white rounded-full text-sm font-semibold border-2 border-gray-200 dark:border-gray-700 hover:border-primary-400 dark:hover:border-primary-500 hover:bg-primary-50 dark:hover:bg-gray-700 hover:text-primary-700 dark:hover:text-primary-300 transition-all duration-300 shadow-md hover:shadow-lg transform hover:-translate-y-1">
            {skill}
          </span>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .tech-card {
    width: 160px;
    height: 160px;
    margin: 0 auto;
    opacity: 0;
    transform: translateY(30px) scale(0.9);
    transition: all 0.3s ease;
  }
  
  .tech-card.animate-fade-in {
    animation: cardFadeIn 0.8s ease-out forwards;
  }
  
  .tech-card:hover {
    transform: translateY(-8px) scale(1.05);
  }
  
  @keyframes cardFadeIn {
    0% {
      opacity: 0;
      transform: translateY(30px) scale(0.9);
    }
    100% {
      opacity: 1;
      transform: translateY(0) scale(1);
    }
  }
  
  /* Ensure responsive grid centering */
  @media (max-width: 640px) {
    .tech-card {
      width: 140px;
      height: 140px;
    }
  }
  
  @media (max-width: 480px) {
    .tech-card {
      width: 120px;
      height: 120px;
    }
  }
</style>
