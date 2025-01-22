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
