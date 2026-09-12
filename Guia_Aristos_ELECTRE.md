# Áristos ELECTRE

Aplicación web autocontenida para aplicar el método de superación ELECTRE (variantes I y II) en decisiones multicriterio. Pensada para docencia de posgrado y para apoyar decisiones institucionales.

Autor: Mario Sergio Gómez Rueda. Correo: mgomezr1@gmail.com.
Uso de carácter académico. Cualquier otro uso se regirá por el derecho de la propiedad intelectual.

Versión 1.0.

## 1. Descripción general

Áristos ELECTRE ayuda a decidir entre varias alternativas evaluadas con varios criterios, cuando esos criterios no se pueden reducir a un único número sin perder información. A diferencia de los métodos que suman todo en un puntaje, ELECTRE compara las alternativas por pares y admite que algunas sean incomparables entre sí.

La aplicación ofrece dos variantes:

- ELECTRE I. Entrega el núcleo: el subconjunto de alternativas que ninguna otra supera. Sirve para seleccionar un grupo de opciones defendibles, no para ordenarlas.
- ELECTRE II. Produce un ranking completo de mejor a peor, mediante dos relaciones de superación, una fuerte y una débil.

Todo el cálculo ocurre en el navegador. Ningún dato sale del equipo. No se usan servidores, bases de datos ni estadísticas de visitas.

## 2. Cómo guardar el archivo

Guarde el archivo `index.html` en cualquier carpeta de su equipo. No necesita instalar nada. El archivo es autónomo: contiene la estructura, los estilos y toda la lógica.

La única dependencia externa es la biblioteca SheetJS, que se carga desde internet solo cuando usted exporta a Excel. Si trabaja sin conexión, todo funciona menos esa exportación puntual.

## 3. Cómo ejecutarlo

Tiene dos opciones:

- Doble clic sobre `index.html`. Se abre en su navegador predeterminado.
- Publicado en GitHub Pages. Suba el archivo a un repositorio y actívelo en Pages. En la sección 12 de esta guía se explica cómo.

Funciona en los navegadores actuales de escritorio y de dispositivos móviles.

## 4. Estructura de la interfaz

La aplicación se recorre en cinco pasos, señalados en el riel lateral. En pantallas pequeñas el riel se convierte en una barra superior.

- Paso 1. Configuración del modelo. Define el número de alternativas y criterios, la variante de ELECTRE, la normalización y los umbrales.
- Paso 2. Matriz de decisión. Nombra cada criterio, indica si se maximiza o se minimiza, asigna su peso y escribe el desempeño de cada alternativa.
- Paso 3. Resultados. Muestra las matrices de concordancia y discordancia, la relación de superación, el grafo y el resultado final.
- Paso 4. Sensibilidad y robustez. Responde a la pregunta central: qué tendría que cambiar para que la recomendación fuera otra.
- Paso 5. Exportación. Descarga el libro de Excel y el informe en PDF. Incluye además el modo de prueba con las pruebas automáticas.

### Ejemplo interactivo de la portada

La portada incluye un ejemplo con dos alternativas y tres criterios. Al mover los valores, la aplicación recalcula en vivo la concordancia y dice quién supera a quién. Su umbral es fijo, del sesenta por ciento, y sirve solo para enseñar el concepto. No depende de los umbrales que usted configure en el paso 1.

### Mensajes

Los mensajes de error indican qué ocurrió y cómo corregirlo, sin códigos técnicos. Las advertencias aparecen cuando un supuesto del método podría no cumplirse, por ejemplo cuando las escalas de los criterios no son comparables.

### Identidad visual

El fondo es un azul petróleo profundo. Dos colores tienen significado dentro del método: el ámbar señala la concordancia, la fuerza a favor de una superación, y el aqua señala la discordancia, la oposición en contra. Ambos tiñen las matrices y el grafo. Toda la paleta y las medidas están definidas como variables al inicio del bloque de estilos.

## 5. Exportación a Excel

El libro tiene seis hojas:

- Menú. Datos del análisis y un índice con enlaces a las demás hojas.
- Decisión. La matriz de decisión, el mínimo y el máximo por criterio, y la matriz normalizada. Los mínimos, máximos y la normalización están escritos como fórmulas reales de Excel, de modo que el estudiante puede seguir el cálculo celda por celda.
- Concordancia. El índice de concordancia entre cada par de alternativas.
- Discordancia. El índice de discordancia entre cada par.
- Núcleo ELECTRE I. La relación de superación entre cada par y el núcleo de alternativas no superadas.
- Ranking ELECTRE II. El ranking completo de mejor a peor.

Los porcentajes se muestran con dos decimales. Cuando los datos son de prueba, el nombre del archivo lleva el prefijo PRUEBA y la hoja Menú lo advierte.

## 6. Informe ejecutivo en PDF

El PDF se genera con código propio en JavaScript, sin bibliotecas, por lo que funciona sin conexión. El informe presenta los resultados de las dos variantes, sin importar cuál se haya elegido como principal. Su estructura es:

