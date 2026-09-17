# Práctica: Creación de un agente para consulta del proceso de vinculación de clientes de inversión

## 1. Metadatos del laboratorio

| Atributo | Detalle |
|---|---|
| **Duración** | 60 minutos |
| **Complejidad** | Alta |
| **Nivel de Bloom** | Crear |
| **Módulo** | 3 — Creación de agentes personalizados |
| **Laboratorios previos requeridos** | Lab 02-00-01, Lab 02-00-02, Lab 02-00-03 |

---

## 2. Descripción general

En este laboratorio crearás un agente personalizado denominado **"Asistente de Vinculación de Clientes"** utilizando Microsoft Copilot Agent Builder. El agente responderá preguntas sobre el proceso interno de onboarding de nuevos clientes de inversión, consultando en tiempo real los documentos almacenados en SharePoint (manual de vinculación, formularios KYC, checklist de onboarding y política AML). El laboratorio cubre el ciclo completo: exploración de componentes, creación desde Copilot Chat, creación alternativa desde SharePoint, pruebas con casos predefinidos y administración de permisos y publicación.

---

## 3. Objetivos de aprendizaje

Al completar este laboratorio serás capaz de:

- [ ] Explorar y describir los componentes fundamentales de un agente de Copilot (nombre, descripción, instrucciones del sistema, fuentes de conocimiento, acciones y configuración de conversación) mediante un ejercicio de mapeo previo a la construcción.
- [ ] Crear un agente personalizado completo en Copilot Chat usando Agent Builder, configurando nombre, descripción, instrucciones del sistema, fuentes de conocimiento de SharePoint y comportamientos de conversación.
- [ ] Crear una versión alternativa del agente directamente desde SharePoint Online y comparar las diferencias de configuración y capacidades frente al agente creado en Copilot Chat.
- [ ] Probar el agente con casos de consulta predefinidos del proceso de vinculación de clientes, editar su configuración en función de los resultados y administrar permisos de uso compartido.
- [ ] Evaluar la calidad de las respuestas del agente verificando que cite correctamente los documentos fuente y respete los límites definidos en las instrucciones del sistema.

---

## 4. Prerrequisitos

### Conocimientos previos

| Requisito | Descripción |
|---|---|
| Laboratorios del Módulo 2 completados | Haber realizado los Labs 02-00-01, 02-00-02 y 02-00-03 para contar con contexto del dominio de gestión de inversiones |
| Componentes de un agente | Comprensión de los cuatro componentes (instrucciones, conocimiento, acciones e identidad) según la Lección 3.1 |
| Navegación en SharePoint Online | Capacidad de navegar bibliotecas de documentos, carpetas y verificar permisos |
| Prompt engineering básico | Experiencia redactando prompts claros y estructurados (practicado en Módulo 2) |

### Acceso y permisos requeridos

| Recurso | Requisito |
|---|---|
| Licencia Microsoft 365 Copilot Premium | Activa y asignada al menos 24 horas antes del laboratorio |
| Copilot Chat | Acceso en `https://m365.cloud.microsoft/chat` |
| Agent Builder | Disponible dentro de Copilot Chat (requiere licencia Premium) |
| Sitio SharePoint del curso | Rol de **Propietario** en `https://[tenant].sharepoint.com/sites/CursoAgentes` |
| Carpeta de documentos | Archivos verificados en `/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` |

---

## 5. Entorno del laboratorio

### Archivos requeridos en SharePoint

Antes de iniciar, verifica que los siguientes archivos existan en la ruta indicada:

| Archivo | Ruta en SharePoint |
|---|---|
| `manual_vinculacion_clientes_v2.pdf` | `/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` |
| `formularios_KYC_2024.pdf` | `/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` |
| `checklist_onboarding.docx` | `/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` |
| `politica_AML_interna.pdf` | `/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` |

### Software y versiones

| Software | Versión mínima |
|---|---|
| Microsoft Edge | 124.0.2478.97 o superior |
| Microsoft 365 Copilot Chat | Build de producción mayo 2024 |
| Microsoft Copilot Agent Builder | 1.0.0 (integrado en M365 Copilot) |
| Microsoft SharePoint Online | 16.0.24211.12000 |
| Microsoft Teams | 24193.1805.3040.1579 |

### Verificación inicial del entorno

1. Abre Microsoft Edge y navega a `https://m365.cloud.microsoft/chat`.
2. Inicia sesión con tu cuenta del tenant del curso.
3. Confirma que en la interfaz de Copilot Chat aparece el botón **"Crear agente"** o el ícono de agentes en la barra lateral derecha. Si no aparece, tu licencia Copilot Premium no está activa — contacta al administrador.
4. En una pestaña separada, navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/` y confirma que los cuatro archivos están presentes y que puedes abrirlos.

---

## 6. Instrucciones paso a paso

### Paso 1: Ejercicio de mapeo de componentes del agente (10 minutos)

**Objetivo:** Planificar la arquitectura del agente antes de construirlo, mapeando cada componente según el marco de la Lección 3.1.

**Instrucciones:**

1. Abre un documento nuevo en tu editor de texto preferido (Bloc de notas, Word o directamente en un archivo `.txt`). Nómbralo `instrucciones_agente_vinculacion.txt`.

2. Crea la siguiente estructura y complétala con la información proporcionada a continuación. Este archivo servirá como referencia durante la construcción y será reutilizado en el Lab 03-00-02:

```text
============================================================
MAPEO DE COMPONENTES — AGENTE: ASISTENTE DE VINCULACIÓN DE CLIENTES
============================================================

1. IDENTIDAD
   - Nombre: Asistente de Vinculación de Clientes
   - Descripción: Agente especializado en el proceso de vinculación 
     (onboarding) de nuevos clientes de inversión. Responde preguntas 
     sobre requisitos KYC, documentación necesaria, pasos del proceso 
     de vinculación, políticas AML y checklist de incorporación.
   - Icono: Usar icono predeterminado o seleccionar uno relacionado 
     con finanzas/personas.

2. INSTRUCCIONES DEL SISTEMA
   [Ver texto completo en la instrucción 3 de este paso]

3. CONOCIMIENTO (Fuentes de datos)
   - Sitio SharePoint: https://[tenant].sharepoint.com/sites/CursoAgentes
   - Carpeta: /Documentos compartidos/Lab-03-00-01/ProcesosVinculacion/
   - Archivos específicos:
     a) manual_vinculacion_clientes_v2.pdf
     b) formularios_KYC_2024.pdf
     c) checklist_onboarding.docx
     d) politica_AML_interna.pdf

4. ACCIONES
   - Búsqueda en documentos de SharePoint (nativa de Agent Builder)
   - No se configurarán acciones adicionales (conectores/APIs) en 
     este laboratorio.

5. COMPORTAMIENTO DE CONVERSACIÓN
   - Inicios de conversación sugeridos (starters):
     a) "¿Cuáles son los pasos para vincular un nuevo cliente?"
     b) "¿Qué documentos necesito para el proceso KYC?"
     c) "¿Cuál es la política AML vigente?"
============================================================
```

3. Redacta las instrucciones del sistema completas. Copia el siguiente texto en la sección 2 de tu archivo de mapeo:

```text
Eres el Asistente de Vinculación de Clientes de la firma de gestión 
de inversiones. Tu función principal es ayudar al equipo de operaciones 
y cumplimiento a consultar información sobre el proceso de vinculación 
(onboarding) de nuevos clientes de inversión.

REGLAS DE COMPORTAMIENTO:
- Responde siempre en español, de forma clara, profesional y concisa.
- Basa tus respuestas exclusivamente en los documentos proporcionados 
  como fuentes de conocimiento (manual de vinculación, formularios KYC, 
  checklist de onboarding y política AML).
- Cuando cites información, indica el nombre del documento fuente 
  entre corchetes, por ejemplo: [manual_vinculacion_clientes_v2.pdf].
- Si una pregunta no puede responderse con la información disponible 
  en los documentos, indica claramente: "No encontré esta información 
  en los documentos del proceso de vinculación. Te recomiendo consultar 
  directamente con el área de Cumplimiento."
- No inventes procedimientos, plazos ni requisitos que no estén 
  documentados en las fuentes proporcionadas.
- No proporciones asesoría legal ni regulatoria. Si el usuario 
  solicita interpretaciones legales, redirige al departamento jurídico.

FORMATO DE RESPUESTA:
- Usa listas numeradas para describir pasos de procesos.
- Usa viñetas para enumerar documentos o requisitos.
- Incluye siempre la referencia al documento fuente al final de 
  cada respuesta.

ALCANCE:
- Proceso de vinculación de clientes de inversión
- Requisitos KYC (Know Your Customer)
- Checklist de onboarding
- Políticas AML (Anti-Money Laundering) internas
- Formularios y documentación requerida
```

4. Guarda el archivo `instrucciones_agente_vinculacion.txt`. Lo usarás como referencia en los pasos siguientes y en el Lab 03-00-02.

5. Revisa tu mapeo y confirma que cada uno de los cuatro componentes (identidad, instrucciones, conocimiento, acciones) tiene contenido definido. Compara mentalmente con el diagrama de la Lección 3.1: ¿hay algún componente vacío o incompleto?

**Resultado esperado:** Un archivo de texto completo con el mapeo de los cuatro componentes del agente, listo para usar como guía de configuración.

**Verificación:**
- ✅ El archivo contiene las cinco secciones (identidad, instrucciones, conocimiento, acciones, comportamiento).
- ✅ Las instrucciones del sistema incluyen reglas de comportamiento, formato de respuesta y alcance.
- ✅ Las fuentes de conocimiento listan los cuatro archivos de SharePoint con su ruta completa.

---

### Paso 2: Creación del agente en Agent Builder — Parte 1: Identidad e instrucciones (10 minutos)

**Objetivo:** Crear la configuración básica del agente (nombre, descripción e instrucciones del sistema) en Copilot Chat Agent Builder.

**Instrucciones:**

1. Navega a `https://m365.cloud.microsoft/chat` en Microsoft Edge.

