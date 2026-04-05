<script setup lang="ts">
import { inject, type Ref, computed } from 'vue'
import { cn } from '@hemia/lume-vue'
import { Button } from '../button'

const dialog = inject<{
  open: Ref<boolean>
  onOpenChange: (value: boolean) => void
}>('alert-dialog')

const size = inject<string>('alert-dialog-size', 'md')

const props = defineProps<{
  class?: string
}>()

function close() {
  dialog?.onOpenChange(false)
}

const isSm = computed(() => size === 'sm')
</script>

<template>
  <Button
    variant="outline"
    :class="cn(isSm && 'w-full justify-center', props.class)"
    @click="close"
  >
    <slot />
  </Button>
</template>