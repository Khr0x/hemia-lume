<script setup lang="ts">
import { cn } from '@hemia/lume-vue'

const props = defineProps<{
  class?: string
}>()
</script>

<template>
  <div :class="cn('w-auto inline-flex items-center justify-center rounded-md p-3', props.class)">
    <slot />
  </div>
</template>