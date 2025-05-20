<template>
  <div 
    class="rounded-lg shadow-lg overflow-hidden flex flex-col"
    :class="cardClasses"
  >
    <!-- Project Image -->
    <div v-if="!hideCardImage" class="relative w-full h-36 bg-muted overflow-hidden">
      <img
        v-if="logo"
        :src="logo"
        :alt="title + ' screenshot'"
        class="w-full h-full object-cover"
      />
      <div v-else class="w-full h-full flex items-center justify-center bg-muted">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-10 h-10 text-muted-foreground">
          <rect width="18" height="18" x="3" y="3" rx="2" ry="2" />
          <path d="M3 9h18" />
          <path d="M9 21V9" />
        </svg>
      </div>
    </div>

    <!-- Project Content -->
    <div class="p-4 flex flex-col flex-1 bg-card text-card-foreground">
      <div>
        <h3 class="text-lg font-semibold mb-1">{{ title }}</h3>
        <p class="text-xs text-muted-foreground flex items-center gap-1">
          <template v-for="(tech, index) in (Array.isArray(tech) ? tech : [tech])" :key="tech">
            <img 
              :src="techIcon[index]"
              :alt="tech + ' icon'"
              class="w-3 h-3"
            />
            <span>{{ tech }}</span>
            <span v-if="index < (Array.isArray(tech) ? tech.length - 1 : 0)" class="mx-1">•</span>
          </template>
        </p>
      </div>
      <p class="text-sm mt-2">{{ description }}</p>
      <div class="flex gap-2 mt-auto pt-4">
        <Button 
          v-if="demo" 
          as="a" 
          :href="demo" 
          target="_blank" 
          :class="primaryButtonClasses"
          size="sm"
        >
          View
        </Button>
        <Button 
          v-if="source && title !== 'SPA Framework Wizard'" 
          as="a" 
          :href="source" 
          target="_blank" 
          :class="secondaryButtonClasses"
          size="sm"
        >
          Source
        </Button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { computed } from 'vue'

const props = defineProps<{
  title: string
  description: string
  tech: string | string[]
  logo?: string
  demo?: string
  source?: string
  hideViewButton?: boolean
  hideCardImage?: boolean
}>()

// Tech stack icons mapping
const techIcons = {
  'Nuxt': 'https://nuxt.com/assets/design-kit/icon-green.svg',
  'React': 'https://cdn.worldvectorlogo.com/logos/react-2.svg',
  'Vue': 'https://vuejs.org/images/logo.png',
  'Angular': 'https://angular.dev/assets/images/press-kit/angular_icon_gradient.gif',
  'Express': 'https://expressjs.com/images/favicon.png'
}

const techIcon = computed(() => {
  const techs = Array.isArray(props.tech) ? props.tech : [props.tech]
  return techs.map(tech => {
    const techLower = tech.toLowerCase()
    if (techLower.includes('nuxt')) return techIcons.Nuxt
    if (techLower.includes('react')) return techIcons.React
    if (techLower.includes('vue')) return techIcons.Vue
    if (techLower.includes('angular')) return techIcons.Angular
    if (techLower.includes('express')) return techIcons.Express
    return ''
  }).filter(Boolean)
})

// Color mapping based on tech stack
const colorMap = {
  'Nuxt': {
    border: 'border-[#00DC82]',
    primary: 'bg-[#00DC82] hover:bg-[#00DC82]/90 text-white',
    secondary: 'bg-[#00DC82]/10 hover:bg-[#00DC82]/20 text-[#00DC82]'
  },
  'React': {
    border: 'border-[#61DAFB]',
    primary: 'bg-[#61DAFB] hover:bg-[#61DAFB]/90 text-[#282C34]',
    secondary: 'bg-[#61DAFB]/10 hover:bg-[#61DAFB]/20 text-[#61DAFB]'
  },
  'Vue': {
    border: 'border-[#41B883]',
    primary: 'bg-[#41B883] hover:bg-[#41B883]/90 text-white',
    secondary: 'bg-[#41B883]/10 hover:bg-[#41B883]/20 text-[#41B883]'
  },
  'Angular': {
    border: 'border-[#E91E63]',
    primary: 'bg-[#E91E63] hover:bg-[#E91E63]/90 text-white',
    secondary: 'bg-[#E91E63]/10 hover:bg-[#E91E63]/20 text-[#E91E63]'
  },
  'Express': {
    border: 'border-[#000000]',
    primary: 'bg-[#000000] hover:bg-[#000000]/90 text-white',
    secondary: 'bg-[#000000]/10 hover:bg-[#000000]/20 text-[#000000]'
  },
  'default': {
    border: 'border-primary',
    primary: 'bg-primary hover:bg-primary/90 text-primary-foreground',
    secondary: 'bg-secondary hover:bg-secondary/80 text-secondary-foreground'
  }
}

// Determine which color scheme to use based on tech stack
const colorScheme = computed(() => {
  const techs = Array.isArray(props.tech) ? props.tech : [props.tech]
  const tech = techs[0].toLowerCase()
  if (tech.includes('nuxt')) return colorMap.Nuxt
  if (tech.includes('react')) return colorMap.React
  if (tech.includes('vue')) return colorMap.Vue
  if (tech.includes('angular')) return colorMap.Angular
  if (tech.includes('express')) return colorMap.Express
  return colorMap.default
})

const cardClasses = computed(() => ({
  'border-2': true,
  [colorScheme.value.border]: true
}))

const primaryButtonClasses = computed(() => ({
  'inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50': true,
  [colorScheme.value.primary]: true
}))

const secondaryButtonClasses = computed(() => ({
  'inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-1 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50': true,
  [colorScheme.value.secondary]: true
}))
</script> 