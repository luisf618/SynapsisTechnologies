# DICCIONARIO DE CLASES

**Centro de Intervención Multidisciplinario para el Autismo (CIMA)**

Derivado de la Especificación de Casos de Uso

Versión 1.0.0

## Índice

1. Criterios de derivación
2. Tipos de relación y cardinalidad
3. Diccionario de clases
   - 3.1 Actores
   - 3.2 M1: Gestión de pacientes
   - 3.3 M2: Gestión de evaluaciones
   - 3.4 M3: Gestión de planes de intervención
   - 3.5 M4: Gestión de sesiones y progreso terapéutico
   - 3.6 M5: Gestión de casos interdisciplinarios
   - 3.7 M6: Gestión de profesionales y agenda
   - 3.8 M7: Gestión de seguridad de la información
4. Notas y supuestos

---

## 1. Criterios de derivación

| En la línea de la especificación | Va al diccionario como | Ejemplo |
|---|---|---|
| Sujeto que es un sustantivo con identidad propia | **Entidad** | "**La Cita** asigna al Paciente…" → Cita |
| Sustantivo que solo describe a otra entidad | **Atributo** de esa entidad | "la **fecha**, la **hora** y el **lugar** de la Cita" → atributos de Cita |
| Verbo + sustantivo en voz activa | **Método del sujeto** | "El Recepcionista **programa una Cita**" → Recepcionista.programarCita() |
| Voz pasiva: "X es [verbo] por Y" | **Método de Y**, porque Y ejecuta la acción | "El Paciente es admitido por el Recepcionista" → Recepcionista.admitirPaciente() |
| Forma con "se": "X se registra en Y" | **Método de Y**, porque Y guarda el resultado | "La Solicitud se registra en la Lista de Espera" → ListaEspera.agregarSolicitud() |
| Dos entidades en la misma línea | **Relación** entre ambas | "La Cita asigna al Paciente" → Cita – Paciente |

**Convenciones:**

- El nombre de la entidad se escribe con espacios ("Plan de Intervención"). Los atributos y métodos se escriben en camelCase.
- Cada entidad tiene un identificador (`id`).
- Los actores humanos llevan `credenciales` e `iniciarSesion()`.
- Cada relación aparece una sola vez, en la entidad que la inicia: el sujeto de la línea de la especificación o, en las relaciones todo-parte, el "todo". Por eso algunas entidades tienen "—" en las columnas de relación.
- No se incluyen relaciones entre actores (por ejemplo, Representante y Recepcionista): son interacciones entre personas, no vínculos entre datos, y se representan en los diagramas de secuencia.

**Entidades unificadas para evitar duplicados:**

- "Profesional" y "Profesional Clínico" son la misma entidad.
- Reevaluación se representa en **Evaluación** mediante el atributo `tipoEvaluacion`.
- Informe de Evaluación, de Avance y de Alta se representan en **Informe** mediante `tipoInforme`.
- Junta Diagnóstica y Junta de Seguimiento se representan en **Junta Clínica** mediante `tipoJunta`.
- Línea Base, Acuerdos, Recomendaciones y Especialidad son **atributos**, porque solo describen a otra entidad.

---

## 2. Tipos de relación y cardinalidad

### 2.1 Tipos de relación

| Tipo | Significado | Cuándo se usa |
|---|---|---|
| **Asociación** | Dos entidades se conocen y trabajan juntas | Aparecen en la misma línea y la relación se mantiene en el tiempo: "La Cita asigna al Paciente" |
| **Agregación** | Todo-parte; la parte puede existir sin el todo | "La Lista de Espera prioriza la Solicitud": la Solicitud existe aunque salga de la lista |
| **Composición** | Todo-parte; la parte no existe sin el todo | "El Expediente registra la Historia Clínica": no hay Historia Clínica sin Expediente |
| **Dependencia** | Una entidad solo usa o consulta a otra, sin guardar un vínculo | "El Coordinador consulta el Diagnóstico" |

### 2.2 Cardinalidad

Se lee siempre **Entidad (de la fila) : Entidad relacionada**.

