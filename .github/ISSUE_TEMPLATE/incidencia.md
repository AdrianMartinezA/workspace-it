---
name: Incidencia o error (Bug)
about: Plantilla para registrar errores, fallos de validación o problemas detectados durante el desarrollo de WorkSpace IT
title: "[BUG-XX] "
labels: ["bug"]
assignees: ["AdrianMartinezA"]
---

## 1. Descripción del problema
- **Tarea relacionada (`T01`–`T33`):** `TXX`
- **Caso de prueba o requisito asociado (`CP-XX` / `RF-XX`):** `CP-XX`
- **Entorno:** `Local (Laragon - PHP 8 / MySQL)` / `Producción (Render / Railway)`
- **Resumen del fallo:** Explicación breve de qué ocurre y en qué controlador, consulta SQL o vista se produce.

## 2. Pasos para reproducir el problema
1. Iniciar sesión con el rol `...` (o abrir Postman en el endpoint `...`).
2. Enviar los siguientes datos / realizar la acción `...`.
3. Observar la respuesta del servidor o el comportamiento en pantalla.

## 3. Resultado esperado
Describir qué debería hacer la aplicación según los requisitos y criterios de aceptación (código HTTP, respuesta JSON, cambio en base de datos o mensaje en la interfaz).

## 4. Resultado obtenido
Describir qué ocurre realmente (mensaje de error, código HTTP devuelto, comportamiento en el navegador o estado en MySQL).

## 5. Gravedad / Prioridad y Estado
- **Gravedad:** `Crítica` / `Alta` / `Media` / `Baja` *(añadir etiqueta `gravedad: ...`)*
- **Área afectada:** `Base de datos` / `Backend - API REST` / `Seguridad - Roles` / `Frontend - Interfaz`
- **Estado inicial:** `Abierta (Pendiente)`

## 6. Solución aplicada y comprobación posterior *(rellenar al resolver)*
- **Causa raíz identificada:** 
- **Rama y commit de corrección:** `fix/BUG-XX-...` (`Fixes #...`)
- **Archivos modificados:** 
- **Comprobación posterior (prueba de regresión):** Repetición del caso `CP-XX` y verificación de que pasa a estado `Superada`.
