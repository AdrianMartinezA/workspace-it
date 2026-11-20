# Matriz de requisitos y criterios de aceptación: WorkSpace IT

Se actualiza al cierre de los hitos H4, H5 y H6.

| Requisito | Criterio de aceptación | Verificación | Evidencia | Estado |
|---|---|---|---|---|
| RF-01 Inicio de sesión y roles | Solo entran credenciales válidas y cada perfil accede únicamente a sus rutas | CP-06, IC-04 | Respuestas 401 y 403 en Postman y redirección por rol | Pendiente |
| RF-02 Catálogo y estados | El Técnico IT crea, edita, da de baja y cambia el estado de los recursos | CP-04, IC-02 | Peticiones a `/api/recursos` y cambios en MySQL | Pendiente |
| RF-03 Búsqueda y reserva | El Empleado filtra por fecha, hora y zona, ve solo lo libre y reserva | CP-01 | JSON de disponibilidad y reserva guardada | Pendiente |
| RF-04 Sin solapamientos | Se rechaza toda reserva que se cruce con otra activa del mismo recurso | CP-02, IC-01 | Respuesta 409 y tabla sin duplicados | Pendiente |
| RF-05 Mis reservas | El Empleado consulta su historial y cancela reservas futuras, que liberan el recurso | CP-03 | Estado cancelado y recurso disponible de nuevo | Pendiente |
| RF-06 Averías | Una avería queda registrada y bloquea el equipo afectado | CP-05 | Fila en `incidencias` y equipo averiado en el panel IT | Pendiente |
| RF-07 Administración | El Administrador gestiona usuarios, roles, horario y cupo | CP-07, IC-03 | Cambios en `parametros` y reservas fuera de regla rechazadas | Pendiente |
| RNF-01 Seguridad e integridad | Contraseñas con bcrypt, consultas preparadas, entradas validadas y claves foráneas activas | IC-05, IC-06 | Hashes en la base de datos y scripts sin errores | Pendiente |
| RNF-02 Móvil y accesibilidad | Vistas adaptables sin scroll horizontal, válidas en W3C y comprensibles para los usuarios | IC-07, IC-08 | Capturas en ambas resoluciones, Lighthouse y fichas de usuarios | Pendiente |
| RNF-03 Despliegue seguro | Aplicación pública con HTTPS y credenciales solo en variables de entorno | T01, T29 y T30 | `.env.example` en el repositorio y URL con HTTPS | En curso |
