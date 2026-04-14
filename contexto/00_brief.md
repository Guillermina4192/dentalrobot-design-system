# 00 — Brief | DentalRobot Design System v1

**Proyecto:** dentalrobot-design-system  
**Versión:** v1.0  
**Autora:** Guillermina  
**Sistema:** Guillermina × Claude  
**Fecha inicio:** Abril 2025  
**Archivo Figma Library:** [por crear]  
**Archivo Figma Product:** Dashboard-dentalrobot (existente — solo referencia visual)  
**Repo:** https://github.com/Guillermina4192/dentalrobot-design-system  

---

## 1. El Producto — ¿Qué es DentalRobot?

DentalRobot es una plataforma SaaS B2B de automatización con IA para el ciclo de ingresos (Revenue Cycle Management / RCM) de prácticas dentales y DSOs (Dental Support Organizations) en USA.

**Fundada:** 2018, Miami FL  
**Mercado:** USA — dental practices, grupos dentales y DSOs  
**Modelo:** B2B SaaS, contratos month-to-month, desde $150/mes (Lite) hasta planes Enterprise custom  

### Qué automatiza

El producto ataca el proceso más costoso y manual del back-office dental: la **verificación de seguros de pacientes**. Antes de cada cita, alguien en el consultorio tiene que llamar o entrar a portales de seguros para verificar cobertura — proceso que puede tomar 10–20 minutos por paciente. DentalRobot lo automatiza completamente.

Sus módulos core:

| Módulo | Qué hace |
|--------|----------|
| **Insurance Verification AI** | Verifica cobertura en 240+ portales automáticamente, sin llamadas. Escribe el resultado directamente en el PMS (Practice Management Software) del cliente. |
| **Payment Posting** | Postea EOBs (Explanation of Benefits) y pagos de seguros automáticamente. |
| **Voice AI / Call Center** | IA de voz que maneja llamadas entrantes y salientes del front desk. |
| **Workflow Engine** | Motor de automatización custom — convierte SOPs o grabaciones de pantalla en workflows de IA. |
| **Insights Dashboard** | Panel de analytics con métricas de rendimiento del sistema de automatización. |
| **RCM completo** | Suite full-stack: verificación → claims → billing → cobros. |

### Diferenciadores clave vs competencia

- Único en el mercado que **lee y escribe** en cualquier marca/versión de PMS dental (Dentrix, Eaglesoft, Open Dental, Denticon, y otros 12+ sistemas).
- No usa solo EDI/clearinghouse (que da datos genéricos y desactualizados) — usa scraping + APIs directas a 240+ portales de payers para máxima fidelidad de datos.
- Automatización hasta el 93% de tareas repetitivas de RCM.
- ROI promedio reportado: 400%–900%.

### Usuario del sistema (quién usa el dashboard)

El dashboard **Insights** es usado principalmente por:

- **Office Manager / Practice Manager**: necesita ver el estado operacional del sistema de automatización, cuántas verificaciones se procesaron, tasa de éxito, errores pendientes.
- **DSO Executive / Revenue Cycle Director**: necesita KPIs de alto nivel para reportar a liderazgo — ahorro de tiempo, % automatización, impacto en revenue.
- **Billing Coordinator**: necesita ver el detalle de verificaciones individuales, estados, excepciones que requieren atención manual.

**Contexto de uso crítico:** es una herramienta de trabajo diaria, no un dashboard casual. Los usuarios la abren al iniciar la jornada y la consultan múltiples veces. La velocidad de lectura y la claridad de estados es lo más importante. No es un producto de consumo — es software de operaciones.

---

## 2. El Rubro — Dental RCM & Insurance Verification

### El problema que resuelve

La verificación de seguros dentales es el cuello de botella más grande del ciclo de ingresos dental:

- El front desk de un consultorio dedica **4–8 horas semanales** solo a verificación.
- Los errores en verificación son la **causa #1 de rechazo de claims** (denials).
- Un dental group con 10 consultorios puede tener **100–500 verificaciones por semana**.
- El costo de un staff member dedicado a esto: $35,000–$55,000/año.

### El mercado

- **Dental practices en USA:** ~200,000 activas.
- **DSOs (grupos dentales):** segmento de mayor crecimiento — consolidación acelerada desde 2018. Muchos DSOs manejan 20–500+ consultorios.
- **Competidores directos en automatización de insurance verification:**

| Competidor | Enfoque | Debilidad vs DentalRobot |
|------------|---------|--------------------------|
| **Vyne Trellis** | Clearinghouse tradicional + claims | Solo EDI, sin write-back inteligente al PMS |
| **Zuub** | Verificación click-to-verify | Más manual, sin automatización real end-to-end |
| **Dental Intelligence** | Analytics + insurance (powered by Vyne) | No automatiza, solo verifica y muestra datos |
| **Weave** | Comunicación + verificación básica | Generalista, no especializado en RCM profundo |
| **DentalxChange** | Back-office billing | Legacy, sin IA |

### Tendencias del rubro 2025

