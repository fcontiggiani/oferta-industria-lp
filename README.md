# Simulador de la oferta de largo plazo de la industria

Simulador interactivo, en HTML/JavaScript autocontenido, para la derivación gráfica y numérica de la curva de oferta de largo plazo de una industria competitiva, a partir de una tecnología Cobb-Douglas de rendimientos a escala generalizados y de un mecanismo explícito de respuesta de los precios de los factores al número de firmas. Desarrollado como material didáctico para un curso de Microeconomía Intermedia de nivel universitario (Bloque 3 — Estructuras de mercado; corresponde a Pindyck & Rubinfeld, *Microeconomía*, cap. 8.8).

## Contenido

El archivo `oferta_largo_plazo_industria.html` contiene la totalidad del simulador: marcado, estilos y lógica en un único documento, sin dependencias externas más allá de MathJax (cargado desde CDN, únicamente para el renderizado de las ecuaciones del bloque desplegable). No requiere proceso de compilación ni instalación de paquetes: basta con abrirlo en cualquier navegador moderno con JavaScript habilitado.

## Modelo económico

**Tecnología de la firma.** Cada una de las *n* firmas simétricas de la industria produce con una función Cobb-Douglas de rendimientos a escala libres, $q=K^\alpha L^\beta$, con $\alpha,\beta>0$ ajustables de forma independiente. El grado de homogeneidad $\rho=\alpha+\beta$ determina el régimen de la tecnología (constante, creciente o decreciente), indicado en pantalla mediante una insignia de color. A partir de la condición de tangencia de la minimización de costos se deriva la función de costo de largo plazo $C(w,r,q)=\kappa(w,r)\,q^{1/\rho}$, a la que se añade un costo fijo mínimo para generar una curva de costo medio en forma de U con una escala mínima eficiente interior, incluso cuando $\rho\neq 1$ dejaría, en ausencia de ese costo fijo, un costo medio monótono. Cuando $\rho>1$ (rendimientos crecientes a escala) el simulador señala explícitamente, mediante una advertencia visible, que el equilibrio de beneficio nulo con firmas de tamaño finito no está bien definido en sentido estricto bajo precios paramétricos, y que el resultado mostrado es una aproximación numérica sobre el dominio graficado.

**Precios de los factores endógenos al tamaño de la industria.** El mecanismo central del modelo —y la generalización explícita de la sección 8.8 de Pindyck & Rubinfeld— es $w(n)=w_0(n/n_0)^\varepsilon$ y $r(n)=r_0(n/n_0)^\varepsilon$, donde $\varepsilon$ es una elasticidad ajustable por el usuario. El signo de $\varepsilon$ reproduce la tricotomía clásica de industrias: $\varepsilon=0$ corresponde a una industria de costo constante (oferta de largo plazo horizontal), $\varepsilon>0$ a una industria de costo creciente (oferta con pendiente positiva, por presión al alza sobre los precios de los factores a medida que entran firmas) y $\varepsilon<0$ a una industria de costo decreciente (oferta con pendiente negativa, por economías externas a la firma pero internas a la industria). Esta dependencia es conceptualmente independiente del grado de homogeneidad $\rho$ de la tecnología: la pendiente de la oferta de largo plazo está gobernada por $\varepsilon$ (equilibrio del mercado de factores), no por $\rho$ (tecnología de la firma), y el simulador permite disociar ambas dimensiones moviendo cada control por separado.

**Equilibrio y curva de oferta de largo plazo.** Para cada número de firmas *n*, el precio de equilibrio de beneficio nulo es $P^*(n)=CMeL_{\min}(w(n),r(n))$ y la cantidad de equilibrio de la industria es $Q^*(n)=n\cdot q^{ME}(n)$. La curva de oferta de largo plazo $S_L$ es el lugar geométrico $\{(Q^*(n),P^*(n)):n\in\mathbb{N}\}$, trazado en un panel dedicado mediante un barrido numérico sobre *n* (hasta 500 firmas, con muestreo adaptativo para mantener el trazado ágil en todo el rango).

