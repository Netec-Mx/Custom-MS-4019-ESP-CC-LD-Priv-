# Práctica: Análisis comparativo de fondos multiactivo para una revisión interna

## Metadatos del Laboratorio

| Campo | Detalle |
|---|---|
| **Duración** | 55 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Aplicar |
| **Tecnologías principales** | Microsoft 365 Copilot Chat, Agentes preconstruidos (Analista, Investigador, Asistente de solicitudes, Entrenador de ideas, Asesor de escritura), SharePoint Online, Word Online |
| **Archivos de salida** | `analisis_fondos_comparativo.docx`, `tabla_metricas_fondos.xlsx` |

---

## Descripción General

En este laboratorio aplicarás los cinco agentes preconstruidos de Microsoft 365 Copilot en un flujo de trabajo secuencial para realizar un análisis comparativo de tres fondos multiactivo simulados: Fondo A (Renta Variable Global), Fondo B (Mixto Conservador) y Fondo C (Alternativo Diversificado). Trabajarás con datos cuantitativos precargados en SharePoint —archivos Excel con métricas de rendimiento, volatilidad, Sharpe ratio y correlación de activos, además de un PDF de benchmark— y producirás un resumen ejecutivo profesional destinado a una audiencia interna de gestión de inversiones. Este es el primer laboratorio práctico del curso y establece la línea base de competencia en el uso de agentes preconstruidos.

---

## Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Aplicar el agente **Analista** para procesar, comparar y visualizar métricas cuantitativas de múltiples fondos multiactivo (rendimiento, volatilidad, Sharpe ratio, correlación de activos)
- [ ] Utilizar el agente **Investigador** para recopilar contexto de mercado y benchmarks relevantes que enriquezcan el análisis comparativo
- [ ] Emplear el agente **Asistente de solicitudes** para estructurar y gestionar peticiones de información entre las fases del flujo de análisis
- [ ] Aplicar el agente **Entrenador de ideas** para generar hipótesis y perspectivas analíticas adicionales sobre el desempeño diferencial de los fondos
- [ ] Usar el agente **Asesor de escritura** para redactar y pulir un resumen ejecutivo del análisis comparativo adecuado para gestión de inversiones

---

## Prerrequisitos

### Conocimientos Previos

| Conocimiento | Nivel requerido |
|---|---|
| Navegación básica en Microsoft 365 Copilot Chat | Familiaridad con la interfaz, apertura de conversaciones y panel de agentes |
| Conceptos financieros básicos | Comprensión de rendimiento, volatilidad, Sharpe ratio y benchmarks |
| Navegación en SharePoint Online | Capacidad de localizar y abrir archivos en bibliotecas de documentos |
| Microsoft Word Online | Edición básica de documentos en el navegador |

### Acceso y Licenciamiento

| Requisito | Verificación |
|---|---|
| Licencia Microsoft 365 Copilot Premium activa | El icono de Copilot Chat debe aparecer en la barra lateral de Microsoft 365 |
| Rol de **Miembro** (contribuidor) en el sitio SharePoint del curso | Poder acceder a `https://[tenant].sharepoint.com/sites/CursoAgentes` y abrir archivos |
| Cinco agentes preconstruidos disponibles | Analista, Investigador, Asistente de solicitudes, Entrenador de ideas y Asesor de escritura visibles en el panel de agentes de Copilot Chat |
| Archivos de datos precargados en SharePoint | Cuatro archivos en la carpeta `/Lab-02-00-01/` (ver sección siguiente) |

---

## Entorno del Laboratorio

### Archivos Requeridos en SharePoint

Todos los archivos se encuentran en la ruta:
`https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-01/`

| Archivo | Descripción | Formato |
|---|---|---|
| `datos_fondo_A_renta_variable_global.xlsx` | Métricas mensuales del Fondo A: rendimiento, volatilidad, Sharpe ratio, composición por clase de activo, correlaciones | Excel (.xlsx) |
| `datos_fondo_B_mixto_conservador.xlsx` | Métricas mensuales del Fondo B: rendimiento, volatilidad, Sharpe ratio, composición por clase de activo, correlaciones | Excel (.xlsx) |
| `datos_fondo_C_alternativo_diversificado.xlsx` | Métricas mensuales del Fondo C: rendimiento, volatilidad, Sharpe ratio, composición por clase de activo, correlaciones | Excel (.xlsx) |
| `benchmark_msci_world_2023.pdf` | Datos de referencia del índice MSCI World 2023: rendimiento acumulado, volatilidad anualizada, composición sectorial | PDF |

### Software y Versiones

| Software | Versión mínima |
|---|---|
| Microsoft Edge | 124.0.2478.97 |
| Microsoft 365 Copilot Chat | Build de producción M365 Copilot - mayo 2024 |
| Microsoft SharePoint Online | 16.0.24211.12000 |
| Microsoft Word Online | Incluido en Microsoft 365 Apps for Enterprise |

### Carpeta de Salida

Los archivos generados durante el laboratorio se guardarán en:
`https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/`

> **Nota:** La carpeta `/Lab-02-00-02/` debe estar vacía al inicio de este laboratorio. Los archivos de salida serán insumo para el Lab 02-00-02.

---

## Configuración Inicial

Antes de comenzar las fases del laboratorio, realiza la siguiente verificación del entorno.

**Objetivo:** Confirmar que todos los recursos están accesibles y que los agentes preconstruidos están disponibles.

**Instrucciones:**

1. Abre **Microsoft Edge** y navega a `https://www.microsoft365.com`. Inicia sesión con las credenciales del tenant del curso.

2. En la barra lateral izquierda del portal de Microsoft 365, haz clic en el icono de **Copilot Chat** (icono con forma de chispa/estrella). Se abrirá la interfaz de Copilot Chat en una nueva vista.

3. En la interfaz de Copilot Chat, localiza el **panel de agentes**. Haz clic en el icono de agentes (generalmente representado por un ícono de persona con engranaje o el botón "Agentes" en la parte superior derecha del chat).

4. Verifica que los siguientes cinco agentes preconstruidos aparezcan en la lista:
   - **Analista** (Analyst)
   - **Investigador** (Researcher)
   - **Asistente de solicitudes** (Prompt Coach / Request Assistant)
   - **Entrenador de ideas** (Idea Coach)
   - **Asesor de escritura** (Writing Coach)

5. En una pestaña separada del navegador, navega a:
   ```
   https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-01/
   ```

6. Confirma que los cuatro archivos están presentes:
   - `datos_fondo_A_renta_variable_global.xlsx`
   - `datos_fondo_B_mixto_conservador.xlsx`
   - `datos_fondo_C_alternativo_diversificado.xlsx`
   - `benchmark_msci_world_2023.pdf`

7. Haz clic en `datos_fondo_A_renta_variable_global.xlsx` para abrirlo brevemente en Excel Online. Verifica que contiene hojas con datos de rendimiento mensual, volatilidad, Sharpe ratio y composición de activos. Cierra la vista previa.

**Verificación:**

- ✅ Los cinco agentes preconstruidos aparecen listados en el panel de agentes de Copilot Chat
- ✅ Los cuatro archivos son accesibles en la carpeta `/Lab-02-00-01/` de SharePoint
- ✅ Los archivos Excel contienen datos estructurados con métricas financieras

> **⚠️ Importante:** Si algún agente no aparece en la lista o los archivos no están disponibles, notifica al instructor antes de continuar. No es posible completar el laboratorio sin estos recursos.

---

## Paso a Paso

### Fase 1: Análisis de Datos con el Agente Analista (15 minutos)

**Objetivo:** Utilizar el agente Analista para cargar los archivos de los tres fondos, extraer métricas clave, generar comparaciones cuantitativas y producir visualizaciones que resuman el desempeño relativo de cada fondo.

#### Paso 1.1 — Iniciar una conversación con el Agente Analista

**Instrucciones:**

1. En la interfaz de Copilot Chat, haz clic en el panel de **Agentes**.

2. Selecciona el agente **Analista** de la lista. Se abrirá una nueva conversación dedicada con este agente. Observa que el encabezado de la conversación indica que estás interactuando con el agente Analista.

3. Antes de cargar archivos, envía el siguiente mensaje introductorio para establecer el contexto de la sesión:

   ```
   Voy a cargar tres archivos Excel con datos de fondos multiactivo y un PDF con datos de benchmark. Necesito que realices un análisis comparativo cuantitativo de rendimiento, volatilidad, Sharpe ratio y correlación de activos para los tres fondos. Los fondos son:
   - Fondo A: Renta Variable Global
   - Fondo B: Mixto Conservador
   - Fondo C: Alternativo Diversificado
   El benchmark de referencia es el MSCI World 2023.
   ```

4. Espera la respuesta del agente. Debe confirmar que está listo para recibir los archivos y proceder con el análisis.

**Resultado esperado:** El agente Analista responde confirmando que comprende el objetivo del análisis y solicita o espera la carga de los archivos.

#### Paso 1.2 — Cargar los archivos de datos de los fondos

**Instrucciones:**

1. En la ventana de conversación con el agente Analista, haz clic en el icono de **adjuntar archivo** (ícono de clip 📎) ubicado en la barra de entrada de texto.

2. Selecciona la opción de cargar desde **SharePoint** o **OneDrive** (dependiendo de la interfaz, puede aparecer como "Examinar archivos en la nube" o "SharePoint").

3. Navega a la ubicación:
   ```
   Sites > CursoAgentes > Documentos compartidos > Lab-02-00-01
   ```

4. Selecciona los tres archivos Excel simultáneamente (mantén presionada la tecla `Ctrl` mientras haces clic en cada uno):
   - `datos_fondo_A_renta_variable_global.xlsx`
   - `datos_fondo_B_mixto_conservador.xlsx`
   - `datos_fondo_C_alternativo_diversificado.xlsx`

5. Haz clic en **Adjuntar** o **Abrir** para cargar los archivos en la conversación.

6. Una vez adjuntos, escribe el siguiente prompt y envíalo:

   ```
   Analiza los tres archivos Excel que acabo de cargar. Para cada fondo, extrae las siguientes métricas anualizadas:
   1. Rendimiento acumulado 2023
   2. Rendimiento promedio mensual
   3. Volatilidad anualizada (desviación estándar)
   4. Sharpe ratio
   5. Máximo drawdown
   
   Presenta los resultados en una tabla comparativa con los tres fondos en columnas.
   ```

7. Espera a que el agente procese los archivos. Observa que el agente puede mostrar indicadores de que está ejecutando código Python internamente para realizar los cálculos.

**Resultado esperado:** El agente Analista genera una tabla comparativa con las cinco métricas solicitadas para cada uno de los tres fondos. La tabla debe tener un formato similar al siguiente:

| Métrica | Fondo A (RV Global) | Fondo B (Mixto Conservador) | Fondo C (Alternativo Diversificado) |
|---|---|---|---|
| Rendimiento acumulado 2023 | XX.X% | XX.X% | XX.X% |
| Rendimiento promedio mensual | X.X% | X.X% | X.X% |
| Volatilidad anualizada | XX.X% | XX.X% | XX.X% |
| Sharpe ratio | X.XX | X.XX | X.XX |
| Máximo drawdown | -XX.X% | -XX.X% | -XX.X% |

**Verificación:**
- ✅ La tabla contiene datos numéricos coherentes para los tres fondos
- ✅ El Fondo B (Mixto Conservador) debería mostrar menor volatilidad que el Fondo A (Renta Variable Global)
- ✅ Las métricas son consistentes entre sí (por ejemplo, un fondo con mayor rendimiento y mayor volatilidad debería tener un Sharpe ratio razonable)

#### Paso 1.3 — Generar visualizaciones comparativas

**Instrucciones:**

1. En la misma conversación con el agente Analista, envía el siguiente prompt:

   ```
   Genera los siguientes gráficos comparativos:
   1. Un gráfico de barras agrupadas que compare el rendimiento acumulado 2023 de los tres fondos junto al benchmark MSCI World (usa 22.2% como referencia del MSCI World si no tienes el PDF cargado aún).
   2. Un gráfico de dispersión con la volatilidad anualizada en el eje X y el rendimiento acumulado en el eje Y, con un punto por cada fondo, etiquetado con el nombre del fondo.
   3. Una tabla de correlación entre los tres fondos si los datos mensuales lo permiten.
   ```

2. Espera a que el agente genere las visualizaciones. El agente ejecutará código Python internamente y producirá los gráficos como imágenes embebidas en la conversación.

3. Revisa cada gráfico generado:
   - **Gráfico de barras:** Verifica que los cuatro elementos (tres fondos + benchmark) estén representados y etiquetados correctamente.
   - **Gráfico de dispersión:** Confirma que los puntos están posicionados de manera coherente (el Fondo A debería estar más a la derecha y arriba que el Fondo B).
   - **Tabla de correlación:** Verifica que es una matriz simétrica con valores entre -1 y 1.

4. Si algún gráfico no se generó correctamente o falta información, envía un prompt de seguimiento como:

   ```
   El gráfico de barras no incluye el benchmark. Por favor, agrégalo como una barra adicional con el valor de referencia de 22.2% para el MSCI World 2023.
   ```

**Resultado esperado:** Tres visualizaciones claras y correctamente etiquetadas que muestran la comparación entre los fondos. Los gráficos deben ser legibles y contener leyendas apropiadas.

**Verificación:**
- ✅ Se generaron al menos dos gráficos visibles en la conversación
- ✅ Los ejes están etiquetados con las unidades correctas (porcentajes para rendimiento y volatilidad)
- ✅ Los fondos están claramente diferenciados por color o etiqueta

#### Paso 1.4 — Solicitar análisis de composición por clase de activo

**Instrucciones:**

1. Envía el siguiente prompt al agente Analista:

   ```
   Ahora analiza la composición por clase de activo de cada fondo. Muestra un gráfico de torta (pie chart) para cada fondo que refleje la distribución porcentual entre las clases de activo (renta variable, renta fija, alternativos, efectivo, u otras categorías que aparezcan en los datos). Debajo de los gráficos, incluye una tabla resumen con las asignaciones de cada fondo.
   ```

2. Revisa los gráficos de torta generados. Cada fondo debe mostrar una distribución coherente con su perfil:
   - **Fondo A (RV Global):** Mayor concentración en renta variable
   - **Fondo B (Mixto Conservador):** Distribución más equilibrada con peso significativo en renta fija
   - **Fondo C (Alternativo Diversificado):** Presencia notable de activos alternativos

3. **Guarda los resultados clave.** Selecciona la tabla comparativa de métricas del Paso 1.2 y los gráficos principales. Copia la tabla de métricas a un documento temporal (puedes usar el Bloc de notas o un documento Word nuevo) para referencia en fases posteriores.

**Resultado esperado:** Gráficos de torta individuales para cada fondo mostrando la distribución de clases de activo, acompañados de una tabla resumen numérica.

**Verificación:**
- ✅ Las distribuciones de activos suman 100% para cada fondo
- ✅ La composición es coherente con el perfil declarado de cada fondo
- ✅ Has guardado la tabla de métricas comparativas para uso posterior

> **📝 Nota:** Mantén esta conversación con el agente Analista abierta. Podrás volver a ella si necesitas consultar datos específicos en fases posteriores.

---

### Fase 2: Contextualización de Mercado con el Agente Investigador (10 minutos)

**Objetivo:** Utilizar el agente Investigador para obtener contexto de mercado relevante del año 2023 que explique el desempeño observado en los fondos y enriquezca el análisis con información de benchmarks, tendencias macroeconómicas y eventos de mercado significativos.

