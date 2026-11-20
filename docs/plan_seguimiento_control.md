# Plan de seguimiento y control: WorkSpace IT (Fase 4A)

**Alumno:** Adrián Martínez Alarcón · **Ciclo:** 2.º DAW · **Curso:** 2026/2027

## 1. Procedimiento de seguimiento del trabajo

### Frecuencia de revisión
- **Al acabar cada sesión de trabajo**, de dos a cuatro por semana: subir los cambios a la rama de la tarea y mover su tarjeta si cambia de estado.
- **Cada lunes:** comparar el tablero con el diagrama de Gantt, pasar a «Esta semana» las tareas de los siete días siguientes y ajustar la carga a las horas reales disponibles.
- **Al cerrar cada hito:** comprobar que todas sus tareas están en «Hecho», revisar los indicadores asociados, fusionar `develop` en `main` y hacer la copia de seguridad completa.

### Estados del tablero
**Pendiente**, **Esta semana**, **En curso** con un máximo de dos tareas a la vez, **En revisión** y **Hecho**.

### Evidencias según el tipo de tarea
- Base de datos: scripts ejecutados sin errores en una base limpia y consulta de solapamientos que solo devuelve filas cuando hay cruce.
- Backend: capturas de Postman con una petición válida y varias erróneas con su código HTTP.
- Frontend: vista sin errores en consola, validada en W3C y revisada en escritorio y móvil.
- Diseño y documentación: archivo subido a `docs/` con su commit.

### Actuación ante fallos o retrasos
- Si una comprobación falla, la tarjeta vuelve a «En curso» y no se empieza ninguna tarea dependiente.
- Si un problema bloquea más de una hora, se anota, se avanza otra tarea independiente y se retoma al día siguiente.
- Si el retraso supera una semana o pone en riesgo un hito, se usa el margen de Navidad y, si no basta, se aplazan los elementos opcionales registrándolo en `registro_cambios.md`.

### Lista de comprobación para considerar terminada una tarea
- [ ] El entregable existe y cumple el resultado verificable de la Fase 3.
- [ ] El código está en GitHub con un mensaje del tipo `feat(T15): ...` y sin credenciales ni `.env`.
- [ ] Si es de base de datos, el script se ejecuta sin errores y respeta las claves foráneas.
- [ ] Si es un endpoint, está probado en Postman con un caso válido y con casos erróneos o sin permisos.
- [ ] Si es una vista, se adapta a escritorio y móvil, tiene sus etiquetas `label` y no muestra errores en consola.
- [ ] No queda abierta ninguna incidencia crítica o alta relacionada.
- [ ] La documentación de `docs/` afectada está actualizada.

## 2. Indicadores de calidad

| Indicador | Qué controla | Cómo se comprueba | Resultado aceptable | Cuándo |
|---|---|---|---|---|
| IC-01 Reservas solapadas | Reservas incompatibles sobre un mismo recurso | Enviar en Postman reservas con cruce total, parcial y envolvente sobre un recurso ya reservado | Todas rechazadas con HTTP 409 y ninguna fila duplicada | H3, H4 y T26 |
| IC-02 Recursos no operativos | Que no se reserve un recurso en mantenimiento o averiado | Marcar un recurso en mantenimiento, consultar disponibilidad y forzar su reserva | No aparece en el buscador y la API la rechaza | H4 y T26 |
| IC-03 Reglas de reserva | Fechas pasadas, horario y cupo | Reservar en fecha pasada, con fin anterior al inicio, fuera de horario o superando el cupo | Todas rechazadas con HTTP 422 y aviso en el formulario | H4 y T26 |
| IC-04 Acceso por roles | Que cada perfil acceda solo a sus rutas | Acceder sin sesión y con rol Empleado a rutas de Técnico IT y Administrador | HTTP 401 sin sesión y HTTP 403 en accesos cruzados | H4 y T27 |
| IC-05 Credenciales y entradas | Contraseñas, inyección SQL y XSS | Revisar hashes y enviar campos vacíos, `' OR 1=1 --` y `<script>` | Hashes bcrypt, consultas preparadas y ningún script ejecutado | H4 y T27 |
| IC-06 Integridad de datos | Coherencia entre tablas | Importar los scripts en una base limpia y dar de baja un recurso con historial | Cero errores SQL, claves foráneas activas e historial conservado | H3 y T29 |
| IC-07 Adaptación a móvil | Uso en escritorio y teléfono | Revisar a 1920x1080 y 390x844 y reservar desde un móvil real | Sin scroll horizontal y botones utilizables | Bloque 6 y T28 |
| IC-08 Accesibilidad y usabilidad | Marcado, contraste y comprensión | W3C, Lighthouse y cuestionario a usuarios | Sin errores críticos, accesibilidad mínima de 90 y media de 4 sobre 5 | T18 y T28 |
| IC-09 Requisitos sin fallos críticos | Cobertura funcional | Revisar matriz de requisitos, registro de pruebas e Issues | Requisitos esenciales superados y ningún Issue crítico o alto abierto | H5 y H6 |
| IC-10 Cumplimiento de hitos | Avance frente al Gantt | Comparar en cada hito las tarjetas en «Hecho» con lo planificado | Desviación máxima de tres días y cierre antes del 12/02/2027 | Cada hito |
