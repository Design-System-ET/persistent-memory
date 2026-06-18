---
description: Carga la memoria persistente del proyecto
---
Ejecuta el protocolo de carga de memoria:

1. Busca la carpeta `.memory/` en la raíz del proyecto
2. Si no existe, créala usando las plantillas de `~/.config/opencode/skills/memory/templates/`
3. Si existe, verifica que tenga los 5 archivos requeridos (PROJECT.md, CONTEXT.md, TASKS.md, DECISIONS.md, SESSION.md); crea los faltantes desde plantillas
4. Lee PROJECT.md, CONTEXT.md, TASKS.md, DECISIONS.md, SESSION.md
5. Presenta un resumen con: tareas pendientes, último contexto, última decisión
