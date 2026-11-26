# WE MAKE³ · Agente base para solicitudes de cotización

**Karla Rojas · Coderhouse AI Automation Avanzado · Preentrega 1**

El agente recibe una solicitud de un producto personalizado, reúne sus antecedentes y la registra para revisión humana. Si faltan fotos de una figura personalizada o el diseño de un logo, deja el caso en **Faltan antecedentes**. Si hay datos suficientes para comenzar la evaluación, queda **Pendiente de revisión**. Karla conserva la aprobación de viabilidad, tamaño final, material, terminación, precio y plazo.

## Archivo de entrega

`checkpoint1_karla_rojas.json` es el archivo exportado desde n8n después de probar la versión corregida. El workflow está inactivo y el chat de prueba no se publicó como un servicio abierto.

## Flujo

1. **When chat message received:** recibe texto libre en el chat interno.
2. **AI Agent:** interpreta el mensaje con instrucciones modulares **Rol → Ámbito → Objetivo → Reglas → Escalamiento → Respuesta**. Máximo de **5 iteraciones**.
3. **OpenAI Chat Model:** conexión nativa al agente, con gpt-5-mini y credencial Gateway de n8n Cloud en el entorno probado.
4. **Google Sheets Tool:** herramienta lateral del agente, operación Append Row, documento y hoja fijos. Tiene descripción semántica de cuándo usarla y descripción de cada campo que completa el modelo.
5. **Send a message (Gmail):** después del agente, envía al correo interno el identificador de ejecución, fecha y resultado del agente. Permite supervisión humana sin publicar razonamiento interno privado.
6. **Edit Fields:** devuelve al chat únicamente el campo output del agente después de que Gmail confirme el envío, para que el cliente vea la respuesta legible y no el comprobante técnico del correo.

La herramienta de Sheets no está colocada como acción secuencial: se conecta al puerto **ai_tool** del agente. El modelo utiliza el puerto **ai_languageModel**. No hay un bloque IF anterior que sustituya la decisión de usar la herramienta.

La versión actual del AI Agent no muestra un selector independiente de modo Tools Agent; usa la arquitectura de herramientas conectadas lateralmente. La consigna prefiere GPT-4o o Claude 3.5 Sonnet; el entorno probado ofrece gpt-5-mini en el nodo nativo OpenAI Chat Model. Si el docente solicita un modelo concreto, reasignarlo y repetir las pruebas antes de entregar una nueva versión.

## Datos y controles

- Obligatorios para registrar: nombre, contacto, producto, descripción y cantidad entera mayor que cero.
- Identificador generado por n8n: WM3- más el ID de ejecución. Fecha en America/Santiago.
- La cantidad tiene además una expresión determinista que rechaza valores no enteros o menores o iguales a cero antes de la escritura. Las pruebas observaron que el agente no invoca la herramienta con una cantidad negativa; no se forzó deliberadamente una llamada inválida a la expresión.
- Los saludos y consultas generales no deberían crear registros. La prueba negativa se centró en cantidad inválida.
- Sin fecha definida es válido; medidas, colores y terminación pueden quedar pendientes.
- No se inventan cantidades mínimas de fotos, tarifas, plazos o requisitos comerciales.
- No se promete actualizar un registro: la herramienta de esta versión añade filas. Cambios posteriores se derivan a Karla.
- No hay memoria persistente ni aislamiento de varios casos por cliente todavía: corresponde ampliarlo en el módulo 3.

## Credenciales y reproducción

El archivo exportado contiene referencias a las credenciales utilizadas, no sus contraseñas ni tokens OAuth. Al importar en otro entorno:

1. Asignar una credencial válida al nodo nativo OpenAI Chat Model. El Gateway utilizado depende de la disponibilidad de crédito y de n8n Cloud.
2. Conectar Google Sheets con una cuenta de prueba propia y elegir un documento y una hoja con las columnas del CSV incluido. Reasignar el mapeo si se cambian encabezados.
3. Conectar Gmail y establecer un destinatario interno controlado por quien ejecuta la prueba. El JSON exportado usa el correo del proyecto; cambiarlo si se reproduce fuera de este entorno para no enviarle correos de prueba a Karla.
4. Abrir el chat interno y ejecutar las entradas ficticias incluidas. Verificar el recorrido, la fila de Sheets, el resultado de Gmail y el output del chat.

Los permisos concedidos para el entorno del negocio fueron metadatos de Drive, acceso a las planillas y, para Gmail, administrar borradores y enviar correos. No se marcó acceso continuado de Gmail ni el permiso de eliminación permanente de correos. Google mostró vencimiento de Gmail el 24 de mayo de 2027. No se autorizaron estas conexiones con el Drive personal de Karla.

## Validación realizada

Se hicieron cinco ejecuciones manuales. Una prueba detectó nombre incorrecto y requisitos no aprobados; se ajustaron prompt y descripciones y se repitió. La versión final pasó los casos de mascota sin fotos, cantidad negativa y llaveros con antecedentes suficientes. Ver **EVIDENCIA_PRUEBAS.md**.

La planilla conserva registros ficticios de prueba, incluido el intento que detectó el error. No son pedidos reales. No se ejecutaron escenarios de carga, concurrencia, fallos del proveedor ni pruebas con clientes reales.

## Estado de entrega

Repositorio público habilitado con autorización de Karla el 25 de noviembre de 2026. El enlace se envió en la Pre-entrega 1 de Coderhouse. La plataforma confirmó «Entregado» y «En corrección»; Ticher está generando la evaluación. Este estado no equivale a aprobación docente.

Repositorio: https://github.com/wemake3chile-sys/wemake3-coderhouse-automatizacion