2. En la interfaz de Copilot Chat, localiza el panel lateral derecho. Haz clic en el ícono de **"Agentes"** (representado generalmente por un ícono de persona con engranaje o un ícono de rayo).

3. En el panel de agentes, haz clic en el botón **"Crear agente"** (o **"Create agent"** si la interfaz está en inglés). Se abrirá la interfaz de **Copilot Agent Builder**.

> **Nota:** Si no ves el botón "Crear agente", verifica que tu licencia M365 Copilot Premium esté activa. También confirma que el administrador del tenant haya habilitado la creación de agentes para usuarios.

4. En la pantalla de Agent Builder, localiza el campo **"Nombre del agente"** (Agent name). Escribe:

```
Asistente de Vinculación de Clientes
```

5. En el campo **"Descripción"** (Description), escribe:

```
Agente especializado en el proceso de vinculación (onboarding) de nuevos clientes de inversión. Responde preguntas sobre requisitos KYC, documentación necesaria, pasos del proceso de vinculación, políticas AML y checklist de incorporación.
```

6. Localiza el campo **"Instrucciones"** (Instructions). Este es el campo más importante del agente. Copia y pega el texto completo de instrucciones del sistema que redactaste en el Paso 1 (sección 2 de tu archivo de mapeo). El texto comienza con *"Eres el Asistente de Vinculación de Clientes..."* y termina con *"...Formularios y documentación requerida"*.

7. Verifica que el texto de instrucciones se haya pegado correctamente y que no haya caracteres extraños o saltos de línea inesperados. El campo de instrucciones acepta texto largo — no hay límite práctico para este laboratorio.

8. **No hagas clic en "Crear" ni en "Guardar" todavía.** Continuarás la configuración en el Paso 3.

9. Opcionalmente, si la interfaz permite seleccionar un **icono** para el agente, elige uno relacionado con finanzas o personas. Si no hay opción de icono personalizado, deja el icono predeterminado.

**Resultado esperado:** La interfaz de Agent Builder muestra el nombre "Asistente de Vinculación de Clientes", la descripción completa y las instrucciones del sistema en sus respectivos campos, sin errores de formato.

**Verificación:**
- ✅ El campo "Nombre" muestra exactamente: `Asistente de Vinculación de Clientes`.
- ✅ El campo "Descripción" contiene la descripción completa sin truncamiento.
- ✅ El campo "Instrucciones" contiene todo el texto del system prompt, incluyendo las secciones REGLAS DE COMPORTAMIENTO, FORMATO DE RESPUESTA y ALCANCE.
- ✅ No se ha hecho clic en "Crear" aún — la configuración está en progreso.

---

### Paso 3: Creación del agente en Agent Builder — Parte 2: Conocimiento y comportamiento de conversación (10 minutos)

**Objetivo:** Conectar las fuentes de conocimiento de SharePoint al agente y configurar los inicios de conversación sugeridos.

**Instrucciones:**

1. Continuando en la misma pantalla de Agent Builder del Paso 2, localiza la sección **"Conocimiento"** (Knowledge). Haz clic en el botón **"Agregar conocimiento"** (Add knowledge) o en el ícono **"+"**.

2. En el menú de opciones de fuentes de conocimiento, selecciona **"SharePoint"** o **"Archivos de SharePoint"** (SharePoint files).

3. En el campo de búsqueda o URL que aparece, ingresa la URL del sitio SharePoint del curso:

```
https://[tenant].sharepoint.com/sites/CursoAgentes
```

> **Importante:** Reemplaza `[tenant]` con el nombre real del tenant proporcionado por el instructor. Por ejemplo: `https://contoso.sharepoint.com/sites/CursoAgentes`.

4. Navega dentro de la estructura del sitio hasta la carpeta:

```
Documentos compartidos > Lab-03-00-01 > ProcesosVinculacion
```

5. Selecciona **los cuatro archivos** de la carpeta:
   - `manual_vinculacion_clientes_v2.pdf`
   - `formularios_KYC_2024.pdf`
   - `checklist_onboarding.docx`
   - `politica_AML_interna.pdf`

   Si la interfaz permite seleccionar la carpeta completa en lugar de archivos individuales, selecciona la carpeta `ProcesosVinculacion`. Ambos métodos son válidos.

6. Confirma la selección. Deberías ver los archivos (o la carpeta) listados en la sección de Conocimiento del agente.

7. Localiza la sección **"Inicios de conversación"** (Conversation starters). Si esta sección está disponible en la interfaz, agrega los siguientes tres inicios sugeridos:

   **Inicio 1:**
   ```
   ¿Cuáles son los pasos para vincular un nuevo cliente?
   ```

   **Inicio 2:**
   ```
   ¿Qué documentos necesito para el proceso KYC?
   ```

   **Inicio 3:**
   ```
   ¿Cuál es la política AML vigente?
   ```

> **Nota:** Si la interfaz de Agent Builder no muestra una sección de "Inicios de conversación" de forma explícita, omite este sub-paso. No todas las versiones de la interfaz exponen esta opción durante la creación inicial; podrás agregarlos después en la fase de edición.

8. Revisa toda la configuración del agente una última vez:
   - **Nombre:** Asistente de Vinculación de Clientes
   - **Descripción:** Completa y sin errores
   - **Instrucciones:** Texto completo del system prompt
   - **Conocimiento:** 4 archivos de SharePoint (o carpeta ProcesosVinculacion)
   - **Inicios de conversación:** 3 starters configurados (si la opción estaba disponible)

9. Haz clic en el botón **"Crear"** (Create) para finalizar la creación del agente.

10. Espera a que la interfaz confirme la creación exitosa. Deberías ver un mensaje de confirmación y ser redirigido a la vista del agente o a la pantalla de prueba.

**Resultado esperado:** El agente "Asistente de Vinculación de Clientes" se crea exitosamente. La interfaz muestra una confirmación y el agente aparece en tu lista de agentes personalizados. Las fuentes de conocimiento de SharePoint están vinculadas.

**Verificación:**
- ✅ Mensaje de confirmación de creación exitosa visible en pantalla.
- ✅ El agente aparece en la lista de "Mis agentes" (My agents) en el panel de agentes de Copilot Chat.
- ✅ Al hacer clic en el agente, se muestran las fuentes de conocimiento configuradas (4 archivos o carpeta de SharePoint).
- ✅ Las instrucciones del sistema son visibles al editar el agente.

---

### Paso 4: Creación alternativa del agente desde SharePoint Online (10 minutos)

**Objetivo:** Crear una versión alternativa del agente directamente desde la interfaz de SharePoint Online y comparar las diferencias con el método de Agent Builder en Copilot Chat.

**Instrucciones:**

1. Abre una nueva pestaña en Microsoft Edge y navega a la carpeta de documentos de vinculación en SharePoint:

```
https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-03-00-01/ProcesosVinculacion
```

2. Una vez en la vista de la biblioteca de documentos, busca en la barra de comandos superior o en el menú contextual la opción **"Crear un agente"** (Create an agent) o **"Copilot"**. Esta opción puede aparecer como:
   - Un botón directo en la barra de comandos de la biblioteca
   - Dentro del menú **"Automatizar"** (Automate)
   - En el panel de Copilot de SharePoint

> **Nota:** La ubicación exacta de esta opción varía según la versión de SharePoint Online. Si no encuentras la opción, consulta al instructor. El administrador del tenant debe haber habilitado la creación de agentes desde SharePoint en el Centro de Administración de SharePoint.

3. Al seleccionar "Crear un agente", SharePoint abrirá una interfaz simplificada de configuración. Observa que SharePoint **preselecciona automáticamente** los archivos de la carpeta actual como fuentes de conocimiento. Esta es una diferencia clave respecto al método de Copilot Chat.

4. Configura el agente alternativo con los siguientes datos:

   **Nombre:**
   ```
   Asistente Vinculación SP
   ```

   **Descripción:**
   ```
   Versión alternativa del agente de vinculación, creada desde SharePoint. Consulta documentos de onboarding de clientes de inversión.
   ```

5. En el campo de **instrucciones** (si está disponible en la interfaz de SharePoint), pega una versión simplificada:

```
Eres un asistente de vinculación de clientes de inversión. Responde 
preguntas sobre el proceso de onboarding basándote exclusivamente en 
los documentos de esta biblioteca. Responde en español y cita siempre 
el documento fuente. Si no encuentras la información, indícalo 
claramente.
```

> **Importante:** La interfaz de creación de agentes desde SharePoint suele ser más limitada que Agent Builder. Es posible que no permita instrucciones tan detalladas o que no ofrezca opciones de inicios de conversación. Esto es normal y es parte de la comparación que realizarás.

6. Verifica que los cuatro archivos de la carpeta `ProcesosVinculacion` aparezcan como fuentes de conocimiento seleccionadas.

7. Haz clic en **"Crear"** (Create) para generar el agente desde SharePoint.

8. Una vez creado, **documenta las diferencias observadas** entre ambos métodos de creación. Completa la siguiente tabla comparativa en tu archivo `instrucciones_agente_vinculacion.txt`:

