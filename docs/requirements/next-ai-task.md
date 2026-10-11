# GR-REQ-001 — Subconjunto de expresiones y fixtures Rascal

Estado: propuesta pendiente. Objetivo: fijar el contrato antes del runtime.

1. Seleccionar una versión de Rascal de referencia y registrar procedencia/licencia.
2. Definir una gramática limitada de literales enteros/booleanos, paréntesis,
   operadores y acceso a variables. Decidir cómo se suministra el entorno inicial;
   no inventar sintaxis de declaraciones que se presente como Rascal compatible.
3. Documentar precedencia, tipos, igualdad, división, errores y límites de recursos.
4. Redactar al menos 12 fixtures positivos y 8 negativos que incluyan expresiones
   anidadas, enteros grandes, división por cero, nombres desconocidos, tipos
   incompatibles y sintaxis fuera del alcance.
5. Ejecutarlos contra la referencia y guardar resultados normalizados y logs.
6. Elegir parser y combinación de herramientas con decisión técnica documentada.

Entregables previstos: gramática, catálogo de fixtures, runner de referencia,
manifest de versiones y matriz requisito-fixture. Aceptación: cada fixture tiene
origen semántico, resultado ejecutado o bloqueo explícito; FR-01–FR-05 están
cubiertos. Sin runner disponible, la tarea produce borradores y queda parcialmente
pendiente. La IA asiste en extracción/diseño; mantenedores aceptan el contrato.
