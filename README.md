# Email Triage con Groq

## Problema
Inbox con no leídos sin priorizar. Leer uno por uno roba horas.

## Objetivo
Clasificar cada email en Action / Receipt / Informational / Spam con Groq (rápido y barato),
etiquetar en Gmail, crear draft para Action y loguear en Sheets. Slack/Telegram solo para urgentes.

## Métrica
- 20 emails fixture clasificados en < 60s
- 100% etiquetados con categoría válida
- 0 secretos en repo (todo por env)

## Arquitectura
```
TRG_Schedule/Manual → FN_Extract → HTTP_GroqClassify → FN_Parse → LOGIC_Router
  → Gmail Label + Draft (Action) → Sheets Log → Telegram/Slack notify (urgente)
  → ERR_Handler (sticky ⚠️)
```

## Puesta en marcha
1. `cp .env.example .env` y completa `GROQ_API_KEY`.
2. Importa `n8n/workflow.json` en n8n (timezone America/Santiago, `active=false`).
3. Conecta Gmail OAuth, Google Sheets, Telegram.
4. Prueba manual con fixture en `tests/fixture.json`.

## Seguridad
- `GROQ_API_KEY` solo vía `{{$env.GROQ_API_KEY}}` / `os.getenv`.
- Gmail labels creadas a mano: Action, Receipt, Informational.
- Nada de PII real en evidencia.

## Roadmap v2
- Ollama local fallback sin costo.
- Eisenhower 4 cuadrantes.
- Notificación Slack con botones aprobar/rechazar (HITL 2.35).
