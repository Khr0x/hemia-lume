<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const iconVariants = cva(
  "inline-flex shrink-0 items-center justify-center",
  {
    variants: {
      size: {
        default: "size-4",
        sm: "size-3",
        lg: "size-5",
        xl: "size-6",
      },
    },
    defaultVariants: {
      size: "default",
    },
  }
)

type IconVariants = VariantProps<typeof iconVariants>

// Export for external use
defineExpose({ iconVariants, IconVariants })

defineProps<{
  size?: IconVariants["size"]
  class?: string
}>()
</script>

<template>
  <span :class="cn(iconVariants({ size }), props.class)">
    <slot />
  </span>
</template>