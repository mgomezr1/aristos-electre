# Áristos ELECTRE

Aplicación web autocontenida para aplicar el método de superación ELECTRE I en decisiones multicriterio. Pensada para docencia de posgrado y para apoyar decisiones institucionales, con énfasis en la transparencia y la trazabilidad de cada cálculo.

Autor: Mario Sergio Gómez Rueda. Correo: mgomezr1@gmail.com.
Uso de carácter académico. Cualquier otro uso se regirá por el derecho de la propiedad intelectual.

Versión 3.1.

## 1. Descripción general

Áristos ELECTRE ayuda a decidir entre varias alternativas evaluadas con varios criterios, cuando esos criterios no se pueden reducir a un único número sin perder información. A diferencia de los métodos que suman todo en un puntaje, ELECTRE compara las alternativas por pares y admite que algunas sean incomparables entre sí.

La aplicación implementa ELECTRE I, que entrega el núcleo: el subconjunto de alternativas con estabilidad interna, ninguna sobreclasifica a otra del núcleo, y dominancia externa, toda alternativa de fuera es sobreclasificada por alguna de dentro. Cuando el grafo de sobreclasificación contiene circuitos, se contraen antes de extraer el núcleo. ELECTRE I reduce el conjunto de opciones admisibles; no produce necesariamente un orden completo, y esa es una elección metodológica del método, no una carencia de la herramienta.

La versión 3.0 reorganiza la aplicación en torno a la trazabilidad. Cada etapa del cálculo se muestra en un acordeón, con auditorías «Ver cálculo» que exhiben cómo se obtiene cada índice de concordancia y de discordancia par por par. La precisión con que se muestran los números es configurable y afecta solo la presentación, nunca el cálculo interno, que siempre usa precisión completa.

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

- Paso 1. Configuración del modelo. Define el número de alternativas y criterios, la precisión con que se muestran los números y, si se desea, los umbrales de concordancia y de discordancia. Si los umbrales se dejan vacíos, la aplicación los calcula a partir de los datos.
- Paso 2. Matriz de decisión. Nombra cada criterio, indica si se maximiza o se minimiza, asigna su peso y escribe el desempeño de cada alternativa. Los pesos deben sumar 1, equivalente al 100 por ciento.
- Paso 3. Resultados. Presenta las trece etapas del método en acordeones: datos y pesos, concordancia, normalización por rango, ponderación, discordancia, umbrales, dominancias F, G y H, grafo de sobreclasificación y núcleo. Cada acordeón puede abrirse y cerrarse, y varias etapas incluyen la auditoría «Ver cálculo».
- Paso 4. Sensibilidad. Responde a la pregunta central: qué tendría que cambiar para que el resultado fuera otro. Ofrece deslizadores que recalculan en vivo la matriz de dominancia, el grafo y el núcleo, y un barrido del umbral de concordancia que señala el punto de quiebre.
- Paso 5. Exportación. Descarga el libro de Excel y el informe en PDF. Incluye además el modo de prueba con las pruebas automáticas.

### Precisión en pantalla

En el paso 1 se elige cuántos decimales se muestran: dos, tres, cuatro o seis. Esta elección afecta solo lo que se ve. Todos los cálculos internos, y todas las comparaciones contra los umbrales, se hacen con la precisión completa del navegador. Cambiar la precisión vuelve a dibujar los resultados sin recalcular nada.

### Ejemplo interactivo de la portada

La portada incluye un ejemplo con dos alternativas y tres criterios. Al mover los valores, la aplicación recalcula en vivo la concordancia y dice quién sobreclasifica a quién. Su umbral es fijo y sirve solo para enseñar el concepto. No depende de los umbrales que usted configure en el paso 1.

### Identidad visual

El fondo es un azul petróleo profundo. Dos colores tienen significado dentro del método: el ámbar señala la concordancia, la fuerza a favor de una sobreclasificación, y el aqua señala la discordancia, la oposición en contra. Ambos tiñen las matrices y el grafo. En el grafo y en el núcleo, el ámbar marca las alternativas que quedan dentro del núcleo. Toda la paleta y las medidas están definidas como variables al inicio del bloque de estilos.

## 5. Exportación a Excel

El libro tiene dieciséis hojas: una de menú y quince de contenido.

