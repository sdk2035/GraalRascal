# GraalRascal 🚀

**GraalRascal** es una implementación de alto rendimiento del metalenguaje de programación **Rascal**, desarrollada sobre **GraalVM** utilizando el framework Truffle.

Esta plataforma está diseñada para acelerar la metaprogramación, el análisis de código fuente, la transformación de programas y el diseño de Lenguajes de Dominio Específico (DSLs). Combina las potentes abstracciones de Rascal (recorrido de árboles AST, expresiones regulares en términos, relaciones algebraicas) con las optimizaciones JIT avanzadas de GraalVM y su ecosistema políglota.

---

## 🌟 Características Principales

* **Metaprogramación de Alto Rendimiento:** Compilación JIT que optimiza el recorrido de árboles de sintaxis (`visit`), la coincidencia de patrones (*pattern matching*) y las operaciones sobre conjuntos/relaciones algebraicas.
* **Procesamiento Eficiente de ASTs:** Representación optimizada de tipos de datos algebraicos (ADT) mediante nodos Truffle que se auto-modifican según los patrones de ejecución.
* **Interoperabilidad Políglota:** Capacidad para analizar y transformar código fuente de lenguajes ejecutados en GraalVM (Java, Python, JavaScript, C/C++) directamente en memoria y sin sobrecarga de serialización.
* **Ejecución Nativa (Native Image):** Compilación del entorno de metaprogramación a un ejecutable autónomo con **GraalVM Native Image**, ideal para integraciones en pipelines de CI/CD y herramientas de CLI.

---

## 🏗️ Arquitectura de la Plataforma

* **Rascal Truffle Parser:** Convierte la sintaxis del metalenguaje Rascal y la definición de gramáticas RASCAL/SDF en un Árbol de Sintaxis Abstracta (AST) ejecutable por Truffle.
* **Pattern Matching & Traversal Engine:** Motor optimizado enfocado en la coincidencia rápida de patrones sintácticos y traversals profundos en árboles de código.
* **Polyglot AST Bridge:** Interfaz que permite a Rascal inspeccionar e interactuar con los ASTs de otros lenguajes soportados por el framework Truffle.

---

## 🚦 Inicio Rápido

### Prerrequisitos

* **GraalVM JDK** (versión 21 o superior) con componentes Truffle habilitados.
* Variable de entorno `JAVA_HOME` apuntando al directorio de instalación de GraalVM.

### Instalación

```bash
# Clonar el repositorio
git clone [https://github.com/tu-usuario/graalrascal.git](https://github.com/tu-usuario/graalrascal.git)
cd graalrascal

# Construir el proyecto utilizando Gradle
./gradlew build