```text
============================================================
COMPARACIÓN DE MÉTODOS DE CREACIÓN
============================================================

| Aspecto                        | Agent Builder (Copilot Chat) | Desde SharePoint       |
|--------------------------------|------------------------------|------------------------|
| Instrucciones detalladas       | Sí, campo extenso            | [Tu observación]       |
| Selección de conocimiento      | Manual (navegar y elegir)    | [Tu observación]       |
| Inicios de conversación        | Sí (si disponible)           | [Tu observación]       |
| Preselección de archivos       | No                           | [Tu observación]       |
| Icono personalizado            | [Tu observación]             | [Tu observación]       |
| Facilidad/rapidez de creación  | [Tu observación]             | [Tu observación]       |
| Nivel de control               | [Tu observación]             | [Tu observación]       |
```

**Resultado esperado:** Un segundo agente denominado "Asistente Vinculación SP" creado desde SharePoint, y una tabla comparativa documentada con las diferencias observadas entre ambos métodos.

**Verificación:**
- ✅ El agente "Asistente Vinculación SP" se creó exitosamente desde SharePoint.
- ✅ Los cuatro archivos de ProcesosVinculacion están vinculados como conocimiento del agente.
- ✅ La tabla comparativa está completada con observaciones reales en el archivo de texto.
- ✅ Se identificó al menos una diferencia significativa entre ambos métodos (por ejemplo: nivel de detalle en instrucciones, preselección automática de archivos, opciones de configuración disponibles).

---

### Paso 5: Prueba del agente con casos predefinidos (10 minutos)

**Objetivo:** Probar el agente "Asistente de Vinculación de Clientes" (creado en Agent Builder) con casos de consulta predefinidos y evaluar la calidad de las respuestas.

**Instrucciones:**

1. Regresa a la pestaña de Copilot Chat (`https://m365.cloud.microsoft/chat`).

2. En el panel de agentes, localiza y haz clic en **"Asistente de Vinculación de Clientes"** (el creado en los Pasos 2 y 3). Esto abrirá una conversación con el agente.

3. Si configuraste inicios de conversación, deberían aparecer como sugerencias en la pantalla. Si aparecen, haz clic en el primero para iniciar. Si no aparecen, escribe manualmente el primer caso de prueba.

4. **Caso de prueba 1 — Consulta de proceso general.** Escribe el siguiente prompt:

```
¿Cuáles son los pasos principales para vincular un nuevo cliente de inversión según el manual vigente?
```

5. Evalúa la respuesta del agente verificando:
   - ¿Describe pasos numerados del proceso de vinculación?
   - ¿Cita el documento fuente `manual_vinculacion_clientes_v2.pdf`?
   - ¿Responde en español?
   - ¿Usa el formato de lista numerada como se indicó en las instrucciones?

6. **Caso de prueba 2 — Consulta de documentación KYC.** Escribe:

```
¿Qué documentos debe presentar un cliente persona jurídica para completar el proceso KYC?
```

7. Evalúa la respuesta verificando:
   - ¿Lista los documentos requeridos para persona jurídica?
   - ¿Referencia el archivo `formularios_KYC_2024.pdf`?
   - ¿Usa viñetas para enumerar documentos (según las instrucciones)?

8. **Caso de prueba 3 — Consulta de política AML.** Escribe:

```
¿Cuáles son los principales controles de prevención de lavado de activos que se aplican durante la vinculación?
```

9. Evalúa la respuesta verificando:
   - ¿Describe controles AML del documento `politica_AML_interna.pdf`?
   - ¿Cita el documento fuente correctamente?

10. **Caso de prueba 4 — Prueba de límites (pregunta fuera de alcance).** Escribe:

```
¿Cuál es la interpretación legal del artículo 45 de la ley de mercado de valores para clientes extranjeros?
```

11. Evalúa la respuesta verificando:
    - ¿El agente indica que no puede proporcionar asesoría legal?
    - ¿Redirige al departamento jurídico según las instrucciones del sistema?
    - ¿Evita inventar una respuesta legal?

12. **Caso de prueba 5 — Consulta del checklist.** Escribe:

```
Necesito el checklist completo de onboarding. ¿Qué elementos debo verificar antes de activar la cuenta del cliente?
```

13. Evalúa la respuesta verificando:
    - ¿Proporciona elementos del checklist referenciando `checklist_onboarding.docx`?
    - ¿La respuesta es estructurada y completa?

14. Registra los resultados de tus cinco pruebas en el archivo `instrucciones_agente_vinculacion.txt` usando el siguiente formato:

```text
============================================================
RESULTADOS DE PRUEBAS DEL AGENTE
============================================================

Caso 1 - Proceso general:
  Respuesta correcta: [Sí/No/Parcial]
  Cita documento fuente: [Sí/No]
  Formato adecuado: [Sí/No]
  Observaciones: [Tu comentario]

Caso 2 - Documentación KYC:
  Respuesta correcta: [Sí/No/Parcial]
  Cita documento fuente: [Sí/No]
  Formato adecuado: [Sí/No]
  Observaciones: [Tu comentario]

Caso 3 - Política AML:
  Respuesta correcta: [Sí/No/Parcial]
  Cita documento fuente: [Sí/No]
  Formato adecuado: [Sí/No]
  Observaciones: [Tu comentario]

Caso 4 - Fuera de alcance (legal):
  Rechazó correctamente: [Sí/No]
  Redirigió al depto. jurídico: [Sí/No]
  Observaciones: [Tu comentario]

Caso 5 - Checklist onboarding:
  Respuesta correcta: [Sí/No/Parcial]
  Cita documento fuente: [Sí/No]
  Formato adecuado: [Sí/No]
  Observaciones: [Tu comentario]
```

**Resultado esperado:** Cinco pruebas ejecutadas con resultados documentados. El agente debería responder correctamente los casos 1, 2, 3 y 5 citando documentos fuente, y rechazar apropiadamente el caso 4 redirigiendo al departamento jurídico.

**Verificación:**
- ✅ Los cinco casos de prueba fueron ejecutados en la conversación con el agente.
- ✅ Al menos 3 de los 5 casos obtuvieron respuestas correctas con cita de documento fuente.
- ✅ El caso 4 (fuera de alcance) fue manejado correctamente: el agente no inventó una respuesta legal.
- ✅ Los resultados están documentados en el archivo de texto.

---

### Paso 6: Edición, administración de permisos y publicación (10 minutos)

**Objetivo:** Editar el agente para mejorar aspectos identificados en las pruebas, configurar permisos de uso compartido y preparar la publicación para el equipo.

**Instrucciones:**

1. En Copilot Chat, navega al panel de **"Agentes"** y localiza **"Asistente de Vinculación de Clientes"** en tu lista de agentes.

2. Haz clic en el menú de opciones del agente (tres puntos `...` o botón de edición) y selecciona **"Editar"** (Edit). Se abrirá nuevamente la interfaz de Agent Builder con la configuración actual.

3. **Ajuste de instrucciones basado en pruebas.** Revisa los resultados de tus pruebas del Paso 5. Si identificaste algún problema (por ejemplo, el agente no citó documentos en algún caso, o no rechazó correctamente una pregunta fuera de alcance), ajusta las instrucciones. Ejemplo de mejora — agrega al final de la sección REGLAS DE COMPORTAMIENTO:

```text
- Al responder sobre el checklist de onboarding, presenta TODOS los 
  elementos como una lista de verificación con casillas (☐).
- Cuando el usuario pregunte por requisitos para persona jurídica 
  versus persona natural, diferencia claramente ambos casos.
- Si el usuario pide información sobre rendimientos de fondos o 
  análisis de portafolios, indica que esos temas están fuera del 
  alcance de este agente y sugiere consultar con el equipo de 
  gestión de inversiones.
```

4. Haz clic en **"Guardar"** o **"Actualizar"** (Save/Update) para aplicar los cambios a las instrucciones.

5. **Configuración de permisos de uso compartido.** Localiza la opción de **"Compartir"** (Share) o **"Permisos"** (Permissions) del agente. Dependiendo de la interfaz, puede estar en:
   - El menú de opciones (`...`) del agente
   - Un botón "Compartir" en la vista de edición
   - La sección de configuración avanzada

6. Configura los permisos del agente:
   - **Solo yo** (Only me): Mantén esta opción seleccionada inicialmente para pruebas personales.
   - Observa las opciones disponibles de compartición:
     - Compartir con personas específicas
     - Compartir con un grupo de Microsoft 365
     - Publicar para toda la organización

7. Para efectos de este laboratorio, cambia el permiso a **"Personas específicas"** y agrega la dirección de correo de un compañero de clase (o del instructor) como usuario con acceso. Haz clic en **"Compartir"** o **"Enviar"**.

> **Nota:** Si la interfaz solicita que publiques el agente antes de compartirlo, procede con la publicación en el siguiente sub-paso.

8. **Publicación del agente.** Localiza el botón **"Publicar"** (Publish). Al hacer clic, revisa las opciones:
   - **Publicar solo para mí:** El agente solo es visible para ti.
   - **Publicar para la organización / equipo:** El agente se publica en el catálogo de Teams o en la tienda de agentes de la organización (requiere aprobación del administrador en algunos tenants).

9. Selecciona **"Publicar solo para mí"** por ahora. Si el instructor lo indica, selecciona la opción de publicar para el equipo.

10. Confirma la publicación. El agente debería mostrar un estado de **"Publicado"** o **"Activo"**.

11. **Verificación en Teams (opcional pero recomendada).** Abre Microsoft Teams en una nueva pestaña o en la aplicación de escritorio. Navega a la sección de **"Copilot"** o **"Chat"** y busca tu agente por nombre: `Asistente de Vinculación de Clientes`. Si lo publicaste para el equipo, debería aparecer en el catálogo de agentes.

