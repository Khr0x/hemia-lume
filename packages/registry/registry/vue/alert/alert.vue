<!-- eslint-disable vue/no-parsing-error -->
<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const alertVariants = cva(
  "relative w-full rounded-lg border p-4 [&>svg~*]:pl-7 [&>svg+div]:translate-y-[-3px] [&>svg]:absolute [&>svg]:left-4 [&>svg]:top-4 [&>svg]:text-lume-foreground",
  {
    variants: {
      variant: {
        default: "bg-lume-muted/50 text-lume-foreground border-lume-border",
        destructive:
          "border-lume-destructive/50 text-lume-destructive dark:border-lume-destructive [&>svg]:text-lume-destructive bg-lume-destructive/10 dark:bg-lume-destructive/20",
        tonal:
          "border-transparent bg-lume-destructive/10 text-lume-destructive dark:bg-lume-destructive/30 dark:text-lume-destructive-200",
        success:
          "bg-green-50 border-green-200/50 text-green-800 dark:bg-green-900/30 dark:text-green-200 dark:border-green-800/50",
        warning:
          "bg-amber-50 border-amber-200/50 text-amber-800 dark:bg-amber-900/30 dark:text-amber-200 dark:border-amber-800/50",
        info:
          "bg-blue-50 border-blue-200/50 text-blue-800 dark:bg-blue-900/30 dark:text-blue-200 dark:border-blue-800/50",
      },
    },
    defaultVariants: {
      variant: "default",
    },
  }
)

type AlertVariants = VariantProps<typeof alertVariants>

const props = defineProps<{
  variant?: AlertVariants["variant"]
  class?: string
}>()
</script>

<template>
  <div :class="cn(alertVariants({ variant }), props.class)" role="alert">
    <slot />
  </div>
</template>