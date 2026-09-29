# Práctica 5 - Creación de un agente de SharePoint

En esta práctica un usuario autorizado trabajará con el sitio de SharePoint de su organización y creará agentes usando dos puntos de entrada de SharePoint: la creación desde el sitio o biblioteca y la creación a partir de una selección de archivos. El contenido real utilizado debe ser autorizado por la organización.

## Metadatos

| Campo | Detalle |
|---|---|
| Duración | 35 min |
| Complejidad | Intermedia |
| Nivel de Bloom | Aplicar / Comparar |
| Tipo de actividad | Creación guiada de agentes de SharePoint |
| Aplicaciones | SharePoint Online + agentes de SharePoint |
| Modalidad | Demostración práctica guiada con usuario autorizado |
| Insumos previos | Sitio de SharePoint de la organización y archivos existentes autorizados |
| Resultado | Agentes de prueba creados desde el sitio/biblioteca y desde una selección de archivos, con su alcance identificado |

## Distribución de tiempo

| Fase | Actividad | Tiempo |
|---|---|---:|
| 1 | Confirmar sitio, permisos y contenido autorizado | 5 min |
| 2 | Crear un agente desde el sitio o biblioteca | 8 min |
| 3 | Crear un agente desde una selección de archivos | 10 min |
| 4 | Comprobar el alcance de ambos métodos | 7 min |
| 5 | Registrar el resultado y conservar o eliminar pruebas | 5 min |
|  | **TOTAL** | **35 min** |

## Descripción general

El temario establece que un usuario de la organización compartirá pantalla y será guiado para crear un agente con base en los archivos del sitio de la empresa. Esta guía mantiene ese escenario: **no incluye archivos preparados ni inventa nombres de sitios, bibliotecas o documentos**.

La práctica crea dos agentes de prueba breves para evidenciar la diferencia entre partir de un ámbito amplio del sitio/biblioteca y partir de archivos seleccionados. No se comparten los agentes con otros usuarios en esta práctica; el uso compartido se aborda en el módulo siguiente.

## Objetivos de aprendizaje

Al finalizar podrás:

- identificar los permisos mínimos necesarios para crear un agente en SharePoint;
- crear un agente desde el punto de entrada disponible en el sitio o la biblioteca;
- crear un agente a partir de archivos seleccionados;
- reconocer qué contenido queda dentro del alcance de cada agente;
- comprobar que el agente solo puede responder con información a la que el usuario tenga acceso y que haya sido incluida como fuente.

## Escenario de la práctica

Un usuario autorizado de la organización trabaja sobre el sitio real de SharePoint de la empresa. El instructor guía la secuencia durante la sesión, pero el usuario ejecuta las acciones con su propia cuenta y con archivos aprobados para la práctica.

## Prerrequisitos

- Microsoft Copilot disponible en el entorno de la organización según el licenciamiento definido para el curso.
- Permisos de edición en el sitio de SharePoint que se utilizará.
- Acceso a una biblioteca con archivos permitidos para la práctica.
- Autorización para crear agentes de prueba en ese sitio.

## Preparación del entorno

Esta preparación debe completarse antes de iniciar el tiempo de práctica:

1. El instructor o responsable del sitio confirma cuál sitio y biblioteca pueden utilizarse.
2. El usuario autorizado inicia sesión en SharePoint.
3. Se seleccionan previamente entre 2 y 5 archivos no sensibles que puedan usarse en la demostración.
4. Se confirma que el usuario puede abrir esos archivos y que dispone de permisos de edición en el sitio.

No utilices documentos confidenciales, datos personales o información no autorizada solo para completar la práctica.

## Desarrollo de la práctica

### Fase 1 - Confirmar sitio, permisos y contenido autorizado

**Tiempo:** 5 min  
**Aplicación:** SharePoint Online  
**Objetivo:** asegurar que la práctica se realiza sobre un ámbito permitido y que el usuario tiene acceso efectivo.

### Paso 1. Abre el sitio autorizado

Navega al sitio indicado por la organización. No cambies la URL ni utilices otro sitio sin autorización.

### Paso 2. Abre la biblioteca autorizada

Confirma que puedes:

- ver el contenido de la biblioteca;
- abrir los archivos elegidos para la práctica;
- identificar la opción de creación de agente disponible en tu interfaz.

