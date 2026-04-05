---
layout: home

hero:
  name: "@hemia/lume"
  text: "A shadcn-inspired, multi-framework UI system"
  tagline: Local-first. CLI-driven. Themeable.
  actions:
    - theme: brand
      text: Get Started
      link: /guide/introduction
    - theme: alt
      text: View Components
      link: /components/button

features:
  - title: Local-First
    details: Components are copied directly into your project. No runtime dependencies, full control over your code.
  - title: Multi-Framework
    details: Support for Vue, React, Svelte, and Astro. One registry, multiple frameworks.
  - title: CLI-Driven
    details: Add components with a single command. `hemia-lume add button` - it's that simple.
  - title: Themeable
    details: CSS custom properties for complete theming control. Light and dark mode out of the box.
  - title: Accessible
    details: Built with accessibility in mind. ARIA patterns, keyboard navigation, screen reader support.
  - title: TypeScript
    details: Full TypeScript support with auto-generated types. IntelliSense included.

---

## Quick Start

```bash
# Install the CLI
pnpm add -D hemia-lume

# Add a component
bunx --bun hemia-lume add button
```

That's it! The component is copied to your project and ready to use.

---

## Why Lume?

| Feature | Traditional Libraries | Lume |
|---------|----------------------|------|
| Bundle size | Full library import | Zero runtime |
| Customization | Override via CSS | Full source access |
| Updates | npm update | Copy new version |
| Debugging | Minified code | Your local code |
| Theming | Limited tokens | Full CSS control |