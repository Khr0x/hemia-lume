<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority"
import { cn } from "@hemia/lume-vue"
import { Field, FieldLabel, FieldDescription, FieldGroup } from "../field/index"

const textfieldVariants = cva(
  "flex h-9 w-full min-w-0 rounded-lg border border-input bg-transparent px-2.5 py-1 text-base transition-colors outline-none file:inline-flex file:h-6 file:border-0 file:bg-transparent file:text-sm file:font-medium file:text-foreground placeholder:text-muted-foreground disabled:pointer-events-none disabled:cursor-not-allowed disabled:bg-input/50 disabled:opacity-50 focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-0 aria-invalid:border-destructive aria-invalid:ring-3 aria-invalid:ring-destructive/20 md:text-sm dark:bg-input/30 dark:disabled:bg-input/80 dark:aria-invalid:border-destructive/50 dark:aria-invalid:ring-destructive/40",
  {
    variants: {
      variant: {
        default: "",
        error: "bg-background border-destructive aria-invalid:border-destructive aria-invalid:ring-destructive/20 dark:aria-invalid:border-destructive/50 dark:aria-invalid:ring-destructive/40",
      },
      size: {
        default: "",
        sm: "h-8",
        lg: "h-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
)

const textfieldIconVariants = cva(
  "text-muted-foreground flex shrink-0 items-center",
  {
    variants: {
      size: {
        default: "size-4",
        sm: "size-3.5",
        lg: "size-5",
      },
    },
    defaultVariants: {
      size: "default",
    },
  }
)

type TextfieldVariants = VariantProps<typeof textfieldVariants>
type TextfieldIconVariants = VariantProps<typeof textfieldIconVariants>

const props = defineProps<{
  label?: string
  description?: string
  error?: string
  for?: string
  variant?: TextfieldVariants["variant"]
  size?: TextfieldVariants["size"]
  iconSize?: TextfieldIconVariants["size"]
  modelValue?: string
  type?: string
  placeholder?: string
  disabled?: boolean
  class?: string
  prependIcon?: any
  prependInnerIcon?: any
  appendInnerIcon?: any
  appendIcon?: any
}>()

const emit = defineEmits<{
  (e: "update:modelValue", value: string): void
}>()

function onInput(event: Event) {
  const target = event.target as HTMLInputElement
  emit("update:modelValue", target.value)
}

// Compute padding classes for input based on inner icon presence
const getInputPaddingClass = () => {
  const padding = []
  if (props.prependInnerIcon) {
    padding.push("ps-1.5")
  } else {
    padding.push("ps-[var(--tf-padding-x)]")
  }
  if (props.appendInnerIcon) {
    padding.push("pe-1.5")
  } else {
    padding.push("pe-[var(--tf-padding-x)]")
  }
  return padding.join(" ")
}
</script>

<template>
  <Field :class="props.class">
    <FieldLabel v-if="label" :for="for">{{ label }}</FieldLabel>
    <FieldGroup class="flex flex-1 items-center">
      <!-- Prepend icon (outside the textfield, to the left) -->
      <component
        v-if="prependIcon"
        :is="prependIcon"
        class="text-muted-foreground flex shrink-0 items-center"
        :class="iconSize === 'sm' ? 'size-3.5' : iconSize === 'lg' ? 'size-5' : 'size-4'"
      />
      <!-- Textfield inner container -->
      <div
        :class="cn(
          textfieldVariants({ variant: error ? 'error' : variant, size }),
          'flex flex-1 items-center focus-within:rounded-lg focus-within:ring-2 focus-within:ring-ring/50 dark:focus-within:[--ring:217.2_32.6%_50%] focus-within:[--ring:210_5%_80%]'
        )"
      >
        <!-- Prepend-inner icon (inside, at start) -->
        <component
          v-if="prependInnerIcon"
          :is="prependInnerIcon"
          class="text-muted-foreground flex shrink-0 items-center"
          :class="[
            iconSize === 'sm' ? 'size-3.5' : iconSize === 'lg' ? 'size-5' : 'size-4',
            'me-1.5'
          ]"
        />
        <input
          :id="for"
          :type="type"
          :value="modelValue"
          :placeholder="placeholder"
          :disabled="disabled"
          :aria-invalid="!!error"
          :class="cn(
            'flex-1 bg-transparent outline-none placeholder:text-muted-foreground disabled:pointer-events-none disabled:cursor-not-allowed disabled:opacity-50 w-full min-w-0',
            getInputPaddingClass()
          )"
          :style="{ '--tf-padding-x': '0.625rem' }"
          @input="onInput"
        />
        <!-- Append-inner icon (inside, at end) -->
        <component
          v-if="appendInnerIcon"
          :is="appendInnerIcon"
          class="text-muted-foreground flex shrink-0 items-center"
          :class="[
            iconSize === 'sm' ? 'size-3.5' : iconSize === 'lg' ? 'size-5' : 'size-4',
            'ms-1.5'
          ]"
        />
      </div>
      <!-- Append icon (outside the textfield, to the right) -->
      <component
        v-if="appendIcon"
        :is="appendIcon"
        class="text-muted-foreground flex shrink-0 items-center"
        :class="iconSize === 'sm' ? 'size-3.5' : iconSize === 'lg' ? 'size-5' : 'size-4'"
      />
    </FieldGroup>
    <FieldDescription v-if="description && !error">{{ description }}</FieldDescription>
    <p v-if="error" class="text-[0.8rem] font-medium text-destructive">
      {{ error }}
    </p>
  </Field>
</template>