- Menú. Datos del análisis y un índice con enlaces a las demás hojas.
- Datos. Configuración del modelo: tamaño, umbrales y origen de los datos.
- Decisión. La matriz de decisión con el sentido de cada criterio.
- Pesos. El peso de cada criterio y su suma.
- Rangos. El mínimo, el máximo y el rango de cada criterio, escritos como fórmulas reales de Excel que referencian la hoja Decisión, de modo que el estudiante puede seguir el cálculo celda por celda.
- Normalizada. La matriz normalizada por rango, escrita como fórmulas de Excel que dividen la hoja Decisión entre el rango de cada criterio.
- Ponderada. La matriz normalizada y ponderada, escrita como fórmulas que multiplican la hoja Normalizada por los pesos. Las matrices de concordancia, discordancia y dominancia se exportan como resultados calculados en el aplicativo, con una nota que lo indica.
- Concordancia. El índice de concordancia entre cada par de alternativas.
- Discordancia. El índice de discordancia entre cada par.
- Umbrales. Los umbrales de concordancia y de discordancia adoptados, con la indicación de si se fijaron a mano o se calcularon.
- Dominancia F. La matriz de dominancia concordante.
- Dominancia G. La matriz de dominancia discordante.
- Dominancia H. La matriz de dominancia agregada.
- Sobreclasificación. La lista de relaciones i sobreclasifica a k.
- Núcleo. Las alternativas que quedan dentro y fuera del núcleo.
- Sensibilidad. El resultado del barrido de umbrales, si se ejecutó en la sesión.

Cuando los datos son de prueba, el nombre del archivo lleva el prefijo PRUEBA y la hoja Menú lo advierte.

## 6. Informe ejecutivo en PDF

El PDF se genera con código propio en JavaScript, sin bibliotecas, por lo que funciona sin conexión. Su estructura es:

1. Configuración, con la tabla de criterios, sentidos y pesos, y los umbrales adoptados.
2. Matriz de decisión.
3. Concordancia y discordancia.
4. Dominancia agregada H.
5. Grafo de sobreclasificación, dibujado dentro del propio PDF, con los nodos del núcleo en ámbar y los arcos con la dirección de cada sobreclasificación.
6. Núcleo.
7. Robustez, si se ejecutó el análisis de sensibilidad.
8. Nota metodológica, que explicita las convenciones de la implementación.
9. Referencias.

Todas las páginas llevan una marca de agua diagonal translúcida y un pie con el nombre del aplicativo, su versión, el autor, la mención de uso académico, el correo y la numeración de páginas. Cuando los datos son de prueba, el informe lo advierte y el archivo lleva el prefijo PRUEBA.

## 7. Fundamento de cálculo

Sea una matriz de decisión con m alternativas y k criterios. El valor de la alternativa i en el criterio j se denota x(i, j). Cada criterio tiene un peso w(j) y un sentido, maximizar o minimizar. Los pesos suman 1.

Las convenciones que siguen son decisiones de esta implementación. Son razonables y están documentadas, pero no son las únicas posibles dentro de la familia ELECTRE. Conviene interpretarlas en el contexto del problema y someterlas al análisis de sensibilidad.

### Rangos y normalización por rango

Para cada criterio se calcula su rango, es decir la diferencia entre el máximo y el mínimo observados:

    rango(j) = max_j menos min_j

La matriz se normaliza dividiendo cada valor por el rango de su criterio:

    r(i, j) = x(i, j) dividido por (max_j menos min_j)

Esta normalización por rango no reescala al intervalo de cero a uno ni resta el mínimo, y no invierte los criterios de minimizar. La dirección de cada criterio se respeta más adelante, al comparar las alternativas en la concordancia y en la discordancia.

### Ponderación

La matriz normalizada se pondera multiplicando cada valor por el peso de su criterio:

    v(i, j) = w(j) por r(i, j)

La matriz ponderada V es la base del cálculo de la discordancia.

### Índice de concordancia

La concordancia de i frente a k es la suma de los pesos de los criterios en que i es igual o mejor que k, respetando la dirección de cada criterio. Para un criterio de maximizar, i es igual o mejor si x(i, j) es mayor o igual que x(k, j); para uno de minimizar, si x(i, j) es menor o igual que x(k, j).

    C(i, k) = suma de w(j) para los j donde i es igual o mejor que k

El empate recibe el peso completo del criterio. Como los pesos suman 1, la concordancia queda entre cero y uno sin necesidad de dividir.

### Índice de discordancia

