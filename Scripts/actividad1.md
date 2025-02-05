---
title: "Estadística y R para Ciencias de la Salud"
author: "Adrián Alberto Castillo Domínguez"
output: html_document
date: "18 de Noviembre de 2024"
---

```{r setup, include=TRUE}
#Eliminar todas las variables y objetos del espacio de trabajo
rm(list = ls())

#Cargar librerías
library(conflicted)
conflict_prefer("filter", "dplyr")
library(tidyverse)
library(pheatmap)

#Importar el archivo CSV de la actividad
datos <- read.csv("Dataset expresión genes.csv")
```
<br>


<span style="font-size: 22px; font-weight: bold;">Actividad 1. Representación gráfica de datos y análisis de resultados.

<span style="font-size: 15px; font-weight: bold;">1.1. Genera un diagrama de cajas en el que se visualice por cada expresión de gen 2 cajas, una para el tratamiento A y otra para el tratamiento B.</span>

<br>

```{r apartado_1a, echo=TRUE, out.width="50%", out.height="50%"}
# Seleccionar los datos de interes
genes <- c("AQ_ALOX5", "AQ_CD274", "AQ_CHKA", "AQ_CSF2", "AQ_FOXO3", "AQ_IL6", "AQ_LDHA", "AQ_LIF", "AQ_MAPK1", "AQ_NOS2", "AQ_IFNG", "AQ_PDCD1", "AQ_PPARG", "AQ_TGFB1", "AQ_TNF")
data_nf <- datos %>%
  select(id, trat, all_of(genes)) %>%
  pivot_longer(cols = all_of(genes), names_to = "gen", values_to = "expresion")

# Crear un diagrama de cajas para cada gen separado por tratamiento
for (gen_var in genes) {
  
  # Filtrar datos para el gen actual
  data_gen <- data_nf %>% filter(gen == gen_var)
  
  # Crear el diagrama de cajas para el gen actual
  diagrama <- ggplot(data_gen, aes(x = trat, y = expresion, fill = trat)) +
    geom_boxplot() +
    labs(title = paste("Niveles de expresión de ", gen_var),
         x = "Tratamiento",
         y = "Expresión génica") +
    scale_fill_manual(name = "Tratamiento", 
                      values = c("tratA" = "skyblue", "tratB" = "orange")) +
    theme_minimal() +
    theme(
      axis.text.x = element_text(angle = 45, hjust = 1),
      text = element_text(family = "sans", size=16 ),
      plot.title = element_text(hjust = 0.5),
      legend.title = element_text(size = 10)
      )
  print(diagrama)
}
```

<br><br>


```{r apartado_1b, echo=TRUE, out.width="100%", out.height="100%"}
# Crear un diagrama de cajas conjunto para todos los genes
diagrama_conj <- data_nf %>%
  ggplot(aes(x = trat, y = expresion, fill = trat)) +
  geom_boxplot() +
  facet_wrap(~ gen, scales = "free_y") +  # Separación de los genes en diferentes diagramas
  labs(title = "Niveles de expresión génica por tratamiento", # Personalización de las etiquetas del gráfico
       x = "Tratamiento",
       y = "Expresión génica") +
  scale_fill_manual(name = "Tratamiento",  # Título de la leyenda
                    values = c("tratA" = "skyblue", "tratB" = "orange")) + # Colores personalizados
  theme_bw() +
  theme(
    text = element_text(family = "sans" ),
    axis.text.x = element_text(size = 8, angle = 45, hjust = 0.8),
    axis.text.y = element_text(size = 7),
    plot.title = element_text(hjust = 0.5, size = 12, vjust = 2.5),
    axis.title.y = element_text(size = 10, angle = 90, hjust = 0.5, vjust = 4),
    axis.title.x = element_text(size = 9),
    legend.title = element_text(size = 8),
    legend.text = element_text(size = 7),
    strip.background = element_blank(),
    strip.text = element_text(size = 8)
    )
print(diagrama_conj)
```