| Notación | Significado | Ejemplo |
|---|---|---|
| **1:1** | A cada A le corresponde un B, y a cada B un A | Paciente **1:1** Expediente: cada paciente tiene un solo expediente |
| **1:N** | Un A tiene muchos B; cada B pertenece a un A | Plan de Intervención **1:N** Objetivo Terapéutico: un plan tiene varios objetivos |
| **N:1** | Muchos A corresponden a un B | Cita **N:1** Espacio: muchas citas se hacen en el mismo espacio |
| **N:N** | Un A se relaciona con muchos B, y un B con muchos A | Representante **N:N** Paciente: un padre puede tener varios hijos en el centro, y un niño puede tener varios representantes |

---

## 3. Diccionario de clases

### 3.1 Actores

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Representante** | idRepresentante, credenciales, datosPersonales, tipoVinculo, documentosCustodia, estadoVerificacion | iniciarSesion()<br>solicitarAtencion()<br>entregarDocumentos()<br>firmarConsentimiento()<br>registrarRequerimiento()<br>consultarInformacionHabilitada()<br>autorizarCompartirInformacion()<br>aprobarPlanIntervencion()<br>reportarAvanceTarea() | Asociación (N:N) | Paciente |
| | | | Asociación (1:N) | Consentimiento |
| | | | Asociación (1:N) | Documento |
| | | | Asociación (1:N) | Requerimiento |
| | | | Asociación (1:N) | Plan de Intervención |
| | | | Asociación (1:N) | Tarea Terapéutica |
| **Recepcionista** | idRecepcionista, credenciales, datosPersonales | iniciarSesion()<br>registrarSolicitudAtencion()<br>admitirPaciente()<br>registrarRepresentante()<br>verificarVinculoLegal()<br>solicitarAperturaExpediente()<br>adjuntarDocumento()<br>asignarCupo()<br>programarCita()<br>reservarHorarioRecurrente()<br>reprogramarCita()<br>cancelarCita() | Asociación (1:N) | Solicitud de Atención |
| | | | Asociación (1:N) | Paciente |
| | | | Asociación (1:N) | Cita |
| | | | Asociación (1:N) | Horario Recurrente |
| | | | Dependencia (N:1) | Agenda |
| **Coordinador Clínico** | idCoordinador, credenciales, datosPersonales, especialidad | iniciarSesion()<br>abrirExpediente()<br>atenderRequerimiento()<br>cerrarExpediente()<br>planificarEvaluacion()<br>planificarReevaluacion()<br>consultarDiagnostico()<br>ajustarPlanIntervencion()<br>cerrarPlanIntervencion()<br>darAltaPaciente()<br>registrarSeguimientoIncidente()<br>revisarInforme()<br>registrarInformeExpediente()<br>conformarEquipoCaso()<br>designarResponsableCaso()<br>convocarJuntaClinica()<br>registrarProfesional()<br>habilitarProfesionalAgenda()<br>consultarCargaCasos()<br>actualizarDisponibilidad()<br>consultarRegistroAcceso()<br>consultarRegistroModificacion() | Asociación (1:N) | Expediente |
| | | | Asociación (1:N) | Requerimiento |
| | | | Asociación (1:N) | Evaluación |
| | | | Dependencia (1:N) | Diagnóstico |
| | | | Asociación (1:N) | Plan de Intervención |
| | | | Asociación (1:N) | Incidente Clínico |
| | | | Asociación (1:N) | Informe |
| | | | Asociación (1:N) | Equipo de Caso |
| | | | Asociación (1:N) | Junta Clínica |
| | | | Asociación (1:N) | Disponibilidad |
| | | | Dependencia (N:1) | Agenda |
| | | | Dependencia (1:N) | Registro de Acceso |
| | | | Dependencia (1:N) | Registro de Modificación |
| **Profesional Clínico** | idProfesional, credenciales, datosProfesionales, especialidad, habilitacion, cargaCasos | iniciarSesion()<br>actualizarHistoriaClinica()<br>integrarRegistrosDisciplinares()<br>habilitarDocumentoRepresentante()<br>coordinarReunionEscolar()<br>enviarInformeInstitucion()<br>registrarResultadosInstrumento()<br>elaborarInformeEvaluacion()<br>definirObjetivoTerapeutico()<br>registrarLineaBase()<br>asignarTareaTerapeutica()<br>definirIndicadorProgreso()<br>medirProgreso()<br>registrarRecomendaciones()<br>registrarSesionOrientacionFamiliar()<br>reportarIncidenteClinico()<br>elaborarInformeAvance()<br>elaborarInformeAlta()<br>registrarNotaInterdisciplinaria()<br>solicitarInterconsulta()<br>atenderInterconsulta()<br>registrarRespuestaInterconsulta()<br>registrarEspecialidad()<br>recibirPaciente()<br>accederExpediente() | Asociación (N:N) | Paciente |
| | | | Asociación (N:N) | Historia Clínica |
| | | | Asociación (1:N) | Documento |
| | | | Asociación (N:N) | Docente |
| | | | Asociación (N:N) | Institución Educativa |
| | | | Asociación (N:N) | Evaluación |
| | | | Asociación (1:N) | Resultado de Instrumento |
| | | | Asociación (1:N) | Informe |
| | | | Asociación (1:N) | Objetivo Terapéutico |
| | | | Asociación (1:N) | Tarea Terapéutica |
| | | | Asociación (1:N) | Indicador de Progreso |
| | | | Asociación (1:N) | Sesión |
| | | | Asociación (1:N) | Incidente Clínico |
| | | | Asociación (1:N) | Nota Interdisciplinaria |
| | | | Asociación (N:N) | Interconsulta |
| | | | Asociación (N:1) | Perfil de Acceso |
| | | | Dependencia (N:N) | Expediente |
| **Administrador de Seguridad** | idAdminSeguridad, credenciales, nivelAcceso | iniciarSesion()<br>definirPerfilAcceso()<br>asignarPermisos()<br>autorizarAccesoRepresentante()<br>generarReporteAuditoria() | Asociación (1:N) | Perfil de Acceso |
| | | | Asociación (1:N) | Permiso |
| | | | Asociación (1:N) | Reporte de Auditoría |
| **Temporizador** (actor de sistema) | idTemporizador, plazoAnticipacion, frecuenciaEjecucion | activarRecordatorio() | Dependencia (1:N) | Recordatorio |

