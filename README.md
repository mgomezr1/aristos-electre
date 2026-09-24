# Áristos ELECTRE

Aplicación web académica para tomar decisiones con el método de superación **ELECTRE I** de Bernard Roy: compare alternativas criterio por criterio, identifique cuáles no son sobreclasificadas por ninguna otra y siga cada etapa del cálculo con total transparencia.

**Abrir la aplicación:** https://mgomezr1.github.io/aristos-electre/

No requiere instalación ni registro. Funciona en cualquier navegador moderno, en computador, tableta o teléfono.

## Qué permite hacer

- Definir las alternativas y los criterios, en la cantidad que necesite, con su sentido (maximizar o minimizar) y su peso.
- Calcular, paso a paso, los rangos, la matriz normalizada por rango, la matriz ponderada y los índices de concordancia y discordancia entre cada par de alternativas.
- Auditar par por par cómo se obtiene cada índice, con la función «Ver cálculo».
- Ajustar la precisión con que se muestran los números, sin alterar el cálculo interno.
- Ver las matrices de dominancia F, G y H, el grafo de sobreclasificación y el núcleo de alternativas no sobreclasificadas.
- Hacer análisis de sensibilidad en vivo y descubrir qué tendría que cambiar para que el resultado fuera otro.
- Descargar los resultados en Excel, con las fórmulas escritas celda por celda, y un informe ejecutivo en PDF con el grafo dibujado dentro del documento.

## Cómo usarla

1. Lea la explicación del método y pruebe el ejemplo de sobreclasificación de la portada.
2. En **Configuración**, defina el número de alternativas y criterios y la precisión en pantalla, y confirme. Puede fijar los umbrales o dejar que la aplicación los calcule.
3. En **Matriz de decisión**, nombre cada criterio, indique su sentido y su peso (los pesos deben sumar 1) y escriba el desempeño de cada alternativa.
4. Pulse **Calcular** y recorra las trece etapas en los acordeones de resultados.
5. Si quiere, explore la **Sensibilidad** y descargue el **Excel** o el **informe PDF**.

El **modo de prueba** carga el caso de validación con datos ficticios para practicar; esos datos no representan casos reales y los archivos que exporte con ellos llevan el prefijo PRUEBA.

## Privacidad

Todos los cálculos se hacen en su navegador. Los datos no se envían a ningún servidor ni se guardan: al cerrar o recargar la página se pierden, así que descargue el Excel o el PDF antes de salir.

## Requisitos

- Navegador actualizado (Chrome, Edge, Firefox o Safari) con JavaScript activo.
- Conexión a internet para exportar a Excel, porque la aplicación descarga la biblioteca SheetJS. El informe PDF funciona sin conexión.

## Documentación

La guía completa (método, fórmulas, funciones, exportaciones y limitaciones) está en [docs/Guia_Aristos_ELECTRE.md](docs/Guia_Aristos_ELECTRE.md).

## Cómo citar

Gómez Rueda, M. S. (2026). *Áristos ELECTRE* (Versión 3.0) [Software]. https://mgomezr1.github.io/aristos-electre/

## Autoría y uso

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Consulte los términos en [LICENSE.md](LICENSE.md). Sugerencias o dudas: mgomezr1@gmail.com

## Convenciones de la implementación

Áristos ELECTRE explicita las decisiones que toma dentro de la familia ELECTRE, para que puedan interpretarse y discutirse:

- Normalización por rango: cada valor se divide por el rango de su criterio, sin reescalar al intervalo de cero a uno.
- Concordancia: el empate en un criterio recibe el peso completo de ese criterio.
- Umbrales por defecto: el promedio de los elementos fuera de la diagonal de cada matriz, como punto de partida a partir de los datos, no como constante universal.

## Fundamento metodológico

- Roy, B. (1991). The outranking approach and the foundations of ELECTRE methods. *Theory and Decision, 31*(1), 49-73. https://doi.org/10.1007/BF00134132
- Figueira, J., Mousseau, V., & Roy, B. (2005). ELECTRE Methods. En J. Figueira, S. Greco, & M. Ehrgott (Eds.), *Multiple Criteria Decision Analysis: State of the Art Surveys* (pp. 133-162). Springer. https://doi.org/10.1007/0-387-23081-5_4
- Shanian, A., & Savadogo, O. (2006). ELECTRE I decision support model for material selection of bipolar plates for polymer electrolyte fuel cells applications. *Journal of New Materials for Electrochemical Systems, 9*(3), 191-199.

## Componentes de terceros

La exportación a Excel usa [SheetJS Community Edition](https://sheetjs.com), distribuida bajo la licencia Apache 2.0 y cargada desde cdn.sheetjs.com.
