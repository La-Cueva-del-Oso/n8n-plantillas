# Calificación de leads

La Cueva del Oso es una agencia y consultora de IA y automatización para pymes y empresas de Chile y el mundo.

## Qué hace

Recibe un formulario web por webhook (nombre, correo, teléfono, mensaje, presupuesto y urgencia), revisa que los datos básicos vengan completos y asigna una calificación al contacto: alto, medio o bajo. Después lo envía a tu CRM mediante una llamada HTTP y responde al formulario.

Flujo:

1. `Recibir formulario`: webhook POST.
2. `Normalizar campos`: deja los datos con el mismo formato, vengan donde vengan.
3. `Campos validos`: exige nombre, correo con arroba y teléfono. Si falta algo, responde 422 con un mensaje claro.
4. `Calificar lead`: reglas simples por puntos (presupuesto, urgencia y largo del mensaje).
5. `Enviar al CRM`: POST a `https://crm.example.com/api/contactos`.
6. `Responder recibido`: confirma al formulario que los datos llegaron.

Todos los datos del archivo son ficticios.

## Cómo importarlo

1. En n8n, crea un workflow nuevo.
2. Menú de los tres puntos, `Import from file`, y elige `workflow.json`.
3. Revisa cada nodo, reemplaza los marcadores y activa el workflow.

## Qué reemplazar

- URL del nodo `Enviar al CRM`: cambia `https://crm.example.com/api/contactos` por el endpoint de tu CRM.
- Credencial del nodo `Enviar al CRM`: el archivo no trae ninguna. Crea una credencial de tipo `Custom Auth` o `Header Auth` con `<TU_TOKEN>` y asígnala al nodo.
- Cuerpo de la llamada: ajusta los nombres de los campos a los que espera tu CRM.
- Reglas del nodo `Calificar lead`: los umbrales de presupuesto (en pesos chilenos) y los puntos son de ejemplo.
- Ruta del webhook: `calificacion-de-leads` es un nombre de ejemplo. n8n genera la URL real al activarlo.
- Autenticación del webhook: viene en `none`. Para producción conviene activar `Header Auth` y enviar el token desde tu formulario.

## Qué NO incluye

- Credenciales, tokens ni URLs reales.
- Almacenamiento del formulario en bruto (hoja de cálculo o base de datos). Si lo necesitas, agrega un nodo de almacenamiento justo después de `Normalizar campos`.
- Protección contra spam, deduplicación de contactos ni reintentos si el CRM falla.
- Notificaciones al equipo comercial.
- Datos de clientes ni datos de prueba guardados.

## Más información

Si quieres que armemos algo así para tu negocio, revisa el servicio de automatizaciones: https://lacuevadeloso.cl/servicios/automatizaciones

Plantilla de ejemplo por La Cueva del Oso · Francisco Velásquez