**Mercado y distinción corto plazo / largo plazo.** La demanda se modela como una función lineal inversa, $Q^D(P)=a-bP$. El simulador distingue y marca explícitamente dos puntos distintos en el panel de mercado: la intersección efectiva de corto plazo entre la demanda y la oferta agregada de las *n* firmas dadas (que responde a los parámetros de demanda *a* y *b*), y el equilibrio de largo plazo de beneficio nulo (que depende únicamente de la tecnología y de los precios de los factores, y es invariante ante desplazamientos de la demanda dado *n*). La distancia entre ambos puntos ilustra el incentivo a la entrada o salida de firmas que, en el equilibrio de largo plazo pleno, se resuelve ajustando *n* hasta que ambos coincidan.

## Características de la interfaz

- Controles deslizantes agrupados en tres paneles superiores: tecnología de la firma (α, β), precios de los factores y su respuesta a la entrada (w₀, r₀, ε), y número de firmas y mercado (n, a, b).
- Panel de resultados numéricos con el grado de homogeneidad ρ, los precios de factores vigentes, la escala mínima eficiente, el costo medio de largo plazo mínimo, la cantidad de equilibrio de la industria y el régimen de la oferta de largo plazo resultante.
- Tres paneles gráficos en canvas: (i) costo medio y marginal de largo plazo de la firma representativa, con las curvas correspondientes al número de firmas de referencia (n₀) superpuestas en gris punteado junto a las del número de firmas vigente, replicando el análisis "antes/después" de las figuras 8.16 y 8.17 de Pindyck & Rubinfeld; (ii) equilibrio de mercado, con la demanda, la oferta de corto plazo agregada y ambos puntos de equilibrio (corto y largo plazo) diferenciados; (iii) la curva de oferta de largo plazo S_L propiamente dicha, resultante del barrido sobre el número de firmas.
- Botón "Fijar como referencia" en el panel de mercado: congela una fotografía completa de los parámetros vigentes (tecnología, factores, número de firmas y demanda) y superpone, en gris punteado, la demanda, la oferta y ambos equilibrios de ese estado sobre el panel, permitiendo contrastar visualmente el efecto de un cambio posterior en cualquier parámetro (un shock de demanda, una entrada de firmas, un cambio en la elasticidad ε, etc.). Un botón contiguo permite retirar la referencia fijada.
- Bloque "Estructura formal del modelo" desplegable (con marcado `<details>`), que contiene la derivación completa: la tecnología, la minimización de costos, el costo medio y marginal de largo plazo, el mecanismo de precios de factores endógenos, la condición de equilibrio de beneficio nulo y la relación formal entre la pendiente de S_L y el signo de ε, con las ecuaciones renderizadas mediante MathJax.
- Alternancia entre tema claro y tema oscuro, con detección de la preferencia del sistema operativo como valor por defecto y persistencia de la elección explícita del usuario.
- Diseño responsive con los paneles de parámetros en fila superior y los gráficos a ancho completo.

## Uso local

Clonar o descargar este repositorio y abrir `oferta_largo_plazo_industria.html` directamente en el navegador. No se requiere servidor ni conexión a internet una vez descargado el archivo, salvo para el renderizado de las ecuaciones del bloque desplegable, que depende de MathJax servido desde CDN.

## Publicación en GitHub Pages

Este repositorio puede publicarse como sitio estático mediante GitHub Pages para obtener un enlace público permanente, apto para compartir con el estudiantado o incrustar en un entorno virtual de aprendizaje (por ejemplo, Moodle):

1. En **Settings → Pages**, seleccionar como fuente la rama `main` y la carpeta raíz (`/`).
2. Guardar los cambios y aguardar a que GitHub Pages compile el sitio.
3. El simulador quedará disponible en:

   ```
   https://<usuario>.github.io/<repositorio>/oferta_largo_plazo_industria.html
   ```

Toda actualización posterior del archivo se refleja automáticamente en esa misma dirección al subir la nueva versión al repositorio.

## Licencia y uso

Material desarrollado con fines exclusivamente didácticos. Los valores numéricos de ejemplo son ilustrativos salvo que se indique explícitamente lo contrario. Se autoriza su uso, adaptación y redistribución con fines educativos, citando la fuente.
