# Registro de pruebas: WorkSpace IT

Cada caso se anota con su resultado real al ejecutarlo. Si falla, se marca como **Fallida**, se abre una incidencia vinculada y, tras corregirla, se repite el caso junto con los casos cercanos del mismo módulo antes de marcarlo como **Superada**.

## Plantilla

| ID | Requisito | Acción o procedimiento | Resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|---|---|
| CP-XX | RF-XX | Pasos y datos de entrada | Respuesta, código HTTP o estado en MySQL | Lo observado al ejecutar | Pendiente / Superada / Fallida |

## Casos previstos

| ID | Requisito | Acción o procedimiento | Resultado esperado | Resultado obtenido | Estado |
|---|---|---|---|---|---|
| CP-01 | RF-03 Crear una reserva | Como Empleado, buscar disponibilidad para el 20/01/2027 de 09:00 a 13:00 y reservar el puesto P-01 con un monitor | HTTP 201, reserva activa en MySQL y visible en «Mis reservas» | Sin ejecutar | Pendiente |
| CP-02 | RF-04 Rechazar solapamientos | Con CP-01 activa, otro usuario intenta reservar P-01 ese día de 11:00 a 15:00 | HTTP 409, ninguna fila nueva y aviso del conflicto | Sin ejecutar | Pendiente |
| CP-03 | RF-05 Cancelar una reserva | Cancelar una reserva futura desde «Mis reservas» | Estado cancelada y el puesto vuelve a aparecer libre | Sin ejecutar | Pendiente |
| CP-04 | RF-02 Recurso en mantenimiento | El Técnico IT pone la Sala A en mantenimiento y un Empleado intenta reservarla | La sala no aparece libre y la API rechaza la reserva | Sin ejecutar | Pendiente |
| CP-05 | RF-06 Notificar una avería | Notificar una avería sobre el monitor de una reserva | Incidencia abierta, monitor averiado y visible en el panel IT | Sin ejecutar | Pendiente |
| CP-06 | RF-01 Acceso por roles | Con sesión de Empleado, llamar a `POST /api/usuarios` y abrir el panel de administración | HTTP 403, redirección al panel propio y sin cambios en la base de datos | Sin ejecutar | Pendiente |
| CP-07 | RF-07 Cupo y horario | El Administrador fija cupo 2 y horario de 08:00 a 20:00; un Empleado intenta una tercera reserva o reservar a las 21:30 | Ambas rechazadas con HTTP 422 indicando la regla | Sin ejecutar | Pendiente |
