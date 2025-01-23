# Dplyr
## Introducción
La Librería dplyr es una de las herramientas más poderosas del ecosistema R para la manipulación de datos. Forma parte del conjunto de paquetes tidyverse y está diseñada para facilitar la transformación y análisis de datos de manera eficiente.

## Principales Funciones de dplyr

La librería se basa en una serie de funciones clave que operan sobre data frames y tibbles. A continuación se presentan las más importantes:

### 1. filter() ->  Filtra filas según condiciones
 
``` código R
library(dplyr)

df <- data.frame(nombre = c("Ana", "Luis", "Carlos", "Marta"),
                 edad = c(25, 40, 35, 28))

df_filtrado <- df %>% filter(edad > 30) #obtener solo las filas donde edad > 30

print(df_filtrado)

```
### 2. select() -> Selecciona columnas específicas.
Permite elefir columnas por su nombre o rango
``` código R
# Selecionar solo la columna nombre
df_nombres <- df %>% select(nombre)

#rangos de columnas
df_rango <- df %>% select(edad:nombre)
```

### 3. mutate() → Crea o modifica columnas
Añade nuevas columnas basadas en cálculos de las existentes.

``` Código R
# Crear una nueva columna edad_doble

df_modificado <- df %>% mutate(edad_doble = edad * 2)
```

### 4. arrange() → Ordena las filas
Ordena los datos en orden ascendente o descendente.

``` Código R
# Ordenar por edad de menor a mayor

df_ordenado <- df %>% arrange(edad)

# Ordenar en orden descendente

df_ordenado_desc <- df %>% arrange(desc(edad))

```

### 5. summarise() → Resúmenes de datos
Genera estadísticas como medias, sumas o conteos.

``` Código R
# Ejemplo: Calcular la edad promedio
df_resumen <- df %>% summarise(promedio_edad = mean(edad))
```

### 6. group_by() → Agrupamiento de datos
Se usa junto con summarise() para calcular métricas por grupos.

```Código R
# Ejemplo: Promedio de edad por grupo
df_grouped <- df %>%
  group_by(nombre) %>%
  summarise(promedio_edad = mean(edad))
```

## Operador Pipe (%>%)
La librería usa el operador pipe (%>%), que permite encadenar funciones y escribir código más legible.
### Filtrar y ordenar en una sola línea
```Código R
df %>%
  filter(edad > 30) %>%
  arrange(desc(edad))

