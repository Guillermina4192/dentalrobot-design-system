# DentalRobot Design System — v1

Design system para el dashboard Insights de DentalRobot. Cubre las pantallas de Dashboard principal e Insurance Verification.

## Stack

- **Figma**: componentes, variables y text styles (arquitectura 2-file)
- **Style Dictionary v4**: compilación de tokens a CSS / ES6 / JSON
- **Supernova**: documentación y sync
- **GitHub**: versionado (SemVer)

## Estructura

```
dentalrobot-design-system/
├── contexto/          ← documentación del proceso (no borrar)
├── tokens/
│   ├── primitives/    ← paleta cruda (colores, escalas)
│   └── semantic/      ← roles semánticos (background, text, border…)
├── src/               ← outputs compilados por Style Dictionary
├── style-dictionary.config.json
├── package.json
├── CLAUDE.md          ← reglas para agentes de código
└── README.md
```

## Contexto del proceso

Todos los archivos en `contexto/` documentan las decisiones de diseño tomadas en cada etapa. Consultar antes de hacer cambios.

| Archivo | Contenido |
|---------|-----------|
| `00_brief.md` | Research del producto, benchmark, scope v1.0 |
| `01_audit.md` | Auditoría visual del archivo Figma existente |
| `02_tokens.md` | Decisiones de tokens primitivos y semánticos |
| `03_typography.md` | Escala tipográfica y text styles |
| `04_accessibility.md` | Matriz de contraste WCAG 2.2 AA |
| `05_atoms.md` | Documentación de componentes atómicos |
| `06_components.md` | Documentación de moléculas y organismos |
| `07_patterns.md` | UX patterns y estados |
| `08_qa.md` | Checklist de QA y handoff |
| `09_governance.md` | Modelo de contribución y versionado |

## Versión actual

`v1.0.0` — en construcción
