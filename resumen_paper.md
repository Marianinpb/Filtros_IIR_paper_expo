# Resumen del Paper: Optimal Design of Digital IIR Filters Using Robust Group Search Optimization

## 1. Contexto y Motivación
El diseño de filtros digitales IIR (Infinite Impulse Response) es un problema de optimización multiobjetivo sumamente complejo. Aunque existen métodos de transformación (como la transformación bilineal) que mapean filtros analógicos al dominio digital, estos introducen distorsiones (warping effects) en altas frecuencias.

Por ello, el enfoque directo de **optimización numérica de los coeficientes** es preferido, minimizando errores como la norma $L_p$ y los ripples de la banda de paso y rechazo.
Recientemente, los algoritmos bioinspirados como **GSO (Group Search Optimization)** han ganado popularidad; sin embargo, en su forma original, GSO tiende a quedar atrapado en óptimos locales debido a que depende de un único "productor" (producer) para guiar la exploración del resto de la población ("scroungers"). 

El paper propone resolver esto introduciendo **Robust-GSO (R-GSO)**, el cual integra el **Método de Taguchi** en el proceso de GSO para seleccionar un productor óptimo a partir de tres candidatos, garantizando una búsqueda global robusta y un escape eficiente de mínimos locales.

## 2. Formulación Matemática del Problema

El filtro digital IIR en cascada se representa con la función de transferencia:

$$ H(\omega, x) = \alpha \gamma \left( \prod_{i=1}^M \frac{1 + a_i e^{-j\omega}}{1 + b_i e^{-j\omega}} \right) \left( \prod_{k=1}^N \frac{1 + c_{1k} e^{-j\omega} + c_{2k} e^{-2j\omega}}{1 + d_{1k} e^{-j\omega} + d_{2k} e^{-2j\omega}} \right) $$

Donde el vector $x$ contiene todos los coeficientes a optimizar (polos y ceros) y $\alpha$ es una constante de normalización.

### Función Objetivo (Minimización)
Para evaluar el desempeño del filtro, se diseña una función de costo $f(x)$ que unifica cuatro criterios en conflicto:
$$ \min_x f(x) = \min_x \left[ v_1 E^1_M(x) + v_2 E^2_M(x) + v_3 \delta_1(x) + v_4 \delta_2(x) \right] $$

- $E^1_M(x)$: Error de la norma $L_1$ (magnitud absoluta del error).
- $E^2_M(x)$: Error de la norma $L_2$ (error cuadrático).
- $\delta_1(x)$: Magnitud del ripple en la banda de paso.
- $\delta_2(x)$: Magnitud del ripple en la banda de rechazo.
- $v_1, v_2, v_3, v_4$: Pesos ponderados definidos por el diseñador.

### Restricciones de Estabilidad
Para que el filtro IIR sea estable, sus polos deben ubicarse dentro del círculo unitario del plano $Z$, lo que se impone mediante inecuaciones estrictas sobre los coeficientes $b_i$, $d_{1k}$, y $d_{2k}$:
$$ 1 + b_i \ge 0, \quad 1 - b_i \ge 0 $$
$$ 1 - d_{2k} \ge 0, \quad 1 + d_{1k} + d_{2k} \ge 0, \quad 1 - d_{1k} + d_{2k} \ge 0 $$

## 3. Integración del Método de Taguchi (Algoritmo R-GSO)

En lugar de un solo productor, **R-GSO selecciona tres productores** en cada iteración: el de mejor fitness ($X_{p1}$), el segundo mejor ($X_{p2}$) y un miembro aleatorio del grupo ($X_{p3}$), para mantener diversidad.

Se emplean **arreglos ortogonales de Taguchi** (ej. $L_8(2^7)$ para 7 dimensiones) para cruzar y evaluar las combinaciones de estos productores de forma altamente eficiente, limitando la explosión combinatoria.
Para determinar qué nivel de cada factor contribuye más a la estabilidad de la búsqueda, se utiliza la **relación Señal/Ruido (Robust Response Value)**:

$$ E_{fj} = -10 \cdot \log \left( \frac{J_{i(avg)}^2}{J_{Mavg}^2} + \frac{J_{i(std)}^2}{J_{Mstd}^2} \right), \quad j=1, 2 $$

Este criterio evalúa no solo el fitness absoluto (promedio $J_{avg}$), sino también la desviación estándar ($J_{std}$), favoreciendo regiones del espacio de búsqueda que son consistentemente buenas (robustas). El cruce que sobrevive se convierte en el nuevo óptimo para guiar al enjambre.

## 4. Resultados Experimentales

El R-GSO se probó en el diseño de cuatro tipos de filtros: Pasa-bajas (LP), Pasa-altas (HP), Pasa-banda (BP) y Rechaza-banda (BS). Sus métricas se compararon contra el GSO original y contra un algoritmo genético híbrido (HTGA).

- **Fitness Final:** R-GSO obtuvo consistentemente el valor de costo $f(x)$ más bajo frente a HTGA y GSO. En HP, demostró su capacidad para escapar de un óptimo local temprano.
- **Velocidad de Convergencia:** R-GSO convergió mucho más rápido y de manera más estable que el GSO estándar, mostrando gráficas de convergencia precipitadas en las primeras 150-300 iteraciones.
- **Costo Computacional:** La cantidad de evaluaciones de la función objetivo para R-GSO fue significativamente menor que en HTGA (72,500 vs 130,000 en LP/HP), gracias a la eficiencia de los arreglos ortogonales de Taguchi.

## 5. Conclusiones
El enfoque propuesto R-GSO supera con creces las limitaciones inherentes a los algoritmos basados en grupos (como GSO tradicional), al formalizar estadísticamente la búsqueda del productor óptimo. Para el problema altamente no lineal y restringido del diseño de filtros IIR, su rigor se traduce en filtros que se ajustan mejor a la respuesta ideal con menor tiempo de simulación.
