<script setup lang="ts">
import { cva } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const fieldLegendVariants = cva("text-sm font-medium leading-none")

const props = defineProps<{
  class?: string
}>()
</script>

<template>
  <legend :class="cn(fieldLegendVariants(), props.class)">
    <slot />
  </legend>
</template>