La discordancia de i frente a k se calcula sobre la matriz ponderada V. El numerador es la mayor diferencia absoluta entre i y k entre los criterios en que i es peor que k. El denominador es la mayor diferencia absoluta entre i y k en cualquier criterio.

    D(i, k) = numerador dividido por denominador

donde el numerador es la mayor diferencia absoluta entre v(i, j) y v(k, j) en los criterios en que i es peor que k, y el denominador es la mayor diferencia absoluta entre v(i, j) y v(k, j) en cualquier criterio. Si el denominador es cero, la discordancia es cero.

### Umbrales

Por defecto, el umbral de concordancia c* es el promedio de los elementos fuera de la diagonal de la matriz de concordancia, y el umbral de discordancia d* es el promedio de los elementos fuera de la diagonal de la matriz de discordancia. Son un punto de partida a partir de los datos, no constantes universales del método. Pueden fijarse a mano en el paso 1 y explorarse en el paso 4.

### Matrices de dominancia

A partir de los umbrales se construyen tres matrices booleanas:

    F(i, k) = 1 si C(i, k) es mayor o igual que c*
    G(i, k) = 1 si D(i, k) es menor o igual que d*
    H(i, k) = F(i, k) y G(i, k)

Cuando H(i, k) = 1 se cumple i S k: la alternativa i sobreclasifica a k con los parámetros adoptados.

### Núcleo

El núcleo (noyau) del grafo de sobreclasificación es el subconjunto de alternativas que satisface dos propiedades: estabilidad interna, ninguna alternativa del núcleo sobreclasifica a otra del núcleo; y dominancia externa, toda alternativa fuera del núcleo es sobreclasificada por al menos una de dentro. Un grafo sin circuitos tiene un núcleo único. Un grafo con circuitos puede no tener núcleo en sentido estricto; en ese caso el procedimiento detecta los componentes fuertemente conexos, es decir los circuitos, los contrae a una única clase, extrae el núcleo sobre el grafo resultante, que es acíclico, y lo expande. Las alternativas de un mismo circuito son mutuamente indiferentes y entran o salen del núcleo en bloque. El aplicativo verifica las dos propiedades sobre el conjunto devuelto e informa de la presencia de circuitos y relaciones recíprocas. El núcleo puede contener varias alternativas y no debe leerse como la mejor alternativa, sino como el conjunto de opciones admisibles: evaluar no es decidir. Este tratamiento sigue a Roy (1968) y a Hansen, Anciaux-Mundeleer y Vincke (1976).

## 8. Explicación de las funciones

### Motor de cálculo

- `rangosCriterios`. Calcula el mínimo, el máximo y el rango de cada criterio.
- `matrizNormalizadaRango`. Normaliza por rango.
- `matrizPonderada`. Multiplica la matriz normalizada por los pesos.
- `matrizConcordancia`. Suma los pesos de los criterios favorables, con peso completo en los empates.
- `matrizDiscordancia`. Calcula la discordancia sobre la matriz ponderada.
- `promedioFueraDiagonal`. Promedia los elementos fuera de la diagonal, para los umbrales sugeridos.
- `matrizDominanciaConcordante`, `matrizDominanciaDiscordante`, `matrizDominanciaAgregada`. Construyen F, G y H.
- `calcularNucleo`. Obtiene el núcleo a partir de H mediante detección de componentes fuertemente conexos (Tarjan), contracción de circuitos, extracción del núcleo sobre el grafo acíclico y verificación de estabilidad interna y dominancia externa. Devuelve además los circuitos y las relaciones recíprocas.
- `ordenTopologico`. Ordena topológicamente el grafo acíclico de componentes para extraer el núcleo de forma determinista, invariante ante el orden de las alternativas.
- `electreI`. Ejecuta el método completo y devuelve todas las matrices intermedias.

### Utilidades e interpretación

- `conDecimales` y `dec`. Dan formato a los números en español; `dec` respeta la precisión visual configurada.
- `mostrarMensaje` y `actualizarOrigen`. Gestionan los avisos y la insignia de origen de los datos.

### Interfaz y resultados

