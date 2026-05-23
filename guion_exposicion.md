# Guion de Exposición

**Título:** Optimal Design of Digital IIR Filters Using Robust Group Search Optimization
**Expositor:** Mariano Prado Berman
**Audiencia:** Profesor de maestría (Dr. en Física, exigente con el rigor matemático)

---

## Diapositiva 1: Título
**[Acción]** *Mostrar diapositiva de título. Esperar a que la audiencia preste atención.*
**[Narración]** "Buenos días, doctor. Hoy presentaré el análisis del artículo 'Optimal Design of Digital IIR Filters Using Robust Group Search Optimization'. Este trabajo aborda el complejo problema de diseñar filtros digitales IIR minimizando los errores de aproximación mediante la integración de un método heurístico de enjambre con el diseño estadístico experimental de Taguchi."

## Diapositiva 2: Contenido
**[Acción]** *Mostrar el índice general.*
**[Narración]** "La presentación está estructurada en cuatro partes. Comenzaremos con el contexto y la motivación del problema, pasaremos a la formulación matemática rigurosa del filtro y su función de costo, explicaremos el algoritmo propuesto R-GSO y cerraremos con los resultados y conclusiones."

## Diapositiva 3: Contexto y Motivación - El Problema del Diseño de Filtros IIR
**[Acción]** *Señalar los primeros dos puntos de la diapositiva.*
**[Narración]** "Como sabemos, los métodos clásicos de transformación como la transformación bilineal son útiles pero introducen un efecto indeseable de distorsión o 'warping' en las altas frecuencias. Por esta razón, el diseño óptimo suele formularse como un problema de optimización numérica directa sobre los coeficientes."
**[Acción]** *Enfatizar la propuesta.*
**[Narración]** "Los enfoques bioinspirados, como el Group Search Optimization (GSO), son efectivos pero convergen prematuramente a óptimos locales, al depender de un único vector guía o 'productor'. La solución propuesta en el artículo es el R-GSO, que introduce el Método de Taguchi para estructurar la selección del productor óptimo, garantizando una búsqueda global matemáticamente robusta."

## Diapositiva 3b: Algoritmo GSO – Metáfora de forrajeo y sus limitaciones
**[Acción]** *Explicar los roles en el enjambre y la vulnerabilidad de GSO.*
**[Narración]** "Para entender cómo opera esta búsqueda, imaginemos una población donde cada individuo es un vector de coeficientes del filtro. GSO asigna roles en cada iteración: el 'Productor', que tiene el mejor valor de la función de costo (fitness), explora localmente. Los 'Scroungers' (oportunistas) se desplazan hacia el productor copiando su comportamiento, mientras que los 'Rangers' (exploradores) se dispersan aleatoriamente para mantener diversidad. 
El problema estructural del GSO es que si el productor único queda atrapado en un mínimo local, todos los scroungers convergen allí, estancando el algoritmo. R-GSO soluciona esto construyendo un productor óptimo robusto a partir de tres candidatos."

## Diapositiva 4: Formulación Matemática - Función de Transferencia y Costo
**[Acción]** *Mostrar la función de transferencia y la función de costo.*
**[Narración]** "El filtro digital IIR se modela en su forma en cascada. Aquí observamos la función de transferencia $H(\omega, x)$ donde el vector de diseño $x$ contiene los coeficientes de las secciones de primer y segundo orden.
El objetivo es encontrar el vector $x$ que minimice la función de costo $f(x)$. Esta función está construida como una suma ponderada de cuatro componentes: el error de la norma $L_1$, el error cuadrático de la norma $L_2$, y las magnitudes de los ripples en las bandas de paso y rechazo. Las constantes $v_1$ a $v_4$ permiten ajustar el peso relativo de estos errores en el hiperespacio de soluciones."

