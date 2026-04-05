<script setup lang="ts">
import { inject, computed } from 'vue'
import { cn } from '@hemia/lume-vue'
import { Button } from '../button'

const size = inject<string>('alert-dialog-size', 'md')

const props = defineProps<{
  variant?: 'default' | 'destructive'
  class?: string
}>()

const isSm = computed(() => size === 'sm')
</script>

<template>
  <Button :variant="props.variant" :class="cn(isSm && 'w-full justify-center', props.class)">
    <slot />
  </Button>
</template>