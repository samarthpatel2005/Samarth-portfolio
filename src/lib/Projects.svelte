<script lang="ts">
  import { onMount } from 'svelte';
  
  let sectionVisible = false;
  let projectsSection: HTMLElement;
  
  const projects = [
    {
      title: 'Auto Blog Generator',
      description: 'Discover engaging, AI-generated content from trending news and topics. Stay informed with fresh, quality articles updated regularly.',
      image: 'https://images.unsplash.com/photo-1486312338219-ce68d2c6f44d?w=500&h=300&fit=crop',
      technologies: ['React', 'Node.js', 'Express', 'MongoDB'],
      github: 'https://github.com/samarthpatel2005/blog-_generator',
      demo: 'https://auto-blog-generator-lake.vercel.app/',
      featured: true
    },
    {
      title: 'Online Gambling App',
      description: 'A feature-rich gambling platform built with secure backend architecture. Picks7 includes real-time game logic, user wallet management, betting history, and an admin dashboard for game control.',
      image: 'https://images.unsplash.com/photo-1596838132731-3301c3fd4317?w=500&h=300&fit=crop',
      technologies: ['Flutter', 'Node.js', 'MongoDB', 'Stripe', 'Express', 'Digital Ocean'],
      github: 'https://github.com/samarthpatel/task-manager',
      demo: 'https://picks7.com/',
      featured: true
    },
    {
      title: 'FinEd Financial Literacy App',
      description: 'Gamified lessons on budgeting, investing, and saving. AI-driven chatbot to answer financial queries. Daily finance challenges with rewards',
      image: 'https://images.unsplash.com/photo-1563013544-824ae1b704d3?w=500&h=300&fit=crop',
      technologies: ['Typescript', 'Node.js', 'Express', 'Supabase'],
      github: 'https://github.com/samarthpatel2005/FInEd',
      demo: 'https://unique-druid-d481eb.netlify.app/',
      featured: true
    },
    {
      title: 'API Gateway Service',
      description: 'Microservices API gateway with rate limiting, authentication, and comprehensive monitoring.',
      image: 'https://images.unsplash.com/photo-1558494949-ef010cbdcc31?w=500&h=300&fit=crop',
      technologies: ['Node.js', 'Redis', 'JWT', 'Docker', 'Kubernetes'],
      github: 'https://github.com/samarthpatel/api-gateway',
      demo: null,
      featured: true
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
    
    if (projectsSection) {
      observer.observe(projectsSection);
    }
    
    return () => observer.disconnect();
  });
</script>

