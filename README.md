Proyecto DIENO – Gestión Operativa de Imprenta 📦🖨️

Práctica Profesional (AUSI) – Universidad Nacional de Córdoba

📌 Descripción

DIENO es una imprenta que necesita centralizar la trazabilidad de órdenes de trabajo, materiales, procesos y equipo, con foco en control operativo interno (no se gestiona cobros/pagos).
Este repo acompaña la implementación en AppSheet apoyada en una base de datos PostgreSQL ya diseñada (DER, scripts SQL y datos de prueba).

En esta fase se descarta el backend/frontend propio (React/FastAPI) y se prioriza AppSheet sobre la misma BD para acelerar la entrega, mantener gobernanza de datos y simplificar despliegue.

🎯 Objetivos

Registrar y seguir solicitudes de trabajo desde la recepción hasta el cierre.

Controlar materiales, procesos, equipos y asignaciones de personal.

Tableros operativos (estado, prioridad, cuellos de botella) y reportes.

Dejar la BD preparada para futuras integraciones (si luego se retoma API/Front).

🧱 Arquitectura final (sin backend propio)
Capa	Tecnología	Rol
App	AppSheet	UI/UX, formularios, vistas, acciones y automatizaciones.
Datos	PostgreSQL	Persistencia de entidades del sistema.
Modelo	Esquema SQL normalizado	Tablas, FKs, índices y datos semilla.
Fuentes de datos compatibles con AppSheet (opciones)

AppSheet Database (nativa, gestionada por AppSheet). Útil para apps simples o cuando no querés administrar un motor propio.

Hojas: Google Sheets, Microsoft Excel/OneDrive.

Bases SQL administradas (con IP pública y lista de permitidos):

Cloud SQL (Google Cloud): PostgreSQL y MySQL.

AWS/Azure/otros: PostgreSQL, MySQL, SQL Server vía instancias administradas (p. ej., RDS/Aurora/Azure SQL) con firewall/allowlist configurado.

Elegimos PostgreSQL administrado con IP pública y reglas de firewall para permitir el acceso de AppSheet. (AppSheet no puede conectarse a un Postgres local sin túneles o exponer la DB).

🗃️ Modelo de datos (resumen)

cliente_corporativo (CUIT único, contacto)

estado_solicitud (catálogo)

solicitud_trabajo (FK cliente/estado, prioridad, características de impresión, acabados)

proceso, equipo, empleado, material (maestros)

N:M: procesoxsolicitud, equipo_proceso, empleado_proceso, material_solicitud

informes_estadisticos (auditoría/reportes)

En la carrera, la BD es la columna vertebral del sistema y se trabaja con DER, normalización y motores relacionales; tu diseño está alineado con ese enfoque.

🔌 Conectar AppSheet con PostgreSQL (paso a paso)

Alojá la BD en un servicio administrado (p. ej., Cloud SQL Postgres).

Habilitá IP pública y configura firewall/allowlist con las IPs de AppSheet.

En AppSheet: Data → New Data Source → Cloud database → PostgreSQL.

Cargá host, puerto, DB, usuario/clave y probá conexión.

Add table por cada tabla necesaria y define slices si hace falta.

🗂️ Estructura del repo
/
├─ database/
│  ├─ schema.sql           # DDL completo (tablas, claves, índices)
│  ├─ seed.sql             # Datos de ejemplo (10 filas por tabla)
│  └─ views/                # (opcional) vistas para AppSheet
├─ docs/
│  ├─ DER_chen.png
│  ├─ diagrama_clases.png
│  └─ diseño_general.md
├─ appsheet/
│  ├─ capturas/            # Screens de vistas, acciones, bots
│  └─ definiciones/        # CSV/JSON de columnas, tipos, UX
└─ README.md

🚀 Cómo levantar el entorno de datos

Crear DB en Postgres administrado.

Ejecutar en orden:

database/schema.sql

database/seed.sql

(Opcional) ejecutar vistas/índices extras en database/views/.

🧭 Gestión en GitHub
Milestones iniciales

M1 – Base de Datos lista: DDL, datos semilla, conexión AppSheet OK.

M2 – App mínima (MVP): CRUD Solicitudes + Estados, lista y detalle.

M3 – Operación: Procesos, Materiales, Asignaciones, Equipos.

M4 – Reportes: Vistas de tablero y KPIs básicos.

M5 – Calidad: Validaciones, roles, seguridad AppSheet.

Project (kanban)

Columnas: Backlog → To do → In progress → In review → Done.
Vincular issues a milestones.

Labels sugeridas

tipo:datos, tipo:appsheet, tipo:docs, prio:alta, bug, mejora, ayuda, bloqueado.

Plantillas de issues (/.github/ISSUE_TEMPLATE)

feature.md (plantilla de historia de usuario: Como [rol] quiero [función] para [beneficio]).

bug.md (pasos, esperado/obtenido, evidencias).

tarea.md (checklist técnico).

Wiki (ítems sugeridos)

Arquitectura final (AppSheet + Postgres).

Modelo de datos (DER, diccionario).

Guía de conexión AppSheet (con capturas).

UX en AppSheet (vistas, acciones, bots/automatizaciones).

Seguridad y roles (restringir tablas/columnas, filtros).

👥 Equipo
Nombre	Rol
Guillén, Jonathan	Líder funcional y de datos (AppSheet + PostgreSQL)
Rubiolo, Andrea	Co-diseño funcional, pruebas y documentación

Nota: el proyecto inició como equipo de 3; actualmente continúa en dupla, centrado en AppSheet y BD.

📚 Alineación académica

El plan de trabajo sigue la Metodología clásica de Estudio de Sistemas: Estudio Preliminar → Planeamiento → Relevamiento → Diagnóstico → Diseño → Implementación/Seguimiento, tal como se dicta en O&AS (Villagra).
En Sistemas de Datos II se enfatiza DER, normalización, y práctica con motores relacionales (SQL Server, Oracle, MySQL, Postgres), fundamentos aplicados en este diseño.

🔐 Licencia

Privado/Académico. Reutilización condicionada al proyecto de cátedra.

Anexos útiles para AppSheet

AppSheet Database (opción nativa): alternativa cuando no querés administrar motor; ideal para prototipos rápidos.

Conexión a SQL administrado (Cloud SQL/AWS/Azure): requiere IP pública y allowlist.

Hojas (Sheets/Excel): opción simple, pero menos robusta para concurrencia/volumen.
