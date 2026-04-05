<!-- eslint-disable vue/no-parsing-error -->
<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"

const alertVariants = cva(
  "relative w-full rounded-lg border p-4 [&>svg~*]:pl-7 [&>svg+div]:translate-y-[-3px] [&>svg]:absolute [&>svg]:left-4 [&>svg]:top-4 [&>svg]:text-foreground",
  {
    variants: {
      variant: {
        default: "bg-muted/50 text-foreground border-border",
        destructive:
          "border-destructive/50 text-destructive dark:border-destructive [&>svg]:text-destructive bg-destructive/10 dark:bg-destructive/20",
        tonal:
          "border-transparent bg-destructive/10 text-destructive dark:bg-destructive/30 dark:text-destructive-200",
        success:
          "border-transparent bg-emerald-500/10 text-emerald-700 dark:text-emerald-200 dark:bg-emerald-500/30",
        warning:
          "border-transparent bg-amber-500/10 text-amber-700 dark:text-amber-200 dark:bg-amber-500/30",
        info:
          "border-transparent bg-blue-500/10 text-blue-700 dark:text-blue-200 dark:bg-blue-500/30",
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