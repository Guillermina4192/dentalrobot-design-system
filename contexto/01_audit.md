# 01 — Auditoría Visual | DentalRobot Dashboard

**Fuente:** Archivo Figma `Dashboard-dentalrobot` (EEOJtRUCOS2hMw2UvltJhE) — solo referencia visual  
**Pantallas auditadas:** Dashboard principal, Insurance Verification (x2 estados), Dropdown contextual  
**Método:** Análisis visual directo de screenshots + extracción del código React generado por Figma MCP  
**Fecha:** Abril 2025  

---

## 1. Layout General

El sistema tiene una estructura de **app shell fija**:

| Zona | Descripción | Dimensiones aprox. |
|------|-------------|-------------------|
| **Sidebar** | Navegación lateral fija, fondo navy oscuro | 140–150px de ancho |
| **Top header** | Barra superior con breadcrumb + acciones de usuario | 48–56px de alto |
| **Content area** | Área principal scrolleable, fondo blanco/gris muy claro | resto del viewport |
| **Footer** | Copyright mínimo en la base del sidebar | 24px |

**Viewport de referencia:** 1440px (los screenshots son a 1920px pero el layout efectivo es 1440px)

---

## 2. Paleta de Colores — Inventario Completo

### 2.1 Colores de marca / brand

| Uso | Hex | Nombre provisional | Notas |
|-----|-----|--------------------|-------|
| Sidebar background | `#0f1fa5` aprox / `#111784` | brand-navy | Azul marino profundo — color dominante de marca |
| Sidebar background dark | `#060a5a` | brand-navy-deep | Segunda parada del gradiente de marca |
| Gradiente sidebar | `#111784` → `#060a5a` | brand-gradient | Lineal de arriba a abajo |
| Logo mark | Blanco sobre navy | — | Solo se ve en blanco sobre navy |

### 2.2 Colores de superficie (UI)

| Uso | Hex aprox | Nombre provisional | Notas |
|-----|-----------|-------------------|-------|
| Background página | `#ffffff` | surface-page | Blanco puro en content area |
| Background cards | `#ffffff` | surface-card | Cards con borde sutil |
| Background subtle (alternating) | `#f9fafb` | surface-subtle | Casi blanco, para contraste mínimo |
| Border cards / dividers | `#e5e7eb` | border-default | Gris muy claro |
| Sidebar nav item hover | `rgba(255,255,255,0.10)` | sidebar-hover | Blanco al 10% sobre navy |
| Sidebar nav item active | `rgba(255,255,255,0.18)` | sidebar-active | Blanco al 18% sobre navy |

### 2.3 Colores de texto

| Uso | Hex aprox | Nombre provisional |
|-----|-----------|-------------------|
| Texto principal | `#111827` | text-primary |
| Texto secundario | `#6b7280` | text-secondary |
| Texto terciario / placeholder | `#9ca3af` | text-tertiary |
| Texto en sidebar | `#ffffff` | text-on-navy |
| Labels de sección sidebar | `#9ca3af` / blanco al 60% | text-sidebar-label |
| Links / texto interactivo | `#3b82f6` aprox | text-interactive |
| Texto muted en cards | `#6b7280` | text-muted |

### 2.4 Colores semánticos de estado (status)

Extraídos de los badges de la tabla Insurance Verification:

| Estado | Badge background | Badge text | Hex bg aprox | Hex text aprox |
|--------|-----------------|------------|--------------|----------------|
| **Verified** | Verde claro | Verde oscuro | `#d1fae5` | `#065f46` |
| **Failed** | Rojo claro | Rojo oscuro | `#fee2e2` | `#991b1b` |
| **Pending** | Azul claro | Azul oscuro | `#dbeafe` | `#1e40af` |
| **Not Found** | Amarillo claro | Amarillo oscuro | `#fef3c7` | `#92400e` |
| **Needs Review** | Celeste claro | Celeste oscuro | `#e0f2fe` | `#075985` |
| **In Progress** | Azul medio claro | Azul medio | `#dbeafe` | `#1d4ed8` |
| **Audited** | Verde claro | Verde | `#d1fae5` | `#059669` |
| **Not Audited** | Gris claro | Gris | `#f3f4f6` | `#6b7280` |

