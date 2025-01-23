# Dplyr
## Introducción
La Librería dplyr es una de las herramientas más poderosas del ecosistema R para la manipulación de datos. Forma parte del conjunto de paquetes tidyverse y está diseñada para facilitar la transformación y análisis de datos de manera eficiente.

## Principales Funciones de dplyr

La librería se basa en una serie de funciones clave que operan sobre data frames y tibbles. A continuación se presentan las más importantes:
### Obtener sólo las filas donde edad >80 
``` código R
library(dplyr)

df <- data.frame(nombre = c("Ana", "Luis", "Carlos", "Marta"),
                 edad = c(25, 40, 35, 28))

df_filtrado <- df %>% filter(edad > 30)
print(df_filtrado)
```


