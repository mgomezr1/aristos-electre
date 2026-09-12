# Áristos ELECTRE

Aplicación web académica para tomar decisiones con el método de superación **ELECTRE** de Bernard Roy: compare alternativas criterio por criterio, identifique cuáles no son superadas por ninguna otra y, si lo necesita, obtenga un ranking completo.

**Abrir la aplicación:** https://mgomezr1.github.io/aristos-electre/

No requiere instalación ni registro. Funciona en cualquier navegador moderno, en computador, tableta o teléfono.

## Qué permite hacer

- Definir las alternativas y los criterios, en la cantidad que necesite, con su sentido (maximizar o minimizar) y su peso.
- Elegir entre dos variantes: ELECTRE I, que entrega el núcleo de alternativas no superadas, y ELECTRE II, que produce un ranking completo.
- Calcular los índices de concordancia y discordancia entre cada par de alternativas.
- Aplicar el veto de forma global o con un umbral propio por criterio.
- Ver el grafo de superación con el núcleo destacado.
- Hacer análisis de sensibilidad y descubrir qué tendría que cambiar para que la recomendación fuera otra.
- Descargar los resultados en Excel, con las fórmulas escritas celda por celda, y un informe ejecutivo en PDF.

## Cómo usarla

1. Lea la explicación del método y pruebe el ejemplo de superación de la portada.
2. En **Configuración**, defina el número de alternativas y criterios, la variante y los umbrales, y confirme.
3. En **Matriz de decisión**, nombre cada criterio, indique su sentido y su peso, y escriba el desempeño de cada alternativa.
4. Pulse **Calcular** y revise las matrices, el grafo y el resultado.
5. Si quiere, explore la **Sensibilidad** y descargue el **Excel** o el **informe PDF**.

El **modo de prueba** carga ejemplos con datos ficticios para practicar; esos datos no representan casos reales y los archivos que exporte con ellos llevan el prefijo PRUEBA.

## Privacidad

Todos los cálculos se hacen en su navegador. Los datos no se envían a ningún servidor ni se guardan: al cerrar o recargar la página se pierden, así que descargue el Excel o el PDF antes de salir.

## Requisitos

- Navegador actualizado (Chrome, Edge, Firefox o Safari) con JavaScript activo.
- Conexión a internet para exportar a Excel, porque la aplicación descarga la biblioteca SheetJS. El informe PDF funciona sin conexión.

## Documentación

La guía completa (método, fórmulas, funciones, exportaciones y limitaciones) está en [docs/Guia_Aristos_ELECTRE.md](docs/Guia_Aristos_ELECTRE.md).

## Cómo citar

Gómez Rueda, M. S. (2026). *Áristos ELECTRE* (Versión 1.0) [Software]. https://mgomezr1.github.io/aristos-electre/

## Autoría y uso

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Consulte los términos en [LICENSE.md](LICENSE.md). Sugerencias o dudas: mgomezr1@gmail.com

## Fundamento metodológico

- Roy, B. (1968). Classement et choix en présence de points de vue multiples (la méthode ELECTRE). *Revue Française d'Informatique et de Recherche Opérationnelle, 2*(8), 57-75.
- Roy, B. (1991). The outranking approach and the foundations of ELECTRE methods. *Theory and Decision, 31*(1), 49-73. https://doi.org/10.1007/BF00134132
- Figueira, J., Mousseau, V., & Roy, B. (2016). ELECTRE methods. En S. Greco, M. Ehrgott, & J. Figueira (Eds.), *Multiple Criteria Decision Analysis: State of the Art Surveys* (2.ª ed., pp. 155-185). Springer.

## Componentes de terceros

La exportación a Excel usa [SheetJS Community Edition](https://sheetjs.com), distribuida bajo la licencia Apache 2.0 y cargada desde cdn.sheetjs.com.
