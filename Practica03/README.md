# Práctica 3 - Mejora de una comunicación sobre resultados de una revisión de portafolio

CIBEST CAPITAL dispone de un borrador ficticio posterior a una revisión periódica de portafolio. El contenido incluye los hechos necesarios, pero presenta problemas deliberados de extensión, repetición, estructura, claridad y tono. En esta práctica usarás el **Asesor de escritura (Writing Coach)** para diagnosticar los problemas y producir dos versiones dirigidas a audiencias distintas sin alterar los hechos.

## Metadatos

| Campo | Detalle |
|---|---|
| Duración | 32 min |
| Complejidad | Intermedia |
| Nivel de Bloom | Evaluar / Crear |
| Tipo de actividad | Revisión y adaptación de comunicación con IA |
| Aplicaciones | Microsoft Copilot - Asesor de escritura |
| Modalidad | Individual |
| Insumos previos | `recursos/borrador_revision_portafolio.docx` |
| Resultado | Diagnóstico y dos comunicaciones mejoradas para audiencias diferentes |

## Distribución de tiempo

| Fase | Actividad | Tiempo |
|---|---|---:|
| 1 | Revisar el borrador y abrir el Asesor de escritura | 4 min |
| 2 | Diagnosticar el contenido sin reescribirlo | 8 min |
| 3 | Crear la versión para el cliente | 8 min |
| 4 | Crear la versión para el equipo interno | 7 min |
| 5 | Comparar y validar consistencia factual | 5 min |
|  | **TOTAL** | **32 min** |

## Descripción general

Primero pedirás un diagnóstico del borrador sin permitir que el agente lo reescriba de inmediato. Después aplicarás las recomendaciones para crear una versión clara y comprensible para el cliente y otra con mayor detalle técnico para el equipo interno. Finalmente compararás tono, estructura y profundidad, verificando que ambas versiones conserven exactamente los mismos hechos y cifras.

## Objetivos de aprendizaje

Al finalizar podrás:

- usar el Asesor de escritura para diagnosticar problemas de claridad, estructura, extensión y tono;
- separar el diagnóstico de la reescritura;
- adaptar una misma base factual a dos audiencias distintas;
- comprobar que una reescritura con IA no altera cifras, hechos ni próximos pasos.

## Escenario de la práctica

La práctica se desarrolla en el contexto de **CIBEST CAPITAL**. Debes mejorar una comunicación preparada después de una revisión periódica ficticia del portafolio de un cliente, en la que se identificaron cambios en desempeño y algunos aspectos que conviene conversar con él.

## Prerrequisitos

- Experiencia funcional básica con Microsoft 365.
- Acceso al **Asesor de escritura** en Microsoft Copilot.
- Acceso local al archivo `borrador_revision_portafolio.docx`.

## Preparación del entorno

Antes de iniciar el cronómetro:

1. Localiza `recursos/borrador_revision_portafolio.docx`.
2. Abre Microsoft Copilot.
3. En **Agentes**, abre **Asesor de escritura**. Si no aparece, utiliza la opción para ver o agregar todos los agentes disponibles.

## Desarrollo de la práctica

### Fase 1 - Revisar el borrador y abrir el Asesor de escritura

**Tiempo:** 4 min  
**Aplicación:** Word o visor de documentos + Asesor de escritura  
**Objetivo:** comprender la base factual que no debe cambiar durante la reescritura.

### Paso 1. Lee el borrador

Abre `borrador_revision_portafolio.docx` y localiza:

- desempeño del periodo y referencia interna;
- cambios de composición;
- tres aspectos que requieren atención;
- próximos pasos;
- ejemplos de repetición, párrafos extensos o tono inconsistente.

### Paso 2. Lleva el contenido al agente

Si el Asesor de escritura permite adjuntar el documento en tu interfaz, adjúntalo. Si no, copia el texto completo del borrador y pégalo junto con el PROMPT 1.

**Criterio de finalización:** el agente dispone del contenido completo del borrador y tú has identificado las cifras que deben mantenerse.

### Fase 2 - Diagnosticar el contenido sin reescribirlo

**Tiempo:** 8 min  
**Aplicación:** Asesor de escritura  
**Objetivo:** obtener un diagnóstico antes de generar cualquier versión nueva.

### Paso 1. Solicita el diagnóstico

> **PROMPT 1 - DIAGNÓSTICO SIN REESCRITURA**
>
> Evalúa el borrador adjunto o pegado, pero **no lo reescribas todavía**.  
> Identifica problemas de: extensión, estructura, claridad, propósito, repetición, longitud de párrafos y consistencia del tono.  
> Presenta el diagnóstico en una tabla con estas columnas: problema detectado, ubicación o fragmento de referencia, por qué dificulta la comunicación y cambio recomendado.  
> Separa los hallazgos del texto de cualquier sugerencia de estilo. No cambies cifras, hechos, próximos pasos ni introduzcas información nueva.

### Paso 2. Revisa el diagnóstico

Comprueba que el agente haya detectado problemas reales del borrador. No aceptes como `error` una cifra solo porque el agente considere que debería ser distinta.

**Criterio de finalización:** existe un diagnóstico separado de la reescritura y las recomendaciones no alteran los hechos.

### Fase 3 - Crear la versión para el cliente

**Tiempo:** 8 min  
**Aplicación:** Asesor de escritura  
**Objetivo:** convertir el borrador en una comunicación clara para una audiencia no técnica.

### Paso 1. Genera la versión externa

