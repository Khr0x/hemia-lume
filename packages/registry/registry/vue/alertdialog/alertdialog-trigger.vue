<script setup lang="ts">
import { inject, type Ref } from 'vue'

const dialog = inject<{
  open: Ref<boolean>
  onOpenChange: (value: boolean) => void
}>('alert-dialog')

const props = defineProps<{
  asChild?: boolean
  class?: string
}>()

function onClick(event: MouseEvent) {
  // Stop propagation to prevent double-firing
  event.stopPropagation()
  dialog?.onOpenChange(true)
}
</script>

<template>
  <component
    :is="props.asChild ? 'span' : 'button'"
    :class="props.class"
    @click="onClick"
  >
    <slot />
  </component>
</template>