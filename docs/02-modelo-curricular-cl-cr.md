# Modelo curricular canónico · Chile y Costa Rica

> Documento de trabajo · v1 · 28-09-2026 · Complementa la página **02** del diagrama.
> Responsables de validación: **Chile** → Leo + socio/a CL (autor/a de este documento) · **Costa Rica** → Rob + José · **Modelo común** → todo el equipo.
> ⚠️ Todo lo marcado **[validar]** es una lectura preliminar y debe confirmarse contra la fuente oficial antes de cargar datos.

## 1. Idea central

Mantenemos **un modelo canónico** (lo que Evalia entiende) y **un adaptador por país y por programa** que traduce cada fuente oficial a ese modelo. Así evitamos dos cosas:

- construir dos plataformas separadas;
- forzar equivalencias entre un OA chileno y una habilidad o aprendizaje costarricense.

```
Marco (país, autoridad, versión, vigencia)
 └─ Oferta / modalidad
     └─ Tramo o ciclo
         └─ Curso / año
Asignatura ── Agrupador (eje | unidad | área | tema…, jerarquía libre)
               └─ Objetivo curricular (kind + código + texto literal + fuente)
                   ├─ Indicador (origen: oficial | docente | IA aprobada)
                   └─ Descriptor (conocimiento | habilidad | actitud)
```

## 2. Chile · MINEDUC

| Elemento | Detalle | Estado |
|---|---|---|
| Marcos vigentes | Bases Curriculares de Educación Parvularia (2018); 1°–6° básico (2012); 7° básico–2° medio (2015); 3°–4° medio (2019) | Estable |
| Capa adicional | Priorización curricular (OA basales / complementarios) | **[validar]** qué versión rige en 2026 |
| En trámite | Actualización curricular de 1° básico a 2° medio: pasó por consulta pública (2024), el CNED hizo observaciones y el Mineduc reformula la propuesta | Monitorear: el modelo debe soportar dos marcos simultáneos |
| Jerarquía típica | Asignatura → Eje → **OA** (código tipo `MA04 OA 03`) → Indicadores de evaluación sugeridos (en los Programas de Estudio) | Estable |
| Otros objetivos | OAT (transversales), OA de habilidades y OA de actitudes | Estable |
| Unidades | Los Programas de Estudio agrupan los OA en unidades (relación N:M) | Estable |
| Evaluación | Decreto 67/2018: escala 1,0–7,0 y aprobación con 4,0; la exigencia (p. ej. 60 %) la fija el reglamento de cada centro | Estable |
| Diversidad | Decreto 83/2015 (DUA y diversificación) · PIE (Decreto 170) | Estable |
| Identificadores | RBD (centro) · RUN (persona) | Estable |
| Datos personales | Ley 19.628 vigente → **Ley 21.719**: entra en vigencia el 1-dic-2026; hay un proyecto en trámite para postergarla a 2027. Da protección reforzada a niños, niñas y adolescentes | **[validar]** estado del proyecto de postergación |