#### Paso 2.1 — Iniciar conversación con el Agente Investigador

**Instrucciones:**

1. En Copilot Chat, regresa al **panel de Agentes** y selecciona el agente **Investigador**.

2. Se abrirá una nueva conversación. Envía el siguiente prompt para establecer contexto:

   ```
   Necesito que investigues el contexto de mercados financieros globales durante 2023 para enriquecer un análisis comparativo de fondos multiactivo. Los fondos que estoy analizando son:
   - Fondo A: Renta Variable Global (benchmark: MSCI World)
   - Fondo B: Mixto Conservador (benchmark compuesto: 40% MSCI World / 60% Bloomberg Global Aggregate Bond)
   - Fondo C: Alternativo Diversificado (incluye hedge funds, commodities y real estate)
   
   Por favor investiga y proporciona:
   1. Rendimiento del índice MSCI World en 2023 y principales factores que lo impulsaron
   2. Comportamiento de la renta fija global en 2023 (Bloomberg Global Aggregate Bond Index)
   3. Eventos macroeconómicos clave de 2023 que impactaron los mercados (política monetaria de la Fed, inflación, conflictos geopolíticos)
   4. Desempeño de activos alternativos en 2023 (commodities, real estate, hedge funds)
   ```

3. Espera la respuesta del agente. El Investigador compilará información de fuentes disponibles y presentará un resumen estructurado.

**Resultado esperado:** El agente Investigador proporciona un resumen de 4 secciones con datos contextuales del mercado 2023, incluyendo cifras de rendimiento de los índices de referencia y eventos macroeconómicos relevantes.

**Verificación:**
- ✅ La respuesta menciona el rendimiento del MSCI World en 2023 (aproximadamente +22-24%)
- ✅ Se incluyen referencias a la política monetaria de la Reserva Federal y/o el BCE
- ✅ Se menciona el comportamiento de la renta fija en un entorno de tasas altas

#### Paso 2.2 — Profundizar en factores específicos de rendimiento

**Instrucciones:**

1. Basándote en la respuesta del Investigador, envía un prompt de seguimiento para obtener información más específica que puedas vincular con los datos de los fondos:

   ```
   Gracias. Ahora profundiza en los siguientes puntos específicos:
   
   1. ¿Qué sectores del MSCI World tuvieron mejor y peor desempeño en 2023? Esto me ayudará a entender la composición sectorial del Fondo A.
   2. ¿Cuál fue el spread de crédito promedio en 2023 y cómo afectó a los fondos mixtos conservadores?
   3. ¿Qué correlación aproximada existió entre renta variable y renta fija en 2023? ¿Se mantuvo la diversificación tradicional?
   4. ¿Cuáles fueron los principales riesgos de cola (tail risks) que enfrentaron los portafolios multiactivo en 2023?
   
   Presenta la información de forma concisa, con datos numéricos cuando estén disponibles.
   ```

2. Revisa la respuesta y toma nota mental de los puntos clave que podrás usar para contextualizar los resultados del agente Analista.

3. **Copia el resumen de contexto de mercado** generado por el Investigador. Selecciona el texto completo de ambas respuestas y cópialo a tu documento temporal de trabajo (el mismo donde guardaste la tabla de métricas del Paso 1.2).

**Resultado esperado:** Información detallada sobre sectores, spreads de crédito, correlaciones entre clases de activo y riesgos de cola en 2023, presentada con datos numéricos específicos.

**Verificación:**
- ✅ Se mencionan sectores líderes en 2023 (tecnología, comunicaciones) y rezagados
- ✅ Se proporciona contexto sobre la correlación renta variable/renta fija
- ✅ Has copiado el resumen de contexto de mercado para uso en fases posteriores

---

### Fase 3: Gestión del Flujo de Trabajo con el Agente Asistente de Solicitudes (8 minutos)

**Objetivo:** Emplear el agente Asistente de solicitudes para estructurar las peticiones de información pendientes, organizar los hallazgos obtenidos hasta ahora y preparar un esquema lógico del resumen ejecutivo que se redactará en la Fase 5.

#### Paso 3.1 — Estructurar los hallazgos y definir el esquema del entregable

**Instrucciones:**

1. En Copilot Chat, abre una nueva conversación seleccionando el agente **Asistente de solicitudes** desde el panel de Agentes.

2. Envía el siguiente prompt, que resume el trabajo realizado hasta ahora y solicita ayuda para estructurarlo:

   ```
   Estoy realizando un análisis comparativo de tres fondos multiactivo para una revisión interna del equipo de gestión de inversiones. He completado dos fases de trabajo:
   
   FASE 1 - Análisis cuantitativo (completado):
   - Tabla comparativa de métricas: rendimiento, volatilidad, Sharpe ratio, máximo drawdown para Fondo A (RV Global), Fondo B (Mixto Conservador) y Fondo C (Alternativo Diversificado)
   - Gráficos de comparación de rendimiento vs benchmark MSCI World
   - Gráfico de dispersión riesgo-retorno
   - Análisis de composición por clase de activo
   
   FASE 2 - Contexto de mercado (completado):
   - Resumen del entorno de mercado 2023
   - Rendimiento de benchmarks (MSCI World, Bloomberg Global Agg Bond)
   - Factores sectoriales y macroeconómicos
   - Análisis de correlaciones y riesgos de cola
   
   Necesito que me ayudes a:
   1. Identificar qué información adicional podría necesitar antes de redactar el resumen ejecutivo
   2. Proponer una estructura lógica para un resumen ejecutivo de 2-3 páginas dirigido al comité interno de inversiones
   3. Sugerir los puntos clave de conclusión que debería incluir basándome en un análisis típico de este tipo
   ```

3. Revisa la respuesta del agente. Debe proporcionar una estructura organizada y posibles brechas de información.

4. Si el agente identifica información faltante, envía un prompt de seguimiento:

   ```
   Buena observación. Para los fines de este ejercicio, asume que:
   - Los datos de benchmark están disponibles en el PDF del MSCI World 2023
   - Las comisiones de gestión son: Fondo A (1.2% TER), Fondo B (0.8% TER), Fondo C (1.8% TER)
   - El horizonte de inversión del comité es de 3-5 años
   
   Con esta información adicional, refina la estructura del resumen ejecutivo y dame un esquema detallado con los encabezados de sección y los puntos clave a cubrir en cada una.
   ```

**Resultado esperado:** Un esquema detallado del resumen ejecutivo con secciones claramente definidas, como:
1. Resumen ejecutivo / Conclusiones principales
2. Metodología y fuentes de datos
3. Análisis comparativo de rendimiento
4. Análisis de riesgo y eficiencia (Sharpe ratio)
5. Composición y diversificación
6. Contexto de mercado 2023
7. Recomendaciones para el comité

**Verificación:**
- ✅ El esquema tiene al menos 5 secciones lógicamente ordenadas
- ✅ Se identifican los datos clave a incluir en cada sección
- ✅ La estructura es apropiada para una audiencia de gestión de inversiones (no técnica de TI)

> **📝 Nota:** Guarda este esquema. Lo utilizarás como guía en la Fase 5 con el Asesor de escritura.

---

### Fase 4: Generación de Perspectivas con el Agente Entrenador de Ideas (10 minutos)

**Objetivo:** Aplicar el agente Entrenador de ideas para generar hipótesis analíticas, perspectivas adicionales y ángulos de análisis que enriquezcan las conclusiones del resumen ejecutivo, yendo más allá de la simple comparación numérica.

#### Paso 4.1 — Explorar hipótesis sobre el desempeño diferencial

**Instrucciones:**

1. En Copilot Chat, abre una nueva conversación seleccionando el agente **Entrenador de ideas** desde el panel de Agentes.

2. Envía el siguiente prompt con los datos resumidos de las fases anteriores:

   ```
   Soy analista de inversiones y estoy preparando una revisión interna de tres fondos multiactivo. Te presento los resultados principales de mi análisis cuantitativo:
   
   MÉTRICAS CLAVE 2023:
   - Fondo A (Renta Variable Global): Alto rendimiento, alta volatilidad, Sharpe ratio moderado
   - Fondo B (Mixto Conservador): Rendimiento moderado, baja volatilidad, Sharpe ratio competitivo
   - Fondo C (Alternativo Diversificado): Rendimiento bajo-moderado, volatilidad media, Sharpe ratio bajo, pero baja correlación con los otros fondos
   
   CONTEXTO: 2023 fue un año de fuerte recuperación en renta variable (MSCI World +22%), tasas de interés altas, y desempeño mixto en alternativos.
   
   Necesito que me ayudes a generar:
   1. Tres hipótesis sobre por qué el Fondo C tuvo un Sharpe ratio inferior a pesar de su diversificación
   2. Dos perspectivas contraintuitivas que podrían cambiar la valoración del comité sobre alguno de los fondos
   3. Tres preguntas provocadoras que debería plantear al comité de inversiones para estimular la discusión
   4. Una perspectiva sobre cómo cambiaría el ranking de los fondos en un escenario de mercado bajista
   ```

3. Revisa las hipótesis y perspectivas generadas. Evalúa críticamente si son relevantes para un contexto de gestión de inversiones.

**Resultado esperado:** El agente genera un conjunto de hipótesis, perspectivas y preguntas que van más allá del análisis numérico básico, como por ejemplo:
- Hipótesis sobre el impacto de las comisiones más altas del Fondo C en su Sharpe ratio
- Perspectiva contraintuitiva sobre el valor de la baja correlación del Fondo C en un portafolio combinado
- Pregunta provocadora sobre si el benchmark MSCI World es apropiado para evaluar un fondo alternativo

**Verificación:**
- ✅ Se generaron al menos 3 hipótesis diferenciadas y plausibles
- ✅ Las perspectivas contraintuitivas aportan valor analítico real
- ✅ Las preguntas son apropiadas para un comité de inversiones senior

#### Paso 4.2 — Generar recomendaciones de asignación

**Instrucciones:**

1. Envía un segundo prompt al Entrenador de ideas para explorar recomendaciones:

   ```
   Basándote en el análisis anterior, ayúdame a pensar en las siguientes dimensiones:
   
   1. Si el comité tiene un presupuesto de riesgo limitado (volatilidad máxima del portafolio: 10% anualizada), ¿qué combinación de los tres fondos podría ser óptima? Dame 2-3 escenarios con asignaciones porcentuales aproximadas.
   
   2. ¿Qué métricas adicionales debería solicitar a los gestores de cada fondo para profundizar el análisis en la próxima revisión trimestral?
   
   3. ¿Cuál es el principal riesgo oculto que podría no ser evidente en los datos históricos de cada fondo?
   
   Recuerda que esto es para estimular mi pensamiento, no para tomar decisiones definitivas.
   ```

2. Revisa los escenarios de asignación propuestos y las métricas adicionales sugeridas.

3. **Selecciona los 3-4 insights más valiosos** de toda la conversación con el Entrenador de ideas y cópialos a tu documento temporal de trabajo. Estos serán incorporados en el resumen ejecutivo.

**Resultado esperado:** Escenarios de asignación con porcentajes aproximados, lista de métricas adicionales (como tracking error, information ratio, beta, etc.) y riesgos ocultos identificados para cada fondo.

**Verificación:**
- ✅ Los escenarios de asignación suman 100% y respetan la restricción de volatilidad
- ✅ Las métricas adicionales sugeridas son relevantes para análisis de fondos multiactivo
- ✅ Has seleccionado y guardado los insights clave para el resumen ejecutivo

---

### Fase 5: Documentación Ejecutiva con el Agente Asesor de Escritura (12 minutos)

**Objetivo:** Usar el agente Asesor de escritura para redactar un resumen ejecutivo profesional del análisis comparativo, incorporando los datos cuantitativos, el contexto de mercado, las perspectivas analíticas y la estructura definida en las fases anteriores. El documento final se guardará como `analisis_fondos_comparativo.docx`.

#### Paso 5.1 — Redactar el borrador del resumen ejecutivo

**Instrucciones:**

1. En Copilot Chat, abre una nueva conversación seleccionando el agente **Asesor de escritura** desde el panel de Agentes.

2. Envía el siguiente prompt comprehensivo, que integra todos los insumos de las fases anteriores:

   ```
   Necesito que me ayudes a redactar un resumen ejecutivo profesional para el comité interno de inversiones. El documento debe tener entre 800 y 1200 palabras y seguir esta estructura:
   
   TÍTULO: "Análisis Comparativo de Fondos Multiactivo — Revisión Interna Q4 2023"
   
   AUDIENCIA: Miembros del comité de inversiones (directores de inversión, gestores de portafolio senior, director de riesgos). Tono profesional, conciso, orientado a la acción.
   
   ESTRUCTURA:
   1. Resumen Ejecutivo (3-4 oraciones con las conclusiones principales)
   2. Metodología (breve descripción de fuentes de datos y métricas utilizadas)
   3. Análisis Comparativo de Rendimiento (incluir tabla de métricas y comparación vs MSCI World)
   4. Perfil de Riesgo y Eficiencia (volatilidad, Sharpe ratio, drawdown)
   5. Composición y Diversificación (distribución por clase de activo)
   6. Contexto de Mercado 2023 (factores macro que explican el desempeño)
   7. Perspectivas y Consideraciones Adicionales (insights del análisis cualitativo)
   8. Recomendaciones para el Comité (2-3 recomendaciones concretas)
   
   DATOS A INCLUIR:
   - Tres fondos: A (Renta Variable Global), B (Mixto Conservador), C (Alternativo Diversificado)
   - Benchmark: MSCI World 2023 (~22% rendimiento)
   - El Fondo A tuvo el mayor rendimiento pero también la mayor volatilidad
   - El Fondo B tuvo el mejor Sharpe ratio ajustado por riesgo
   - El Fondo C mostró baja correlación con los otros fondos, pero rendimiento inferior y comisiones más altas (TER 1.8%)
   - Contexto: 2023 fue año de recuperación en renta variable, tasas altas, renta fija presionada
   
   INSIGHT CLAVE: El Fondo C, a pesar de su menor rendimiento individual, podría aportar valor significativo en un portafolio combinado por su efecto de diversificación.
   
   Por favor redacta el documento completo siguiendo esta estructura. Usa un tono profesional de gestión de inversiones.
   ```

3. Espera a que el agente genere el borrador completo. Esto puede tomar unos momentos dado la extensión solicitada.

4. Lee el borrador generado completamente. Evalúa:
   - ¿El tono es apropiado para un comité de inversiones?
   - ¿La estructura sigue el esquema solicitado?
   - ¿Los datos están presentados de forma clara y precisa?
   - ¿Las recomendaciones son accionables?

**Resultado esperado:** Un documento de 800-1200 palabras con las 8 secciones solicitadas, tono profesional financiero, datos cuantitativos integrados y recomendaciones concretas.

#### Paso 5.2 — Refinar el documento con retroalimentación específica

**Instrucciones:**

1. Basándote en tu lectura del borrador, envía un prompt de refinamiento. Adapta este prompt según las áreas que consideres que necesitan mejora:

   ```
   El borrador es bueno. Necesito los siguientes ajustes:
   
   1. En la sección de Resumen Ejecutivo, hazlo más directo y orientado a la acción. Comienza con la conclusión principal, no con contexto.
   2. En la sección de Análisis Comparativo, formatea la tabla de métricas de forma que sea fácil de escanear visualmente. Usa negrita para los mejores valores de cada métrica.
   3. En las Recomendaciones, añade una tercera recomendación sobre solicitar datos de tracking error y beta a los gestores de los fondos para la próxima revisión trimestral.
   4. Añade un disclaimer al final indicando que este análisis es para uso interno y no constituye asesoría de inversión.
   5. Revisa que no haya repeticiones innecesarias entre secciones.
   
   Por favor genera la versión revisada completa.
   ```

