# Plantillas de n8n de La Cueva del Oso

La Cueva del Oso es una agencia y consultora de IA y automatización para pymes y empresas de Chile y el mundo.

Tres plantillas de ejemplo para n8n, con datos ficticios y nodos genéricos. Sirven como punto de partida: se importan, se reemplazan los marcadores y se adaptan a cada negocio.

| Plantilla                                       | Qué hace                                                                                              |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [calificacion-de-leads](calificacion-de-leads/) | Recibe un formulario por webhook, valida, califica (alto, medio o bajo) y envía el contacto a un CRM. |
| [recordatorio-de-cita](recordatorio-de-cita/)   | Lee las citas de mañana y envía un recordatorio por la API de WhatsApp Business.                      |
| [derivacion-a-persona](derivacion-a-persona/)   | Pasa a una persona las conversaciones donde el agente tiene baja confianza o el tema está vetado.     |

## Cómo usarlas

Cada carpeta trae un `workflow.json` y un `README.md` con el detalle. En n8n: workflow nuevo, `Import from file`, `workflow.json`.

## Antes de activar cualquiera

- Ninguna plantilla incluye credenciales, tokens ni URLs reales. Los marcadores se ven como `<TU_TOKEN>` o `https://crm.example.com`.
- Crea tus propias credenciales en n8n y asígnalas a los nodos HTTP.
- Prueba primero con datos ficticios.

## Servicios relacionados

- Automatizaciones: https://lacuevadeloso.cl/servicios/automatizaciones
- Agentes de WhatsApp: https://lacuevadeloso.cl/servicios/agentes-whatsapp

## Licencia

MIT. Ver [LICENSE](LICENSE).

Plantilla de ejemplo por La Cueva del Oso · Francisco Velásquez
