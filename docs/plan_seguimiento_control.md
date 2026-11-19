# Plan de Seguimiento y Control del Proyecto — WorkSpace IT (Fase 4A)

**Alumno:** Adrián Martínez Alarcón  
**Ciclo:** 2.º CFGS Desarrollo de Aplicaciones Web (DAW) · **Curso:** 2026/2027

Este documento recoge el procedimiento de seguimiento del trabajo, la lista de comprobación para dar una tarea por terminada y la tabla de indicadores de calidad aplicables durante el desarrollo de **WorkSpace IT**.

---

## 1. Procedimiento de seguimiento del trabajo

### 1.1. Frecuencia de revisión
- **Al finalizar cada sesión de trabajo (2–4 veces por semana):** subida de cambios a la rama activa (`git push`), actualización de las casillas logradas dentro del Issue y movimiento de la tarjeta en **GitHub Projects** si cambia de estado.
- **Revisión semanal (cada lunes):** contraste del tablero Kanban con el diagrama de Gantt (`docs/plan_ejecucion.md`), paso a la columna *Esta semana* de las tareas planificadas para los siguientes 7 días y ajuste de horas según el calendario de clase y exámenes.
- **Revisión de cierre de hito (`H1` a `H6` y Entrega final):** comprobación de los indicadores de calidad del bloque, fusión de `develop` en `main` si todas las tareas del hito están en *Hecho*, y copia de seguridad completa (`.zip` + `mysqldump`) en OneDrive y Google Drive.

### 1.2. Estados de las tareas en el tablero Kanban
1. **Pendiente:** tareas de bloques futuros planificadas en la Fase 3 que aún no han comenzado.
2. **Esta semana:** tareas seleccionadas cada lunes según el cronograma para trabajar en la semana en curso.
3. **En curso:** tareas en desarrollo activo en su rama `feature/TXX-descripcion` *(límite WIP: máximo 2 tareas simultáneas)*.
4. **En revisión:** tareas cuyo entregable está terminado y pendiente de superar las pruebas locales (DBeaver, Postman, navegador) y la lista de comprobación.
5. **Hecho:** tareas verificadas con su evidencia, subidas al repositorio y con su Issue cerrado.

### 1.3. Lista de comprobación para considerar terminada una tarea (*Definition of Done*)

Antes de mover cualquier tarjeta de **En revisión** a **Hecho**, verifico la siguiente lista de comprobación:

- [ ] **1. Resultado verificable cumplido:** existe el entregable definido en la Tabla 1 de la Fase 3 y cumple su objetivo funcional.
- [ ] **2. Código en el repositorio:** los cambios están subidos (`git push`) en su rama `feature/TXX-*` o fusionados en `develop` siguiendo *Conventional Commits* (`feat(TXX): ...`, `fix(TXX): ...`, `docs(TXX): ...`) y sin credenciales ni archivos `.env`.
- [ ] **3. Comprobación específica según el tipo de tarea:**
  - *Si es de base de datos (`T07`–`T09`):* el script SQL se ejecuta de principio a fin en MySQL/MariaDB sin errores y respeta las claves foráneas.
  - *Si es de backend / API REST (`T10`–`T17`):* el endpoint se ha probado en **Postman** con al menos una petición válida (`200/201`) y una petición inválida o sin permisos (`400/401/403/409`), devolviendo siempre JSON válido.
  - *Si es de frontend / integración (`T18`–`T25`):* la vista se visualiza sin desbordamientos en escritorio (`1920x1080`) y móvil (`390x844`), supera el validador W3C sin errores críticos y no arroja errores en la consola de Chrome DevTools.
- [ ] **4. Sin errores críticos abiertos:** no queda ningún Issue con etiqueta `gravedad: critica` o `gravedad: alta` asociado a la tarea.
- [ ] **5. Documentación actualizada:** si la tarea modifica una tabla, ruta JSON o decisión de diseño, se ha actualizado el documento correspondiente en `docs/`.

---

## 2. Indicadores de calidad del proyecto