### 3.2 M1: Gestión de pacientes

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Paciente** | idPaciente, datosIdentificacion, fechaNacimiento, antecedentes, estado | actualizarEstado() | Asociación (1:1) | Expediente |
| **Solicitud de Atención** | idSolicitud, fechaSolicitud, motivoConsulta, nivelUrgencia, estado | registrarDatosPaciente() | Asociación (N:1) | Paciente |
| **Lista de Espera** | idListaEspera, solicitudes, criterioPrioridad | agregarSolicitud()<br>priorizarSolicitud() | Agregación (1:N) | Solicitud de Atención |
| **Expediente** | idExpediente, fechaApertura, fechaCierre, estado | registrarConsentimiento()<br>vincularRepresentante()<br>crearHistoriaClinica()<br>vincularInstitucionEducativa()<br>registrarInforme()<br>registrarDevolucionResultados()<br>archivar()<br>generarRegistroAcceso() | Composición (1:1) | Historia Clínica |
| | | | Agregación (1:N) | Consentimiento |
| | | | Agregación (1:N) | Documento |
| | | | Agregación (1:N) | Informe |
| | | | Asociación (N:N) | Representante |
| | | | Asociación (N:1) | Institución Educativa |
| | | | Asociación (1:N) | Registro de Acceso |
| **Historia Clínica** | idHistoriaClinica, registrosDisciplinares, fechaActualizacion | — | — | — |
| **Consentimiento** | idConsentimiento, tipoConsentimiento, alcance, fechaFirma | — | — | — |
| **Documento** | idDocumento, tipoDocumento, archivo, fechaCarga, habilitadoRepresentante | notificarRepresentante() | — | — |
| **Requerimiento** | idRequerimiento, descripcion, fechaRegistro, estado, respuesta | enviarRespuesta() | — | — |
| **Institución Educativa** | idInstitucion, nombre, nivelEducativo, contacto | — | Agregación (1:N) | Docente |
| **Docente** | idDocente, nombre, contacto, idInstitucion | recibirRecomendaciones() | — | — |

