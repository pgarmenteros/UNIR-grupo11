# Pheatmap
## Introducción
El paquete pheatmap en R es una herramienta versátil y fácil de usar para crear mapas de calor con una variedad de opciones de personalización. Los mapas de calor son esenciales para visualizar datos de alta dimensión, particularmente para descubrir patrones, relaciones y agrupamientos en matrices de datos. El paquete pheatmap simplifica este proceso al ofrecer funciones avanzadas como anotaciones, gradientes de color, agrupamiento jerárquico y personalización de leyendas.

### ¿Por qué usar pheatmap?

Los mapas de calor creados con **pheatmap** son invaluables en bioinformática y otras áreas de investigación porque:  

- Proporcionan una representación visual clara de conjuntos de datos complejos.  
- Facilitan la identificación de agrupamientos y patrones en datos de expresión génica, proteómica o metabolómica.  
- Permiten la anotación de datos, ayudando a comprender las relaciones entre variables.  
- Ofrecen amplias opciones de personalización, como la definición de esquemas de colores y diseños de anotación.  

---

### Cómo instalar pheatmap  

La instalación de **pheatmap** es sencilla en R. Para comenzar:  

1. Abre R o RStudio.  
2. Ejecuta el siguiente comando para instalar el paquete desde CRAN:  

```R
install.packages("pheatmap")
```  

3. Carga el paquete en tu sesión:  

```R
library(pheatmap)
```  

---

### Aplicaciones de pheatmap en bioinformática  

El paquete **pheatmap** es especialmente valioso en investigaciones bioinformáticas, donde los mapas de calor se utilizan frecuentemente para:  

**Estudios de expresión génica:**  
- Visualizar datos de expresión diferencial de genes.  
- Identificar genes coexpresados en diferentes muestras o condiciones.  
- Destacar vías y agrupamientos en datos de RNA-seq o microarrays.  

**Proteómica:**  
- Explorar niveles de expresión de proteínas en diferentes condiciones experimentales.  
- Detectar patrones en modificaciones postraduccionales.  

**Metabolómica:**  
- Comparar concentraciones de metabolitos en muestras biológicas.  
- Detectar cambios metabólicos asociados a enfermedades.  

**Estudios multi-ómicos:**  
- Integrar datos de transcriptómica, proteómica y metabolómica.  
- Comprender interacciones entre diferentes niveles moleculares.  

**Análisis de vías metabólicas:**  
- Visualizar resultados de análisis funcionales y enriquecimiento.  

**Genómica poblacional:**  
- Agrupar variantes genéticas o genotipos.  
- Comprender la estructura de poblaciones o relaciones filogenéticas.  

**Análisis de comunidades microbianas:**  
- Comparar datos de abundancia microbiana en estudios de metagenómica.  

---

### Proyectos de investigación donde pheatmap es útil  

- **Genómica del cáncer:** Analizar perfiles de expresión en tumores vs. tejidos normales.  
- **Descubrimiento de fármacos:** Identificar biomarcadores para la respuesta a tratamientos.  
- **Genómica funcional:** Investigar elementos regulatorios o el splicing alternativo.  
- **Inmunología:** Visualizar perfiles de células inmunes y niveles de citocinas.  
- **Virología:** Estudiar patrones de expresión génica viral (por ejemplo, SARS-CoV-2).  

Con su adaptabilidad y facilidad de uso, **pheatmap** es una herramienta indispensable para crear visualizaciones significativas de mapas de calor en bioinformática y otras áreas.  

---

# Argumentos de la función `pheatmap`

- **mat**: Matriz numérica con los valores que se van a representar en el mapa de calor.

- **color**: Vector de colores utilizados en el mapa de calor.

- **kmeans_k**: Número de clusters de k-means para agrupar filas antes de dibujar el mapa de calor. Si es `NA`, no se agrupan las filas.

- **breaks**: Secuencia de números que cubre el rango de valores de la matriz `mat`. Debe tener un elemento más que el vector `color`. Útil para mapear ciertos valores a colores específicos. Si se define como `NA`, los valores se calculan automáticamente. Los valores fuera del rango se asignan al color mínimo o máximo.

- **border_color**: Color de los bordes de las celdas del mapa de calor. Usa `NA` si no deseas dibujar bordes.

- **cellwidth**: Ancho individual de cada celda en puntos. Si se deja como `NA`, el tamaño depende de la ventana de trazado.

- **cellheight**:
Altura individual de cada celda en puntos. Si se deja como `NA`, el tamaño depende de la ventana de trazado.

- **scale**: Indica si los valores deben centrarse y escalarse en filas, columnas o no escalarse. Valores posibles: `"row"`, `"column"`, `"none"`.

- **cluster_rows**: Valor booleano que determina si las filas deben agruparse. También puede ser un objeto `hclust`.

- **cluster_cols**: Valor booleano que determina si las columnas deben agruparse. También puede ser un objeto `hclust`.

- **clustering_distance_rows**: Métrica de distancia para el agrupamiento de filas. Valores posibles: `"correlation"` (correlación de Pearson) y las admitidas por `dist`, como `"euclidean"`. También puede ser una matriz de distancias.

- **clustering_distance_cols**: Métrica de distancia para el agrupamiento de columnas. Valores posibles similares a las de `clustering_distance_rows`.

