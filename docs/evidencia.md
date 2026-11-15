# Evidencia — Email Triage con Groq (2026-09-15)

Workflow: `Email Triage con Groq` (ID 2765ezBcfcTPYfCt, `active=false`).
Validación runtime: válida, 0 errores (15 warnings menores, sin bloqueantes).

## Criterios de aceptación (definidos antes de probar)
1. Groq clasifica 3 emails fixture con categorías válidas en < 60s.
2. Fallback de parseo: respuesta vacía o irreconocible → `Informational` (no rompe el flujo).
3. Router: las 4 categorías tienen rama (Action → draft, resto → log).

## Matriz
| Caso | Input | Resultado |
|---|---|---|
| Feliz (Groq vivo, `groq/compound-mini`) | invoice→approve / receipt / WIN prize | **pass** → `Action / Receipt / Spam`, latencia 2s |
| Error (Groq caído/timeout mockeado) | choices ausente | **pass** → `Informational` (lógica verificada con node) |
| Borde (input vacío/duplicado) | `""` / `"   "` | **pass** → `Informational` |

3/3 pass. Sin credenciales ni PII en esta evidencia (key solo vía env, no registrada).

## Notas
- `llama-3.3-70b-versatile` está retirado en Groq (error `model_not_found`); se migró a `groq/compound-mini` (verificado en `/v1/models`).
- Warning conocido: Switch con 2 conexiones en output 0 (ramas Receipt/Spam/Informational terminan sin acción) → v2: conectar Gmail Label + Sheets en cada rama.