| ID | Indicador | Qué aspecto controla | Cómo se comprobará | Resultado aceptable | Cuándo se comprueba |
|---|---|---|---|---|---|
| **IC-01** | **Ausencia de reservas solapadas** | Prevención de reservas incompatibles sobre el mismo puesto, sala o equipo en horarios cruzados. | Ejecutar la consulta SQL en DBeaver (`T08`) y enviar en Postman (`POST /api/reservas`) reservas con cruce total, parcial y envolvente sobre un recurso ya reservado. | El 100 % de los intentos solapados se rechaza con código `HTTP 409 Conflict` y mensaje JSON; 0 reservas solapadas en la tabla `reservas`. | Hito H3 (`T08`), Hito H4 (`T15`) y Bloque 8 (`T26`). |
| **IC-02** | **Bloqueo de recursos en mantenimiento o averiados** | Que ningún empleado pueda reservar un recurso marcado por IT como `En mantenimiento` o `Averiado`. | Cambiar el estado de un recurso a mantenimiento (`T13`/`T21`), consultar `GET /api/disponibilidad` e intentar reservarlo por API. | El recurso no figura como disponible y cualquier petición directa de reserva es rechazada (`HTTP 400/409`). | Hito H4 (`T13`–`T15`) y Bloque 8 (`T26`). |
| **IC-03** | **Cumplimiento de horarios, fechas y cupo** | Correcto funcionamiento de las validaciones de negocio (fechas pasadas, horario de oficina y límite de reservas activas). | Intentar crear reservas en fechas pasadas, con `hora_fin <= hora_inicio`, fuera del horario permitido o superando el cupo configurado por el Administrador. | 100 % de las solicitudes fuera de regla rechazadas en servidor (`HTTP 400/422`) y avisadas en el formulario cliente. | Hito H4 (`T15`, `T17`) y Bloque 8 (`T26`). |
| **IC-04** | **Seguridad de acceso y control de roles (RBAC)** | Protección de contraseñas y restricción de rutas según el rol (`Empleado`, `Técnico IT`, `Administrador`). | Comprobar en MySQL que las claves usan hash `bcrypt` (`$2y$`) e intentar acceder con sesión de Empleado a endpoints y paneles de IT o Admin, y sin sesión. | 0 contraseñas en texto plano; respuestas `HTTP 401` sin sesión y `HTTP 403` en el 100 % de accesos a rutas de un rol superior. | Hito H4 (`T11`, `T12`) y Bloque 8 (`T27`). |
| **IC-05** | **Validación de formularios y prevención SQLi / XSS** | Sanitización de entradas, campos obligatorios y protección frente a inyecciones en login, buscador y averías. | Enviar campos vacíos, cadenas `' OR 1=1 --` en login/filtros y `<script>alert(1)</script>` en la descripción de una avería (`T16`/`T20`). | Uso de consultas preparadas PDO en el 100 % de los modelos; rechazo de campos vacíos y escape del texto sin ejecución de scripts. | Hito H4 (`T10`–`T16`) y Bloque 8 (`T27`). |
| **IC-06** | **Integridad referencial de la base de datos** | Coherencia de los datos entre `usuarios`, `roles`, `zonas`, `recursos`, `reservas` e `incidencias`. | Ejecutar `01_schema.sql` y `02_seed.sql` en una BD limpia y probar la baja lógica (`activo = 0`) de un recurso con reservas previas. | 0 errores SQL al importar scripts; claves foráneas (`FOREIGN KEY`) operativas y 0 registros huérfanos en el historial. | Hito H3 (`T07`, `T09`) y Hito H6 (`T29`). |
| **IC-07** | **Adaptación a dispositivos móviles (Responsive)** | Visualización y manejo de las vistas tanto en ordenador como en teléfono móvil. | Revisar las 5 vistas (`T18`–`T22`) en Chrome DevTools a `1920x1080` y `390x844` px, y realizar una reserva completa desde un móvil real. | 0 desbordamientos horizontales, tablas y tarjetas adaptadas al ancho móvil y botones pulsables sin solaparse. | Bloque 6 (`T18`–`T22`) y Bloque 8 (`T28`). |
| **IC-08** | **Accesibilidad, validez HTML y usabilidad** | Calidad del marcado HTML5/CSS3 y facilidad de comprensión para los usuarios finales. | Validar las vistas en W3C Validator, auditar etiquetas `<label>` y contraste en Lighthouse y pasar el cuestionario de evaluación a usuarios. | 0 errores críticos en W3C Validator, índice de accesibilidad ≥ 90 en Lighthouse y valoración media ≥ 4/5 en el cuestionario. | Bloque 6 (`T18`) y Bloque 8 (`T28`). |
| **IC-09** | **Cobertura funcional y ausencia de fallos críticos** | Cumplimiento de las funcionalidades esenciales de la Fase 2 sin errores bloqueantes conocidos. | Revisar la matriz de requisitos (`docs/matriz_requisitos.md`), el registro de pruebas (`docs/registro_pruebas.md`) y los GitHub Issues abiertos. | 100 % de los requisitos esenciales con pruebas en estado `Superada` y 0 Issues abiertos de gravedad `Crítica` o `Alta`. | Hito H5 (`24/01/2027`) y Hito H6 (`03/02/2027`). |
| **IC-10** | **Cumplimiento de hitos del cronograma** | Control del avance real de las 33 tareas respecto a las fechas de los hitos `H1`–`H6`. | Comparar en cada fecha de hito las tareas en la columna `Hecho` de GitHub Projects frente a lo planificado en el Gantt. | 100 % de las tareas esenciales del bloque completadas con una desviación máxima ≤ 3 días respecto al hito, cerrando antes del 12/02/2027. | En cada hito (`H1` a `H6`). |
