<template>
  <section class="mb-16">
    <h2 class="text-3xl font-semibold mb-8">Blog Posts</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 w-full">
      <div 
        v-for="post in posts" 
        :key="post.title"
        class="rounded-lg shadow-lg overflow-hidden flex flex-col border-2 border-primary"
      >
        <!-- Blog Content -->
        <div class="p-4 flex flex-col flex-1 bg-card text-card-foreground">
          <div>
            <h3 class="text-lg font-semibold mb-1">{{ post.title }}</h3>
            <p class="text-xs text-muted-foreground mb-2">{{ post.date }}</p>
          </div>
          <p class="text-sm mt-2">{{ post.description }}</p>
          <div class="flex gap-2 mt-auto pt-4">
            <Button 
              as="a" 
              :href="post.url" 
              target="_blank" 
              class="bg-primary hover:bg-primary/90 text-primary-foreground"
              size="sm"
            >
              Read More
            </Button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Button } from '@/components/ui/button'

const posts = [
  {
    title: 'The Rendering Equation: Client + Server + Framework',
    description: 'A deep dive into client-side rendering, server-side rendering, and how modern frameworks handle both approaches.',
    date: 'March 2024',
    url: 'https://medium.com/state-farm-engineering-blog/the-rendering-equation-client-server-framework-aca0018832b6'
  }
]
</script> 