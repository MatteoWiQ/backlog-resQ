# ResQ — Backlog de producto

Backlog del proyecto **ResQ**, una plataforma de rescate y gestión de casos de
animales para refugios, veterinarias, rescatistas independientes y voluntarios.

Este repositorio **no contiene código**: existe únicamente para alojar las
historias de usuario como *issues*. El tablero de trabajo vive en
[GitHub Projects v2](https://github.com/users/MatteoWiQ/projects/1) y es la
fuente de verdad de la planificación.

---

## 1. Convenciones

### Idioma

Todo el contenido del backlog está en **español**. Los nombres de los campos
del tablero están en inglés porque son los que usa GitHub.

### Títulos

| Elemento | Formato | Ejemplo |
|---|---|---|
| Historia de usuario | `HU-XX Descripción` | `HU-09 Crear reporte` |
| Épica | `EP-XX Descripción` | `EP-03 Gestión de reportes` |

Dos dígitos con cero a la izquierda, **un espacio**, sin dos puntos ni guiones
después del ID. El ID **no se renumera nunca**: `HU-00` existe y renumerarlo
chocaría con `HU-01` y rompería las referencias cruzadas.

### Formato de la historia de usuario

El cuerpo de cada HU sigue la convención en español, no la inglesa
*As a / I want / so that*:

```markdown
Como representante de un refugio o veterinaria
Quiero registrar mi organización en la plataforma
Para aparecer como refugio aliado y poder gestionar casos y voluntarios

Criterios de aceptación:
- [ ] Formulario con: nombre de la organización, tipo, dirección, teléfono
- [ ] Opción de subir logo/foto de la organización
- [ ] El registro queda en estado "pendiente de verificación" hasta revisión
- [ ] Validación de campos obligatorios y formato de email/teléfono
- [ ] Confirmación por email al completar el registro
```

Tres reglas:

1. `Como` nombra **un rol concreto**, no "el usuario".
2. `Para` expresa **el valor de negocio**, no la acción repetida.
3. Los criterios de aceptación son verificables y binarios. Una historia sin
   criterios **no está lista para estimar**.

---

## 2. Estructura del backlog

### Épicas y su alcance

| Épica | Alcance | Historias |
|---|---|---|
| EP-01 Configuración y arquitectura | Entorno, base de datos, arquitectura | HU-00 … HU-03 |
| EP-02 Usuarios y autenticación | Registro, login, roles, perfil | HU-04 … HU-07 |
| EP-03 Gestión de reportes | Crear, adjuntar, consultar, actualizar | HU-08 … HU-13 |
| EP-04 Mapa y geolocalización | Visualizar, filtrar, ubicar | HU-14, HU-15, HU-16 |
| EP-05 Voluntarios | Registro, consulta de casos, solicitudes | HU-17, HU-18, HU-19 |
| EP-06 Organizaciones | Registro y gestión de casos | HU-20, HU-21 |
| EP-07 Administración | Gestión de usuarios, reportes, organizaciones | HU-23, HU-24, HU-25 |
| EP-08 Notificaciones y chat | Coordinar ayuda, notificar, mensajería | HU-22, HU-26, HU-27 |

El vínculo HU → épica se materializa con el campo nativo **`Parent issue`**
(sub-issues de GitHub), no con un campo de texto. Así la relación es
consultable y aparece en el body de ambos issues.

### Tipos (`Type.`)

| Tipo | Qué es |
|---|---|
| `Epic` | Una épica. 8 en total. |
| `User Story` | Historia con el patrón `Como / Quiero / Para`. 24 en total. |
| `Task` | Trabajo técnico sin valor de usuario directo. 4 en total. |
| `Bug` | Defecto. |

**HU-00 a HU-03 son `Task`, no `User Story`.** Son configuración de entorno,
base de datos, arquitectura y comunicación frontend-backend. No les falta la
sección `Quiero`: no son historias de usuario. Clasifícalas mal y el backlog
reporta una falsa conformidad de formato.

---

## 3. Tablero ResQ

### Campos disponibles

| Campo | Tipo | Valores |
|---|---|---|
| `Title` | texto | |
| `Assignees` | personas | |
| `Status` | selección | `Backlog`, `Ready`, `In progress`, `In review`, `Done` |
| `Labels` | labels | sin uso |
| `Repository` | repo | |
| `Milestone` | milestone | |
| **`Parent issue`** | sub-issue | vínculo HU → épica |
| `Sub-issues progress` | calculado | |
| `Created`, `Updated`, `Closed` | fecha | |
| **`Priority`** | selección | `Must`, `Should`, `Could`, `Won't` — **es MoSCoW** |
| `Size` | selección | `XS`, `S`, `M`, `L`, `XL` — sin uso |
| `Estimate` | número | sin uso |
| `Start date`, `Target date` | fecha | |
| `Story Points` | número | |
| `Area` | selección | `Frontend`, `Backend`, `Database`, `DevOps`, `Testing` |
| `Sprint` | iteración | `Sprint 1` (completado), `Sprint 2`, `Sprint 3` |
| **`Type.`** | selección | `Epic`, `User Story`, `Task`, `Bug` — **ojo el punto final** |

El campo de MoSCoW se llama `Priority`, no `MoSCoW`. El de tipo se llama
`Type.` **con punto final**, que es fácil de tipear mal en una API.

### MoSCoW

Se aplica **solo a historias de usuario**, no a épicas ni tareas. Los valores
preexistentes en las épicas no son válidos y distorsionan cualquier conteo a
nivel de tablero.

| Valor | Criterio |
|---|---|
| `Must` | Sin esto no hay producto. |
| `Should` | Importante, pero el MVP funciona sin ello. |
| `Could` | Deseable, no bloqueante. |
| `Won't` | Fuera de alcance explícito para la versión actual. |

**Anti-patrón:** si el 100% de las historias es `Must`, no estás priorizando,
estás sellando. La distribución actual es 14 / 9 / 4 / 1.

### Story Points

Escala Fibonacci, derivada de la cantidad de criterios de aceptación como
señal de complejidad:

| Criterios | Tipo de historia | Puntos |
|---|---|---|
| 0–2 | o infraestructura pura | 2 |
| 4–5 | CRUD directo | 3 |
| 6–7 | multipaso o entre servicios | 5 |
| 8–10 | o autenticación / arquitectura | 8 |

Reglas:

- **Una historia sin criterios de aceptación no se estima.** Se marca para
  refinamiento. Ponerle un número a algo no refinado anula el propósito de
  estimar.
- La estimación siempre se acompaña del conteo de criterios que la justifica.
- Total actual: **127 puntos en 27 historias**.

### Sprints

Un ítem en `Backlog` **sin sprint asignado no es un defecto**: es correcto que
una historia no agendada no tenga iteración. No fuerces sprints.

Asigna sprint sólo cuando la historia entra a `Ready`.

---

## 4. Reglas de higiene del backlog

1. **Nunca dupliques épicas.** Resolvé los epics por **número de issue**, no
   por el prefijo `EP-NN` del título. El repo tuvo tres issues `EP-03` y dos
   `EP-05`; indexar por título asoció historias al duplicado equivocado.
2. **Una historia, un padre.** GitHub rechaza un sub-issue que ya tiene padre.
3. **Normalizá separadores, no IDs.**
4. **No inventes estimaciones ni prioridades.** Son decisiones del equipo.
   Cualquier valor generado automáticamente es una *propuesta* a confirmar.
5. **Cerrá duplicados con `state_reason: duplicate`** y un comentario que
   apunte al issue canónico.

---

## 5. Skill de organización

La auditoría y corrección de este backlog se automatizó con el skill
**`resq-backlog-triage`**, instalado en
`~/.config/opencode/skills/resq-backlog-triage/SKILL.md`.

El skill:

1. Lee el tablero vía GraphQL con una query ya depurada contra el schema real.
2. Valida contra las convenciones de este README.
3. Reporta desviaciones en tabla.
4. **Nunca escribe sin confirmación explícita** del usuario.

Contiene el detalle técnico que costó descubrir a fuerza de errores: los nombres
exactos de los tipos de valor de campo en GraphQL (`ProjectV2ItemField*`, con
el iterador exponiendo `title` y no `iteration`), el input real de
`addSubIssue` (`issueId` es el **padre**, no `parentIssueId`), y los workarounds
para los bugs de PowerShell 5.1 en el cliente GraphQL.

### Cómo usarlo

```
Read the ResQ backlog and report deviations from the conventions in README.md
```

El skill propone; vos aprobás; recién entonces escribe.

---

## 6. Estado al 2026-09-26

| Métrica | Valor |
|---|---|
| Historias de usuario | 24 |
| Tareas técnicas | 4 |
| Épicas | 8 |
| Story Points | 127 (en 27 historias; HU-27 sin estimar) |
| MoSCoW | 14 Must · 9 Should · 4 Could · 1 Won't |

Pendientes conocidos:

- **7 de 8 épicas sin descripción.** Sólo EP-06 tiene cuerpo.
- **HU-27** (`Mensajes entre usuarios`) no tiene criterios de aceptación y no
  fue estimada. Marcada `Won't` para v1.
- **6 épicas tienen `Must` en `Priority`**, valor inválido para una épica.
- **6 de 8 campos sin usar**: `Labels`, `Size`, `Estimate`, `Start date`,
  `Target date`, `Area` parcialmente.