- Recomendación, con el resultado de ELECTRE I y el de ELECTRE II.
- Estructura del modelo, con la tabla de criterios, sentidos y pesos.
- Resultados principales, con la tabla del núcleo de ELECTRE I y la tabla del ranking de ELECTRE II.
- Robustez de la recomendación, si se ejecutó el análisis de sensibilidad.
- Nota metodológica.
- Referencias en APA 7.

Todas las páginas llevan una marca de agua diagonal translúcida y un pie con el nombre del aplicativo, su versión, el autor, la mención de uso académico, el correo y la numeración de páginas. Cuando los datos son de prueba, el informe lo advierte y el archivo lleva el prefijo PRUEBA.

## 7. Fundamento de cálculo

Sea una matriz de decisión con m alternativas y k criterios. El valor de la alternativa i en el criterio j se denota x(i, j). Cada criterio tiene un peso w(j) y un sentido, maximizar o minimizar.

### Normalización

Cada criterio se reescala al rango de cero a uno, donde uno es siempre lo mejor. Para un criterio de maximizar:

    r(i, j) = (x(i, j) − min_j) / (max_j − min_j)

Para un criterio de minimizar se invierte:

    r(i, j) = 1 − (x(i, j) − min_j) / (max_j − min_j)

Si el máximo y el mínimo coinciden, el criterio no distingue y se asigna uno a todas las alternativas.

### Índice de concordancia

La concordancia de a frente a b es la proporción del peso de los criterios en que a iguala o supera a b:

    C(a, b) = (suma de w(j) para los j donde r(a, j) >= r(b, j)) / (suma de todos los w(j))

Toma valores entre cero y uno. Más alto significa más apoyo a que a supere a b.

### Índice de discordancia global

La discordancia de a frente a b es la peor desventaja de a, dividida por el mayor rango de cualquier criterio:

    D(a, b) = (mayor valor de r(b, j) − r(a, j) sobre todos los j) / (mayor rango entre todos los criterios)

Más alto significa más oposición a que a supere a b.

### Relación de superación en ELECTRE I

La alternativa a supera a b cuando se cumplen dos condiciones a la vez:

    C(a, b) >= c*    y    D(a, b) <= d*

donde c* es el umbral de concordancia y d* el de discordancia. En el modo de veto por criterio, la segunda condición se sustituye por la ausencia de veto: a no supera a b si en algún criterio la desventaja de a, medida en las unidades propias de ese criterio, supera el umbral de veto v(j) de ese criterio.

### Umbrales recomendados

La aplicación ofrece una opción recomendada para fijar los umbrales, siguiendo la práctica clásica del método: c* se toma como el promedio de los elementos de la matriz de concordancia, y d* como el promedio de los elementos de la matriz de discordancia. En ambos casos el promedio se calcula sobre los elementos fuera de la diagonal. En el paso 2, una vez completa la matriz de decisión, el botón «Calcular umbrales recomendados» los aplica. Conviene después someterlos al análisis de sensibilidad del paso 4, porque siguen siendo valores de referencia y no constantes universales.

### Núcleo

El núcleo es el subconjunto de alternativas tal que ninguna alternativa de fuera del núcleo supera a las de dentro, y dentro del núcleo ninguna supera a otra de forma estricta. Se obtiene retirando de forma iterativa las alternativas que son superadas por alguna otra que permanece.

### ELECTRE II

Usa dos pares de umbrales. La superación fuerte se acepta cuando C(a, b) >= c1 y D(a, b) <= d1. La débil cuando C(a, b) >= c2 y D(a, b) <= d2, con c2 menor que c1 y d2 mayor que d1. A partir de esas relaciones se construyen dos ordenamientos, uno descendente y uno ascendente, y el ranking final promedia la posición de cada alternativa en ambos.

## 8. Explicación de las funciones

### Motor de cálculo

- `normalizarDecision`. Reescala la matriz según el sentido de cada criterio.
- `matrizConcordancia`. Calcula el índice de concordancia entre cada par.
- `matrizDiscordanciaGlobal`. Calcula el índice de discordancia global.
- `matrizVetoPorCriterio`. Determina, para el modo por criterio, dónde una desventaja excesiva impide la superación.
- `relacionSuperacionI`. Construye la matriz booleana de superación de ELECTRE I.
- `calcularNucleo`. Obtiene el núcleo a partir de la relación de superación.
- `electreI` y `electreII`. Ejecutan cada variante completa.
- `relacionesII` y `destilar`. Construyen las relaciones fuerte y débil y los preórdenes de ELECTRE II.

### Utilidades e interpretación

- `comoPorcentaje` y `conDecimales`. Dan formato a los números en español.
- `mostrarMensaje` y `actualizarOrigen`. Gestionan los avisos y la insignia de origen de los datos.

### Interfaz y resultados

- `aplicarConfiguracion`. Valida la configuración y construye las estructuras del modelo.
- `construirTablaCriterios` y `construirMatrizDecision`. Arman las tablas editables.
- `cargarDatosPrueba`. Genera datos ficticios reproducibles, marcados como prueba.
- `calcularYMostrar` y `renderizarResultados`. Ejecutan el cálculo y muestran los resultados.
- `grafoSuperacion`. Dibuja el grafo en SVG, con el núcleo en ámbar.

