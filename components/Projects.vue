<template>
  <section class="mb-16">
    <h2 class="text-3xl font-semibold mb-8">Projects</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 w-full">
      <ProjectCard
        v-for="project in projects"
        :key="project.title"
        v-bind="project"
      />
    </div>
  </section>
</template>

<script setup lang="ts">
import ProjectCard from '@/components/ui/ProjectCard.vue'

const projects = [
  {
    title: 'SPA Framework Wizard',
    description: 'A wizard application that helps developers choose the right Single Page Application framework based on their needs and experience.',
    tech: 'Angular',
    logo: '/spa-framework-wizard.png',
    demo: 'https://spa-framework-wizard.web.app',
    source: 'https://github.com/jmleep/spa-framework-wizard'
  },
  {
    title: 'LocalBirdTracker',
    description: 'A website that allows users to query recent bird sightings based on their current latitude and longitude (US only).',
    tech: 'Vue',
    logo: '/localbirdtracker.png',
    demo: 'https://www.localbirdtracker.com',
    source: 'https://github.com/jmleep/LocalBirdTracker'
  },
  {
    title: 'CocktailGenie',
    description: 'A web application that uses the free cocktail API to help you find new drink recipes.',
    tech: 'Angular',
    logo: '/cocktailgenie.png',
    demo: 'https://cocktail-genie-1804c.web.app',
    source: 'https://github.com/jmleep/cocktails'
  },
  {
    title: 'Dev Logo Colorizer',
    description: 'A web application that allows developers to customize and download colored versions of popular development framework logos.',
    tech: 'Nuxt',
    logo: '/dev-logo-colorizer.png',
    demo: 'https://dev-logo-colorizer.nuxt.dev',
    source: 'https://github.com/jmleep/dev-logo-colorizer'
  },
  {
    title: 'Site Parser',
    description: 'A web application that allows users to enter a URL and view information about the site, including images and word frequency analysis.',
    tech: ['React', 'Express'],
    logo: 'https://cdn.worldvectorlogo.com/logos/react-2.svg',
    source: 'https://github.com/jmleep/SiteParser',
    hideViewButton: true,
    hideCardImage: true
  }
]
</script> 