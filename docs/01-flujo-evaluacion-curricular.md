# Flujo 01 · Evaluación alineada al currículo oficial

> Documento de trabajo · v2 · 28-09-2026
> Diagrama editable: [`flujos/Evalia_flujo_01_v2.drawio`](flujos/Evalia_flujo_01_v2.drawio) (abrir en [app.diagrams.net](https://app.diagrams.net) o con la extensión Draw.io de VS Code)
> Reemplaza la versión 1 (`Evalia_flujo_01_curriculo_evaluacion.drawio`, que tenía 26 componentes y 16 transiciones).

## 1. Qué cambia respecto de la v1

| v1 | v2 |
|---|---|
| 4 carriles por **etapa** | 5 carriles por **rol** (centro, docente/tutor, servicios Evalia, estudiante, apoderado) × 8 **fases** (A–H) |
| Un solo diagrama | 4 páginas: flujo por rol · modelo curricular · visibilidad por rol · estados |
| Gobernanza como columna lateral | Capa transversal con la normativa concreta de cada país |
| Tutor independiente implícito | Entrada explícita (D0): cuenta sin centro, que declara país, nivel y grupo |
| Consentimiento mencionado | Consentimiento como **condición de acceso** (A0 → E0) y guardado en cada intento |
| Corrección IA genérica | Corrección asistida con confianza; las preguntas abiertas **nunca** se publican sin el docente (S6 → D6) |
| — | V°B° opcional de coordinación / UTP (C4), activado por política del centro |

## 2. Diagnóstico del prototipo actual (repo `evalia`)

Lo que ya existe en `index.html` (versión METIS):

- Wizard de creación: idea en texto libre, archivos adjuntos y **4 chips genéricos**: *12 preguntas · Secundaria · Dificultad media · Español*.
- Esquema editable con 12 bloques, tipos de pregunta (única, múltiple, abierta) y cita de la fuente.
- Toma de la prueba con temporizador, chat con el tutor (voz simulada) y avatar.
- Compartir por link, QR y WhatsApp. Reportes con datos de ejemplo.

Brechas respecto del flujo 01:

1. **No existe contexto curricular.** El modelo de datos (`evalia-prompt.md`) no tiene país, curso, asignatura ni objetivo; `Exam.subject` es texto libre y `difficulty` es Básico/Intermedio/Avanzado.
2. **No hay roles ni organizaciones.** No existen `Organization`, `Course`, `Enrollment` ni `Guardian`; el estudiante entra por link.
3. **Sin trazabilidad al objetivo.** `Question.sourceCitation` apunta al material, no a un OA ni a una habilidad.
4. **La política del tutor no se puede configurar.** El comportamiento del agente está hardcodeado; no hay niveles de ayuda por ítem (sí están priorizados en `metis-iteration-1.md`).
5. **No hay revisión humana en la corrección** ni estados de publicación o versionado.
6. **Persistencia en `localStorage`**: sirve para una demo, pero no para datos de menores.

**Cambio mínimo en el demo** (para que Ariel pueda avanzar en local): reemplazar los chips por un selector encadenado *País → Curso → Asignatura → Unidad/Eje → Objetivos*, alimentado por un JSON de piloto (ver `02-modelo-curricular-cl-cr.md` §5), y mostrar en cada bloque del esquema el objetivo que evalúa.

## 3. Pasos del flujo

La numeración coincide con el diagrama. Cada paso es una **épica o historia candidata**.

### A · Alta y acceso
- **C1 Alta del centro**: país, identificador oficial (RBD en CL / código del centro en CR), dependencia, modalidad, jornada, calendario y plan de estudios adoptado.
  *Criterio:* un centro pertenece a un solo país; el país determina los marcos curriculares disponibles.
- **D0 Cuenta docente o tutor**: si el docente tiene centro, lo invitan y hereda el contexto. Si es independiente, declara país y nivel y crea su propio grupo.
- **E0 Cuenta estudiante**: la crea el centro o llega por invitación. Un menor de edad no puede iniciar un intento sin consentimiento vigente.
- **A0 Vinculación y consentimiento**: autorización verificable del responsable, que puede revocarla. Se registra quién, cuándo, con qué alcance y con qué evidencia.

### B · Curso y ruta curricular
- **C2 Estructura académica**: cursos y secciones, docentes, matrícula (CSV o SSO), vínculo estudiante ↔ responsable y apoyos (PIE en CL / apoyos educativos en CR).
- **S1 Catálogo curricular versionado**: modelo canónico con adaptador por país. El origen puede ser un catálogo propio, una API externa (p. ej. la plataforma de Orlando) o una carga manual.
- **D1 Elegir curso y ruta curricular**: el curso hereda país, nivel y marco vigente; el docente elige asignatura → unidad/eje/área → objetivos. Ve los indicadores oficiales y puede agregar los suyos.
  *Criterio:* nunca se muestra un objetivo sin su fuente y su versión.

### C · Diseño (blueprint)
- **C3 Políticas institucionales**: uso permitido de IA, nivel máximo de ayuda, escala (CL 1,0–7,0 / CR 1–100), retención y si el centro exige V°B°.
- **D2 Blueprint / tabla de especificaciones**: propósito (diagnóstica, formativa o sumativa), la matriz *objetivo × habilidad cognitiva × peso × n.º de ítems*, tipos de ítem, tiempo, exigencia, adecuaciones, material propio y política de ayuda por defecto.
- **S2 Asistente de blueprint**: sugiere la distribución, valida la cobertura frente al tiempo y advierte cuando un objetivo no es evaluable con el formato elegido (p. ej. un OA de expresión oral en selección múltiple).

### D · Generación y revisión
- **S3 Generación IA y validaciones**: ítems, claves, distractores basados en errores esperados, rúbrica, feedback previsto y guion de ayuda. Chequeos automáticos: alineación, legibilidad para la edad, sesgo, accesibilidad, duplicados y que la ayuda no revele la respuesta.
- **D3 Revisión ítem a ítem**: editar, regenerar, reordenar; ver la trazabilidad ítem ↔ objetivo ↔ fuente; ajustar la ayuda por ítem (0–3); previsualizar.

### E · Aprobación y publicación
- **G1 Decisión docente**: ¿está alineada, tiene calidad, es accesible y la ayuda es segura? Si no, se edita o regenera.
- **C4 V°B° de coordinación** (opcional, según C3).
- **S4 Publicación**: versión inmutable (hash), asignación a curso o estudiantes, link / QR / código y notificaciones (**A1** aviso opcional al responsable).

### F · Aplicación con tutor
- **E1 → E2**: el estudiante ve las instrucciones, el tiempo, la política de ayuda y los criterios; responde, justifica (texto o voz), pide ayuda y marca su confianza por ítem.
- **S5 Orquestador del tutor socrático**: aplica la política del ítem (pregunta → pista gradual → comprobación) y registra cada evento.
- **D5 Monitoreo en vivo** (opcional): progreso, alertas y la posibilidad de extender el tiempo.

### G · Corrección y feedback
- **S6 Corrección asistida**: las preguntas cerradas se corrigen automáticamente; en las abiertas la IA sugiere un puntaje con rúbrica y nivel de confianza.
- **D6 Validar corrección**: el docente confirma o ajusta, edita el feedback y libera.
- **E3 Retroalimentación**: por objetivo y no solo la nota, con historial de razonamiento y autorreflexión.

### H · Análisis y mejora
- **S7 Analítica**: logro por objetivo e indicador, patrones de error y dependencia de ayuda, con agregación y anonimización según el rol.
- **D7** Reenseñanza o nueva evaluación, lo que cierra el ciclo hacia D2. **C5** Tablero agregado del centro. **A2** Resumen para el responsable. **E4** Práctica sugerida.

## 4. Principios no negociables

1. **La IA sugiere y el docente decide**, tanto al publicar como al calificar preguntas abiertas.
2. **Texto oficial literal y con fuente**: la IA solo parafrasea para el estudiante, en un campo aparte.
3. **Sin equivalencias automáticas CL ↔ CR.**
4. **Versión anclada**: un cambio curricular no altera las evaluaciones históricas.
5. **Datos de menores tratados como sensibles**: consentimiento verificable, minimización y ningún uso comercial.
6. **Visibilidad mínima por defecto** (ver página 03 del diagrama).
