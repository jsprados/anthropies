---
name: pre-mortem-check
description: Guardia previa a implementar. Usar cuando el usuario pida implementar, construir, programar o "pasar a código" una feature compleja (varios archivos o componentes, nuevo flujo de usuario, integración externa, cambio del modelo de datos, autenticación o permisos, migración) sin un PLAN_MAESTRO.md validado que la cubra; recuerda ejecutar /elephant-goldfish:elephant y /elephant-goldfish:goldfish antes de escribir código. Do NOT use when the request is a bounded bug fix, a one-line or few-line change in a single file, a typo, rename, formatting or dependency bump, tests or docs for existing code, a question or explanation with no implementation, when /elephant or /goldfish is already running, or when the user explicitly says to skip planning.
allowed-tools: Glob, Read
---

# Pre-mortem check

Objetivo: que ninguna feature compleja pase a código sin un plan auditado. Es un aviso, no un bloqueo: decide el usuario.

## Procedimiento

1. Si la petición cae en algún caso «Do NOT use» de la descripción, no intervengas y sigue con la tarea.
2. Comprueba con Glob si existe `PLAN_MAESTRO.md` en la raíz del proyecto.
3. Actúa según el resultado, sin escribir código mientras esperas respuesta:
   - **No existe**: di «Esta feature es compleja y no hay PLAN_MAESTRO.md. Recomiendo ejecutar primero /elephant-goldfish:elephant (plan) y después /elephant-goldfish:goldfish (auditoría). ¿Lo hacemos, o implemento sin plan?».
   - **Existe pero no cubre esta feature** (léelo: ni el título ni el objetivo la mencionan): da el mismo aviso e indica que el plan existente es de otra feature.
   - **Existe y la cubre**: pregunta si ya se ejecutó /elephant-goldfish:goldfish y se resolvieron sus hallazgos. Si no, recomienda ejecutarlo. Si sí, implementa siguiendo el plan.
4. Si el usuario decide implementar sin plan, respeta la decisión y no repitas el aviso en esta conversación.
