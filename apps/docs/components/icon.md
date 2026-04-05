# Icon

Un wrapper componente para renderizar iconos de forma consistente. Proporciona tamaños predefinidos, alineación automática, y soporte completo para theming. Ideal para usar con librerías de iconos como Lucide, Heroicons, o cualquier otra.

## Instalación

```bash
bunx --bun hemia-lume@latest add icon
```

## Uso Básico

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Loader2 } from 'lucide-vue-next'
</script>

<template>
  <Icon>
    <Loader2 :size="16" />
  </Icon>
</template>
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `size` | `'default' \| 'sm' \| 'lg' \| 'xl'` | `'default'` | Tamaño predefinido del icono |
| `class` | `string` | `''` | Clases CSS adicionales |

## Slots

| Slot | Descripción |
|------|-------------|
| `default` | El contenido del icono (componente de librería de iconos) |

## Tamaños

| Tamaño | Dimensión | Uso recomendado |
|--------|-----------|-----------------|
| `sm` | 12px (size-3) | Texto pequeño, badges |
| `default` | 16px (size-4) | General, botones |
| `lg` | 20px (size-5) | Headers, títulos |
| `xl` | 24px (size-6) | Íconos principales |

---

## Ejemplos

### Con Lucide

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { 
  ArrowRight, 
  Check, 
  AlertCircle,
  Loader2,
  Search 
} from 'lucide-vue-next'
</script>

<template>
  <div class="flex gap-4">
    <Icon><ArrowRight :size="20" /></Icon>
    <Icon size="sm"><Check :size="12" /></Icon>
    <Icon size="lg"><AlertCircle :size="20" /></Icon>
    <Icon class="animate-spin"><Loader2 :size="16" /></Icon>
  </div>
</template>
```

### En botones

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Plus, Download, Send } from 'lucide-vue-next'
</script>

<template>
  <div class="flex gap-2">
    <Button>
      <Icon :size="16" class="mr-2" />
      Add Item
    </Button>
    
    <Button variant="outline">
      <Icon :size="16" class="mr-2" />
      Download
    </Button>
    
    <Button variant="ghost" size="icon">
      <Icon :size="18">
        <Search />
      </Icon>
    </Button>
  </div>
</template>
```

### Con colores custom

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Heart, Star, Zap } from 'lucide-vue-next'
</script>

<template>
  <div class="flex gap-4">
    <Icon class="text-red-500">
      <Heart :size="24" />
    </Icon>
    
    <Icon class="text-yellow-500">
      <Star :size="24" />
    </Icon>
    
    <Icon class="text-blue-500">
      <Zap :size="24" />
    </Icon>
  </div>
</template>
```

### Animaciones

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { Loader2, RefreshCw, Loader } from 'lucide-vue-next'
</script>

<template>
  <div class="flex gap-4 items-center">
    <!-- Spinning -->
    <Icon class="animate-spin">
      <Loader2 :size="20" />
    </Icon>
    
    <!-- Counter-clockwise spin -->
    <Icon class="animate-spin [animation-direction:reverse]">
      <RefreshCw :size="20" />
    </Icon>
    
    <!-- Pulsing -->
    <Icon class="animate-pulse">
      <Loader :size="20" />
    </Icon>
  </div>
</template>
```

---

## Uso con otras librerías de iconos

### Heroicons

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
</script>

<template>
  <Icon>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
      <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25zm-2.625 6c-.54 0-.828.419-.936.634a6.953 6.953 0 00-.189 1.707c0 .895.392 1.73 1.05 2.305.322.283.483.597.483.928 0 .165-.055.276-.14.352-.12.108-.315.19-.54.19-.35 0-.562-.198-.932-.634-.372-.367-.622-.89-.622-1.413 0-.865.385-1.73 1.05-2.304.322-.282.483-.596.483-.927 0-.165-.055-.276-.14-.352-.12-.108-.315-.19-.54-.19z" clip-rule="evenodd" />
    </svg>
  </Icon>
</template>
```

### Iconify (como componente)

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
</script>

<template>
  <Icon>
    <iconify-icon icon="mdi:account" />
  </Icon>
</template>
```

---

## Casos de uso comunes

### Indicador de loading

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Loader2 } from 'lucide-vue-next'

defineProps<{
  loading?: boolean
}>()
</script>

<template>
  <Button :disabled="loading">
    <Icon v-if="loading" class="animate-spin mr-2">
      <Loader2 :size="16" />
    </Icon>
    {{ loading ? 'Saving...' : 'Save' }}
  </Button>
</template>
```

### Icono de estado

```vue
<script setup lang="ts">
import { Icon } from '@/components/ui/icon'
import { CheckCircle, XCircle, AlertCircle } from 'lucide-vue-next'

defineProps<{
  status: 'success' | 'error' | 'warning'
}>()
</script>

<template>
  <Icon 
    v-if="status === 'success'" 
    class="text-green-500"
  >
    <CheckCircle :size="20" />
  </Icon>
  
  <Icon 
    v-else-if="status === 'error'" 
    class="text-red-500"
  >
    <XCircle :size="20" />
  </Icon>
  
  <Icon 
    v-else 
    class="text-yellow-500"
  >
    <AlertCircle :size="20" />
  </Icon>
</template>
```

### Toolbar con iconos

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Bold, Italic, Underline, AlignLeft } from 'lucide-vue-next'
</script>

<template>
  <div class="flex gap-1 border rounded-md p-1">
    <Button size="icon" variant="ghost">
      <Icon :size="18"><Bold /></Icon>
    </Button>
    <Button size="icon" variant="ghost">
      <Icon :size="18"><Italic /></Icon>
    </Button>
    <Button size="icon" variant="ghost">
      <Icon :size="18"><Underline /></Icon>
    </Button>
    <div class="w-px bg-border mx-1" />
    <Button size="icon" variant="ghost">
      <Icon :size="18"><AlignLeft /></Icon>
    </Button>
  </div>
</template>
```

---

## Notas Técnicas

- **Wrapper genérico**: Funciona con cualquier librería de iconos o SVG inline
- **Slots**: Usa slot default para inyectar el contenido del icono
- **Inline-flex**: El componente usa `inline-flex` para mantener el flujo del documento
- **Shrink-0**: Evita que el icono se encoja en contextos flex
- **Class merging**: Soporta merge de clases via `cn()` helper
- **Exports**: Expone `iconVariants` y `IconVariants` para uso externo si necesitas acceder a los types