# ESPECIFICACIÓN DE CASOS DE USO

**Centro de Intervención Multidisciplinario para el Autismo (CIMA)**

*Basado en ISO/IEC/IEEE 29148:2018*

Versión 1.0.0

## Información del documento

| | |
|---|---|
| **Título** | Especificación de Casos de Uso |
| **Subtítulo** | Sistema de gestión clínica y terapéutica de CIMA |
| **Versión** | 1.0.0 |
| **Autor** | |
| **Estado** | En revisión |

## Índice

1. Introducción
2. M1: Módulo de Gestión de pacientes
3. M2: Módulo de Gestión de evaluaciones
4. M3: Módulo de Gestión de planes de intervención
5. M4: Módulo de Gestión de sesiones y progreso terapéutico
6. M5: Módulo de Gestión de casos interdisciplinarios
7. M6: Módulo de Gestión de profesionales y agenda
8. M7: Módulo de Gestión de seguridad de la información
9. Notas sobre decisiones tomadas

---

## 1. Introducción

Este documento especifica los siete módulos del sistema de gestión clínica y terapéutica de CIMA. Cada módulo corresponde a una capacidad de Nivel 1 del mapa de capacidades, y agrupa los casos de uso principales (capacidades de Nivel 2) y sus casos de uso secundarios (capacidades de Nivel 3).

Cada especificación incluye información general (casos de uso, actores, prioridad y estado), descripción, precondiciones, flujo principal en pasos numerados, flujos alternativos y postcondiciones.

**Criterios de redacción:**

- El flujo principal contiene los casos de uso relacionados con «include».
- Cada caso de uso relacionado con «extend» se describe como un flujo alternativo, con su condición.
- Cada línea tiene la forma: entidad que actúa + verbo + objeto + entidad que recibe.
- Cada línea empieza con la entidad con la que terminó la anterior.
- Las entidades se escriben con mayúscula inicial y nunca se usa "el sistema" como sujeto, para derivar después el modelo de dominio: los sustantivos son clases o atributos, los verbos son métodos y las entidades en una misma línea indican relaciones.

---

## 2. M1: Módulo de Gestión de pacientes

| | |
|---|---|
| **ID** | M1 |
| **Nombre** | Gestión de pacientes |
| **Casos de uso** | CU-01 Gestionar ingreso e información del paciente · CU-02 Gestionar representantes · CU-03 Gestionar expediente único · CU-04 Gestionar entorno educativo |
| **Actor principal** | Recepcionista, Representante |
| **Actor secundario** | Coordinador Clínico, Profesional Clínico |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 2.1 Descripción

El Representante solicita atención para el Paciente y el Recepcionista registra la Solicitud de Atención con los datos y antecedentes del Paciente. El Recepcionista registra al Representante, verifica su vínculo legal y obtiene el Consentimiento. El Coordinador Clínico abre el Expediente, donde los Profesionales Clínicos mantienen la Historia Clínica y se vincula la Institución Educativa del Paciente.

### 2.2 Precondiciones

- El Representante es mayor de edad y tiene un vínculo legal con el Paciente.
- El Paciente no tiene un Expediente abierto en el centro.

### 2.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Representante solicita atención para el Paciente al Recepcionista. |
| 2 | El Recepcionista registra una Solicitud de Atención. |
| 3 | La Solicitud de Atención registra los datos de identificación y los antecedentes del Paciente. |
| 4 | El Paciente es admitido por el Recepcionista. |
| 5 | El Recepcionista registra los datos del Representante. |
| 6 | El Representante entrega los documentos de vínculo legal y custodia al Recepcionista. |
| 7 | El Recepcionista verifica el vínculo legal y la custodia del Representante. |
| 8 | El Representante firma el Consentimiento ante el Recepcionista. |
| 9 | El Recepcionista solicita la apertura del Expediente al Coordinador Clínico. |
| 10 | El Coordinador Clínico abre el Expediente del Paciente. |
| 11 | El Expediente registra el Consentimiento, los datos del Representante y la Historia Clínica. |
| 12 | La Historia Clínica es actualizada por el Profesional Clínico. |
| 13 | El Profesional Clínico integra sus registros disciplinares en el Expediente. |
| 14 | El Expediente vincula la Institución Educativa y los Docentes del Paciente. |

### 2.4 Flujos alternativos

