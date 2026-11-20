# Registro de cambios: WorkSpace IT

Antes de aplicar cualquier cambio se responde: por qué es necesario, qué tareas, tablas, endpoints o vistas modifica, qué recursos exige, cuántas horas añade y si pone en riesgo el siguiente hito, y si altera el alcance o el coste. La decisión puede ser **Aprobado**, **Aplazado** o **Descartado**.

## Plantilla

| ID | Descripción y motivo | Impacto en tareas, recursos y planificación | Decisión | Fecha y responsable | Documentos a actualizar |
|---|---|---|---|---|---|
| RC-XX | | | | | |

## Registro

| ID | Descripción y motivo | Impacto en tareas, recursos y planificación | Decisión | Fecha y responsable | Documentos a actualizar |
|---|---|---|---|---|---|
| RC-01 | Avisos por correo al confirmar o cancelar reservas, para informar al empleado sin entrar en la aplicación | Afecta a T15, T16 y T25. Requiere Mailtrap y una librería SMTP. Unas 4 horas más y una dependencia externa, sin coste | Aplazado. Solo se hará en T25 si H5 se cierra sin retraso | 19/11/2026, Adrián Martínez | `plan_ejecucion.md`, `.env.example`, `decisiones_tecnicas.md` y tarjeta T25 |
| RC-02 | Guardar puesto y equipo en una misma transacción para que nunca quede una reserva a medias | Afecta a T04, T07 y T15. Transacciones PDO sobre InnoDB, sin recursos nuevos ni horas añadidas | Aprobado, refuerza la integridad sin coste ni retraso | 19/11/2026, Adrián Martínez | Diagrama de la base de datos, `01_schema.sql` y `decisiones_tecnicas.md` |
