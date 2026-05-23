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

## Diapositiva 4: Formulación Matemática - Función de Transferencia y Costo
**[Acción]** *Mostrar la función de transferencia y la función de costo.*
**[Narración]** "El filtro digital IIR se modela en su forma en cascada. Aquí observamos la función de transferencia $H(\omega, x)$ donde el vector de diseño $x$ contiene los coeficientes de las secciones de primer y segundo orden.
El objetivo es encontrar el vector $x$ que minimice la función de costo $f(x)$. Esta función está construida como una suma ponderada de cuatro componentes: el error de la norma $L_1$, el error cuadrático de la norma $L_2$, y las magnitudes de los ripples en las bandas de paso y rechazo. Las constantes $v_1$ a $v_4$ permiten ajustar el peso relativo de estos errores en el hiperespacio de soluciones."

## Diapositiva 5: Restricciones de Estabilidad
**[Acción]** *Mostrar las inecuaciones.*
**[Narración]** "Un filtro IIR diseñado numéricamente carece de utilidad si es inestable. Matemáticamente, esto exige que todos los polos de la función de transferencia residan estrictamente dentro del círculo unitario en el plano complejo $Z$. Esta condición de frontera impone que los coeficientes del denominador cumplan el sistema de inecuaciones lineales mostrado en pantalla. Esto convierte la optimización en un problema altamente restringido, reduciendo el espacio de soluciones factibles."

## Diapositiva 6: Algoritmo R-GSO (Integración de Taguchi)
**[Acción]** *Mostrar la explicación del algoritmo y la métrica de Taguchi.*
**[Narración]** "El verdadero aporte del R-GSO radica en cómo escapa de los óptimos locales. En lugar de un productor único, el algoritmo selecciona tres vectores base en cada iteración: el mejor, el segundo mejor y un vector de exploración estocástica. 
Para combinarlos, se emplean arreglos ortogonales de Taguchi. Estos arreglos permiten barrer el espacio combinatorio de manera probabilísticamente eficiente. El nivel óptimo de cada factor no se decide únicamente por el valor de costo, sino a través de esta relación Señal-a-Ruido $E_{fj}$. Al considerar la desviación estándar en el denominador logarítmico, la métrica de Taguchi prioriza configuraciones paramétricas que son tanto precisas como estructuralmente estables frente a perturbaciones."

## Diapositiva 7: Resultados Experimentales
**[Acción]** *Mostrar los hallazgos experimentales.*
**[Narración]** "El modelo propuesto fue sometido a prueba evaluando filtros Pasa-bajas, Pasa-altas, Pasa-banda y Rechaza-banda. Al compararse frente al GSO clásico y frente al Algoritmo Genético de Taguchi Híbrido o HTGA, R-GSO reportó el menor valor absoluto en la función de costo en todos los casos. 
Adicionalmente, el esfuerzo computacional fue mucho menor. Mientras que el algoritmo genético requirió 130,000 evaluaciones de la función objetivo para converger en el filtro pasa-altas, R-GSO requirió aproximadamente 72,500 evaluaciones. Esto demuestra empíricamente la eficiencia de usar el método de Taguchi como motor de cruce."

## Diapositiva 8: Conclusiones
**[Acción]** *Cerrar la exposición con las conclusiones.*
**[Narración]** "En conclusión, el uso de arreglos ortogonales estadísticos para regular una metaheurística de enjambre resulta ser un abordaje matemáticamente sólido. R-GSO mitiga con éxito el principal defecto del GSO clásico que es la convergencia prematura. Como resultado, es posible diseñar filtros digitales IIR más exactos que satisfacen rigurosamente tanto las tolerancias de ripple como la condición de estabilidad de los polos.
Muchas gracias. Quedo a su disposición para responder a sus preguntas técnicas."
