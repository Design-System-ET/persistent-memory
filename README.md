# persistent-memory

Sistema de memoria persistente para opencode que permite mantener continuidad entre sesiones de trabajo sin depender del historial de la conversación.

Cada sesión de opencode comienza con contexto cero: el LLM no recuerda lo que se hizo antes, lo que obliga a repetir instrucciones y reconstruir el estado del proyecto desde cero. Esto consume tokens innecesariamente y ralentiza el trabajo.

**persistent-memory** resuelve esto almacenando el estado del proyecto en archivos Markdown planos dentro de `.memory/`. Al iniciar una sesión, `/memory load` inyecta el contexto guardado directamente en el prompt del LLM, evitando que tenga que reconstruirlo desde el historial. Esto reduce significativamente el consumo de tokens y acelera el inicio de cada sesión.

El sistema incluye 4 comandos (`/memory load|save|compact|status`) y un skill con el protocolo de formatos, reglas de compactación y plantillas para inicializar la memoria en cualquier proyecto.

## Instalación

### 1. Clonar este repositorio

Clonar dentro de la carpeta de configuración de opencode:

```powershell
git clone https://github.com/Design-System-ET/persistent-memory.git "$env:USERPROFILE\.config\opencode"
```

Esto copia:
- `skills/memory/` — skill con el protocolo y plantillas
- `commands/memory-*.md` — los 4 comandos (/memory load, save, compact, status)

### 2. Configurar AGENTS.md global

Ejecutar `/init` en opencode para generar el AGENTS.md base (si no existe).
Luego editar `~/.config/opencode/AGENTS.md` y agregar al final:

```markdown
## Memoria persistente
Cada proyecto puede tener `.memory/` con: PROJECT, CONTEXT, TASKS, DECISIONS, SESSION.
Usar `/memory load` al iniciar sesión y `/memory save` al cerrar.
Los comandos y la skill `memory` detallan el protocolo completo.
```

### 3. Reiniciar opencode

Cerrar y volver a abrir opencode. Los comandos `/memory load`, `/memory save`, `/memory compact` y `/memory status` ya están disponibles.

## Uso diario

```powershell
# Al iniciar una sesión de trabajo
/memory load

# Antes de cerrar la sesión
/memory save

# Periódicamente para limpiar
/memory compact

# Consulta rápida
/memory status
```

## Estructura instalada

```
~/.config/opencode/
├── AGENTS.md                    # Agregar bloque de memoria manualmente
├── skills/memory/
│   ├── SKILL.md                 # Protocolo de memoria
│   └── templates/               # Plantillas para .memory/
└── commands/
    ├── memory-load.md
    ├── memory-save.md
    ├── memory-compact.md
    └── memory-status.md
```

Por proyecto, al ejecutar `/memory load` se crea:

```
[proyecto]/
└── .memory/
    ├── PROJECT.md
    ├── CONTEXT.md
    ├── TASKS.md
    ├── DECISIONS.md
    └── SESSION.md
```

## Licencia

MIT License. Ver [LICENSE](LICENSE).