**Flujo alternativo 1: Priorizar lista de espera (paso 2)**

- Si no hay cupo disponible, la Solicitud de Atención se registra en la Lista de Espera.
- La Lista de Espera prioriza la Solicitud de Atención según la edad y la urgencia del Paciente.
- El Paciente queda en espera hasta que el Recepcionista le asigne un cupo.

**Flujo alternativo 2: Adjuntar documentos del paciente (paso 11)**

- Si el Representante entrega informes previos, el Representante entrega los Documentos al Recepcionista.
- El Recepcionista adjunta los Documentos al Expediente.

**Flujo alternativo 3: Habilitar información para representante**

- Si un Profesional Clínico decide compartir información, el Profesional Clínico habilita un Documento del Expediente para el Representante.
- El Documento es notificado al Representante.
- El Representante consulta el Documento habilitado.

**Flujo alternativo 4: Atender requerimiento de representante**

- Si el Representante solicita información, el Representante registra un Requerimiento ante el Coordinador Clínico.
- El Coordinador Clínico atiende el Requerimiento.
- El Requerimiento es respondido al Representante.

**Flujo alternativo 5: Cerrar expediente**

- Si el Paciente fue dado de alta, el Coordinador Clínico cierra el Expediente.
- El Expediente queda archivado.

**Flujo alternativo 6: Coordinar con institución educativa**

- Si el Plan de Intervención incluye objetivos escolares, el Profesional Clínico coordina una reunión con el Docente.
- El Docente recibe las recomendaciones del Profesional Clínico.

**Flujo alternativo 7: Compartir información con institución educativa**

- Si el Representante lo autoriza, el Representante autoriza al Profesional Clínico a compartir información.
- El Profesional Clínico envía el Informe autorizado a la Institución Educativa.

### 2.5 Postcondiciones

- El Paciente queda admitido con su Expediente abierto.
- El Representante queda registrado con su vínculo legal verificado y el Consentimiento firmado.
- La Historia Clínica queda actualizada con los registros de cada disciplina.

---

## 3. M2: Módulo de Gestión de evaluaciones

| | |
|---|---|
| **ID** | M2 |
| **Nombre** | Gestión de evaluaciones |
| **Casos de uso** | CU-05 Gestionar evaluaciones disciplinares · CU-06 Gestionar diagnósticos · Analizar evaluación · Dar recomendación médica · Generar conclusión médica |
| **Actor principal** | Coordinador Clínico, Profesional Clínico |
| **Actor secundario** | Representante, Agente RAG (externo), Agente LLM (externo) |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 3.1 Descripción

El Coordinador Clínico planifica la Evaluación del Paciente y cada Profesional Clínico registra los Resultados de los Instrumentos aplicados. Con esos Resultados se registra el Diagnóstico, se elabora el Informe de Evaluación y se registra la devolución de resultados al Representante.

De forma opcional, el módulo se apoya en un agente de IA compuesto por un Agente RAG, que recupera conocimiento de referencia, y un Agente LLM, que genera conclusiones. Este agente analiza la Evaluación y entrega recomendaciones de nueva evaluación y de diagnóstico al Profesional Clínico. El Profesional Clínico mantiene la decisión final sobre el Diagnóstico.

### 3.2 Precondiciones

1. El Paciente tiene el Expediente abierto (M1).
2. El Representante firmó el Consentimiento para la evaluación.
3. Para usar el apoyo de IA, los Agentes RAG y LLM están disponibles.

### 3.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Coordinador Clínico planifica la Evaluación del Paciente. |
| 2 | La Evaluación es asignada a cada Profesional Clínico. |
| 3 | El Profesional Clínico registra los Resultados de los Instrumentos en la Evaluación. |
| 4 | La Evaluación consolida los Resultados para el Diagnóstico. |
| 5 | El Diagnóstico registra la conclusión diagnóstica del Profesional Clínico. |
| 6 | El Profesional Clínico elabora el Informe de Evaluación. |
| 7 | El Informe de Evaluación se registra en el Expediente. |
| 8 | El Expediente registra la devolución de resultados al Representante. |

### 3.4 Flujos alternativos

**Flujo alternativo 1: Registrar reevaluación**

1. Si termina un ciclo del Plan de Intervención, el Plan de Intervención solicita una Reevaluación al Coordinador Clínico.
2. El Coordinador Clínico planifica la Reevaluación.
3. La Reevaluación registra los nuevos Resultados del Profesional Clínico.

