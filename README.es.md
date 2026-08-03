<!-- hide -->
<div align="center">

# Modelado de Datos Intermedio con Diagramas de Clases

[![Certificado por 4Geeks Academy](https://img.shields.io/badge/certificado_por-4Geeks_Academy-2563eb)](https://4geeks.com)
[![Funciona con LearnPack](https://img.shields.io/badge/funciona_con-LearnPack-2563eb)](https://learnpack.co)
[![Abrir en Codespaces](https://img.shields.io/badge/abrir_en-Codespaces-fb5a1f)](https://codespaces.new/4GeeksAcademy/intermediate-data-modeling-class-diagrams)

</div>

*Estas instrucciones también están disponibles en [inglés / English](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/blob/HEAD/README.md).*

<!-- endhide -->

Este tutorial es una práctica guiada de 12 pasos en la que construyes un único diagrama de clases acumulativo para una plataforma de cursos online dentro de [diagram.4geeks.com](https://diagram.4geeks.com/). Modelas 9 clases — `Course`, `Student`, `Instructor`, `Lesson`, `Enrollment`, `StudentProfile`, `Category`, `Certificate` y `Review` — unidas por 9 relaciones tipadas que cubren cardinalidades 1:1, 1:N, N:M y opcional 0..1. Dura unas 3 horas y no requiere escribir código.

<!-- hide -->

## 📋 Sobre este tutorial

- **Dificultad:** intermedia
- **Duración estimada:** 3 horas
- **Pasos:** 13 carpetas — 1 de bienvenida y 12 pasos numerados de modelado (`01` a `12`)
- **Tecnologías:** diagramas de clases UML, modelado de datos, [diagram.4geeks.com](https://diagram.4geeks.com/), sintaxis `classDiagram` de Mermaid
- **Corrección:** ninguna automática — no hay ficheros de test y `learn.json` declara `no_delivery`; te autocorriges comparando con el modelo de referencia del paso 12
- **Idiomas:** español e inglés (`README.es.md` y `README.md` en cada paso)
- **Entorno:** LearnPack `5.0.348` sobre un devcontainer de Node.js 22, o simplemente leyendo los pasos en GitHub

<!-- endhide -->

## 🎯 ¿Qué vas a aprender?

Al terminar los 12 pasos vas a saber:

- Convertir la descripción de un producto en lenguaje natural en **clases con atributos de tipo explícito** (`int`, `string`, `boolean`, `date`).
- Distinguir las tres cardinalidades que aparecen en casi cualquier esquema real: **uno a uno**, **uno a muchos** y **muchos a muchos**.
- **Resolver una relación muchos a muchos con una clase intermedia** en lugar de con una línea suelta. Es el reflejo de modelado más útil de toda la práctica y aquí lo aplicas dos veces: con `Enrollment` y con `Review`.
- Expresar una **relación opcional** (`0..1`) para registros que solo existen si se cumple una condición, como el certificado que se emite tras completar una matrícula.
- Sortear las limitaciones de una herramienta real: si no hay tipo enumerado, la respuesta correcta es una propiedad `string` acompañada de una nota que documente los valores, no quedarse bloqueado.
- Leer y escribir un `classDiagram` de Mermaid, que es el formato de texto en el que está la solución de referencia del paso 12.

## 👀 ¿Qué vas a construir?

Un solo diagrama que va creciendo. Nada se descarta entre pasos: el lienzo del paso 12 es el mismo que abriste en el paso 01.

- **00 - Bienvenida.** Cómo funciona la práctica, qué admite y qué no admite el editor, y dónde vas a dibujar.
- **01 - Entidad Course.** Clase `Course` con `id` (`int`), `title` (`string`) y `description` (`string`).
- **02 - Entidad Student.** Clase `Student` con `id`, `name` y `email`. Todavía sin ninguna relación, y es a propósito.
- **03 - Entidad Instructor.** Clase `Instructor` con `id`, `name` y `bio`. Tres clases sueltas en el lienzo.
- **04 - Cursos del instructor.** Tu primera relación: un enlace 1:N de `Instructor` a `Course`, con `1` y `N` escritos como etiquetas de texto en los extremos y una etiqueta opcional `teaches` sobre la línea.
- **05 - Lecciones.** Clase `Lesson` con `id`, `title`, `durationMinutes` y `orderIndex`, enlazada 1:N desde `Course` (etiqueta opcional `contains`).
- **06 - Asociación Enrollment.** El paso del muchos a muchos. La clase `Enrollment`, con `id` y `enrolledAt` (`date`), se coloca en medio: `Student` 1 — N `Enrollment` y `Enrollment` N — 1 `Course`. Trazar una línea directa `Student`–`Course` está explícitamente prohibido aquí.
- **07 - Progreso y estado de la matrícula.** Amplías `Enrollment` con `progressPercent` (`int`, de 0 a 100) y `status` (`string`, con los valores documentados `active`, `completed` y `dropped`).
- **08 - Perfil del estudiante uno a uno.** Clase `StudentProfile` con `id`, `avatarUrl` y `timezone`, enlazada 1:1 con `Student` para que la entidad principal no se infle.
- **09 - Categorías.** Clase `Category` con `id`, `name` y `slug`, enlazada 1:N con `Course`. En este modelo simplificado cada curso pertenece a una sola categoría.
- **10 - Certificado.** Clase `Certificate` con `id`, `issuedAt` (`date`) y `certificateCode` (`string`), colgada de `Enrollment` con cardinalidad `1` — `0..1`.
- **11 - Reseñas.** Clase `Review` con `id`, `rating` (`int`), `comment` (`string`) y `createdAt` (`date`), conectada como `Student` → `Review` → `Course`. A estas alturas tienes al menos seis clases distintas en el lienzo.
- **12 - Modelo final.** Comparas tu diagrama con el `classDiagram` de Mermaid de referencia (9 clases y 9 enlaces) y respondes tres preguntas de discusión sobre enumerados, cursos con varios instructores y por qué `Review` merece ser su propia clase.

## 🎓 ¿Qué necesitas antes de empezar?

- **Ningún lenguaje de programación.** No se compila ni se ejecuta nada. Aquí se dibuja, no se programa.
- **Un navegador** y [diagram.4geeks.com](https://diagram.4geeks.com/), la herramienta de dibujo que se usa de principio a fin. Mantén un único diagrama abierto desde el paso 01 hasta el 12.
- **Una noción básica de qué es una clase**: una cosa con nombre y con propiedades. Haber tocado programación orientada a objetos ayuda, pero no es obligatorio.
- **Opcionalmente, una cuenta de GitHub** para abrir el repositorio en Codespaces y seguir los pasos dentro de LearnPack. Leer los `README.es.md` de cada paso directamente en GitHub funciona igual de bien.
- **Opcionalmente, Node.js 22 y LearnPack** si prefieres trabajar en tu propia máquina.

## ✅ ¿Cómo se corrige si no hay tests?

Conviene tenerlo claro desde el principio: **este paquete no tiene corrección automática**. Cada una de las 13 carpetas de ejercicio contiene exactamente dos ficheros, `README.md` y `README.es.md`. No hay ficheros de test, ni soluciones, ni rúbrica, y `learn.json` declara el formato de entrega como `no_delivery`, así que no se sube nada a ninguna parte.

La corrección la haces tú, y el paquete te da tres apoyos para hacerla bien:

- **Una lista de comprobación de dos puntos al final de los pasos 01 a 11**, con condiciones concretas que confirmar antes de avanzar; por ejemplo, que la cardinalidad aparezca escrita en ambos enlaces. El paso de bienvenida y el modelo final no la llevan.
- **El `classDiagram` de Mermaid de referencia del paso 12**, que detalla las 9 clases con sus atributos y las 9 relaciones con sus cardinalidades.
- **Tu propio criterio sobre qué cuenta como equivalente.** La distribución, los colores y la redacción exacta de las etiquetas pueden diferir del modelo de referencia y aun así ser correctos. Lo que sí tiene que coincidir es el conjunto de entidades, los tipos de las propiedades y la cardinalidad escrita en cada enlace.

Cuando tu diagrama te convenza, marca el paso como completado a mano en LearnPack. Exportar un PNG para tus apuntes es opcional y solo para ti.

## 💡 ¿Qué errores conviene evitar?

- **Empezar un diagrama nuevo en cada paso.** El modelo es acumulativo. El paso 02 pide explícitamente conservar `Course` del paso 01, y el 03 pide conservar los dos anteriores.
- **Unir `Student` con `Course` de forma directa.** El paso 06 lo prohíbe: el muchos a muchos tiene que pasar por `Enrollment`, y el mismo patrón se repite con `Review` en el paso 11.
- **Añadir relaciones antes de tiempo.** Los pasos 02 y 03 dejan las clases sin conectar a propósito. Aguanta las ganas.
- **Dejar propiedades sin tipo.** Cada clase que añades llega con una tabla de propiedades y tipos en las instrucciones, y la mayoría de las listas de comprobación te piden confirmar que esos tipos se ven. No basta con `title`, tiene que verse como `string`.
- **Buscar un tipo enumerado para `status`.** La herramienta no lo necesita. `status: string` más una nota corta con `active`, `completed` y `dropped` es exactamente la respuesta esperada en el paso 07.
- **Colgar el certificado directamente del estudiante.** El paso 10 pide enlazar `Certificate` con `Enrollment` y evitar una línea duplicada estudiante–certificado, porque lo que se completa es la matrícula.
- **Meter `rating` dentro de `Enrollment`.** Una reseña es un hecho aparte, con su propia fecha y su comentario: justo la tercera pregunta de discusión del paso 12.
- **Esperar notación UML estricta.** Este editor trabaja con cajas de clase, propiedades tipadas y etiquetas de texto. La cardinalidad se escribe como `1`, `N`, `*` o `0..1` sobre el conector, no con puntas de flecha especiales ni rombos de composición.

## ❓ Preguntas frecuentes

### ¿Hace falta saber programar para hacer este tutorial?

No. En los 12 pasos no hay código fuente, ni lenguaje que instalar, ni nada que ejecutar. Basta con entender la idea de clase con propiedades, que se explica en el paso de bienvenida. Tener experiencia programando hace que el vocabulario suene familiar, pero el ejercicio es puramente de modelado.

### ¿Con qué herramienta se dibujan los diagramas?

Con [diagram.4geeks.com](https://diagram.4geeks.com/), un editor de diagramas que funciona en el navegador. Ofrece cajas de clase con atributos tipados, enlaces entre clases y etiquetas de texto libre sobre esos enlaces. Abre un diagrama al principio y ve añadiendo sobre él: cada paso parte del lienzo anterior.

### ¿Hay corrección automática o algún archivo que entregar?

Ni lo uno ni lo otro. `learn.json` fija el formato de entrega en `no_delivery` y ninguna carpeta de ejercicio incluye tests. Comparas tu resultado con el modelo de referencia del paso 12 y marcas la práctica como completada tú mismo.

### ¿En qué se diferencia un diagrama de clases de un diagrama entidad-relación?

Un diagrama de clases UML describe clases de software orientado a objetos: atributos, operaciones y relaciones entre objetos. Un diagrama entidad-relación describe tablas, columnas y claves de una base de datos relacional. Para modelar datos se solapan muchísimo — entidades, atributos y cardinalidad se ven casi igual — y por eso esta práctica se traduce sin fricción a un esquema de base de datos aunque nunca mencione SQL.

### ¿Cómo se modela una relación muchos a muchos?

Poniendo una clase en medio. En lugar de unir `Student` y `Course` con una sola línea, añades `Enrollment`, enlazas `Student` 1 — N `Enrollment` y `Enrollment` N — 1 `Course`, y le das a `Enrollment` sus propios atributos: `enrolledAt`, `progressPercent` y `status`. Esos atributos son la razón de ser de la clase intermedia, porque pertenecen a la pareja y no a ninguno de los dos lados.

### ¿Puedo saltarme pasos o hacerlos en otro orden?

LearnPack te deja navegar libremente, pero los pasos son acumulativos. El paso 07 amplía la clase creada en el 06, y el 10 también se apoya en ella. Si te adelantas, vuelve atrás y añade las clases que falten; si no, la comparación con la referencia del paso 12 no te va a cuadrar.

<!-- hide -->

## 📝 Tutoriales relacionados

Si los diagramas de clases te han dejado con ganas de ver cómo esas clases se convierten en código real, estos tutoriales interactivos son la continuación natural:

- [Aprende Programación Orientada a Objetos con Python](https://4geeks.com/es/interactive-exercise/aprende-programacion-orientada-a-objetos-con-python)
- [Programación Orientada a Objetos en JavaScript](https://4geeks.com/es/interactive-exercise/object-oriented-programing-in-javascript-es)
- [Aprende las Mejores Prácticas de Python](https://4geeks.com/es/interactive-exercise/aprende-las-mejores-practicas-de-python)

## 🚀 Cómo empezar

La vía más rápida es GitHub Codespaces, que no requiere instalar nada en tu ordenador.

1. Abre el repositorio en [GitHub Codespaces](https://codespaces.new/4GeeksAcademy/intermediate-data-modeling-class-diagrams) y crea un codespace sobre la rama `main`.

2. Espera a que termine de construirse el contenedor. Instala LearnPack `5.0.348` de forma global sobre una imagen de Node.js 22 y añade la extensión de LearnPack para VS Code automáticamente.

3. Arranca el tutorial:

    ```bash
    learnpack start
    ```

4. Abre [diagram.4geeks.com](https://diagram.4geeks.com/) en otra pestaña, crea un diagrama nuevo y mantenlo abierto durante toda la práctica.

5. Sigue los pasos en orden, de `00-welcome` a `12-final-model`.

## 💻 Instalación local

Si prefieres trabajar en tu propia máquina:

1. Instala [Node.js](https://nodejs.org/en/download) 22 o superior.

2. Instala LearnPack de forma global, fijando la versión con la que se construyó este paquete:

    ```bash
    npm i @learnpack/learnpack@5.0.348 -g
    ```

3. Clona el repositorio y entra en la carpeta:

    ```bash
    git clone https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams.git
    cd intermediate-data-modeling-class-diagrams
    ```

4. Arranca LearnPack:

    ```bash
    learnpack start
    ```

También puedes saltarte todo lo anterior y leer directamente los pasos de la carpeta [`exercises`](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/tree/HEAD/exercises), porque las instrucciones son todo el contenido del paquete.

## 📚 Cómo están organizados los ejercicios

Cada paso vive en su propia carpeta dentro de [`exercises`](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams/tree/HEAD/exercises), con un prefijo numérico que marca el orden: `00-welcome`, `01-course-entity`, `02-student-entity` y así hasta `12-final-model`.

Cada carpeta contiene exactamente dos ficheros:

- `README.es.md` — las instrucciones en español
- `README.md` — las mismas instrucciones en inglés

Dentro de las carpetas no hay soluciones, ni tests, ni configuración. Un paso típico se compone de un **Escenario** breve, unas **Instrucciones**, una **Lista de comprobación** de dos puntos y un enlace al paso siguiente. El paso 12 añade el [diagrama de clases de Mermaid](https://mermaid.js.org/syntax/classDiagram.html) de referencia y tres preguntas de discusión.

## 🤝 Contribuidores

Creado por [@ehiber](https://github.com/ehiber) y contribuidores de [4Geeks Academy](https://4geeksacademy.com/).

Este repositorio no incluye fichero LICENSE, así que por defecto todos los derechos están reservados. El acceso al tutorial no cuesta nada y los diagramas que produzcas son tuyos, pero el contenido didáctico no se publica bajo una licencia de código abierto.

¿Has visto una errata, un paso roto o un detalle de modelado que se podría explicar mejor? Abre un issue o un pull request en [el repositorio](https://github.com/4GeeksAcademy/intermediate-data-modeling-class-diagrams): estos materiales se mantienen de forma colaborativa.

<!-- endhide -->
