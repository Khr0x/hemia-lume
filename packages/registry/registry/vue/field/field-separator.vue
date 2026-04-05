<script setup lang="ts">
import { cva } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const fieldSeparatorVariants = cva("h-px bg-border")

const props = defineProps<{
  class?: string
}>()
</script>

<template>
  <div :class="cn(fieldSeparatorVariants(), props.class)" />
</template>