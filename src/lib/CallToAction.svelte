<script lang="ts">
  import { onMount } from 'svelte';
  import { SITE_CONFIG } from './utils/constants';
  
  let sectionVisible = false;
  let ctaSection: HTMLElement;
  
  const contactMethods = [
    {
      icon: '📧',
      label: 'Email',
      value: SITE_CONFIG.email,
      href: `mailto:${SITE_CONFIG.email}`
    },
    {
      icon: '💼',
      label: 'LinkedIn',
      value: 'Smarth Patel',
      href: SITE_CONFIG.linkedin
    },
    {
      icon: '🐙',
      label: 'GitHub',
      value: 'Samarthpatel',
      href: SITE_CONFIG.github
    }
  ];
  
  // Modal / form state
  let showModal = false;
  let isSubmitting = false;
  let name = '';
  let email = '';
  let message = '';
  
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
    
    // Close modal on Escape key
    const onKey = (e: KeyboardEvent) => {
      if (e.key === 'Escape' && showModal) showModal = false;
    };
    window.addEventListener('keydown', onKey);

    return () => {
      observer.disconnect();
      window.removeEventListener('keydown', onKey);
    };
  });
  
  const openContactForm = () => {
    showModal = true;
  };
  
  const closeModal = () => {
    showModal = false;
  };
  
  const handleOverlayClick = (e: MouseEvent) => {
    if (e.target === e.currentTarget) closeModal();
  };
  
  const handleOverlayKeydown = (e: KeyboardEvent) => {
    // Only close when Enter/Space is pressed and the overlay (not an input) is the target or focused.
    const target = e.target as HTMLElement;
    const current = e.currentTarget as HTMLElement | null;
    const active = document.activeElement as HTMLElement | null;

    if ((e.key === 'Enter' || e.key === ' ') && (current && (target === current || active === current))) {
      e.preventDefault();
      closeModal();
    }
  };
  
  async function handleSubmit(e: Event) {
    e.preventDefault();
    if (isSubmitting) return;
    isSubmitting = true;

    const subject = encodeURIComponent(`${name ? name + ' - ' : ''}Website inquiry`);
    const bodyText = `Name: ${name}\nEmail: ${email}\n\n${message}`;
    const body = encodeURIComponent(bodyText);
    const mailtoLink = `mailto:${SITE_CONFIG.email}?subject=${subject}&body=${body}`;

    try {
      // If you have a form endpoint (Formspree / EmailJS / Netlify) configured in SITE_CONFIG.formEndpoint,
      // try to POST first. Fallback to mailto if not present or if POST fails.
      if ((SITE_CONFIG as any).formEndpoint) {
        const resp = await fetch((SITE_CONFIG as any).formEndpoint, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json', 'Accept': 'application/json' },
          body: JSON.stringify({ name, email, message })
        });
        if (resp.ok) {
          alert('Message sent — thank you!');
          closeModal();
          isSubmitting = false;
          return;
        }
      }

      // Open user's email client as a fallback
      window.location.href = mailtoLink;
      closeModal();
    } catch (err) {
      // If anything fails, fallback to mailto
      window.location.href = mailtoLink;
      closeModal();
    } finally {
      isSubmitting = false;
    }
  }
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

      <!-- Modal: Contact Form -->
      {#if showModal}
        <div class="fixed inset-0 z-50 flex items-center justify-center bg-black/50" on:click={handleOverlayClick} on:keydown={handleOverlayKeydown} aria-modal="true" role="dialog" tabindex="-1">
          <div class="bg-white rounded-lg p-6 max-w-md w-full mx-4">
            <h3 class="text-xl font-semibold mb-4 text-black">Get in Touch</h3>
            <form on:submit={handleSubmit} class="space-y-4">
              <div>
                <label for="contact-name" class="block text-sm text-black mb-1">Your name</label>
                <input id="contact-name" class="w-full border rounded px-3 py-2 bg-white text-black" bind:value={name} required />
              </div>
              <div>
                <label for="contact-email" class="block text-sm text-black mb-1">Your email</label>
                <input id="contact-email" type="email" class="w-full border rounded px-3 py-2 bg-white text-black" bind:value={email} required />
              </div>
              <div>
                <label for="contact-message" class="block text-sm text-black mb-1">Message</label>
                <textarea id="contact-message" class="w-full border rounded px-3 py-2 h-28 bg-white text-black" bind:value={message} required></textarea>
              </div>
              <div class="flex items-center justify-between">
                <button type="submit" class="bg-primary-600 text-white px-4 py-2 rounded font-medium" disabled={isSubmitting}>{isSubmitting ? 'Sending...' : 'Send Message'}</button>
                <button type="button" class="text-sm text-gray-600 underline" on:click={closeModal}>Cancel</button>
              </div>
            </form>
          </div>
        </div>
      {/if}

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