<br><br>

<span style="font-size: 15px; font-weight: bold;">1.2. ¿Qué interpretación sacas de la distribución de la expresión de los genes cuando los comparamos por tipo de tratamiento?</span>

<span style="text-align: justify; display: block;">Los diagramas de cajas (box plots) son herramientas útiles para representar la distribución de datos, mostrando cuartiles a través de una caja central y líneas (bigotes) que indican los valores mínimo y máximo. La caja representa el rango intercuartílico (IQR), que abarca el 50% central de los datos, mientras que la línea central indica la mediana. Los puntos fuera de los bigotes representan outliers o datos atípicos. Se han representado cuantificaciones absolutas, midiendo la expresión génica y reflejando así la actividad de varios genes en distintas condiciones de tratamiento. Por tanto, un valor de 0 indicará que el gen no muestra actividad detectable en las muestras estudiadas.

<span style="text-align: justify; display: block;">En los resultados obtenidos, se observa que en la mayoría de los genes analizados, la expresión génica es más baja en presencia del tratamiento B en comparación con el tratamiento A. Esta tendencia se refleja en genes como AQ_CD274, AQ_CHKA, AQ_CSF2, AQ_IL6, AQ_LIF, AQ_MAPK1, AQ_IFNG, AQ_PDCD1, AQ_TGFB1, y AQ_TNF, donde se aprecia una disminución significativa de la expresión en el tratamiento B. Estos resultados sugieren que el tratamiento B podría tener un efecto inhibitorio sobre la expresión de estos genes, lo que podría indicar una respuesta reguladora o supresora frente a la estimulación del tratamiento. Este patrón es común en terapias que buscan modular la expresión génica en la lucha contra enfermedades o en la regulación de ciertos procesos biológicos.

<span style="text-align: justify; display: block;">Sin embargo, en el caso de otros genes como AQ_ALOX5, AQ_FOXO3, AQ_LDHA, AQ_NOS2, y AQ_PPARG, no se observa una alteración significativa en su expresión tras la administración del tratamiento B. En estos casos, los tratamientos no parecen tener un efecto pronunciado en la regulación de estos genes, lo que podría indicar que estos genes están bajo una regulación menos sensible a las condiciones experimentales o que están involucrados en procesos biológicos distintos que no se ven afectados por el tratamiento B.

<span style="text-align: justify; display: block;">En ningún caso se observó un aumento en los niveles de expresión de los genes en presencia del tratamiento B. Esto es relevante, ya que sugiere que el tratamiento no tiene efectos positivos sobre la expresión génica en los genes analizados. En otras palabras, no se observó ningún efecto estimulante de B sobre los genes estudiados comparándolo con el tratamiento A, lo cual es importante para interpretar las características y mecanismos de acción de ambos tratamientos.

<span style="text-align: justify; display: block;">Adicionalmente, se observa que las medianas de expresión en los diagramas de caja (boxplots) son muy similares entre los distintos grupos, a pesar de las diferencias en los niveles de expresión. Este fenómeno podría reflejar que, aunque los tratamientos generan diferencias en la expresión de ciertos genes, la tendencia central de la expresión no varía tanto entre los grupos. Las medianas representan el punto medio de la distribución de los datos, y su similitud sugiere que la respuesta global a los tratamientos no muestra grandes alteraciones en cuanto a la posición central de los datos. Sin embargo, es importante analizar otras métricas, como la dispersión de los datos, para obtener una visión más completa del impacto de los tratamientos en la expresión génica.</span>

<br><br>

<span style="font-size: 15px; font-weight: bold;">2.1. Teniendo en cuenta los parámetros bioquímicos de la población de estudio, genera un histograma en el que se visualice la frecuencia de cada variable utilizando aproximadamente 30 bins.</span>

<br>

