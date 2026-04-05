<script setup lang="ts">
import { cn } from '@hemia/lume-vue'

const props = defineProps<{
  class?: string
}>()
</script>

<template>
  <div :class="cn('flex flex-col space-y-1.5 text-center sm:text-left px-6 pt-6 pb-2', props.class)">
    <div v-if="$slots.media" class="flex justify-center">
      <slot name="media" />
    </div>
    <slot />
  </div>
</template>