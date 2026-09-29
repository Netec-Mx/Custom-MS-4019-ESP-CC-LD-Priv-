# Práctica 4 - Creación de un agente para consulta del proceso de vinculación de clientes de inversión

CIBEST CAPITAL desea facilitar a sus colaboradores la consulta de un procedimiento ficticio de vinculación de nuevos clientes de inversión. En esta práctica crearás un agente con **Agent Builder** usando cuatro documentos de laboratorio, configurarás su comportamiento y lo someterás a cinco pruebas diseñadas para comprobar respuestas directas, combinación de fuentes, documentación incompleta, ambigüedad y límites de conocimiento.

## Metadatos

| Campo | Detalle |
|---|---|
| Duración | 60 min |
| Complejidad | Intermedia |
| Nivel de Bloom | Crear / Evaluar |
| Tipo de actividad | Construcción y prueba de agente declarativo |
| Aplicaciones | Microsoft Copilot - Agent Builder |
| Modalidad | Individual |
| Insumos previos | Cuatro documentos ficticios en `recursos/` |
| Resultado | Agente de laboratorio configurado, probado y ajustado para responder únicamente desde sus fuentes |

## Distribución de tiempo

| Fase | Actividad | Tiempo |
|---|---|---:|
| 1 | Revisar fuentes y definir comportamiento | 10 min |
| 2 | Crear identidad e instrucciones del agente | 12 min |
| 3 | Agregar conocimiento y preguntas iniciales | 10 min |
| 4 | Ejecutar cinco pruebas funcionales | 18 min |
| 5 | Ajustar instrucciones y volver a probar | 10 min |
|  | **TOTAL** | **60 min** |

## Descripción general

Crearás un agente denominado **Vinculación CIBEST Lab** o un nombre equivalente aceptado por la interfaz. Debe quedar claro que utiliza información completamente ficticia para capacitación. El agente responderá sobre etapas del proceso, documentación requerida, responsables, documentación incompleta y siguientes pasos.

Las fuentes están diseñadas para ser complementarias y también omiten deliberadamente determinadas respuestas. El objetivo no es que el agente responda siempre, sino comprobar que sabe reconocer cuándo necesita pedir una aclaración o cuándo la información no existe en sus fuentes.

## Objetivos de aprendizaje

Al finalizar podrás:

- configurar nombre, descripción, instrucciones, conocimiento y preguntas iniciales en Agent Builder;
- restringir el comportamiento de un agente a las fuentes proporcionadas;
- diseñar instrucciones para evitar políticas, requisitos, excepciones o autorizaciones inventadas;
- probar un agente con casos directos, cruzados, incompletos, ambiguos y fuera de alcance;
- ajustar instrucciones a partir de evidencia observada en las pruebas.

## Escenario de la práctica

La práctica se desarrolla en el contexto de **CIBEST CAPITAL**. El agente se crea exclusivamente con información ficticia para capacitación y busca reducir el tiempo dedicado a localizar requisitos, responsables y pasos dentro de varios documentos.

## Prerrequisitos

- Experiencia funcional básica con Microsoft 365.
- Acceso a creación de agentes con Agent Builder en el entorno del curso.
- Capacidad para cargar archivos locales o seleccionar archivos autorizados desde OneDrive/SharePoint.

## Preparación del entorno

Antes de iniciar el cronómetro, confirma que existen estos archivos:

- `recursos/procedimiento_vinculacion_lab.docx`
- `recursos/matriz_requisitos_documentales_lab.docx`
- `recursos/roles_responsabilidades_lab.docx`
- `recursos/preguntas_frecuentes_lab.docx`

Todos los archivos indican que son ficticios y no representan políticas reales de CIBEST CAPITAL.

## Desarrollo de la práctica

### Fase 1 - Revisar fuentes y definir comportamiento

**Tiempo:** 10 min  
**Aplicación:** Word o visor de documentos + Microsoft Copilot  
**Objetivo:** comprender qué información existe y qué debe hacer el agente cuando falte contexto.

### Paso 1. Revisa rápidamente los cuatro documentos

Identifica dónde se encuentran:

- etapas del proceso;
- requisitos para persona natural, persona jurídica y cliente institucional;
- responsabilidades del Área Comercial, Equipo de Vinculación y Responsable de Validación;
- plazos ficticios y estados de seguimiento;
- preguntas para las que los documentos declaran que no existe respuesta.

### Paso 2. Abre Agent Builder

En Microsoft Copilot, selecciona **Nuevo agente**. Si tu interfaz ofrece una creación conversacional, puedes utilizarla; para esta práctica es preferible abrir la opción equivalente a **Omitir para configurar / Skip to configure** para ver directamente nombre, descripción, instrucciones, conocimiento y prompts.

**Criterio de finalización:** conoces el contenido básico de las fuentes y tienes abierta la configuración del nuevo agente.

### Fase 2 - Crear identidad e instrucciones del agente

**Tiempo:** 12 min  
**Aplicación:** Agent Builder  
**Objetivo:** definir alcance, restricciones y comportamiento esperado.

