# 03 — Typography | Escala tipográfica y text styles

**Etapa:** E3 — Foundations (Tipografía)  
**Fecha:** Abril 2025  
**Archivos generados:**
- `tokens/semantic/typography.json` — 19 typography tokens compuestos
- Figma Library: 17 text styles en archivo `[DR] Design System — Library v1`
- Página visual "🎨 Foundations" con specimens tipográficos

---

## 1. Decisiones clave

### 1.1 Inter como fuente del sistema

**Decisión:** Inter es la fuente principal para 100% del UI. Poppins queda reservado solo para elementos de marca (logo, slides de marketing, marketing site).

**Razones:**
- Inter fue diseñada específicamente para interfaces digitales — optimizada para tamaños chicos (11–14px) donde los dashboards densos viven.
- El prototipo actual (generado con Lovable) ya usa Inter implícitamente — está alineada con el stack real.
- Es la fuente más adoptada en B2B SaaS moderno (Stripe, Linear, Vercel, shadcn/ui).
- Open source vía Google Fonts, sin costos de licencia.

**Trade-off aceptado:** Perdemos la calidez de Poppins (más humana, más brand-forward) en el UI. Pero la legibilidad y densidad de Inter es más importante para el usuario del dashboard (office managers consultando tablas durante 8h al día).

### 1.2 Escala modular de tamaños

**Decisión:** 10 tamaños en escala geométrica aproximada (11, 12, 14, 16, 18, 20, 24, 30, 36, 48 px).

Nombrados por t-shirt size en `font.size`:

| Token | Valor | Uso típico |
|-------|-------|-----------|
| `xs` | 11px | Section dividers (MODULES, GENERAL), micro labels |
| `sm` | 12px | Captions, metadata, timestamps |
| `base` | 14px | Body default — nav items, table rows, form labels |
| `md` | 16px | Emphasized body, card subtitles |
| `lg` | 18px | Card titles, subsection headings |
| `xl` | 20px | Modal / section titles |
| `2xl` | 24px | Page titles (Dashboard, Insurance Verifications) |
| `3xl` | 30px | KPI numbers (38, 12, 4) |
| `4xl` | 36px | Display medium |
| `5xl` | 48px | Display large — marketing slides |

**Razón:** En dashboards B2B la mayoría del contenido vive entre 11–16px. Los tamaños grandes (24px+) son minoría pero necesarios para jerarquía. Saltar de 20 a 24 y de 24 a 30 da suficiente contraste visual sin fragmentar la escala.

### 1.3 Categorías de text styles: 6 familias

| Familia | Propósito | Cantidad |
|---------|-----------|----------|
| `display/*` | Brand display — Poppins, marketing | 2 |
| `heading/*` | Jerarquía de títulos UI — Inter Semi Bold/Bold | 5 |
| `body/*` | Texto regular — Inter Regular | 3 |
| `body-strong/*` | Texto enfatizado — Inter Medium | 2 |
| `label/*` | UI labels — form, nav, buttons | 3 |
| `caption/*` | Metadata, timestamps | 2 |

**Total: 17 text styles.** Deliberadamente compacto. Cada style tiene un propósito claro. No hay duplicados decorativos.

### 1.4 Line height proporcional al tamaño

**Decisión:** 4 niveles de line-height (tight 1.2, snug 1.35, normal 1.5, relaxed 1.65).

- `tight` (1.2) para display y headings grandes (30px+): reduce espacio vertical.
- `snug` (1.35) para headings medianos y labels: balance entre legibilidad y compactación.
- `normal` (1.5) para body: estándar de lectura.
- `relaxed` (1.65) reservado para long-form (no se usa en v1.0 pero queda definido).

**Razón:** Un line-height fijo aplicado a todos los tamaños genera problemas — 1.5× en una página title de 24px deja demasiado aire (36px), mientras que 1.2× en body de 14px aplasta la lectura. Proporcionalidad inversa es la regla.

### 1.5 Letter-spacing solo para casos específicos

**Decisión:** Casi todo usa `letterSpacing: 0`. Excepciones:

- `display/*` y `heading/xl` usan `tight` (-0.02em): los tamaños grandes necesitan compactación.
- `label/xs` usa `wider` (+0.08em): uppercase mechánico (MODULES, GENERAL) necesita más aire entre letras para leerse bien.

**Razón:** El letter-spacing modificado puede causar issues de consistencia en diferentes renderers. Solo se aplica donde mejora objetivamente la legibilidad.

---

## 2. Mapping prototipo → sistema

Traducción de valores del prototipo actual a tokens:

| Prototipo | Token asignado | Cambio |
|-----------|---------------|--------|
| "Dashboard" (page title) 24px SemiBold | `heading/lg` | ✓ sin cambio |
| "38" (KPI number) ~28–32px Bold | `heading/xl` 30px Bold | Normalizado a 30 |
| "Verified Today" (KPI label) 13px | `body/md` 14px | Subido 1px para respetar escala |
| Table header 12px Medium | `label/sm` | ✓ |
| Table body 13px | `body/md` 14px | Subido 1px |
| Patient name (bold in table) 13–14px Medium | `body-strong/md` | ✓ |
| "MODULES" / "GENERAL" 11px uppercase | `label/xs` con letter-spacing wider | ✓ |
| Badge text 11–12px | `label/sm` | ✓ |
| Copyright footer 11px | `caption/sm` | ✓ |

**Nota:** donde el prototipo usaba 13px, el sistema estandariza a 14px. 13px no está en la escala y no aporta diferencia visual significativa vs 14px, pero sí rompe la consistencia del sistema.

---

## 3. Lo que NO entra en v1.0

- **Variable font settings personalizados** (Inter soporta opsz, wght continuo). Usamos los pesos discretos Regular/Medium/Semi Bold/Bold — suficiente para este sistema.
- **Tipografía responsive / fluid typography.** Todos los valores son absolutos en px. Si en el futuro se necesita, se construye sobre esta base.
- **Estilos de internacionalización** (árabe, CJK). Scope es USA only.

---

## 4. Cómo usar en Figma

Cualquier texto en el archivo Library o Product debe usar un text style de la lista:

1. Seleccionar el texto en canvas
2. Panel Typography → click en el ícono de estilo
3. Elegir el style apropiado (ej: `body-strong/md` para un patient name en una tabla)
4. **Nunca** modificar tamaño / peso manualmente después — si no existe el style que necesito, es una señal de que falta un token y hay que agregarlo al sistema.

## 5. Cómo usar en código

Desde el CSS compilado por Style Dictionary:

```css
.page-title {
  font: var(--typography-heading-lg);
}
```

O desde JS/TS:

```js
import { typography } from './tokens';
const pageTitle = typography.headingLg;
```
