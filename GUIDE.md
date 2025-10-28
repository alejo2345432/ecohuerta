## 🌻 Resumen y Explicación del Código Base EcoHuerta (Tailwind CSS v4)

El código demuestra la implementación de una web "utility-first" usando **Tailwind CSS v4** a través del Play CDN, permitiendo la definición de temas y componentes directamente en el CSS embebido.

---

### 0) Configuración Base (Play CDN + CSS Embebido)

| Concepto                 | Directiva/Clave                                   | Explicación Ampliada                                                                                                                                                                                                                      |
| :----------------------- | :------------------------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Play CDN**             | `<script src="...">`                              | Carga Tailwind v4 directamente en el navegador sin paso de _build_, ideal para prototipos.                                                                                                                                                |
| **CSS Completo (v4)**    | `<style type="text/tailwindcss">`                 | Permite escribir **CSS "completo"** incluyendo directivas avanzadas de Tailwind (`@theme`, `@layer`) dentro del HTML.                                                                                                                     |
| **Tokens de Diseño**     | `@theme { ... }`                                  | Define **variables de diseño** (colores OKLCH para buen contraste, fuentes, y el breakpoint `3xl`) que automáticamente generan utilidades como `bg-eco-600` y `text-eco-200`. _En v4, esto sustituye a `tailwind.config.js` para tokens._ |
| **Dark Mode por Clase**  | `@custom-variant dark (&:where(.dark, .dark *));` | Crea el modificador `dark:` para que responda a la clase **`.dark`** en la etiqueta `<html>`, en lugar de solo la preferencia del sistema. Esto habilita el _toggle_ manual vía JavaScript.                                               |
| **Clases Reutilizables** | `@layer components { .btn, .card, ... }`          | Centraliza la definición de patrones UI comunes (botones, tarjetas) agrupando utilidades con **`@apply`**. Esto favorece la reutilización sin abandonar la filosofía _utility-first_.                                                     |

---

### 1) Estilo Global (`<body>`)

- **Tipografía y Colores:** `font-sans bg-surface text-ink dark:bg-surface dark:text-ink`. Los tokens de color se redefinen en la clase `.dark` (gracias a los valores OKLCH) para mantener un alto contraste visual en ambos temas.
- **Altura de Vista:** `min-h-dvh`. Utiliza la **Dynamic Viewport Height** (`dvh`) para una mejor compatibilidad y comportamiento en dispositivos móviles.
- **Selección:** `selection:bg-eco-200/60 selection:text-ink` personaliza el color de la selección de texto para mantener la coherencia de la marca.

---

### 2) Componentes Clave

#### 🧭 Header / Navbar (Sticky & Blur)

- **Fijación UX:** `header.sticky top-0 z-50` mantiene la navegación visible al hacer scroll.
- **Efecto:** `bg-surface/80 backdrop-blur` implementa un sutil efecto de "cristal esmerilado" o _glas-morphism_ que mejora la legibilidad sobre el contenido.
- **Toggle:** El botón activa/desactiva la clase `.dark` en `<html>` mediante JavaScript y sincroniza el estado ARIA (`aria-pressed`).

#### 🌿 Hero (Diseño Responsive)

- **Fondo:** `bg-gradient-to-b from-eco-50 to-surface dark:from-white/5 dark:to-surface`. Un gradiente suave de bajo contraste para delimitar la sección.
- **Layout:** `grid lg:grid-cols-2 gap-10 items-center`. Patrón responsive que apila en móvil y divide en dos columnas en `lg`.
- **Jerarquía Tipográfica:** El título combina clases de tamaño (`text-4xl sm:text-5xl`) y color de marca (`text-eco-700 dark:text-eco-200`) para énfasis.
- **CTAs:** Se usan los componentes definidos: `.btn-primary` (acción principal) y `.btn-secondary` (acción secundaria/contraste).

#### 🌱 Grid de Cultivos (`#crops`)

- **Estructura de Grid:** `grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 3xl:grid-cols-4 gap-6`. Demuestra la **escalabilidad progresiva** usando breakpoints, incluyendo el personalizado `--breakpoint-3xl`.
- **Tarjeta (`.card card-hover`):**
  - `.card`: Incluye efectos de capa como `shadow`, `backdrop-blur`, y un borde sutil (`ring-1 ring-black/5`).
  - `.card-hover`: `hover:shadow-lg hover:-translate-y-0.5` añade una micro-interacción de elevación.
- **Badges de Estado:** `.badge-seed`, `.badge-grow`, `.badge-harvest`. Usan colores semánticos (`bg-eco-100`, `bg-amber-100`, `bg-emerald-100`) para una rápida identificación visual del estado del cultivo.

#### 📝 Contacto y Suscripción

- **Inputs Estilizados:** `.input`. Estilo unificado para campos de formulario, destacando:
  - **Contraste Dark Mode:** `dark:bg-white/10 dark:placeholder:text-gray-400`.
  - **Accesibilidad (a11y):** `outline-none focus-visible:ring-2 focus-visible:ring-eco-600` garantiza un indicador de foco claro solo cuando se navega con teclado.
- **Layout Adaptable:** El formulario de suscripción usa `flex flex-col sm:flex-row gap-3` para que el campo y el botón se apilen en móvil y se alineen en fila en pantallas `sm` y superiores.