### Paso 1. Configura identidad

Usa estos valores o equivalentes que acepte tu interfaz:

- **Nombre:** `Vinculación CIBEST Lab`
- **Descripción:** `Agente de capacitación que responde consultas sobre el proceso ficticio de vinculación de clientes usando únicamente los documentos del laboratorio.`

### Paso 2. Configura las instrucciones

Copia el siguiente bloque completo en el campo **Instrucciones**.

> **PROMPT 1 - INSTRUCCIONES DEL AGENTE**
>
> Eres un asistente de capacitación para consultas sobre el proceso ficticio de vinculación de clientes de inversión de CIBEST CAPITAL.  
>  
> Reglas obligatorias:  
> - Responde en español.  
> - Basa tus respuestas exclusivamente en los documentos proporcionados como fuentes de conocimiento del laboratorio.  
> - Distingue requisitos según el tipo de caso consultado: persona natural, persona jurídica o cliente institucional.  
> - Cuando el tipo de caso sea necesario y el usuario no lo haya indicado, solicita una aclaración antes de enumerar requisitos.  
> - Cuando la respuesta requiera combinar información de varias fuentes, integra la información y menciona los documentos utilizados cuando sea posible.  
> - No inventes políticas, requisitos, plazos, excepciones, autorizaciones, consecuencias regulatorias ni decisiones.  
> - Si la respuesta no existe en las fuentes, indícalo claramente y orienta al usuario a consultar al área responsable.  
> - Si la documentación está incompleta, identifica únicamente los faltantes que puedan verificarse en la matriz y explica el siguiente paso usando el procedimiento y los roles.  
> - No uses información de la web ni conocimiento externo para completar vacíos del caso.  
> - Recuerda que todos los documentos son ficticios y se usan exclusivamente para capacitación.  
>  
> Formato: usa pasos numerados para procesos, viñetas para requisitos y una sección final `Fuentes utilizadas` cuando puedas identificar el origen de la respuesta.

Si tu interfaz ofrece un control para búsqueda web o conocimiento externo, desactívalo para esta práctica cuando sea posible; el objetivo es evaluar el comportamiento basado únicamente en los documentos del laboratorio.

**Criterio de finalización:** el agente tiene nombre, descripción e instrucciones completas que obligan a reconocer ambigüedad y falta de información.

### Fase 3 - Agregar conocimiento y preguntas iniciales

**Tiempo:** 10 min  
**Aplicación:** Agent Builder  
**Objetivo:** conectar las cuatro fuentes del laboratorio y ofrecer consultas iniciales útiles.

### Paso 1. Agrega los cuatro documentos

En la sección **Conocimiento**, utiliza la opción disponible para **Cargar**, **Examinar** o adjuntar archivos de trabajo. Agrega exactamente los cuatro archivos indicados en Preparación del entorno.

Confirma que los cuatro aparecen listados antes de continuar.

### Paso 2. Configura preguntas iniciales

Agrega tres prompts o inicios de conversación, si la interfaz los admite:

1. `¿Cuáles son las etapas del proceso de vinculación del laboratorio?`
2. `¿Qué documentos se requieren según el tipo de caso?`
3. `¿Qué sucede si la documentación está incompleta?`

### Paso 3. Crea el agente

Utiliza **Crear** cuando la configuración esté completa. No compartas el agente en esta práctica; el uso compartido se aborda posteriormente en el curso.

**Criterio de finalización:** el agente fue creado con las cuatro fuentes y dispone de preguntas iniciales o equivalentes.

### Fase 4 - Ejecutar cinco pruebas funcionales

**Tiempo:** 18 min  
**Aplicación:** Agente creado  
**Objetivo:** comprobar cinco comportamientos definidos expresamente en el temario.

Ejecuta los siguientes casos uno por uno. No corrijas las instrucciones hasta completar los cinco; registra qué funcionó y qué debe ajustarse.

#### Prueba 1 - Pregunta directa

> **PROMPT 2 - PREGUNTA DIRECTA**
>
> ¿Cuáles son las etapas del proceso de vinculación del laboratorio desde la recepción de la solicitud hasta la finalización?

**Qué revisar:** la respuesta debe seguir el procedimiento y no añadir etapas ajenas a la fuente.

#### Prueba 2 - Consulta que combina dos o más documentos

> **PROMPT 3 - CONSULTA CRUZADA**
>
> Para un cliente institucional, ¿qué documentos obligatorios exige el laboratorio y qué rol revisa o valida cada uno? Indica las fuentes utilizadas.

**Qué revisar:** la respuesta debe combinar la matriz de requisitos con los roles/responsabilidades.

#### Prueba 3 - Documentación incompleta

> **PROMPT 4 - CASO INCOMPLETO**
>
> Caso de laboratorio: una persona jurídica entregó el formulario LAB-01 y el documento constitutivo, pero no entregó la identificación del representante ni la declaración LAB-BENEF. ¿Qué falta y cuál es el siguiente paso según las fuentes?

