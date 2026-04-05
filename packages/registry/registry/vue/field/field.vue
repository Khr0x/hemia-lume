<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const fieldVariants = cva("grid gap-1.5 rounded-lg", {
  variants: {
    orientation: {
      horizontal: "grid-cols-[1fr,auto]",
      vertical: "",
    },
  },
  defaultVariants: {
    orientation: "vertical",
  },
})

type FieldVariants = VariantProps<typeof fieldVariants>

const props = defineProps<{
  orientation?: FieldVariants["orientation"]
  class?: string
}>()
</script>

<template>
  <div :class="cn(fieldVariants({ orientation }), props.class)">
    <slot />
  </div>
</template>