## Diapositiva 5: Restricciones de Estabilidad
**[Acción]** *Mostrar las inecuaciones.*
**[Narración]** "Un filtro IIR diseñado numéricamente carece de utilidad si es inestable. Matemáticamente, esto exige que todos los polos de la función de transferencia residan estrictamente dentro del círculo unitario en el plano complejo $Z$. Esta condición de frontera impone que los coeficientes del denominador cumplan el sistema de inecuaciones lineales mostrado en pantalla. Esto convierte la optimización en un problema altamente restringido, reduciendo el espacio de soluciones factibles."

## Diapositiva 5b: Método de Taguchi – Diseño Robusto y Arreglos Ortogonales
**[Acción]** *Explicar el arreglo ortogonal y la relación Señal-Ruido (S/N).*
**[Narración]** "Antes de ver la integración, debemos entender el Método de Taguchi. Su objetivo en R-GSO es encontrar una combinación (productor) que rinda bien y tenga muy baja variabilidad (robustez). 
Para ello, consideramos a los coeficientes del filtro como 'factores', y tomamos sus valores en dos soluciones candidatas como los 'niveles' (1 y 2). Al usar un arreglo ortogonal, como el L8, evaluamos un número drásticamente reducido de combinaciones que, al estar balanceadas, nos permiten estimar el efecto de cada coeficiente por separado. 
En cada prueba añadimos perturbaciones controladas a partir de un tercer candidato, evaluamos la media y la variabilidad, y calculamos la Relación Señal-Ruido con la fórmula en pantalla. Así, para cada coeficiente, se elige el nivel que aporte mayor robustez, formando un vector final estadísticamente óptimo."

## Diapositiva 6: Integración de Taguchi en el ciclo de GSO (Algoritmo R-GSO)
**[Acción]** *Mostrar el diagrama de flujo o listado de pasos del algoritmo completo.*
**[Narración]** "Al fusionar ambas metodologías, el ciclo de R-GSO funciona de la siguiente manera:
1. Primero, evaluamos el costo de toda la población de vectores estables.
2. Segundo, elegimos tres productores: el mejor (Xp1), el segundo mejor (Xp2) y uno aleatorio (Xp3).
3. Tercero, aplicamos el Método de Taguchi usando Xp1 y Xp2 como niveles de los factores, y evaluamos la variabilidad usando Xp3 en el arreglo ortogonal. A partir de esto determinamos el nuevo vector productor óptimo.
4. Finalmente, actualizamos el productor a este nuevo vector, los scroungers se dirigen hacia él y los rangers continúan la exploración aleatoria. Este ciclo se repite hasta la convergencia, logrando saltar de los mínimos locales mediante cruzamientos altamente eficientes."

## Diapositiva 7: Resultados Experimentales
**[Acción]** *Mostrar los hallazgos experimentales.*
**[Narración]** "El modelo propuesto fue sometido a prueba evaluando filtros Pasa-bajas, Pasa-altas, Pasa-banda y Rechaza-banda. Al compararse frente al GSO clásico y frente al Algoritmo Genético de Taguchi Híbrido o HTGA, R-GSO reportó el menor valor absoluto en la función de costo en todos los casos. 
Adicionalmente, el esfuerzo computacional fue mucho menor. Mientras que el algoritmo genético requirió 130,000 evaluaciones de la función objetivo para converger en el filtro pasa-altas, R-GSO requirió aproximadamente 72,500 evaluaciones. Esto demuestra empíricamente la eficiencia de usar el método de Taguchi como motor de cruce."

## Diapositiva 8: Conclusiones
**[Acción]** *Cerrar la exposición con las conclusiones.*
**[Narración]** "En conclusión, el uso de arreglos ortogonales estadísticos para regular una metaheurística de enjambre resulta ser un abordaje matemáticamente sólido. R-GSO mitiga con éxito el principal defecto del GSO clásico que es la convergencia prematura. Como resultado, es posible diseñar filtros digitales IIR más exactos que satisfacen rigurosamente tanto las tolerancias de ripple como la condición de estabilidad de los polos.
Muchas gracias. Quedo a su disposición para responder a sus preguntas técnicas."
