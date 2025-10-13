<script lang="ts">
  import { onMount } from 'svelte';
  
  let sectionVisible = false;
  let achievementsSection: HTMLElement;
  
  const achievements = [
    {
      title: "AWS Certified Solutions Architect",
      issuer: "Amazon Web Services",
      date: "2024",
      description: "Professional certification in cloud architecture and AWS services",
      type: "certification",
      credentialId: "AWS-SA-2024",
      verifyUrl: "/certificates/aws-solutions-architect.pdf"
    },
    {
      title: "Google Cloud Professional Developer",
      issuer: "Google Cloud",
      date: "2024",
      description: "Expertise in developing applications on Google Cloud Platform",
      type: "certification",
      credentialId: "GCP-PD-2024",
      verifyUrl: "/certificates/gcp-professional-developer.pdf"
    },
    {
      title: "ISRO Hack2Skill Certification",
      issuer: "ISRO (Indian Space Research Organisation)",
      date: "2024",
      description: "Certification in space technology and satellite data analysis",
      type: "certificate",
      credentialId: "ISRO-H2S-2024",
      verifyUrl: "/certificates/Hack2skill-Certificate.png"
    },
    {
      title: "Google Agile Project Management Certificate",
      issuer: "Google",
      date: "2024",
      description: "Professional certificate in Agile Project Management",
      type: "certificate",
      credentialId: "GOOGLE-DA-2024",
      verifyUrl: "/certificates/Agile Project Management.pdf"
    },
    {
      title: "Google Foundations of Project Management",
      issuer: "Google",
      date: "2024",
      description: "Comprehensive training in project management methodologies and tools",
      type: "certificate",
      credentialId: "GOOGLE-PM-2024",
      verifyUrl: "/certificates/Foundations of Project Management.pdf"
    },
    {
      title: "Hackathon Participant",
      issuer: "techtonic 2023",
      date: "2023",
      description: "Participent in web development category",
      type: "certificate",
      credentialId: "DEVFEST-2023",
      verifyUrl: "/certificates/Techtonic.jpg"
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
    
    if (achievementsSection) {
      observer.observe(achievementsSection);
    }
    
    return () => observer.disconnect();
  });
  
  function getIconForType(type: string): string {
    switch (type) {
      case 'certification':
        return '🏆';
      case 'certificate':
        return '📜';
      case 'award':
        return '🥇';
      default:
        return '🏅';
    }
  }
  
  function getColorForType(type: string): string {
    switch (type) {
      case 'certification':
        return 'from-yellow-400 to-orange-500';
      case 'certificate':
        return 'from-blue-400 to-purple-500';
      case 'award':
        return 'from-green-400 to-emerald-500';
      default:
        return 'from-gray-400 to-gray-500';
    }
  }
  
  function openCertificate(verifyUrl: string) {
    if (verifyUrl) {
      // Open the certificate file in a new tab
      window.open(verifyUrl, '_blank');
    }
  }
</script>

