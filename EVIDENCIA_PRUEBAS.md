# Evidencia de pruebas manuales · Preentrega 1

**Fecha:** 25 de noviembre de 2026, hora de Santiago. Los datos de clientes y sus correos son ficticios.

La evidencia se observó en el chat y los paneles de ejecución de n8n. El proveedor de correo devolvió identificador de mensaje; la herramienta de Sheets devolvió los datos de la fila creada. No se afirma haber comprobado una lectura humana del correo.

| Prueba | Resultado observado | Evaluación |
|---|---|---|
| 1 · Llaveros, versión inicial | Fila WM3-1, Cliente Prueba, cantidad 3, Pendiente de revisión. Ejecución completa de 26,847 s, 4.089 tokens. Gmail devolvió un comprobante de envío. El chat mostraba ese comprobante técnico. | Detectada mejora de presentación. Se agregó Edit Fields para devolver output del agente. |
| 2 · Mascota sin fotos, versión intermedia | Fila WM3-2 y Faltan antecedentes, pero tomó PRUEBA FICTICIA 2 como nombre, agregó requisitos no aprobados y prometió una actualización no implementada. | No aprobada funcionalmente. Se reescribió el prompt y se agregaron descripciones a los 13 campos del agente. |
| 3 · Repetición exacta tras corrección | Fila WM3-3, Cliente Mascota, cantidad 1, Faltan antecedentes, faltante Fotos de la mascota; Sin fecha definida válido. El chat mostró el resultado del agente sin imponer vistas ni número mínimo de fotos. 24,991 s y 4.496 tokens. | Aprobada en la versión final. |
| 4 · Cantidad negativa | Solicitud de -2 llaveros; pidió un entero mayor que cero. El árbol de ejecución no incluyó la herramienta de Sheets. Gmail y Edit Fields finalizaron correctamente. Inicio visible 21:04:18; 8,928 s y 1.836 tokens. | Aprobada. No se creó fila para esta solicitud. |
| 5 · Llaveros, repetición final | Fila WM3-5, Cliente Prueba, cantidad 3, 6 cm, verde/sin pintura, Sin fecha definida, Pendiente de revisión y faltantes Ninguno. Chat con ID real y revisión de Karla. Recorrido con Sheets, Gmail y Edit Fields. 16,772 s y 3.930 tokens. | Aprobada en la versión final. |

## Entradas exactas

### Llaveros · pruebas 1 y 5

> PRUEBA FICTICIA DE CODERHOUSE. Soy Cliente Prueba, mi contacto es cliente@example.invalid. Quiero 3 llaveros con el nombre LUNA, de 6 cm, color verde, sin pintura. Sin fecha definida. La personalización es solo el nombre escrito, no lleva logo ni imagen. Registra mi solicitud para que Karla la revise; no necesito un precio confirmado ahora.

### Mascota sin fotos · pruebas 2 y 3

> PRUEBA FICTICIA 2. Soy Cliente Mascota, contacto mascota@example.invalid. Quiero una figura pintada de mi perro, una unidad de unos 12 cm. Todavía no tengo fotografías. Sin fecha definida. Registra la consulta indicando qué hace falta para que Karla la evalúe.

### Cantidad negativa · prueba 4

> Soy Cliente Cantidad, mi correo es cantidad@example.invalid. Quiero -2 llaveros con el nombre LUNA. Registra la solicitud ahora.

## Respuestas finales observadas

En la prueba 3, la respuesta incluyó: Resultado: Registro creado con éxito; Identificador: WM3-3; Estado: Faltan antecedentes; Nombre: Cliente Mascota; Cantidad: 1; Fecha deseada: Sin fecha definida; Faltantes imprescindibles: Fotos de la mascota (no adjuntas). Derivó diseño, material, precio y plazo a Karla.

En la prueba 4, informó que -2 era inválido y pidió confirmar una cantidad entera mayor que cero para poder registrar. No aparece Sheets en el recorrido.

En la prueba 5, la respuesta incluyó: Registro exitoso; ID: WM3-5; Estado: Pendiente de revisión; Nombre: Cliente Prueba; Cantidad: 3; Fecha deseada: Sin fecha definida; Faltantes imprescindibles: Ninguno. Indicó que Karla revisará viabilidad, precio y plazo, y que Karla incorporará eventuales cambios.

## Alcance de esta evidencia

La aprobación significa que esos casos concretos tuvieron el comportamiento esperado. No demuestra ausencia de alucinaciones en todos los mensajes posibles, ni funcionamiento de memoria, actualización de filas, carga concurrente o canales aún no implementados.
