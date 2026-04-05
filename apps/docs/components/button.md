# Button

Un componente de botón flexible y versátil con múltiples variantes y tamaños. Implementa el patrón de diseño de shadcn/ui utilizando class-variance-authority para manejar variantes de manera declarativa.

## Instalación

```bash
bunx --bun hemia-lume@latest add button
```

## Uso Básico

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
  <Button>Click me</Button>
</template>
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `variant` | `'default' \| 'destructive' \| 'outline' \| 'secondary' \| 'ghost' \| 'link'` | `'default'` | Variante visual del botón |
| `size` | `'default' \| 'xs' \| 'sm' \| 'lg' \| 'icon' \| 'icon-xs' \| 'icon-sm' \| 'icon-lg'` | `'default'` | Tamaño del botón |
| `type` | `'button' \| 'submit' \| 'reset'` | `'button'` | Tipo de botón HTML |
| `class` | `string` | `''` | Clases CSS adicionales |

## Slots

| Slot | Descripción |
|------|-------------|
| `default` | Contenido del botón (texto, iconos, etc.) |

## Variantes

### Default

El botón primario predeterminado. Usa el color `primary` del tema.

```vue
<Button variant="default">Primary</Button>
```

### Destructive

Para acciones destructivas o peligrosas como eliminar, cancelar, etc. Color rojo.

```vue
<Button variant="destructive">Delete</Button>
```

### Outline

Borde visible con fondo transparente. Ideal para acciones secundarias.

```vue
<Button variant="outline">Cancel</Button>
```

### Secondary

Para acciones de menor jerarquía. Color secundario del tema.

```vue
<Button variant="secondary">Secondary</Button>
```

### Ghost

Sin fondo visible, solo aparece en hover. Para barras de herramientas.

```vue
<Button variant="ghost">Ghost</Button>
```

### Link

Estilo de enlace texto. Sin fondo, con subrayado en hover.

```vue
<Button variant="link">Link Button</Button>
```

## Tamaños

### Tamaños de contenido

| Tamaño | Altura | Padding | Uso recomendado |
|--------|--------|---------|-----------------|
| `xs` | 28px (h-7) | px-2 | Botones compactos |
| `sm` | 32px (h-8) | px-3 | Formularios |
| `default` | 36px (h-9) | px-4 | General |
| `lg` | 40px (h-10) | px-8 | CTAs principales |

### Tamaños de icono

| Tamaño | Dimensión | Uso recomendado |
|--------|-----------|-----------------|
| `icon-xs` | 28px (size-7) | Iconos muy pequeños |
| `icon-sm` | 32px (size-8) | Iconos pequeños |
| `icon` | 36px (size-9) | Iconos medianos |
| `icon-lg` | 40px (size-10) | Iconos grandes |

## Ejemplos Completos

### Con icono

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Loader2 } from 'lucide-vue-next'
</script>

<template>
  <Button>
    <Icon :size="16" class="mr-2" />
    Save
  </Button>
  
  <Button variant="outline">
    <Icon :size="16" class="mr-2" />
    Download
  </Button>
</template>
```

### Loading state

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Icon } from '@/components/ui/icon'
import { Loader2 } from 'lucide-vue-next'
</script>

<template>
  <Button disabled>
    <Icon class="animate-spin mr-2">
      <Loader2 :size="16" />
    </Icon>
    Loading...
  </Button>
</template>
```

### Grupo de botones

```vue
<script setup lang="ts">
import { Button } from '@/components/ui/button'
</script>

<template>
  <div class="flex gap-2">
    <Button size="sm">Previous</Button>
    <Button size="sm" variant="outline">1</Button>
    <Button size="sm" variant="outline">2</Button>
    <Button size="sm" variant="outline">3</Button>
    <Button size="sm">Next</Button>
  </div>
</template>
```

## Accesibilidad

- El componente usa el elemento nativo `<button>` de HTML
- Soporta todos los atributos nativos de botón (`disabled`, `type`, etc.)
- Los estilos de focus-visible aseguran visibilidad en navegación por teclado
- Compatible con lectores de pantalla

## Notas técnicas

- Utiliza `class-variance-authority` (CVA) para gestión de variantes
- Implementa el helper `cn()` de `@hemia/lume-vue` para combinar clases
- Soporte para Theming mediante tokens CSS custom properties
- Transiciones suaves en todos los estados (hover, focus, disabled)