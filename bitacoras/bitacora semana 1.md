# Semana 1 — Guía del Estudiante

## Modelado Conceptual y Diseño Entidad-Relación (2.1–2.8)

### Caso hilo conductor: DataLab

\---

## Objetivos de la semana

Al final de esta semana estarán en capacidad de:

* Explicar qué es el diseño conceptual y por qué es independiente del motor de base de datos.
* Diferenciar los niveles de modelado: conceptual, lógico, físico.
* Aplicar la notación del modelo entidad-relación de Chen.
* Clasificar entidades, atributos y relaciones a partir de un enunciado en lenguaje natural.
* Determinar cardinalidad y participación, justificando con base en el enunciado.
* Diferenciar llave candidata de llave primaria y justificar la elección.
* Usar una herramienta de modelado para documentar un diagrama E-R.
* Entregar el modelo E-R completo de DataLab — **Hito 1** del semestre.

**Equipo:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ **Integrantes:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

\---

## El caso: DataLab

> DataLab es la plataforma interna que usa un equipo de ciencia de datos para llevar el control de sus proyectos de inteligencia artificial. Cada científico de datos del equipo puede participar en uno o varios proyectos, y cada proyecto agrupa el trabajo alrededor de un problema de negocio concreto (por ejemplo, "Detección de fraude en transacciones" o "Clasificación de imágenes médicas"). Para resolver un proyecto, el equipo se apoya en datasets: conjuntos de datos con un nombre, una fuente (interna o externa), una fecha de carga y un tamaño en filas; un mismo dataset puede reutilizarse en varios experimentos, incluso de proyectos distintos. Dentro de cada proyecto se ejecutan experimentos: cada experimento usa un dataset, fue ejecutado por un científico de datos del equipo, tiene una fecha de ejecución y una configuración (los hiperparámetros usados en esa corrida). Cuando un experimento resulta exitoso, produce un modelo entrenado, identificado por un nombre, una versión y un algoritmo (por ejemplo, "Random Forest" o "Red neuronal convolucional"). Cada modelo se evalúa con una o varias métricas de desempeño (accuracy, precisión, F1-score, entre otras), cada una con su valor numérico y la fecha en que fue calculada.

Este será el caso que van a construir, capa sobre capa, durante todo el semestre. Todo lo que hagan hoy lo van a volver a tocar en las próximas 13 semanas.

\---

## BLOQUE 1 — Laboratorio (3 horas, con PC)

### Hito 0 — Preparar el repositorio (15 min)

1. Formen su equipo (3-4 integrantes).
2. Creen el repositorio `datalab-<equipo>` con esta estructura:

```
datalab-<equipo>/
├── README.md
├── .gitignore
├── diagramas/e-r/
├── scripts/{ddl,dml,consultas}/
├── casos\_uso/
├── documentacion/
├── mongodb/
└── bitacoras/
```

3. Primer commit: `git commit -m "modelo: estructura inicial del repositorio"`.
4. Den acceso de lectura al docente.

### Actividad 1 — Lectura y extracción cruda (30 min)

**Sin dibujar nada todavía**, respondan en su bitácora (`bitacoras/s01-<nombre>.md`):

**a)** ¿De qué "cosas" del negocio de DataLab se necesita guardar información? Listen todas las que encuentren, en sus propias palabras.



Científicos de datos del equipo.



**b)** ¿Qué preguntas le harían al equipo de ciencia de datos antes de empezar a modelar?



¿Qué información necesita analizar el negocio?



**c)** Reto Feynman: expliquen en voz alta a su compañero de equipo qué es un "Experimento" en DataLab, **sin usar la palabra "entidad"**. Si se traban, ahí hay algo que todavía no tienen claro — vuelvan al enunciado antes de seguir.



Un experimento es una ejecución realizada dentro de un proyecto. Utiliza un dataset, es ejecutado por un científico de datos y registra la fecha de ejecución y la configuración o hiperparámetros utilizados. Si tiene éxito, puede producir un modelo entrenado.



### Actividad 2 — Primer boceto (45 min)

Abran una herramienta de modelado (ERDPlus o draw.io recomendadas). Construyan su primer intento de diagrama E-R con lo que identificaron en la Actividad 1: entidades, algunos atributos, relaciones. No se preocupen por que quede perfecto — este es un primer boceto exploratorio.

**Herramienta usada:** \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

### Descanso (15 min)

### Actividad 3 — Puesta en común (45 min)

Van a proyectar su boceto ante el resto del curso. Mientras ven los bocetos de los demás equipos, anoten:

**a)** ¿En qué se parece su boceto al de otros equipos?

\---

**b)** ¿En qué se diferencia? ¿Alguna diferencia les genera dudas sobre cuál versión es la correcta?

\---

**c)** Preguntas abiertas que les quedan después de ver otros bocetos:

\---

\---

### Actividad 4 — Commit del boceto (30 min)

1. Exporten su boceto como imagen a `diagramas/e-r/s01-boceto-inicial.png`.
2. Commit: `git commit -m "modelo: boceto inicial del diagrama E-R de DataLab"`.
3. Escriban en `documentacion/decisiones.md` las preguntas abiertas de la Actividad 3 — las van a resolver en la sesión de formalización.

