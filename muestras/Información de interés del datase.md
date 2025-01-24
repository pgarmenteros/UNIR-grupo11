# Información de interés del dataset

## Conceptos de expresión de genes e interpretación de valores de AQ en la expresión de genes
La PCR en tiempo real o qPCR (quantitative PCR) es una técnica ampliamente utilizada para medir y comparar la expresión génica. Este método permite la cuantificación de la cantidad de ADN presente en una muestra en tiempo real, a medida que se amplifica. A continuación, se explica cómo se relacionan los conceptos mencionados con la qPCR:

- Ct (Threshold Cycle): En qPCR, el Ct es el ciclo en el que la cantidad de ADN amplificado supera un umbral detectable. Esto se utiliza para determinar la cantidad inicial de ADN en la muestra.
- DCt (Delta Ct): DCt se calcula restando el Ct del gen de referencia (normalizador, para este ejericio se ha utilizado el 18S rRNA o ARN ribosómico 18S, que es un gen comúnmente utilizado como control interno o gen normalizador debido a su expresión estable en diferentes tipos de células y condiciones experimentales) del Ct del gen de interés. Este valor nos permite normalizar la expresión del gen de interés respecto a un gen cuya expresión es constante.
- AQ (Absolute Quantification):  AQ se calcula como 2(-DCt), y representa la expresión del gen en una condición específica sin comparación directa con otra condición. Los valores de AQ en la expresión de genes representan cuánto están activos o produciendo proteínas esos genes en respuesta a diferentes condiciones o factores en un organismo. En otras palabras, estos valores indican la cantidad de actividad o expresión de cada gen en el contexto específico de estudio, como tratamientos médicos, tipos de tumor, o la extensión de la enfermedad. Cuando el valor de AQ es 0, significa que no se detecta ninguna expresión o actividad del gen en las muestras analizadas bajo las condiciones específicas del estudio. Esto puede indicar que el gen no está siendo trascrito o que su expresión es extremadamente baja y no detectable por los métodos utilizados.

## Genes relacionados con el metabolismo y la adipogénesis:
- **AQ_ADIPOQ:** Adiponectina, implicada en la regulación del metabolismo de la glucosa y la descomposición de ácidos grasos.
- **AQ_FASN:** Ácido graso sintasa, clave en la síntesis de ácidos grasos.
- **AQ_PPARG:** Peroxisome proliferator-activated receptor gamma, regula la adipogénesis.
- **AQ_SREBF1:** Sterol regulatory element-binding protein 1, regula la síntesis de lípidos.

## Genes relacionados con la respuesta inmune e inflamación:
- **AQ_CCL2 (MCP-1):** Quimiocina que atrae monocitos.
- **AQ_CCL5 (RANTES):** Quimiocina implicada en la respuesta inflamatoria.
- **AQ_CCR5:** Receptor de quimiocinas, implicado en la respuesta inmune.
- **AQ_CD274 (PD-L1):** Inhibe la respuesta inmune, relacionado con la evasión inmune en cáncer.
- **AQ_IFNG:** Interferón gamma, juega un papel crucial en la inmunidad innata y adaptativa.
- **AQ_IL10:** Interleucina 10, antiinflamatoria.
- **AQ_IL1B:** Interleucina 1 beta, proinflamatoria.
- **AQ_IL6:** Interleucina 6, proinflamatoria.
- **AQ_TNF:** Factor de necrosis tumoral alfa, proinflamatorio.

## Genes relacionados con la señalización celular y el ciclo celular:
- **AQ_JAK1:** Janus kinase 1, involucrado en la señalización de citoquinas.
- **AQ_JAK3:** Janus kinase 3, similar a JAK1, también en señalización de citoquinas.
- **AQ_STAT3:** Signal transducer and activator of transcription 3, mediador de señales de citoquinas.
- **AQ_MAPK1:** Mitogen-activated protein kinase 1, implicada en la proliferación y diferenciación celular.
- **AQ_NFE2L2:** Nuclear factor erythroid 2-related factor 2, regula la respuesta antioxidante.
- **AQ_NFKB1:** Nuclear factor kappa B subunit 1, regula la respuesta inmune y la inflamación.
- **AQ_FOXO3:** Forkhead box O3, regulador de la apoptosis y la resistencia al estrés.
- **AQ_FOXP3:** Forkhead box P3, regula el desarrollo y función de células T reguladoras.
- **AQ_PDCD1 (PD-1):** Programmed cell death protein 1, regula la inmunidad adaptativa.

## Genes relacionados con el estrés oxidativo y la apoptosis:
- **AQ_G6PD:** Glucose-6-phosphate dehydrogenase, protege contra el estrés oxidativo.
- **AQ_GPX1:** Glutathione peroxidase 1, protege contra el daño oxidativo.
- **AQ_SOD1:** Superoxide dismutase 1, elimina radicales libres.
- **AQ_NOS2 (iNOS):** Inducible nitric oxide synthase, produce óxido nítrico en respuesta a infecciones.
- **AQ_NOX5:** NADPH oxidase 5, produce especies reactivas de oxígeno.

## Genes relacionados con la inflamación y la señalización inflamatoria:
- **AQ_ALOX5:** Arachidonate 5-lipoxygenase, produce leucotrienos inflamatorios.
- **AQ_PTGS2 (COX-2):** Cyclooxygenase 2, produce prostaglandinas inflamatorias.
- **AQ_NLRP3:** NOD-like receptor family pyrin domain containing 3, componente del inflamasoma.
- **AQ_TLR3:** Toll-like receptor 3, detecta patógenos virales.
- **AQ_TLR4:** Toll-like receptor 4, detecta lipopolisacáridos bacterianos.

## Genes relacionados con el transporte y metabolismo energético:
- **AQ_CPT1A:** Carnitine palmitoyltransferase 1A, esencial para la oxidación de ácidos grasos.
- **AQ_GPD2:** Glycerol-3-phosphate dehydrogenase 2, involucrado en el metabolismo energético.
- **AQ_SLC2A4 (GLUT4):** Facilita el transporte de glucosa en células musculares y adiposas.

## Genes relacionados con el desarrollo y la diferenciación celular:
- **AQ_BMP2:** Bone morphogenetic protein 2, implicado en la formación ósea.
- **AQ_LIF:** Leukemia inhibitory factor, afecta la diferenciación celular y la respuesta inmune.

## Genes relacionados con la función y desarrollo de la célula inmunitaria:
- **AQ_CSF2:** Colony stimulating factor 2, estimula el crecimiento y diferenciación de células inmunitarias.
- **AQ_CXCR1:** Receptor para IL-8, implicado en la migración de neutrófilos.
