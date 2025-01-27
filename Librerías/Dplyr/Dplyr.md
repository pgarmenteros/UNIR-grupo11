# Dplyr
## Introducción
La Librería dplyr es una de las herramientas más poderosas del ecosistema R para la manipulación de datos. Forma parte del conjunto de paquetes **tidyverse** y está diseñada para facilitar la transformación y análisis de datos de manera eficiente.

## Principales Funciones de dplyr

La librería se basa en una serie de funciones clave que operan sobre data frames y tibbles. A continuación se presentan las más importantes:

### 1. `filter()` ->  Filtra filas según condiciones
 
``` r
library(dplyr)

df <- data.frame(nombre = c("Ana", "Luis", "Carlos", "Marta"),
                 edad = c(25, 40, 35, 28))

df_filtrado <- df %>% filter(edad > 30) # Obtener solo las filas donde edad > 30

print(df_filtrado)

```
### 2. `select()` -> Selecciona columnas específicas.
Permite elegir columnas por su nombre o rango
``` r

# Seleccionar solo la columna nombre
df_nombres <- df %>% select(nombre)

# Rangos de columnas
df_rango <- df %>% select(edad:nombre)

```

### 3. `mutate()` → Crea o modifica columnas
Añade nuevas columnas basadas en cálculos de las existentes.

``` r

# Crear una nueva columna edad_doble
df_modificado <- df %>% mutate(edad_doble = edad * 2)

```

### 4. `arrange()` → Ordena las filas
Ordena los datos en orden ascendente o descendente.

``` r
# Ordenar por edad de menor a mayor
df_ordenado <- df %>% arrange(edad)

# Ordenar en orden descendente
df_ordenado_desc <- df %>% arrange(desc(edad))


```

### 5. `summarise()` → Resúmenes de datos
Genera estadísticas como medias, sumas o conteos.

``` r
# Ejemplo: Calcular la edad promedio
df_resumen <- df %>% summarise(promedio_edad = mean(edad))

```

### 6. `group_by()` → Agrupamiento de datos
Se usa junto con `summarise()` para calcular métricas por grupos.

``` r
# Ejemplo: Promedio de edad por grupo
df_grouped <- df %>%
  group_by(nombre) %>%
  summarise(promedio_edad = mean(edad))

```

## Operador Pipe (`%>%`)
La librería usa el operador pipe (%>%), que permite encadenar funciones y escribir código más legible.
### Filtrar y ordenar en una sola línea

``` r
df %>%
  filter(edad > 30) %>%
  arrange(desc(edad))
```

## Ejemplos de aplicaciones en la bioinformática
`dplyr` es una herramienta fundamental en bioinformática para manipular, limpiar y analizar datos de gran tamaño en estudios genómicos, transcriptómicos y metagenómicos. Su uso optimiza el preprocesamiento y facilita la interpretación de datos biológicos.
### 1. Filtrar secuencias genéticas según criterios específicos
Los datos genómicos suelen contener información sobre genes, mutaciones y expresiones génicas. `dplyr` permite filtrar rápidamente secuencias de interés

- **Filtrar genes con expresión mayo a 1000 en un dataset de RNA-Seq**. Uso en transcriptómica, para seleccionar genes altamente expresados
``` r

# Simulación de un dataset con genes y su expresión
genes <- data.frame(
  Gene = c("BRCA1", "TP53", "EGFR", "MYC", "APOE"),
  Expresion = c(1200, 800, 1500, 200, 3000)
)

# Filtrar genes con expresión mayor a 1000
genes_filtrados <- genes %>% filter(Expresion > 1000)
print(genes_filtrados)
```
### 2. Seleccionar solo columnas relevantes en datos biológicos 
Los datos suelen tener muchas columnas innecesarias. `select()`ayuda a mantener solo lo necesario
- **Seleccionar solo ID y expresión en datos genómicos**. Para simplificar las tablas con muchas variables irrelevantes.
``` r
genes_reducidos <- genes %>% select(Gene, Expresion)
```
### 3. Crear nuevas variables a partir de datos biológicos
`mutate()`es útil para calcular valores derivados de datos crudos
- **Normalizar expresión génica dividiéndola entre el valor máximo

``` r
genes_normalizados <- genes %>%
  mutate(Expresion_Norm = Expresion / max(Expresion))
```
### 4. Ordenar datos genómicos por expresión génica
A veces es útil ver los genes más y menos expresados 
- **Ordenar genes de mayor a menor expresión**. Para encontrar genes con mayor relevancia en un estudio
``` r
genes_ordenados <- genes %>% arrange(desc(Expresion))
```
### 5. Agrupar y resumir datos por condiciones experimentales
En estudios de expresión génica, se comparan muestras de diferentes condiciones
- **calcular la expresión promedio por tipo de célula**. Para comparar expresión génica entre condiciones experimentales
``` r
expresion_celulas <- data.frame(
  Gene = c("BRCA1", "TP53", "EGFR", "MYC", "APOE"),
  Celula = c("Cáncer", "Sana", "Cáncer", "Cáncer", "Sana"),
  Expresion = c(1200, 800, 1500, 200, 3000)
)

# Promedio de expresión por tipo de célula
expresion_resumen <- expresion_celulas %>%
  group_by(Celula) %>%
  summarise(Expresion_Prom = mean(Expresion))
```

### 6. Integración con datos de metagenómica y microbiomas
Para analizar comunidades microbianas, se suele trabajar con archivos **OTU** (Operational Taxonomic Units) o **datos de taxonomía**
- **Filtrar bacterias con más de 500 lecturas en metagenómica**. Para analizar la abundancia relativa de distintos grupos bacterianos.

``` r
otu_table <- data.frame(
  Taxonomia = c("Firmicutes", "Bacteroidetes", "Proteobacteria", "Actinobacteria"),
  Lecturas = c(1500, 800, 300, 700)
)

# Filtrar bacterias con más de 500 lecturas
bacterias_abundantes <- otu_table %>% filter(Lecturas > 500)
```