- `aplicarConfiguracion`. Valida la configuración y construye las estructuras del modelo.
- `construirTablaCriterios` y `construirMatrizDecision`. Arman las tablas editables.
- `cargarDatosPrueba`. Carga el caso de validación, marcado como prueba.
- `calcularYMostrar` y `renderizarResultados`. Ejecutan el cálculo y muestran las trece etapas en acordeones.
- `detalleConcordancia` y `detalleDiscordancia`. Auditan par por par cada índice.
- `grafoSuperacion`. Dibuja el grafo en SVG, con el núcleo en ámbar.

### Sensibilidad

- `actualizarSensibilidadVivo`. Recalcula H, el grafo y el núcleo con los umbrales de los deslizadores.
- `ejecutarBarridoI`. Recalcula el núcleo para un rango de umbrales de concordancia y señala el punto de quiebre.

### Exportación

- `crearHojaExcel`. Fábrica de hojas con soporte para celdas, fórmulas y enlaces.
- `excelHojaMenu`, `excelHojaDatos`, `excelHojaDecision`, `excelHojaPesos`, `excelHojaRangos`, `excelHojaMatriz`, `excelHojaUmbrales`, `excelHojaSobreclasificaciones`, `excelHojaNucleo`, `excelHojaSensibilidad`. Construyen cada hoja.
- `DocumentoPDF`. Motor de PDF propio, sin bibliotecas, con soporte para círculos y líneas.
- `dibujarGrafoPDF`. Dibuja el grafo de sobreclasificación dentro del PDF.
- `generarInformePDF` y `exportarInformePDF`. Ensamblan y descargan el informe.

### Pruebas

- `PRUEBAS` y `ejecutarPruebas`. Batería de pruebas automáticas que se ejecutan desde la interfaz, incluidas las de regresión sobre el caso de validación.

## 9. Caso de validación

La aplicación trae cargado, con el botón «Cargar datos de prueba», un caso de cinco proyectos evaluados en cinco criterios.

| Alternativa | VAN | TIR | Empleo | Ventas | Impacto ambiental |
| --- | --- | --- | --- | --- | --- |
| A | 100 | 15 | 7 | 40 | 50 |
| B | 200 | 25 | 7 | 60 | 200 |
| C | 100 | 20 | 4 | 25 | 25 |
| D | 200 | 30 | 20 | 70 | 350 |
| E | 250 | 25 | 15 | 100 | 500 |

Los primeros cuatro criterios se maximizan y el impacto ambiental se minimiza. Los pesos son 0,25 para el VAN, 0,25 para la TIR, 0,20 para el empleo, 0,10 para las ventas y 0,20 para el impacto ambiental.

Con los umbrales calculados por defecto, el resultado verificado es:

- Umbral de concordancia c* = 0,5475.
- Sobreclasificaciones: B sobre A, B sobre C, C sobre A, D sobre A, D sobre B, D sobre C, E sobre A y E sobre C.
- Núcleo: D y E.

El núcleo reúne las dos alternativas que ninguna otra sobreclasifica. Decidir entre ellas requiere criterios adicionales a los del modelo. Este resultado se obtiene igual en la aplicación, en el libro de Excel al recalcular sus fórmulas y en el cálculo manual con las fórmulas de la sección 7.

## 10. Modo de prueba

La aplicación carga el caso de validación como datos de prueba, marcados como tales. Los archivos que exporte con esos datos llevan el prefijo PRUEBA y una advertencia dentro. La aplicación nunca presenta datos de prueba como si fueran reales.

## 11. Verificación realizada

Antes de la entrega se ejecutó la aplicación en un navegador real y se comprobó lo siguiente:

- Las veintisiete pruebas automáticas pasan, incluidas las de regresión sobre el caso de validación y las ocho pruebas estructurales del núcleo.
- El motor de cálculo reproduce el caso de validación: c* = 0,5475, d* ≈ 0,8099375843, las ocho sobreclasificaciones y el núcleo D y E, con estabilidad interna y dominancia externa verificadas.
- El tratamiento de circuitos es correcto: en el grafo A → B → C → A el procedimiento detecta el circuito y no selecciona una alternativa arbitraria por el orden de recorrido; el resultado es invariante ante permutaciones del orden de las alternativas.
- El libro de Excel, recalculado de forma independiente con LibreOffice, produce los mismos valores que la aplicación; las fórmulas de rangos, la matriz normalizada y la matriz ponderada recalculan correctamente encadenadas entre hojas.
- Los resultados de pantalla, Excel y PDF coinciden en datos, umbrales, matrices, núcleo, interpretación y versión.
- El PDF abre sin errores, dibuja el grafo dentro del documento y presenta la marca de agua y el pie de página en todas sus páginas.
- Los criterios con rango cero se manejan sin producir NaN ni Infinity, con una advertencia al usuario.
- La página no se desplaza en sentido horizontal a cuatrocientos píxeles de ancho.
- No hay errores en la consola del navegador.
- La precisión en pantalla cambia la presentación sin alterar el cálculo.

