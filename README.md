# Proyecto Dieno – Gestión de Imprenta (AppSheet + PostgreSQL)

Repositorio académico para la tesis y el sistema de gestión de **Dieno Impresos**.  
Foco actual: **AppSheet** como capa de aplicación sobre la base **PostgreSQL** ya diseñada.  
Los prototipos previos de Front/Back quedan **en pausa**; se preservan solo para referencia.

---

## Estado del proyecto

| Componente | Estado |
| --- | --- |
| Base de datos PostgreSQL | ✅ Aprobada y poblada con datos de prueba |
| AppSheet (App no-code) | 🚧 En construcción |
| Backend FastAPI | ⏸️ Pausado |
| Frontend React | ⏸️ Pausado |
| Documentación de tesis | 🟡 En curso |

---

## Objetivo

Disponer de una app interna para la imprenta que permita **trazabilidad de solicitudes de trabajo**, **gestión de materiales, procesos, equipos y empleados**, con **reportes básicos**; todo **sin código** con AppSheet y **persistencia en PostgreSQL**.

---

## Equipo

| Nombre | Rol |
| --- | --- |
| **Jonathan E. Guillén** | Dirección, BD, AppSheet, Documentación |
| **Andrea Rubiolo** | Co-desarrollo AppSheet, QA, Documentación |

> Trabajo en **dupla**. Se gestionan tareas con _Issues_, _Milestones_ y un _Project_ Kanban.

---

## Estructura del repositorio


AppSheet Database (opción nativa): alternativa cuando no querés administrar motor; ideal para prototipos rápidos.

Conexión a SQL administrado (Cloud SQL/AWS/Azure): requiere IP pública y allowlist.

Hojas (Sheets/Excel): opción simple, pero menos robusta para concurrencia/volumen.
