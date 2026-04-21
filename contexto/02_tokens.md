# 02 — Tokens | Primitivos + Semánticos

**Etapa:** E2 — Foundations (Tokens)  
**Fecha:** Abril 2025  
**Archivos generados:**
- `tokens/primitives/colors.json`
- `tokens/primitives/dimensions.json` (spacing, radius, shadow, motion, z-index)
- `tokens/semantic/colors.json`

---

## 1. Filosofía de arquitectura

**Tres capas, referencias en cascada:**

```
Primitivos (valores crudos — hex, px, ms)
   ↓  referenciados por
Semánticos (roles de UI — background/surface, text/primary, status/success)
   ↓  consumidos por
Componentes (tokens específicos de componente — emergen en E5+)
```

**Regla estricta:** los componentes NUNCA consumen primitivos directamente. Siempre consumen semánticos. Esto permite que un cambio de marca (ej: swap de brand color) se propague sin tocar componentes.

---

## 2. Decisiones clave tomadas

### 2.1 Separación navy vs blue

**Decisión:** Dos escalas de color azul, con propósitos separados.

| Escala | Rol | Uso |
|--------|-----|-----|
| `navy` (50–950) | Brand identity | Sidebar background, logo, gradientes de marca, slides de presentación |
| `blue` (50–900) | Interactive primary | Botones, links, focus rings, acciones primarias |

**Razón:** El navy `#111784` es demasiado oscuro y saturado para usarse como color de acción en UI. Un botón primario navy sobre fondo blanco genera mucho peso visual y compite con el contenido. El `blue.600` (`#2563eb`) da mejor jerarquía sin perder la conexión con la identidad de marca.

### 2.2 Escala de color completa por matiz (50–900)

**Decisión:** Cada matiz tiene 10 stops (50, 100, 200, 300, 400, 500, 600, 700, 800, 900). Navy y gray tienen adicionalmente 950 para tonos muy oscuros.

**Razón:** Es el estándar de la industria (Tailwind, Radix, Material 3). Permite construir cualquier componente sin necesidad de agregar tonos intermedios. La mayoría de los componentes van a usar solo 3–4 stops por matiz (típicamente 100, 600, 800), pero tener la escala completa evita refactors cuando aparecen casos edge.

### 2.3 Spacing base 4px con escala nombrada por múltiplo

**Decisión:** `space/N` donde N es el múltiplo. `space/4 = 8px`, `space/8 = 16px`, `space/12 = 24px`.

**Razón:** Es la convención de Tailwind y coincide con el sistema del prototipo actual (construido en Lovable/shadcn, que usa la misma base). Mantener naming consistente reduce cognitive load cuando se traduce de Figma a código.

**Alternativa considerada:** Naming por t-shirt size (xs/sm/md/lg/xl). Descartado porque limita la expresividad a 5–6 valores y es más ambiguo. El naming por múltiplo escala.

### 2.4 Radius con t-shirt sizes

**Decisión:** `radius/none | xs | sm | md | lg | xl | 2xl | 3xl | full`.

**Razón:** A diferencia del spacing, el radius tiene pocos valores discretos que se usan con frecuencia (sm para inputs, lg para cards, full para pills). T-shirt sizing es más legible acá.

### 2.5 Shadows — sistema mínimo de 5 niveles

**Decisión:** `shadow/none | xs | sm | md | lg | xl`.

**Razón:** El prototipo actual usa casi exclusivamente bordes, no sombras. El sistema de elevación va a ser minimalista. 5 niveles cubren desde subtle elevation (xs) hasta modals/popovers (xl). No necesitamos más.

### 2.6 Motion tokens

**Decisión:** Duration con 5 valores (instant/fast/base/slow/slower) + 4 easings nombrados.

**Razón:** Definir motion en tokens desde v1.0 evita animaciones arbitrarias en componentes. `standard` como default cubre el 80% de casos. `decelerate` para entradas, `accelerate` para salidas — alineado con Material Design 3.