### 3.3 M2: Gestión de evaluaciones

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Evaluación** | idEvaluacion, tipoEvaluacion, fechaPlanificada, disciplinas, estado | asignarProfesional()<br>consolidarResultados()<br>registrarResultados() | Asociación (N:1) | Paciente |
| | | | Composición (1:N) | Resultado de Instrumento |
| | | | Asociación (1:1) | Diagnóstico |
| **Resultado de Instrumento** | idResultado, instrumento, disciplina, puntaje, observaciones | — | — | — |
| **Diagnóstico** | idDiagnostico, conclusion, nivelApoyo, fechaDiagnostico | registrarConclusion()<br>generarPlanIntervencion() | Asociación (1:N) | Plan de Intervención |
| **Informe** | idInforme, tipoInforme, contenido, fechaElaboracion, estadoRevision | — | Asociación (N:1) | Institución Educativa |

### 3.4 M3: Gestión de planes de intervención

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Plan de Intervención** | idPlan, version, fechaInicio, fechaFin, fechaCierre, estado | registrarObjetivo()<br>registrarServicio()<br>presentarRepresentante()<br>activar()<br>generarVersion()<br>registrarCierre()<br>solicitarReevaluacion() | Asociación (N:1) | Paciente |
| | | | Composición (1:N) | Objetivo Terapéutico |
| | | | Composición (1:N) | Servicio |
| | | | Composición (1:N) | Tarea Terapéutica |
| | | | Asociación (1:N) | Evaluación |
| **Objetivo Terapéutico** | idObjetivo, area, descripcion, lineaBase, criterioLogro | asociarServicio() | Asociación (N:N) | Servicio |
| | | | Composición (1:N) | Indicador de Progreso |
| | | | Asociación (N:N) | Sesión |
| **Servicio** | idServicio, disciplina, modalidad, intensidadSemanal | — | — | — |
| **Tarea Terapéutica** | idTarea, descripcion, fechaAsignacion, estadoCumplimiento | registrarSeguimiento() | — | — |

### 3.5 M4: Gestión de sesiones y progreso terapéutico

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Sesión** | idSesion, fecha, tipoSesion, asistencia, observaciones, avances, recomendaciones | registrarObjetivoTrabajado()<br>registrarAsistencia()<br>registrarObservaciones()<br>enviarRecomendaciones()<br>registrarParticipacionRepresentante() | Asociación (1:1) | Cita |
| | | | Asociación (N:1) | Paciente |
| | | | Asociación (N:N) | Representante |
| | | | Asociación (1:N) | Incidente Clínico |
| **Indicador de Progreso** | idIndicador, descripcion, meta, valorActual, fechaMedicion | registrarAvance() | Asociación (N:1) | Expediente |
| **Incidente Clínico** | idIncidente, tipoIncidente, descripcion, fechaHora, estadoSeguimiento | notificar() | Asociación (N:N) | Representante |

### 3.6 M5: Gestión de casos interdisciplinarios

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Equipo de Caso** | idEquipo, profesionales, responsableCaso | integrarProfesional()<br>tomarAcuerdos() | Agregación (N:N) | Profesional Clínico |
| | | | Asociación (1:1) | Paciente |
| | | | Asociación (1:N) | Junta Clínica |
| **Junta Clínica** | idJunta, tipoJunta, fecha, participantes, acuerdos | registrarAcuerdos()<br>enviarConclusionDiagnostico()<br>enviarAcuerdosPlan() | Asociación (N:1) | Expediente |
| | | | Asociación (1:1) | Diagnóstico |
| | | | Asociación (N:1) | Plan de Intervención |
| **Nota Interdisciplinaria** | idNota, autor, contenido, fecha | notificarEquipo() | Asociación (N:1) | Equipo de Caso |
| **Interconsulta** | idInterconsulta, motivo, disciplinaDestino, respuesta, estado | — | — | — |

### 3.7 M6: Gestión de profesionales y agenda

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Agenda** | idAgenda, periodo | consultarHorariosDisponibles()<br>validarConflictoHorario()<br>generarCitasRecurrentes()<br>notificarCambioCita() | Agregación (1:N) | Cita |
| | | | Asociación (1:N) | Horario Recurrente |
| **Disponibilidad** | idDisponibilidad, tipoRecurso, diaSemana, horaInicio, horaFin | actualizarAgenda() | Asociación (N:1) | Agenda |
| | | | Asociación (N:1) | Profesional Clínico |
| | | | Asociación (N:1) | Espacio |
| **Espacio** | idEspacio, nombre, tipoEspacio, capacidad | — | — | — |
| **Cita** | idCita, fecha, hora, lugar, estado | asignarParticipantes()<br>enviarConfirmacion()<br>validarNuevoHorario()<br>liberarHorario() | Asociación (N:1) | Paciente |
| | | | Asociación (N:1) | Profesional Clínico |
| | | | Asociación (N:1) | Espacio |
| | | | Asociación (N:N) | Representante |
| | | | Composición (1:N) | Recordatorio |
| **Horario Recurrente** | idHorario, diaSemana, hora, frecuencia, fechaInicio, fechaFin | — | Asociación (1:N) | Cita |
| | | | Asociación (N:1) | Plan de Intervención |
| **Recordatorio** | idRecordatorio, fechaEnvio, canal, mensaje | enviar() | Asociación (N:N) | Representante |

