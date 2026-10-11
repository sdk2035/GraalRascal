# Arquitectura propuesta de GraalRascal

## Contexto y límites

Usuarios: ingenieros de lenguajes, autores de DSL y responsables de validación.
Entradas: texto fuente Rascal y configuración del subconjunto. Salidas: valores
normalizados o diagnósticos. Un CLI y un adaptador Polyglot compartirán el runtime.
El intérprete Rascal de referencia es un oráculo externo de pruebas, no parte del
runtime GraalRascal. No hay servicios desplegados en el repositorio actual.

## Componentes propuestos

| ID | Componente | Responsabilidad | Estado |
| --- | --- | --- | --- |
| C1 | CLI/host Polyglot | Crear contexto, enviar fuente y presentar resultados | MVP propuesto |
| C2 | Frontend | Tokens, parser del subconjunto y AST de análisis con source spans | MVP propuesto |
| C3 | Validación/lowering | Resolver nombres, comprobar operadores y construir nodos ejecutables | MVP propuesto |
| C4 | Runtime Truffle | Contexto, frames, nodos y ejecución | MVP propuesto |
| C5 | Modelo de valores | Enteros/booleanos y contratos de igualdad; valores inmutables | MVP propuesto |
| C6 | Diagnósticos | Código, fase, mensaje y ubicación | MVP propuesto |
| C7 | Harness diferencial | Ejecutar fixtures en ambos motores y comparar resultados | MVP propuesto |
| C8 | Extensiones | ADT, matching, visit, relaciones y adaptadores explícitos | Posterior |

El AST de análisis, los nodos ejecutables Truffle y los valores/árboles tratados
como datos son tres representaciones distintas. La especialización de un nodo
ejecutable no autoriza mutar un valor Rascal observable.

## Contratos técnicos

- SourceUnit: texto, URI lógica, versión del subconjunto y hash de contenido.
- SourceSpan: offset inicial/final y línea/columna; convención de índices y Unicode
  por fijar en la tarea inicial, con pruebas de límites.
- EvaluationResult: valor etiquetado normalizado o Diagnostic; nunca salida parcial
  presentada como éxito. Excepciones internas se registran separadamente.
- Diagnostic: código estable, fase, mensaje y span cuando exista; comparación por
  código/ubicación normalizados, no por texto idéntico entre motores.
- Fixture: ID, fuente, categoría, resultado de referencia, versión de referencia
  y estado de ejecución. Un resultado esperado redactado no es evidencia ejecutada.

## Decisiones y alternativas

1. Seleccionar parser propio para un subconjunto o reutilizar frontend Rascal tras
   revisar APIs/licencias. Registrar la decisión y coste; no asumir un parser SDF.
2. Evaluar reutilización del modelo de valores Rascal frente a modelo mínimo propio.
   Exigir igualdad e inmutabilidad observables y evitar semántica numérica Java implícita.
3. Fijar combinaciones JDK/Truffle y build tras un spike; no declarar que cualquier
   JDK 21+ es compatible. Registrar lockfiles y artefactos de annotation processing.
4. Exportar valores mediante contratos interop explícitos. Polyglot no constituye
   un contrato de exposición universal de AST privados de otros lenguajes.
5. Mantener Native Image y benchmarking fuera del primer gate funcional.

## Referencias primarias

- [Valores inmutables de Rascal](https://www.rascal-mpl.org/docs/Recipes/BasicProgramming/ImmutableValues/): guía para C5.
- [Visit en Rascal](https://www.rascal-mpl.org/docs/Rascal/Expressions/Visit/): alcance posterior de recorridos.
- [Polyglot de GraalVM](https://www.graalvm.org/reference-manual/polyglot-programming/): integración mediante contratos de valores.
- [Implementación y embedding de lenguajes](https://github.com/oracle/graal/blob/master/docs/reference-manual/embedding/embed-languages.md): referencia para C1/C4.

Consultadas el 11 de octubre de 2026; las versiones efectivamente usadas se fijarán
antes de implementar. No se importaron fuentes o dependencias externas.
