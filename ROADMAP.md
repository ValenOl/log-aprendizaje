# Roadmap AI Engineer (v2)

Creado: 2026-10-27. Reemplaza al roadmap por fases con ejercicios sueltos.

## Idea central

Un proyecto real como columna vertebral: **recordatorios**, un asistente de cobranza
por WhatsApp para una tienda (recordatorio de vencimiento + clasificación de la
respuesta del cliente con Gemini). Cada tema de fundamentos se aprende cuando el
proyecto lo necesita, no en un ejercicio aparte.

`reglamento-futbol` queda como segundo proyecto, para RAG (Hito 3).

## Pedagogía

Objetivo doble: entender lo que construyo y poder escribir código desde cero en una
entrevista técnica con live coding.

### 1. PRIMM completo en cada pieza

1. **Predict:** especifico en palabras qué hace la pieza y, cuando ya existe el código, predigo qué va a hacer antes de correrlo.
2. **Run:** lo corro y comparo con mi predicción.
3. **Investigate:** lo explico línea por línea, como en una entrevista.
4. **Modify:** hago un cambio chico a mano o encuentro un bug plantado.
5. **Make:** escribo algo parecido desde cero, sin IA. Este paso no se saltea.

### 2. Fading: la IA escribe cada vez menos

El nivel se lleva por tema, no por calendario.

| Nivel | Quién escribe | Cómo se ve |
|---|---|---|
| 1. Ejemplo resuelto | La IA escribe todo; yo predigo y explico | Código completo para leer |
| 2. Completar | La IA deja la función vacía con su test; yo la lleno | Firma + test + `pass` |
| 3. Crear | Escribo todo; la IA solo revisa | Hoja en blanco |

Paso al nivel siguiente de un tema cuando apruebo su checkpoint "explicalo sin mirar".
Los ejemplos resueltos ayudan al principio y estorban cuando ya sé el tema
(expertise reversal), por eso el nivel 1 no es permanente.

### 3. Recuperación espaciada con el proyecto

- Los primeros 10 minutos de cada sesión: reescribo sin mirar algo de la sesión anterior.
- Repito lo mismo al día siguiente y a la semana.
- Ejemplo: reescribir el CRUD de cero (`servidor2.ts`, 2026-10-26).

### 4. Live coding semanal

- Una sesión por semana, 45 minutos, sin IA, con cronómetro y pensando en voz alta.
- Mitad problemas del proyecto (fechas, agrupar deudas, parsear mensajes), mitad problemas clásicos fáciles.
- Al terminar: anoto en el log qué me trabó.

### Regla para la IA

En nivel 3, en el paso Make y en live coding, la IA da pistas, nunca la solución.

### Cierre de cada hito

Checkpoint "explicalo sin mirar". Lo que no sale sin apuntes vuelve a la lista del
hito. Un hito se cierra con evidencia, no con "ya lo sé".

### Evidencia

- PRIMM: evidencia modesta pero positiva (Sentance, Waite y Kallia 2019; réplica chica en Italia, 2023).
- Ejemplos resueltos con fading: evidencia fuerte, sobre todo en matemática y física (Sweller; Renkl y Atkinson).
- Recuperación espaciada con IA: estudios chicos y recientes.

## Rutina

- **Lunes a viernes:** dos bloques por día (10 min de repaso sin mirar + proyecto, y proyecto + entrada del log).
- **Sábado:** live coding de 45 min sin IA y repaso de la semana.
- **Domingo:** descanso.

## Hitos

Total estimado: ~280 h. A unas 26 h por semana son unas 11 semanas.

### Hito 0 — Cierre del setup (3 h)

- [x] `uv` en recordatorios (reemplaza `requirements.txt`).
- [x] Primera entrada en `log-aprendizaje/entradas/`.
- [x] Rutina fija: días y horario de estudio por semana.

**Checkpoint:** qué es el PATH y qué hace un entorno virtual.

### Hito 1 — Python sólido (40 h)