12. Actualiza tu archivo `instrucciones_agente_vinculacion.txt` con una sección final:

```text
============================================================
ESTADO FINAL DEL AGENTE
============================================================

Agente principal (Agent Builder):
  Nombre: Asistente de Vinculación de Clientes
  Estado: Publicado
  Permisos: Compartido con [nombre del compañero/instructor]
  Instrucciones: Actualizadas con mejoras post-prueba
  Fuentes de conocimiento: 4 archivos de SharePoint confirmados

Agente alternativo (SharePoint):
  Nombre: Asistente Vinculación SP
  Estado: [Publicado/Borrador]
  Diferencias clave identificadas: [Tu resumen]
```

13. Guarda el archivo `instrucciones_agente_vinculacion.txt` en la carpeta de salida de SharePoint:

```
https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-03-00-02/
```

> Este archivo será utilizado como referencia en el Lab 03-00-02.

**Resultado esperado:** El agente ha sido editado con instrucciones mejoradas, los permisos de compartición están configurados y el agente está publicado. El archivo de documentación final está guardado en SharePoint.

**Verificación:**
- ✅ Las instrucciones del agente fueron actualizadas con al menos una mejora basada en los resultados de las pruebas.
- ✅ El agente fue compartido con al menos una persona adicional (compañero o instructor).
- ✅ El agente muestra estado "Publicado" o "Activo".
- ✅ El archivo `instrucciones_agente_vinculacion.txt` fue guardado en `/Documentos compartidos/Lab-03-00-02/`.
- ✅ El archivo contiene: mapeo de componentes, tabla comparativa, resultados de pruebas y estado final.

---

## 7. Validación y pruebas finales

Ejecuta la siguiente lista de verificación para confirmar que todos los entregables del laboratorio están completos:

| # | Criterio de validación | Estado |
|---|---|---|
| 1 | El archivo `instrucciones_agente_vinculacion.txt` existe en `/Lab-03-00-02/` con todas las secciones completas | ☐ |
| 2 | El agente "Asistente de Vinculación de Clientes" existe en la lista de "Mis agentes" en Copilot Chat | ☐ |
| 3 | El agente tiene 4 archivos de SharePoint configurados como fuentes de conocimiento | ☐ |
| 4 | El agente responde correctamente a la pregunta: "¿Cuáles son los pasos para vincular un nuevo cliente?" citando el documento fuente | ☐ |
| 5 | El agente rechaza apropiadamente preguntas legales fuera de su alcance | ☐ |
| 6 | El agente "Asistente Vinculación SP" existe como segundo agente creado desde SharePoint | ☐ |
| 7 | La tabla comparativa entre ambos métodos de creación está completada con observaciones reales | ☐ |
| 8 | El agente principal está publicado y compartido con al menos una persona adicional | ☐ |
| 9 | Las instrucciones del agente fueron editadas al menos una vez después de las pruebas iniciales | ☐ |

**Prueba final de integración:** Inicia una nueva conversación con el agente "Asistente de Vinculación de Clientes" y realiza la siguiente secuencia de preguntas en una sola sesión:

```
1. ¿Cuál es el primer paso del proceso de vinculación?
2. ¿Qué formularios KYC necesita una persona natural?
3. ¿Puedes darme asesoría legal sobre regulación bancaria?
```

El agente debe: responder las preguntas 1 y 2 con información de los documentos y rechazar la pregunta 3 redirigiendo al departamento jurídico. Si las tres respuestas son coherentes con las instrucciones configuradas, el laboratorio está completo.

---

## 8. Solución de problemas

### Problema 1: El agente no encuentra información en los documentos de SharePoint

**Síntomas:** Al hacer una pregunta al agente, responde con mensajes genéricos como "No tengo información sobre eso" o proporciona respuestas que no provienen de los documentos cargados, a pesar de que la información sí existe en los archivos de SharePoint.

**Causa:** Las fuentes de conocimiento no se vincularon correctamente durante la creación, o los archivos PDF no son indexables (por ejemplo, son PDFs escaneados como imagen sin OCR). También puede ocurrir si los permisos de SharePoint del usuario que ejecuta el agente no permiten acceso de lectura a los archivos.

**Solución:**
1. Edita el agente en Agent Builder y verifica que las fuentes de conocimiento muestren los 4 archivos correctamente vinculados.
2. Si los archivos no aparecen, elimínalos de la configuración y vuelve a agregarlos navegando a la carpeta `/Lab-03-00-01/ProcesosVinculacion/`.
3. Abre cada archivo PDF directamente en SharePoint para confirmar que el texto es seleccionable (no es una imagen escaneada). Si un PDF es una imagen, solicita al instructor una versión con texto OCR.
4. Verifica tus permisos en SharePoint: navega a la carpeta y confirma que puedes abrir y leer cada archivo. Si no tienes acceso, solicita al administrador que te asigne rol de Miembro en el sitio.
5. Espera 2-3 minutos después de vincular los archivos antes de probar nuevamente — la indexación de contenido puede tomar un momento.

### Problema 2: El botón "Crear agente" no aparece en Copilot Chat ni en SharePoint

**Síntomas:** Al acceder a Copilot Chat en `https://m365.cloud.microsoft/chat`, el panel de agentes no muestra la opción "Crear agente". En SharePoint, no aparece la opción de crear un agente desde la biblioteca de documentos.

**Causa:** La licencia Microsoft 365 Copilot Premium no está asignada o activada correctamente en la cuenta del estudiante, o el administrador del tenant no ha habilitado la funcionalidad de creación de agentes en las políticas de Copilot.

**Solución:**
1. Verifica tu licencia: navega a `https://myaccount.microsoft.com` > **Suscripciones** y confirma que aparece "Microsoft 365 Copilot" en la lista de licencias activas.
2. Si la licencia no aparece, contacta al administrador del tenant para que la asigne. La activación puede tardar hasta 24 horas.
3. Si la licencia está activa pero el botón no aparece, el administrador debe verificar en el **Centro de Administración de Microsoft 365** > **Configuración** > **Copilot** que la opción "Permitir a los usuarios crear agentes" esté habilitada.
4. Para la creación desde SharePoint específicamente, el administrador debe ir al **Centro de Administración de SharePoint** > **Configuración** y verificar que la creación de agentes de Copilot desde sitios de SharePoint esté habilitada.
5. Cierra sesión completamente de Microsoft 365, limpia la caché del navegador (Ctrl+Shift+Delete en Edge) y vuelve a iniciar sesión. En algunos casos, los cambios de licencia requieren un nuevo inicio de sesión para reflejarse.

---

## 9. Limpieza

> **Importante:** El agente "Asistente de Vinculación de Clientes" creado en este laboratorio **NO debe eliminarse**. Será referenciado conceptualmente en el Lab 03-00-02.

Realiza las siguientes acciones de limpieza:

1. **Agente alternativo de SharePoint:** El agente "Asistente Vinculación SP" puede conservarse para referencia futura o eliminarse si el instructor lo indica. Para eliminarlo:
   - Navega al panel de agentes en Copilot Chat
   - Localiza "Asistente Vinculación SP"
   - Haz clic en el menú de opciones (`...`) y selecciona **"Eliminar"** (Delete)
   - Confirma la eliminación

2. **Archivo de documentación:** Confirma que `instrucciones_agente_vinculacion.txt` está guardado en `/Documentos compartidos/Lab-03-00-02/`. No lo elimines — es insumo del siguiente laboratorio.

3. **Archivos fuente:** No elimines ni muevas los archivos de la carpeta `/Lab-03-00-01/ProcesosVinculacion/`. Estos archivos son las fuentes de conocimiento activas del agente y deben permanecer en su ubicación.

4. **Conversaciones de prueba:** Las conversaciones con el agente en Copilot Chat se almacenan en tu historial. No es necesario eliminarlas, pero puedes hacerlo si deseas mantener limpio tu historial seleccionando cada conversación y eligiendo "Eliminar".

---

## 10. Resumen

### Lo que lograste en este laboratorio

En 60 minutos completaste el ciclo completo de creación de un agente personalizado en Microsoft 365 Copilot:

- **Planificaste** la arquitectura del agente mapeando sus cuatro componentes (identidad, instrucciones, conocimiento y acciones) antes de abrir cualquier herramienta, aplicando la práctica recomendada de la Lección 3.1.
- **Construiste** el agente "Asistente de Vinculación de Clientes" en Agent Builder, configurando instrucciones detalladas del sistema con reglas de comportamiento, formato de respuesta y alcance operativo.
- **Conectaste** cuatro documentos de SharePoint como fuentes de conocimiento del agente, habilitando la consulta en tiempo real (RAG) sobre el proceso de vinculación de clientes.
- **Creaste** una versión alternativa desde SharePoint Online y documentaste las diferencias entre ambos métodos de creación.
- **Probaste** el agente con cinco casos predefinidos que cubrieron consultas dentro del alcance y fuera del alcance, evaluando la calidad de las respuestas y el cumplimiento de las instrucciones del sistema.
- **Editaste** las instrucciones basándote en los resultados de las pruebas, configuraste permisos de compartición y publicaste el agente.

### Conceptos clave reforzados

| Concepto | Aplicación en este laboratorio |
|---|---|
| Instrucciones del sistema (System Prompt) | Redacción de reglas de comportamiento, formato y alcance que controlan las respuestas del agente |
| RAG (Retrieval Augmented Generation) | Conexión de documentos de SharePoint como fuentes de conocimiento consultadas en tiempo real |
| Mapeo de componentes | Planificación previa de identidad, instrucciones, conocimiento y acciones antes de la construcción |
| Pruebas de límites | Verificación de que el agente rechaza consultas fuera de su alcance definido |
| Gestión de permisos | Configuración de quién puede acceder y usar el agente |

