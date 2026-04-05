<script setup lang="ts">
import { cva } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const fieldLabelVariants = cva(
  "text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
)

const props = defineProps<{
  forId?: string
  class?: string
}>()
</script>

<template>
  <label :for="forId" :class="cn(fieldLabelVariants(), props.class)">
    <slot />
  </label>
</template>