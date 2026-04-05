# Field

Un sistema completo de componentes para construir formularios accesibles y bien estructurados. Proporciona etiquetas, descripciones, grupos y separadores con soporte completo para Theming y accesibilidad.

## Instalación

```bash
bunx --bun hemia-lume@latest add field
```

El componente Field incluye 7 subcomponentes:
- Field
- FieldLabel
- FieldDescription
- FieldGroup
- FieldLegend
- FieldSeparator
- FieldSet

## Uso Básico

```vue
<script setup lang="ts">
import { Field, FieldLabel, FieldDescription, FieldGroup } from '@/components/ui/field'
</script>

<template>
  <Field>
    <FieldLabel>Email</FieldLabel>
    <FieldGroup>
      <input type="email" placeholder="you@example.com" />
    </FieldGroup>
    <FieldDescription>We'll never share your email.</FieldDescription>
  </Field>
</template>
```

---

## Field

El componente contenedor principal que agrupa todos los elementos de un campo de formulario.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `orientation` | `'horizontal' \| 'vertical'` | `'vertical'` | Orientación del layout |
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<template>
  <!-- Vertical (default) -->
  <Field>
    <FieldLabel>Name</FieldLabel>
    <FieldGroup><input /></FieldGroup>
  </Field>
  
  <!-- Horizontal -->
  <Field orientation="horizontal">
    <FieldLabel>Email</FieldLabel>
    <FieldGroup><input /></FieldGroup>
  </Field>
</template>
```

---

## FieldLabel

Etiqueta asociable a un input. Implementa el patrón de accesibilidad correcto vinculándose mediante el atributo `for`.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `for` | `string` | `undefined` | ID del input asociado |
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<script setup lang="ts">
const usernameId = 'username-input'
</script>

<template>
  <FieldLabel :for="usernameId">Username</FieldLabel>
  <FieldGroup>
    <input :id="usernameId" type="text" />
  </FieldGroup>
</template>
```

### Notas

- Usa `<label>` semántico de HTML
- Aplicar estilos de `peer` para estados de disabled
- Soporta estados de focus via CSS peer selectors

---

## FieldDescription

Proporciona texto de ayuda adicional para el usuario. Usado para instrucciones, hints, o información complementaria.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<template>
  <Field>
    <FieldLabel>Password</FieldLabel>
    <FieldGroup>
      <input type="password" />
    </FieldGroup>
    <FieldDescription>
      Must be at least 8 characters long.
    </FieldDescription>
  </Field>
</template>
```

### Notas

- Estilo visual: texto más pequeño y color muted
- Posicionado después del input dentro del container
- No visible cuando hay un error (ver TextField)

---

## FieldGroup

Contenedor especial que agrupa el input con iconos opcionales. Proporciona estados visuales automáticos cuando el input interno tiene focus.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `class` | `string` | `''` | Clases CSS adicionales |

### Características

- **Focus automático**: Aplica estilos de ring cuando cualquier input hijo tiene focus
- **Soporte para iconos**: Ideal para envolver inputs con iconos prepend/append
- **Transiciones suaves**: Estados de focus con transiciones animadas

### Ejemplo

```vue
<script setup lang="ts">
import { FieldGroup } from '@/components/ui/field'
import { Icon } from '@/components/ui/icon'
import { Mail, Search } from 'lucide-vue-next'
</script>

<template>
  <FieldGroup>
    <Icon><Mail :size="16" /></Icon>
    <input type="email" placeholder="Email" />
    <Icon><Search :size="16" /></Icon>
  </FieldGroup>
</template>
```

### Estados visuales

- **Default**: Sin estilos adicionales
- **Focus**: Aplica border-ring, ring-3 ring-ring/50
- **Disabled**: Hereda el estado del input interno

---

## FieldLegend

Título para grupos de campos usando `<fieldset>`. Semánticamente correcto para agrupar campos relacionados.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<script setup lang="ts">
import { FieldSet, FieldLegend, FieldGroup } from '@/components/ui/field'
</script>

<template>
  <FieldSet>
    <FieldLegend>Personal Information</FieldLegend>
    <FieldGroup>
      <input placeholder="First name" />
      <input placeholder="Last name" />
    </FieldGroup>
  </FieldSet>
</template>
```

