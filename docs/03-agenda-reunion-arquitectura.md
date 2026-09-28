# Próxima sesión · Arquitectura y modelo de datos

> Prepara: **Leo** · Participan: Leo (CL), Rob (CR), José (CR), socio/a CL, Ariel (demo)
> Insumos: [`01-flujo-evaluacion-curricular.md`](01-flujo-evaluacion-curricular.md), [`02-modelo-curricular-cl-cr.md`](02-modelo-curricular-cl-cr.md), [`flujos/Evalia_flujo_01_v2.drawio`](flujos/Evalia_flujo_01_v2.drawio) y el diagrama de contrato de entidades compartido en Slack (`contrato-entidades.png`)

## Seguimiento de la sesión anterior

| # | Acuerdo | Responsable | Estado |
|---|---|---|---|
| 1 | Comprar un dominio `.com` económico (o la alternativa que convenga) para la imagen institucional | Equipo | ☐ Definir nombre: ¿Evalia o METIS? (el repo usa ambos) |
| 2 | Descargar el repo en local y avanzar hacia un demo más funcional | Ariel | ☐ Sugerencia: empezar por el selector curricular (ver 01 §2) |
| 3 | Preparar la reunión de arquitectura: entidades y flujos | Leo | ☐ Este documento |
| 4 | Explorar la integración con la plataforma de Orlando (API / embed) para no duplicar el catálogo curricular | Equipo + Orlando | ☐ Requiere contrato de datos y acuerdo de ambas partes |

## Agenda propuesta (90 min)

1. **Recorrido del flujo 01 v2** (10 min): confirmar roles, fases y pasos. ¿Falta algún actor, como la coordinación / UTP o el profesional PIE?
2. **Modelo canónico** (25 min): cerrar las entidades de la página 02.
   - ¿`LearningObjective.kind` como enum cerrado o catálogo extensible?
   - ¿Jerarquía de agrupadores libre (árbol) o niveles fijos?
   - ¿Cómo generamos códigos internos estables para CR?
   - ¿Qué entidades del `contrato-entidades.png` calzan con estas y cuáles faltan?
3. **Autoridad y vigencia** (10 min): quién cura el catálogo, cómo se versiona y cómo se convive con la actualización curricular chilena y con el REAC 2026 de CR.
4. **Integración con Orlando** (15 min): proveedor externo frente a catálogo propio; revisar el contrato v0 (02 §6) y la lista de preguntas para él.
5. **Política del tutor y visibilidad** (15 min): niveles de ayuda 0–3, efecto en el puntaje (ninguno / informativo / ponderado), matriz de visibilidad (página 03) y preguntas legales abiertas.
6. **Piloto** (10 min): asignatura y curso por país, métricas y próximos pasos.
7. **Acuerdos y responsables** (5 min).

## Decisiones que deben salir de la reunión

| ID | Decisión | Opciones | Recomendación |
|---|---|---|---|
| D-01 | Alcance del piloto | 1 asignatura × 1 curso por país / 2 × 2 | Matemática 7° (CL) y 7.° año (CR) |
| D-02 | Origen del catálogo curricular en el piloto | Propio / Orlando / híbrido | Propio y mínimo, detrás de la interfaz `CurriculumProvider` para migrar luego |
| D-03 | Efecto de la ayuda del tutor en la nota | Ninguno / informativo / ponderado | **Informativo** en el piloto: se reporta, pero no descuenta |
| D-04 | Revisión humana obligatoria | Solo abiertas / todas en sumativas | Abiertas siempre; cerradas solo en sumativas de alto impacto |
| D-05 | Visibilidad de conversaciones para el responsable | Nunca / con consentimiento / siempre | Con consentimiento explícito y registrado |
| D-06 | Retención de conversaciones | 6 meses / fin de año + 1 / configurable | Fin de año + 1 año, configurable por centro |
| D-07 | Stack del demo funcional | Mantener vanilla JS / migrar a un framework + backend | Definir con Ariel; mínimo: un backend con autenticación para salir de `localStorage` |
| D-08 | Nombre de marca y dominio | Evalia / METIS / otro | Unificar antes de comprar el dominio |

## Métricas del piloto (propuesta)

- **Alineación curricular**: % de ítems que el docente valida como alineados a su objetivo (meta ≥ 85 %).
- **Calidad de ítems**: % de ítems aprobados sin edición y n.º de regeneraciones por evaluación.
- **Seguridad del tutor**: % de conversaciones auditadas en que el tutor reveló la respuesta (meta 0 %).
- **Dependencia de pistas**: nivel de ayuda promedio por ítem y su relación con el logro.
- **Utilidad docente**: tiempo para crear una evaluación, y NPS/encuesta sobre el reporte por objetivo.
- **Comprensión del feedback**: el estudiante puede explicar su próximo paso (encuesta breve).

## Tareas de preparación

- [ ] **Leo + socio/a CL**: validar la tabla Chile (02 §2) y conseguir los OA e indicadores de Matemática 7° básico.
- [ ] **Rob + José**: inventariar la estructura de 3 programas del MEP (Matemáticas, Español, Ciencias) y confirmar las cifras del REAC 45509-MEP.
- [ ] **Leo**: contrastar `contrato-entidades.png` con el modelo de la página 02.
- [ ] **Ariel**: estimar el esfuerzo del selector curricular y del backend mínimo.
- [ ] **Todos**: revisar la matriz de visibilidad (página 03) y traer las objeciones.
- [ ] **Pendiente**: consulta legal breve en CL (Ley 21.719) y CR (Ley 8968) sobre consentimiento de menores y el tratamiento con IA.
