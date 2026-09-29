# Práctica 1 - Análisis comparativo de fondos multiactivo para una revisión interna

CIBEST CAPITAL realizará una revisión interna de seis fondos multiactivo ficticios. En esta práctica usarás el agente **Analista (Analyst)** de Microsoft Copilot para explorar los datos, comparar características, detectar comportamientos atípicos, generar visualizaciones y documentar cuestiones que requieren profundización. La actividad no busca seleccionar un fondo ganador ni emitir una recomendación de inversión.

## Metadatos

| Campo | Detalle |
|---|---|
| Duración | 55 min |
| Complejidad | Intermedia |
| Nivel de Bloom | Analizar |
| Tipo de actividad | Análisis guiado de datos con IA |
| Aplicaciones | Microsoft Copilot - agente Analista |
| Modalidad | Individual |
| Insumos previos | `recursos/fondos_multiactivo_24m.xlsx` |
| Resultado | Análisis comparativo, visualizaciones, hallazgos y cuestiones para profundización |

## Distribución de tiempo

| Fase | Actividad | Tiempo |
|---|---|---:|
| 1 | Cargar y comprobar el conjunto de datos | 8 min |
| 2 | Comparar los seis fondos | 15 min |
| 3 | Visualizar diferencias y detectar comportamientos atípicos | 12 min |
| 4 | Explicar cálculos, criterios y relaciones | 10 min |
| 5 | Sintetizar hallazgos y validar el resultado | 10 min |
|  | **TOTAL** | **55 min** |

## Descripción general

Trabajarás con 24 meses de observaciones ficticias para los fondos A-F. El archivo incluye rendimiento mensual, volatilidad, composición por clase de activo, exposición geográfica, moneda base, comisión anual y categoría de riesgo. El conjunto contiene diferencias intencionales y observaciones atípicas que deben descubrirse durante el análisis.

El resultado debe permitir comprender las diferencias observables entre los fondos sin convertir el análisis en una recomendación de inversión.

## Objetivos de aprendizaje

Al finalizar podrás:

- utilizar Analista para explorar un conjunto de datos multivariable;
- comparar rendimiento, volatilidad, composición, exposición geográfica, comisión y riesgo;
- identificar valores atípicos y relaciones entre variables;
- solicitar visualizaciones y explicaciones de los cálculos utilizados;
- sintetizar fortalezas, diferencias, riesgos observables y preguntas para profundización sin seleccionar un fondo ganador.

## Escenario de la práctica

La práctica se desarrolla en el contexto de **CIBEST CAPITAL**. Un equipo de inversiones realiza una revisión interna de seis fondos multiactivo ficticios y necesita comprender sus diferencias antes de continuar con una evaluación especializada.

## Prerrequisitos

- Experiencia funcional básica con Microsoft 365.
- Acceso al agente **Analista** en Microsoft Copilot según el licenciamiento y la configuración del entorno del curso.
- Permiso para cargar el archivo de laboratorio en la conversación con Analista.

## Preparación del entorno

Antes de iniciar el cronómetro de la práctica:

1. Descarga o localiza `recursos/fondos_multiactivo_24m.xlsx`.
2. Abre Microsoft Copilot con la cuenta del curso.
3. En **Agentes**, abre **Analista**. Si no aparece en la navegación, busca la opción equivalente para ver todos los agentes disponibles.
4. No modifiques el archivo de datos antes de iniciar el análisis.

> Los nombres y la ubicación de los controles pueden variar con las actualizaciones de Microsoft Copilot. Utiliza la opción equivalente disponible en tu interfaz.

## Desarrollo de la práctica

### Fase 1 - Cargar y comprobar el conjunto de datos

**Tiempo:** 8 min  
**Aplicación:** Analista  
**Objetivo:** confirmar que Analista reconoce correctamente el archivo y las variables antes de realizar comparaciones.

### Paso 1. Adjunta el archivo

Adjunta `fondos_multiactivo_24m.xlsx` a una conversación nueva con Analista.

### Paso 2. Solicita una exploración inicial

