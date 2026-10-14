---
name: Focused Learning Studio
colors:
  surface: '#FFFFFF'
  surface-dim: '#d2d9f4'
  surface-bright: '#faf8ff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#f2f3ff'
  surface-container: '#eaedff'
  surface-container-high: '#e2e7ff'
  surface-container-highest: '#dae2fd'
  on-surface: '#131b2e'
  on-surface-variant: '#464555'
  inverse-surface: '#283044'
  inverse-on-surface: '#eef0ff'
  outline: '#777587'
  outline-variant: '#c7c4d8'
  surface-tint: '#4d44e3'
  primary: '#3525cd'
  on-primary: '#ffffff'
  primary-container: '#4f46e5'
  on-primary-container: '#dad7ff'
  inverse-primary: '#c3c0ff'
  secondary: '#006591'
  on-secondary: '#ffffff'
  secondary-container: '#39b8fd'
  on-secondary-container: '#004666'
  tertiary: '#7e3000'
  on-tertiary: '#ffffff'
  tertiary-container: '#a44100'
  on-tertiary-container: '#ffd2be'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#e2dfff'
  primary-fixed-dim: '#c3c0ff'
  on-primary-fixed: '#0f0069'
  on-primary-fixed-variant: '#3323cc'
  secondary-fixed: '#c9e6ff'
  secondary-fixed-dim: '#89ceff'
  on-secondary-fixed: '#001e2f'
  on-secondary-fixed-variant: '#004c6e'
  tertiary-fixed: '#ffdbcc'
  tertiary-fixed-dim: '#ffb695'
  on-tertiary-fixed: '#351000'
  on-tertiary-fixed-variant: '#7b2f00'
  background: '#F8FAFC'
  on-background: '#131b2e'
  surface-variant: '#dae2fd'
  correct: '#16A34A'
  incorrect: '#DC2626'
typography:
  headline-xl:
    fontFamily: Outfit
    fontSize: 36px
    fontWeight: '700'
    lineHeight: 44px
  headline-xl-mobile:
    fontFamily: Outfit
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 36px
  headline-lg:
    fontFamily: Outfit
    fontSize: 28px
    fontWeight: '600'
    lineHeight: 36px
  headline-lg-mobile:
    fontFamily: Outfit
    fontSize: 22px
    fontWeight: '600'
    lineHeight: 30px
  headline-md:
    fontFamily: Outfit
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  body-lg:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: '500'
    lineHeight: 30px
  body-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  label-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 24px
  label-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
  label-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 1.5rem
  gutter-sm: 1rem
  margin: 2rem
  margin-sm: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 1rem
  space-lg: 1.5rem
  space-xl: 2rem
---

# Diseño de la Plataforma de Estudio

## 1. Resumen

Plataforma web de estudio donde el estudiante practica con **3 ejercicios de alternativas** y cuenta con un **chatbot** que entrega las respuestas y explica el razonamiento detrás de cada una.

**Objetivo:** que el estudiante practique, se equivoque, entienda por qué y vuelva a intentar.

**Público objetivo:** estudiantes de enseñanza media y superior.

---

## 2. Alcance del MVP

| Incluido | Fuera de alcance (por ahora) |
|---|---|
| 3 ejercicios de alternativas (A, B, C, D) | Cuentas de profesor y panel docente |
| Corrección inmediata con retroalimentación | Ranking entre estudiantes |
| Chatbot que entrega respuestas y explicaciones | Banco de ejercicios ampliable |
| Resumen de resultados al finalizar | Aplicación móvil nativa |

---

## 3. Flujo de usuario

```
Inicio → Ejercicio 1 → Ejercicio 2 → Ejercicio 3 → Resultados
              ↕              ↕              ↕
                  Chatbot (siempre disponible)
```

---

## 7. Diseño visual

### 7.1 Paleta
| Uso | Color |
|---|---|
| Primario | `#4F46E5` (índigo) |
| Fondo | `#F8FAFC` |
| Tarjetas | `#FFFFFF` |
| Texto | `#0F172A` |
| Correcto | `#16A34A` |
| Incorrecto | `#DC2626` |
| Acento chatbot | `#0EA5E9` |

### 7.2 Tipografía
- Títulos: **Poppins** (600–700)
- Texto: **Inter** (400–500)
- Tamaño base: 16 px; enunciados 20 px.

### 7.3 Componentes
- **Tarjeta de ejercicio:** bordes redondeados (16 px), sombra suave.
- **Alternativa:** botón de ancho completo, letra a la izquierda, estados *normal*, *hover*, *seleccionada*, *correcta*, *incorrecta*.
- **Barra de progreso:** 3 segmentos que se llenan al avanzar.
- **Burbujas del chat:** estudiante a la derecha (primario), bot a la izquierda (gris claro).

### 7.4 Responsive
- **Móvil (< 640 px):** una columna, chatbot a pantalla completa.
- **Escritorio:** ejercicio al centro y chatbot como panel lateral de 360 px.

---

## 8. Accesibilidad
- Contraste mínimo AA en todos los textos.
- Navegación completa por teclado (Tab, Enter, flechas entre alternativas).
- Los estados correcto/incorrecto usan **ícono + color**, no solo color.
- Etiquetas `aria` en alternativas y en el campo del chat.
- Respeto por `prefers-reduced-motion`.
