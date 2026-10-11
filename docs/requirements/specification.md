# Especificación de requisitos propuesta

Estado: línea base para revisión, no requisitos aceptados ni funciones existentes.
Objetivo: un piloto reproducible que ejecute un subconjunto definido de Rascal
preservando comportamiento observable frente a una referencia versionada.

## Requisitos y trazabilidad

| ID | Requisito verificable | Aceptación propuesta | Componente/diagrama |
| --- | --- | --- | --- |
| FR-01 | Reconocer únicamente la gramática del subconjunto versionado | Fixtures válidos producen AST; construcciones fuera del alcance dan diagnóstico explícito | C2 / D2 |
| FR-02 | Evaluar enteros, booleanos y operadores del contrato | Cada fixture coincide con valor/tipo de la referencia; overflow y división definidos antes de implementar | C3–C5 / D2 |
| FR-03 | Resolver variables en un entorno con reglas explícitas | Fixtures de nombre desconocido y alcance producen la categoría esperada | C3/C4 / D2 |
| FR-04 | Mantener valores observables inmutables | Actualizar una variable no cambia un valor previamente retenido; fixture de regresión | C5 / D2 |
| FR-05 | Asociar errores a fase y origen | Casos de léxico, sintaxis y evaluación producen código y span comprobados | C6 / D2 |
| FR-06 | Ofrecer una entrada host/CLI reproducible | Mismo fixture devuelve mismo resultado normalizado mediante CLI; comandos documentados | C1 / D1 |
| FR-07 | Comparar motores con evidencia versionada | Registrar salida, versión, código de salida y diferencias por fixture en ambos motores | C7 / D3 |
| FR-08 | Aislar el estado entre contextos | Dos evaluaciones en contextos nuevos no comparten variables | C4 / D2 |
| NFR-01 | Construir desde checkout limpio con dependencias fijadas | Build documentado pasa en entorno limpio y registra versiones/checksums | C1–C7 / D3 |
| NFR-02 | Rechazar acceso host/IO no habilitado | Caso de acceso no permitido falla; tests sin red ni escritura arbitraria | C1/C4 / D1 |
| NFR-03 | Mantener trazabilidad requisito-fixture | Todos los requisitos del gate tienen al menos un fixture y resultado registrado | C7 / D3 |
| NFR-04 | Medir rendimiento sin sustituir validación semántica | Benchmark posterior registra warmup, muestras, entorno y versión; sin promesa de mejora | C7 / D3 |

## Casos de uso

UC-01: usuario envía expresión válida → frontend/validación/runtime → resultado.
UC-02: usuario envía construcción no soportada → diagnóstico y salida de error.
UC-03: mantenedor ejecuta corpus → comparación con Rascal → informe de diferencias.

## Gate de aceptación MVP

Todos los fixtures declarados dentro del alcance deben coincidir en tipo y valor
normalizados; todos los negativos deben cumplir el contrato de diagnóstico.
No debe haber fallos inexplicados, dependencia de red durante las pruebas ni
contaminación entre contextos. El corpus y el entorno deben ser reproducibles.
El tamaño del corpus se fijará en la primera tarea y será revisado por mantenedores.

## Fuera de alcance inicial

Rascal completo, gramáticas de usuario, módulos/imports completos, ADT, visit,
matching avanzado, relaciones, inspección automática de AST ajenos y Native Image.
Estos temas requieren nuevos requisitos y aceptación independiente.

## Riesgos y asuntos abiertos

Semántica de enteros arbitrarios, división y igualdad; API/licencia del frontend
reutilizado; diagnóstico equivalente entre motores; correspondencia entre valores
y nodos; compatibilidad JDK/Truffle; obtención del runner de referencia.
Cada decisión debe registrar alternativas, fuente y fixture afectado.