### Conexión con el siguiente laboratorio

El archivo `instrucciones_agente_vinculacion.txt` que generaste será utilizado como referencia en el **Lab 03-00-02**, donde profundizarás en la creación de agentes desde SharePoint con configuraciones más avanzadas. El agente "Asistente de Vinculación de Clientes" que publicaste permanecerá activo como ejemplo de referencia.

### Recursos adicionales

- [Creación de agentes en Microsoft 365 Copilot Chat — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-365-copilot/extensibility/copilot-chat-agent-builder)
- [Configuración de fuentes de conocimiento para agentes — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-365-copilot/extensibility/knowledge-sources)
- [Mejores prácticas para instrucciones de agentes — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-copilot-studio/guidance/building-effective-instructions)
- [Creación de agentes desde SharePoint — Microsoft Learn](https://learn.microsoft.com/es-es/sharepoint/create-agent-sharepoint)

---

# Práctica: Creación de un agente de SharePoint

## 1. Metadatos del Laboratorio

| Campo | Valor |
|---|---|
| **Duración** | 35 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Crear (Create) |
| **Laboratorio previo requerido** | Lab 03-00-01 |
| **Rol del estudiante en SharePoint** | Propietario del sitio `/sites/CursoAgentes` |

---

## 2. Descripción General

En este laboratorio crearás un agente personalizado denominado **"Consultor de Documentos de Inversión"** directamente desde la biblioteca de documentos de SharePoint Online, utilizando la funcionalidad nativa de agentes de Copilot en SharePoint. A diferencia del agente construido en Copilot Chat Agent Builder (Lab 03-00-01), este agente se origina desde el contexto documental de SharePoint, lo que le confiere un alcance de conocimiento delimitado automáticamente a la biblioteca seleccionada. El laboratorio culmina con una evaluación comparativa entre ambos enfoques de creación, cerrando el arco de aprendizaje del curso completo.

---

## 3. Objetivos de Aprendizaje

Al finalizar este laboratorio, serás capaz de:

- [ ] Identificar y describir los componentes específicos de un agente creado nativamente en SharePoint Online, diferenciándolos del agente creado en Copilot Chat (Lab 03-00-01)
- [ ] Crear un agente de SharePoint desde una biblioteca de documentos, configurando su alcance de conocimiento a una colección documental delimitada del sitio del curso
- [ ] Configurar el comportamiento conversacional del agente, incluyendo instrucciones de tono, restricciones de alcance y mensajes de bienvenida personalizados
- [ ] Probar el agente con consultas que crucen información de múltiples documentos generados durante el curso
- [ ] Administrar permisos de acceso del agente y comparar las capacidades administrativas frente al agente del Lab 03-00-01

---

## 4. Prerrequisitos

### Conocimiento Previo

| Requisito | Detalle |
|---|---|
| Lab 03-00-01 completado | El agente "Asistente de Vinculación de Clientes" debe estar publicado y funcional en Teams |
| Componentes de un agente | Comprensión de los cuatro componentes: instrucciones, conocimiento, acciones e identidad (Lección 3.1) |
| Navegación en SharePoint | Familiaridad con bibliotecas de documentos, permisos y configuración de sitios |
| Labs 02-00-01 a 02-00-03 | Haber generado los archivos de output de los laboratorios anteriores |

### Acceso y Licenciamiento

| Requisito | Verificación |
|---|---|
| Licencia Microsoft 365 Copilot Premium activa | Confirmar en `https://admin.microsoft.com` > Usuarios > [tu usuario] > Licencias |
| Rol de **Propietario** en el sitio SharePoint del curso | Confirmar en `https://[tenant].sharepoint.com/sites/CursoAgentes/_layouts/15/people.aspx` |
| Funcionalidad de agentes habilitada en el tenant | El administrador debe haberlo habilitado en el Centro de Administración de SharePoint |
| Microsoft Edge actualizado (v124+) | Confirmar en `edge://settings/help` |

---

## 5. Entorno del Laboratorio

### Archivos Requeridos en SharePoint

Antes de iniciar, verifica que los siguientes archivos existan en la biblioteca **Documentos compartidos** del sitio `https://[tenant].sharepoint.com/sites/CursoAgentes/`:

| Carpeta | Archivo | Origen |
|---|---|---|
| `/Lab-02-00-01/` | `datos_fondo_A_renta_variable_global.xlsx` | Pre-cargado |
| `/Lab-02-00-01/` | `datos_fondo_B_mixto_conservador.xlsx` | Pre-cargado |
| `/Lab-02-00-01/` | `datos_fondo_C_alternativo_diversificado.xlsx` | Pre-cargado |
| `/Lab-02-00-01/` | `benchmark_msci_world_2023.pdf` | Pre-cargado |
| `/Lab-02-00-02/` | `analisis_fondos_comparativo.docx` | Generado en Lab 02-00-01 |
| `/Lab-02-00-02/` | `informe_regulatorio_EEUU.docx` | Generado en Lab 02-00-02 |
| `/Lab-02-00-03/` | `borrador_comunicacion_portafolio.docx` | Pre-cargado |
| `/Lab-02-00-03/` | `comunicacion_portafolio_final.docx` | Generado en Lab 02-00-03 |
| `/Lab-03-00-01/ProcesosVinculacion/` | `manual_vinculacion_clientes_v2.pdf` | Pre-cargado |
| `/Lab-03-00-01/ProcesosVinculacion/` | `formularios_KYC_2024.pdf` | Pre-cargado |
| `/Lab-03-00-01/ProcesosVinculacion/` | `checklist_onboarding.docx` | Pre-cargado |
| `/Lab-03-00-01/ProcesosVinculacion/` | `politica_AML_interna.pdf` | Pre-cargado |

### Software Requerido

| Software | Versión Mínima | Propósito |
|---|---|---|
| Microsoft Edge | 124.0.2478.97 | Navegador principal |
| SharePoint Online | 16.0.24211.12000 | Plataforma de creación del agente |
| Microsoft 365 Copilot Chat | Build producción mayo 2024 | Plataforma de prueba |
| Microsoft Teams | 24193.1805.3040.1579 | Canal de distribución del agente |

---

## 6. Instrucciones Paso a Paso

### Paso 1: Verificar los archivos de la biblioteca de documentos y explorar la interfaz de agentes en SharePoint

**Objetivo:** Confirmar que todos los documentos necesarios están disponibles en la biblioteca de SharePoint y localizar la opción de creación de agentes nativos desde la interfaz de SharePoint.

**Instrucciones:**

1. Abre **Microsoft Edge** y navega a la URL del sitio del curso:
   ```
   https://[tenant].sharepoint.com/sites/CursoAgentes
   ```

2. En el panel de navegación izquierdo, haz clic en **Documentos** (o **Documentos compartidos**) para acceder a la biblioteca principal del sitio.

3. Verifica que las carpetas `Lab-02-00-01`, `Lab-02-00-02`, `Lab-02-00-03` y `Lab-03-00-01` estén visibles. Haz clic en cada una para confirmar que los archivos listados en la sección 5 están presentes.

4. Regresa a la vista raíz de la biblioteca **Documentos compartidos**. Observa la barra de comandos superior de la biblioteca.

5. En la barra de comandos, localiza el icono de **Copilot** (ícono de chispa/destello) en la esquina superior derecha de la biblioteca. Haz clic en él.

   > **Nota:** Si no ves el icono de Copilot, haz clic en los tres puntos (`...`) de la barra de comandos para ver opciones adicionales. Si aún no aparece, confirma con el administrador que la funcionalidad de agentes de Copilot en SharePoint está habilitada en el tenant.

6. Al hacer clic en el icono de Copilot, se abrirá un panel lateral de Copilot en SharePoint. En la parte inferior de este panel, o en su encabezado, busca la opción **"Crear agente"** (o **"Create agent"** si la interfaz está parcialmente en inglés).

7. **No hagas clic todavía en "Crear agente"**. Antes, observa el panel de Copilot en SharePoint y anota mentalmente los siguientes elementos:
   - El panel muestra el contexto de la biblioteca actual como fuente de conocimiento predeterminada.
   - Aparece una indicación de que el agente tendrá acceso a los documentos de esta biblioteca.
   - La interfaz muestra sugerencias de preguntas basadas en el contenido de la biblioteca.

**Resultado Esperado:**

- Todos los archivos de los Labs 02 y 03 están presentes en sus respectivas carpetas dentro de la biblioteca de documentos.
- El panel lateral de Copilot en SharePoint está visible y muestra la opción de **"Crear agente"**.
- El contexto de la biblioteca se identifica automáticamente como fuente de conocimiento.

**Verificación:**

- [ ] Las 4 carpetas de laboratorio (`Lab-02-00-01`, `Lab-02-00-02`, `Lab-02-00-03`, `Lab-03-00-01`) están visibles en la biblioteca.
- [ ] Los archivos generados en laboratorios anteriores (`analisis_fondos_comparativo.docx`, `informe_regulatorio_EEUU.docx`, `comunicacion_portafolio_final.docx`) están presentes en sus carpetas correspondientes.
- [ ] El icono de Copilot es visible en la barra de comandos de la biblioteca de SharePoint.
- [ ] La opción **"Crear agente"** es accesible desde el panel de Copilot.

---

### Paso 2: Crear el agente de SharePoint y mapear sus componentes

**Objetivo:** Crear el agente "Consultor de Documentos de Inversión" desde la interfaz nativa de SharePoint y configurar los componentes de identidad y conocimiento, identificando las diferencias con el proceso de creación en Copilot Chat Agent Builder.

**Instrucciones:**

1. Desde el panel lateral de Copilot en SharePoint (abierto en el paso anterior), haz clic en **"Crear agente"**.

2. Se abrirá la interfaz de configuración del agente de SharePoint. Esta interfaz presenta un formulario con varias secciones. Observa que, a diferencia de Copilot Chat Agent Builder, la **fuente de conocimiento ya está preconfigurada** con la biblioteca de documentos actual.

3. **Configura la Identidad del agente** con los siguientes valores:

   | Campo | Valor |
   |---|---|
   | **Nombre** | `Consultor de Documentos de Inversión` |
   | **Descripción** | `Agente especializado en consultar y analizar la biblioteca completa de documentos del curso de agentes, incluyendo análisis de fondos, informes regulatorios, comunicaciones de portafolio y procesos de vinculación de clientes de inversión.` |
   | **Icono** | Selecciona un icono de la galería que represente documentos o finanzas (por ejemplo, un icono de gráfico o libro). Si no hay galería disponible, deja el icono predeterminado. |

4. **Verifica el componente de Conocimiento.** En la sección de fuentes de conocimiento (Knowledge / Sources), confirma que aparece:
   ```
   Documentos compartidos - CursoAgentes
   ```
   Esta es la biblioteca completa del sitio SharePoint. El agente de SharePoint, por defecto, toma como alcance la biblioteca desde la cual fue creado.

5. **Amplía o ajusta el alcance de conocimiento** (si la interfaz lo permite):
   - Si la interfaz muestra la opción de seleccionar carpetas específicas, **no restrinjas** el alcance. Deja seleccionada la biblioteca completa para que el agente pueda cruzar información entre todos los documentos del curso.
   - Si la interfaz permite agregar fuentes adicionales (otros sitios o bibliotecas), **no agregues** fuentes adicionales en este momento.

6. **Documenta el mapeo de componentes.** Antes de continuar, completa mentalmente (o en un documento aparte) la siguiente tabla comparativa, que usarás en el Paso 5:

   | Componente | Agente SharePoint (este lab) | Agente Copilot Chat (Lab 03-00-01) |
   |---|---|---|
   | **Punto de creación** | Biblioteca de documentos de SharePoint | Interfaz de Copilot Chat |
   | **Conocimiento predeterminado** | Biblioteca de documentos del sitio (automático) | Requiere agregar fuentes manualmente |
   | **Alcance de conocimiento** | Delimitado a la biblioteca del sitio | Configurable a cualquier fuente de M365 |
   | **Identidad** | Nombre, descripción, icono | Nombre, descripción, icono |
   | **Instrucciones** | Se configuran en el siguiente paso | Se configuran durante la creación |

**Resultado Esperado:**

- La interfaz de creación del agente de SharePoint muestra los campos de identidad completados.
- La fuente de conocimiento muestra automáticamente la biblioteca **Documentos compartidos** del sitio `CursoAgentes`.
- El alcance de conocimiento abarca toda la biblioteca sin restricciones de carpeta.

**Verificación:**

- [ ] El nombre del agente es exactamente `Consultor de Documentos de Inversión`.
- [ ] La descripción refleja el alcance completo de documentos del curso.
- [ ] La fuente de conocimiento muestra la biblioteca `Documentos compartidos` del sitio `CursoAgentes`.
- [ ] No se han agregado fuentes de conocimiento externas al sitio.

---

### Paso 3: Configurar el comportamiento conversacional del agente

**Objetivo:** Redactar las instrucciones del agente que definan su tono, restricciones de alcance y comportamiento, y configurar un mensaje de bienvenida personalizado.

**Instrucciones:**

1. En la interfaz de configuración del agente, localiza la sección de **Instrucciones** (Instructions / System prompt / Comportamiento). Esta sección permite definir cómo debe comportarse el agente en cada conversación.

2. Ingresa las siguientes instrucciones en el campo correspondiente:

   ```
   Eres el Consultor de Documentos de Inversión del equipo de gestión 
   de inversiones. Tu función principal es ayudar a los usuarios a 
   consultar, analizar y cruzar información contenida en la biblioteca 
   de documentos del sitio SharePoint del curso.

   ALCANCE DE CONOCIMIENTO:
   - Tienes acceso a análisis comparativos de fondos de inversión 
     (renta variable global, mixto conservador y alternativo diversificado).
   - Tienes acceso a informes regulatorios del mercado estadounidense.
   - Tienes acceso a comunicaciones de portafolio dirigidas a clientes.
   - Tienes acceso a documentos de procesos de vinculación de clientes, 
     incluyendo manuales KYC, checklists de onboarding y políticas AML.

   REGLAS DE COMPORTAMIENTO:
   1. Responde siempre en español, de forma profesional y precisa.
   2. Cuando cites información de un documento, indica el nombre del 
      archivo fuente entre corchetes, por ejemplo: [analisis_fondos_comparativo.docx].
   3. Si una pregunta requiere cruzar información de múltiples documentos, 
      hazlo explícitamente indicando las fuentes consultadas.
   4. No inventes datos financieros. Si la información no está disponible 
      en los documentos de la biblioteca, indícalo claramente.
   5. No proporciones asesoría financiera personalizada ni recomendaciones 
      de inversión. Tu rol es informativo y consultivo.
   6. Cuando te pregunten sobre procesos de vinculación o KYC, basa tus 
      respuestas exclusivamente en los documentos de la carpeta 
      ProcesosVinculacion.

   TONO:
   - Profesional pero accesible.
   - Usa terminología financiera cuando sea apropiado, pero explica 
     conceptos técnicos si el usuario lo solicita.
   - Sé conciso en respuestas simples y detallado en análisis complejos.
   ```

3. Localiza la sección de **Mensaje de bienvenida** (Welcome message / Starter prompts). Si la interfaz ofrece esta opción, configura el siguiente mensaje:

   ```
   ¡Hola! Soy el Consultor de Documentos de Inversión. Puedo ayudarte 
   a consultar y analizar toda la documentación del curso, incluyendo:

   📊 Análisis comparativos de fondos de inversión
   📋 Informes regulatorios del mercado estadounidense
   ✉️ Comunicaciones de portafolio para clientes
   📁 Procesos de vinculación, KYC y políticas AML

   ¿En qué puedo ayudarte hoy?
   ```

4. Si la interfaz permite configurar **preguntas sugeridas** (Starter prompts / Conversation starters), agrega las siguientes:

   - `¿Cuáles son las principales diferencias entre los tres fondos de inversión analizados?`
   - `Resume los requisitos KYC para la vinculación de nuevos clientes de inversión.`
   - `¿Qué aspectos regulatorios del mercado estadounidense se destacan en el informe?`
   - `¿Cuál fue el mensaje principal de la comunicación de portafolio enviada a clientes?`

5. **No publiques el agente todavía.** Revisa toda la configuración antes de proceder al siguiente paso.

**Resultado Esperado:**

- Las instrucciones del agente están completas con las seis reglas de comportamiento, el alcance de conocimiento y la definición de tono.
- El mensaje de bienvenida está configurado con los cuatro temas de consulta.
- Las preguntas sugeridas están ingresadas (si la interfaz lo permite).

**Verificación:**

- [ ] Las instrucciones incluyen las seis reglas de comportamiento numeradas.
- [ ] Las instrucciones especifican que el agente debe citar el nombre del archivo fuente.
- [ ] Las instrucciones prohíben explícitamente la asesoría financiera personalizada.
- [ ] El mensaje de bienvenida lista las cuatro categorías de documentos disponibles.
- [ ] Se han configurado al menos 3 preguntas sugeridas (si la interfaz lo permite).

---

### Paso 4: Publicar y probar el agente con consultas cruzadas

**Objetivo:** Publicar el agente de SharePoint y ejecutar un ciclo de pruebas con preguntas que requieran cruzar información de múltiples documentos del curso, validando la precisión y el cumplimiento de las instrucciones configuradas.

**Instrucciones:**

1. Una vez revisada toda la configuración, haz clic en el botón **"Crear"** o **"Publicar"** (Create / Publish) en la interfaz de configuración del agente.

   > **Nota:** Dependiendo de la versión del tenant, el agente puede estar disponible inmediatamente o requerir unos minutos para indexar las fuentes de conocimiento. Si aparece un mensaje indicando que el agente se está preparando, espera hasta 2 minutos.

2. Una vez creado, el agente debería abrirse automáticamente en el panel de conversación de Copilot en SharePoint, o bien mostrará un enlace para iniciar una conversación. Haz clic en **"Iniciar conversación"** o equivalente.

3. **Prueba 1 — Consulta simple de un solo documento.** Escribe el siguiente prompt:

   ```
   ¿Cuáles son los principales hallazgos del análisis comparativo de fondos de inversión?
   ```

   **Evalúa la respuesta verificando que:**
   - El agente hace referencia al archivo `analisis_fondos_comparativo.docx`.
   - La respuesta menciona los tres fondos: renta variable global, mixto conservador y alternativo diversificado.
   - El tono es profesional y en español.
   - Cita la fuente entre corchetes según las instrucciones.

4. **Prueba 2 — Consulta cruzada entre documentos de diferentes carpetas.** Escribe:

   ```
   Compara los requisitos de vinculación de clientes del manual KYC con 
   los aspectos regulatorios mencionados en el informe del mercado 
   estadounidense. ¿Hay puntos en común?
   ```

   **Evalúa la respuesta verificando que:**
   - El agente consulta documentos de al menos dos carpetas diferentes (`Lab-03-00-01/ProcesosVinculacion/` y `Lab-02-00-02/`).
   - Indica explícitamente las fuentes consultadas.
   - Identifica puntos en común (si los hay) o indica claramente que los documentos abordan temas distintos.

5. **Prueba 3 — Validación de restricciones.** Escribe:

   ```
   ¿Me recomiendas invertir en el fondo de renta variable global o en 
   el mixto conservador?
   ```

   **Evalúa la respuesta verificando que:**
   - El agente **NO** proporciona una recomendación de inversión personalizada.
   - El agente indica que su rol es informativo y consultivo, conforme a la regla 5 de las instrucciones.
   - Opcionalmente, el agente puede ofrecer información comparativa objetiva sin emitir una recomendación.

6. **Prueba 4 — Consulta sobre información no disponible.** Escribe:

   ```
   ¿Cuál fue el rendimiento del fondo de renta variable global en el 
   primer trimestre de 2025?
   ```

   **Evalúa la respuesta verificando que:**
   - El agente indica que no tiene información sobre 2025 en la biblioteca de documentos.
   - No inventa datos financieros (regla 4 de las instrucciones).

7. Registra los resultados de cada prueba en la siguiente tabla:

   | Prueba | Criterio | Cumple (Sí/No) | Observaciones |
   |---|---|---|---|
   | Prueba 1 | Cita fuente correcta | | |
   | Prueba 1 | Tono profesional en español | | |
   | Prueba 2 | Cruza información de múltiples carpetas | | |
   | Prueba 2 | Indica fuentes consultadas | | |
   | Prueba 3 | Rechaza dar recomendación de inversión | | |
   | Prueba 4 | No inventa datos no disponibles | | |

**Resultado Esperado:**

- El agente responde correctamente a las cuatro pruebas.
- Las respuestas citan fuentes documentales entre corchetes.
- El agente respeta las restricciones de no recomendar inversiones y no inventar datos.
- Las consultas cruzadas identifican y referencian documentos de múltiples carpetas.

**Verificación:**

- [ ] Prueba 1: La respuesta referencia el archivo `analisis_fondos_comparativo.docx` y menciona los tres fondos.
- [ ] Prueba 2: La respuesta cruza información de al menos dos carpetas y cita ambas fuentes.
- [ ] Prueba 3: El agente no emite una recomendación de inversión personalizada.
- [ ] Prueba 4: El agente declara que la información de 2025 no está disponible en la biblioteca.
- [ ] Todas las respuestas están en español con tono profesional.

---

### Paso 5: Editar el agente y ajustar la configuración

**Objetivo:** Realizar ajustes al agente basándose en los resultados de las pruebas, demostrando el ciclo iterativo de edición y mejora continua.

**Instrucciones:**

1. Desde el panel de conversación del agente en SharePoint, localiza la opción de **"Editar agente"** (Edit agent). Esta opción generalmente aparece como un icono de lápiz o engranaje en el encabezado del panel de conversación, o bien en el menú de opciones (`...`) del agente.

   > **Nota:** Si el agente se abrió en Copilot Chat en lugar de SharePoint, navega de regreso a la biblioteca de documentos en `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos`, abre el panel de Copilot y selecciona tu agente desde la lista de agentes disponibles.

2. En la interfaz de edición, realiza los siguientes ajustes a las **instrucciones**. Agrega el siguiente párrafo al final de las instrucciones existentes:

   ```
   FORMATO DE RESPUESTAS:
   - Para consultas comparativas, presenta la información en formato 
     de tabla cuando sea posible.
   - Para resúmenes de documentos extensos, utiliza viñetas organizadas 
     por tema.
   - Al final de cada respuesta que cite múltiples fuentes, incluye una 
     sección "Fuentes consultadas:" con la lista de archivos referenciados.
   ```

3. Guarda los cambios haciendo clic en **"Guardar"** o **"Actualizar"** (Save / Update).

4. Regresa al panel de conversación y ejecuta la siguiente prueba para validar los ajustes:

   ```
   Haz una comparación entre la política AML interna y los requisitos 
   del checklist de onboarding. Presenta la información en formato 
   de tabla.
   ```

5. Verifica que la respuesta:
   - Presenta la información en formato de tabla (conforme al ajuste realizado).
   - Incluye una sección "Fuentes consultadas:" al final.
   - Referencia los archivos `politica_AML_interna.pdf` y `checklist_onboarding.docx`.

6. Si la respuesta no cumple con el formato esperado, regresa a la edición y ajusta las instrucciones de formato. Este ciclo de prueba-edición es parte natural del proceso de refinamiento de un agente.

**Resultado Esperado:**

- El agente ha sido editado exitosamente con las instrucciones de formato adicionales.
- La respuesta a la prueba post-edición muestra el formato de tabla solicitado.
- La sección "Fuentes consultadas:" aparece al final de la respuesta.

**Verificación:**

- [ ] Las instrucciones actualizadas incluyen la sección "FORMATO DE RESPUESTAS".
- [ ] La respuesta post-edición presenta información en formato de tabla.
- [ ] La respuesta incluye la sección "Fuentes consultadas:" con los archivos correctos.
- [ ] El ciclo edición → prueba se completó sin errores.

---

### Paso 6: Administrar permisos y realizar la comparación final

**Objetivo:** Configurar los permisos de acceso del agente de SharePoint, explorar las opciones de administración disponibles y completar una evaluación comparativa formal entre el agente de SharePoint y el agente de Copilot Chat del Lab 03-00-01.

**Instrucciones:**

1. Desde la interfaz de edición del agente (o desde la configuración del sitio SharePoint), localiza la sección de **Permisos** o **Compartir** (Permissions / Share) del agente.

2. Revisa la configuración de permisos predeterminada del agente. En un agente de SharePoint nativo, los permisos de acceso al agente están vinculados a los permisos del sitio SharePoint. Esto significa que:
   - Los **miembros** del sitio SharePoint pueden usar el agente.
   - Los **visitantes** del sitio pueden usar el agente solo si tienen permisos de lectura en la biblioteca.
   - Los **propietarios** del sitio pueden editar y administrar el agente.

3. Verifica que el agente está configurado para ser accesible por los miembros del sitio `CursoAgentes`. No modifiques los permisos predeterminados.

4. Si la interfaz ofrece la opción de **compartir el agente en Teams**, observa esta opción pero **no la ejecutes** en este momento. Toma nota de que esta funcionalidad está disponible.

5. Si la interfaz permite acceder a **Copilot Studio** para configuración avanzada (generalmente un enlace como "Editar en Copilot Studio" o "Configuración avanzada"), haz clic para explorar brevemente las opciones adicionales disponibles:
   - Observa si hay opciones de **acciones** (conectores, flujos de Power Automate).
   - Observa si hay opciones de **análisis** (métricas de uso, conversaciones).
   - Observa si hay opciones de **versionamiento** o historial de cambios.
   - **No realices cambios en Copilot Studio.** Regresa a SharePoint después de la exploración.

6. **Evaluación comparativa final.** Completa la siguiente tabla comparando ambos agentes creados durante el curso. Esta tabla constituye el entregable final del laboratorio:

   | Criterio de Comparación | Agente Copilot Chat (Lab 03-00-01): "Asistente de Vinculación de Clientes" | Agente SharePoint (Lab 03-00-02): "Consultor de Documentos de Inversión" |
   |---|---|---|
   | **Punto de creación** | Copilot Chat → Agent Builder | Biblioteca de documentos de SharePoint |
   | **Configuración de conocimiento** | Manual: se agregan fuentes específicas (carpetas, archivos, sitios) | Automática: hereda la biblioteca del sitio desde donde se crea |
   | **Alcance de conocimiento** | Flexible: cualquier fuente de M365 accesible | Delimitado: biblioteca del sitio SharePoint de origen |
   | **Facilidad de creación** | *(Completa con tu experiencia)* | *(Completa con tu experiencia)* |
   | **Control de instrucciones** | Campo de texto libre en Agent Builder | Campo de texto libre en la interfaz de SharePoint |
   | **Distribución en Teams** | Publicación directa a Teams desde Agent Builder | Compartir desde SharePoint con opción de agregar a Teams |
   | **Permisos de acceso** | Configurables independientemente del contenido | Heredados de los permisos del sitio SharePoint |
   | **Ideal para** | Agentes que necesitan fuentes de conocimiento diversas y distribución amplia | Agentes centrados en una biblioteca documental específica con permisos ya definidos |
   | **Acceso a Copilot Studio** | Sí, para configuración avanzada | Sí, para configuración avanzada |
   | **Caso de uso óptimo** | *(Completa con tu análisis)* | *(Completa con tu análisis)* |

7. Reflexiona y completa las celdas marcadas con *(Completa con tu experiencia/análisis)* basándote en tu experiencia directa con ambos laboratorios.

**Resultado Esperado:**

- Los permisos del agente de SharePoint están verificados y alineados con los permisos del sitio.
- La exploración de Copilot Studio (si está disponible) reveló opciones adicionales de configuración.
- La tabla comparativa está completada con observaciones basadas en la experiencia práctica del estudiante.

**Verificación:**

- [ ] Los permisos del agente reflejan los permisos del sitio SharePoint (miembros pueden usar, propietarios pueden editar).
- [ ] Se identificó la opción de compartir el agente en Teams (aunque no se ejecutó).
- [ ] La tabla comparativa tiene todas las celdas completadas, incluyendo las de experiencia personal.
- [ ] Se identificaron al menos 3 diferencias clave entre ambos enfoques de creación de agentes.

---

## 7. Validación y Pruebas Finales

Ejecuta las siguientes validaciones para confirmar que el laboratorio se completó exitosamente:

### Validación Funcional del Agente

| # | Validación | Método | Resultado Esperado |
|---|---|---|---|
| 1 | El agente existe y es accesible | Abrir el panel de Copilot en la biblioteca de SharePoint y seleccionar el agente | El agente "Consultor de Documentos de Inversión" aparece en la lista y se puede iniciar una conversación |
| 2 | El mensaje de bienvenida se muestra | Iniciar una nueva conversación con el agente | Se muestra el mensaje personalizado con las cuatro categorías de documentos |
| 3 | Las instrucciones se respetan | Preguntar: `¿Me recomiendas un fondo de inversión?` | El agente declina dar recomendaciones y explica su rol informativo |
| 4 | El conocimiento abarca toda la biblioteca | Preguntar: `Lista todos los documentos que puedes consultar` | El agente menciona documentos de múltiples carpetas (Labs 02 y 03) |
| 5 | El formato de respuestas funciona | Preguntar: `Compara los tres fondos de inversión en formato de tabla` | La respuesta incluye una tabla y la sección "Fuentes consultadas:" |

### Validación Administrativa

| # | Validación | Método | Resultado Esperado |
|---|---|---|---|
| 1 | El agente es editable | Acceder a la opción "Editar agente" desde el panel de Copilot | La interfaz de edición se abre con la configuración actual del agente |
| 2 | Los permisos son correctos | Revisar la sección de permisos del agente | Los permisos reflejan los roles del sitio SharePoint |
| 3 | La tabla comparativa está completa | Revisar las 10 filas de la tabla del Paso 6 | Todas las celdas están completadas con información específica |

---

## 8. Solución de Problemas

### Problema 1: El icono de Copilot no aparece en la barra de comandos de la biblioteca de SharePoint

**Síntomas:** Al navegar a la biblioteca de documentos del sitio `CursoAgentes`, no se muestra el icono de Copilot (chispa/destello) en la barra de comandos superior. El menú de opciones adicionales (`...`) tampoco contiene la opción de Copilot o "Crear agente".

**Causa:** La funcionalidad de agentes de Copilot en SharePoint no está habilitada en el tenant de Microsoft 365, o la licencia Microsoft 365 Copilot Premium no está correctamente asignada al usuario. Esta funcionalidad requiere habilitación explícita por parte del administrador del tenant en el Centro de Administración de SharePoint.

**Solución:**

1. Verifica tu licencia navegando a `https://www.microsoft.com/microsoft-365/copilot` e iniciando sesión. Si ves un mensaje indicando que no tienes acceso a Copilot, contacta al administrador del curso.

2. Solicita al administrador del tenant que verifique la habilitación en el **Centro de Administración de SharePoint**:
   - Navegar a `https://[tenant]-admin.sharepoint.com`.
   - Ir a **Configuración** > **Copilot en SharePoint** (o equivalente).
   - Confirmar que la opción de agentes de Copilot está habilitada para el sitio `CursoAgentes` o para todo el tenant.

3. Después de que el administrador realice los cambios, cierra completamente Microsoft Edge, espera 5 minutos y vuelve a abrir la biblioteca de documentos. Los cambios de configuración del tenant pueden tardar hasta 15 minutos en propagarse.

4. Si el problema persiste, intenta acceder desde una ventana de navegación InPrivate en Edge (`Ctrl + Shift + N`) para descartar problemas de caché.

---

### Problema 2: El agente no encuentra documentos de carpetas específicas al responder consultas cruzadas

**Síntomas:** Al realizar la Prueba 2 (consulta cruzada entre documentos de diferentes carpetas), el agente solo referencia documentos de una carpeta pero ignora los de otras carpetas de la biblioteca. Por ejemplo, responde con información de `Lab-03-00-01/ProcesosVinculacion/` pero no encuentra nada de `Lab-02-00-02/`.

**Causa:** El índice de búsqueda de SharePoint puede no haber procesado completamente todos los documentos de la biblioteca, especialmente si los archivos de output de los Labs 02 fueron subidos recientemente (menos de 30 minutos antes). SharePoint requiere tiempo para indexar nuevos documentos y hacerlos disponibles para Copilot.

**Solución:**

1. Verifica que los archivos existen en las carpetas correspondientes navegando manualmente a cada carpeta en la biblioteca de documentos.

2. Abre uno de los archivos no encontrados (por ejemplo, `informe_regulatorio_EEUU.docx`) directamente en SharePoint para confirmar que es accesible y no está corrupto.

3. Espera al menos 15-20 minutos desde la última carga de archivos para que el índice de SharePoint se actualice. Durante este tiempo, puedes continuar probando con documentos de carpetas que sí están siendo reconocidas.

4. Fuerza una re-indexación manual del sitio (si tienes permisos de administrador):
   - Navega a **Configuración del sitio** (`⚙️` > **Configuración del sitio**).
   - En la sección **Búsqueda**, selecciona **Volver a indizar el sitio**.
   - Confirma la re-indexación. Este proceso puede tardar entre 15 minutos y varias horas dependiendo del volumen de documentos.

5. Como alternativa inmediata, reformula la pregunta al agente incluyendo el nombre exacto del archivo:
   ```
   Busca información en el archivo informe_regulatorio_EEUU.docx sobre 
   aspectos regulatorios y compárala con los requisitos del archivo 
   politica_AML_interna.pdf
   ```
   Esto puede ayudar al agente a localizar los documentos específicos incluso si el índice no está completamente actualizado.

---

## 9. Limpieza del Entorno

Dado que este es el **laboratorio final del curso**, la limpieza depende de las instrucciones del administrador del tenant:

| Acción | Instrucción | ¿Obligatoria? |
|---|---|---|
| **Conservar el agente** | No elimines el agente "Consultor de Documentos de Inversión" hasta recibir instrucciones del instructor. Puede ser requerido para evaluación final. | Sí |
| **Conservar los documentos** | No elimines los archivos de la biblioteca de documentos de SharePoint. Son parte del registro del curso. | Sí |
| **Cerrar sesiones** | Cierra sesión en Microsoft 365 en todas las pestañas de Edge al finalizar el curso. | Sí |
| **Limpiar caché del navegador** | Si utilizaste un equipo compartido, limpia el historial y caché de Edge: `Ctrl + Shift + Delete` > selecciona "Todo el tiempo" > marca "Cookies", "Caché" e "Historial". | Solo en equipos compartidos |

> **Nota para el administrador:** Al finalizar el curso, el administrador del tenant puede eliminar el sitio `CursoAgentes` y revocar las licencias de Copilot Premium según las políticas de la organización. Se recomienda exportar la tabla comparativa del Paso 6 como entregable del curso antes de eliminar los recursos.

---

## 10. Resumen

### Lo que Lograste en Este Laboratorio

En este laboratorio completaste el ciclo de creación de agentes personalizados en Microsoft 365 Copilot, esta vez utilizando el método nativo de SharePoint Online:

1. **Exploraste** la interfaz de creación de agentes en SharePoint y verificaste que el conocimiento se preconfigura automáticamente desde la biblioteca de documentos del sitio.

2. **Creaste** el agente "Consultor de Documentos de Inversión" con identidad, conocimiento e instrucciones configuradas específicamente para consultar la biblioteca completa del curso.

3. **Configuraste** instrucciones detalladas que incluyen reglas de comportamiento, restricciones de alcance, definición de tono y formato de respuestas.

4. **Probaste** el agente con cuatro tipos de consultas: simple, cruzada, de restricción y de información no disponible, validando el cumplimiento de las instrucciones.

5. **Editaste** el agente en un ciclo iterativo de mejora, agregando instrucciones de formato y verificando su efecto.

6. **Administraste** los permisos del agente y completaste una evaluación comparativa entre los dos enfoques de creación de agentes del curso.

### Conclusión Comparativa Clave

| Aspecto | Usar Copilot Chat Agent Builder cuando... | Usar Agente Nativo de SharePoint cuando... |
|---|---|---|
| **Fuentes de conocimiento** | Necesitas combinar fuentes diversas (múltiples sitios, archivos individuales, web) | El conocimiento está concentrado en una biblioteca de documentos específica |
| **Permisos** | Necesitas control granular de acceso independiente del contenido | Los permisos del sitio SharePoint ya reflejan quién debe acceder al agente |
| **Velocidad de creación** | Tienes un caso de uso complejo que requiere configuración detallada | Necesitas un agente funcional rápidamente sobre documentos existentes |
| **Distribución** | Quieres publicar directamente en Teams como aplicación | Quieres que el agente esté disponible en el contexto de SharePoint |

### Recursos Adicionales

- [Crear un agente para un sitio de SharePoint — Microsoft Learn](https://learn.microsoft.com/es-es/sharepoint/create-agent-sharepoint)
- [Administrar agentes de Copilot en SharePoint — Microsoft Learn](https://learn.microsoft.com/es-es/sharepoint/manage-copilot-agents)
- [Información general sobre agentes de Microsoft 365 Copilot — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-365-copilot/extensibility/agents-overview)
- [Configuración de instrucciones, conocimiento y acciones en Copilot Studio — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-copilot-studio/microsoft-copilot-extend-copilot-extensions)
- [Controles de acceso y permisos en agentes de Microsoft 365 — Microsoft Learn](https://learn.microsoft.com/es-es/microsoft-365-copilot/extensibility/declarative-agent-permissions)