### Sensibilidad

- `ejecutarBarridoI`. Recalcula el núcleo para un rango de umbrales de concordancia.
- `ejecutarRobustezII`. Perturba los umbrales de ELECTRE II y mide con qué frecuencia cada alternativa queda primera.

### Exportación

- `crearHojaExcel`. Fábrica de hojas con soporte para celdas, fórmulas y enlaces.
- `excelHojaMenu`, `excelHojaDecision`, `excelHojaConcordancia`, `excelHojaDiscordancia`, `excelHojaResultado`. Construyen cada hoja.
- `DocumentoPDF`. Motor de PDF propio, sin bibliotecas.
- `generarInformePDF` y `exportarInformePDF`. Ensamblan y descargan el informe.

### Pruebas

- `PRUEBAS` y `ejecutarPruebas`. Batería de pruebas automáticas que se ejecutan desde la interfaz.

## 9. Ejemplo de uso

Considere tres proveedores evaluados en tres criterios, todos a maximizar, con pesos 0,5, 0,3 y 0,2.

| Alternativa | Criterio 1 | Criterio 2 | Criterio 3 |
| --- | --- | --- | --- |
| P1 | 6 | 5 | 4 |
| P2 | 9 | 8 | 7 |
| P3 | 5 | 9 | 6 |

Con normalización de mínimo a máximo, umbral de concordancia c* = 0,50 y umbral de discordancia d* = 0,60, el resultado verificado es:

- Matriz normalizada: P1 queda en 0,25, 0,00 y 0,00; P2 en 1,00, 0,75 y 1,00; P3 en 0,00, 1,00 y 0,67.
- Concordancia: C(P2, P1) = 1,00, C(P2, P3) = 0,70, C(P3, P1) = 0,50, C(P1, P3) = 0,50.
- Relación de superación: P2 supera a P1 y a P3; P3 supera a P1.
- Núcleo: P2.

La recomendación es P2, la única alternativa que ninguna otra supera. Este resultado se obtiene igual en la aplicación, en el libro de Excel al recalcular sus fórmulas y en el cálculo manual con las fórmulas de la sección 7.

## 10. Modo de prueba

La aplicación puede generar datos de prueba de distintos tamaños, siempre marcados como tales. Los archivos que exporte con esos datos llevan el prefijo PRUEBA y una advertencia dentro. La aplicación nunca presenta datos inventados como si fueran reales.

## 11. Verificación realizada

Antes de la entrega se ejecutó la aplicación en un navegador real y se comprobó lo siguiente:

- Las doce pruebas automáticas pasan.
- El motor de cálculo coincide, celda por celda, con un cálculo independiente hecho en Python.
- El libro de Excel, recalculado de forma independiente con LibreOffice, produce los mismos valores que la aplicación.
- El PDF abre sin errores y presenta la marca de agua y el pie de página en todas sus páginas.
- La página no se desplaza en sentido horizontal a cuatrocientos píxeles de ancho.
- No hay errores en la consola del navegador.

## 12. Publicación en GitHub Pages

1. Cree un repositorio en GitHub y suba el contenido del paquete: `index.html`, `README.md`, `LICENSE`, `CITATION.cff` y la carpeta `docs`.
2. En el repositorio, entre a Settings y luego a Pages.
3. En Source elija la rama principal y la carpeta raíz.
4. Guarde. En pocos minutos la aplicación quedará disponible en la dirección que GitHub indique.

## 13. Limitaciones

- Los umbrales de concordancia y discordancia no son constantes universales. Dependen del problema y de la actitud de quien decide. La aplicación sugiere valores de partida, pero no los presenta como referencias publicadas.
- La discordancia global supone que las escalas de los criterios son comparables. Cuando las unidades son muy distintas, conviene usar el modo de veto por criterio, más defendible.
- ELECTRE I no ordena las alternativas. Entrega un subconjunto. Esa es una característica del método, no una carencia de la aplicación.
- La destilación de ELECTRE II implementada es una versión didáctica orientada al grafo de superación. Es adecuada para la enseñanza y para casos de tamaño moderado; para estudios que exijan la formulación exacta de una variante específica, conviene contrastar con la fuente original.
- El ejemplo interactivo de la portada usa un umbral fijo con fines ilustrativos y no refleja la configuración del paso 1.

## 14. Referencias

Figueira, J., Mousseau, V., & Roy, B. (2016). ELECTRE methods. En S. Greco, M. Ehrgott, & J. Figueira (Eds.), Multiple Criteria Decision Analysis: State of the Art Surveys (2.ª ed., pp. 155-185). Springer.

Roy, B. (1968). Classement et choix en présence de points de vue multiples (la méthode ELECTRE). Revue Française d'Informatique et de Recherche Opérationnelle, 2(8), 57-75.

Roy, B. (1991). The outranking approach and the foundations of ELECTRE methods. Theory and Decision, 31(1), 49-73.

Roy, B., & Bouyssou, D. (1993). Aide multicritère à la décision: méthodes et cas. Economica.