Según la experiencia actual de SharePoint, la creación puede aparecer desde **Nuevo > Agente**, desde **Acciones de IA > Crear un agente** en una biblioteca o desde el menú contextual de archivos seleccionados. Si tu interfaz muestra un botón de Copilot u otra etiqueta equivalente, utiliza esa opción.

**Criterio de finalización:** el usuario está en el sitio correcto, puede abrir los archivos autorizados y ve una opción equivalente para crear un agente.

### Fase 2 - Crear un agente desde el sitio o biblioteca

**Tiempo:** 8 min  
**Aplicación:** SharePoint Online  
**Objetivo:** crear un primer agente usando el punto de entrada general disponible en el sitio o la biblioteca.

### Paso 1. Inicia la creación

Utiliza una de estas rutas, según lo que muestre tu interfaz:

- página principal del sitio: **Nuevo > Agente**;
- biblioteca: **Acciones de IA > Crear un agente**;
- botón de Copilot o comando equivalente disponible en el sitio.

### Paso 2. Revisa el ámbito propuesto

Antes de confirmar, revisa qué sitio, biblioteca, carpetas o archivos aparecen como fuentes. No añadas ubicaciones ajenas al sitio autorizado.

### Paso 3. Personaliza solo lo mínimo necesario

Asigna un nombre de prueba que identifique claramente el origen, por ejemplo:

`Agente práctica - biblioteca`

Si la interfaz solicita propósito o instrucciones, utiliza un texto equivalente a:

> **PROMPT 1 - PROPÓSITO DEL AGENTE DE BIBLIOTECA**
>
> Responde preguntas únicamente con información de las fuentes de SharePoint incluidas en este agente. Si la respuesta no está disponible en esas fuentes, indícalo. No inventes información ni uses el agente para modificar archivos.

Crea el agente.

**Criterio de finalización:** existe un agente de prueba creado desde el sitio o biblioteca y su ámbito de fuentes puede identificarse.

### Fase 3 - Crear un agente desde una selección de archivos

**Tiempo:** 10 min  
**Aplicación:** SharePoint Online  
**Objetivo:** crear un segundo agente cuyo conocimiento quede limitado a archivos seleccionados.

### Paso 1. Selecciona entre 2 y 5 archivos autorizados

En la biblioteca, selecciona únicamente los archivos aprobados para la práctica.

### Paso 2. Abre el comando de creación

Utiliza el menú contextual, los puntos suspensivos o la acción disponible para **Crear un agente** a partir de los archivos seleccionados.

### Paso 3. Revisa el ámbito

Confirma que las fuentes del agente corresponden a la selección realizada y que no se añadieron archivos fuera del conjunto autorizado.

### Paso 4. Identifica el agente

Usa un nombre de prueba como:

`Agente práctica - archivos`

Si se solicita propósito o instrucciones, utiliza:

> **PROMPT 2 - PROPÓSITO DEL AGENTE DE ARCHIVOS**
>
> Responde únicamente con información contenida en los archivos seleccionados para esta práctica. Si la respuesta no está disponible en esos archivos, indícalo claramente. No inventes información ni amplíes el alcance a otros documentos.

Crea el agente.

**Criterio de finalización:** existe un segundo agente cuyo ámbito corresponde a los archivos seleccionados.

### Fase 4 - Comprobar el alcance de ambos métodos

**Tiempo:** 7 min  
**Aplicación:** SharePoint Online  
**Objetivo:** evidenciar la diferencia entre crear desde un ámbito general y desde una selección específica.

### Paso 1. Formula una consulta verificable

Elige una pregunta cuya respuesta aparezca claramente en uno de los archivos seleccionados. No uses datos sensibles en el prompt.

> **PROMPT 3 - COMPROBACIÓN DE FUENTE**
>
> Responde esta pregunta únicamente usando las fuentes incluidas en este agente: [ESCRIBE AQUÍ UNA PREGUNTA BASADA EN UNO DE LOS ARCHIVOS AUTORIZADOS]. Indica qué fuente utilizaste cuando sea posible. Si la respuesta no está en el ámbito del agente, dilo explícitamente.

Ejecuta la misma pregunta en ambos agentes.

