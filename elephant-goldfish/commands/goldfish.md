---
description: Peces de Colores — 7 auditorías ciegas e independientes de PLAN_MAESTRO.md
allowed-tools: Glob, Read, Grep
---

# Peces de Colores

Orquesta la auditoría ciega de `PLAN_MAESTRO.md`. Tú no auditas, no opinas y no añades hallazgos.

## 1. Precondición

Comprueba con Glob que `PLAN_MAESTRO.md` existe en la raíz del proyecto. Si no existe, responde «No hay PLAN_MAESTRO.md. Ejecuta primero /elephant-goldfish:elephant.» y detente.

## 2. Delegación aislada

Lanza 7 subagentes `elephant-goldfish:goldfish-auditor` en paralelo: un único mensaje con 7 llamadas a la herramienta Agent. El prompt de cada llamada es EXACTAMENTE esta línea, con N de 1 a 7:

```
Audita PLAN_MAESTRO.md. Lente: N.
```

- Prohibido añadir al prompt cualquier otra cosa: ni resumen de la conversación, ni objetivos del usuario, ni pistas, ni otros archivos. Cualquier contexto añadido rompe la ceguera.
- Nunca uses un fork: hereda la conversación.
- Si `elephant-goldfish:goldfish-auditor` no está disponible, usa `goldfish-auditor`. Si tampoco lo está, detente y dilo. No lo sustituyas por otro tipo de agente: perdería el aislamiento.

## 3. Consolidación

1. Une las 7 respuestas en una sola tabla, por orden de lente:

   | Lente | Fallo en la vida real | Cita del plan | Solución requerida antes de programar |
   |---|---|---|---|

2. Copia las filas literalmente. No las edites, fusiones ni reordenes dentro de su lente, y no añadas filas propias.
3. Si un subagente devuelve `ERROR` o una salida sin tabla, pon la fila `| N. <lente> | ERROR: <mensaje literal> | — | — |`. No repitas esa auditoría por tu cuenta.
4. Verifica cada cita contra `PLAN_MAESTRO.md` con Read: el texto entrecomillado debe aparecer literalmente en la línea indicada. Si no aparece, antepón `⚠ CITA NO VERIFICADA` a esa celda. Marca la fila; no la borres.
5. Si algún subagente añadió `Contexto ajeno al plan recibido e ignorado.`, indícalo debajo de la tabla: significa que la delegación no fue ciega.
6. Cierra con una sola línea: `Filas: X · Lentes sin hallazgos: Y · Citas no verificadas: Z`.