**Qué revisar:** debe identificar únicamente los faltantes documentados y explicar que el expediente queda pendiente; no debe inventar una excepción.

#### Prueba 4 - Pregunta ambigua

> **PROMPT 5 - PREGUNTA AMBIGUA**
>
> ¿Qué documentos debo presentar para vincular un cliente?

**Qué revisar:** el agente debe pedir el tipo de caso antes de dar una lista cerrada de requisitos.

#### Prueba 5 - Respuesta inexistente en las fuentes

> **PROMPT 6 - LÍMITE DE CONOCIMIENTO**
>
> ¿Cuál es la multa o consecuencia regulatoria aplicable si un expediente queda incompleto?

**Qué revisar:** el agente debe reconocer que las fuentes no contienen esa respuesta y orientar a consultar al área responsable. No debe buscar o inventar una consecuencia externa.

**Criterio de finalización:** se ejecutaron las cinco pruebas y se registró si cada comportamiento fue correcto o necesita ajuste.

### Fase 5 - Ajustar instrucciones y volver a probar

**Tiempo:** 10 min  
**Aplicación:** Agent Builder + agente creado  
**Objetivo:** mejorar el comportamiento con base en resultados observados, no en suposiciones.

### Paso 1. Edita solo lo necesario

Si una o más pruebas fallaron, abre la configuración del agente y ajusta las instrucciones. Ejemplos:

- si respondió una pregunta ambigua sin aclarar el tipo de caso, refuerza la regla de aclaración;
- si inventó una respuesta fuera de las fuentes, refuerza la prohibición de conocimiento externo y la regla de reconocer límites;
- si no citó fuentes, refuerza la sección `Fuentes utilizadas`.

No cambies los documentos para ocultar un problema de instrucciones.

### Paso 2. Repite las pruebas que fallaron

Vuelve a ejecutar únicamente los casos que no cumplieron el criterio esperado.

### Paso 3. Registra el estado final

Marca cada caso como **Cumple** o **Requiere revisión**. La salida generativa puede variar; el criterio es el comportamiento, no una frase exacta.

**Criterio de finalización:** el agente responde desde las fuentes, pide aclaraciones cuando corresponde y reconoce límites de conocimiento.

## Validación y pruebas finales

| # | Criterio | Estado |
|---|---|---|
| 1 | El agente indica que usa información ficticia de capacitación. | ☐ |
| 2 | Se añadieron exactamente cuatro documentos de conocimiento. | ☐ |
| 3 | Las instrucciones prohíben inventar políticas, requisitos, excepciones y autorizaciones. | ☐ |
| 4 | La pregunta directa se responde desde el procedimiento. | ☐ |
| 5 | La consulta cruzada combina requisitos y roles. | ☐ |
| 6 | El caso incompleto identifica faltantes y siguiente paso sin inventar excepciones. | ☐ |
| 7 | La pregunta ambigua provoca una solicitud de aclaración. | ☐ |
| 8 | La pregunta fuera de las fuentes produce un reconocimiento de limitación. | ☐ |
| 9 | Se ajustaron instrucciones solo cuando las pruebas demostraron la necesidad. | ☐ |

## Solución de problemas

| Situación | Qué hacer |
|---|---|
| No aparece **Nuevo agente** | Confirma que la cuenta y la configuración del tenant permiten crear agentes con Agent Builder. |
| No puedes cargar los documentos | Usa la opción equivalente para adjuntar archivos de trabajo o súbelos previamente a una ubicación de OneDrive/SharePoint a la que tengas acceso y selecciónalos desde allí. |
| El agente usa información externa | Desactiva búsqueda web si está disponible y refuerza en instrucciones que solo debe usar las fuentes del laboratorio. |
| No pide aclaración en la prueba ambigua | Añade una regla explícita: `si el tipo de caso no está indicado, pregunta si es persona natural, persona jurídica o cliente institucional antes de responder`. |
| No encuentra una respuesta que sí existe | Confirma que el archivo correcto está en Conocimiento y formula la pregunta usando el término que aparece en la fuente; después vuelve a probar. |

## Limpieza y conservación

- Conserva los cuatro documentos de `recursos/` para repetir o auditar las pruebas.
- Conserva el agente únicamente dentro del entorno de capacitación y de acuerdo con las políticas de la organización.
- No compartas el agente como si contuviera políticas reales de CIBEST CAPITAL.
- No reemplaces los documentos ficticios por documentación sensible sin autorización.

## Resumen de la práctica

Revisaste cuatro fuentes ficticias, configuraste un agente en Agent Builder, cargaste su conocimiento, ejecutaste cinco tipos de prueba y ajustaste sus instrucciones según evidencia observable.

## Referencias oficiales de apoyo

- Microsoft Learn - Agent Builder in Microsoft 365 Copilot: https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/agent-builder
- Microsoft Learn - Add knowledge sources to your agent: https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/agent-builder-add-knowledge
- Microsoft Support - Build your own agent with Microsoft Copilot: https://support.microsoft.com/en-US/Microsoft-365-Copilot/build-your-own-agent-with-microsoft-365-copilot
