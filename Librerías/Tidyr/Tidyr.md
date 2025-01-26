# tidyr: Limpieza y organización de datos en R

`tidyr` es una librería de R diseñada para ayudar a limpiar, organizar y transformar datos de manera estructurada y ordenada. Forma parte del ecosistema de paquetes `tidyverse`, que ofrece herramientas para la manipulación de datos de forma intuitiva y eficiente.

<a href="https://github.com/pgarmenteros/UNIR-grupo11/blob/Adrian/Librer%C3%ADas/Tidyr/cheat%20sheet%20tidyr.pdf">
  <img src="https://github.com/pgarmenteros/UNIR-grupo11/blob/Adrian/Librer%C3%ADas/Tidyr/Miniatura%20cheat%20sheet%20tidyr1.png" alt="Vista previa 1" width="300">
</a>
<a href="https://github.com/pgarmenteros/UNIR-grupo11/blob/Adrian/Librer%C3%ADas/Tidyr/cheat%20sheet%20tidyr.pdf">
  <img src="https://github.com/pgarmenteros/UNIR-grupo11/blob/Adrian/Librer%C3%ADas/Tidyr/Miniatura%20cheat%20sheet%20tidyr2.png" alt="Vista previa 2" width="300">
</a>


## Características principales

- **Conversión de datos desordenados a formatos "tidy"** (ordenados y estructurados).
- **Funciones intuitivas para la manipulación de datos tabulares**, permitiendo una mejor comprensión y exploración.
- **Integración con otros paquetes del tidyverse**, como `dplyr` para la manipulación de datos, `ggplot2` para visualización y `readr` para importación de datos.
- **Facilita la preparación de datos para análisis y visualización**, asegurando la coherencia en su estructura.
- **Funciones para gestionar valores faltantes**, transformación de columnas y reestructuración de tablas.

## Principales funciones de tidyr

A continuación, se describen algunas funciones clave que proporciona `tidyr` para manipular datos:

### 1. `pivot_longer()`
Convierte columnas en filas, ideal para transformar datos anchos a largos, facilitando su análisis.

**Sintaxis:**
```r
pivot_longer(data, cols, names_to, values_to)
```

**Ejemplo:**
```r
library(tidyr)
data <- data.frame(
  id = 1:3,
  var1 = c(10, 20, 30),
  var2 = c(40, 50, 60)
)

data_long <- pivot_longer(data, cols = c(var1, var2), names_to = "variable", values_to = "valor")
```

### 2. `pivot_wider()`
Convierte filas en columnas, útil para transformar datos largos a anchos y mejorar la legibilidad.

**Sintaxis:**
```r
pivot_wider(data, names_from, values_from)
```

**Ejemplo:**
```r
pivot_wider(data_long, names_from = "variable", values_from = "valor")
```

### 3. `expand()`
Genera todas las combinaciones posibles de valores en las columnas seleccionadas, útil para análisis de datos.

**Sintaxis:**
```r
expand(data, ...)
```

**Ejemplo:**
```r
data <- data.frame(producto = c("A", "B"), region = c("Norte", "Sur"))
data_expanded <- expand(data, producto, region)
```

### 4. `complete()`
Asegura que todas las combinaciones posibles de valores de una o más columnas estén presentes en los datos.

**Sintaxis:**
```r
complete(data, ...)
```

**Ejemplo:**
```r
data_complete <- complete(data, producto, region)
```

### 5. `replace_na()`
Reemplaza valores faltantes en una o más columnas con valores específicos.

**Sintaxis:**
```r
replace_na(data, replace)
```

**Ejemplo:**
```r
data <- data.frame(a = c(1, NA, 3), b = c(4, 5, NA))
data_replaced <- replace_na(data, list(a = 0, b = 99))
```

### 6. `separate()`
Divide una columna en múltiples columnas según un separador específico.

### 7. `separate_wider_delim()`
Divide una columna en varias columnas según un delimitador específico.

### 8. `separate_longer_delim()`
Expande una columna dividiendo su contenido en múltiples filas basadas en un delimitador específico.

### 9. `unite()`
Combina varias columnas en una sola.

### 10. `drop_na()`
Elimina las filas que contienen valores faltantes.

### 11. `fill()`
Rellena valores faltantes hacia adelante o hacia atrás.

## Nested Data en tidyr

`tidyr` permite trabajar con datos anidados (nested data), agrupando datos dentro de listas para un análisis estructurado.

**Funciones clave:**
- `nest()`: Agrupa columnas en una lista anidada.
- `unnest()`: Expande columnas anidadas de nuevo en filas.

**Ejemplo:**
```r
data <- data.frame(grupo = c("A", "B", "A"), valor = c(10, 15, 20))
data_nested <- nest(data, data = c(valor))

data_unnested <- unnest(data_nested, cols = c(data))
```

## Instalación

Para instalar `tidyr`, se puede utilizar el siguiente comando en R:

```r
install.packages("tidyr")
```

O si se desea instalar todo el conjunto de paquetes del tidyverse:

```r
install.packages("tidyverse")
```

## Casos de uso

- **Preparación de datos para machine learning:** Asegurar que los datos estén en el formato adecuado antes del modelado.
- **Análisis exploratorio de datos (EDA):** Reestructurar y limpiar datos para facilitar su exploración.
- **Generación de reportes:** Formatear datos para visualización y presentación.

## Referencias
- [Cheat sheet de tidyr](https://github.com/pgarmenteros/UNIR-grupo11/blob/Adrian/Librer%C3%ADas/Tidyr/tidyr.pdf)
- [Repositorio github de tidyr](https://github.com/tidyverse/tidyr)

## Conclusión

`tidyr` es una herramienta poderosa para la limpieza y reestructuración de datos en R. Su integración con el resto del ecosistema `tidyverse` la hace indispensable para analistas y científicos de datos que trabajan con datos tabulares de forma eficiente y reproducible.


