# Plan de Estudios Completo: Sistema de Macros a la Antigua (Estilo MacLisp / Timothy Hart, 1963)

## 🗺️ Mapa de Ruta del Aprendizaje

Este curso está diseñado de forma incremental. Ningún módulo avanzado se puede abordar sin haber construido y dominado los ladrillos de software del módulo anterior, utilizando únicamente primitivas de manipulación de listas sin ayudas sintácticas modernas.

---

## 🛠️ ADENDA METODOLÓGICA: La Rutina Práctica contra el Bloqueo Mental ("Escribir para Ver")

> **Regla de oro para mentes prácticas:** Si te cuesta imaginar cómo fluyen los datos en una lista de más de 4 elementos o en una forma anidada de `defun`/`eval`, **no lo imagines: imprímelo**. Utiliza siempre esta rutina de boceto rápido en el REPL antes de escribir código a ciegas:
> 1. **El Banco de Pruebas (Mock Input):** Define una variable global con `defparameter` que contenga una lista real idéntica a la que recibiría tu macro o función.
> 2. **El Trazado Desglosado:** Ejecuta individualmente cada `car`, `cdr`, `cadr` o combinación sobre esa variable en el REPL y observa inmediatamente el resultado en pantalla.
> 3. **El Ensamblaje con `list`:** Construye la salida deseada usando la función `list` para ver físicamente cómo se rearma el árbol de código antes de meterlo dentro de una definición formal.
> 
> 

---

## 📦 FASE 1: La Fundación Conceptual (Pensar en Datos)

### Módulo 0 — La mentalidad Lisp y la Homoiconicidad

* **Objetivo:** Aprender a mirar una expresión Lisp como una estructura de datos en el espacio (listas enlazadas de celdas cons) y no como simple texto plano.
* **Contenido:**
* Anatomía de una lista evaluable en el REPL de SBCL.
* Qué significa el primer elemento frente a los argumentos en una S-expression.
* Experimentación y distinción visual entre datos estáticos y ejecución.



### Módulo 1 — Listas como estructuras físicas (Celdas Cons) y Listas Largas

* **Objetivo:** Dominar el árbol de celdas cons y perder el miedo a listas complejas de más de 4 elementos mediante inspección real.
* **Contenido:**
* Uso de las primitivas clásicas (`car`, `cdr`, `cadr`, `caddr`, `cadddr`) y cuándo dejar de encadenarlas para usar funciones auxiliares o iterativas si la lista supera los límites manejables.
* Uso correcto de `defparameter` en SBCL para crear bancos de pruebas estables y evitar advertencias de variables globales libres.
* Representación mental y práctica de diagramas de cajas, flechas y resultados directos en el REPL.



### Módulo 2 — La Evaluación y su Ausencia

* **Objetivo:** Comprender la bifurcación lógica entre datos que existen pasivamente y datos que se ejecutan activamente.
* **Contenido:**
* Análisis de la diferencia exacta entre la ejecución de `(+ 2 3)` y la congelación de datos en `'(+ 2 3)`.
* El papel del evaluador al inspeccionar una estructura de datos antes de calcularla.



### Módulo 3 — La Comilla (`QUOTE`) como Congelador

* **Objetivo:** Aprender a congelar y descongelar estructuras a voluntad para evitar la evaluación prematura.
* **Contenido:**
* Qué hace realmente la comilla simple `'` a nivel de representación en memoria.
* El concepto de control sintáctico: cuándo tratar un símbolo como variable de trabajo o como dato literal para ser manipulado.



---

## 🛠️ FASE 2: Herramientas de Construcción y Destrucción

### Módulo 4 — `let` y `let*` (La Mesa de Trabajo del Cirujano)

* **Objetivo:** Almacenar variables temporales de forma secuencial sin alterar el estado global del entorno.
* **Contenido:**
* La diferencia entre asignación en paralelo (`let`) y asignación secuencial o incremental (`let*`).
* Uso de `let*` como plantilla para retener piezas extraídas de una lista compleja de código paso a paso.



### Módulo 5 — Construir código con constructores puros (`list` y `cons`)

* **Objetivo:** Aprender a fabricar planos de código combinando elementos sueltos sin usar plantillas mágicas.
* **Contenido:**
* El uso exclusivo de constructores puros: `list`, `cons` y `append`.
* Diferencia práctica entre crear la lista de código mediante funciones y ordenar al evaluador que la ejecute.