## 12. Publicación en GitHub Pages

1. Cree un repositorio en GitHub y suba el contenido del paquete: `index.html`, `README.md`, `LICENSE.md`, `CITATION.cff` y la carpeta `docs`.
2. En el repositorio, entre a Settings y luego a Pages.
3. En Source elija la rama principal y la carpeta raíz.
4. Guarde. En pocos minutos la aplicación quedará disponible en la dirección que GitHub indique.

## 13. Limitaciones

- Los umbrales de concordancia y de discordancia no son constantes universales. Dependen del problema y de la actitud de quien decide. La aplicación calcula valores de partida a partir de los datos, pero no los presenta como referencias publicadas.
- La normalización por rango, el tratamiento del empate con peso completo y el promedio como umbral sugerido son convenciones de esta implementación. Están documentadas y son razonables, pero no son las únicas posibles dentro de la familia ELECTRE.
- El cálculo de la discordancia sobre la matriz ponderada supone que la ponderación hace comparables las diferencias entre criterios. Cuando las unidades son muy dispares, conviene revisar el resultado con cuidado.
- ELECTRE I no ordena las alternativas. Entrega un subconjunto. Esa es una característica del método, no una carencia de la aplicación.
- Un grafo de sobreclasificación con circuitos puede no tener núcleo en sentido estricto. La aplicación resuelve estos casos por contracción de los circuitos e informa de su presencia, pero la interpretación de un circuito, alternativas mutuamente sobreclasificadas, corresponde a quien decide.
- El ejemplo interactivo de la portada usa un umbral fijo con fines ilustrativos y no refleja la configuración del paso 1.

## 14. Historial de versiones

Versión 3.1. Corrección del tratamiento de circuitos en el cálculo del núcleo mediante contracción de componentes fuertemente conexos, con verificación de estabilidad interna y dominancia externa. Ocho nuevas pruebas estructurales del grafo. Revalidación de la sensibilidad con la misma lógica del análisis principal. Manejo explícito de criterios con rango cero. Validación de c* en el intervalo de 0 a 1. Precisión terminológica de los pesos, no negativos y con suma 1. Mejoras en la interpretación metodológica del núcleo. Fortalecimiento de la trazabilidad bibliográfica. Mayor auditabilidad del Excel, con fórmulas encadenadas para la matriz normalizada y la ponderada. Identificación de la versión y consistencia entre exportaciones y documentación.

Versión 3.0. Versión base centrada en ELECTRE I, con las trece etapas en acordeones, trazabilidad «Ver cálculo», grafo de sobreclasificación, análisis de sensibilidad, exportación a Excel y PDF, y pruebas automáticas. Fue la versión sometida a la auditoría metodológica.

## 15. Referencias

Figueira, J., Mousseau, V., & Roy, B. (2005). ELECTRE Methods. En J. Figueira, S. Greco, & M. Ehrgott (Eds.), Multiple Criteria Decision Analysis: State of the Art Surveys (pp. 133-162). Springer. https://doi.org/10.1007/0-387-23081-5_4

Hansen, P., Anciaux-Mundeleer, M., & Vincke, P. (1976). Quasi-kernels of outranking relations. En H. Thiriez & S. Zionts (Eds.), Multiple Criteria Decision Making (Lecture Notes in Economics and Mathematical Systems, vol. 130, pp. 53-63). Springer. https://doi.org/10.1007/978-3-642-87563-2_3

Roy, B. (1968). Classement et choix en présence de points de vue multiples (la méthode ELECTRE). RIRO, 2(8), 57-75. https://doi.org/10.1051/ro/196802v100571

Roy, B. (1991). The outranking approach and the foundations of ELECTRE methods. Theory and Decision, 31(1), 49-73. https://doi.org/10.1007/BF00134132

Shanian, A., & Savadogo, O. (2006). ELECTRE I decision support model for material selection of bipolar plates for polymer electrolyte fuel cells applications. Journal of New Materials for Electrochemical Systems, 9(3), 191-199.
