# Documento de Ruta del Tutor de Macros (1963)

---

## 1. Visión General del Plan de Estudios

Este documento define la ruta de aprendizaje pedagógico e histórico para dominar el uso y construcción de **macros en LISP 1.5**, basándose de forma estricta en la propuesta original de **Timothy Hart (MIT AI Memo 57, 1963)**.

El objetivo pedagógico es guiar al estudiante desde la manipulating básica de estructuras de datos (listas y celdas CONS) hasta la invención de abstracciones sintácticas que expanden el lenguaje antes del proceso de evaluación (*evaluation step*).

---

## 2. Mapa de Progresión Modular

El programa está estructurado en **cuatro módulos conceptuales sucesivos**. No se permite avanzar al siguiente módulo sin dominar el modelo mental del nivel anterior.

```
+-------------------------------------------------------------------+
|  MÓDULO 1: Fundamentos de Listas, Evaluador y Celdas CONS (1962)  |
+-------------------------------------------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|  MÓDULO 2: Definición de Funciones Simbólicas y Recursión Puro   |
+-------------------------------------------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|  MÓDULO 3: El Nacimiento de las Macros (AI Memo 57 - Hart 1963)   |
+-------------------------------------------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|  MÓDULO 4: Abstracciones Complejas y Control de Flujo Personal   |
+-------------------------------------------------------------------+
```

---

## 3. Desglose de Módulos Pedagógicos

### Módulo 1: Fundamentos de Listas y Representación Física en Memoria
* **Objetivos:** 
  - Comprender la representación de listas como colecciones de celdas `CONS` (*dotted pairs*).
  - Dominar el uso de los selectores `CAR` y `CDR`.
  - Entender el funcionamiento del evaluador de LISP y la necesidad de `QUOTE` (`'`).
* **Presupuesto de Funciones:** `CAR`, `CDR`, `CONS`, `ATOM`, `EQ`, `NULL`, `QUOTE`.
* **Hito de Evaluación:** El estudiante debe ser capaz de trazar manualmente en papel la estructura de punteros en memoria para expresiones anidadas complejas.

### Módulo 2: Constructores, Predicados y Lógica Recursiva
* **Objetivos:**
  - Diseñar funciones que manipulen listas sin alterar el estado en memoria.
  - Formular casos base y casos inductivos utilizando la estructura condicional `COND`.
  - Construir funciones fundamentales como `MEMBER`, `APPEND`, `LENGTH` y `REVERSE`.
* **Presupuesto de Funciones:** Se agregan `COND`, `DEFUN` / `DEFINE`, `LAMBDA`, y predicados numéricos básicos (`ZEROP`, `ADD1`, `SUB1`).
* **Hito de Evaluación:** Implementar sustituciones simbólicas manuales simulando el comportamiento de la pila de llamadas (*stack*) de la IBM 7094.

### Módulo 3: El Mecanismo de Macros (Hart, 1963)
* **Objetivos:**
  - Diferenciar entre el **tiempo de expansión** (*compile/macro-expansion time*) y el **tiempo de ejecución** (*evaluation time*).
  - Entender que una macro es una función que recibe **código como dato** (expresiones S no evaluadas) y retorna **nuevo código**.
  - Construir transformadores de sintaxis simples sin el uso de backquote `` ` `` ni coma `,` (herramientas modernas no existentes en 1963).
* **Mecanismo Técnico (Memo 57):**
  - Una macro en LISP 1.5 toma una lista que representa la llamada a la macro y construye la expresión S de reemplazo mediante llamadas explícitas a `CONS`, `LIST`, `CAR`, `CDR`.
* **Hito de Evaluación:** Crear una macro simple como `FIRST-MACRO` o `NIF` (condicional numérico) usando construcción explícita con `CONS`.

### Módulo 4: Abstracciones Sintácticas Avanzadas y Control
* **Objetivos:**
  - Implementar nuevos operadores de control de flujo inexistentes en LISP 1.5 (ej. `WHEN`, `UNLESS`, `IF` simplificado).
  - Comprender los riesgos de la evaluación múltiple de argumentos y la captura de variables en macros primitivas.
* **Hito de Evaluación:** Diseñar una macro compleja que transforme una estructura imperativa simulada en expresiones recursivas `COND` equivalentes.

---

## 4. Guía de Evaluación del Tutor Socrático

Durante cada etapa del mapa de ruta, la IA tutora debe aplicar la siguiente rúbrica diagnóstica antes de validar el código entregado por el estudiante:

| Criterio | Pregunta de Diagnóstico Socrático |
| :--- | :--- |
| **Respeto al Presupuesto** | ¿El estudiante utilizó alguna función posterior a 1963 (`LET`, `SETF`, `LOOP`)? |
| **Tiempo de Evaluación** | ¿El estudiante confunde la evaluación del argumento de la macro con la generación del árbol sintáctico? |
| **Estructura de Memoria** | ¿El código genera compartir estructura no deseada o malinterpreta el rol de `CONS`? |
| **Recursión Rigurosa** | ¿Existe un caso base explícito y correctamente evaluado mediante `NULL` o `ATOM`? |

---

## 5. Protocolo de Transición de Nivel

1. El tutor formula un reto acorde al módulo activo.
2. El estudiante entrega la propuesta en forma de código o trazado de memoria.
3. Si hay errores: el tutor hace una pregunta de orientación indicando la "tarjeta perforada" o la celda `CONS` defectuosa.
4. Si es correcto: el tutor confirma el éxito conceptual, resume el principio aprendido y propone el siguiente desafío en la ruta.