### Módulo 6 — Desmontar código (Extracción Quirúrgica y Práctica)

* **Objetivo:** Desarrollar el automatismo mental y práctico para trocear expresiones complejas de longitud variable.
* **Contenido:**
* Extracción sistemática de componentes en formas largas utilizando variables temporales en lugar de adivinar el flujo mentalmente.
* Aplicación directa de la *Rutina Práctica de Escritura de Código* para auditar listas de código crudo antes de pasarlas al expansor.



---

## 🏗️ FASE 3: Fábrica de Primitivas Clásicas para SBCL (Sin Magia Moderna)

*Este bloque enseña cómo solucionar las carencias del dialecto moderno usando ingeniería propia basada en MacLisp.*

### Unidad Herramental A: Creación de `PUTPROP` artesanal

* **Objetivo:** Encapsular el almacenamiento de propiedades en la espalda de los símbolos (Listas de Propiedades o *PLists*).
* **Contenido:**
* Uso práctico de `SETF` combinado con `GET` en Common Lisp para emular el comportamiento histórico de MacLisp.
* Implementación con `defun` de la función clásica `(putprop simbolo valor etiqueta)`.



### Unidad Herramental B: Simulación de FEXPRs (Funciones que no evalúan)

* **Objetivo:** Crear estructuras de control que imiten funciones clásicas que reciben argumentos sin evaluar.
* **Contenido:**
* Modelado de listas especiales marcadas con la etiqueta `'MACRO` o `'FEXPR` en la propiedad del símbolo.
* El uso de `cond` y listas de asociación (`A-lists`) para interceptar la ejecución normal del código antes de que llegue al evaluador estándar.



---

## 🔄 FASE 4: El Motor de Transformación y Expansión Manual

### Módulo 7 — La primera función que transforma código

* **Objetivo:** Programar un traductor puro de listas que reciba una forma y retorne otra mediante `list` y `cons`.
* **Contenido:**
* Implementación de una función que toma `'(mi-suma x y)` y devuelve `'(+ x y)` sin ejecutar nada en el proceso.



### Módulo 8 — Del transformador a la macro histórica

* **Objetivo:** Entender la línea de tiempo del flujo de datos en una macro primitiva.
* **Contenido:**
* Flujo de función normal: Evaluación previa automática de argumentos.
* Flujo de macro clásica: Transformación previa manual del código fuente crudo.



### Módulo 9 — Construir un expansor manual

* **Objetivo:** Crear el primer expansor de código (`expandir-mi-suma`) aplicando estrictamente la Regla del Espejo y la inspección en el REPL.
* **Contenido:**
* Pruebas analíticas inyectando listas de prueba fijas y evaluando paso a paso los resultados de las transformaciones.



### Módulo 10 — El registro de macros en la PList

* **Objetivo:** Crear la base de datos de control de macros de nuestro propio sistema usando `putprop`.
* **Contenido:**
* Asociación del nombre de la macro con su función expansora almacenándola directamente en las propiedades del símbolo.



### Módulo 11 — Construir un pequeño macroexpansor casero

* **Objetivo:** Programar el algoritmo que busca y aplica expansores sin usar las funciones nativas de SBCL.
* **Contenido:**
* Implementación de `mi-macroexpand-1` (un solo pase de expansión).
* Implementación de `mi-macroexpand` (expansión recursiva continua hasta estabilizar la forma).



### Módulo 12 — Nuestro primer sistema de macros funcional

* **Objetivo:** Integrar el registro, la tabla de propiedades y el macroexpansor en una sola infraestructura visible y depurable paso a paso.

---

## 🎛️ FASE 5: Diseño de la Interfaz Humana (Tu propia DSL Primitiva)

### Módulo 13 — Construir nuestro propio mecanismo equivalente a `defmacro`

* **Objetivo:** Crear la función auxiliar que automatiza la creación y el registro de expansores a partir de una descripción de sintaxis propia.
* **Contenido:**
* Desarmado manual de la definición de la macro: nombre, parámetros y cuerpo usando `car`, `cdr` y la rutina de inspección práctica.



### Módulo 14 — Diseñar nuestra propia forma de definir macros

* **Objetivo:** Romper la convención sintáctica estándar y diseñar una interfaz propia más fácil de leer, auditar y depurar.
* **Contenido:**
* Análisis crítico de alternativas de diseño sintáctico sin depender de azúcar sintáctico moderno.