<section id="projects" bind:this={projectsSection} class="section-padding bg-white dark:bg-gray-900">
  <div class="container-custom">
    <!-- Section Header -->
    <div class={`text-center mb-16 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-4xl md:text-5xl font-bold mb-6 text-gray-900 dark:text-white">
        My <span class="text-gradient">Projects</span>
      </h2>
      <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
        A showcase of recent projects demonstrating technical expertise and problem-solving capabilities
      </p>
    </div>
    
    <!-- Featured Projects -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12 items-stretch">
      {#each projects.filter(p => p.featured) as project, index}
        <div 
          class={`project-card featured flex flex-col transition-all duration-700 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}
          style={`transition-delay: ${index * 200}ms`}
        >
          <!-- Project Image -->
          <div class="relative overflow-hidden rounded-t-xl h-48 group flex-shrink-0">
            <img 
              src={project.image} 
              alt={`${project.title} screenshot`}
              class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
              loading="lazy"
            />
            <div class="absolute inset-0 bg-black/40 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center">
              <div class="flex space-x-4">
                {#if project.demo}
                  <a 
                    href={project.demo}
                    target="_blank"
                    rel="noopener noreferrer"
                    class="px-4 py-2 bg-white text-gray-900 rounded-lg font-medium hover:bg-gray-100 transition-colors"
                    aria-label={`View live demo of ${project.title}`}
                  >
                    Live Demo
                  </a>
                {/if}
                <a 
                  href={project.github}
                  target="_blank"
                  rel="noopener noreferrer"
                  class="px-4 py-2 bg-gray-900 text-white rounded-lg font-medium hover:bg-gray-800 transition-colors"
                  aria-label={`View ${project.title} source code on GitHub`}
                >
                  GitHub
                </a>
              </div>
            </div>
          </div>
          
          <!-- Project Content -->
          <div class="p-6 bg-white dark:bg-gray-800 flex-grow flex flex-col">
            <h3 class="text-xl font-semibold mb-3 text-gray-900 dark:text-white">
              {project.title}
            </h3>
            <p class="text-gray-600 dark:text-gray-300 mb-4 leading-relaxed flex-grow">
              {project.description}
            </p>
            
            <!-- Technologies -->
            <div class="flex flex-wrap gap-2 mt-auto">
              {#each project.technologies as tech}
                <span class="px-3 py-1 bg-primary-100 dark:bg-primary-900/40 text-primary-700 dark:text-primary-200 text-sm rounded-full border dark:border-primary-700/50">
                  {tech}
                </span>
              {/each}
            </div>
          </div>
        </div>
      {/each}
    </div>
    
    <!-- Other Projects -->
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 items-stretch">
      {#each projects.filter(p => !p.featured) as project, index}
        <div 
          class={`project-card flex flex-col transition-all duration-700 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}
          style={`transition-delay: ${(index + 2) * 200}ms`}
        >
          <!-- Project Image -->
          <div class="relative overflow-hidden rounded-t-xl h-32 group flex-shrink-0">
            <img 
              src={project.image} 
              alt={`${project.title} screenshot`}
              class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
              loading="lazy"
            />
          </div>
          
          <!-- Project Content -->
          <div class="p-4 bg-white dark:bg-gray-800 flex-grow flex flex-col">
            <h3 class="text-lg font-semibold mb-2 text-gray-900 dark:text-white">
              {project.title}
            </h3>
            <p class="text-gray-600 dark:text-gray-300 mb-3 text-sm leading-relaxed flex-grow">
              {project.description}
            </p>
            
            <!-- Technologies -->
            <div class="flex flex-wrap gap-1 mb-3">
              {#each project.technologies.slice(0, 3) as tech}
                <span class="px-2 py-1 bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 text-xs rounded border dark:border-gray-600">
                  {tech}
                </span>
              {/each}
              {#if project.technologies.length > 3}
                <span class="px-2 py-1 bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-200 text-xs rounded border dark:border-gray-600">
                  +{project.technologies.length - 3} more
                </span>
              {/if}
            </div>
            
            <!-- Links -->
            <div class="flex space-x-3 mt-auto">
              {#if project.demo}
                <a 
                  href={project.demo}
                  target="_blank"
                  rel="noopener noreferrer"
                  class="text-primary-600 dark:text-primary-400 hover:text-primary-700 dark:hover:text-primary-300 font-medium text-sm"
                  aria-label={`View live demo of ${project.title}`}
                >
                  Demo ↗
                </a>
              {/if}
              <a 
                href={project.github}
                target="_blank"
                rel="noopener noreferrer"
                class="text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-gray-100 font-medium text-sm"
                aria-label={`View ${project.title} source code on GitHub`}
              >
                GitHub ↗
              </a>
            </div>
          </div>
        </div>
      {/each}
    </div>
    
    <!-- Call to Action -->
    <div class={`text-center mt-12 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style="transition-delay: 800ms">
      <p class="text-gray-600 dark:text-gray-400 mb-4">
        Want to see more of my work?
      </p>
      <a 
        href="https://github.com/samarthpatel2005"
        target="_blank"
        rel="noopener noreferrer"
        class="btn-primary"
        aria-label="View all projects on GitHub"
      >
        View All Projects on GitHub
        <svg class="ml-2 w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
        </svg>
      </a>
    </div>
  </div>
</section>

<style>
  .project-card {
    @apply bg-white dark:bg-gray-800 rounded-xl border border-gray-200 dark:border-gray-600 hover:shadow-lg dark:hover:shadow-2xl dark:hover:shadow-primary-500/20 transition-all duration-300 overflow-hidden;
  }
  
  .project-card.featured {
    @apply hover:shadow-xl dark:hover:shadow-2xl dark:hover:shadow-primary-500/25 border-gray-300 dark:border-gray-500;
  }
  
  .project-card:hover {
    transform: translateY(-5px);
  }
</style>