```{r apartado_2a, echo=TRUE, out.width="50%", out.height="50%"}
# Seleccionar los datos de interes
vbq <- c("glucosa", "leucocitos", "linfocitos", "neutrofilos", "chol", "hdl", "hierro", "igA","igE", "igG", "igN", "ldl","pcr", "transferrina", "trigliceridos", "cpk")
data_nf2 <- datos %>%
  select(id, all_of(vbq))

#Generar el histograma para cada variable bioquímica
suppressWarnings(for (vbq_var in vbq) {
  histogram <- ggplot(data=data_nf2, aes_string(x = vbq_var))  + 
    geom_histogram(aes(y = ..density..),bins=30, fill="skyblue", color="black", position = "identity") +
    geom_density(color = "red", size = 1) +
    labs(title = paste("Histograma de", vbq_var),
         x = "Valores medidos",
         y = "Frecuencia") +
    theme_minimal() +
    theme(
      axis.text.x = element_text(angle = 45, hjust = 1),
      text = element_text(family = "sans", size=16 ),
      plot.title = element_text(hjust = 0.5),
      legend.title = element_text(size = 10))
  print(histogram)
})
```

<br><br>

```{r apartado_2b, echo=TRUE, out.width="120%", out.height="120%"}
# Seleccionar los datos de interes
vbq <- c("glucosa", "leucocitos", "linfocitos", "neutrofilos", "chol", "hdl", "hierro", "igA","igE", "igG", "igN", "ldl","pcr", "transferrina", "trigliceridos", "cpk")
data_nf2 <- datos %>%
  select(id, all_of(vbq)) %>%
  pivot_longer(cols = all_of(vbq), names_to = "bq", values_to = "valores")

# Generar histograma para todas las variables bioquímicas
histogram_conj <- ggplot(data=data_nf2, aes_string(x = "valores"))  +
  geom_histogram(aes(y = ..density..),bins=30, fill="skyblue", color="black", position = "identity") +
  geom_density(color = "red", size = 1.25) +
  facet_wrap(~ bq, scales = "free") +
  labs(title = paste("Histograma de las variables bioquímicas"),
       x = "Valores medidos",
       y = "Frecuencia") +
  theme_minimal() +
  theme(
    text = element_text(family = "sans" ),
    axis.text.x = element_text(size = 7, angle = 90, hjust = 0.8),
    axis.text.y = element_text(size = 7),
    plot.title = element_text(hjust = 0.5, size = 12, vjust = 2.5),
    axis.title.y = element_text(size = 10, angle = 90, hjust = 0.5, vjust = 4),
    axis.title.x = element_text(size = 9),
    legend.title = element_text(size = 8),
    legend.text = element_text(size = 7),
    strip.background = element_blank(),
    strip.text = element_text(size = 8)
    )
suppressWarnings({
  print(histogram_conj)
})
```

<br><br>

<span style="font-size: 15px; font-weight: bold;">2.2.¿Qué interpretación sacas de la distribución de los datos de las variables bioquímicas en toda la población? </span>

<span style="text-align: justify; display: block;">Los histogramas son herramientas gráficas que permiten visualizar la distribución de datos continuos al dividir la variable en intervalos o "bins". Ayudan a identificar patrones en los datos, como la concentración de valores en ciertas áreas, la presencia de valores extremos y la forma general de la distribución. Al analizarlos, podemos determinar si los datos siguen una distribución simétrica, sesgada o normal. Las curvas de densidad son una versión suavizada de los histogramas, que muestran de forma continua la distribución de los datos, proporcionando una visión más precisa, especialmente con grandes conjuntos de datos. Al interpretar una curva de densidad, se deben observar aspectos como la forma, el centro y la dispersión de los datos.

