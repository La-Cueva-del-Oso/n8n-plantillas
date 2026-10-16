# Recordatorio de cita

La Cueva del Oso es una agencia y consultora de IA y automatización para pymes y empresas de Chile y el mundo.

## Qué hace

Cada día a las 09:00 lee las citas confirmadas del día siguiente desde una hoja o API, envía un recordatorio por la API de WhatsApp Business con una plantilla aprobada y registra que el recordatorio salió.

Flujo:

1. `Cada dia a las 09:00`: disparador programado.
2. `Leer citas de manana`: GET a `https://api.example.com/citas` con la fecha de mañana. Se espera una respuesta con la forma `{ "citas": [ ... ] }`, donde cada cita trae `id`, `nombre`, `telefono`, `fecha` y `hora`.
3. `Separar citas`: convierte la lista en un ítem por cita.
4. `Enviar recordatorio por WhatsApp`: POST a `https://graph.facebook.com/<VERSION>/<PHONE_NUMBER_ID>/messages` con un mensaje de plantilla, a razón de uno por segundo.
5. `Registrar confirmacion`: POST a `https://api.example.com/citas/confirmaciones` con el id de la cita y el id del mensaje.

Todos los datos del archivo son ficticios.

## Cómo importarlo

1. En n8n, crea un workflow nuevo.
2. Menú de los tres puntos, `Import from file`, y elige `workflow.json`.
3. Revisa cada nodo, reemplaza los marcadores y activa el workflow.

## Qué reemplazar

- `https://api.example.com/citas` y `https://api.example.com/citas/confirmaciones`: tus endpoints reales (o cambia el nodo por uno de Google Sheets, Airtable u otro).
- `<VERSION>`: versión vigente de la API de WhatsApp Business, según la documentación de Meta.
- `<PHONE_NUMBER_ID>`: identificador del número de WhatsApp Business de tu cuenta.
- `<NOMBRE_PLANTILLA_APROBADA>`: nombre de una plantilla de mensaje ya aprobada por Meta. Los parámetros del cuerpo (nombre, fecha, hora) deben coincidir con las variables de esa plantilla.
- Credenciales: el archivo no trae ninguna. Crea una credencial `Custom Auth` o `Header Auth` con `<TU_TOKEN>` para cada nodo HTTP que la necesite.
- Horario y zona horaria: ajusta el disparador y la zona horaria del workflow.

## Qué NO incluye

- Credenciales, tokens ni identificadores reales.
- La plantilla de WhatsApp: la crea y aprueba cada negocio en su cuenta de Meta.
- Manejo de respuestas del cliente (confirmar, cancelar o reagendar).
- Reintentos ante fallas del envío ni control de números inválidos.
- Datos de clientes ni datos de prueba guardados.

## Más información

Si quieres automatizar recordatorios y agenda en WhatsApp para tu negocio, revisa el servicio de agentes de WhatsApp: https://lacuevadeloso.cl/servicios/agentes-whatsapp

Plantilla de ejemplo por La Cueva del Oso · Francisco Velásquez