Fuente principal: [curriculumnacional.cl](https://www.curriculumnacional.cl/Curriculum/Bases_Curriculares). Ojo: desde el entorno de desarrollo el sitio bloquea el acceso automatizado, así que la carga de datos probablemente será semi-manual o vía un proveedor (ver §6).

## 3. Costa Rica · MEP

| Elemento | Detalle | Estado |
|---|---|---|
| Estructura | Preescolar (Interactivo II, Transición) · Educación General Básica: I Ciclo (1°–3°), II Ciclo (4°–6°), III Ciclo (7°–9°) · Educación Diversificada (10°–11°; 12° en técnica) | Estable |
| Modalidades | Académica, Técnica, Artística, CINDEA / IPEC (personas jóvenes y adultas), nocturna, educación especial, indígena… | **[validar]** lista para el piloto |
| Programas | **Uno por asignatura**, con fechas y estructura distintas. Ejemplo Matemáticas (2012): áreas (Números, Geometría, Medidas, Relaciones y Álgebra, Estadística y Probabilidad) → conocimientos → **habilidades específicas** → indicaciones puntuales | Estable (Matemáticas) |
| Otros programas | Serie “Educar para una nueva ciudadanía” (2016+): pueden usar aprendizajes esperados, criterios de evaluación, indicadores, saberes | **[validar]** inventario por programa (Rob / José) |
| Especificaciones | La DGEC publicó en 2026 los *Marcos de especificaciones* de las Pruebas Nacionales (primaria: Español y Matemáticas) | Muy útil para el piloto |
| Evaluación | **Nuevo REAC, Decreto 45509-MEP** (publicado en feb-2026, rige desde el curso lectivo 2026). La prensa reporta que la nota mínima sube de 65 a 75, el trabajo cotidiano baja de 60 % a 50 % y se elimina el arrastre de materias | **[validar]** contra el texto oficial |
| Diversidad | Apoyos educativos: de acceso, curriculares no significativos y significativos | **[validar]** terminología 2026 |
| Identificadores | Código del centro educativo · cédula / DIMEX | **[validar]** |
| Datos personales | Ley 8968 (PRODHAB) | Estable |

Fuentes: [Programas de estudio MEP](https://mep.go.cr/programas-estudio) · [Oferta educativa](https://www.mep.go.cr/oferta-educativa) · [Programa de Matemáticas (PDF)](https://www.mep.go.cr/sites/default/files/media/matematica.pdf) · [REAC 45509-MEP (PDF)](https://www.mep.go.cr/sites/default/files/2026-05/ReglamentoEvalAprendizajesConducta.pdf) · [Marco de especificaciones Matemáticas Primaria (DGEC)](https://dgec.mep.go.cr/wp-content/uploads/2026/03/Marco-especificaciones-Matematicas-Primaria-VF.pdf)

## 4. Mapeo canónico → país

| Campo canónico | Chile | Costa Rica |
|---|---|---|
| `CurriculumFramework` | Bases Curriculares + versión | Programa de estudio de la asignatura + año |
| `Pathway` | Regular HC / TP / Artística, EPJA, Especial | Académica, Técnica, CINDEA / IPEC… |
| `Stage` → `Grade` | Parvularia / Básica / Media → 1°–8° básico, 1°–4° medio | Preescolar / Ciclos I–III / Diversificada → 1°–12° año |
| `CurriculumGroup.kind` | `eje`, `unidad` | `área`, `unidad`, `eje_temático`, `tema` |
| `LearningObjective.kind` | `OA`, `OAT` | `habilidad_específica`, `aprendizaje_esperado`, `criterio_evaluación`, `saber` |
| `LearningObjective.official_code` | `MA07 OA 01` | La mayoría de los programas no usa códigos: generamos uno **interno** estable (p. ej. `CR-MAT-7-NUM-HE-03`) y lo marcamos como no oficial |
| `Indicator` | Indicadores de evaluación | Indicaciones puntuales / indicadores |
| `Assessment.scale` | 1,0–7,0 + exigencia | 1–100 (REAC 2026) |

## 5. Alcance propuesto para el piloto

Recomendación: **Matemática, 7° básico (CL) y 7.° año, III Ciclo (CR)**.

- Son edades comparables (12–13 años) y permiten comparar ambos adaptadores con la misma asignatura.
- Matemáticas es el programa costarricense con la estructura más regular (área → habilidad específica → indicación puntual).
- La cantidad de objetivos es acotada: se carga y valida a mano en pocos días.

Segunda asignatura opcional: Lenguaje y Comunicación (CL) / Español (CR), útil para probar preguntas abiertas y rúbricas. **Decisión pendiente del equipo.**

Formato del JSON del piloto (textos entre `<…>` = copiar literal desde la fuente oficial; no los inventamos):

```json
{
  "framework": {
    "id": "cl-bc-7b2m-2015", "country": "CL", "authority": "MINEDUC",
    "name": "Bases Curriculares 7° básico a 2° medio", "version": "2015",
    "valid_from": "2016-03-01", "status": "vigente",
    "source_url": "https://www.curriculumnacional.cl/..."
  },
  "subject": { "id": "cl-ma", "code": "MA", "name": "Matemática", "grades": ["7B"] },
  "groups": [ { "id": "cl-ma-7b-eje-num", "kind": "eje", "name": "Números" } ],
  "objectives": [
    {
      "id": "cl-ma07-oa01", "group_id": "cl-ma-7b-eje-num", "grade_id": "7B",
      "kind": "OA", "official_code": "MA07 OA 01", "code_is_official": true,
      "official_text": "<texto literal del OA>",
      "student_paraphrase": null,
      "indicators": [ { "text": "<indicador del Programa de Estudio>", "origin": "oficial" } ],
      "source_ref": { "doc": "Programa de Estudio 7° básico Matemática", "page": null }
    }
  ]
}
```

En Costa Rica el mismo esquema cambia solo en `kind: "habilidad_específica"`, `groups[].kind: "área"`, `code_is_official: false` e `indicators[].origin: "oficial"` (indicaciones puntuales).

## 6. Proveedor curricular e integración con la plataforma de Orlando

El catálogo se consume detrás de una interfaz `CurriculumProvider`, así que Evalia no depende de dónde viven los datos:

| Proveedor | Cuándo | Riesgo |
|---|---|---|
| `evalia_catalog` (propio) | Piloto (carga manual validada) | Costo de mantener vigencias |
| `external_api` (Orlando) | Si se firma el contrato de datos | Dependencia de terceros, disponibilidad, licencia |
| `manual_upload` | Programas propios o de centros privados | Calidad variable, marcar origen |

Lo mínimo que Evalia necesita del proveedor (contrato v0):

1. Listar marcos por país, con versión y vigencia.
2. Recorrer el árbol curso → asignatura → agrupador → objetivo.
3. Cada objetivo con **ID estable**, tipo, código oficial (si existe), texto literal, indicadores y URL de la fuente.
4. Un feed de cambios (`updated_since` o webhook) para detectar nuevas versiones.
5. Garantía de que los IDs no se reutilizan y de que la versión anterior queda disponible (las evaluaciones históricas apuntan a ella).
6. Solo datos curriculares, que son públicos. **No se comparten datos de estudiantes en ninguna dirección** sin un acuerdo aparte.

Preguntas para Orlando: ¿qué países y niveles cubre hoy? ¿cómo modela Costa Rica? ¿qué tan frecuente es su actualización? ¿qué SLA ofrece? ¿con qué licencia o costo? ¿permite cache local? ¿hay un embed de UI o solo API?
