# TextField

Un componente de input de texto completo y flexible que incluye integración automática con el sistema Field. Soporta iconos internos y externos, validación de errores, múltiples tamaños y estados, todo con accesibilidad incluida.

## Instalación

```bash
bunx --bun hemia-lume@latest add textfield
```

## Uso Básico

```vue
<script setup lang="ts">
import { TextField } from '@/components/ui/textfield'
import { ref } from 'vue'

const value = ref('')
</script>

<template>
  <TextField 
    v-model="value"
    label="Username"
    placeholder="Enter your username"
  />
</template>
```

## Props

### Props principales

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `label` | `string` | `undefined` | Etiqueta del campo |
| `description` | `string` | `undefined` | Texto de ayuda |
| `error` | `string` | `undefined` | Mensaje de error |
| `for` | `string` | `undefined` | ID del input (para label) |
| `variant` | `'default' \| 'error'` | `'default'` | Variante visual |
| `size` | `'default' \| 'sm' \| 'lg'` | `'default'` | Tamaño del input |
| `modelValue` | `string` | `undefined` | Valor v-model |
| `type` | `string` | `'text'` | Tipo de input HTML |
| `placeholder` | `string` | `undefined` | Placeholder del input |
| `disabled` | `boolean` | `false` | Estado deshabilitado |
| `class` | `string` | `''` | Clases CSS adicionales |

### Props de iconos

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `prependIcon` | `any` | `undefined` | Icono externo antes del input |
| `prependInnerIcon` | `any` | `undefined` | Icono interno antes del input |
| `appendInnerIcon` | `any` | `undefined` | Icono interno después del input |
| `appendIcon` | `any` | `undefined` | Icono externo después del input |
| `iconSize` | `'default' \| 'sm' \| 'lg'` | `'default'` | Tamaño de los iconos |

## Eventos

| Evento | Payload | Descripción |
|--------|---------|-------------|
| `update:modelValue` | `string` | Emitido cuando el valor cambia |

## Slots

No hay slots directos; el componente usa composición interna con componentes Field.

## Variantes

### Default

Input estándar con borde normal.

```vue
<TextField 
  label="Email"
  placeholder="you@example.com"
/>
```

### Error

Input con estilos de error. Muestra el mensaje de error proporcionado.

```vue
<script setup lang="ts">
const errorMessage = 'Invalid email format'
</script>

<template>
  <TextField 
    label="Email"
    modelValue="invalid-email"
    error="Invalid email format"
  />
</template>
```

El componente automáticamente:
- Aplica border destructive
- Aplica ring destructive
- Muestra el mensaje de error en color rojo
- Oculta la descripción (si existe)

---

## Tamaños

| Tamaño | Altura | Uso recomendado |
|--------|--------|-----------------|
| `sm` | 32px (h-8) | Formularios compactos |
| `default` | 36px (h-9) | General |
| `lg` | 40px (h-10) | CTAs, formularios importantes |

---

## Iconos

El TextField soporta 4 posiciones de iconos:

### Prepend Icon (externo, izquierda)

Icono fuera del border del input, a la izquierda.

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Mail } from 'lucide-vue-next'
</script>

<template>
  <TextField 
    label="Email"
    placeholder="you@example.com"
    :prependIcon="h(Icon, null, { default: () => h(Mail) })"
  />
</template>
```

### Prepend Inner Icon (interno, izquierda)

Icono dentro del border del input, a la izquierda (entre label e input).

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Search } from 'lucide-vue-next'
</script>

<template>
  <TextField 
    placeholder="Search..."
    :prependInnerIcon="h(Icon, null, { default: () => h(Search) })"
  />
</template>
```

### Append Inner Icon (interno, derecha)

Icono dentro del border del input, a la derecha (derecha del input, antes del cierre).

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Eye } from 'lucide-vue-next'
</script>

<template>
  <TextField 
    type="password"
    placeholder="Password"
    :appendInnerIcon="h(Icon, null, { default: () => h(Eye) })"
  />
</template>
```

### Append Icon (externo, derecha)

Icono fuera del border del input, a la derecha.

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { ArrowRight } from 'lucide-vue-next'
</script>

<template>
  <TextField 
    placeholder="Search"
    :appendIcon="h(Icon, null, { default: () => h(ArrowRight) })"
  />
</template>
```

---

## Ejemplos Completos

### Formulario de login

```vue
<script setup lang="ts">
import { TextField } from '@/components/ui/textfield'
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Mail, Lock, ArrowRight } from 'lucide-vue-next'
import { h } from 'vue'

const email = ref('')
const password = ref('')

function handleLogin() {
  // Login logic
}
</script>

<template>
  <form @submit.prevent="handleLogin" class="space-y-4 max-w-sm">
    <TextField
      v-model="email"
      label="Email"
      type="email"
      for="login-email"
      placeholder="you@example.com"
      description="We'll never share your email."
      :prependInnerIcon="h(Icon, { size: 'sm' }, () => h(Mail))"
    />
    
    <TextField
      v-model="password"
      label="Password"
      type="password"
      for="login-password"
      placeholder="••••••••"
      :prependInnerIcon="h(Icon, { size: 'sm' }, () => h(Lock))"
    />
    
    <Button type="submit" class="w-full">
      Sign In
      <Icon :size="16" class="ml-2">
        <ArrowRight />
      </Icon>
    </Button>
  </form>
</template>
```

### Con validación de error

```vue
<script setup lang="ts">
import { TextField } from '@/components/ui/textfield'

const email = ref('invalid-email')
const error = ref('')

function validate() {
  if (!email.value.includes('@')) {
    error.value = 'Please enter a valid email'
  } else {
    error.value = ''
  }
}
</script>

<template>
  <TextField
    v-model="email"
    label="Email"
    type="email"
    placeholder="you@example.com"
    :error="error"
    @update:modelValue="validate"
  />
</template>
```

### Search input con iconos

```vue
<script setup lang="ts">
import { TextField } from '@/components/ui/textfield'
import { Icon } from '@/components/ui/icon'
import { Search, X } from 'lucide-vue-next'
import { ref } from 'vue'

const search = ref('')

function clear() {
  search.value = ''
}
</script>

<template>
  <TextField
    v-model="search"
    placeholder="Search..."
    :prependInnerIcon="h(Icon, null, () => h(Search))"
    :appendIcon="search ? h(Icon, { size: 'sm', class: 'cursor-pointer' }, () => h(X)) : null"
  />
</template>
```

### Input con diferentes tamaños

```vue
<template>
  <div class="space-y-4">
    <TextField 
      size="sm" 
      placeholder="Small input" 
    />
    <TextField 
      size="default" 
      placeholder="Default input" 
    />
    <TextField 
      size="lg" 
      placeholder="Large input" 
    />
  </div>
</template>
```

---

## Accesibilidad

- **Label asociable**: Usa el atributo `for` para vincular con el input
- **ARIA invalid**: Aplica `aria-invalid="true"` cuando hay error
- **Descripción accesible**: FieldDescription proving información adicional
- **Keyboard navigation**: Soporte completo para navegación por teclado
- **Screen readers**: Compatible con lectores de pantalla

---

## Notas Técnicas

- **Composición**: Usa internamente los componentes Field, FieldLabel, FieldDescription, y FieldGroup
- **v-model**: Soporta v-model nativamente con `update:modelValue`
- **Iconos dinámicos**: Usa `h()` de Vue para renderizar componentes de iconos
- **Padding dinámico**: Calcula el padding del input basado en la presencia de iconos internos
- **Theming**: Soporta modo oscuro automáticamente
- **Transiciones**: Estados de focus con transiciones suaves