- [x] Type hints en todo el proyecto y chequeo con un type checker.
- [x] Diccionarios: cómo funciona una tabla hash y por qué buscar por clave es rápido.
- [x] Excepciones: qué pasa cuando Gemini falla o no responde, cómo se propagan y dónde se atrapan.
- [x] Tests con pytest para todo lo que no llama a la IA (fechas, mensajes).
- [x] Separar el código en módulos con responsabilidades claras.

**Entregable:** recordatorios corre de punta a punta desde una función `main` y no se
cae si la API falla.
**Checkpoint:** explicar tablas hash, propagación de excepciones y para qué sirven los type hints.

### Hito 2 — Ingeniería de software (45 h)

- [ ] Guardar clientes, deudas y respuestas en SQLite (reutilizar lo practicado en `Ideas`).
- [ ] API con FastAPI: recibir el mensaje del cliente y devolver la clasificación.
- [ ] Git con ramas y pull requests propios, aunque trabaje solo.
- [ ] Docker: imagen del proyecto y contenedor corriendo.
- [ ] Diagrama simple de la arquitectura.

**Entregable:** `docker run` levanta la API.
**Checkpoint:** diferencia entre imagen y contenedor, y entre commit, push y merge.

### Hito 3 — LLM Engineering (45 h)

- [x] Structured output con esquema pydantic (hecho 2026-10-27).
- [x] Primer eval del clasificador, 7/7 (hecho 2026-10-27).
- [ ] Eval más grande: 3 o 4 frases distintas por intención, incluidas las ambiguas.
- [ ] Tool calling: que el modelo pueda consultar la deuda del cliente. Entender quién ejecuta la herramienta.
- [ ] Guardrails: qué hacer si el cliente insulta, manda datos sensibles o intenta manipular al bot.
- [ ] RAG en `reglamento-futbol`: embeddings, búsqueda y respuesta con fuentes.

**Checkpoint:** quién ejecuta una tool call, qué es un embedding y por qué un eval que
copia las frases del prompt no mide nada.

### Hito 4 — Fundamentos de ML (60 h)

Se aprende midiendo el clasificador propio.

- [ ] Matriz de confusión, precision y recall por intención.
- [ ] Separar datos de desarrollo y de prueba. Overfitting con el ejemplo propio:
      definir una categoría copiando la frase del test.
- [ ] Clasificador clásico con scikit-learn como base de comparación contra Gemini.
- [ ] Cuándo conviene fine-tuning y cuándo alcanza con prompt y ejemplos.

**Entregable:** reporte comparando Gemini contra el modelo clásico (aciertos, costo, latencia).
**Checkpoint:** explicar overfitting, precision y recall con números del propio eval.

### Hito 5 — Producción (40 h)

- [ ] Deploy en Cloud Run (ya hay proyecto en GCP).
- [ ] Logs y métricas: costo por mensaje, latencia y errores.
- [ ] Reintentos y límites de uso.
- [ ] Integración con WhatsApp en modo de prueba.

**Entregable:** URL pública que recibe un mensaje y responde.
**Checkpoint:** qué pasa en el sistema cuando llegan 100 mensajes juntos.

### Hito 6 — Portfolio y entrevistas (50 h, en paralelo desde hoy)

- [ ] Una entrada del log por semana, como mínimo.
- [ ] README de recordatorios con demo, arquitectura y resultados del eval.
- [ ] Banco de preguntas de entrevista armado con los checkpoints de cada hito.
- [ ] Live coding semanal (ver Pedagogía, punto 4): una entrada corta en el log por sesión.

## Progreso

| Hito | Horas | Estado |
|---|---|---|
| 0 Setup | 3 | Hecho |
| 1 Python | 40 | En curso (falta checkpoint) |
| 2 Ingeniería de software | 45 | Pendiente |
| 3 LLM Engineering | 45 | Empezado (2 de 6) |
| 4 Fundamentos de ML | 60 | Pendiente |
| 5 Producción | 40 | Pendiente |
| 6 Portfolio | 50 | En paralelo |