<section id="achievements" bind:this={achievementsSection} class="section-padding bg-gradient-to-br from-gray-50 to-gray-100 dark:from-gray-900 dark:to-gray-800">
  <div class="container-custom">
    <!-- Section Header -->
    <div class={`text-center mb-20 transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
      <h2 class="text-5xl md:text-6xl font-bold mb-6 text-gray-900 dark:text-white">
        Achievements & 
        <span class="text-gradient bg-gradient-to-r from-primary-600 to-purple-600 bg-clip-text text-transparent">
          Certifications
        </span>
      </h2>
      <p class="text-xl text-gray-600 dark:text-gray-300 max-w-3xl mx-auto leading-relaxed">
        Recognition and certifications that validate my skills and commitment to continuous learning
      </p>
      <div class="w-24 h-1 bg-gradient-to-r from-primary-500 to-purple-500 mx-auto mt-6 rounded-full"></div>
    </div>
    
    <!-- Achievements Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-7xl mx-auto">
      {#each achievements as achievement, index}
        <div 
          class={`achievement-card group relative ${sectionVisible ? 'animate-fade-in' : ''}`}
          style={`animation-delay: ${index * 150}ms`}
        >
          <!-- Card Content -->
          <div class="relative z-10 bg-white dark:bg-gray-800 rounded-2xl p-6 h-full border border-gray-200 dark:border-gray-700 group-hover:border-blue-500 group-hover:shadow-[0_0_15px_rgba(59,130,246,0.5)] transition-all duration-300 shadow-lg dark:shadow-xl">
            <!-- Achievement Type Badge -->
            <div class="flex items-center justify-between mb-4">
              <div class={`inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold text-white bg-gradient-to-r ${getColorForType(achievement.type)}`}>
                <span class="mr-1">{getIconForType(achievement.type)}</span>
                {achievement.type.charAt(0).toUpperCase() + achievement.type.slice(1)}
              </div>
              <span class="text-sm text-gray-500 dark:text-gray-400 font-medium">
                {achievement.date}
              </span>
            </div>
            
            <!-- Achievement Title -->
            <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors duration-300">
              {achievement.title}
            </h3>
            
            <!-- Issuer -->
            <p class="text-primary-600 dark:text-primary-400 font-semibold mb-3">
              {achievement.issuer}
            </p>
            
            <!-- Description -->
            <p class="text-gray-600 dark:text-gray-300 text-sm leading-relaxed mb-4">
              {achievement.description}
            </p>
            
            <!-- Credential Info -->
            {#if achievement.credentialId}
              <div class="mt-auto">
                <div class="flex items-center justify-between text-xs text-gray-500 dark:text-gray-400">
                  <span>ID: {achievement.credentialId}</span>
                  {#if achievement.verifyUrl}
                    <button 
                      on:click={() => openCertificate(achievement.verifyUrl)}
                      class="text-blue-500 hover:text-blue-600 dark:text-blue-400 dark:hover:text-blue-300 font-medium transition-colors duration-200 cursor-pointer border-none bg-transparent"
                    >
                      View Certificate →
                    </button>
                  {/if}
                </div>
              </div>
            {/if}
          </div>
        </div>
      {/each}
    </div>
    
    <!-- Call to Action -->
    <div class={`mt-16 text-center transition-all duration-1000 ${sectionVisible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`} style="transition-delay: 800ms">
      <p class="text-gray-600 dark:text-gray-300 mb-6">
        Continuously learning and growing in the tech industry
      </p>
      <div class="flex justify-center items-center space-x-8">
        <div class="text-center">
          <div class="text-3xl font-bold text-primary-600 dark:text-primary-400">6+</div>
          <div class="text-sm text-gray-500 dark:text-gray-400">Certifications</div>
        </div>
        <div class="w-px h-12 bg-gray-300 dark:bg-gray-600"></div>
        <div class="text-center">
          <div class="text-3xl font-bold text-primary-600 dark:text-primary-400">3+</div>
          <div class="text-sm text-gray-500 dark:text-gray-400">Awards</div>
        </div>
        <div class="w-px h-12 bg-gray-300 dark:bg-gray-600"></div>
        <div class="text-center">
          <div class="text-3xl font-bold text-primary-600 dark:text-primary-400">2024</div>
          <div class="text-sm text-gray-500 dark:text-gray-400">Latest Cert</div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .achievement-card {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
    transition: all 0.3s ease;
  }
  
  .achievement-card.animate-fade-in {
    animation: cardFadeIn 0.8s ease-out forwards;
  }
  
  .achievement-card:hover {
    transform: translateY(-4px) scale(1.02);
  }
  
  @keyframes cardFadeIn {
    0% {
      opacity: 0;
      transform: translateY(30px) scale(0.95);
    }
    100% {
      opacity: 1;
      transform: translateY(0) scale(1);
    }
  }
  
  /* Responsive adjustments */
  @media (max-width: 768px) {
    .achievement-card {
      transform: translateY(20px) scale(0.98);
    }
    
    .achievement-card:hover {
      transform: translateY(-2px) scale(1.01);
    }
  }
</style>