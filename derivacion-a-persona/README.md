# Derivación a persona

La Cueva del Oso es una agencia y consultora de IA y automatización para pymes y empresas de Chile y el mundo.

## Qué hace

Recibe por webhook el mensaje de un cliente junto con la respuesta de un agente de IA. Si el agente marca baja confianza o el tema está vetado, crea una tarea para una persona del equipo y le responde al cliente que lo contactará una persona. Si no, devuelve la respuesta del agente tal cual.

Flujo:

1. `Recibir mensaje del agente`: webhook POST con `cliente_id`, `canal`, `mensaje_cliente`, `respuesta_agente`, `confianza` (de 0 a 1), `tema` y, opcionalmente, `derivar`.
2. `Decidir derivacion`: marca `derivar` en verdadero si el agente lo pide, si la confianza es menor a 0,6 o si el tema está en la lista de vetados (`reclamo`, `legal`, `pago`, `salud`).
3. `Requiere persona`: separa los dos caminos.
4. `Crear tarea para una persona`: POST a `https://tareas.example.com/api/tareas`.
5. `Avisar que lo contactara una persona`: responde al cliente un aviso amable.
6. `Devolver respuesta del agente`: camino normal, sin derivación.

Todos los datos del archivo son ficticios.

## Cómo importarlo

1. En n8n, crea un workflow nuevo.
2. Menú de los tres puntos, `Import from file`, y elige `workflow.json`.
3. Revisa cada nodo, reemplaza los marcadores y activa el workflow.

## Qué reemplazar

- URL del nodo `Crear tarea para una persona`: cambia `https://tareas.example.com/api/tareas` por tu gestor de tareas o CRM.
- `<TU_PERSONA_RESPONSABLE>`: a quién se asigna la tarea.
- Credencial del nodo de tareas: el archivo no trae ninguna. Crea una credencial `Custom Auth` o `Header Auth` con `<TU_TOKEN>`.
- Umbral de confianza (0,6) y lista de temas vetados: están en el nodo `Decidir derivacion`. Ajústalos a tu negocio.
- Texto del aviso al cliente, en el nodo `Avisar que lo contactara una persona`.
- Autenticación del webhook: viene en `none`. Para producción conviene activar `Header Auth` y enviar el token desde tu agente.

## Qué NO incluye

- Credenciales, tokens ni URLs reales.
- El agente de IA: esta plantilla solo recibe lo que el agente ya decidió.
- Envío del aviso por WhatsApp u otro canal: el workflow responde al sistema que lo llamó y ese sistema entrega el mensaje al cliente.
- Notificación al equipo (correo o chat) ni seguimiento de la tarea hasta que se cierre.
- Datos de clientes ni datos de prueba guardados.

## Más información

Si quieres un agente de WhatsApp que sepa cuándo pasar la conversación a una persona, revisa el servicio de agentes de WhatsApp: https://lacuevadeloso.cl/servicios/agentes-whatsapp

Plantilla de ejemplo por La Cueva del Oso · Francisco Velásquez