- **clustering_method**: Método de agrupamiento usado. Acepta los mismos valores que `hclust`.

- **clustering_callback**: Función de callback para modificar el agrupamiento. Recibe como parámetros el objeto `hclust` y la matriz usada para agrupar. Debe devolver un objeto `hclust`.

- **cutree_rows**: Número de clusters en los que se dividen las filas, basado en el agrupamiento jerárquico. Ignorado si no hay agrupamiento de filas.

- **cutree_cols**: Similar a `cutree_rows`, pero para las columnas.

- **treeheight_row**: Altura del árbol de agrupamiento de filas, si están agrupadas. Valor predeterminado: 50 puntos.

- **treeheight_col**: Altura del árbol de agrupamiento de columnas, si están agrupadas. Valor predeterminado: 50 puntos.

- **legend**: Valor lógico para determinar si se debe dibujar la leyenda.

- **legend_breaks**: Vector de puntos de interrupción para la leyenda.

- **legend_labels**: Vector de etiquetas para los puntos de interrupción de la leyenda.

- **annotation_row**: Data frame que especifica las anotaciones en el lado izquierdo del mapa de calor. Las filas se emparejan según los nombres.

- **annotation_col**: Similar a `annotation_row`, pero para las columnas.

- **annotation**: Parámetro obsoleto que establece `annotation_col` si falta.

- **annotation_colors**: Lista para especificar manualmente los colores de `annotation_row` y `annotation_col`. Es posible definir colores solo para algunas características.

- **annotation_legend**: Valor booleano que indica si se debe mostrar la leyenda de las anotaciones.

- **annotation_names_row**: Valor booleano que indica si se deben mostrar los nombres de las anotaciones de fila.

- **annotation_names_col**: Valor booleano que indica si se deben mostrar los nombres de las anotaciones de columna.

- **drop_levels**: Determina si los niveles no usados se muestran en la leyenda.

- **show_rownames**: Especifica si se deben mostrar los nombres de las filas.

- **show_colnames**: Especifica si se deben mostrar los nombres de las columnas.

- **main**: Título del gráfico.

- **fontsize**: Tamaño de fuente base para el gráfico.

- **fontsize_row**: Tamaño de fuente para los nombres de las filas (predeterminado: `fontsize`).

- **fontsize_col**: Tamaño de fuente para los nombres de las columnas (predeterminado: `fontsize`).

- **angle_col**: Ángulo de las etiquetas de las columnas. Opciones disponibles: 0, 45, 90, 270 y 315.

- **display_numbers**: Valor lógico para determinar si se deben mostrar valores numéricos en las celdas. Si es una matriz con las mismas dimensiones, se muestra su contenido en lugar de los valores originales.

- **number_format**: Formato de los números mostrados en las celdas (estilo printf en C, e.g., `"%.2f"` para 2 decimales).

- **number_color**: Color del texto numérico.

- **fontsize_number**: Tamaño de fuente de los números en las celdas.

- **gaps_row**: Vector con índices de filas donde insertar espacios. Solo usado si las filas no están agrupadas.

- **gaps_col**: Similar a `gaps_row`, pero para columnas.

- **labels_row**: Etiquetas personalizadas para las filas, en lugar de los nombres de las filas.

- **labels_col**: Similar a `labels_row`, pero para las columnas.

- **filename**: Ruta del archivo donde guardar la imagen. El tipo de archivo se decide por la extensión (png, pdf, tiff, bmp, jpeg).

- **width**: Ancho del archivo de salida en pulgadas.

- **height**: Altura del archivo de salida en pulgadas.

- **silent**: Si es `TRUE`, no se dibuja el gráfico (útil cuando se usa la salida de tipo `gtable`).

- **na_col**: Especifica el color de las celdas con valores `NA`.

- **…**: Parámetros gráficos adicionales para el texto del gráfico, pasados a `grid.text` (ver `gpar`).

---

# Conceptos relacionados con los mapas de calor

Antes de profundizar en la creación de mapas de calor con **pheatmap**, repasemos algunos conceptos clave asociados a ellos:  

- **Escalado de datos (Data Scaling)**: El escalado de datos es un paso importante en el preprocesamiento para crear mapas de calor. Consiste en transformar los valores de los datos a una escala estandarizada para evitar que puntos de datos con magnitudes muy diferentes distorsionen la escala de colores. Esto garantiza que todos los valores sean comparables dentro del mapa de calor.  

- **Agrupamiento de filas y columnas (Row and Column Clustering)**: El agrupamiento (clustering) consiste en agrupar filas o columnas similares basándose en sus valores de datos. Este enfoque ayuda a identificar patrones, tendencias y relaciones dentro de los datos. El agrupamiento jerárquico es una técnica comúnmente utilizada para visualizar estas similitudes.  

- **Esquemas de colores (Color Schemes)**: Los esquemas de colores se utilizan para asignar los valores de los datos a colores específicos en el mapa de calor. La elección del esquema de colores es fundamental y depende del tipo de datos que se están visualizando y del mensaje que se desea transmitir. Por ejemplo:  
    - Gradientes suaves para valores continuos.  
    - Colores contrastantes para datos categóricos o de relevancia específica.  

---