**Flujo alternativo 2: Analizar evaluación con IA**

1. El Profesional Clínico solicita el análisis de la Evaluación con los Resultados de los Instrumentos registrados.
2. La Evaluación envía los Resultados de los Instrumentos al Agente RAG.
3. El Agente RAG recupera el conocimiento de referencia relacionado con los Resultados de los Instrumentos.
4. El Agente RAG devuelve el análisis de la Evaluación.
5. La Evaluación registra el análisis como apoyo para el Profesional Clínico y el flujo continúa en el paso 4 del flujo principal.

**Flujo alternativo 3: Dar recomendación médica**

1. El Profesional Clínico solicita una recomendación médica para el Diagnóstico.
2. El sistema ejecuta el análisis de la Evaluación.
3. El sistema ejecuta la generación de la conclusión médica.
4. La Recomendación médica presenta al Profesional Clínico las sugerencias de nueva evaluación y de diagnóstico.
5. El Profesional Clínico revisa las sugerencias y las acepta, las modifica o las descarta.
6. El Diagnóstico registra la conclusión diagnóstica del Profesional Clínico y el flujo continúa en el paso 5 del flujo principal.

### 3.5 Postcondiciones

1. La Evaluación queda registrada con los Resultados de cada disciplina.
2. El Diagnóstico y el Informe de Evaluación quedan registrados en el Expediente.
3. La devolución de resultados al Representante queda registrada.
4. Si se usó el apoyo de IA, el análisis de la Evaluación y la conclusión médica generada quedan registrados como apoyo. El Diagnóstico final corresponde al Profesional Clínico.

---

## 4. M3: Módulo de Gestión de planes de intervención

| | |
|---|---|
| **ID** | M3 |
| **Nombre** | Gestión de planes de intervención |
| **Casos de uso** | CU-07 Gestionar diseño de planes · CU-08 Gestionar vigencia de planes · CU-09 Gestionar tareas terapéuticas |
| **Actor principal** | Coordinador Clínico, Profesional Clínico |
| **Actor secundario** | Representante |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 4.1 Descripción

A partir del Diagnóstico, el Coordinador Clínico crea el Plan de Intervención con sus Objetivos Terapéuticos, Líneas Base y Servicios. El Representante aprueba el Plan de Intervención y el Profesional Clínico asigna Tareas Terapéuticas para el hogar.

### 4.2 Precondiciones

- El Paciente tiene un Diagnóstico registrado (M2).

### 4.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Coordinador Clínico consulta el Diagnóstico del Paciente. |
| 2 | El Diagnóstico da origen al Plan de Intervención. |
| 3 | El Plan de Intervención registra los Objetivos Terapéuticos definidos por el Profesional Clínico. |
| 4 | El Profesional Clínico registra la Línea Base de cada Objetivo Terapéutico. |
| 5 | El Objetivo Terapéutico se asocia a los Servicios y a su intensidad semanal. |
| 6 | Los Servicios se registran en el Plan de Intervención. |
| 7 | El Plan de Intervención se presenta al Representante. |
| 8 | El Representante aprueba el Plan de Intervención. |
| 9 | El Plan de Intervención queda vigente para el Profesional Clínico. |
| 10 | El Profesional Clínico asigna una Tarea Terapéutica al Representante. |

### 4.4 Flujos alternativos

**Flujo alternativo 1: Ajustar plan de intervención**

- Si una Reevaluación o una Junta Clínica lo indica, el Coordinador Clínico ajusta el Plan de Intervención.
- El Plan de Intervención genera una nueva versión para el Representante.
- El Representante aprueba la nueva versión del Plan de Intervención.

**Flujo alternativo 2: Cerrar plan de intervención**

- Si termina la vigencia, el Coordinador Clínico cierra el Plan de Intervención.
- El Plan de Intervención registra su fecha de cierre.

**Flujo alternativo 3: Dar de alta al paciente**

- Si se cumplen los criterios de alta, el Coordinador Clínico da de alta al Paciente.
- El Paciente queda con estado de alta en el Expediente.

**Flujo alternativo 4: Registrar seguimiento de tarea**

- Si se reporta el cumplimiento, el Representante reporta el avance de la Tarea Terapéutica.
- La Tarea Terapéutica registra el seguimiento para el Profesional Clínico.

