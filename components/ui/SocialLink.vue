<template>
  <a 
    :href="href" 
    target="_blank"
    class="inline-flex items-center text-lg text-primary hover:underline"
  >
    <slot name="icon" />
    <span class="ml-2">{{ text }}</span>
  </a>
</template>

<script setup lang="ts">
defineProps<{
  href: string
  text: string
}>()
</script> 