<span style="text-align: justify; display: block;">En los resultados obtenidos, se observa que, en términos generales, los datos tienden a concentrarse alrededor de un valor central, lo cual es un patrón esperado en muchas distribuciones estadísticas. Este comportamiento sugiere que la mayoría de los individuos de la población presentan valores similares para las variables estudiadas, lo que indica cierta homogeneidad dentro del grupo en cuanto a esas características específicas. Sin embargo, al analizar más detalladamente, se observa que algunas variables presentan una mayor dispersión, lo cual indica una variabilidad considerable en los valores de esas características. Variables como lipoproteínas de alta densidad (hdl), creatina fosfoquinasa (cpk) y colesterol total (chol) muestran esta mayor dispersión, lo que sugiere que los datos no se distribuyen de manera uniforme alrededor del centro, sino que se extienden más ampliamente hacia ambos extremos. Esta variabilidad podría ser el resultado de múltiples factores, tales como diferencias biológicas entre los individuos, la presencia de subgrupos dentro de la población, o incluso la influencia de otros factores externos, como hábitos de vida, dietas o tratamientos previos.

<span style="text-align: justify; display: block;">La dispersión observada también puede reflejar una heterogeneidad en la población, lo que implica que no todos los individuos responden de la misma manera a ciertos factores o condiciones de salud, lo que puede ser importante para la interpretación y el análisis de los resultados. Este comportamiento no es inusual en estudios que involucran características biológicas, ya que los individuos pueden presentar variaciones naturales en los niveles de ciertos parámetros bioquímicos debido a diferencias genéticas, fisiológicas o ambientales.

<span style="text-align: justify; display: block;">Además de esta variabilidad, se identifican valores atípicos o outliers, es decir, puntos de datos que se desvían significativamente de la concentración principal de la mayoría de los valores. Estos valores atípicos pueden ser indicativos de varios fenómenos. En algunos casos, podrían ser el resultado de errores de medición o de errores experimentales, como fallos en el equipo de medición, errores humanos o problemas técnicos durante la recolección de datos. En otros casos, los valores atípicos podrían reflejar fenómenos raros o condiciones excepcionales en la población estudiada. Por ejemplo, un valor extremadamente alto de colesterol podría indicar un caso específico de dislipidemia en un individuo, lo cual no es representativo del comportamiento general de la población, pero es relevante desde una perspectiva clínica.La presencia de estos valores atípicos debe ser cuidadosamente analizada, ya que su influencia en los resultados podría distorsionar las conclusiones si no se tienen en cuenta adecuadamente.</span> 

<br>

<span style="font-size: 15px; font-weight: bold;">2.3.¿Crees que sigue una distribución normal o simétrica en la que se visualiza una distribución parecida a una campana de Gauss?</span>


<span style="text-align: justify; display: block;">Podemos observar que algunas de las distribuciones de las variables bioquímicas son simétricas, lo que sugiere que los datos de estas variables podrían seguir una distribución normal. Este tipo de distribución es característico de muchos fenómenos biológicos y estadísticos, donde los valores se distribuyen de manera equilibrada alrededor de un valor central, es decir, la media o la mediana. Ejemplos de variables que parecen seguir una distribución normal incluyen colesterol (chol), lipoproteínas de alta densidad (hdl), leucocitos, linfocitos, igN, lipoproteínas de baja densidad (ldl), transferrina y triglicéridos. Para estas variables, no parece haber muchos valores extremos o inusuales, y la mayoría de los datos se concentran en una zona alrededor del valor medio.

<span style="text-align: justify; display: block;">Por otro lado, algunas variables presentan distribuciones asimétricas, lo que indica que los datos pueden no seguir una distribución normal. Esto puede ser un indicio de que los valores están sesgados hacia un extremo, ya sea hacia valores más altos o más bajos. El sesgo podría deberse a la presencia de valores atípicos o a que la población no sigue un patrón normal debido a factores biológicos. Las variables que muestran una asimetría incluyen proteína C reactiva (pcr), glucosa, hierro, neutrófilos, creatina fosfoquinasa (cpk), inmunoglobulina A (igA), inmunoglobulina E (igE) e inmunoglobulina G (igG). En estos casos, la distribución de los datos podría reflejar la variabilidad natural de la población en ciertos trastornos o condiciones de salud.

