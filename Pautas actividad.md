#Actividad. Representación gráfica de datos y análisis de resultados

##Objetivos 
En esta actividad, aplicarás los conceptos aprendidos sobre visualización de datos biológicos y análisis estadístico. Utilizarás un dataset que contiene información de la expresión de 46 genes en 65 pacientes, cada uno con distintos tipos de tratamiento y características tumorales. El objetivo principal es que seas capaz de interpretar los datos mediante la generación de gráficos adecuados y la respuesta a preguntas específicas que se detallan más adelante.

##Pautas de elaboración

Esta actividad consistirá en dos partes principales relacionado con datos de diferentes genes: 1) elaboración de código para que generes gráficos y los reflejes en el documento HTML; y 2) breve interpretación de los gráficos del dataset en el documento HTML.

A continuación verás: un apartado que explica el dataset, mientras que el siguiente son las preguntas que deberás de contestar.

Dataset de expresión de genes: para la realización de esta parte de la actividad, deberás cargar el dataset de interés «Dataset expresión genes.csv», el cual se trata de una base de datos de 65 pacientes que contiene información de la expresión de 46 genes con diferentes funciones (para más información, ver el apartado de «Información de interés del dataset» después de la rúbrica). Además de estas variables, contiene otras variables de interés como el tratamiento (A o B) que siguen cada paciente, tipo de tumor que tienen (colorrectal, pulmón y mama) y la extensión tumoral (localizado, metastásico o regional). Por último, se recoge información de variables bioquímicas, síntomas y otras variables sociodemográficas.

Tras importarlo, deberás responder a las siguientes cuestiones, teniendo en cuenta todos los gráficos generados mediante ggplot2, pheatmap o ComplexHeatmap. R se caracteriza por su amplia gama de funciones para la creación de gráficos originales. Los gráficos profesionales deben tener: título y subtítulo, etiquetas de ejes, leyenda (si aplica), etiquetas de datos, escalas apropiadas, colores y estilos uniformes, ajustes de líneas y puntos similar en todos los gráficos, temas consistentes, etc.

---

##1. Teniendo en cuenta los siguientes genes: AQ_ALOX5, AQ_CD274, AQ_CHKA, AQ_CSF2, AQ_FOXO3, AQ_IL6, AQ_LDHA, AQ_LIF, AQ_MAPK1, AQ_NOS2, AQ_IFNG, AQ_PDCD1, AQ_PPARG, AQ_TGFB1, AQ_TNF:
- Para responder este ejercicio, apóyate en un diagrama de cajas en el que visualices por cada expresión de gen 2 cajas: 1 para trata y otro para tratB.
- ¿Qué interpretación sacas de la distribución de la expresión de los genes cuando los comparamos por tipo de tratamiento? (mínimo 150 palabras de extensión).
- Consejos: 
  - Crea los gráficos de forma individual y luego para visualizarlos mejor en 1 gráfica conjunta, utiliza la librería library(patchwork) (https://patchwork.data-imaginist.com):
    combined_plot <- plot_A + plot_B + … + plot_layout(ncol = 3) # ncol es el número de columnas que quieres que haya en tu gráfico, juega con este dato para poder encajar bien los gráficos.
  - Para ayudarte en la interpretación de la expresión de genes (valores AQ), ver el apartado de Información de interés del dataset después de la rúbrica).

---

##2. Teniendo en cuenta los siguientes parámetros bioquímicos para toda la población: glucosa, leucocitos, linfocitos, neutrofilos, chol, hdl, hierro, igA, igE, igG, igN, ldl, pcr, transferrina, trigliceridos, cpk:
- Para responder este ejercicio, apóyate en un histograma en el que se visualice la frecuencia de cada variable utilizando aproximadamente 30 bins (a mayor bins, mayor número de barras).
- ¿Qué interpretación sacas de la distribución de los datos de las variables bioquímicas en toda la población? (mínimo 100 palabras de extensión).
- ¿Crees que sigue una distribución normal o simétrica en la que se visualiza una distribución parecida a una campana de Gauss? (mínimo 100 palabras de extensión).
- Consejos: puedes utilizar la función geom_density (https://r-charts.com/distribution/histogram-density-ggplot2/) vista en clase para visualizar la densidad.

---

##3. Mapea todos los valores de expresión de genes para poder visualizar posibles patrones entre los datos de los pacientes:
- Para responder esta pregunta, apóyate en un heatmap en el que visualices los datos crudos de todas las variables AQ (expresión de genes). 
- ¿Hay algún tipo de patrón de pacientes que tiene la expresión de genes similar o diferenciada? (mínimo 150 palabras de extensión).
- ¿Hay grupos de genes con patrones de expresión similares o diferenciadas? 
- Consejos: 
  - Puedes utilizar la librería pheatmap o ComplexHeatmap (instalación previa) vista en clase para visualizar patrones de los datos jerárquicamente.
  - Establece antes del gráfico siempre una semilla de aleatorización, para que pueda ser reproducible para todos de una forma similar, utilizaremos siempre set.seed(1995). Si no pones esta semilla de aleatorización, tu gráfico cambiará cada vez que ejecutas la sintaxis y no será igual al resto de tus compañeros.
  - Escala siempre los datos para que sean comparables entre sí usando la función scale(dataframe), lo que normaliza las variables centrándolas alrededor de una media de 0 y una desviación estándar de 1, asegurando que todas las variables contribuyan equitativamente al análisis.
  - No se te pide que hagas correlaciones, simplemente visualiza de forma cruda los datos, en donde el eje X se localicen los pacientes, mientras que en el eje Y las variables de los genes. 
  - Para visualizar patrones, recuerda que hay funciones específicas dentro de las librerías de pheatmap o ComplexHeatmap. Por ejemplo, en pheatmap (https://r-charts.com/es/correlacion/pheatmap/ y https://davetang.org/muse/2018/05/15/making-a-heatmap-in-r-with-the-pheatmap-package/) está las funciones row_km, cutree_rows, column_km, cutree_cols. Por ejemplo, en ComplexHeatmap (https://jokergoo.github.io/ComplexHeatmap-reference/book/a-single-heatmap.html#heatmap-split) están las funciones row_km y column_km. Estas funciones podéis encontrarlas en el help de R o en Google para ver cómo funcionan.

---

##Extensión y formato 
Para la resolución de esta actividad, deberás entregar dos archivos:
- Un único fichero R Markdown (.Rmd) con todo el código y texto Markdown que hayas generado. No existe un límite de extensión para este fichero.
- Un fichero HTML generado a partir de dicho archivo R Markdown. Asegúrate de que aparecen todas las figuras, todo el texto y todos los cuadros de código R que hayas introducido en el archivo .Rmd anterior. Este fichero es el evaluable.