> **PROMPT 1 - COMPROBACIÓN DEL CONJUNTO DE DATOS**
>
> Analiza el archivo `fondos_multiactivo_24m.xlsx` como un conjunto de datos ficticio para una revisión interna de seis fondos multiactivo denominados Fondo A-F.  
> Antes de comparar resultados, comprueba la estructura y la calidad del archivo. Indica:  
> 1. cuántos fondos identificas;  
> 2. cuántos meses de observaciones existen por fondo;  
> 3. qué variables están disponibles;  
> 4. si detectas valores faltantes, duplicados o problemas de formato que puedan afectar el análisis.  
> No emitas recomendaciones de inversión ni selecciones un fondo ganador. Usa únicamente los datos del archivo.

Revisa la respuesta. Debe reconocer seis fondos y al menos 24 meses de observaciones por fondo. Si Analista interpreta mal una columna, indícale el nombre exacto mostrado en la hoja **Diccionario** del libro y vuelve a solicitar la comprobación.

**Criterio de finalización:** Analista reconoce los seis fondos, el periodo de observación y las variables necesarias para continuar.

### Fase 2 - Comparar los seis fondos

**Tiempo:** 15 min  
**Aplicación:** Analista  
**Objetivo:** obtener una comparación estructurada de las principales dimensiones del temario.

### Paso 1. Ejecuta la comparación principal

> **PROMPT 2 - COMPARACIÓN MULTIVARIABLE**
>
> Compara los seis fondos del archivo usando estas dimensiones: rendimiento, volatilidad, distribución por clases de activo, exposición geográfica, moneda base, comisión anual y categoría de riesgo.  
> Para rendimiento, utiliza los 24 meses disponibles y explica qué medida calculas para comparar el periodo completo. Para volatilidad, indica si utilizas la columna proporcionada o una medida calculada a partir de los rendimientos.  
> Presenta primero una tabla comparativa por fondo y después resume las diferencias más relevantes.  
> No clasifiques los fondos de mejor a peor y no hagas recomendaciones de inversión.

### Paso 2. Revisa la lógica del análisis

Comprueba que la tabla incluya los fondos A-F y las dimensiones solicitadas. Si aparece una medida calculada que no comprendes, anótala para la Fase 4.

**Criterio de finalización:** existe una tabla o estructura equivalente que permite comparar los seis fondos en todas las dimensiones solicitadas.

### Fase 3 - Visualizar diferencias y detectar comportamientos atípicos

**Tiempo:** 12 min  
**Aplicación:** Analista  
**Objetivo:** representar visualmente las diferencias y localizar patrones o valores atípicos.

### Paso 1. Solicita visualizaciones

> **PROMPT 3 - VISUALIZACIONES Y VALORES ATÍPICOS**
>
> Genera visualizaciones que ayuden a comprender este conjunto de datos. Incluye, como mínimo:  
> - evolución o rendimiento acumulado de los seis fondos durante el periodo;  
> - relación entre rendimiento y volatilidad por fondo;  
> - comparación de la composición por clases de activo.  
> Después identifica observaciones atípicas o cambios que destaquen frente al comportamiento habitual de cada fondo. Explica qué criterio usaste para considerarlos atípicos.  
> Describe los hallazgos sin atribuir causas que no estén respaldadas por el archivo y sin recomendar un fondo.

Si la interfaz no muestra un gráfico en algún momento, solicita que represente la misma comparación mediante una tabla o visualización equivalente y conserva los demás gráficos generados.

### Paso 2. Comprueba los hallazgos

Localiza en el archivo las filas relacionadas con los valores atípicos detectados. No aceptes como hecho una explicación causal que no pueda rastrearse a los datos.

**Criterio de finalización:** existen visualizaciones del rendimiento, la relación rendimiento-volatilidad y la composición, y se han señalado observaciones atípicas con un criterio explícito.

### Fase 4 - Explicar cálculos, criterios y relaciones

**Tiempo:** 10 min  
**Aplicación:** Analista  
**Objetivo:** comprender cómo se obtuvieron los principales resultados y evitar aceptar cálculos de IA sin revisión.

### Paso 1. Pide trazabilidad de los cálculos

> **PROMPT 4 - EXPLICACIÓN DE CÁLCULOS Y RELACIONES**
>
> Explica de forma verificable los cálculos y criterios que utilizaste en la comparación. Incluye:  
> - fórmula o procedimiento para el rendimiento del periodo;  
> - tratamiento de la volatilidad;  
> - cómo comparaste comisiones y categorías de riesgo;  
> - relaciones que observaste entre composición, exposición geográfica, rendimiento y volatilidad.  
> Distingue claramente entre datos observados, cálculos derivados e interpretaciones. Si una relación no implica causalidad, indícalo.

