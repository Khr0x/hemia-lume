# Alert

Un componente de alerta versatile y flexible con múltiples variantes y estilos. Implementa el patrón de diseño de shadcn/ui utilizando class-variance-authority para manejar variantes de manera declarativa.

## Instalación

```bash
bunx --bun hemia-lume@latest add alert
```

## Uso Básico

```vue
<script setup lang="ts">
import { Alert, AlertTitle, AlertDescription } from '@/components/ui/alert'
</script>

<template>
  <Alert>
    <AlertTitle>Alert Title</AlertTitle>
    <AlertDescription>
      This is the alert description with important information.
    </AlertDescription>
  </Alert>
</template>
```

## Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `variant` | `'default' \| 'destructive' \| 'tonal' \| 'success' \| 'warning' \| 'info'` | `'default'` | Variante visual de la alerta |
| `class` | `string` | `''` | Clases CSS adicionales |

## Slots

| Slot | Descripción |
|------|-------------|
| `default` | Contenido de la alerta (título, descripción, icono, acciones) |

## Sub-componentes

### AlertTitle

Título de la alerta. Se recomienda usar dentro de `<Alert>`.

```vue
<Alert>
  <AlertTitle>Title</AlertTitle>
</Alert>
```

### AlertDescription

Descripción de la alerta. Puede contener texto y enlaces.

```vue
<Alert>
  <AlertDescription>
    This is the description with a <a href="#">link</a>.
  </AlertDescription>
</Alert>
```

### AlertAction

Contenedor para botones de acción dentro de la alerta.

```vue
<Alert>
  <AlertTitle>Title</AlertTitle>
  <AlertDescription>Description</AlertDescription>
  <AlertAction>
    <Button>Action</Button>
  </AlertAction>
</Alert>
```

## Variantes

### Default

La alerta predeterminada con borde sutil y fondo claro.

```vue
<Alert>
  <AlertTitle>Default Alert</AlertTitle>
  <AlertDescription>
    This is the default alert style.
  </AlertDescription>
</Alert>
```

### Destructive

Para errores y acciones destructivas. Color rojo.

```vue
<Alert variant="destructive">
  <AlertTitle>Error</AlertTitle>
  <AlertDescription>
    Something went wrong. Please try again.
  </AlertDescription>
</Alert>
```

### Tonal

Alerta con fondo sutil y texto en rojo. Sin borde visible.

```vue
<Alert variant="tonal">
  <AlertTitle>Tonal Alert</AlertTitle>
  <AlertDescription>
    A tonal alert with subtle background.
  </AlertDescription>
</Alert>
```

### Success

Para mensajes de éxito. Fondo verde esmeralda.

```vue
<Alert variant="success">
  <AlertTitle>Success</AlertTitle>
  <AlertDescription>
    Your changes have been saved successfully.
  </AlertDescription>
</Alert>
```

### Warning

Para advertencias. Fondo ámbar.

```vue
<Alert variant="warning">
  <AlertTitle>Warning</AlertTitle>
  <AlertDescription>
    Please review before proceeding.
  </AlertDescription>
</Alert>
```

### Info

Para información general. Fondo azul.

```vue
<Alert variant="info">
  <AlertTitle>Info</AlertTitle>
  <AlertDescription>
    Here's some additional information.
  </AlertDescription>
</Alert>
```

## Ejemplos Completos

### Con icono

```vue
<script setup lang="ts">
import { Alert, AlertTitle, AlertDescription } from '@/components/ui/alert'
</script>

<template>
  <Alert>
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <circle cx="12" cy="12" r="10"/>
      <line x1="12" x2="12" y1="8" y2="12"/>
      <line x1="12" x2="12.01" y1="16" y2="16"/>
    </svg>
    <AlertTitle>Info Alert</AlertTitle>
    <AlertDescription>
      This is an informational alert with an icon.
    </AlertDescription>
  </Alert>
</template>
```

### Con acciones

```vue
<script setup lang="ts">
import { Alert, AlertTitle, AlertDescription, AlertAction, Button } from '@/components/ui/alert'
</script>

<template>
  <Alert>
    <AlertTitle>Update Available</AlertTitle>
    <AlertDescription>
      A new version is ready to install.
    </AlertDescription>
    <AlertAction>
      <Button>Update Now</Button>
    </AlertAction>
  </Alert>
</template>
```

### Con icono y acciones

```vue
<script setup lang="ts">
import { Alert, AlertTitle, AlertDescription, AlertAction, Button } from '@/components/ui/alert'
</script>

<template>
  <Alert variant="success">
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
      <polyline points="22 4 12 14.01 9 11.01"/>
    </svg>
    <AlertTitle>Changes saved</AlertTitle>
    <AlertDescription>
      Your preferences have been updated successfully.
    </AlertDescription>
    <AlertAction>
      <Button variant="ghost">View details</Button>
    </AlertAction>
  </Alert>
</template>
```

### Con enlace

```vue
<script setup lang="ts">
import { Alert, AlertTitle, AlertDescription } from '@/components/ui/alert'
</script>

<template>
  <Alert>
    <AlertTitle>New message</AlertTitle>
    <AlertDescription>
      You have a new message from
      <a href="#" class="font-medium text-primary hover:underline">
        john@example.com
      </a>
    </AlertDescription>
  </Alert>
</template>
```

## Comportamiento en Dark Mode

Todas las variantes están optimizadas para funcionar correctamente en modo oscuro:

- **default**: fondo `muted/50` con borde
- **destructive**: fondo `destructive/10` en light, `destructive/20` en dark
- **tonal**: fondo `destructive/30` en dark para mayor contraste
- **success**: fondo `emerald-500/30` en dark
- **warning**: fondo `amber-500/30` en dark
- **info**: fondo `blue-500/30` en dark

## Accesibilidad

- El componente usa el rol `role="alert"` para lectores de pantalla
- Compatible con navegación por teclado
- El icono se posiciona automáticamente a la izquierda del contenido

## Notas técnicas

- Utiliza `class-variance-authority` (CVA) para gestión de variantes
- Implementa el helper `cn()` de `@hemia/lume-vue` para combinar clases
- El icono se posiciona automáticamente usando selectores CSS avanzados
- Soporte para Theming mediante tokens CSS custom properties