### 4.5 Postcondiciones

- El Plan de Intervención queda aprobado y vigente, con Objetivos Terapéuticos, Líneas Base y Servicios.
- Las Tareas Terapéuticas quedan asignadas al Representante.

---

## 5. M4: Módulo de Gestión de sesiones y progreso terapéutico

| | |
|---|---|
| **ID** | M4 |
| **Nombre** | Gestión de sesiones y progreso terapéutico |
| **Casos de uso** | CU-10 Gestionar registro de sesiones · CU-11 Gestionar incidentes clínicos · CU-12 Gestionar indicadores de progreso · CU-13 Gestionar informes de progreso |
| **Actor principal** | Profesional Clínico |
| **Actor secundario** | Coordinador Clínico, Representante |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 5.1 Descripción

El Profesional Clínico define un Indicador de Progreso por cada Objetivo Terapéutico y lo trabaja con el Paciente en la Sesión. La Sesión registra la asistencia, las observaciones y los avances, con los que el Profesional Clínico mide el progreso. Cuando corresponde, se reportan Incidentes Clínicos y se elaboran Informes de Avance o de Alta.

### 5.2 Precondiciones

- El Paciente tiene un Plan de Intervención vigente (M3).
- La Sesión corresponde a una Cita programada (M6).

### 5.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Profesional Clínico define un Indicador de Progreso para el Objetivo Terapéutico. |
| 2 | El Objetivo Terapéutico se trabaja con el Paciente en la Sesión. |
| 3 | La Sesión registra la asistencia del Paciente y las observaciones y avances del Profesional Clínico. |
| 4 | El Profesional Clínico mide el progreso en el Indicador de Progreso. |
| 5 | El Indicador de Progreso registra el avance en el Expediente. |

### 5.4 Flujos alternativos

**Flujo alternativo 1: Emitir recomendaciones de sesión**

- Si hay indicaciones para el hogar, el Profesional Clínico registra Recomendaciones en la Sesión.
- La Sesión envía las Recomendaciones al Representante.

**Flujo alternativo 2: Registrar sesión de orientación familiar**

- Si la Sesión es con la familia, el Profesional Clínico registra la Sesión como orientación familiar.
- La Sesión registra la participación del Representante.

**Flujo alternativo 3: Reportar y dar seguimiento a incidente clínico**

- Si ocurre un incidente durante la Sesión, el Profesional Clínico reporta un Incidente Clínico.
- El Incidente Clínico se notifica al Coordinador Clínico y al Representante.
- Si el Incidente Clínico requiere acciones, el Coordinador Clínico registra el seguimiento del Incidente Clínico.

**Flujo alternativo 4: Elaborar informe de avance**

- Si termina un ciclo del Plan de Intervención, el Profesional Clínico elabora un Informe de Avance.
- El Informe de Avance es revisado por el Coordinador Clínico.
- El Coordinador Clínico registra el Informe de Avance en el Expediente.

**Flujo alternativo 5: Elaborar informe de alta**

- Si el Paciente egresa, el Profesional Clínico elabora el Informe de Alta.
- El Informe de Alta es revisado por el Coordinador Clínico.
- El Coordinador Clínico registra el Informe de Alta en el Expediente.

### 5.5 Postcondiciones

- La Sesión queda registrada con asistencia, observaciones y avances.
- El Indicador de Progreso queda actualizado.
- Los Incidentes Clínicos y los Informes quedan registrados en el Expediente cuando corresponde.

---

## 6. M5: Módulo de Gestión de casos interdisciplinarios

| | |
|---|---|
| **ID** | M5 |
| **Nombre** | Gestión de casos interdisciplinarios |
| **Casos de uso** | CU-14 Gestionar equipos de caso · CU-15 Gestionar juntas clínicas · CU-16 Gestionar comunicación clínica interna |
| **Actor principal** | Coordinador Clínico |
| **Actor secundario** | Profesional Clínico |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 6.1 Descripción

El Coordinador Clínico conforma el Equipo de Caso del Paciente y designa al Responsable de Caso. El Equipo de Caso se reúne en Juntas Clínicas, cuyos Acuerdos se registran en el Expediente. Los Profesionales Clínicos se comunican mediante Notas Interdisciplinarias e Interconsultas.

### 6.2 Precondiciones