### Paso 2. Compara el alcance

Registra:

- qué fuentes tiene cada agente;
- si ambos pudieron responder;
- si la respuesta se mantiene dentro de las fuentes;
- qué diferencia produce haber creado el segundo agente desde archivos seleccionados.

No evalúes todavía edición avanzada, permisos de uso compartido o publicación en Teams; esos temas aparecen después en el curso.

**Criterio de finalización:** puedes explicar la diferencia de alcance entre el agente creado desde el sitio/biblioteca y el creado desde archivos seleccionados.

### Fase 5 - Registrar el resultado y conservar o eliminar pruebas

**Tiempo:** 5 min  
**Aplicación:** SharePoint Online  
**Objetivo:** dejar el entorno en el estado acordado por la organización.

### Paso 1. Registra los nombres y fuentes

Anota temporalmente:

- nombre del agente 1 y su ámbito;
- nombre del agente 2 y los archivos seleccionados;
- una observación breve sobre la diferencia entre ambos métodos.

### Paso 2. Aplica la decisión del responsable del sitio

- Si los agentes deben conservarse para las actividades posteriores del curso, mantenlos sin ampliar su uso compartido.
- Si eran únicamente pruebas, elimínalos siguiendo la opción disponible en SharePoint y la instrucción del responsable del sitio.

**Criterio de finalización:** el resultado está documentado y no quedan agentes de prueba innecesarios si la organización indicó eliminarlos.

## Validación y pruebas finales

| # | Criterio | Estado |
|---|---|---|
| 1 | El usuario trabajó en el sitio autorizado. | ☐ |
| 2 | El usuario tenía permisos de edición y acceso a los archivos utilizados. | ☐ |
| 3 | Se creó un agente desde el sitio o biblioteca. | ☐ |
| 4 | Se creó un agente desde una selección de archivos. | ☐ |
| 5 | El segundo agente quedó limitado a los archivos seleccionados. | ☐ |
| 6 | Se ejecutó al menos una consulta verificable en cada agente. | ☐ |
| 7 | Se identificó la diferencia de alcance entre ambos métodos. | ☐ |
| 8 | No se compartieron agentes con otros usuarios como parte de esta práctica. | ☐ |

## Solución de problemas

| Situación | Qué hacer |
|---|---|
| No aparece la opción para crear un agente | Confirma que la cuenta tiene la licencia necesaria y permisos de edición en el sitio; después busca la opción equivalente en **Nuevo**, **Acciones de IA** o el menú contextual. |
| La opción aparece en la biblioteca pero no en la página principal | Continúa desde la biblioteca; Microsoft puede mostrar distintos puntos de entrada según la experiencia habilitada. |
| El agente no usa un archivo seleccionado | Comprueba que el archivo sigue dentro de las fuentes del agente y que el usuario tiene acceso directo a ese archivo. |
| Una persona que prueba el agente no recibe información | Los agentes respetan los permisos de SharePoint; confirma que esa persona tiene acceso a las fuentes antes de interpretar el comportamiento como un error del agente. |
| El contenido elegido no puede usarse para capacitación | Detén la práctica y solicita al responsable del sitio otra selección autorizada. No copies el contenido a otra ubicación para eludir permisos. |

## Limpieza y conservación

- No se incluyen archivos de ejemplo en esta práctica porque el temario exige usar contenido del sitio de la organización.
- Conserva los agentes solo si el instructor o responsable del sitio los necesita para las actividades siguientes.
- No amplíes permisos ni compartas agentes con otros usuarios durante esta práctica.
- No dupliques documentos sensibles para facilitar la demostración.

## Resumen de la práctica

Creaste agentes desde dos puntos de entrada de SharePoint, verificaste las fuentes asociadas, ejecutaste una consulta de control y comparaste cómo cambia el ámbito cuando el agente se crea desde una selección específica de archivos.

## Referencias oficiales de apoyo

- Microsoft Support - Create an agent in SharePoint: https://support.microsoft.com/en-us/sharepoint/copilot-in-sharepoint/create-an-agent-in-sharepoint
- Microsoft Support - Get started with agents in SharePoint: https://support.microsoft.com/en-us/sharepoint/copilot-in-sharepoint/get-started-with-agents-in-sharepoint
