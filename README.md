# GraalRascal

GraalRascal propone investigar e implementar un subconjunto del metalenguaje
Rascal sobre GraalVM/Truffle para análisis y transformación de programas.
Su objetivo es preservar la semántica del subconjunto elegido antes de evaluar
optimización JIT e interoperabilidad.

## Estado del proyecto

Evaluación: 11 de octubre de 2026. La base inspeccionada contiene solo un README;
no hay implementación, build, ejemplos ejecutables ni mediciones. Los diagramas
representan una arquitectura propuesta, no ingeniería inversa de código existente.
No se declara compatibilidad completa con Rascal, aceleración demostrada,
acceso automático a AST de otros lenguajes ni soporte Native Image validado.

## Primer alcance propuesto

Expresiones enteras y booleanas, operadores definidos, entorno de variables
inmutable por valor y diagnósticos con ubicación de origen. El contrato semántico
se fijará mediante fixtures ejecutados contra una versión identificada de Rascal.
ADT, matching, visit, relaciones, gramáticas de usuario e interop ampliarán ese
alcance en hitos posteriores.

## Documentación

- [Índice técnico](docs/README.md)
- [Arquitectura y contratos](docs/architecture/high-level-design.md)
- [Requisitos y aceptación](docs/requirements/specification.md)
- [Siguiente tarea asistida por IA](docs/requirements/next-ai-task.md)
- [Diagramas draw.io](docs/diagrams/README.md)

No existe aún un comando de compilación válido. La primera implementación debe
fijar JDK, Truffle, dependencias, licencias y versión de referencia antes de
publicar instrucciones reproducibles.