- El Paciente tiene el Expediente abierto (M1).
- Los Profesionales Clínicos están registrados con su Especialidad (M6).

### 6.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Coordinador Clínico conforma el Equipo de Caso del Paciente. |
| 2 | El Equipo de Caso integra a los Profesionales Clínicos de cada disciplina. |
| 3 | El Profesional Clínico es designado Responsable de Caso por el Coordinador Clínico. |
| 4 | El Coordinador Clínico convoca una Junta Clínica con el Equipo de Caso. |
| 5 | El Equipo de Caso toma Acuerdos en la Junta Clínica. |
| 6 | La Junta Clínica registra los Acuerdos en el Expediente. |

### 6.4 Flujos alternativos

**Flujo alternativo 1: Registrar junta diagnóstica**

- Si el Paciente está en evaluación, la Junta Clínica se registra como Junta Diagnóstica.
- La Junta Diagnóstica envía su conclusión al Diagnóstico.

**Flujo alternativo 2: Registrar junta de seguimiento**

- Si el Paciente está en intervención, la Junta Clínica se registra como Junta de Seguimiento.
- La Junta de Seguimiento envía sus Acuerdos al Plan de Intervención.

**Flujo alternativo 3: Registrar nota interdisciplinaria**

- Si hay algo que informar al equipo, el Profesional Clínico registra una Nota Interdisciplinaria.
- La Nota Interdisciplinaria se notifica al Equipo de Caso.

**Flujo alternativo 4: Atender interconsulta**

- Si un Profesional Clínico necesita otra opinión, el Profesional Clínico solicita una Interconsulta.
- La Interconsulta es atendida por el Profesional Clínico de la otra disciplina.
- El Profesional Clínico registra la respuesta en la Interconsulta.

### 6.5 Postcondiciones

- El Equipo de Caso queda conformado con un Responsable de Caso.
- Los Acuerdos de la Junta Clínica quedan registrados en el Expediente.

---

## 7. M6: Módulo de Gestión de profesionales y agenda

| | |
|---|---|
| **ID** | M6 |
| **Nombre** | Gestión de profesionales y agenda |
| **Casos de uso** | CU-17 Gestionar profesionales · CU-18 Gestionar disponibilidad · CU-19 Gestionar citas |
| **Actor principal** | Coordinador Clínico, Recepcionista |
| **Actor secundario** | Temporizador, Representante |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 7.1 Descripción

El Coordinador Clínico registra al Profesional con su Especialidad y Habilitación y lo habilita en la Agenda. El Recepcionista programa Citas según los horarios disponibles del Profesional y del Espacio, la Agenda evita conflictos de horario y el Temporizador envía Recordatorios sin datos clínicos.

### 7.2 Precondiciones

- El Paciente tiene el Expediente abierto (M1).
- El Profesional y el Espacio tienen Disponibilidad registrada.

### 7.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Coordinador Clínico registra los datos del Profesional. |
| 2 | El Profesional registra su Especialidad y su Habilitación ante el Coordinador Clínico. |
| 3 | El Coordinador Clínico habilita al Profesional en la Agenda. |
| 4 | La Agenda envía los horarios disponibles del Profesional y del Espacio al Recepcionista. |
| 5 | El Recepcionista programa una Cita en la Agenda. |
| 6 | La Agenda valida que la Cita no tenga conflicto de horario. |
| 7 | La Cita asigna al Paciente, al Profesional y al Espacio. |
| 8 | La Cita envía la confirmación al Representante. |

### 7.4 Flujos alternativos

**Flujo alternativo 1: Distribuir carga de casos**

- Si se asigna un Paciente nuevo, el Coordinador Clínico consulta la carga de casos de cada Profesional.
- El Profesional con menor carga de casos recibe al Paciente.

**Flujo alternativo 2: Registrar disponibilidad del profesional**

- Si cambia el horario del Profesional, el Coordinador Clínico actualiza la Disponibilidad del Profesional.
- La Disponibilidad actualiza los horarios en la Agenda.

**Flujo alternativo 3: Registrar disponibilidad de espacios**

- Si cambia el uso de un Espacio, el Coordinador Clínico actualiza la Disponibilidad del Espacio.
- La Disponibilidad actualiza los horarios en la Agenda.

**Flujo alternativo 4: Reservar horario recurrente**