### Paso 2. Contrasta al menos un cálculo

Selecciona uno de los fondos y verifica manualmente que los datos de composición sumen 100 %. Comprueba también que las exposiciones geográficas sumen 100 % para ese fondo.

**Criterio de finalización:** puedes explicar al menos un cálculo utilizado por Analista y has verificado manualmente la consistencia de una composición y una exposición geográfica.

### Fase 5 - Sintetizar hallazgos y validar el resultado

**Tiempo:** 10 min  
**Aplicación:** Analista  
**Objetivo:** producir una síntesis final útil para una revisión interna especializada posterior.

### Paso 1. Solicita la síntesis final

> **PROMPT 5 - SÍNTESIS PARA REVISIÓN INTERNA**
>
> A partir exclusivamente del archivo y del análisis realizado en esta conversación, prepara una síntesis para una revisión interna de CIBEST CAPITAL. Incluye:  
> 1. diferencias relevantes entre los seis fondos;  
> 2. fortalezas observables en los datos, sin convertirlas en recomendaciones;  
> 3. riesgos o señales que merecen atención;  
> 4. observaciones atípicas identificadas;  
> 5. al menos cinco preguntas o aspectos que deberían investigarse posteriormente por especialistas.  
> No selecciones un fondo ganador, no generes una recomendación de inversión y no inventes causas o información externa.

### Paso 2. Revisa la respuesta

Confirma que la síntesis se mantiene dentro de los datos. Elimina o vuelve a consultar cualquier afirmación que introduzca hechos externos, causas no demostradas o una recomendación de inversión.

**Criterio de finalización:** dispones de una síntesis comparativa con hallazgos y preguntas de profundización, sin selección de ganador ni recomendación de inversión.

## Validación y pruebas finales

| # | Criterio | Estado |
|---|---|---|
| 1 | Se analizaron exactamente seis fondos, A-F. | ☐ |
| 2 | Se utilizaron al menos 24 meses de observaciones por fondo. | ☐ |
| 3 | La comparación cubre rendimiento, volatilidad, composición, geografía, moneda, comisión y riesgo. | ☐ |
| 4 | Existen visualizaciones del rendimiento, rendimiento-volatilidad y composición. | ☐ |
| 5 | Se identificaron observaciones atípicas y se explicó el criterio usado. | ☐ |
| 6 | Se explicó cómo se realizaron los principales cálculos. | ☐ |
| 7 | La síntesis contiene cuestiones para profundización. | ☐ |
| 8 | No se seleccionó un fondo ganador ni se emitió una recomendación de inversión. | ☐ |

## Solución de problemas

| Situación | Qué hacer |
|---|---|
| Analista no reconoce el archivo | Vuelve a adjuntar `fondos_multiactivo_24m.xlsx` en una conversación nueva y confirma que la carga finalizó antes de enviar el prompt. |
| Analista interpreta mal una columna | Usa la hoja **Diccionario** y menciona explícitamente el nombre exacto de la columna en el siguiente mensaje. |
| No se genera una visualización | Solicita de nuevo la visualización especificando los ejes o pide una tabla equivalente para continuar; conserva las demás visualizaciones disponibles. |
| Aparece una recomendación de inversión | Indica a Analista que elimine la recomendación y reformule el hallazgo como diferencia observable, riesgo o cuestión para investigar. |
| La respuesta atribuye una causa no presente en el archivo | Pide separar datos, cálculos e hipótesis, y elimina cualquier causalidad no respaldada. |

## Limpieza y conservación

- Conserva `fondos_multiactivo_24m.xlsx` como insumo del laboratorio.
- Conserva la conversación o el reporte final únicamente si la política del entorno de capacitación lo permite.
- No presentes los datos como información real de fondos o clientes; son completamente ficticios.
- No utilices la salida de la práctica como recomendación de inversión.

## Resumen de la práctica

Cargaste un conjunto de datos ficticio, verificaste su estructura, comparaste seis fondos, generaste visualizaciones, detectaste observaciones atípicas, pediste trazabilidad de los cálculos y terminaste con una síntesis orientada a una revisión especializada posterior.

## Referencia oficial de apoyo

- Microsoft Support - Get started with Analyst in Microsoft Copilot: https://support.microsoft.com/en-us/microsoft-365-copilot/get-started-with-analyst-in-microsoft-365-copilot