> **PROMPT 2 - VERSIÓN PARA EL CLIENTE**
>
> Ahora crea una versión dirigida al cliente a partir del mismo borrador.  
> Requisitos:  
> - conserva exactamente todas las cifras y hechos;  
> - deja visible desde el inicio el propósito de la comunicación;  
> - elimina repeticiones;  
> - usa párrafos breves y lenguaje claro;  
> - separa `Hallazgos de la revisión` de `Siguientes pasos`;  
> - evita tecnicismos innecesarios y evita un tono alarmista;  
> - no introduzcas recomendaciones de inversión nuevas ni hechos que no estén en el borrador.  
> Devuelve únicamente la comunicación final para el cliente.

### Paso 2. Compara con el borrador

Verifica las cifras de rendimiento, composición, concentración, duración y exposición en dólares. Si alguna cambió, pide una corrección antes de avanzar.

**Criterio de finalización:** existe una versión para cliente con propósito visible, estructura clara y las mismas cifras del borrador.

### Fase 4 - Crear la versión para el equipo interno

**Tiempo:** 7 min  
**Aplicación:** Asesor de escritura  
**Objetivo:** adaptar los mismos hechos a una audiencia interna que requiere mayor detalle técnico.

### Paso 1. Genera la versión interna

> **PROMPT 3 - VERSIÓN PARA EL EQUIPO INTERNO**
>
> Crea una segunda versión dirigida al equipo interno de CIBEST CAPITAL usando exactamente la misma base factual del borrador.  
> Mantén todas las cifras sin cambios y conserva los mismos hallazgos y siguientes pasos.  
> Utiliza mayor detalle técnico que en la versión para cliente, organiza la información en secciones y deja explícitos los cambios de composición, concentración, duración y exposición en dólares.  
> No inventes causas, decisiones, acuerdos, tolerancia al riesgo ni recomendaciones que no aparezcan en el borrador.  
> Devuelve únicamente la comunicación interna final.

### Paso 2. Revisa la profundidad

La versión interna puede ser más técnica, pero no debe introducir hechos adicionales. Si aparece una causa o decisión no presente en el borrador, solicita su eliminación.

**Criterio de finalización:** existe una versión interna más técnica que mantiene los mismos hechos y próximos pasos.

### Fase 5 - Comparar y validar consistencia factual

**Tiempo:** 5 min  
**Aplicación:** Asesor de escritura  
**Objetivo:** demostrar cómo cambian tono, estructura y profundidad sin alterar la base factual.

### Paso 1. Solicita la comparación final

> **PROMPT 4 - COMPARACIÓN DE AUDIENCIAS Y CONTROL FACTUAL**
>
> Compara la versión para cliente y la versión para el equipo interno.  
> Crea una tabla con: audiencia, propósito, tono, estructura, nivel de detalle y tecnicismo.  
> Después realiza un control factual contra el borrador original y enumera todas las cifras clave, indicando si son idénticas en las dos versiones.  
> Si detectas una diferencia factual, señálala sin intentar justificarla.

### Paso 2. Corrige cualquier diferencia

Si el control detecta una discrepancia, vuelve a la versión correspondiente y pide corregir únicamente esa diferencia manteniendo el resto del texto.

**Criterio de finalización:** las dos versiones muestran diferencias de tono, estructura y profundidad, pero conservan exactamente los hechos del borrador.

## Validación y pruebas finales

| # | Criterio | Estado |
|---|---|---|
| 1 | El diagnóstico se realizó antes de la reescritura. | ☐ |
| 2 | Existe una versión dirigida al cliente. | ☐ |
| 3 | Existe una versión dirigida al equipo interno. | ☐ |
| 4 | Las dos versiones conservan las mismas cifras del borrador. | ☐ |
| 5 | La versión del cliente es más clara y menos técnica que la versión interna. | ☐ |
| 6 | Hallazgos y siguientes pasos están diferenciados. | ☐ |
| 7 | No se añadieron causas, decisiones o hechos no presentes en el insumo. | ☐ |

## Solución de problemas

| Situación | Qué hacer |
|---|---|
| El agente reescribe durante el diagnóstico | Repite el PROMPT 1 destacando `no reescribas todavía` y solicita únicamente la tabla de diagnóstico. |
| Cambia una cifra | Señala la cifra del borrador y pide corregir solo ese dato, sin reescribir nuevamente todo el contenido. |
| La versión interna inventa causas o decisiones | Pide eliminar cualquier afirmación no sustentada por el borrador y conservar únicamente hechos presentes en el insumo. |
| No puedes adjuntar el DOCX | Copia el texto completo desde Word y pégalo en el mensaje junto con el prompt correspondiente. |
| El Asesor de escritura no aparece en la navegación | Busca **Todos los agentes** y agrega/abre el agente si el entorno del curso lo tiene habilitado. |

## Limpieza y conservación

- Conserva `borrador_revision_portafolio.docx` como insumo del laboratorio.
- Puedes conservar las dos versiones finales como texto o copiarlas a un documento si la política del entorno lo permite.
- No sustituyas el borrador original por una versión generada hasta haber completado el control factual.
- Todo el contenido del caso es ficticio y no debe presentarse como información real de un cliente.

## Resumen de la práctica

Diagnosticaste un borrador sin reescribirlo de inmediato, creaste dos comunicaciones para audiencias distintas y validaste que la adaptación de tono y profundidad no modificara los hechos ni las cifras.

## Referencia oficial de apoyo

- Microsoft Support - Agents built by Microsoft (Writing Coach): https://support.microsoft.com/en-us/microsoft-365-copilot/agents-built-by-microsoft