### Módulo 15 — Abstracciones sin magia (Inspección de Estado)

* **Objetivo:** Garantizar que el sistema final permita "abrir la máquina" para auditar qué enlaces creó, qué propiedades tienen los símbolos y dónde se registraron.

### Módulo 16 — Soporte para cuerpos de varias expresiones

* **Objetivo:** Resolver el problema de macros con múltiples instrucciones de código utilizando construcciones explícitas con `'progn`.
* **Contenido:**
* Inyección dinámica y automática del operador `progn` mediante manipulación de listas.



### Módulo 17 — Argumentos variables (Listas Rest manuales)

* **Objetivo:** Diseñar soporte para macros con cero, uno o infinitos argumentos utilizando la extracción recursiva mediante `cdr`.

---

## 🚨 FASE 6: Estabilidad y el Infierno de la Higiene Primitiva

### Módulo 18 — Errores y robustez estructural

* **Objetivo:** Implementar validaciones manuales que detecten errores semánticos cerca del origen antes de evaluar el código generado.
* **Contenido:**
* Captura de parámetros mal formados o cuerpos inexistentes mediante validaciones con `atom` y `cond`.



### Módulo 19 — Higiene y captura accidental de variables

* **Objetivo:** Comprender el error histórico de las colisiones de nombres entre las variables internas de la macro y las variables del usuario.

### Módulo 20 — Símbolos generados de forma única (Versión didáctica de gensym)

* **Objetivo:** Resolver la captura accidental mediante la creación manual de un generador de símbolos únicos basado en contadores atómicos y `intern`/`symbol-name`.

### Módulo 21 — Fases completas de expansión recursiva segura

* **Objetivo:** Garantizar que el expansor procese macros anidadas dentro de otras macros de forma estable y ordenada.

---

## 🏁 FASE 7: El Sistema Completo e Integración Final

### Módulo 22 — Construir un pequeño evaluador con soporte manual para macros

* **Objetivo:** Integrar tu macroexpansor dentro de un intérprete didáctico personalizado (`mi-eval`).
* **Contenido:**
* El ciclo de control: Interceptar la lista ➔ Comprobar si es macro ➔ Si lo es, expandir y reevaluar el resultado ➔ Si no, ejecutar evaluación estándar.



### Módulos 23 y 24 — Perfeccionamiento y DSL Avanzada

* **Objetivo:** Pulir y expandir las capacidades sintácticas de tu sistema bajo la regla de oro: *"La interfaz puede ser sencilla; el mecanismo interno debe seguir siendo totalmente transparente y comprensible con `car`, `cdr` y `list`."*

### Módulo 25 — Compartación y Auditoría Crítica

* **Objetivo:** Evaluar las ventajas, desventajas, velocidad y límites de tu lenguaje frente al `defmacro` moderno de Common Lisp.

### Módulo 26 — Proyecto Final y Prueba de Comprensión

* **Objetivo:** Demostrar el dominio absoluto del sistema de expansión de código a la antigua.
* **Contenido:**
* Implementación funcional en tu entorno de las macros básicas: `(mi-cuando ...)`, `(mi-unless ...)`, `(mi-progn ...)` y `(mi-let ...)`.
* Explicación oral de los puntos de control del flujo de datos en el REPL.
* Diseño y ejecución de una macro completamente original e inédita creada de forma independiente por el alumno usando exclusivamente las herramientas construidas.



---

# 📚 FUENTES Y REFERENCIAS BIBLIOGRÁFICAS OFICIALES (DOCUMENTACIÓN DE CONTROL)

* **McCarthy, John et al. (1962). *LISP 1.5 Programmer's Manual*. MIT Computation Center and Research Laboratory of Electronics.**
* **Moon, David A. (1974). *MacLisp Reference Manual*. Project MAC, MIT.**
* **Pitman, Kent M. (1980). *Special Forms in Lisp*. Proceedings of the 1980 ACM Conference on LISP and Functional Programming.**
* **Abelson, Harold; Sussman, Gerald Jay; Sussman, Julie (1996). *Structure and Interpretation of Computer Programs (SICP)* (2nd ed.). MIT Press.**
* **Steele, Guy L. Jr. (1990). *Common Lisp the Language* (2nd ed.). Digital Press (CLtL2).**

---
