# Registro de Decisiones Técnicas — WorkSpace IT

En este documento se registran las decisiones arquitectónicas, cambios de diseño en base de datos o API REST, elección de herramientas e incidencias relevantes tomadas durante el desarrollo del proyecto, indicando su fecha, motivo y tareas afectadas.

---

## Plantilla de registro

```markdown
### [DT-XX] Título de la decisión
- **Fecha:** DD/MM/AAAA
- **Tareas afectadas:** TXX, TYY
- **Contexto / Motivo:** Explicación del problema o necesidad detectada.
- **Decisión adoptada:** Solución elegida e implementación.
- **Consecuencias:** Impacto en el código, base de datos o planificación.
```

---

## Historial de decisiones

### [DT-01] Definición de arquitectura MVC en PHP 8, API REST y MySQL
- **Fecha:** 15/11/2026
- **Tareas afectadas:** T01, T04, T05, T10–T17
- **Contexto / Motivo:** Se requiere una arquitectura mantenible y sin costes de licencia que separe claramente la lógica de negocio y validación de solapamientos (servidor) de la interfaz de usuario adaptable (cliente).
- **Decisión adoptada:** Implementar el backend en PHP 8 bajo el patrón Modelo-Vista-Controlador (MVC) utilizando PDO con consultas preparadas para MySQL/MariaDB, exponiendo endpoints JSON consumidos mediante Fetch API desde un frontend HTML5 + CSS3 (Bootstrap) + JavaScript ES6+.
- **Consecuencias:** Facilita las pruebas independientes de la API con Postman antes de integrar las vistas y garantiza la validación centralizada de roles y horarios en el servidor.

### [DT-02] Estructura del repositorio, flujo de ramas y gestión de credenciales
- **Fecha:** 15/11/2026
- **Tareas afectadas:** T01, T03, T10, T30, T32
- **Contexto / Motivo:** Es necesario mantener una rama principal siempre estable para los hitos de entrega y evitar la exposición de contraseñas de base de datos o SMTP en el repositorio público.
- **Decisión adoptada:**
  - Organizar el repositorio en tres directorios principales (`src/`, `sql/`, `docs/`).
  - Excluir `.env` desde el primer commit mediante `.gitignore` y distribuir únicamente `.env.example`.
  - Utilizar las ramas `main` (estable por hito), `develop` (integración) y ramas `feature/TXX-descripcion` o `fix/descripcion` con mensajes bajo la convención *Conventional Commits*.
- **Consecuencias:** Trazabilidad directa entre cada commit, su tarea (`T01`–`T33`) en GitHub Projects y los Issues asociados.