1. **Consolidación en DSOs**: los grupos grandes buscan plataformas que escalen a cientos de consultorios, no soluciones por consultorio.
2. **AI-first**: el diferenciador está en qué tan autónomo es el sistema — cuánto puede hacer sin intervención humana.
3. **Write-back al PMS**: el estándar del mercado ahora exige que los datos de verificación vuelvan automáticamente al PMS, no solo se muestren en un portal externo.
4. **Datos de alta fidelidad**: los clientes ya no aceptan datos EDI genéricos — exigen los mismos datos que ven en los portales de los payers.

---

## 3. Benchmark de UI — Referentes para el Dashboard

### Referentes directos (dental/healthcare RCM)

- **Dental Intelligence**: dashboard con KPIs de práctica, métricas de producción, gráficos de tendencia. Fondo claro, tablas de datos densas. Audiencia: practice owners y managers.
- **Carestream Dental**: UI legacy, alta densidad de información, poco diseño — referencia de qué evitar.
- **Availity**: portal de seguros médicos B2B — muy funcional, muy denso, accesibilidad media.

### Referentes de UI por categoría

**Para el nivel de complejidad visual y densidad de datos:**
- **Stripe Dashboard**: el estándar de calidad en B2B SaaS financiero — sidebar limpio, KPI cards con trends, tablas de datos con estados claros, paleta neutra con acentos de color funcionales.
- **Linear** (project management): sidebar oscuro + contenido claro, densidad alta sin ruido visual, excelente uso de tipografía.
- **Mixpanel**: dashboard de analytics — excelente manejo de datos vacíos, loading states, y visualizaciones de tendencia.

**Para el visual de marca (navy/dark blue + branding premium):**
- **Salesforce Lightning**: dark navy sidebar + contenido claro, sistema de colores funcional muy maduro, referencia directa para healthcare B2B.
- **Figma** (producto en sí): uso de azul como color de acción, neutros muy bien calibrados.

### Patrones de UI que aplican al dashboard de DentalRobot

**Dashboard principal (Insights Dashboard):**
- KPI cards en la parte superior (4–6 métricas clave con trend)
- Gráfico de volumen/tendencia en el tiempo (línea o barra)
- Tabla de estado de automatizaciones recientes
- Indicadores de health del sistema (éxito / error / pendiente)

**Insurance Verification view:**
- Tabla densa con: paciente, fecha de cita, estado de verificación, payer, cobertura clave, acción requerida
- Sistema de estados con colores semánticos: verde (verificado), amarillo (pendiente), rojo (error/requiere atención), gris (no aplica)
- Filtros por fecha, por consultorio (para DSOs), por estado
- Acceso rápido al detalle de cada verificación

---

## 4. Scope v1.0

### Qué entra en v1.0

**Pantallas:**
1. **Insights Dashboard** — métricas generales de rendimiento del sistema
2. **Insurance Verification** — tabla de verificaciones con estados y filtros

**Fundaciones del sistema:**
- Tokens primitivos + semánticos (color, spacing, radius, shadow, motion, z-index)
- Text styles completos
- Accesibilidad: WCAG 2.2 AA en toda la paleta

**Componentes mínimos para renderizar las 2 pantallas:**
- Button (primary, secondary, ghost, destructive)
- Badge / Status chip (5 estados semánticos)
- Input / Search field
- Dropdown / Select
- Data Table (header, row, sort, empty state, loading state)
- Metric Card (KPI card con trend)
- Sidebar navigation
- Top header / App bar
- Date range filter
- Modal básico
- Toast / Alert

**Documentación:**
- CLAUDE.md — reglas del sistema
- README.md — cómo usar el DS
- Supernova conectado a Figma Library + repo

### Qué NO entra en v1.0 (queda para v1.1+)

- Practice Connections view
- Tools view
- Mobile / responsive
- Dark mode
- Onboarding / empty states elaborados
- Componentes de gráficos/charts complejos
- Voice AI interface

---

## 5. Decisiones de arquitectura

| Decisión | Elección | Razón |
|----------|----------|-------|
| Arquitectura Figma | 2-file (Library + Product) | Standard enterprise — nadie diseña en la Library |
| Token tool en Figma | Variables nativas | Figma Variables ya soporta primitivos + semánticos sin plugins extra |
| Export de tokens | Style Dictionary v4 | Estándar del mercado, compila a CSS + JS + JSON |
| Documentación | Supernova Free | Free tier suficiente para v1, sync nativo con Figma + GitHub |
| Versionado | SemVer (v1.0.0) | Permite comunicar breaking changes claramente |
| Accesibilidad | WCAG 2.2 AA mínimo | Requisito legal para software B2B en USA (ADA compliance) |
| Tipografía principal | Poppins (identificada en el prototipo) | Familia de marca existente — mantener coherencia |

---

## 6. Próximos pasos (orden)

1. ✅ Setup repo + estructura carpetas
2. → E1: Auditoría visual del archivo Figma existente
3. E2: Definición de tokens primitivos + semánticos
4. E3: Text styles
5. E4: Validación WCAG de la paleta
6. E5: Átomos
7. E6: Moléculas + organismos
8. E7: UX Patterns
9. E8: QA + Handoff
10. E9: Docs + Export + Governance
