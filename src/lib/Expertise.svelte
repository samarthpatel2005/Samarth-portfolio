<script lang="ts">
  import { onMount } from 'svelte';
  
  let sectionVisible = false;
  let expertiseSection: HTMLElement;
  
  const expertiseAreas = [
    {
      title: 'Full-Stack Development',
      description: 'End-to-end web application development with modern frameworks and best practices.',
      icon: '🌐',
      technologies: ['React/Svelte', 'Node.js', 'TypeScript', 'Express']
    },
    {
      title: 'Mobile Development',
      description: 'Cross-platform mobile applications with native performance and beautiful UI.',
      icon: '📱',
      technologies: ['Flutter', 'Android']
    },
    {
      title: 'Cloud Architecture',
      description: 'Scalable cloud solutions with microservices and serverless architectures.',
      icon: '☁️',
      technologies: ['AWS', 'Docker', 'Kubernetes']
    },
    {
      title: 'DevOps & CI/CD',
      description: 'Automated deployment pipelines and infrastructure as code for reliable delivery.',
      icon: '🚀',
      technologies: ['GitHub Actions', 'Jenkins',]
    },
    {
      title: 'Database Design',
      description: 'Efficient database architecture for optimal performance and scalability.',
      icon: '🗄️',
      technologies: ['MongoDB', 'Redis', 'supabase']
    },
    {
      title: 'Web Technologies',
      description: 'Modern web technologies and frameworks for exceptional user experiences.',
      icon: '⚡',
      technologies: ['SvelteKit', 'Next.js', 'Tailwind CSS']
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
    
    if (expertiseSection) {
      observer.observe(expertiseSection);
    }
    
    return () => observer.disconnect();
  });
</script>

<section id="expertise" bind:this={expertiseSection} class="section-padding bg-white dark:bg-gray-900">
  <div class="container-custom">
    <!-- Section Header -->
    <div class={`text-center mb-16 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-4xl md:text-5xl font-bold mb-6 text-gray-900 dark:text-white">
        My <span class="text-gradient">Expertise</span>
      </h2>
      <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
        I specialize in building robust, scalable solutions across the full technology stack
      </p>
    </div>
    
    <!-- Expertise Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      {#each expertiseAreas as area, index}
        <div 
          class={`expertise-card group transition-all duration-700 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}
          style={`transition-delay: ${index * 100}ms`}
        >
          <!-- Icon -->
          <div class="text-4xl mb-4 group-hover:animate-float">
            {area.icon}
          </div>
          
          <!-- Title -->
          <h3 class="text-xl font-semibold mb-3 text-gray-900 dark:text-white group-hover:text-primary-600 transition-colors">
            {area.title}
          </h3>
          
          <!-- Description -->
          <p class="text-gray-600 dark:text-gray-400 mb-4 leading-relaxed">
            {area.description}
          </p>
          
          <!-- Technologies -->
          <div class="flex flex-wrap gap-2">
            {#each area.technologies as tech}
              <span class="px-3 py-1 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 text-sm rounded-full">
                {tech}
              </span>
            {/each}
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .expertise-card {
    @apply p-6 rounded-xl border border-gray-200 dark:border-gray-700 hover:border-primary-300 dark:hover:border-primary-600 hover:shadow-lg dark:hover:shadow-primary-500/10 transition-all duration-300 cursor-pointer;
    background: linear-gradient(145deg, rgba(255,255,255,0.1), rgba(255,255,255,0.05));
  }
  
  .dark .expertise-card {
    background: linear-gradient(145deg, rgba(17,24,39,0.8), rgba(31,41,55,0.4));
  }
  
  .expertise-card:hover {
    transform: translateY(-5px);
  }
</style>