\---

## BLOQUE 2 — Formalización (2 horas, sin PC)

### Retomando las preguntas abiertas

Antes de seguir, revisen la lista de preguntas abiertas que dejaron en `documentacion/decisiones.md`. El docente va a resolverlas junto con ustedes en esta sesión — guárdenlas a la vista.

### Niveles de modelado — verificación rápida

Clasifiquen cada frase como **conceptual**, **lógico** o **físico**:

|Frase|Nivel|
|-|-|
|"Un experimento puede producir, como máximo, un modelo"|Conceptual|
|"La tabla EXPERIMENTO tiene una llave foránea id\_dataset"|Logico|
|"La columna fecha\_ejecucion es de tipo DATE"|Fisico|

### Corrección del boceto con notación de Chen

Con la explicación del docente, corrijan en papel su propio boceto de la Actividad 2. Marquen con un color los cambios respecto al boceto original — esa comparación es la evidencia de lo que aprendieron hoy.

**Preguntas guía para la corrección:**

**a)** ¿`algoritmo` en su boceto quedó como atributo o como entidad? Si quedó como entidad, ¿por qué debería ser atributo de MODELO?

\---

**b)** ¿DATASET es una entidad fuerte o débil en su modelo? Justifiquen.

\---

**c)** ¿EXPERIMENTO quedó modelado como entidad o como relación en su boceto original? Si quedó como relación, ¿qué atributos propios tiene que solo tienen sentido si EXPERIMENTO es entidad?

\---

### Cardinalidad y participación

Para cada relación, determinen la cardinalidad (1:1, 1:N o N:M) y la participación (total o parcial) de cada lado, con una frase que lo justifique:

|Relación|Cardinalidad|Participación (¿por qué?)|
|-|-|-|
|CIENTIFICO\_DATOS – participa en – PROYECTO|N:M|Cada científico puede participar en uno o varios proyectos y cada proyecto agrupa el trabajo del equipo.|
|DATASET – se usa en – EXPERIMENTO|1:N|Un dataset puede reutilizarse en varios experimentos, mientras que cada experimento usa un dataset.|
|EXPERIMENTO – produce – MODELO|1:0..1|Un experimento puede no producir un modelo si no resulta exitoso; cuando resulta exitoso, produce un modelo.|
|MODELO – se evalúa con – METRICA|N:M|Cada modelo se evalúa con una o varias métricas y una métrica puede utilizarse para evaluar distintos modelos.|

**Ejercicios rápidos — otros contextos de datos e IA:**

**a)** *Pipeline de anotación de datos:* "Un anotador etiqueta imágenes; cada imagen puede ser revisada por un segundo anotador antes de aprobarse." ¿Cardinalidad y participación entre ANOTADOR e IMAGEN?

\---

**b)** *Plataforma de MLOps:* "Un modelo en producción puede desplegarse en varios ambientes (staging, producción); cada despliegue tiene su propia fecha y versión de infraestructura." ¿MODELO–DESPLIEGUE es 1:N o N:M? ¿Por qué?

\---

### Llaves primarias y candidatas

La entidad EXPERIMENTO tiene los atributos: `id\_experimento\_interno`, `nombre\_experimento`, `fecha\_ejecucion`, `configuracion`.

**a)** ¿Cuál es la llave candidata más evidente?

\---

**b)** ¿Por qué `nombre\_experimento` no sirve como llave por sí sola?

\---

**c)** Ahora identifiquen las llaves candidatas y primarias de las otras 5 entidades de DataLab:

|Entidad|Llave(s) candidata(s)|Llave primaria elegida|Justificación|
|-|-|-|-|
|CIENTIFICO\_DATOS|Identificador del científico de datos|Identificador del científico de datos|Permite distinguir individualmente a cada científico.|
|PROYECTO|Identificador del proyecto|Identificador del proyecto|Permite identificar cada proyecto de manera única.|
|DATASET|Identificador del dataset|Identificador del dataset|Permite distinguir cada conjunto de datos.|
|MODELO|Identificador del modelo|Identificador del modelo|Permite identificar de forma única cada modelo entrenado.|
|METRICA|Identificador de la métrica|Identificador de la métrica|métrica<br />Permite identificar cada registro de métrica.|

\---

## Entregable — Hito 1 (antes de la Semana 2)

* \[ ] Diagrama E-R final y corregido en `diagramas/e-r/s01-modelo-final.png` (o enlace de la herramienta).
* \[ ] Diccionario de datos completo en `documentacion/diccionario\_datos.md` (entidad, atributo, tipo de atributo, llave candidata/primaria).
* \[ ] Todas las decisiones de diseño discutidas hoy, registradas en `documentacion/decisiones.md`.
* \[ ] Commit final: `git commit -m "modelo: diagrama E-R final de DataLab (Hito 1)"`.
* \[ ] Tag: `git tag h1-modelo-er`.

**Recuerden:** el historial de commits de hoy (boceto → correcciones → versión final) es evidencia de su proceso, no solo del resultado. No lo aplasten en un único commit al final.