2. Revisa la versión refinada. Verifica que los ajustes solicitados se implementaron correctamente.

3. Si necesitas ajustes adicionales de estilo, envía un último prompt:

   ```
   Revisa el documento una vez más enfocándote en:
   - Consistencia en el uso de términos financieros
   - Que todas las cifras porcentuales tengan un decimal
   - Que las transiciones entre secciones sean fluidas
   - Que el documento no exceda 1200 palabras
   ```

**Resultado esperado:** Versión final pulida del resumen ejecutivo con todos los ajustes incorporados.

**Verificación:**
- ✅ El documento tiene entre 800 y 1200 palabras
- ✅ Las 8 secciones están presentes y correctamente estructuradas
- ✅ El tono es profesional y apropiado para gestión de inversiones
- ✅ Se incluye un disclaimer al final
- ✅ Las recomendaciones son concretas y accionables

#### Paso 5.3 — Guardar los archivos de salida en SharePoint

**Instrucciones:**

1. **Crear el documento Word:** Abre una nueva pestaña en el navegador y navega a:
   ```
   https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/
   ```

2. Haz clic en **+ Nuevo** > **Documento de Word**. Se abrirá Word Online con un documento en blanco.

3. Nombra el documento como `analisis_fondos_comparativo.docx` (haz clic en el nombre del documento en la parte superior de Word Online para editarlo).

4. Regresa a la conversación con el Asesor de escritura en Copilot Chat. Selecciona todo el texto de la versión final del resumen ejecutivo (Ctrl+A en el texto de respuesta, o selecciona manualmente).

5. Copia el texto (Ctrl+C) y pégalo en el documento Word Online (Ctrl+V).

6. Aplica formato básico al documento:
   - Título principal: **Título 1** (Heading 1)
   - Secciones: **Título 2** (Heading 2)
   - Tabla de métricas: Usa la función de insertar tabla de Word Online
   - Verifica que el formato se vea profesional

7. El documento se guardará automáticamente en SharePoint. Verifica que aparezca la indicación "Guardado" en la barra superior.

8. **Crear la tabla de métricas en Excel:** Regresa a la carpeta `/Lab-02-00-02/` en SharePoint.

9. Haz clic en **+ Nuevo** > **Libro de Excel**. Nombra el archivo como `tabla_metricas_fondos.xlsx`.

10. Regresa a la conversación con el agente **Analista** (debería estar aún abierta). Localiza la tabla comparativa de métricas generada en el Paso 1.2.

11. Copia la tabla de métricas y pégala en la hoja de Excel Online. Ajusta el formato:
    - Fila 1: Encabezados en negrita
    - Columna A: Nombres de métricas
    - Columnas B, C, D: Valores para Fondo A, B, C respectivamente
    - Aplica formato de número con un decimal para los porcentajes

12. El archivo se guardará automáticamente. Verifica la indicación "Guardado".

**Resultado esperado:** Dos archivos guardados en la carpeta `/Lab-02-00-02/` de SharePoint:
- `analisis_fondos_comparativo.docx` — Resumen ejecutivo completo con formato profesional
- `tabla_metricas_fondos.xlsx` — Tabla de métricas comparativas de los tres fondos

**Verificación:**
- ✅ Ambos archivos aparecen en la carpeta `/Lab-02-00-02/` de SharePoint
- ✅ El documento Word se abre correctamente y muestra el contenido formateado
- ✅ El archivo Excel contiene la tabla de métricas con datos numéricos correctos
- ✅ Ambos archivos muestran la fecha de modificación actual

---

## Validación y Pruebas

Realiza las siguientes verificaciones finales para confirmar que has completado exitosamente todas las fases del laboratorio.

### Lista de Verificación Final

| # | Criterio de validación | Estado |
|---|---|---|
| 1 | Se utilizó el agente **Analista** para generar una tabla comparativa de métricas y al menos 2 visualizaciones | ☐ |
| 2 | Se utilizó el agente **Investigador** para obtener contexto de mercado 2023 con datos de benchmarks | ☐ |
| 3 | Se utilizó el agente **Asistente de solicitudes** para estructurar el esquema del resumen ejecutivo | ☐ |
| 4 | Se utilizó el agente **Entrenador de ideas** para generar al menos 3 hipótesis y 2 perspectivas adicionales | ☐ |
| 5 | Se utilizó el agente **Asesor de escritura** para redactar y refinar el resumen ejecutivo | ☐ |
| 6 | El archivo `analisis_fondos_comparativo.docx` existe en `/Lab-02-00-02/` con contenido formateado | ☐ |
| 7 | El archivo `tabla_metricas_fondos.xlsx` existe en `/Lab-02-00-02/` con datos numéricos correctos | ☐ |
| 8 | El resumen ejecutivo tiene entre 800 y 1200 palabras y contiene las 8 secciones requeridas | ☐ |

### Prueba de Integridad de los Archivos de Salida

1. Navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/`.

2. Abre `analisis_fondos_comparativo.docx` y verifica:
   - El título es "Análisis Comparativo de Fondos Multiactivo — Revisión Interna Q4 2023"
   - Contiene las 8 secciones definidas en el esquema
   - Incluye datos numéricos de los tres fondos
   - Tiene un disclaimer al final

3. Abre `tabla_metricas_fondos.xlsx` y verifica:
   - Contiene al menos 5 filas de métricas (rendimiento, volatilidad, Sharpe ratio, drawdown, rendimiento mensual promedio)
   - Contiene 3 columnas de datos (una por fondo)
   - Los valores numéricos son coherentes (por ejemplo, la volatilidad del Fondo B es menor que la del Fondo A)

---

## Solución de Problemas

### Problema 1: El agente Analista no genera gráficos o muestra un error al procesar los archivos Excel

**Síntomas:** Al enviar un prompt solicitando gráficos o análisis de datos, el agente Analista responde con un mensaje genérico sin datos, muestra un error de procesamiento, o indica que no puede acceder a los archivos adjuntos. Los gráficos no aparecen embebidos en la conversación.

**Causa:** Este problema generalmente ocurre por una de las siguientes razones:
- Los archivos Excel tienen un formato no compatible (por ejemplo, contienen macros VBA, tablas dinámicas complejas o están protegidos con contraseña).
- La sesión de ejecución de código Python del agente ha expirado o ha alcanzado un límite de recursos.
- Los archivos se adjuntaron desde una ubicación de SharePoint donde el agente no tiene permisos de lectura.
- El navegador está bloqueando la carga de contenido embebido (gráficos) por configuración de seguridad.

**Solución:**

1. **Descarga los archivos localmente primero.** Navega a la carpeta de SharePoint `/Lab-02-00-01/`, descarga los tres archivos Excel a tu equipo local y luego adjúntalos directamente desde tu disco local en lugar de desde SharePoint.

2. **Inicia una nueva conversación.** Si la sesión actual muestra errores repetidos, cierra la conversación con el agente Analista y abre una nueva. Las sesiones de ejecución de código tienen límites de tiempo y recursos.

3. **Simplifica la solicitud.** En lugar de solicitar múltiples gráficos en un solo prompt, divide la solicitud:
   ```
   Primero carga y analiza solo el archivo datos_fondo_A_renta_variable_global.xlsx. 
   Muéstrame las primeras 10 filas para confirmar que lo leíste correctamente.
   ```
   Una vez confirmada la lectura, procede con solicitudes incrementales.

4. **Verifica la configuración del navegador.** Asegúrate de que Microsoft Edge no esté bloqueando ventanas emergentes o contenido embebido para el dominio `*.microsoft.com`. Ve a `edge://settings/content/popups` y añade una excepción si es necesario.

---

### Problema 2: Los agentes preconstruidos no aparecen en el panel de agentes de Copilot Chat

**Síntomas:** Al abrir el panel de agentes en Copilot Chat, la lista está vacía, muestra solo agentes personalizados, o faltan uno o más de los cinco agentes preconstruidos requeridos (Analista, Investigador, Asistente de solicitudes, Entrenador de ideas, Asesor de escritura). El botón de agentes puede no estar visible en absoluto.

**Causa:** Este problema está relacionado con el licenciamiento o la configuración del tenant:
- La licencia Microsoft 365 Copilot Premium no está correctamente asignada a la cuenta del estudiante, o la asignación fue reciente (menos de 24 horas) y aún no se ha propagado.
- El administrador del tenant ha deshabilitado los agentes preconstruidos desde el Centro de Administración de Microsoft 365.
- El navegador tiene una sesión de caché antigua que no refleja los permisos actualizados.

**Solución:**

1. **Verifica tu licencia.** Navega a `https://myaccount.microsoft.com` y revisa la sección "Suscripciones" o "Licencias". Confirma que aparece **Microsoft 365 Copilot** en la lista de licencias activas.

2. **Limpia la caché del navegador.** En Microsoft Edge:
   - Presiona `Ctrl + Shift + Delete`
   - Selecciona "Última hora" como rango de tiempo
   - Marca "Cookies y otros datos del sitio" e "Imágenes y archivos en caché"
   - Haz clic en "Borrar ahora"
   - Cierra y reabre el navegador, luego inicia sesión nuevamente en Microsoft 365

3. **Prueba en una ventana InPrivate.** Abre una ventana InPrivate en Edge (`Ctrl + Shift + N`), navega a `https://www.microsoft365.com`, inicia sesión y verifica si los agentes aparecen. Esto descarta problemas de caché o extensiones del navegador.

4. **Contacta al instructor/administrador.** Si los pasos anteriores no resuelven el problema, es probable que la licencia no esté asignada o que los agentes estén deshabilitados a nivel de tenant. El administrador debe verificar en el **Centro de Administración de Microsoft 365** > **Usuarios** > **Usuarios activos** > [tu cuenta] > **Licencias y aplicaciones** que la licencia de Copilot Premium está activa y que los agentes preconstruidos están habilitados en **Configuración** > **Copilot**.

---

## Limpieza

Este laboratorio **no requiere limpieza de archivos generados**, ya que los archivos de salida (`analisis_fondos_comparativo.docx` y `tabla_metricas_fondos.xlsx`) en la carpeta `/Lab-02-00-02/` serán utilizados como insumo de referencia en el **Lab 02-00-02**.

**Acciones de cierre:**

1. **No elimines** los archivos de la carpeta `/Lab-02-00-01/` ni de `/Lab-02-00-02/`.

2. Puedes cerrar las conversaciones individuales con cada agente en Copilot Chat. Las conversaciones quedarán en tu historial y podrás consultarlas posteriormente si lo necesitas.

3. Elimina cualquier archivo temporal que hayas descargado a tu equipo local durante el Problema 1 de la sección de solución de problemas (si aplica).

4. Cierra las pestañas adicionales del navegador que ya no necesites, manteniendo abierta únicamente la sesión de Microsoft 365.

---

## Resumen del Laboratorio

### Lo que Aprendiste

En este laboratorio aplicaste los cinco agentes preconstruidos de Microsoft 365 Copilot en un flujo de trabajo secuencial y complementario para producir un análisis comparativo profesional de fondos multiactivo:

| Fase | Agente Utilizado | Resultado Producido |
|---|---|---|
| 1. Análisis cuantitativo | **Analista** | Tabla comparativa de métricas, gráficos de rendimiento, dispersión riesgo-retorno y composición de activos |
| 2. Contexto de mercado | **Investigador** | Resumen del entorno de mercado 2023, benchmarks, factores macroeconómicos |
| 3. Estructura del flujo | **Asistente de solicitudes** | Esquema lógico del resumen ejecutivo, identificación de brechas de información |
| 4. Perspectivas analíticas | **Entrenador de ideas** | Hipótesis sobre desempeño diferencial, perspectivas contraintuitivas, escenarios de asignación |
| 5. Documentación ejecutiva | **Asesor de escritura** | Resumen ejecutivo de 800-1200 palabras, formateado y refinado para el comité de inversiones |

### Puntos Clave

- El agente **Analista** es especialmente poderoso para procesamiento cuantitativo: ejecuta código Python internamente para calcular métricas, generar gráficos y analizar datos estructurados sin requerir conocimientos de programación.
- Cada agente preconstruido tiene un propósito específico. La combinación secuencial de agentes permite abordar problemas complejos que ningún agente individual podría resolver completamente.
- La calidad de los resultados depende directamente de la calidad de los prompts. Prompts específicos con contexto, datos y formato deseado producen resultados significativamente mejores.
- Los archivos de salida de este laboratorio (`analisis_fondos_comparativo.docx` y `tabla_metricas_fondos.xlsx`) serán utilizados en el **Lab 02-00-02** para contextualizar la investigación regulatoria.

### Recursos Adicionales

