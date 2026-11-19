# Registro y Gestión de Cambios — WorkSpace IT

En este documento se valoran y registran las solicitudes de cambio (funcionales, técnicas, de recursos o de planificación) que surjan durante el desarrollo de **WorkSpace IT**, evaluando su impacto antes de decidir si se aprueban, se aplazan o se descartan.

---

## 1. Plantilla de registro de cambios

| Campo | Descripción |
|---|---|
| **ID del cambio** | Identificador correlativo (`RC-01`, `RC-02`...) |
| **Descripción y motivo** | Qué se propone cambiar y por qué es necesario (nueva necesidad, dificultad técnica o ajuste de calendario) |
| **Impacto en tareas, recursos y planificación** | Tareas `T01`–`T33` afectadas, nuevos recursos necesarios, horas adicionales e impacto en alcance o costes |
| **Decisión adoptada** | `Aprobado` / `Aplazado` / `Descartado` y justificación |
| **Fecha y responsable** | Fecha de la valoración y responsable (`Adrián Martínez Alarcón`) |
| **Documentos a actualizar** | Archivos de `docs/`, scripts `sql/` o tarjetas de GitHub Projects que deben modificarse |

---

## 2. Registro de cambios (ejemplos iniciales de valoración en Fase 4A)

> **Nota:** Los siguientes registros (`RC-01` y `RC-02`) ilustran la aplicación del procedimiento de control de cambios sobre supuestos planteados durante la planificación de las Fases 3 y 4A.

| ID | Descripción y motivo | Impacto en tareas, recursos y planificación | Decisión adoptada | Fecha y responsable | Documentos que deberán actualizarse |
|---|---|---|---|---|---|
| **RC-01** *(Simulado)* | **Añadir notificaciones por correo electrónico al confirmar o cancelar reservas.**<br>*Motivo:* Mejorar el aviso al empleado cuando confirma una reserva o cuando el Técnico IT cancela una reserva por avería sobrevenida del recurso. | **Tareas afectadas:** `T15`, `T16` y `T25`.<br>**Recursos:** Servicio SMTP de pruebas **Mailtrap** (plan gratuito ya contemplado en `.env.example`) y librería PHPMailer o función SMTP.<br>**Tiempo y alcance:** Añade unas **+4 h** al Bloque 7 y una dependencia externa (`R07`). Coste: **0 €**. | **Aplazado (condicionado al Hito H5)**.<br>Se mantiene como mejora opcional en `T25`: solo se implementará si el día `24/01/2027` (`H5`) todas las funciones esenciales están terminadas sin retraso. | 19/11/2026<br>Adrián Martínez Alarcón | `docs/plan_ejecucion.md`, `.env.example`, `docs/decisiones_tecnicas.md` y tarjeta `T25` en GitHub Projects. |
| **RC-02** *(Simulado)* | **Gestionar el préstamo de equipo como registro vinculado dentro de la misma transacción de reserva de puesto.**<br>*Motivo:* Prevenir el riesgo `R03` de la Fase 3 (que se guarde el puesto pero falle el bloqueo del equipo portátil o monitor solicitado junto a él). | **Tareas afectadas:** `T04` (modelo E-R), `T07` (DDL SQL) y `T15` (creación de reservas).<br>**Recursos:** Transacciones `PDO::beginTransaction()` y `commit()/rollBack()` en PHP 8 y MySQL (InnoDB).<br>**Tiempo y alcance:** **+0 h** (se absorbe dentro de las 5 h de `T04` y 7 h de `T15`). Coste: **0 €**. | **Aprobado**.<br>Se incorpora al diseño del modelo de datos en `T04` porque garantiza la integridad de los datos (`IC-06`) sin aumentar horas ni costes. | 19/11/2026<br>Adrián Martínez Alarcón | `docs/diagrama_bd.pdf` (`T04`), `sql/01_schema.sql` (`T07`) y `docs/decisiones_tecnicas.md`. |
