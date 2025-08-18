<script lang="ts">
  import { onMount } from 'svelte';
  
  let sectionVisible = false;
  let ctaSection: HTMLElement;
  
  const contactMethods = [
    {
      icon: '📧',
      label: 'Email',
      value: 'samarthpatel2706@gmail.com',
      href: 'mailto:samarthpatel2706@gmail.com'
    },
    {
      icon: '💼',
      label: 'LinkedIn',
      value: 'Smarth Patel',
      href: 'https://www.linkedin.com/in/samarth-patel-051757283/'
    },
    {
      icon: '🐙',
      label: 'GitHub',
      value: 'Samarthpatel',
      href: 'https://github.com/samarthpatel2005'
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
    
    if (ctaSection) {
      observer.observe(ctaSection);
    }
    
    return () => observer.disconnect();
  });
  
  const openContactForm = () => {
    // Create a proper mailto link that should work across all systems
    const subject = encodeURIComponent("Let's collaborate!");
    const body = encodeURIComponent("Hi Samarth,\n\nI'd love to discuss a potential project with you.\n\nBest regards");
    const mailtoLink = `mailto:samarthpatel2706@gmail.com?subject=${subject}&body=${body}`;
    
    try {
      // Try to open the default email client
      window.location.href = mailtoLink;
    } catch (error) {
      // Fallback: copy email to clipboard and show notification
      navigator.clipboard.writeText('samarthpatel2706@gmail.com').then(() => {
        alert('Email address copied to clipboard: samarthpatel2706@gmail.com');
      }).catch(() => {
        // Ultimate fallback: just show the email
        alert('Please send an email to: samarthpatel2706@gmail.com');
      });
    }
  };
</script>

<section id="cta" bind:this={ctaSection} class="section-padding bg-gradient-to-br from-primary-600 via-primary-700 to-purple-700 relative overflow-hidden">
  <!-- Background Pattern -->
  <div class="absolute inset-0 opacity-10">
    <div class="absolute inset-0" style="background-image: radial-gradient(circle at 2px 2px, white 1px, transparent 0); background-size: 50px 50px;"></div>
  </div>
  
  <div class="container-custom relative z-10">
    <div class={`text-center text-white transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <!-- Main CTA -->
      <h2 class="text-4xl md:text-6xl font-bold mb-6 leading-tight">
        Ready to Build Something
        <span class="block bg-gradient-to-r from-yellow-300 to-orange-300 bg-clip-text text-transparent">
          Amazing?
        </span>
      </h2>
      
      <p class="text-xl md:text-2xl mb-8 text-blue-100 max-w-3xl mx-auto">
        Let's collaborate and turn your vision into reality. I'm always excited to work on innovative projects and solve challenging problems.
      </p>
      
      <!-- Primary CTA Button -->
      <div class="mb-12">
        <button 
          on:click={openContactForm}
          class="inline-flex items-center px-8 py-4 bg-white text-primary-700 font-semibold text-lg rounded-lg hover:bg-gray-100 transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-4 focus:ring-white/30 group"
          aria-label="Get in touch to start a project"
        >
          Get in Touch
          <svg class="ml-3 w-6 h-6 transition-transform group-hover:translate-x-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
          </svg>
        </button>
      </div>
      
      <!-- Contact Methods -->
      <div class={`transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style="transition-delay: 300ms">
        <p class="text-blue-200 mb-6">Or reach out directly:</p>
        <div class="flex flex-col sm:flex-row justify-center items-center gap-6">
          {#each contactMethods as method, index}
            <a 
              href={method.href}
              target="_blank"
              rel="noopener noreferrer"
              class="contact-method group"
              style={`animation-delay: ${index * 100}ms`}
              aria-label={`Contact via ${method.label}: ${method.value}`}
            >
              <span class="text-2xl group-hover:animate-float">{method.icon}</span>
              <div class="text-left">
                <div class="text-sm text-blue-200 group-hover:text-white transition-colors">
                  {method.label}
                </div>
                <div class="text-white font-medium group-hover:text-yellow-300 transition-colors">
                  {method.value}
                </div>
              </div>
            </a>
          {/each}
        </div>
      </div>
      
      <!-- Additional Info -->
      <div class={`mt-16 pt-8 border-t border-white/20 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style="transition-delay: 600ms">
        <p class="text-blue-200 text-sm">
          Available for freelance projects, full-time opportunities, and consulting work
        </p>
        <div class="flex justify-center items-center mt-4 space-x-4">
          <span class="flex items-center text-blue-200 text-sm">
            <span class="w-2 h-2 bg-green-400 rounded-full mr-2 animate-pulse"></span>
            Currently available
          </span>
          <span class="text-blue-300">•</span>
          <span class="text-blue-200 text-sm">
            Response time: 24h
          </span>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .contact-method {
    @apply flex items-center space-x-3 p-4 rounded-lg bg-white/10 hover:bg-white/20 transition-all duration-300 transform hover:scale-105 border border-white/20 hover:border-white/40;
    animation: slideUp 0.6s ease-out forwards;
    opacity: 0;
  }
  
  @keyframes slideUp {
    from {
      opacity: 0;
      transform: translateY(30px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
</style>
