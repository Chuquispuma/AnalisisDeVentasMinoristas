# Análisis de Ventas Minoristas con Power BI

Este repositorio contiene un análisis de ventas minoristas realizado con Power BI.  El informe completo se encuentra en formato PDF:

[Informe_Ventas.pdf](Informe_Ventas.pdf)


## Descripción del Proyecto

Este proyecto analiza datos de ventas semanales de una cadena de tiendas minoristas. El objetivo es comprender las tendencias de ventas, el impacto de las promociones y otros factores que influyen en el rendimiento.  Las fuentes de datos utilizadas son `train.csv`, `features.csv` y `stores.csv`, que contienen información sobre las ventas, las características de las tiendas y eventos promocionales.  Además, se incorpora una dimensión temporal mediante el archivo `DIM_FECHA.csv`.

## Visualizaciones y Análisis Clave

El informe incluye las siguientes visualizaciones:

* **Tendencias de Ventas (Gráfico de líneas):** Muestra la evolución de las ventas semanales a lo largo del tiempo, permitiendo identificar patrones estacionales y tendencias generales.  Se ha incorporado una media móvil de 7 días para suavizar las fluctuaciones y visualizar la tendencia subyacente.

* **Ventas por Tipo de Tienda (Gráfico circular):**  Desglosa las ventas totales por tipo de tienda (A, B, C), mostrando la contribución de cada tipo al total.

* **Impacto de Días Festivos (Gráficos de columnas agrupadas):**  Compara las ventas en días festivos y no festivos, tanto para valores positivos como negativos, para analizar el impacto de estos eventos en el rendimiento.

* **Ventas por Departamento (Treemap):**  Visualiza las ventas promedio por departamento, permitiendo identificar los departamentos con mayor y menor rendimiento.

* **Ventas por Tienda y Departamento (Matriz):** Muestra un desglose detallado de las ventas por tienda y departamento, facilitando la comparación del rendimiento entre diferentes tiendas y la identificación de áreas de oportunidad.

* **Análisis Temporal (Gráfico de líneas con dimensión temporal):**  Permite analizar las ventas en función del tiempo, utilizando la dimensión temporal incorporada. Se incluyen el promedio de ventas y una media móvil para facilitar la comparación y el análisis de tendencias.

## Preparación de Datos (Power Query)

Los datos se prepararon utilizando Power Query en Power BI Desktop. Se realizaron los siguientes pasos:

1. **Importación de datos:** Se importaron los archivos CSV `train.csv`, `features.csv`, `stores.csv` y `DIM_FECHA.csv`.
2. **Fusión de tablas:** Se fusionaron las tablas `train` y `features` utilizando la columna `Store` como clave.
3. **Limpieza de datos:** Se reemplazaron los valores "NA" en las columnas `MarkDown` por valores nulos.
4. **Transformación de tipos de datos:**  Se ajustaron los tipos de datos de las columnas según su contenido (ej. número decimal para las columnas `MarkDown`).
5. **Creación de columna calculada:** Se creó la columna `FechaKey` en la tabla `Consolidado_Train_Features` para relacionarla con la tabla `DIM_FECHA`.
6. **Configuración de tabla de fechas:** Se configuró la tabla `DIM_FECHA` como tabla de fechas en Power BI.


## Modelo de Datos

El modelo de datos consta de las tablas `stores`, `Consolidado_Train_Features` y `DIM_FECHA`, relacionadas a través de las columnas `Store` y `FechaKey`.


**(Insertar imagen del modelo de datos aquí)**


## Métricas DAX

Se crearon las siguientes métricas DAX:

* **.AVG_WeeklySales:**  `AVERAGE(Consolidado_Train_Features[Weekly_Sales])` - Calcula el promedio de las ventas semanales.
* **.Sum_WeeklySales:** `SUM(Consolidado_Train_Features[Weekly_Sales])` - Calcula la suma de las ventas semanales.
* **.MediaMovil:** `CALCULATE ([.AVG_WeeklySales], DATESINPERIOD ( DIM_FECHA[FECHA], MAX (DIM_FECHA[FECHA] ), -7, DAY ))` - Calcula la media móvil de 7 días de las ventas semanales.
* **.Sum_Anio-1:** `CALCULATE ([.Sum_WeeklySales], DATEADD (DIM_FECHA[FECHA], -1, YEAR ))` - Calcula la suma de las ventas del año anterior.


## Consideraciones

Este análisis se basa en los datos proporcionados en los archivos CSV.  Se asume que los datos son representativos y están completos.  Se podrían realizar análisis adicionales para profundizar en la comprensión de los factores que influyen en las ventas, como la correlación entre las promociones y las ventas.


## Herramientas Utilizadas

* Power BI Desktop