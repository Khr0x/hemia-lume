<script setup lang="ts">
import { cn } from '@hemia/lume-vue'
import { ref, provide } from 'vue'

const open = ref(false)

function onOpenChange(value: boolean) {
  open.value = value
}

provide('alert-dialog', {
  open,
  onOpenChange,
})

const props = defineProps<{
  class?: string
}>()
</script>

<template>
  <div :class="cn(props.class)">
    <slot :open="open" :on-open-change="onOpenChange" />
  </div>
</template>