### 2.7 Z-index escalonado con gap amplio

**Decisión:** Gaps de 100 entre cada nivel (base=0, dropdown=1000, sticky=1100, overlay=1200, modal=1300…).

**Razón:** Los gaps grandes permiten insertar capas intermedias sin refactorizar. Si mañana necesito un toast por encima de un modal pero debajo de un tooltip, el sistema lo soporta sin renumerar todo.

### 2.8 Status colors: 6 roles semánticos

**Decisión:** `success | error | warning | info | neutral | progress`.

**Razón directa del audit:** El prototipo tiene 8 estados semánticos en los badges (Verified, Failed, Pending, Not Found, Needs Review, In Progress, Audited, Not Audited). Mapeo a 6 roles:

| Estado del prototipo | Token semántico |
|---------------------|----------------|
| Verified, Audited | `status.success` |
| Failed | `status.error` |
| Not Found | `status.warning` |
| Needs Review, Pending (icon) | `status.info` |
| Not Audited | `status.neutral` |
| In Progress | `status.progress` |

Cada rol tiene 5 variantes: `background`, `text`, `icon`, `border`, `solid`. Eso da flexibilidad para badges suaves (bg+text), dots (solid), iconos con o sin fondo, y bordes de notificación.

### 2.9 Cobertura WCAG 2.2 AA integrada a los semánticos

**Decisión:** Los tokens semánticos de texto están calibrados para cumplir AA sobre sus backgrounds previstos. Validamos matriz completa en E4.

**Pares críticos que cumplen AA:**
- `text.primary` (`gray.900`) sobre `background.surface` (white) → 18.6:1 (AAA)
- `text.secondary` (`gray.600`) sobre white → 6.8:1 (AA cumple, cerca de AAA)
- `text.tertiary` (`gray.500`) sobre white → 4.5:1 (AA mínimo — justo)
- `text.disabled` (`gray.400`) → NO cumple AA intencionalmente (es el comportamiento WCAG esperado para disabled)

**Corrección del audit:** El prototipo usaba `#9ca3af` (`gray.400`) como texto secundario. Ese mapeo era incorrecto. En el sistema `gray.400` queda reservado solo para disabled/placeholder. El texto secundario pasa a `gray.600`.

---

## 3. Naming conventions finales

| Categoría | Formato | Ejemplo |
|-----------|---------|---------|
| Primitivo color | `color.{matiz}.{stop}` | `color.blue.600` |
| Semántico color | `color.{rol}.{elemento}[.{estado}]` | `color.text.primary`, `color.interactive.primary.hover` |
| Spacing | `space.{múltiplo}` | `space.4` = 8px |
| Radius | `radius.{tamaño}` | `radius.lg` = 8px |
| Shadow | `shadow.{nivel}` | `shadow.md` |
| Motion | `motion.duration.{velocidad}` | `motion.duration.base` |
| Z-index | `zIndex.{capa}` | `zIndex.modal` |

---

## 4. Lo que NO entra en los tokens (aún)

- **Dark mode / theming:** fuera de scope v1.0. La arquitectura de semánticos permite agregar un tema dark en v1.1 sin refactorizar componentes.
- **Responsive breakpoints:** se definen en E7 (UX Patterns).
- **Grid / layout tokens:** idem E7.
- **Component-specific tokens:** emergen en E5 cuando identifiquemos tokens que solo aplican a un componente.
- **Brand gradients:** se declaran como styles en Figma, no como tokens (los tokens son valores escalares).

---

## 5. Próximos pasos dentro de E2

1. Crear variables en Figma Library con exactamente esta estructura
2. Bindear semánticos a primitivos vía `figma.variables.setBoundVariableForConsumer`
3. Configurar Style Dictionary v4
4. Compilar tokens → CSS custom properties + ES6 + JSON plano
5. Validar build output