### 2.5 Colores funcionales / interactivos

| Uso | Hex aprox | Nombre provisional |
|-----|-----------|-------------------|
| CTA Button (Show / primary action) | `#1e3a8a` / navy | interactive-primary |
| Button Logout | `#ffffff` border `#e5e7eb` | interactive-secondary |
| Trend positivo | `#16a34a` | feedback-positive |
| Trend negativo | `#dc2626` | feedback-negative |
| System status: Healthy | `#22c55e` text on `#f0fdf4` | status-healthy |
| System status: Online | `#3b82f6` text on `#eff6ff` | status-online |
| System status: Slow | `#f59e0b` text on `#fffbeb` | status-slow |
| Icon de verificación (check) | `#22c55e` | icon-success |
| Icon de pending (clock) | `#60a5fa` | icon-pending |
| Icon de failed (triangle) | `#f87171` | icon-error |
| Icon de location pin | `#a78bfa` | icon-accent |

---

## 3. Tipografía — Inventario

### 3.1 Familia tipográfica

| Familia | Uso | Pesos detectados |
|---------|-----|-----------------|
| **Poppins** | Branding / slides de presentación | SemiBold (600), Medium (500) |
| **Inter** (implícito) | UI del dashboard (inferido — sistema estándar en Lovable/shadcn) | Regular (400), Medium (500), SemiBold (600) |

> **Nota crítica:** El dashboard fue generado con Lovable (herramienta AI-to-code). El stack base es React + Tailwind + shadcn/ui, que usa Inter como fuente por defecto. La fuente del UI es Inter, no Poppins. Poppins aparece solo en las slides de título de la presentación (no en el dashboard funcional).

### 3.2 Escala de tamaños detectados (estimados desde screenshots)

| Uso en UI | Tamaño aprox | Peso | 
|-----------|-------------|------|
| Page title ("Dashboard", "Insurance Verifications") | 24px | SemiBold |
| Page subtitle / description | 13–14px | Regular |
| Section label ("MODULES", "GENERAL") | 11px | SemiBold / uppercase |
| Nav item | 13–14px | Medium |
| Table header | 12px | Medium / SemiBold |
| Table body | 13–14px | Regular / Medium |
| KPI number (38, 12, 4) | 28–32px | Bold |
| KPI label ("Verified Today") | 13px | Regular |
| KPI trend (+5% since yesterday) | 12px | Regular |
| Badge text | 11–12px | Medium |
| Button text | 13–14px | Medium |
| Breadcrumb | 13px | Regular |
| Timestamp / metadata | 12px | Regular |
| Footer | 11–12px | Regular |

---

## 4. Espaciado — Patrones Detectados

Sistema base: **múltiplos de 4px** (inferido de Tailwind)

| Uso | Valor aprox |
|-----|-------------|
| Padding interno de cards | 16–24px |
| Gap entre KPI cards | 16px |
| Padding horizontal content area | 24–32px |
| Padding vertical entre secciones | 24px |
| Padding interno tabla (row height) | 12–16px vertical |
| Gap entre ícono y texto en nav | 8–12px |
| Padding horizontal nav item | 12–16px |
| Margen entre label de sección y nav items | 8px |
| Padding interno badges | 4px vertical, 8–12px horizontal |
| Gap entre columnas de tabla | 16–24px |

---

## 5. Border Radius — Patrones Detectados

| Elemento | Radio aprox |
|----------|-------------|
| Cards / panels | 8px |
| Badges / chips de estado | 9999px (pill / full) |
| Botones primarios (Show) | 6–8px |
| Botones secundarios (Logout) | 6–8px |
| Inputs / dropdowns | 6px |
| Dropdown contextual menu | 6–8px |
| Sidebar | 0px (full bleed) |

---

## 6. Sombras y Elevación

| Elemento | Sombra detectada |
|----------|-----------------|
| Cards | Sombra muy sutil o solo borde — `box-shadow: 0 1px 3px rgba(0,0,0,0.07)` aprox |
| Dropdown contextual | Sombra media — `box-shadow: 0 4px 12px rgba(0,0,0,0.12)` aprox |
| Botón primary (Show) | Sin sombra visible |
| Header top | Borde inferior sutil `border-bottom: 1px solid #e5e7eb` |