### Notas

- Usa elemento `<legend>` de HTML semántico
- Similar estilísticamente a FieldLabel
- Usado principalmente con FieldSet

---

## FieldSeparator

Línea divisora visual entre secciones de formulario. Útil para separar grupos de campos lógicos.

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<template>
  <Field>
    <FieldLabel>Section 1</FieldLabel>
    <FieldGroup><input /></FieldGroup>
  </Field>
  
  <FieldSeparator class="my-4" />
  
  <Field>
    <FieldLabel>Section 2</FieldLabel>
    <FieldGroup><input /></FieldGroup>
  </Field>
</template>
```

### Notas

- Color basado en token `border`
- Altura de 1px (h-px)
- Totalmente personalizable via class prop

---

## FieldSet

Wrapper semántico que usa el elemento `<fieldset>` de HTML. Ideal para agrupar campos relacionados con un título (FieldLegend).

### Props

| Prop | Tipo | Default | Descripción |
|------|------|---------|-------------|
| `class` | `string` | `''` | Clases CSS adicionales |

### Ejemplo

```vue
<script setup lang="ts">
import { FieldSet, FieldLegend, FieldLabel, FieldGroup, FieldDescription } from '@/components/ui/field'
</script>

<template>
  <FieldSet>
    <FieldLegend>Contact Details</FieldLegend>
    
    <Field>
      <FieldLabel for="email">Email</FieldLabel>
      <FieldGroup>
        <input id="email" type="email" />
      </FieldGroup>
      <FieldDescription>We'll send confirmation here</FieldDescription>
    </Field>
    
    <Field>
      <FieldLabel for="phone">Phone</FieldLabel>
      <FieldGroup>
        <input id="phone" type="tel" />
      </FieldGroup>
    </Field>
  </FieldSet>
</template>
```

### Props de accesibilidad

- El elemento `<fieldset>` provee grouping semántico para lectores de pantalla
- Compatible con navegacion por teclado
- Soporta todos los atributos estándar de fieldset

---

## Ejemplo Completo: Formulario de Registro

```vue
<script setup lang="ts">
import { 
  Field, 
  FieldLabel, 
  FieldDescription, 
  FieldGroup,
  FieldSeparator,
  FieldSet,
  FieldLegend
} from '@/components/ui/field'
import { TextField } from '@/components/ui/textfield'
import { Button } from '@/components/ui/button'
</script>

<template>
  <form class="space-y-6 max-w-md">
    <FieldSet>
      <FieldLegend>Account Information</FieldLegend>
      
      <Field>
        <TextField 
          label="Username" 
          for="username"
          placeholder="Choose a username"
        />
      </Field>
      
      <Field>
        <TextField 
          label="Email" 
          for="email"
          type="email"
          placeholder="you@example.com"
        />
      </Field>
    </FieldSet>
    
    <FieldSeparator />
    
    <FieldSet>
      <FieldLegend>Preferences</FieldLegend>
      
      <Field orientation="horizontal">
        <FieldLabel for="newsletter">
          Subscribe to newsletter
        </FieldLabel>
        <FieldGroup>
          <input id="newsletter" type="checkbox" />
        </FieldGroup>
      </Field>
    </FieldSet>
    
    <Button type="submit">Create Account</Button>
  </form>
</template>
```

---

## Notas Técnicas

- Todos los componentes usan `class-variance-authority` para management de variantes
- Implementan el helper `cn()` de `@hemia/lume-vue`
- Soportan theming completo via CSS custom properties
- Transiciones suaves en todos los estados interactivos
- Diseño responsive que funciona en todos los tamaños de pantalla