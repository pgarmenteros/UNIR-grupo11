# Conflicted
## Introducción
El paquete conflicted en R es una herramienta diseñada para ayudarte a manejar conflictos entre funciones con el mismo nombre que provienen de diferentes paquetes. En R, cuando cargas varios paquetes en un entorno, es común que dos o más de ellos contengan funciones con nombres idénticos, lo que puede llevar a resultados inesperados si no se tiene cuidado.

### Funcionalidad principal

Cuando hay un conflicto de nombres de funciones, R por defecto usa la función del último paquete cargado (el que aparece más arriba en la jerarquía de búsqueda). Sin embargo, esto puede ser confuso y llevar a errores. conflicted obliga a que los conflictos sean explícitos y que tú elijas qué función usar.

### ¿Cómo funciona?

1. **Detección de conflictos**: El paquete identifica cuando hay un conflicto en el entorno global debido a funciones con nombres idénticos.
2. **Errores claros**: Si intentas usar una función que tiene un conflicto, **conflicted** genera un error en lugar de asumir qué versión de la función usar.
3. **Soluciones explícitas**: Puedes resolver el conflicto especificando cuál función prefieres, usando la notación paquete::función. Por ejemplo:

```R
dplyr::filter(data, condition)
stats::filter(signal, filter)
````

### Ejemplo básico

```R
library(conflicted)
library(dplyr)
library(stats)

# Si intentas usar **"filter"** sin especificar el paquete, **conflicted** mostrará un error
filter(data, condition) # Error: filter es ambiguo.

# Solución: especificar el paquete
dplyr::filter(data, condition)
```

### Ventajas
- Hace tu código más claro y explícito.
- Reduce el riesgo de usar funciones incorrectas.
- Ayuda a depurar conflictos entre paquetes.

---

### Aplicaciones de conflicted en bioinformática

El paquete **conflicted** puede ser especialmente útil en bioinformática porque esta disciplina a menudo implica trabajar con múltiples paquetes que pueden tener funciones con nombres similares o idénticos. Esto ocurre, por ejemplo, al usar herramientas populares como **dplyr**, **tidyr**, **Bioconductor**, o paquetes específicos para análisis genómico, proteómico o transcriptómico. Aquí hay algunas aplicaciones concretas en bioinformática:

**1. Análisis de datos genómicos**
En proyectos de bioinformática, es común trabajar con paquetes como **GenomicRanges**, **DESeq2**, **edgeR**, y **dplyr**, donde funciones con nombres comunes como **filter** o **select** pueden entrar en conflicto. **conflicted** asegura que no uses accidentalmente la función incorrecta.

Ejemplo:
- El paquete **dplyr** tiene una función **select** para elegir columnas en un data.frame.
- El paquete **GenomicRanges** también tiene una función **select** para manejar datos genómicos.

```R
library(conflicted)
library(dplyr)
library(GenomicRanges)

# Conflicted detectará el conflicto entre dplyr::select y GenomicRanges::select
select(my_data) 
# Error: La función select es ambigua.

# Resolviendo explícitamente
dplyr::select(my_data, gene, expression)
GenomicRanges::select(granges_object, seqnames)
```

**2. Procesamiento de datos transcriptómicos**
En análisis de RNA-seq, es habitual trabajar con datos tabulares y herramientas estadísticas. Por ejemplo, se suelen combinar **DESeq2**, **edgeR**, y **dplyr**, lo que puede provocar conflictos con funciones como **filter**.

Ejemplo:
- Filtrado de genes según expresión diferencial:

```R
library(conflicted)
library(dplyr)
library(DESeq2)

# Detecta el conflicto entre dplyr::filter y stats::filter
filter(de_data, pvalue < 0.05)
# Error: La función filter es ambigua.

# Resolución explícita
dplyr::filter(de_data, pvalue < 0.05)
```

**3. Visualización y manipulación de datos**
Paquetes como **ggplot2**, **plotly**, **ComplexHeatmap**, y herramientas de manipulación como **reshape2** o **tidyr** pueden generar conflictos en funciones como **spread**, **gather**, o **plot**.

Ejemplo:
- Evitando conflictos entre funciones para reformatear datos.

```R
library(conflicted)
library(tidyr)
library(reshape2)

# Detecta conflicto entre tidyr::spread y reshape2::spread
spread(data, key = condition, value = expression)
# Error: La función spread es ambigua.

# Resolución explícita
tidyr::spread(data, key = condition, value = expression)
```

**4. Integración de datos multi-ómicos**
Al trabajar con datos de diferentes tipos (genómicos, transcriptómicos, epigenómicos, etc.), se combinan paquetes como **Bioconductor**, **limma**, y **dplyr**, lo que hace que **conflicted** sea útil para evitar confusiones al realizar análisis complejos.

Ejemplo:

```R
library(conflicted)
library(limma)
library(dplyr)

# Identifica conflicto entre dplyr::mutate y limma::mutate
mutate(data, logFC = log2(fold_change))
# Error: La función mutate es ambigua.

# Resolviendo conflictos
dplyr::mutate(data, logFC = log2(fold_change))
```

## Ventajas de usar conflicted en bioinformática
- **Evitar errores críticos**: En análisis biológicos, usar la función equivocada puede cambiar los resultados y llevar a conclusiones incorrectas.
- **Mejor colaboración**: Cuando trabajas en equipos, el código explícito es más fácil de entender y depurar.
- **Código reproducible**: Hacer que las elecciones de funciones sean claras ayuda a mantener la reproducibilidad, especialmente en entornos complejos con múltiples dependencias.
