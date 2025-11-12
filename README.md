# iccafe_anteproyecto

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

**Flujo**
Definición espacial (filtrar Quindío y Cundinamarca; validar polígonos / altitud)
Extracción de datos (NASA POWER hourly por coordenada, 2005-06-06 → 2025-06-06)
Limpieza de datos (timestamps UTC, missing, unidades, reintentos)
Variabbles calculadas (calcular VPD, días secos, acumulados mensuales, etc.)
Agregación mensual (medias, sumas, sd, percentiles por variable)
Agregación anual por id_coordenada (estadísticos anuales a partir de mensuales)
Análisis descriptivo (correlación, VIF, distribuciones, outliers)
PCA con variables seleccionadas (estandarizar → PCA → validar cargas y varianza)
Generación de ICCafé anual (normalizar PC1 → 0–1; validar sentido agronómico)
Validación agronómica del ICC (comparar con altitud, eventos Niño/La Niña, patrones esperados)
Construcción del dataset para primas (ICC, variabilidad, covariables zonales)
Modelo de primas (fórmula paramétrica / regresión / ML según disponibilidad de siniestros)
Evaluación y calibración (backtest, sensibilidad, escenarios)
Entrega: tablas por id_coordenada (series mensuales), ICC anual y primas estimadas