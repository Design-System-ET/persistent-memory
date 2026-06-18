# Memory Skill — Sistema de Memoria Persistente

## Propósito
Mantener continuidad entre sesiones de opencode almacenando el estado del proyecto en archivos Markdown planos dentro de `.memory/`.

## Estructura
```
.memory/
├── PROJECT.md      # Info estable del proyecto
├── CONTEXT.md      # Estado actual consolidado
├── TASKS.md        # Tareas
├── DECISIONS.md    # Decisiones con fecha
└── SESSION.md      # Memoria temporal de la sesión activa
```

## Formato de cada archivo

### PROJECT.md
```
# [Nombre]

## Descripción
[breve descripción]

## Tecnologías
- [Tecnología]

## Arquitectura
[descripción]
```

### CONTEXT.md
```
# Contexto Actual

Estado:
- [logro]
- [logro]

Próximo paso:
- [siguiente acción]
```

### TASKS.md
```
# Tareas

- [ ] tarea pendiente
- [x] tarea completada
```

### DECISIONS.md
```
# Decisiones

YYYY-MM-DD
- [decisión]
```

### SESSION.md
```
# Sesión Actual

- [acción realizada]
```

## Reglas de compactación
- DECISIONS.md: eliminar duplicados, mantener recientes
- TASKS.md: eliminar completadas [x] con más de 7 días
- CONTEXT.md: resumir solo info vigente
- SESSION.md: limpiar después de consolidar en CONTEXT.md

## Reglas de save
- CONTEXT.md: actualizar estado y próximo paso
- TASKS.md: marcar completadas, agregar nuevas
- DECISIONS.md: agregar nuevas con fecha YYYY-MM-DD
- SESSION.md: registrar acción de esta sesión
- Eliminar duplicados en todos los archivos