- [Documentación oficial del agente Analista en Microsoft 365 Copilot](https://support.microsoft.com/es-es/topic/analyst-agent-in-microsoft-365-copilot)
- [Introducción a los agentes de Microsoft 365 Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/agents-overview)
- [Mejores prácticas de prompt engineering para Microsoft Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/microsoft-365-copilot-overview)
- [Seguridad y privacidad en Microsoft 365 Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/microsoft-365-copilot-privacy)

---

# Práctica: Investigación de actualizaciones regulatorias relevantes para la gestión de clientes de inversión en Estados Unidos

## 1. Metadatos del Laboratorio

| Campo | Detalle |
|---|---|
| **Duración** | 55 minutos |
| **Complejidad** | Alta |
| **Nivel de Bloom** | Crear |
| **Módulo** | 02 — Agentes preconstruidos de Microsoft 365 Copilot |
| **Laboratorio previo requerido** | Lab 02-00-01 |
| **Laboratorio siguiente** | Lab 02-00-03 |

---

## 2. Descripción General

En este laboratorio asumirás el rol de un analista de cumplimiento regulatorio en una firma de gestión de inversiones que opera en Estados Unidos. Tu objetivo es preparar un informe regulatorio integral para la revisión trimestral de clientes institucionales, utilizando los cinco agentes preconstruidos de Microsoft 365 Copilot en una secuencia coordinada. Partirás de los archivos de análisis de fondos generados en el Lab 02-00-01 y producirás dos entregables clave — un informe de cumplimiento regulatorio y una matriz de impacto — que servirán como insumo para el Lab 02-00-03. Este ejercicio integra investigación normativa (SEC, FINRA, Dodd-Frank Act), análisis de impacto cruzado con fondos multiactivo, priorización de hallazgos, generación de estrategias de adaptación y redacción profesional de informes.

---

## 3. Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Crear un flujo de investigación regulatoria completo utilizando el agente Investigador para identificar actualizaciones normativas recientes de la SEC, FINRA y el Dodd-Frank Act relevantes para la gestión de clientes de inversión en EE.UU.
- [ ] Aplicar el agente Analista para evaluar cuantitativamente el impacto de las actualizaciones regulatorias identificadas sobre los fondos multiactivo analizados en el Lab 02-00-01, generando una matriz de impacto en Excel
- [ ] Utilizar el agente Asistente de solicitudes para organizar y priorizar actualizaciones regulatorias según nivel de impacto y urgencia de implementación, y emplear el agente Entrenador de ideas para generar estrategias de adaptación y cumplimiento
- [ ] Producir un informe de cumplimiento regulatorio profesional con el agente Asesor de escritura que integre hallazgos de investigación, análisis de impacto y estrategias de adaptación en un documento listo para revisión trimestral
- [ ] Evaluar la efectividad de la secuencia coordinada de agentes preconstruidos como flujo de trabajo replicable para procesos de cumplimiento regulatorio en gestión de inversiones

---

## 4. Prerrequisitos

### Conocimientos Previos

| Requisito | Nivel | Detalle |
|---|---|---|
| Lab 02-00-01 completado | **Obligatorio** | Debes tener los archivos de salida `análisis_fondos_comparativo.docx` y `tabla_metricas_fondos.xlsx` guardados en SharePoint |
| Agentes preconstruidos M365 Copilot | Intermedio | Haber practicado el uso de los cinco agentes en el Lab 02-00-01 |
| Marco regulatorio EE.UU. | Básico-conceptual | Familiaridad con SEC, FINRA, Regulation Best Interest (Reg BI), FINRA Rule 4210, Dodd-Frank Act |
| Prompt engineering | Básico | Capacidad de formular prompts claros y con contexto para obtener respuestas precisas |
| SharePoint Online | Básico | Navegación, carga y descarga de archivos en bibliotecas de documentos |

### Acceso y Licencias

| Recurso | Requisito |
|---|---|
| Licencia Microsoft 365 Copilot Premium | Activa y asignada al menos 24 horas antes del laboratorio |
| Sitio SharePoint del curso | Rol de **Miembro** (contribuidor) en `https://[tenant].sharepoint.com/sites/CursoAgentes` |
| Carpeta de salida | Carpeta `/Documentos compartidos/Lab-02-00-02/` vacía y accesible |
| Archivos del Lab 02-00-01 | `análisis_fondos_comparativo.docx` y `tabla_metricas_fondos.xlsx` en `/Documentos compartidos/Lab-02-00-01/` |
| Microsoft Edge | Versión 124.0.2478.97 o superior |

---

## 5. Entorno del Laboratorio

### Hardware Mínimo

| Componente | Especificación |
|---|---|
| Procesador | 64 bits, 4 núcleos (Intel Core i5 8.ª gen. o AMD Ryzen 5 equivalente) |
| RAM | 8 GB mínimo (16 GB recomendado) |
| Almacenamiento | 10 GB disponibles (SSD recomendado) |
| Pantalla | 1920×1080 (Full HD) mínimo |
| Red | 10 Mbps bajada / 5 Mbps subida (25 Mbps simétrico recomendado) |

### Software Requerido

| Aplicación | Versión | Propósito en este lab |
|---|---|---|
| Microsoft Edge | 124.0.2478.97+ | Navegador principal para acceder a Copilot Chat y SharePoint |
| Microsoft 365 Copilot Chat | Build producción mayo 2024 | Interfaz de interacción con los cinco agentes preconstruidos |
| Microsoft SharePoint Online | 16.0.24211.12000 | Almacenamiento de archivos de entrada y salida |
| Microsoft Word Online | 16.0.17628.20144 | Edición del informe regulatorio final |
| Microsoft Excel Online | 16.0.17628.20144 | Creación y edición de la matriz de impacto regulatorio |

### Configuración Inicial

Antes de comenzar, verifica tu entorno:

1. Abre **Microsoft Edge** y navega a `https://m365.cloud.microsoft/chat`
2. Confirma que ves la interfaz de **Microsoft 365 Copilot Chat** y que los agentes preconstruidos están disponibles en el panel lateral o mediante el selector de agentes
3. En una pestaña nueva, navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-01/`
4. Verifica que existen los archivos:
   - `análisis_fondos_comparativo.docx`
   - `tabla_metricas_fondos.xlsx`
5. Navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/` y confirma que la carpeta existe y está vacía
6. Descarga temporalmente a tu equipo local ambos archivos del Lab 02-00-01 (los necesitarás para cargarlos en las conversaciones con los agentes)

> **⏱ Tiempo estimado para configuración inicial:** 5 minutos

---

## 6. Instrucciones Paso a Paso

### Paso 1: Definición del Alcance Regulatorio con el Agente Asistente de Solicitudes

**Objetivo:** Utilizar el agente Asistente de solicitudes para estructurar y delimitar el alcance de la investigación regulatoria, definiendo los organismos, regulaciones y períodos relevantes para la revisión trimestral.

**⏱ Tiempo estimado:** 8 minutos

**Instrucciones:**

1. En Microsoft 365 Copilot Chat (`https://m365.cloud.microsoft/chat`), selecciona el agente **Asistente de solicitudes** desde el selector de agentes disponibles. Si no lo ves directamente, utiliza la barra de búsqueda de agentes y escribe "Asistente de solicitudes" o "Prompt Coach".

2. Carga el archivo `análisis_fondos_comparativo.docx` en la conversación haciendo clic en el ícono de adjuntar archivo (📎) y seleccionando el archivo descargado de tu equipo local.

3. Escribe el siguiente prompt inicial para establecer el contexto:

```
He adjuntado un análisis comparativo de tres fondos de inversión multiactivo (Fondo A: Renta Variable Global, Fondo B: Mixto Conservador, Fondo C: Alternativo Diversificado). Necesito preparar un informe de cumplimiento regulatorio para la revisión trimestral de clientes institucionales en Estados Unidos.

Ayúdame a estructurar una solicitud de investigación regulatoria que cubra:
1. Los organismos reguladores relevantes (SEC, FINRA, y regulaciones derivadas del Dodd-Frank Act)
2. Las regulaciones específicas que podrían impactar estos tres tipos de fondos (Regulation Best Interest, FINRA Rule 4210, requisitos de reporte ESG 2024)
3. El período de revisión (actualizaciones de los últimos 12 meses)
4. Los criterios de priorización por nivel de impacto y urgencia

Organiza la solicitud en un formato estructurado que pueda usar como guía para mi investigación posterior.
```

4. Revisa la respuesta del agente. Debe proporcionarte una solicitud estructurada con secciones claramente definidas. Si la respuesta es demasiado genérica, refina con el siguiente prompt de seguimiento:

```
Necesito que la solicitud sea más específica para el contexto de gestión de inversiones multiactivo. Incluye:
- Para SEC: enfócate en Regulation Best Interest (Reg BI), Form CRS, y las enmiendas recientes a la Investment Advisers Act
- Para FINRA: enfócate en Rule 4210 (margin requirements), Rule 2111 (suitability), y los cambios en requisitos de supervisión
- Para Dodd-Frank: enfócate en las actualizaciones de Volcker Rule y los requisitos de reporting de derivados que afectan fondos alternativos
- Criterios de priorización: clasifica por (a) impacto directo en operaciones del fondo, (b) fecha límite de cumplimiento, (c) penalidades por incumplimiento
```

5. Copia la solicitud estructurada resultante y guárdala en un archivo de texto temporal en tu equipo. La usarás como guía en los pasos siguientes.

**Resultado Esperado:**

El agente Asistente de solicitudes debe generar un documento estructurado que contenga:
- Una lista organizada de al menos 6-8 regulaciones específicas a investigar, agrupadas por organismo regulador (SEC, FINRA, Dodd-Frank)
- Criterios claros de priorización con tres niveles (alto, medio, bajo impacto)
- Un marco temporal definido (últimos 12 meses)
- La conexión explícita entre cada regulación y los tipos de fondos del análisis (renta variable global, mixto conservador, alternativo diversificado)

**Verificación:**

- [ ] La solicitud estructurada menciona al menos 3 regulaciones específicas de la SEC
- [ ] La solicitud incluye al menos 2 reglas de FINRA con sus números de referencia
- [ ] Se incluyen criterios de priorización con niveles definidos
- [ ] La solicitud referencia los tres fondos del Lab 02-00-01 por nombre o tipo

---

### Paso 2: Investigación de Normativas Vigentes con el Agente Investigador

**Objetivo:** Utilizar el agente Investigador para realizar una investigación profunda de las actualizaciones regulatorias identificadas en el Paso 1, obteniendo información detallada sobre cada regulación, sus cambios recientes y sus implicaciones para fondos multiactivo.

**⏱ Tiempo estimado:** 12 minutos

**Instrucciones:**

1. Cambia al agente **Investigador** (Researcher) en Microsoft 365 Copilot Chat. Puedes iniciar una nueva conversación o cambiar el agente activo desde el selector.

2. Carga nuevamente el archivo `análisis_fondos_comparativo.docx` en esta nueva conversación para proporcionar contexto.

3. Utiliza la solicitud estructurada del Paso 1 como base y escribe el siguiente prompt de investigación:

```
Actúa como investigador especializado en regulación financiera de Estados Unidos. He adjuntado un análisis de tres fondos de inversión multiactivo. Necesito una investigación exhaustiva sobre las siguientes actualizaciones regulatorias de los últimos 12 meses que afectan la gestión de clientes de inversión en EE.UU.:

BLOQUE 1 - SEC:
a) Regulation Best Interest (Reg BI): actualizaciones recientes en requisitos de divulgación y estándar de conducta para broker-dealers que recomiendan fondos multiactivo
b) Form CRS: cambios en los requisitos del formulario de resumen de relación con el cliente
c) Enmiendas a la Investment Advisers Act: nuevas obligaciones para asesores de inversión registrados
d) Reglas de reporte ESG 2024: requisitos de la SEC para divulgación de factores ESG en fondos de inversión

BLOQUE 2 - FINRA:
a) Rule 4210 (Margin Requirements): cambios en requisitos de margen que afectan fondos con exposición a derivados
b) Rule 2111 (Suitability): actualizaciones en obligaciones de idoneidad para recomendaciones de fondos
c) Cambios en requisitos de supervisión y compliance para firmas miembros

BLOQUE 3 - Dodd-Frank Act:
a) Actualizaciones de la Volcker Rule que afectan fondos alternativos diversificados
b) Requisitos de reporting de derivados bajo Title VII que impactan fondos con estrategias de cobertura

Para cada regulación, proporciona:
1. Descripción del cambio o actualización
2. Fecha de entrada en vigor o fecha límite de cumplimiento
3. Impacto específico en cada uno de los tres fondos (Fondo A: Renta Variable Global, Fondo B: Mixto Conservador, Fondo C: Alternativo Diversificado)
4. Fuente de referencia (URL del Federal Register, SEC.gov o FINRA.org cuando sea posible)
```

4. Espera a que el agente Investigador procese la solicitud. Dado que es una consulta compleja, puede tomar entre 30 segundos y 2 minutos en generar una respuesta completa.

5. Revisa la respuesta y evalúa la calidad de la investigación. Si algún bloque está incompleto o es superficial, solicita profundización:

```
Necesito más detalle sobre el BLOQUE 1, punto d) (reglas de reporte ESG 2024). Específicamente:
- ¿Cuáles son los requisitos de divulgación de la SEC para fondos que se comercializan como "ESG" o "sostenibles"?
- ¿Cómo afecta la regla "Names Rule" (Investment Company Act Rule 35d-1) enmendada a los fondos multiactivo que incluyen criterios ESG?
- ¿Cuál es el cronograma de implementación?
```

6. Realiza una segunda ronda de investigación enfocada en las regulaciones con mayor impacto potencial:

```
De las regulaciones investigadas, profundiza en las tres que consideres de mayor impacto para una firma que gestiona los tres tipos de fondos mencionados. Para cada una, incluye:
- Texto clave de la regulación o enmienda
- Ejemplos concretos de cómo cambia la operación diaria
- Comparación del requisito anterior vs. el nuevo requisito
- Riesgos de incumplimiento (multas, sanciones, restricciones operativas)
```

7. Copia toda la investigación resultante (respuestas de ambas rondas) en un documento de Word nuevo. Guárdalo temporalmente como `investigacion_regulatoria_borrador.docx` en tu equipo local.

**Resultado Esperado:**

El agente Investigador debe producir un informe de investigación que contenga:
- Información detallada sobre al menos 7 regulaciones o actualizaciones normativas
- Fechas de entrada en vigor o plazos de cumplimiento para cada regulación
- Análisis diferenciado del impacto por tipo de fondo
- Referencias a fuentes oficiales (SEC.gov, FINRA.org, Federal Register)
- Identificación de las 3 regulaciones de mayor impacto con análisis profundo

**Verificación:**

- [ ] La investigación cubre los tres organismos reguladores (SEC, FINRA, Dodd-Frank)
- [ ] Se incluyen fechas específicas de entrada en vigor o cumplimiento para al menos 5 regulaciones
- [ ] El impacto se diferencia por tipo de fondo (no es genérico)
- [ ] Se proporcionan al menos 3 referencias a fuentes oficiales
- [ ] Se identifican claramente las regulaciones de mayor impacto

> **💡 Nota importante:** El agente Investigador utiliza información de entrenamiento y búsqueda web. Las fechas y detalles regulatorios deben verificarse contra fuentes oficiales en un entorno de producción real. Para efectos de este laboratorio, trabaja con la información proporcionada por el agente como base de análisis.

---

### Paso 3: Análisis de Impacto Regulatorio con el Agente Analista

**Objetivo:** Emplear el agente Analista para cruzar las regulaciones investigadas con los datos de los fondos del Lab 02-00-01, generando una matriz cuantitativa de impacto regulatorio y visualizaciones que faciliten la toma de decisiones.

**⏱ Tiempo estimado:** 12 minutos

**Instrucciones:**

1. Cambia al agente **Analista** (Analyst) en Microsoft 365 Copilot Chat. Inicia una nueva conversación.

2. Carga el archivo `tabla_metricas_fondos.xlsx` del Lab 02-00-01 en la conversación. Este archivo contiene las métricas comparativas de los tres fondos (rendimiento, volatilidad, Sharpe ratio, composición de activos, etc.).

3. Escribe el siguiente prompt para establecer el contexto de análisis:

```
He cargado un archivo Excel con métricas comparativas de tres fondos de inversión multiactivo. Necesito que analices los datos y luego crees una matriz de impacto regulatorio.

Primero, examina el archivo y describe:
1. La estructura de datos (columnas, filas, tipos de datos)
2. Las métricas clave de cada fondo
3. La composición de activos de cada fondo (porcentajes por clase de activo)

Esto me servirá como base para el análisis de impacto regulatorio que haré a continuación.
```

4. Una vez que el agente Analista haya descrito la estructura de datos, procede con el análisis de impacto cruzado:

```
Ahora necesito que crees una matriz de impacto regulatorio. Basándote en los datos del archivo y en las siguientes regulaciones, asigna un puntaje de impacto de 1 a 5 (1=mínimo, 5=crítico) para cada combinación fondo-regulación:

REGULACIONES A EVALUAR:
1. SEC Regulation Best Interest (Reg BI) - requisitos de divulgación ampliados
2. SEC ESG Disclosure Rules 2024 - reporte obligatorio de factores ESG
3. SEC Names Rule Amendment - restricciones de nomenclatura para fondos
4. FINRA Rule 4210 (Margin Requirements) - cambios en requisitos de margen para derivados
5. FINRA Rule 2111 (Suitability) - estándar actualizado de idoneidad
6. Dodd-Frank Volcker Rule Updates - restricciones a inversiones propietarias
7. Dodd-Frank Title VII Derivatives Reporting - reporte de posiciones en derivados

CRITERIOS DE PUNTUACIÓN:
- Considera la composición de activos de cada fondo (un fondo con más derivados será más impactado por reglas de margen)
- Considera el perfil de riesgo (un fondo conservador tiene diferentes implicaciones de suitability)
- Considera la exposición geográfica y sectorial

Genera:
1. Una tabla con la matriz de impacto (filas: regulaciones, columnas: fondos + puntaje promedio)
2. Un puntaje total de impacto por fondo
3. Una clasificación de urgencia: Alta (puntaje 4-5), Media (puntaje 2-3), Baja (puntaje 1)
```

5. Revisa la matriz generada. Si el agente Analista ha ejecutado código Python para los cálculos, verifica que los puntajes sean coherentes con la composición de los fondos. Si detectas inconsistencias, solicita ajustes:

```
Revisa los puntajes asignados considerando lo siguiente:
- El Fondo C (Alternativo Diversificado) debería tener mayor impacto en Volcker Rule y Derivatives Reporting dado que típicamente incluye estrategias alternativas con derivados
- El Fondo B (Mixto Conservador) debería tener menor impacto en reglas de margen pero mayor sensibilidad a cambios en suitability por su perfil de cliente conservador
- El Fondo A (Renta Variable Global) debería tener alto impacto en ESG Disclosure si tiene exposición a mercados con requisitos ESG

Ajusta la matriz y recalcula los totales.
```

6. Solicita la generación de visualizaciones:

```
Genera las siguientes visualizaciones basadas en la matriz de impacto:
1. Un gráfico de calor (heatmap) que muestre la intensidad del impacto regulatorio por fondo y regulación
2. Un gráfico de barras apiladas que muestre el impacto total por fondo, desglosado por regulación
3. Un gráfico de radar que compare el perfil de impacto regulatorio de los tres fondos

Adicionalmente, genera una tabla resumen con:
- Top 3 combinaciones fondo-regulación de mayor impacto
- Fecha límite de cumplimiento estimada para cada una
- Acción requerida principal
```

7. Exporta los resultados. Solicita al agente:

```
Genera un archivo Excel descargable que contenga:
- Hoja 1: "Matriz de Impacto" - la tabla completa con puntajes
- Hoja 2: "Resumen Ejecutivo" - top combinaciones de mayor impacto con acciones requeridas
- Hoja 3: "Datos de Soporte" - las métricas de los fondos utilizadas para la evaluación
```

8. Descarga el archivo Excel generado por el agente Analista. Renómbralo como `matriz_impacto_regulatorio.xlsx` y guárdalo en tu equipo local.

9. Sube el archivo `matriz_impacto_regulatorio.xlsx` a la carpeta SharePoint del laboratorio:
   - Navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/`
   - Haz clic en **Cargar** > **Archivos** y selecciona el archivo

**Resultado Esperado:**

El agente Analista debe producir:
- Una matriz de impacto con puntajes de 1-5 para cada combinación de 7 regulaciones × 3 fondos (21 celdas de evaluación)
- Al menos 2 visualizaciones (heatmap y gráfico de barras como mínimo)
- Un archivo Excel descargable con múltiples hojas
- Identificación clara de las 3 combinaciones de mayor impacto
- Puntajes totales por fondo que reflejen coherentemente su composición de activos

**Verificación:**

- [ ] La matriz contiene puntajes para las 21 combinaciones fondo-regulación
- [ ] Los puntajes son coherentes con la composición de activos de cada fondo (ej.: Fondo C tiene mayor impacto en regulaciones de derivados)
- [ ] Se generaron al menos 2 visualizaciones legibles
- [ ] El archivo `matriz_impacto_regulatorio.xlsx` se descargó correctamente
- [ ] El archivo fue subido exitosamente a la carpeta `/Lab-02-00-02/` en SharePoint

---

### Paso 4: Generación de Estrategias de Adaptación con el Agente Entrenador de Ideas

**Objetivo:** Utilizar el agente Entrenador de ideas para generar estrategias creativas y viables de adaptación y cumplimiento ante las regulaciones de mayor impacto identificadas en el Paso 3.

**⏱ Tiempo estimado:** 8 minutos

**Instrucciones:**

1. Cambia al agente **Entrenador de ideas** (Idea Coach) en Microsoft 365 Copilot Chat. Inicia una nueva conversación.

2. Proporciona el contexto completo del análisis realizado hasta ahora:

```
Soy analista de cumplimiento en una firma de gestión de inversiones en EE.UU. He completado un análisis de impacto regulatorio para tres fondos:
- Fondo A: Renta Variable Global (alto impacto en ESG Disclosure y Reg BI)
- Fondo B: Mixto Conservador (alto impacto en Suitability y Reg BI)
- Fondo C: Alternativo Diversificado (alto impacto en Volcker Rule, Derivatives Reporting y Margin Requirements)

Las tres combinaciones de mayor impacto crítico identificadas son:
1. Fondo C + Dodd-Frank Volcker Rule Updates (puntaje 5/5)
2. Fondo C + FINRA Rule 4210 Margin Requirements (puntaje 4-5/5)
3. Fondo A + SEC ESG Disclosure Rules 2024 (puntaje 4-5/5)

Necesito que me ayudes a generar estrategias de adaptación y cumplimiento para cada una de estas tres áreas críticas. Para cada estrategia, quiero:
1. Descripción de la estrategia
2. Pasos de implementación (3-5 pasos concretos)
3. Recursos necesarios (personal, tecnología, presupuesto estimado)
4. Cronograma sugerido de implementación
5. Indicadores de éxito (KPIs de cumplimiento)
```

3. Revisa las estrategias generadas. Solicita expansión en áreas donde necesites más creatividad:

```
Para la estrategia de cumplimiento ESG del Fondo A, necesito ideas más innovadoras. Considera:
- ¿Cómo podemos convertir el cumplimiento ESG en una ventaja competitiva frente a competidores?
- ¿Qué herramientas tecnológicas podrían automatizar el reporte ESG?
- ¿Cómo comunicamos los cambios ESG a clientes institucionales de manera que refuerce la confianza?

Genera al menos 3 ideas adicionales que vayan más allá del cumplimiento mínimo.
```

4. Solicita una visión integrada:

```
Ahora genera una estrategia integrada que aborde las tres áreas críticas de manera coordinada. Quiero evitar esfuerzos duplicados y maximizar sinergias. Por ejemplo:
- ¿Puede un mismo sistema de reporting cubrir tanto ESG Disclosure como Derivatives Reporting?
- ¿Puede la actualización del proceso de suitability del Fondo B servir como modelo para Reg BI en los tres fondos?
- ¿Qué capacitaciones pueden cubrir múltiples requisitos regulatorios simultáneamente?

Presenta la estrategia integrada en formato de plan de acción con fases (Fase 1: 0-30 días, Fase 2: 30-90 días, Fase 3: 90-180 días).
```

5. Copia todas las estrategias generadas (individuales + integrada) y agrégalas al archivo `investigacion_regulatoria_borrador.docx` que creaste en el Paso 2.

**Resultado Esperado:**

El agente Entrenador de ideas debe generar:
- Al menos 3 estrategias individuales detalladas (una por área crítica) con pasos de implementación, recursos y KPIs
- Al menos 3 ideas innovadoras adicionales para el cumplimiento ESG
- Una estrategia integrada con plan de acción en 3 fases temporales
- Identificación de sinergias entre los distintos requisitos regulatorios

**Verificación:**

- [ ] Cada estrategia individual incluye al menos 3 pasos de implementación concretos
- [ ] Se incluyen KPIs medibles para cada estrategia
- [ ] La estrategia integrada identifica al menos 2 sinergias entre requisitos regulatorios
- [ ] El plan de acción tiene 3 fases con plazos definidos
- [ ] Las estrategias son realistas y aplicables a una firma de gestión de inversiones

---

### Paso 5: Redacción del Informe de Cumplimiento Regulatorio con el Agente Asesor de Escritura

**Objetivo:** Utilizar el agente Asesor de escritura para producir un informe de cumplimiento regulatorio profesional que integre todos los hallazgos de los pasos anteriores en un documento formal listo para la revisión trimestral de clientes institucionales.

**⏱ Tiempo estimado:** 12 minutos

**Instrucciones:**

1. Cambia al agente **Asesor de escritura** (Writing Coach) en Microsoft 365 Copilot Chat. Inicia una nueva conversación.

2. Carga el archivo `investigacion_regulatoria_borrador.docx` (que contiene la investigación del Paso 2 y las estrategias del Paso 4) en la conversación.

3. Proporciona las instrucciones de redacción:

```
He adjuntado un borrador con investigación regulatoria y estrategias de cumplimiento. Necesito que me ayudes a redactar un informe formal de cumplimiento regulatorio para la revisión trimestral de clientes institucionales.

El informe debe tener la siguiente estructura:

1. PORTADA
   - Título: "Informe de Cumplimiento Regulatorio - Revisión Trimestral Q[X] 2024"
   - Subtítulo: "Análisis de Impacto Regulatorio para Fondos Multiactivo"
   - Preparado por: [Nombre del analista]
   - Fecha: [Fecha actual]
   - Clasificación: Confidencial - Uso Interno

2. RESUMEN EJECUTIVO (máximo 300 palabras)
   - Hallazgos clave
   - Regulaciones de mayor impacto
   - Recomendaciones principales

3. ALCANCE DE LA REVISIÓN
   - Organismos reguladores cubiertos
   - Período de revisión
   - Fondos bajo análisis

4. ACTUALIZACIONES REGULATORIAS IDENTIFICADAS
   - 4.1 Securities and Exchange Commission (SEC)
   - 4.2 Financial Industry Regulatory Authority (FINRA)
   - 4.3 Dodd-Frank Act y regulaciones derivadas

5. ANÁLISIS DE IMPACTO POR FONDO
   - 5.1 Fondo A: Renta Variable Global
   - 5.2 Fondo B: Mixto Conservador
   - 5.3 Fondo C: Alternativo Diversificado
   - 5.4 Matriz consolidada de impacto (referencia al archivo Excel adjunto)

6. ESTRATEGIAS DE ADAPTACIÓN Y CUMPLIMIENTO
   - 6.1 Acciones inmediatas (0-30 días)
   - 6.2 Acciones a mediano plazo (30-90 días)
   - 6.3 Acciones a largo plazo (90-180 días)

7. RECOMENDACIONES Y PRÓXIMOS PASOS

8. ANEXOS
   - Referencia a matriz_impacto_regulatorio.xlsx
   - Fuentes consultadas

TONO Y ESTILO:
- Formal y profesional, apropiado para audiencia de directivos y clientes institucionales
- Preciso en terminología regulatoria (usar nombres oficiales de regulaciones)
- Orientado a la acción (cada sección debe terminar con implicaciones prácticas)
- Extensión total: 2,000-3,000 palabras
```

4. Revisa el borrador generado por el agente. Solicita mejoras específicas de estilo y contenido:

```
Revisa el informe generado y mejora los siguientes aspectos:
1. El Resumen Ejecutivo debe ser más impactante - incluye una frase de apertura que capture la urgencia de las actualizaciones regulatorias
2. En la sección 4 (Actualizaciones Regulatorias), asegúrate de que cada regulación tenga un formato consistente: Nombre oficial → Descripción del cambio → Fecha de cumplimiento → Impacto esperado
3. En la sección 5 (Análisis de Impacto), incluye una tabla resumen al inicio que muestre el puntaje de impacto total por fondo
4. En la sección 6 (Estrategias), cada acción debe tener un responsable sugerido (ej: "Equipo de Compliance", "Gestores de Portafolio", "Legal")
5. Verifica que la terminología regulatoria sea correcta y consistente en todo el documento
```

5. Solicita una revisión final de calidad:

```
Realiza una revisión final del informe considerando:
- Coherencia: ¿las recomendaciones de la sección 7 se alinean con los hallazgos de las secciones 4 y 5?
- Completitud: ¿se cubren todas las regulaciones mencionadas en el alcance?
- Claridad: ¿un director de inversiones sin expertise regulatoria profunda podría entender las implicaciones?
- Profesionalismo: ¿el tono es apropiado para una revisión trimestral de clientes institucionales?

Haz las correcciones necesarias y genera la versión final.
```

6. Copia el informe final completo y crea un nuevo documento en **Word Online**:
   - Navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/`
   - Haz clic en **+ Nuevo** > **Documento de Word**
   - Nombra el archivo como `informe_regulatorio_EEUU.docx`
   - Pega el contenido del informe
   - Aplica formato básico: títulos con estilos de encabezado (Heading 1, Heading 2, Heading 3), tablas formateadas, numeración de secciones
   - Guarda el documento (se guarda automáticamente en SharePoint)

7. Verifica que ambos archivos de salida estén en la carpeta SharePoint:
   - `informe_regulatorio_EEUU.docx`
   - `matriz_impacto_regulatorio.xlsx`

**Resultado Esperado:**

El agente Asesor de escritura debe producir un informe que contenga:
- Las 8 secciones solicitadas con contenido sustantivo
- Resumen ejecutivo de máximo 300 palabras
- Formato consistente para cada regulación (nombre, cambio, fecha, impacto)
- Tablas resumen integradas
- Estrategias con responsables asignados y plazos
- Tono profesional apropiado para audiencia ejecutiva e institucional
- Extensión entre 2,000-3,000 palabras

**Verificación:**

- [ ] El informe contiene las 8 secciones requeridas
- [ ] El Resumen Ejecutivo no excede 300 palabras y menciona los hallazgos clave
- [ ] Cada regulación sigue el formato consistente: nombre → cambio → fecha → impacto
- [ ] Las estrategias incluyen responsables y plazos
- [ ] El archivo `informe_regulatorio_EEUU.docx` está guardado en `/Lab-02-00-02/` en SharePoint
- [ ] El archivo `matriz_impacto_regulatorio.xlsx` está guardado en `/Lab-02-00-02/` en SharePoint
- [ ] Ambos archivos son accesibles y se abren correctamente desde SharePoint

---

## 7. Validación y Pruebas

### Validación de Entregables

Realiza las siguientes verificaciones finales para confirmar que el laboratorio se completó exitosamente:

**Verificación de archivos en SharePoint:**

1. Navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/`
2. Confirma la presencia de los dos archivos de salida:

| Archivo | Formato | Contenido Esperado | ✓ |
|---|---|---|---|
| `informe_regulatorio_EEUU.docx` | Word | Informe de cumplimiento regulatorio con 8 secciones, 2,000-3,000 palabras | ☐ |
| `matriz_impacto_regulatorio.xlsx` | Excel | Matriz de impacto con puntajes 1-5 para 7 regulaciones × 3 fondos, mínimo 2 hojas | ☐ |

**Verificación de calidad del informe (`informe_regulatorio_EEUU.docx`):**

| Criterio | Requisito | ✓ |
|---|---|---|
| Estructura | 8 secciones completas con numeración | ☐ |
| Resumen Ejecutivo | ≤ 300 palabras, menciona hallazgos clave y recomendaciones | ☐ |
| Cobertura regulatoria | Mínimo 7 regulaciones de 3 organismos (SEC, FINRA, Dodd-Frank) | ☐ |
| Análisis por fondo | Secciones diferenciadas para Fondo A, B y C | ☐ |
| Estrategias | Plan de acción en 3 fases con responsables y plazos | ☐ |
| Tono | Formal, profesional, orientado a acción | ☐ |
| Referencias | Mención de fuentes oficiales y del archivo Excel adjunto | ☐ |

**Verificación de calidad de la matriz (`matriz_impacto_regulatorio.xlsx`):**

| Criterio | Requisito | ✓ |
|---|---|---|
| Completitud | 21 celdas de evaluación (7 regulaciones × 3 fondos) | ☐ |
| Coherencia | Puntajes reflejan la composición de activos de cada fondo | ☐ |
| Totales | Puntaje total por fondo calculado correctamente | ☐ |
| Múltiples hojas | Mínimo 2 hojas (Matriz de Impacto + Resumen) | ☐ |

**Verificación de flujo de trabajo entre agentes:**

| Paso | Agente Utilizado | Output Generado | Usado como Input en | ✓ |
|---|---|---|---|---|
| 1 | Asistente de solicitudes | Solicitud estructurada de investigación | Paso 2 (Investigador) | ☐ |
| 2 | Investigador | Investigación regulatoria detallada | Pasos 3, 4 y 5 | ☐ |
| 3 | Analista | Matriz de impacto regulatorio (.xlsx) | Pasos 4 y 5 | ☐ |
| 4 | Entrenador de ideas | Estrategias de adaptación | Paso 5 | ☐ |
| 5 | Asesor de escritura | Informe final (.docx) | Lab 02-00-03 | ☐ |

---

## 8. Solución de Problemas

### Problema 1: El Agente Analista No Genera el Archivo Excel Descargable

**Síntomas:**
- El agente Analista muestra la matriz de impacto como texto o tabla en la conversación, pero no ofrece un enlace de descarga de archivo Excel
- Al solicitar "genera un archivo Excel descargable", el agente responde con instrucciones para crear el archivo manualmente en lugar de generarlo automáticamente
- El código Python se ejecuta pero el output no incluye un archivo `.xlsx`

**Causa:**
El agente Analista genera archivos descargables mediante la ejecución de código Python con bibliotecas como `openpyxl` o `pandas`. En algunas sesiones, si la solicitud no es suficientemente explícita sobre el formato de salida, o si la sesión ha acumulado demasiado contexto, el agente puede optar por mostrar resultados en texto en lugar de generar un archivo. También puede ocurrir si el entorno de ejecución de Python tiene restricciones temporales en la generación de archivos.

**Solución:**

1. Inicia una nueva conversación con el agente Analista para limpiar el contexto acumulado.

2. Carga nuevamente el archivo `tabla_metricas_fondos.xlsx`.

3. Usa un prompt más directo que fuerce la generación del archivo:

```
Necesito que generes un archivo Excel (.xlsx) descargable. Usa Python con la biblioteca openpyxl o pandas para crear un archivo con las siguientes hojas:

Hoja "Matriz_Impacto": Crea una tabla con las siguientes columnas: Regulación, Fondo_A_RV_Global, Fondo_B_Mixto_Conservador, Fondo_C_Alternativo, Promedio. Las filas son: Reg BI (3,4,3), ESG Disclosure (5,2,3), Names Rule (3,2,2), FINRA 4210 (2,2,5), FINRA 2111 (3,4,3), Volcker Rule (2,2,5), Derivatives Reporting (2,2,5). Calcula los promedios.

Hoja "Resumen": Lista las top 3 combinaciones de mayor puntaje con columnas: Ranking, Fondo, Regulación, Puntaje, Acción_Requerida.

Genera el archivo y proporciona el enlace de descarga.
```

4. Si aún no genera el archivo, copia los datos tabulares de la respuesta del agente y créalos manualmente en Excel Online:
   - Navega a la carpeta `/Lab-02-00-02/` en SharePoint
   - Haz clic en **+ Nuevo** > **Libro de Excel**
   - Nombra el archivo `matriz_impacto_regulatorio.xlsx`
   - Crea las hojas y pega los datos de la conversación del agente

---

### Problema 2: El Agente Investigador Proporciona Información Regulatoria Genérica o Desactualizada

**Síntomas:**
- El agente Investigador responde con descripciones generales de las regulaciones (ej.: "La SEC regula los mercados de valores...") en lugar de actualizaciones específicas recientes
- Las fechas mencionadas son anteriores al período de revisión solicitado (últimos 12 meses)
- No se proporcionan referencias específicas a enmiendas, reglas finales o propuestas recientes
- Las respuestas no diferencian el impacto por tipo de fondo

**Causa:**
El agente Investigador basa sus respuestas en su conocimiento de entrenamiento y, cuando está disponible, en búsqueda web. Si el prompt es demasiado amplio o no especifica suficiente contexto, el agente tiende a proporcionar información de nivel introductorio en lugar de actualizaciones específicas. Además, la fecha de corte del conocimiento del modelo puede limitar la información sobre regulaciones muy recientes.

**Solución:**

1. Reformula el prompt con mayor especificidad temporal y técnica:

```
Necesito actualizaciones regulatorias ESPECÍFICAS y RECIENTES (2023-2024) para la gestión de fondos de inversión en EE.UU. NO necesito descripciones generales de qué es la SEC o FINRA.

Para cada regulación, necesito:
- El NÚMERO de la regla o enmienda específica (ej: "SEC Release No. 34-XXXXX")
- La FECHA exacta de publicación o entrada en vigor
- El CAMBIO ESPECÍFICO respecto a la regulación anterior
- El IMPACTO CONCRETO en fondos multiactivo

Ejemplo del nivel de detalle que necesito:
"SEC Regulation Best Interest (Reg BI) - Enmienda de junio 2023: Se amplió el requisito de divulgación del Form CRS para incluir información sobre conflictos de interés en la recomendación de fondos multiactivo con componentes alternativos. Fecha límite de cumplimiento: [fecha]. Impacto: Las firmas deben actualizar sus formularios CRS para todos los clientes retail que inviertan en fondos con más del 20% en activos alternativos."

Ahora proporciona este nivel de detalle para las 7 regulaciones que te solicité anteriormente.
```

2. Si el agente sigue siendo genérico, divide la solicitud en consultas individuales:

```
Enfócate ÚNICAMENTE en SEC Regulation Best Interest (Reg BI). ¿Cuáles son las actualizaciones, enmiendas o guías interpretativas publicadas por la SEC entre enero 2023 y la fecha actual respecto a Reg BI? Incluye números de release, fechas y cambios específicos.
```

3. Repite la consulta individual para cada regulación (FINRA Rule 4210, ESG Disclosure, etc.).

4. Si las fechas proporcionadas no son verificables, añade una nota en el informe final indicando: *"Las fechas regulatorias incluidas en este informe son aproximadas y deben verificarse contra las publicaciones oficiales en SEC.gov y FINRA.org antes de su uso en decisiones de cumplimiento."*

---

## 9. Limpieza del Entorno

Al finalizar el laboratorio, realiza las siguientes acciones de limpieza:

1. **Archivos locales temporales:** Elimina de tu equipo local los archivos descargados temporalmente:
   - `análisis_fondos_comparativo.docx` (copia local del Lab 02-00-01)
   - `tabla_metricas_fondos.xlsx` (copia local del Lab 02-00-01)
   - `investigacion_regulatoria_borrador.docx` (borrador temporal)
   - Cualquier archivo Excel temporal descargado del agente Analista

2. **Conversaciones de Copilot Chat:** Las conversaciones con los agentes se mantienen en tu historial de Copilot Chat. No es necesario eliminarlas, ya que pueden servir como referencia. Sin embargo, si deseas limpiar:
   - En Copilot Chat, navega al historial de conversaciones
   - Identifica las 5 conversaciones de este laboratorio (una por agente)
   - Opcionalmente, elimínalas haciendo clic en los tres puntos (⋯) > **Eliminar**

3. **Archivos en SharePoint — NO ELIMINAR:**
   > ⚠️ **IMPORTANTE:** Los archivos `informe_regulatorio_EEUU.docx` y `matriz_impacto_regulatorio.xlsx` en la carpeta `/Lab-02-00-02/` **NO deben eliminarse**. Son insumos requeridos para el **Lab 02-00-03**.

4. **Verificación final de SharePoint:**
   - Confirma que la carpeta `/Lab-02-00-02/` contiene exactamente 2 archivos
   - Confirma que los archivos del `/Lab-02-00-01/` no fueron modificados ni eliminados

---

## 10. Resumen

### Logros del Laboratorio

En este laboratorio completaste un flujo de investigación regulatoria integral utilizando los cinco agentes preconstruidos de Microsoft 365 Copilot en secuencia coordinada:

| Paso | Agente | Acción Realizada | Entregable |
|---|---|---|---|
| 1 | Asistente de solicitudes | Estructuración del alcance regulatorio | Solicitud de investigación estructurada |
| 2 | Investigador | Investigación de actualizaciones SEC, FINRA y Dodd-Frank | Investigación regulatoria detallada |
| 3 | Analista | Análisis cuantitativo de impacto cruzado regulación-fondo | `matriz_impacto_regulatorio.xlsx` |
| 4 | Entrenador de ideas | Generación de estrategias de adaptación y cumplimiento | Estrategias con plan de acción en 3 fases |
| 5 | Asesor de escritura | Redacción del informe formal de cumplimiento | `informe_regulatorio_EEUU.docx` |

### Competencias Desarrolladas

- **Creación de flujos de trabajo multi-agente:** Aprendiste a encadenar la salida de un agente como entrada del siguiente, creando un pipeline de análisis regulatorio replicable.
- **Prompt engineering avanzado:** Practicaste la formulación de prompts con contexto específico, criterios de evaluación cuantitativos y requisitos de formato para obtener resultados profesionales.
- **Análisis de impacto regulatorio:** Aplicaste el agente Analista para generar evaluaciones cuantitativas cruzando datos de fondos con requisitos regulatorios, aprovechando su capacidad de ejecutar código Python de forma autónoma.
- **Producción de documentos profesionales:** Utilizaste el agente Asesor de escritura para transformar investigación y análisis en un informe formal con estructura, tono y nivel de detalle apropiados para audiencia ejecutiva.

### Conexión con Laboratorios Posteriores

Los archivos generados en este laboratorio (`informe_regulatorio_EEUU.docx` y `matriz_impacto_regulatorio.xlsx`) serán utilizados en el **Lab 02-00-03** como contexto para la comunicación de resultados de portafolio. En ese laboratorio, integrarás los hallazgos regulatorios con el borrador de comunicación a clientes (`borrador_comunicacion_portafolio.docx`) para producir una comunicación que aborde tanto el rendimiento del portafolio como las implicaciones regulatorias.

### Recursos Adicionales

| Recurso | URL |
|---|---|
| SEC - Regulation Best Interest | `https://www.sec.gov/regulation-best-interest` |
| FINRA - Reglas y Guías | `https://www.finra.org/rules-guidance` |
| Dodd-Frank Act - Texto completo | `https://www.congress.gov/bill/111th-congress/house-bill/4173` |
| Agentes preconstruidos M365 Copilot | `https://learn.microsoft.com/es-es/microsoft-365-copilot/agents-overview` |
| Seguridad y privacidad en M365 Copilot | `https://learn.microsoft.com/es-es/microsoft-365-copilot/microsoft-365-copilot-privacy` |

---

# Práctica: Mejora de una comunicación sobre resultados de una revisión de portafolio

## Metadatos del Laboratorio

| Campo | Detalle |
|---|---|
| **Duración** | 32 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Crear |
| **Módulo** | 2 — Agentes preconstruidos de Microsoft 365 Copilot |
| **Posición** | Laboratorio de cierre del Módulo 2 |

---

## Descripción General

En este laboratorio consolidarás el uso encadenado de los cinco agentes preconstruidos de Microsoft 365 Copilot para transformar un borrador técnico de resultados de portafolio en una comunicación profesional orientada al cliente. Partirás del archivo `borrador_comunicacion_portafolio.docx` y lo enriquecerás con los outputs generados en los Labs 02-00-01 y 02-00-02 (análisis comparativo de fondos e informe regulatorio). El flujo de trabajo sigue una secuencia deliberada: verificación de consistencia de datos (Analista), enriquecimiento con contexto de mercado (Investigador), generación de variantes por perfil de cliente (Entrenador de ideas), refinamiento profesional del texto (Asesor de escritura) y coordinación del flujo completo (Asistente de solicitudes). El entregable final — `comunicacion_portafolio_final.docx` — representa el cierre del Módulo 2 y servirá como referencia de calidad para los laboratorios del Módulo 3.

---

## Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Aplicar el agente Asesor de escritura para transformar un borrador técnico de resultados de portafolio en una comunicación clara, profesional y orientada al cliente
- [ ] Utilizar el agente Entrenador de ideas para generar variantes del mensaje principal adaptadas a tres perfiles de cliente distintos (institucional, retail, family office)
- [ ] Emplear el agente Analista para verificar la consistencia y precisión de los datos financieros incluidos en la comunicación frente a los informes de los Labs anteriores
- [ ] Usar el agente Investigador para incorporar referencias de mercado actualizadas que refuercen los mensajes clave de la comunicación
- [ ] Producir una versión final pulida que integre los hallazgos de análisis de fondos y cumplimiento regulatorio de los laboratorios anteriores

---

## Prerrequisitos

### Conocimientos Previos

| Requisito | Detalle |
|---|---|
| Labs anteriores completados | Labs 02-00-01 y 02-00-02 finalizados con todos los archivos de salida generados |
| Agentes preconstruidos | Dominio práctico de los cinco agentes preconstruidos adquirido en los laboratorios previos |
| Prompt engineering básico | Capacidad de formular instrucciones claras y específicas en lenguaje natural |
| Conceptos financieros | Comprensión básica de métricas de portafolio (rendimiento, volatilidad, Sharpe ratio, drawdown) |

### Acceso y Archivos Requeridos

| Recurso | Ubicación / Detalle |
|---|---|
| Licencia M365 Copilot Premium | Activa y asignada al menos 24 horas antes del laboratorio |
| Sitio SharePoint del curso | `https://[tenant].sharepoint.com/sites/CursoAgentes` — rol de Miembro o superior |
| `borrador_comunicacion_portafolio.docx` | `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-03/` |
| `análisis_fondos_comparativo.docx` | `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-01/` (generado en Lab 02-00-01) |
| `tabla_metricas_fondos.xlsx` | `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-01/` (generado en Lab 02-00-01) |
| `informe_regulatorio_EEUU.docx` | `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/` (generado en Lab 02-00-02) |
| `matriz_impacto_regulatorio.xlsx` | `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-02/` (generado en Lab 02-00-02) |

---

## Entorno del Laboratorio

### Hardware Mínimo

| Componente | Especificación |
|---|---|
| Procesador | 64 bits, 4 núcleos (Intel Core i5 8.ª gen. o AMD Ryzen 5 equivalente) |
| RAM | 8 GB mínimo (16 GB recomendado) |
| Almacenamiento disponible | 10 GB libres (SSD recomendado) |
| Pantalla | 1920×1080 (Full HD) |
| Conexión a internet | 10 Mbps bajada / 5 Mbps subida (25 Mbps simétrico recomendado) |

### Software Requerido

| Software | Versión | Propósito en este lab |
|---|---|---|
| Microsoft Edge | 124.0.2478.97+ | Navegador principal para acceder a M365 Copilot Chat |
| Microsoft 365 Copilot Chat | Build de producción mayo 2024 | Interfaz de interacción con los cinco agentes preconstruidos |
| Microsoft Word Online | Integrado en M365 | Edición y entrega del documento final |
| Microsoft SharePoint Online | 16.0.24211.12000 | Repositorio de documentos de entrada y salida |
| Microsoft OneDrive for Business | 24.071.0407.0003 | Sincronización de archivos si se trabaja localmente |

### Configuración Inicial

1. Abre **Microsoft Edge** y navega a `https://m365.cloud.microsoft/chat`.
2. Inicia sesión con tu cuenta del tenant del curso.
3. Verifica que en la interfaz de Copilot Chat aparezcan los agentes preconstruidos haciendo clic en el ícono de **agentes** (ícono de persona con engranaje) en el panel lateral o en la barra superior.
4. Confirma que puedes ver los cinco agentes: **Analista**, **Investigador**, **Entrenador de ideas**, **Asesor de escritura** y **Asistente de solicitudes**.
5. En otra pestaña del navegador, navega a `https://[tenant].sharepoint.com/sites/CursoAgentes/Documentos compartidos/Lab-02-00-03/` y confirma que el archivo `borrador_comunicacion_portafolio.docx` está presente.
6. Navega también a las carpetas `/Lab-02-00-01/` y `/Lab-02-00-02/` para confirmar que los archivos de salida de los laboratorios anteriores están disponibles.

> **⚠️ Importante:** Si alguno de los archivos de los Labs anteriores no está disponible, contacta a tu instructor antes de continuar. Este laboratorio depende directamente de esos outputs.

---

## Instrucciones Paso a Paso

### Paso 1: Revisar el borrador original y descargar los archivos de contexto

**Objetivo:** Familiarizarte con el contenido del borrador de comunicación y preparar todos los archivos necesarios para cargarlos en las sesiones de los agentes.

**Instrucciones:**

1. En SharePoint, navega a `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-03/`.
2. Haz clic en `borrador_comunicacion_portafolio.docx` para abrirlo en **Word Online**.
3. Lee el documento completo. Identifica y toma nota mental de:
   - Las cifras de rendimiento mencionadas para cada fondo (Fondo A, Fondo B, Fondo C).
   - El tono general del documento (técnico, informal, neutro).
   - Las secciones que contiene (resumen ejecutivo, detalle por fondo, conclusiones, recomendaciones).
   - Cualquier dato que parezca incompleto o que requiera contexto adicional.
4. Descarga los siguientes archivos a tu equipo local (los necesitarás para cargarlos en Copilot Chat):
   - `/Lab-02-00-03/borrador_comunicacion_portafolio.docx`
   - `/Lab-02-00-01/análisis_fondos_comparativo.docx`
   - `/Lab-02-00-01/tabla_metricas_fondos.xlsx`
   - `/Lab-02-00-02/informe_regulatorio_EEUU.docx`
   - `/Lab-02-00-02/matriz_impacto_regulatorio.xlsx`

   Para descargar cada archivo: haz clic en los **tres puntos (⋯)** junto al nombre del archivo → selecciona **Descargar**.

5. Crea una carpeta local temporal llamada `Lab-02-00-03-Archivos` y coloca allí los cinco archivos descargados.

**Resultado esperado:** Tienes una comprensión clara del estado actual del borrador y los cinco archivos están descargados y accesibles localmente para carga en Copilot Chat.

**Verificación:**
- [ ] Puedes describir al menos tres problemas o áreas de mejora del borrador original
- [ ] Los cinco archivos están en tu carpeta local `Lab-02-00-03-Archivos`

> **⏱️ Tiempo estimado:** 4 minutos

---

### Paso 2: Verificar consistencia de datos con el Agente Analista

**Objetivo:** Utilizar el agente Analista para comparar los datos financieros del borrador de comunicación con los datos de referencia generados en el Lab 02-00-01, identificando inconsistencias o errores.

**Instrucciones:**

1. En Copilot Chat (`https://m365.cloud.microsoft/chat`), haz clic en el selector de agentes y selecciona **Analista**.
2. Una vez activo el agente Analista, carga los siguientes archivos usando el ícono de **adjuntar archivo** (📎) o arrastrándolos al área de chat:
   - `borrador_comunicacion_portafolio.docx`
   - `tabla_metricas_fondos.xlsx`
3. Escribe el siguiente prompt en el chat:

```
Analiza el documento "borrador_comunicacion_portafolio.docx" y compáralo con los datos del archivo "tabla_metricas_fondos.xlsx". Identifica:

1. Cualquier cifra de rendimiento, volatilidad, ratio de Sharpe o drawdown máximo que sea inconsistente entre ambos documentos.
2. Datos que aparezcan en la tabla de métricas pero no estén mencionados en el borrador.
3. Datos del borrador que no tengan respaldo en la tabla de métricas.

Presenta los resultados en una tabla con las columnas: Dato, Valor en borrador, Valor en tabla de métricas, Estado (Consistente / Inconsistente / Faltante).
```

4. Revisa la respuesta del agente Analista. Espera una tabla comparativa con el estado de cada dato.
5. Si el agente identifica inconsistencias, escribe un prompt de seguimiento:

```
Para cada inconsistencia encontrada, indica cuál es el valor correcto basándote en la tabla de métricas y sugiere la corrección exacta que debería hacerse en el borrador.
```

6. Ahora carga el archivo adicional `análisis_fondos_comparativo.docx` y escribe:

```
Verifica si las conclusiones del borrador de comunicación son coherentes con las conclusiones del análisis comparativo de fondos. Identifica contradicciones o afirmaciones del borrador que no estén respaldadas por el análisis.
```

7. Copia todas las respuestas del agente Analista. Abre un nuevo documento en **Word Online** (desde SharePoint, en la carpeta `/Lab-02-00-03/`, haz clic en **+ Nuevo** → **Documento de Word**) y nómbralo `notas_verificacion_analista.docx`. Pega allí los hallazgos del Analista organizados bajo los encabezados:
   - **Inconsistencias de datos**
   - **Datos faltantes en el borrador**
   - **Contradicciones en conclusiones**

**Resultado esperado:** El agente Analista genera una tabla de verificación que muestra el estado de consistencia de cada dato financiero. Se identifican al menos 1-3 inconsistencias o datos faltantes. Las conclusiones del borrador se validan contra el análisis comparativo.

**Verificación:**
- [ ] La tabla comparativa muestra el estado de al menos 8-10 datos financieros del borrador
- [ ] Se identificaron las correcciones necesarias para cada inconsistencia
- [ ] El archivo `notas_verificacion_analista.docx` está guardado en `/Lab-02-00-03/`

> **⏱️ Tiempo estimado:** 7 minutos

---

### Paso 3: Enriquecer con contexto de mercado usando el Agente Investigador

**Objetivo:** Utilizar el agente Investigador para obtener referencias de mercado actualizadas que refuercen los mensajes clave de la comunicación de portafolio.

**Instrucciones:**

1. En Copilot Chat, cambia al agente **Investigador** usando el selector de agentes.
2. Escribe el siguiente prompt para establecer el contexto:

```
Estoy preparando una comunicación de resultados de portafolio para clientes de una firma de gestión de inversiones. El portafolio incluye tres fondos:
- Fondo A: Renta Variable Global
- Fondo B: Mixto Conservador
- Fondo C: Alternativo Diversificado

Necesito contexto de mercado actualizado para enriquecer la comunicación. Investiga y proporciona:

1. Rendimiento reciente del índice MSCI World y principales índices bursátiles globales (S&P 500, STOXX 600, MSCI Emerging Markets) para contextualizar el desempeño del Fondo A.
2. Tendencias recientes en mercados de renta fija y tasas de interés de bancos centrales principales (Fed, BCE, BoE) para contextualizar el Fondo B.
3. Tendencias en inversiones alternativas (private equity, hedge funds, commodities) para contextualizar el Fondo C.
4. Eventos macroeconómicos clave del período reciente que hayan impactado los mercados globales.

Para cada punto, incluye datos específicos y cita las fuentes.
```

3. Espera la respuesta del agente Investigador. Revisa que incluya datos concretos y fuentes verificables.
4. Escribe un prompt de seguimiento para obtener contexto regulatorio:

```
Adicionalmente, investiga las tendencias regulatorias recientes en el sector de gestión de inversiones en Estados Unidos y Europa que sean relevantes para comunicar a clientes. Específicamente:

1. Cambios recientes o propuestos en regulación SEC que afecten fondos de inversión.
2. Actualizaciones en normativa MiFID II o SFDR en Europa.
3. Tendencias en requisitos de transparencia y reporting para gestores de activos.

Presenta la información de forma que pueda integrarse directamente en una comunicación al cliente.
```

5. Copia las respuestas del Investigador. En SharePoint, abre el archivo `notas_verificacion_analista.docx` que creaste en el Paso 2 (o crea un nuevo documento llamado `contexto_mercado_investigador.docx` en `/Lab-02-00-03/`) y añade una nueva sección titulada **Contexto de mercado y regulatorio** con la información obtenida.

**Resultado esperado:** El agente Investigador proporciona datos de mercado actualizados con fuentes, incluyendo rendimientos de índices de referencia, tendencias de tasas de interés, contexto de inversiones alternativas y actualizaciones regulatorias relevantes.

**Verificación:**
- [ ] Se obtuvieron datos de al menos 3 índices de referencia relevantes para contextualizar los fondos
- [ ] Se identificaron al menos 2 eventos macroeconómicos clave del período reciente
- [ ] Se recopiló información regulatoria relevante para la comunicación al cliente
- [ ] La información está documentada en SharePoint en la carpeta `/Lab-02-00-03/`

> **⏱️ Tiempo estimado:** 6 minutos

---

### Paso 4: Generar variantes por perfil de cliente con el Agente Entrenador de Ideas

**Objetivo:** Utilizar el agente Entrenador de ideas para crear tres variantes del mensaje principal de la comunicación, cada una adaptada a un perfil de cliente específico: institucional, retail y family office.

**Instrucciones:**

1. En Copilot Chat, cambia al agente **Entrenador de ideas**.
2. Carga el archivo `borrador_comunicacion_portafolio.docx` en el chat.
3. Escribe el siguiente prompt:

```
Tengo un borrador de comunicación de resultados de portafolio adjunto. Necesito adaptar el mensaje principal (resumen ejecutivo y conclusiones) para tres perfiles de cliente diferentes. Para cada perfil, genera una variante del mensaje que mantenga los mismos datos pero adapte:
- El tono y nivel de tecnicismo
- El enfoque de los puntos destacados
- Las recomendaciones y llamados a la acción

Los tres perfiles son:

**Perfil 1 - Cliente Institucional (fondo de pensiones, aseguradora):**
- Tono formal y técnico
- Énfasis en métricas de riesgo-retorno, cumplimiento regulatorio y benchmark
- Foco en gobernanza y proceso de inversión
- Incluir referencias a marcos regulatorios

**Perfil 2 - Cliente Retail (inversionista individual de patrimonio medio):**
- Tono accesible y educativo, evitando jerga excesiva
- Énfasis en rendimiento en términos simples y protección del capital
- Foco en cómo le afecta personalmente y próximos pasos claros
- Usar analogías cuando sea apropiado

**Perfil 3 - Cliente Family Office:**
- Tono sofisticado pero personalizado
- Énfasis en diversificación, preservación patrimonial intergeneracional y oportunidades
- Foco en visión de largo plazo y alineación con objetivos familiares
- Incluir consideraciones de planificación patrimonial

Para cada variante, genera: (a) un párrafo de apertura, (b) los 3 puntos clave adaptados al perfil, y (c) un cierre con llamado a la acción.
```

4. Revisa las tres variantes generadas. Evalúa si el tono y enfoque son apropiados para cada perfil.
5. Si alguna variante necesita ajuste, escribe un prompt de refinamiento. Por ejemplo:

```
La variante para el cliente retail todavía usa términos como "ratio de Sharpe" y "drawdown máximo". Reformúlala usando lenguaje más accesible, explicando estos conceptos en términos que un inversionista no especializado pueda entender fácilmente.
```

6. Una vez satisfecho con las tres variantes, escribe un prompt adicional:

```
Ahora genera una tabla comparativa que muestre, para cada perfil de cliente, los siguientes elementos lado a lado:
- Tono recomendado
- Métricas a destacar
- Métricas a omitir o simplificar
- Tipo de visualizaciones recomendadas para acompañar la comunicación
- Frecuencia de comunicación sugerida
```

7. Copia todas las variantes y la tabla comparativa. Crea un nuevo documento en Word Online en `/Lab-02-00-03/` llamado `variantes_por_perfil.docx` y pega el contenido organizado por perfil.

**Resultado esperado:** Tres variantes claramente diferenciadas del mensaje de comunicación, cada una con tono, enfoque y nivel de detalle apropiados para su perfil de cliente. Una tabla comparativa que resume las diferencias de enfoque comunicacional.

**Verificación:**
- [ ] Las tres variantes son claramente distinguibles en tono y enfoque
- [ ] La variante institucional incluye terminología técnica y referencias regulatorias
- [ ] La variante retail usa lenguaje accesible sin jerga financiera compleja
- [ ] La variante family office equilibra sofisticación con personalización
- [ ] El archivo `variantes_por_perfil.docx` está guardado en `/Lab-02-00-03/`

> **⏱️ Tiempo estimado:** 6 minutos

---

### Paso 5: Refinar y profesionalizar el texto con el Agente Asesor de Escritura

**Objetivo:** Utilizar el agente Asesor de escritura para transformar el borrador original en una comunicación profesional y pulida, incorporando las correcciones del Analista, el contexto del Investigador y seleccionando la mejor estructura de las variantes generadas.

**Instrucciones:**

1. En Copilot Chat, cambia al agente **Asesor de escritura**.
2. Carga los siguientes archivos en el chat:
   - `borrador_comunicacion_portafolio.docx`
   - `notas_verificacion_analista.docx` (o el documento donde guardaste los hallazgos del Paso 2)
3. Escribe el siguiente prompt:

```
Actúa como un editor senior de comunicaciones financieras. Tengo un borrador de comunicación de resultados de portafolio que necesita una transformación profesional. Adjunto el borrador original y un documento con las correcciones de datos identificadas.

Reescribe la comunicación completa aplicando las siguientes directrices:

**Estructura:**
1. Encabezado profesional con nombre de la firma, fecha y tipo de documento
2. Saludo personalizable [Nombre del cliente]
3. Resumen ejecutivo (máximo 150 palabras) con los 3 hallazgos más relevantes
4. Contexto de mercado (2-3 párrafos integrando tendencias macro relevantes)
5. Análisis por fondo (Fondo A, B y C) con datos corregidos según las notas de verificación
6. Consideraciones regulatorias relevantes
7. Perspectivas y recomendaciones
8. Cierre profesional con próximos pasos y datos de contacto

**Tono y estilo:**
- Profesional pero accesible (orientado a un cliente institucional como base)
- Frases concisas, párrafos de máximo 4 líneas
- Datos presentados con contexto (no solo cifras aisladas)
- Uso de conectores que guíen la narrativa
- Evitar lenguaje excesivamente optimista o pesimista; mantener objetividad

**Correcciones requeridas:**
- Incorporar todas las correcciones de datos identificadas en las notas de verificación
- Asegurar que cada cifra mencionada sea consistente con las fuentes de datos originales
```

4. Revisa la comunicación reescrita. Verifica que:
   - Las correcciones de datos del Paso 2 se hayan aplicado.
   - La estructura siga las directrices solicitadas.
   - El tono sea apropiado.
5. Ahora solicita la integración del contexto de mercado. Escribe:

```
Excelente base. Ahora integra el siguiente contexto de mercado en la sección correspondiente de la comunicación:

[Pega aquí los datos de mercado más relevantes obtenidos del agente Investigador en el Paso 3, incluyendo rendimientos de índices de referencia y eventos macroeconómicos clave]

Asegúrate de que el contexto de mercado se conecte naturalmente con el desempeño de cada fondo. Por ejemplo, si el MSCI World tuvo un rendimiento de X%, explica cómo se compara el Fondo A de Renta Variable Global contra ese benchmark.
```

6. Revisa la versión actualizada. Escribe un último prompt de pulido:

```
Revisa la comunicación completa y:
1. Verifica que no haya repeticiones innecesarias entre secciones.
2. Asegura transiciones fluidas entre cada sección.
3. Confirma que el resumen ejecutivo refleja fielmente el contenido detallado.
4. Sugiere 2-3 mejoras adicionales de estilo o contenido que elevarían la calidad del documento.
5. Añade una nota al pie indicando: "Este documento fue preparado con asistencia de herramientas de inteligencia artificial y revisado por [nombre del asesor]. Los datos presentados corresponden al período [período] y las proyecciones no constituyen garantía de resultados futuros."
```

7. Copia la versión final de la comunicación.

**Resultado esperado:** Una comunicación completa, profesionalmente estructurada, con datos corregidos, contexto de mercado integrado, tono apropiado y todas las secciones requeridas. El agente Asesor de escritura habrá sugerido mejoras adicionales de estilo.

**Verificación:**
- [ ] La comunicación tiene las 8 secciones solicitadas en la estructura
- [ ] Los datos financieros son consistentes con `tabla_metricas_fondos.xlsx`
- [ ] El contexto de mercado se integra naturalmente con el análisis de cada fondo
- [ ] El tono es profesional, objetivo y accesible
- [ ] Se incluye la nota al pie sobre uso de IA y disclaimer de proyecciones

> **⏱️ Tiempo estimado:** 6 minutos

---

### Paso 6: Coordinar el entregable final con el Agente Asistente de Solicitudes

**Objetivo:** Utilizar el agente Asistente de solicitudes para crear una lista de verificación del entregable final, confirmar la completitud del documento y generar el archivo definitivo en SharePoint.

**Instrucciones:**

1. En Copilot Chat, cambia al agente **Asistente de solicitudes**.
2. Escribe el siguiente prompt:

```
Estoy finalizando una comunicación de resultados de portafolio para clientes. Necesito tu ayuda para coordinar la entrega final. Genera una checklist de calidad que verifique los siguientes aspectos del documento:

1. **Completitud de contenido:**
   - ¿Incluye resumen ejecutivo?
   - ¿Incluye contexto de mercado?
   - ¿Incluye análisis de los tres fondos (A, B, C)?
   - ¿Incluye consideraciones regulatorias?
   - ¿Incluye perspectivas y recomendaciones?
   - ¿Incluye cierre con próximos pasos?

2. **Consistencia de datos:**
   - ¿Todas las cifras de rendimiento están verificadas?
   - ¿Los benchmarks de referencia son correctos?
   - ¿Las métricas de riesgo son consistentes con las fuentes?

3. **Calidad de comunicación:**
   - ¿El tono es apropiado para el público objetivo?
   - ¿Las frases son claras y concisas?
   - ¿Hay transiciones fluidas entre secciones?
   - ¿Se evita jerga innecesaria?

4. **Cumplimiento:**
   - ¿Incluye disclaimers apropiados?
   - ¿Incluye nota sobre uso de IA?
   - ¿Evita promesas de rendimiento futuro?

5. **Formato:**
   - ¿Tiene encabezado profesional?
   - ¿Los párrafos son de longitud adecuada?
   - ¿Los datos numéricos están formateados consistentemente?

Presenta la checklist en formato de tabla con columnas: Ítem, Criterio, Estado (para marcar ✅ o ❌).
```

3. Usa la checklist generada para revisar mentalmente la comunicación que creaste en el Paso 5. Identifica cualquier elemento faltante.
4. Si identificas elementos faltantes, regresa al agente correspondiente para completarlos:
   - Datos faltantes → Agente Analista
   - Contexto adicional → Agente Investigador
   - Ajustes de tono → Agente Asesor de escritura
5. Una vez que todos los elementos de la checklist estén satisfechos, abre **Word Online** en SharePoint navegando a `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-03/`.
6. Haz clic en **+ Nuevo** → **Documento de Word** y nómbralo `comunicacion_portafolio_final.docx`.
7. Pega el contenido completo de la comunicación refinada del Paso 5 en este nuevo documento.
8. Aplica formato profesional básico en Word Online:
   - **Título** del documento: usa el estilo **Título** de Word.
   - **Encabezados de sección**: usa el estilo **Título 1** para secciones principales y **Título 2** para subsecciones de cada fondo.
   - **Datos numéricos**: verifica que estén en formato consistente (por ejemplo, porcentajes con un decimal: 12.5%).
   - **Tabla de métricas**: si incluyes una tabla resumen, asegúrate de que tenga bordes y encabezados en negrita.
9. Guarda el documento (se guarda automáticamente en SharePoint).
10. Regresa al agente Asistente de solicitudes y escribe:

```
El documento final "comunicacion_portafolio_final.docx" ha sido completado y guardado. Genera un breve resumen ejecutivo de las acciones realizadas en este flujo de trabajo, incluyendo:
1. Agentes utilizados y su contribución específica
2. Correcciones de datos aplicadas
3. Enriquecimientos de contexto incorporados
4. Variantes generadas por perfil de cliente
5. Archivos de salida producidos y su ubicación

Este resumen servirá como registro del proceso para el equipo.
```

11. Copia el resumen y agrégalo como última sección del archivo `comunicacion_portafolio_final.docx` bajo el título **Anexo: Registro del proceso de elaboración** (o guárdalo como documento separado si lo prefieres).

**Resultado esperado:** Una checklist de calidad completa, un documento final formateado profesionalmente en SharePoint y un resumen ejecutivo del proceso que documenta la contribución de cada agente.

**Verificación:**
- [ ] La checklist de calidad tiene todos los ítems marcados como completados
- [ ] El archivo `comunicacion_portafolio_final.docx` existe en `/Lab-02-00-03/` en SharePoint
- [ ] El documento tiene formato profesional con estilos de Word aplicados
- [ ] Se generó un resumen del proceso que documenta el uso de cada agente

> **⏱️ Tiempo estimado:** 3 minutos

---

## Validación y Pruebas

Una vez completados todos los pasos, realiza las siguientes verificaciones finales para confirmar que el laboratorio se ha completado exitosamente:

### Verificación de Archivos en SharePoint

Navega a `/sites/CursoAgentes/Documentos compartidos/Lab-02-00-03/` y confirma la existencia de los siguientes archivos:

| Archivo | Propósito | Estado |
|---|---|---|
| `borrador_comunicacion_portafolio.docx` | Archivo original de entrada (pre-existente) | ☐ Presente |
| `notas_verificacion_analista.docx` | Hallazgos de consistencia del Agente Analista | ☐ Creado en Paso 2 |
| `contexto_mercado_investigador.docx` | Contexto de mercado del Agente Investigador (si se creó separado) | ☐ Creado en Paso 3 |
| `variantes_por_perfil.docx` | Variantes de comunicación por perfil de cliente | ☐ Creado en Paso 4 |
| `comunicacion_portafolio_final.docx` | **Entregable principal del laboratorio** | ☐ Creado en Paso 6 |

### Verificación de Calidad del Entregable Final

Abre `comunicacion_portafolio_final.docx` y verifica:

1. **Estructura completa:** El documento contiene las 8 secciones definidas en el Paso 5 (encabezado, saludo, resumen ejecutivo, contexto de mercado, análisis por fondo, consideraciones regulatorias, perspectivas, cierre).
2. **Datos verificados:** Compara al menos 3 cifras clave del documento final con `tabla_metricas_fondos.xlsx` — deben coincidir exactamente.
3. **Contexto integrado:** La sección de contexto de mercado incluye al menos 2 referencias a índices de mercado o eventos macroeconómicos.
4. **Disclaimers presentes:** El documento incluye la nota sobre uso de IA y el disclaimer de proyecciones.
5. **Formato profesional:** Los estilos de Word están aplicados correctamente (títulos, encabezados, formato numérico consistente).

### Verificación de Competencias con Agentes

Confirma que durante el laboratorio utilizaste los cinco agentes preconstruidos:

- [ ] **Analista**: Verificación de consistencia de datos (Paso 2)
- [ ] **Investigador**: Enriquecimiento con contexto de mercado (Paso 3)
- [ ] **Entrenador de ideas**: Generación de variantes por perfil (Paso 4)
- [ ] **Asesor de escritura**: Refinamiento profesional del texto (Paso 5)
- [ ] **Asistente de solicitudes**: Coordinación y checklist final (Paso 6)

---

## Solución de Problemas

### Problema 1: El agente Analista no detecta inconsistencias o responde de forma genérica

**Síntomas:** Al cargar el borrador y la tabla de métricas, el agente Analista responde con comentarios vagos como "El documento parece consistente" sin proporcionar una tabla comparativa detallada, o no identifica datos específicos para comparar.

**Causa:** El agente Analista necesita instrucciones explícitas sobre qué datos comparar. Cuando los archivos contienen múltiples hojas, tablas o secciones, el agente puede no identificar automáticamente los puntos de comparación relevantes. Además, si los archivos son muy extensos, el agente puede resumir en lugar de analizar dato por dato.

**Solución:**

1. Reformula el prompt siendo más específico sobre los datos a comparar. Por ejemplo:

```
En el archivo "borrador_comunicacion_portafolio.docx", localiza todas las cifras numéricas mencionadas (rendimientos porcentuales, ratios, valores de drawdown). Luego, busca esas mismas métricas en el archivo "tabla_metricas_fondos.xlsx". Compara cifra por cifra y presenta una tabla con las diferencias encontradas. Si una cifra del borrador no tiene equivalente exacto en la tabla, márcala como "Sin respaldo en fuente".
```

2. Si el archivo Excel tiene múltiples hojas, especifica cuál usar:

```
Usa la hoja principal (primera hoja) del archivo Excel que contiene las métricas consolidadas de los tres fondos.
```

3. Si el problema persiste, intenta cargar los archivos uno por uno: primero la tabla Excel, pide al agente que la describa, y luego carga el borrador para la comparación.

---

### Problema 2: El agente Asesor de escritura genera un texto que pierde datos financieros clave o inventa cifras

**Síntomas:** La comunicación reescrita por el Asesor de escritura omite métricas importantes que estaban en el borrador original, modifica cifras numéricas, o incluye datos que no estaban en ninguno de los archivos fuente (alucinación).

**Causa:** Los agentes de lenguaje pueden priorizar la fluidez narrativa sobre la precisión de datos. Al reescribir un texto extenso con muchas cifras, el agente puede parafrasear valores numéricos de forma imprecisa o, si el contexto es insuficiente, generar datos plausibles pero incorrectos.

**Solución:**

1. Añade una restricción explícita en tu prompt:

```
REGLA CRÍTICA: No modifiques, redondees ni inventes ninguna cifra numérica. Todos los porcentajes, ratios y valores monetarios deben copiarse exactamente como aparecen en los documentos fuente. Si no encuentras un dato específico en los archivos adjuntos, escribe [DATO PENDIENTE DE VERIFICACIÓN] en su lugar.
```

2. Después de recibir la respuesta, realiza una verificación cruzada manual: abre `tabla_metricas_fondos.xlsx` en una pestaña separada y compara las 5-10 cifras más importantes del documento reescrito contra la fuente.

3. Si encuentras cifras incorrectas, señálalas explícitamente al agente:

```
En la sección del Fondo A, escribiste que el rendimiento fue de 14.2%, pero según la tabla de métricas el valor correcto es 13.8%. Corrige esta cifra y revisa si hay otras discrepancias numéricas en todo el documento.
```

4. Como buena práctica, siempre incluye la tabla de métricas como archivo adjunto cuando trabajes con el Asesor de escritura, no solo el borrador de texto. Esto le da al agente una fuente de datos estructurada para referenciar.

---

## Limpieza

Al finalizar el laboratorio, realiza las siguientes acciones de organización:

1. **Archivos en SharePoint (conservar):** No elimines ningún archivo de la carpeta `/Lab-02-00-03/`. Los siguientes archivos deben permanecer para referencia en los laboratorios del Módulo 3:
   - `comunicacion_portafolio_final.docx` (entregable principal)
   - `variantes_por_perfil.docx` (referencia para personalización de agentes)
   - `notas_verificacion_analista.docx` (registro de verificación)
   - `borrador_comunicacion_portafolio.docx` (archivo original — no modificar)

2. **Archivos locales (eliminar):** Elimina la carpeta temporal `Lab-02-00-03-Archivos` de tu equipo local, ya que todos los archivos relevantes están en SharePoint.

3. **Historial de Copilot Chat:** Los historiales de conversación con los agentes se conservan automáticamente en Copilot Chat. No es necesario eliminarlos; pueden servir como referencia del proceso seguido.

4. **Verificación final de permisos:** Confirma que el archivo `comunicacion_portafolio_final.docx` es accesible para el instructor. En SharePoint, haz clic en los tres puntos (⋯) junto al archivo → **Administrar acceso** → verifica que los miembros del sitio tengan acceso de lectura.

---

## Resumen

En este laboratorio completaste el ciclo de uso encadenado de los cinco agentes preconstruidos de Microsoft 365 Copilot para producir una comunicación profesional de resultados de portafolio. El flujo de trabajo que ejecutaste representa un patrón replicable en escenarios reales de gestión de inversiones:

| Agente | Contribución en este laboratorio |
|---|---|
| **Analista** | Verificó la consistencia de datos financieros entre el borrador y las fuentes de referencia, identificando y corrigiendo inconsistencias |
| **Investigador** | Aportó contexto de mercado actualizado (índices, tasas, eventos macro) para enriquecer la narrativa de la comunicación |
| **Entrenador de ideas** | Generó tres variantes del mensaje adaptadas a perfiles de cliente institucional, retail y family office |
| **Asesor de escritura** | Transformó el borrador técnico en una comunicación profesional, estructurada y con tono apropiado |
| **Asistente de solicitudes** | Coordinó la checklist de calidad final y documentó el proceso completo |

### Lecciones Clave

- **El orden de los agentes importa:** Verificar datos antes de escribir evita propagar errores. Investigar contexto antes de redactar enriquece el resultado.
- **La especificidad en los prompts es determinante:** Cuanto más preciso sea el prompt, más útil y accionable será la respuesta del agente. Esto es especialmente crítico con datos numéricos.
- **La verificación humana es insustituible:** Los agentes son herramientas poderosas, pero la validación final de cifras y conclusiones debe ser realizada por el profesional.
- **La adaptación por audiencia multiplica el valor:** Un mismo análisis puede comunicarse de formas muy diferentes según el perfil del destinatario, y el Entrenador de ideas facilita esta personalización.

### Conexión con el Módulo 3

El documento `comunicacion_portafolio_final.docx` y el flujo de trabajo documentado en este laboratorio servirán como caso de referencia en el Módulo 3, donde construirás un **agente personalizado** mediante Copilot Agent Builder que podría automatizar parcialmente este proceso de generación de comunicaciones de portafolio.

### Recursos Adicionales

- [Documentación oficial de agentes preconstruidos de M365 Copilot](https://support.microsoft.com/es-es/copilot-agents)
- [Mejores prácticas de prompt engineering para Microsoft Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/prompt-engineering)
- [Guía de comunicaciones financieras — CFA Institute](https://www.cfainstitute.org/en/ethics-standards)
- [Seguridad y cumplimiento en Microsoft 365 Copilot](https://learn.microsoft.com/es-es/microsoft-365-copilot/microsoft-365-copilot-privacy)
