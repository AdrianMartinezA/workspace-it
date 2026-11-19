# Registro de Pruebas y Comprobaciones — WorkSpace IT

En este documento se registran los casos de prueba funcionales, de validación, seguridad y usabilidad definidos para verificar el comportamiento de **WorkSpace IT**.

> **Nota de estado (Fase 4A — 19/11/2026):** De acuerdo con la planificación del proyecto, la implementación de la base de datos, backend y frontend se desarrolla entre los bloques 3 y 7. Por tanto, todos los casos de prueba se encuentran actualmente diseñados y en estado **`Pendiente`** para su ejecución conforme se completen los hitos `H3`, `H4`, `H5` y el Bloque 8 (`T26`–`T28`).

---

## 1. Plantilla de caso de prueba

| Campo | Descripción |
|---|---|
| **ID de prueba** | Código único (`CP-01`, `CP-02`...) |
| **Funcionalidad / Requisito** | Requisito funcional o no funcional (`RF-XX` / `RNF-XX`) y tarea (`TXX`) verificada |
| **Acción o procedimiento** | Pasos concretos y datos de entrada empleados en DBeaver, Postman o navegador |
| **Resultado esperado** | Respuesta exacta que debe dar el sistema (código HTTP, JSON, estado en MySQL o vista) |
| **Resultado obtenido** | Resultado real observado al ejecutar la prueba *(vacío mientras esté pendiente)* |
| **Estado** | `Pendiente` / `Superada` / `Fallida` |

---

## 2. Casos de prueba previstos

| ID | Funcionalidad / Requisito relacionado | Acción o procedimiento que se realizará | Resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|---|---|
| **CP-01** | **Creación correcta de una reserva** (`RF-04`, tareas `T15` y `T24`) | Iniciar sesión como `Empleado`, buscar disponibilidad para una fecha futura (p. ej. `20/01/2027` de `09:00` a `13:00`), seleccionar un puesto con estado `Disponible` y un monitor libre, y enviar la solicitud (`POST /api/reservas`). | El servidor responde `HTTP 201 Created`, inserta la reserva con estado `Activa` en MySQL y la interfaz muestra el aviso de confirmación y la reserva en la vista «Mis reservas». | — *(Pendiente de ejecución en H4/H5)* | **Pendiente** |
| **CP-02** | **Rechazo de reservas solapadas** (`RF-05`, indicador `IC-01`, tareas `T08`, `T15` y `T26`) | Con la reserva del `CP-01` activa (`09:00`–`13:00` sobre el mismo recurso y fecha), enviar desde otro usuario o desde Postman una segunda solicitud para ese mismo recurso con horario cruzado (`11:00`–`15:00`). | El servidor detecta la colisión con la consulta SQL de solapamientos, rechaza la operación con `HTTP 409 Conflict`, no inserta ninguna fila en `reservas` e informa del conflicto horario al usuario. | — *(Pendiente de ejecución en H3/H4/T26)* | **Pendiente** |
| **CP-03** | **Modificación / cancelación de una reserva existente** (`RF-06`, tareas `T16`, `T20` y `T24`) | Desde el panel «Mis reservas» del `Empleado`, seleccionar una reserva futura activa y pulsar «Cancelar reserva» (o modificar el tramo horario cancelando y reservando el nuevo tramo libre). | El endpoint actualiza el estado de la reserva a `Cancelada` (`HTTP 200 OK`), el recurso vuelve a aparecer inmediatamente como libre en `GET /api/disponibilidad` para ese horario y la reserva pasa al historial. | — *(Pendiente de ejecución en H4/H5)* | **Pendiente** |
| **CP-04** | **Bloqueo de reserva sobre recurso en mantenimiento** (`RF-03` y `RF-05`, indicador `IC-02`, tareas `T13`, `T14` y `T26`) | Con rol `Técnico IT`, cambiar el estado de la `Sala A` a `En mantenimiento`. A continuación, con rol `Empleado`, consultar disponibilidad para mañana e intentar forzar `POST /api/reservas` sobre la `Sala A`. | La `Sala A` no aparece como reservable en el buscador de disponibilidad y la petición directa a la API es rechazada con código `HTTP 409 Conflict` indicando que el recurso no está operativo. | — *(Pendiente de ejecución en H4/T26)* | **Pendiente** |
| **CP-05** | **Notificación de avería sobre equipo reservado** (`RF-07`, tareas `T16`, `T20` y `T21`) | Con rol `Empleado`, abrir el formulario de incidencia desde una reserva en «Mis reservas», describir un fallo en el equipo asociado y enviarlo (`POST /api/incidencias`). Revisar después el panel del `Técnico IT`. | Se registra la incidencia en la tabla `incidencias` con estado `Abierta`, el equipo vinculado pasa a estado `Averiado` / `En mantenimiento` para evitar nuevos préstamos y aparece en la bandeja del Técnico IT. | — *(Pendiente de ejecución en H4/H5)* | **Pendiente** |
| **CP-06** | **Control de acceso por roles (RBAC) ante acceso no autorizado** (`RF-01` y `RNF-01`, indicador `IC-04`, tareas `T12` y `T27`) | Con una sesión iniciada con rol `Empleado`, intentar acceder desde el navegador al panel de administración y enviar desde Postman una petición `POST /api/usuarios` o `PUT /api/recursos/1` para crear o editar recursos. | El middleware de autorización (`T12`) intercepta la petición, devuelve `HTTP 403 Forbidden` en la API (y redirige al panel de empleado en la vista web) y no modifica ningún dato en MySQL. | — *(Pendiente de ejecución en H4/T27)* | **Pendiente** |
| **CP-07** | **Validación de límites horarios y modificación de parámetros por el Administrador** (`RF-08`, indicador `IC-03`, tareas `T17`, `T22` y `T26`) | Con rol `Administrador`, fijar el cupo máximo en `2` reservas activas por empleado y el horario de oficina de `08:00` a `20:00`. Intentar después como `Empleado` crear una tercera reserva activa o reservar a las `22:00`. | El servidor guarda los nuevos parámetros en la tabla `parametros` y rechaza con `HTTP 400/422` tanto la tercera reserva simultánea como la reserva fuera del horario permitido, mostrando la regla incumplida. | — *(Pendiente de ejecución en H4/T26)* | **Pendiente** |
