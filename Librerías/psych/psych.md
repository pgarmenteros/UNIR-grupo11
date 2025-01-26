# Psych
## Guía completa paquete psych

# Introducción
El paquete psych en R es una herramienta poderosa y multifacética diseñada para realizar análisis estadísticos complejos, con un enfoque especial en psicometría y ciencias del comportamiento. Desde análisis factorial hasta estadísticas descriptivas avanzadas, psych se destaca por su facilidad de uso y la amplia gama de funciones que ofrece para analizar y comprender datos.

Este paquete se convierte en una opción esencial para investigadores, académicos y estudiantes que desean explorar patrones subyacentes en sus datos, construir modelos psicométricos y generar estadísticas descriptivas detalladas.

---

# ¿Porque usar psych?

El paquete psych se ha ganado un lugar destacado en la comunidad estadística y psicométrica debido a su:

1. **Versatilidad**: Compatible con una amplia gama de análisis, desde descripciones básicas hasta modelos complejos.
2. **Facilidad de uso**: Sintaxis clara y funciones intuitivas que facilitan el aprendizaje y aplicación.
3. **Fuerza psicométrica**: Diseñado específicamente para el análisis de cuestionarios, escalas y pruebas psicológicas.
4. **Documentación extensa**: Soporte completo para cada función, con ejemplos claros y detallados.
5. **Gráficos avanzados**: Genera gráficos para representar resultados de manera clara y visualmente atractiva.

---

# Aplicaciones de psych en psciometría y estadística

**Análisis Factorial**
- Exploratorio (EFA): Descubre las estructuras subyacentes en tus datos.
- Confirmatorio (en combinación con otros paquetes): Valida estructuras propuestas.
- Rotaciones: Incluye rotaciones ortogonales y oblicuas.

**Estadísticas Descriptivas**
Genera estadísticas descriptivas detalladas:
- Media, mediana y moda.
- Desviación estándar y varianza.
- Asimetría y curtosis.

**Análisis de Fiabilidad**
- Cálculo del coeficiente alpha de Cronbach.
- Análisis de consistencia interna.
- Creación de escalas compuestas basadas en ítems.

**Análisis de Correlaciones**
- Correlaciones simples y parciales.
- Matrices de correlación con significancia estadística.
- Visualización de correlaciones con diagramas circulares o mapas de calor.

**Análisis Multivariante**
- Componentes principales (PCA).
- Escalamiento multidimensional (MDS).
- Clustering jerárquico.

**Aplicaciones Específicas**
- Diseño y evaluación de cuestionarios.
- Estudios longitudinales y transversales.
- Creación de modelos estructurales preliminares.

---
# Instalación y Uso

Instalar y cargar el paquete **psych** es simple:
```R
install.packages("psych")
library(psych)
```
Una vez cargado, se puede comenzar a explorar sus funciones con datos propios o datasets incluidos en R.

---

# Principales Funciones del Paquete psych

A continuación, exploraremos las funciones más relevantes del paquete psych, con descripciones detalladas y ejemplos prácticos:

**describe()**
Obtiene estadísticas descriptivas detalladas de un conjunto de datos o una variable.
```R
ibrary(psych)
data <- mtcars

describe(data)
```
**Salida**
- Media, desviación estándar, mínimos y máximos.
- Valores de asimetría y curtosis.

**pairs.panels()**
Crea paneles de gráficos que incluyen histogramas, diagramas de dispersión y correlaciones.
```R
pairs.panels(data)
```
**Características**
- Histograma para cada variable.
- Correlaciones con valores p.
- Gráficos de dispersión con ajuste lineal.

**alpha()**
Evalúa la consistencia interna de una escala mediante el coeficiente alpha de Cronbach.
```R
alpha(scale_data)
```
**Parámetros importantes:**
- **check.keys**: Detecta ítems invertidos.
- **n.iter**: Realiza bootstrapping para calcular intervalos de confianza.

**fa()**
Realiza análisis factorial exploratorio con diversas opciones de extracción y rotación.
```R
fa(data, nfactors = 3, rotate = "oblimin")
```
**Opciones destacadas:**
- Métodos de extracción: **minres**, **ml**, **pa**.
- Rotaciones: **varimax**, **promax**, **oblimin**.

**omega()**
Realiza un análisis factorial jerárquico, incluyendo el coeficiente omega.
```R
omega(data)
```
**¿Por qué usar omega?**
- Mide fiabilidad jerárquica.
- Identifica factores generales y específicos.

**corPlot()**
Genera mapas de calor para matrices de correlación.
```R
cor_matrix <- cor(data)
corPlot(cor_matrix)
```
**Características destacadas:**
- Gradientes de color personalizables.
- Opciones para ordenar variables según dendrogramas.

---

# Caso de Estudio
**Diseño de Cuestionarios Genómicos**
**Objetivo**:  Crear un cuestionario genómico con alta fiabilidad para medir variables relacionadas con predisposiciones genéticas a enfermedades.
Primero, vamos a generar un conjunto de datos simulados que representan respuestas genómicas a diferentes estímulos biológicos. Posteriormente, evaluaremos su consistencia interna utilizando el coeficiente alpha de Cronbach y optimizaremos el cuestionario eliminando ítems problemáticos para mejorar la fiabilidad de las escalas que miden constructos genómicos específicos.
```R
set.seed(42)
genes_data <- data.frame(
  Gene1 = rnorm(100, mean = 3, sd = 1),
  Gene2 = rnorm(100, mean = 3, sd = 1.2),
  Gene3 = rnorm(100, mean = 3, sd = 0.8),
  Gene4 = rnorm(100, mean = 3, sd = 1.5)
)

# Evaluar fiabilidad inicial
alpha_result <- alpha(genes_data)
print(alpha_result)
```
**Optimización del Cuestionario**
```R
# Eliminar ítems con baja correlación
optimized_genes <- genes_data[, -which.min(alpha_result$item.stats$r.drop)]
alpha(optimized_genes)
```
En este ejemplo, podemos identificar genes con baja correlación con el constructo de interés y ajustamos el cuestionario para mejorar la consistencia interna. Este enfoque es clave para garantizar que el cuestionario mide de manera confiable las predisposiciones genéticas deseadas.

**Análisis Factorial Exploratorio en Genómica**
**Objetivo**: Identificar factores subyacentes en datos genómicos.
Utilizaremos el método de mínimos cuadrados ("minres") y una rotación oblicua ("oblimin") para entender mejor las interacciones genéticas y su contribución a ciertos rasgos o enfermedades.
```R
set.seed(42)
genomic_data <- data.frame(
  Factor1_Gene1 = rnorm(100, mean = 5, sd = 1),
  Factor1_Gene2 = rnorm(100, mean = 5, sd = 1.1),
  Factor2_Gene1 = rnorm(100, mean = 3, sd = 0.9),
  Factor2_Gene2 = rnorm(100, mean = 3, sd = 1)
)

# Análisis factorial exploratorio
fa_result <- fa(genomic_data, nfactors = 2, rotate = "oblimin")
print(fa_result)
```
Este análisis ayuda a identificar qué genes están agrupados bajo factores comunes y cómo estos pueden estar implicados en rasgos biológicos similares, proporcionando una base para la interpretación genómica de los datos.


# Conclusión
El paquete **psych** es una plataforma integral para el análisis psicométrico y de datos complejos. Su facilidad de uso y potentes funciones lo convierten en un recurso indispensable para investigadores en ciencias del comportamiento.

Con **psych**, no solo se analizan datos, sino que se obtiene una comprensión profunda y visualmente atractiva de ellos.
