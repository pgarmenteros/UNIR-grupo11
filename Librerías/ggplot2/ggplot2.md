## Ggplot2
Ggplot2 es una libreria para crear gráficos. Proporcionando los datos e indicando como asignar variables se encarga de hacer la representación. Un grafico realizado en ggplot tiene al menos tres elementos: 

- **Datos** que queremos representar
- **Características estéticas (aesthetic mappings)** que describen cómo queremos que los datos se vean en el gráfico. Para más información podemos consultar la vignette (vignette(“ggplot2-specs”)). Como luego veremos, se introducen con la función aes() y se refieren a: 

  posición (en los ejes) 

  color exterior (color) 

  color de relleno (fill) 

  forma de puntos (shape) 

  tipo de línea (linetype) 

  tamaño (size) 

- **Objetos geométricos (Geom)** representan lo que vemos en un gráficos (puntos, líneas, etc.). Todo gráfico tiene, como mínimo, una geometría. La geometría determina el tipo de gráfico: 

  geom_point (para puntos) 

  geom_lines (para lineas) 

  geom_histogram (para histograma) 

  geom_boxplot (para boxplot) 

  geom_bar (para barras) 

  geom_smooth (líneas suavizadas) 

  geom_polygons (para polígonos en un mapa) 


Por tanto, para construir un gráfico con ggplot2 comenzamos con la siguiente estructura de código, usando + como nexo entre argumentos: 

**ggplot(datos, aes() ) + geom_tipo()**

A partir de esta estructura básica puede mejorarse la presentación de los gráficos introduciendo, por ejemplo, características estéticas en los objetos geométricos, rotulando los gráficos, etc. 

Otros elementos que conviene tener presente en un gráfico de ggplot2 son: 

Stat (Stat), transformaciones estadísticas para, generalmente, resumir datos (por ejemplo: contar frecuencias, número de intervalos en los histogramas, etc.). 

Escalas (Scale). Las escalas, por ejemplo, convierten datos en características estéticas (colores, etc.), crean leyendas… . 

Coordenadas (coord): sistema de coordenadas cartesianas, polares, proyecciones, etc. 

Faceting (Faceting), permite representar gráficos separados para subconjuntos de los datos originales. 
