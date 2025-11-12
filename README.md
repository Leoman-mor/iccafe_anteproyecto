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
Definición espacial (filtrar Quindío 63 y Cundinamarca 25; validar geometrías por municipio)
Extracción de datos climáticos (NASA POWER hourly por coordenada, 2014-06-06 → 2025-07-06, por años, JSON → CSV)
Limpieza de datos (timestamps UTC, imputación/marcado de faltantes, validación de unidades, reintentos de API)
Calculo de variables (cálculo VPD, días secos, meses extremos, humedad de suelo, etc.)
Agregación mensual (sumas, medias, desviación, percentiles p10/p50/p90 por variable)
Agregación anual por id_coordenada (estadísticos climáticos anuales derivados de los mensuales)
Construcción del proxy de impacto climático (variable continua 0–1 con pesos expertos)
PCA con variables climáticas (estandarizar → PCA → PC1 = ICCafé normalizado 0–1)
Fusión del dataset anual (ICCafé + proxy de impacto + variables zonales como altitud y área ha)
Definir familia de función de prima (lineal, piecewise o potencial) con parámetros interpretables
Calibración de parámetros de prima (por experto si no hay siniestros, por regresión si hay datos históricos)
Validación agronómica y de negocio (ENSO, altitud, correlaciones esperadas, stress tests)
Generación del dataset final para primas (ICC, impacto, prima estimada, banda min–max, ahorros)
Entrega de resultados (tablas por coordenada/año, mapas, curvas de prima, reporte de supuestos)