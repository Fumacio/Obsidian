# Schema del Wiki de Gustavo Cerati

Este archivo define cómo el LLM debe mantener y estructurar el wiki.

## Estructura del Wiki

```
Cerati/
├── raw/                    # Fuentes inmutables (nunca modificar)
│   ├── articulos/          # Artículos, entrevistas, reseñas
│   └── imagenes/           # Imágenes descargadas localmente
├── wiki/                   # Wiki generado por el LLM (solo lectura para humans)
│   ├── entidades/          # Páginas sobre personas, bandas, álbumes, canciones
│   ├── conceptos/          # Páginas sobre temas: rock argento, producción, etc.
│   ├── fuentes/            # Resúmenes de cada fuente procesada
│   ├── comparaciones/      # Tablas comparativas, análisis
│   └── resumenes/          # Resúmenes generales y síntesis
├── index.md                # Catálogo de todo el wiki
├── log.md                  # Registro cronológico de actividades
└── CLAUDE.md               # Este archivo (schema)
```

## Convenciones de Nomenclatura

- **Entidades**: `Nombre del artista.md`, `Nombre del álbum.md`, `Nombre de la canción.md`
- **Conceptos**: `tema-en-minusculas.md` (ej: `rock-argentino.md`)
- **Fuentes**: `YYYY-MM-DD titulo de la fuente.md`
- **Comparaciones**: `comparacion-tema1-tema2.md`

## Formato de Páginas

### Entidades (personas, bandas, álbumes, canciones)
```markdown
---
tipo: [persona|banda|album|cancion]
fechas: [fechas relevantes]
etiquetas: [etiqueta1, etiqueta2]
fuentes: [fuente1.md, fuente2.md]
---

# Nombre de la Entidad

## Resumen
[Breve descripción]

## Detalles
[Información detallada]

## Relaciones
- [[Otra entidad]]
- [[Concepto relacionado]]

## Fuentes
- [[fuente1.md]]
```

### Conceptos (temas, géneros, técnicas)
```markdown
---
tipo: concepto
etiquetas: [etiqueta1, etiqueta2]
fuentes: [fuente1.md]
---

# Nombre del Concepto

## Definición
[Qué es]

## Relevancia para Cerati
[Cómo se conecta]

## Ejemplos
- [[Entidad1]]
- [[Entidad2]]

## Fuentes
- [[fuente1.md]]
```

### Fuentes (resúmenes de artículos, entrevistas, etc.)
```markdown
---
tipo: fuente
fecha: YYYY-MM-DD
autor: [nombre del autor]
medio: [nombre del medio]
url: [URL original si existe]
---

# Título de la Fuente

## Resumen
[Resumen ejecutivo]

## Puntos Clave
- Punto 1
- Punto 2

## Información Relevante para el Wiki
[Qué datos nuevos aporta]

## Páginas Actualizadas
- [[entidad1.md]] - [qué se actualizó]
- [[concepto1.md]] - [qué se actualizó]
```

## Flujo de Trabajo

### Al Ingerir una Fuente
1. Leer el archivo en `raw/`
2. Discutir puntos clave con el usuario
3. Crear página de fuente en `wiki/fuentes/`
4. Actualizar o crear páginas de entidades afectadas
5. Actualizar o crear páginas de conceptos afectados
6. Actualizar `index.md`
7. Registrar en `log.md`

### Al Responder Preguntas
1. Buscar en `index.md` páginas relevantes
2. Leer páginas relevantes del wiki
3. Sintetizar respuesta con citas
4. Si la respuesta es valiosa, guardarla como nueva página en el wiki
5. Actualizar `index.md`
6. Registrar en `log.md`

### Al Hacer Lint (mantenimiento)
1. Buscar contradicciones entre páginas
2. Identificar páginas huérfanas (sin enlaces de entrada)
3. Detectar conceptos mencionados sin página propia
4. Actualizar páginas desactualizadas
5. Registrar cambios en `log.md`

## Formato del Log

Cada entrada debe empezar con:
```markdown
## [YYYY-MM-DD] tipo | descripción breve
```

Tipos: `ingest`, `query`, `lint`, `actualización`, `creación`

Ejemplo:
```markdown
## [2026-09-12] ingest | Entrevista a Cerati en La Nación
```

## Reglas Generales

1. **Nunca modificar** archivos en `raw/`
2. **Siempre actualizar** `index.md` al agregar o modificar páginas
3. **Siempre registrar** actividad en `log.md`
4. **Mantener consistencia** en formato y nomenclatura
5. **Priorizar calidad** sobre cantidad
6. **Usar enlaces internos** `[[nombre]]` para conectar páginas
7. **Todo en español**
