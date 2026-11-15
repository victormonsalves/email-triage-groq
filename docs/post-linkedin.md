# Borrador LinkedIn — Email Triage con Groq (NO publicado)

Mi inbox era un segundo trabajo: cientos de no leídos y media mañana decidiendo qué mirar primero.

Armé un workflow n8n que clasifica cada correo con Groq en Action / Receipt / Informational / Spam, prepara el borrador de los importantes y registra todo en una planilla. Corre cada hora, sin intervención.

Resultado medible: 3/3 casos de prueba en verde — 3 correos clasificados correctamente en 2 segundos, con fallback seguro a Informational si la IA falla. Stack: n8n self-hosted + Groq + Gmail + Sheets.

Aprendizaje: los modelos se retiran (llama-3.3-70b-versatile murió esta semana) — fijar el modelo por variable de entorno y validar contra /v1/models ahorra un debug entero.

¿Tu inbox también necesita un portero? El workflow completo está en [github.com/victormonsalves/email-triage-groq](https://github.com/victormonsalves/email-triage-groq).

#n8n #automatizacion #IA #productividad

---
Variante corta (<600 caracteres, primer comentario):
Inbox en piloto automático: n8n + Groq clasifica mis correos cada hora (Action/Receipt/Info/Spam) y me deja los borradores listos. 3/3 tests en verde, 2s por tanda. Lo que más me enseñó: versionar el modelo por env porque los modelos se retiran sin avisar. #n8n #automatizacion
