# ICCafe_anteproyecto

**Proyecto desarrollado por:**
1. Lizeth Garcia
2. Maria Alejandra Herrera
3. Carlos Silva
4. Leonardo Guzman

**data**
*data en drive compartido -> descargar carpeta completa y dejarla en la raiz del proyecto, gitignore ya tiene en cuenta esta carpeta*
coordenadas: documentación de la extracción realizada, datos en formato geojson y csv. Generación de csv con variables a usar. **Hay un archivo interesante para tenerlo en cuenta en la elaboración del documento final.**
nasa_power: Esta relacionado por id_coordenada cada archivo generado de nasa power

**Archivos de consolidación**
fuentes.txt está la relación de las fuentes consultadas de los datos extraídos
variables_nasa.txt son las variables que se tomaron en cuenta inicialmente para el modelo PCA

**notebooks**
extraccion_coordenadas -> extrae las coordenadas de datos abiertos del gobierno y los transorma para generar coordenadas
extraccion_variables_climaticas_nasa -> extrae información del API de nasa
pendiente extraer datos de indice de vegetación de NASA





## FLUJO COMPLETO DEL PROYECTO ICCAFE

---

### ETAPA 1: EXTRACCIÓN DE DATOS

**Definir las unidades espaciales.**  
Se procesan las geometrías de la zonificación del cultivo de café, se reproyectan a WGS84 y se disuelven por municipio. A partir de estas geometrías se calculan los centroides (latitud y longitud). Con esto se construye el archivo `zonificacion_coordenadas_cafe.csv`.

**Extraer datos climáticos desde NASA POWER utilizando los centroides.**  
Se realizan solicitudes por municipio y por año para el período 2014-06-06 a 2025-07-06.  
Para información de las variables extraídas, consultar `variables_nasa.txt`.
Los resultados se guardan en archivos CSV individuales en la carpeta `nasa_power`. 

**Reunir datos productivos y económicos.**  
Incluye producción anual por departamento y el valor de venta del café en los años correspondientes `Precios-area-y-produccion-de-cafe-2025`.

**Extraer datos de vegetación (NDVI o EVI).**  PENDIENTE

---

## ETAPA 2: REVISIÓN Y LIMPIEZA DE DATOS

**Validación temporal.**  
Ajuste de timestamps, revisión de duplicados y aseguramiento de continuidad temporal.

**Comprobación de rangos físicos.**  
Temperatura, radiación, humedad, precipitación, viento y humedad del suelo.

**Gestión de datos faltantes.**  
Marcado explícito, interpolación o imputación según corresponda.

**Homogeneización de unidades.**  
Asegurar compatibilidad entre variables y municipios.

**Consolidación en un dataset general.**  
Exportado dataset final.

---

## ETAPA 3: TRANSFORMACIÓN Y CÁLCULO DE VARIABLES

**Cálculo de variables derivadas relevantes para café.**  
- VPD (déficit de presión de vapor)  
- Días secos  
- Días de lluvia extrema  
- Días con estrés térmico (> 30°C)  
- Radiación extrema  
- Humedad crítica   

**Agregación mensual.**  
Medias, sumas, conteos y percentiles de las variables.

**Agregación anual.**  
Promedios, desviaciones estándar y extremos para cada municipio.  

---

## ETAPA 4: PCA (ÍNDICE CLIMÁTICO ICCAFE)

**Preparación de datos.**  
Estandarización con z-score y selección de variables representativas.

**Ejecución del PCA.**  
Se calcula PC1, que captura la mayor parte de la variabilidad climática.

**Normalización del índice.**  
PC1 se normaliza entre 0 y 1, generando el índice **ICCafé**.

---

## ETAPA 5: MODELO CLASIFICATORIO DE RIESGO

**Construcción de etiquetas de riesgo.**  
Categorías: riesgo bajo, medio y alto.

**Entrenamiento del modelo.**  
Modelos supervisados de supervición.

**Validación del modelo.**  
Matriz de confusión y análisis de coherencia con eventos ENSO (Niño/Niña).

---

## ETAPA 6: MODELO DE PRIMA

**Definir estructura de la función de prima.**  
Modelos posibles: lineal, piecewise, potencial o mixto.

**Calibración de parámetros.**  
Mediante ajuste experto (si no hay históricos de siniestros) o ajuste estadístico (si existen datos reales).

**Validación técnica.**  
Análisis de sensibilidad, pruebas de estrés y validación agronómica.

---

## ETAPA 7: RESULTADOS Y COMUNICACIÓN

**Dataset final.**  
Incluye variables climáticas agregadas, ICCafé, clasificación de riesgo, prima estimada y metadatos relevantes.

**Mapas y visualizaciones.**  
Mapas de ICCafé, mapas de riesgo, curvas ICCafé–prima, series históricas.

**Reporte técnico.**  
Documentación completa de supuestos, metodología, validación y recomendaciones para implementación.