<span style="text-align: justify; display: block;">En resumen, la simetría en algunas distribuciones sugiere una distribución normal, mientras que la asimetría en otras variables podría ser el resultado de un sesgo o de falta de normalidad, lo que tiene implicaciones importantes para los análisis estadísticos y la interpretación de los datos.</span>

<br>

<span style="font-size: 15px; font-weight: bold;">3.1.Mapea todos los valores de expresión de genes para poder visualizar posibles patrones entre los datos de los pacientes.</span>

<br>

```{r apartado_3a, echo=TRUE, out.width="100%", out.height="100%"}
# Seleccionar solo las columnas de expresión génica e ids
datos_hm <- datos %>%
  select(starts_with("AQ_"),-one_of("AQ_ADIPOQ", "AQ_NOX5"))

# Convertir 'ids' en nombres de fila
rownames(datos_hm) <- datos$id

# Estandarizar y transponer los datos
datos_hm_ts <- t(scale(datos_hm))

# Heatmap
set.seed(1995)
pheatmap(datos_hm_ts,
         main = "Heatmap de los genes para cada paciente",
         cluster_cols = TRUE,
         cluster_rows = TRUE,
         color = colorRampPalette(c("blue", "white", "red"))(100),
         show_rownames = TRUE,
         show_colnames = TRUE,
         fontsize = 6,
         )
```

<br>

<span style="font-size: 15px; font-weight: bold;">3.2.¿Hay algún tipo de patrón de pacientes que tiene la expresión de genes similar o diferenciada?</span>

<span style="text-align: justify; display: block;">En los resultados obtenidos, se puede observar una clara división de los pacientes en 4 grupos principales, basados en sus patrones de expresión génica. El primer grupo está compuesto por aproximadamente el 40% de los pacientes, quienes presentan una expresión génica muy baja. Este grupo podría estar asociado con una falta de activación de los genes en respuesta a ciertos estímulos o condiciones biológicas, lo que sugiere una regulación génica reducida o una falta de respuesta en comparación con otros grupos.El segundo grupo, que representa alrededor del 30% de los pacientes, muestra una expresión baja de los genes en comparación con otros grupos, pero aún superior al primer grupo. Estos pacientes podrían estar experimentando una expresión génica moderada, posiblemente debido a factores que afectan parcialmente su activación génica. El tercer grupo, que comprende cerca del 20% de los pacientes, muestra una expresión media. En este caso, los pacientes en este grupo tienen una activación génica más pronunciada, lo que podría reflejar un equilibrio entre la expresión génica y las condiciones biológicas. El cuarto y último grupo, que agrupa alrededor del 10% de los pacientes, se caracteriza por una expresión media-alta. Este grupo refleja una mayor activación génica, lo que podría estar relacionado con una respuesta activa a estímulos o condiciones fisiológicas específicas. Estos pacientes podrían estar experimentando un nivel de respuesta biológica más alto, lo que sugiere que los genes involucrados están más activos en comparación con los demás grupos.

<br>

<span style="font-size: 15px; font-weight: bold;">3.3.¿Hay grupos de genes con patrones de expresión similares o diferenciadas?</span>

<span style="text-align: justify; display: block;">Al analizar los genes, se observa una clara división en 4 grupos diferenciados que comparten una expresión similar entre ellos. Estos grupos de genes presentan patrones de expresión coherentes dentro de cada uno, lo que sugiere que podrían estar involucrados en procesos biológicos relacionados o en redes de regulación génica comunes. Cada grupo de genes podría representar una función biológica específica o una respuesta adaptativa frente a estímulos o condiciones particulares, proporcionando así información valiosa sobre los mecanismos moleculares subyacentes en los pacientes.

<br>
<br>
<br>
<br>
