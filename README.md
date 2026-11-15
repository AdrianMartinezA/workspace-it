# WorkSpace IT

Sistema web para la gestión de reservas de puestos, salas y préstamo de equipamiento tecnológico en empresas con trabajo híbrido.

Proyecto Intermodular · 2.º CFGS Desarrollo de Aplicaciones Web (DAW)  
**Autor:** Adrián Martínez Alarcón · **Curso:** 2026/2027

## Descripción
WorkSpace IT es una aplicación web para pymes tecnológicas con trabajo híbrido (*hot-desking*). Permite gestionar desde un mismo sitio la reserva de puestos rotativos, salas de reuniones y el préstamo de equipos informáticos y ergonómicos compartidos.

## Problema que resuelve
Sustituye las hojas de cálculo compartidas y los avisos informales, que provocan reservas duplicadas, desconocimiento de la disponibilidad y préstamos de equipos sin registro. La aplicación valida en el servidor que no haya solapamientos y deja un historial para el departamento de IT.

## Funcionalidades previstas
- Inicio de sesión seguro y control de acceso por roles (RBAC): **Empleado**, **Técnico IT** y **Administrador**.
- Gestión (CRUD) de puestos y salas organizados por zonas, e inventario de equipos con su estado (`Disponible` / `En mantenimiento`).
- Buscador de disponibilidad por fecha, franja horaria y categoría, con validación en servidor para evitar reservas solapadas.
- Panel «Mis reservas» con cancelación de reservas futuras y notificación de incidencias/averías.
- Panel de administración de usuarios, roles, horarios y límites de reserva.

## Estructura del repositorio

```text
workspace-it/
├── README.md                 # Presentación y estado del proyecto
├── .gitignore                # Excluye .env, /vendor, /node_modules y temporales
├── .env.example              # Plantilla de variables sin datos reales
├── docs/
│   ├── plan_ejecucion.md       # Tareas, hitos, cronograma, procedimiento y riesgos
│   ├── decisiones_tecnicas.md  # Registro de decisiones técnicas
│   └── diagrama_gantt.png      # Cronograma y diagrama de Gantt del proyecto
├── sql/                      # Scripts 01_schema.sql y 02_seed.sql
└── src/                      # Código MVC (controllers, models, views, public)
```

## Requisitos e instalación en local (entorno de desarrollo)
1. Clonar el repositorio:
   ```bash
   git clone https://github.com/AdrianMartinezA/workspace-it.git
   cd workspace-it
   ```
2. Copiar la plantilla de variables de entorno y configurar las credenciales locales (Laragon / MySQL / Mailtrap):
   ```bash
   cp .env.example .env
   ```
3. Importar los scripts de la carpeta [`sql/`](./sql) (`01_schema.sql` y `02_seed.sql`) cuando estén disponibles a partir del Hito 3.
4. Servir el directorio `src/public` desde Apache (Laragon) con PHP 8.x.

## Estado actual
- [x] Fase 1: Análisis de la necesidad
- [x] Fase 2: Diseño funcional, arquitectura y viabilidad
- [x] Fase 3: Plan de ejecución y repositorio
- [ ] Desarrollo: base de datos, backend, frontend, pruebas y despliegue

## Documentación
La documentación del proyecto está centralizada en la carpeta [`docs/`](./docs):
- [Plan de ejecución](./docs/plan_ejecucion.md)
- [Registro de decisiones técnicas](./docs/decisiones_tecnicas.md)
- [Diagrama de Gantt](./docs/diagrama_gantt.png)