Sistema de elevación: **mínimo** — el diseño usa bordes más que sombras. Solo dropdowns y overlays tienen sombra real.

---

## 7. Iconografía

| Sistema | Notas |
|---------|-------|
| **Lucide Icons** | Inferido del stack Lovable/shadcn — íconos de línea, 16–20px, stroke 1.5–2px |
| Tamaños detectados | 16px (tabla), 20px (nav), 24px (acciones) |
| Color | Heredan el color del contexto (text-secondary en nav, colores semánticos en badges) |
| Logo DR | Marca propia — cuadrado con "DR" en blanco, fondo navy |

---

## 8. Componentes Identificados en las Pantallas

### Dashboard principal
- App shell (sidebar + header + content)
- Sidebar navigation con secciones (MODULES / GENERAL)
- Top header con breadcrumb + user info + logout
- Tabs (Overview / Patient Insights)
- Context bar (Client / fecha / CTA)
- KPI cards x4 (Metric Card con trend)
- Recent Activity list
- System Status list con badges de salud
- Footer

### Insurance Verification
- Mismo app shell
- Page header con título + descripción
- Context bar con multi-select práctica + date picker + CTA
- Filter bar (All Practices dropdown + All Status dropdown + Search input)
- Data table con 9 columnas:
  - Appointment (time)
  - Patient Name (bold)
  - Practice (link)
  - Type (text)
  - Carrier (text)
  - Verification By (text)
  - Eligibility Status (badge semántico)
  - Missing Fields (ratio x/y)
  - Audited (badge semántico)
  - Actions (icon button `...`)
- Contextual dropdown menu (Insights / View / Recheck)
- Pagination implícita (no visible en screenshots pero estructuralmente necesaria)

---

## 9. Patrones de Interacción Detectados

- **Hover en tabla:** highlight de fila (color de fondo sutil)
- **Dropdown contextual:** se abre desde el botón `...` de cada fila
- **Nav active state:** ítem activo con fondo levemente más claro
- **Links en tabla:** texto azul interactivo (Practice name)
- **Trend indicators:** texto coloreado con prefijo + o - y porcentaje
- **Date navigation:** flechas `<` `>` para navegar por fechas

---

## 10. Gaps y Problemas Detectados

| Problema | Impacto | Acción |
|----------|---------|--------|
| No hay estados de loading en ninguna pantalla | Alto — UI queda en blanco durante cargas | Diseñar skeleton screens en E7 |
| No hay empty state definido | Alto — sin datos la tabla desaparece | Diseñar empty state en E7 |
| Los badges de estado no tienen iconos consistentes | Medio — algunos tienen ícono, otros no | Estandarizar en E5 |
| El sidebar no tiene estado collapsed | Medio — en viewports menores a 1440px queda muy apretado | Definir comportamiento responsive en E7 |
| Contraste del texto secundario sobre blanco no validado | Alto — `#9ca3af` sobre `#ffffff` es ~2.4:1 (FALLA WCAG AA) | Corregir en E4 |
| Sin focus states visibles en ningún elemento | Alto — WCAG 2.4.7 | Diseñar en E4/E5 |
| Fuente del sistema no confirmada (Inter vs Poppins) | Medio | Confirmar en E3 |

---

## 11. Decisiones de Diseño a Tomar en E2+

1. **¿Adoptamos la paleta tal cual o la elevamos?** — Recomendación: mantener navy `#111784` como brand color primario pero construir una escala de grises más calibrada con WCAG en mente.
2. **¿Inter o Poppins como fuente del sistema?** — Recomendación: Inter para UI (mejor legibilidad en dashboards densos), Poppins solo para elementos de marca (logo, headings de marketing).
3. **Modo claro como único por ahora** — Dark mode fuera de scope v1.0.
4. **9 columnas en la tabla de Insurance Verification** es denso — evaluar si en v1.0 se puede priorizar u ocultar columnas opcionales.