- Si el Plan de Intervención define sesiones semanales fijas, el Recepcionista reserva un Horario Recurrente en la Agenda.
- La Agenda genera las Citas del Horario Recurrente.

**Flujo alternativo 5: Reprogramar cita**

- Si el Representante o el Profesional pide un cambio, el Recepcionista reprograma la Cita.
- La Cita valida el nuevo horario en la Agenda.
- La Agenda envía la nueva confirmación al Representante.

**Flujo alternativo 6: Cancelar cita**

- Si la Cita no se realizará, el Recepcionista cancela la Cita.
- La Cita libera el horario del Profesional y del Espacio en la Agenda.
- La Agenda notifica la cancelación al Representante.

**Flujo alternativo 7: Enviar recordatorio de cita**

- Si se cumple el plazo previo a la Cita, el Temporizador activa el Recordatorio.
- El Recordatorio envía la fecha, la hora y el lugar de la Cita al Representante, sin datos clínicos.

### 7.5 Postcondiciones

- El Profesional queda registrado y habilitado en la Agenda.
- La Cita queda registrada sin conflicto de horario y confirmada al Representante.

---

## 8. M7: Módulo de Gestión de seguridad de la información

| | |
|---|---|
| **ID** | M7 |
| **Nombre** | Gestión de seguridad de la información |
| **Casos de uso** | CU-20 Gestionar accesos · CU-21 Gestionar trazabilidad |
| **Actor principal** | Administrador de Seguridad |
| **Actor secundario** | Coordinador Clínico, Profesional Clínico, Representante |
| **Prioridad** | Alta (Must) |
| **Estado** | Especificado |

### 8.1 Descripción

El Administrador de Seguridad define los Perfiles de Acceso y asigna los Permisos según la Especialidad del Profesional, aplicando el principio de mínimo privilegio. Cada acceso al Expediente queda en un Registro de Acceso, que el Administrador de Seguridad y el Coordinador Clínico pueden consultar y auditar.

### 8.2 Precondiciones

- El Profesional está registrado con su Especialidad (M6).

### 8.3 Flujo principal (escenario de éxito)

| Paso | Descripción de la acción |
|---|---|
| 1 | El Administrador de Seguridad define un Perfil de Acceso. |
| 2 | El Perfil de Acceso agrupa los Permisos por Especialidad. |
| 3 | Los Permisos se asignan al Profesional según su Especialidad. |
| 4 | El Profesional accede al Expediente según su Perfil de Acceso. |
| 5 | El Expediente genera un Registro de Acceso. |

### 8.4 Flujos alternativos

**Flujo alternativo 1: Autorizar acceso de representante**

- Si se registra un Representante con derecho a información, el Administrador de Seguridad autoriza el acceso del Representante.
- El Representante accede solo a la información habilitada del Expediente.
- El Expediente genera un Registro de Acceso.

**Flujo alternativo 2: Consultar registro de accesos**

- Si se requiere revisar quién vio la información, el Coordinador Clínico consulta el Registro de Acceso.
- El Registro de Acceso muestra el usuario, la fecha y la información consultada al Coordinador Clínico.

**Flujo alternativo 3: Consultar registro de modificaciones**

- Si se requiere revisar quién cambió la información, el Coordinador Clínico consulta el Registro de Modificación.
- El Registro de Modificación muestra el usuario, la fecha y el cambio realizado al Coordinador Clínico.

**Flujo alternativo 4: Generar reporte de auditoría**

- Si se ejecuta una revisión de auditoría, el Administrador de Seguridad genera un Reporte de Auditoría.
- El Reporte de Auditoría consolida los Registros de Acceso y los Registros de Modificación.

### 8.5 Postcondiciones

- El Profesional queda con los Permisos de su Especialidad y nada más.
- Cada acceso y cada modificación quedan registrados para su auditoría.

---

## 9. Notas sobre decisiones tomadas

- En M4, "Reportar incidente clínico" es «include» en el diagrama de CU-11, pero en el flujo del módulo va como flujo alternativo, porque CU-11 solo se ejecuta cuando ocurre un incidente.
- En M6, la disponibilidad ya registrada es una precondición, y sus cambios van como flujos alternativos, porque en el diagrama son «extend».
- En todo el documento no aparece "el sistema": cada acción la ejecuta una entidad (Agenda, Expediente, Cita…), para derivar directamente las clases, atributos y métodos del modelo de dominio.