### 3.8 M7: Gestión de seguridad de la información

| Entidad | Atributos | Operaciones / Métodos | Tipo de relación | Entidad relacionada |
|---|---|---|---|---|
| **Perfil de Acceso** | idPerfil, nombrePerfil, especialidad | agruparPermisos() | Agregación (N:N) | Permiso |
| **Permiso** | idPermiso, recurso, accion, especialidad | — | — | — |
| **Registro de Acceso** | idRegistro, usuario, fechaHora, informacionConsultada | mostrarDetalle() | — | — |
| **Registro de Modificación** | idRegistro, usuario, fechaHora, valorAnterior, valorNuevo | mostrarDetalle() | — | — |
| **Reporte de Auditoría** | idReporte, periodo, fechaGeneracion, hallazgos | consolidarRegistros() | Agregación (N:N) | Registro de Acceso |
| | | | Agregación (N:N) | Registro de Modificación |

---

## 4. Notas y supuestos

### 4.1 Resumen

- **Entidades:** 42 (6 actores y 36 del dominio).
- **Relaciones:** 98 (74 de asociación, 10 de agregación, 7 de composición y 7 de dependencia).

### 4.2 Entidades sin métodos

Historia Clínica, Consentimiento, Institución Educativa, Resultado de Instrumento, Informe, Servicio, Interconsulta, Espacio, Horario Recurrente y Permiso no tienen métodos porque ninguna es sujeto de una acción en las especificaciones; las acciones sobre ellas las ejecuta otra entidad. Son clases de datos.

### 4.3 Elementos agregados por convención

`iniciarSesion()` y `credenciales` no provienen de una línea específica de la especificación. Se agregan a los actores humanos porque el módulo M7 exige control de accesos y el reto pide un portal para representantes. El Paciente no los tiene porque es menor de edad y no usa el sistema; su representante lo hace por él.

### 4.4 Composiciones

Expediente → Historia Clínica, Evaluación → Resultado de Instrumento, Plan de Intervención → Objetivo Terapéutico, Servicio y Tarea Terapéutica, Objetivo Terapéutico → Indicador de Progreso, y Cita → Recordatorio. Si se elimina el todo, se elimina la parte.

### 4.5 Relaciones N:N a validar con el centro

- **Representante N:N Paciente:** depende de si atienden hermanos y de cómo manejan a padres separados.
- **Profesional Clínico N:N Paciente:** un niño tiene varios terapeutas y cada terapeuta atiende varios niños.
- **Equipo de Caso N:N Profesional Clínico:** un profesional participa en los equipos de varios pacientes.

### 4.6 Supuestos de cardinalidad

- **Expediente N:1 Institución Educativa:** se guarda solo la escuela actual del niño. Si se requiere el historial de escuelas, pasa a N:N.
- **Evaluación 1:1 Diagnóstico:** cada evaluación inicial produce un diagnóstico; las reevaluaciones no generan un diagnóstico nuevo.
- **Diagnóstico 1:N Plan de Intervención:** un mismo diagnóstico da origen a los planes de los distintos ciclos.

### 4.7 Mejoras opcionales

- **Herencia:** los cinco actores humanos comparten `credenciales` e `iniciarSesion()`. Se podría crear una clase padre **Usuario** con esos elementos y que los actores la hereden.
- **Notación UML:** la cardinalidad usa 1 y N. Si se requiere la notación UML con opcionales, se convierte directamente (por ejemplo, 0..1 o 0..*).
- **Agente de planificación:** si se incorpora a las especificaciones, se agregan las entidades Agente de Planificación, Perfil del Caso, Caso Similar, Protocolo Clínico y Propuesta de Plan.
