# ERP - Gestión de Propiedad Horizontal

Documentación de arquitectura de software del proyecto **ERP de Gestión de Propiedad
Horizontal**, desarrollado como parte de la asignatura de Arquitectura del Software de la
Universidad Manuela Beltrán.

## 📌 Descripción del proyecto

Actualmente, muchos conjuntos residenciales administran sus procesos (solicitudes de
mantenimiento, quejas, comunicación con residentes, documentación) mediante canales
dispersos y no integrados: WhatsApp, llamadas telefónicas, correos electrónicos, hojas de
cálculo y documentos físicos. Esto genera pérdida de información, falta de trazabilidad sobre
las solicitudes y retrasos en la atención de los residentes.

Este proyecto propone el desarrollo de un **ERP (Enterprise Resource Planning)**
especializado para la administración de conjuntos residenciales, que centraliza en una sola
plataforma:

- Gestión de residentes y propietarios.
- Registro y seguimiento de PQRS (peticiones, quejas, reclamos y solicitudes).
- Administración de mantenimiento preventivo y correctivo.
- Gestión documental (actas, contratos, manuales).
- Generación de reportes e indicadores de gestión.
- Control de usuarios mediante roles y permisos.
- Auditoría de todas las acciones realizadas sobre el sistema.

El producto es una **aplicación de escritorio** construida en **C# (.NET 8)** con **WPF**,
bajo una arquitectura cliente-servidor por capas, con **Microsoft SQL Server** como motor de
base de datos y **Entity Framework Core** como ORM.

## 📁 Estructura del repositorio

```
erp-software-architecture/
├── docs/
│   ├── images/                        # Diagramas exportados (C1, C2, secuencia, MER, despliegue)
│   ├── 01_introduction_and_goals.md
│   ├── 02_architecture_constraints.md
│   ├── 03_system_scope_and_context.md
│   ├── 04_solution_strategy.md
│   ├── 05_building_block_view.md
│   ├── 06_runtime_view.md
│   ├── 07_deployment_view.md
│   ├── 08_concepts.md
│   └── 10_glossary.md
└── README.md
```

La documentación sigue la plantilla **arc42** para la documentación de arquitecturas de
software, y los diagramas se modelan siguiendo el enfoque **C4 Model** (Contexto,
Contenedores) apoyados con diagramas complementarios UML (secuencia, entidad-relación,
despliegue) elaborados en **PlantUML**.

## 🎓 Sobre el taller

Este repositorio y su documentación son el resultado de un taller académico de Arquitectura
del Software cuyo objetivo era llevar un proyecto ERP desde la gestión ágil del backlog hasta
la documentación formal de su arquitectura. El taller constaba de las siguientes partes:

### 1. Preparación del entorno

- Creación de un espacio de trabajo en **Jira** o **Notion** (plantilla Kanban o Scrum) como
  centro de gestión del Product Backlog y los Sprints.
- Creación de un repositorio público en **GitHub** llamado `erp-software-architecture`, para
  alojar tanto la futura documentación de arquitectura.
- Preparación del entorno de **PlantUML**, ya sea mediante un servidor online (PlantText) o de
  forma local con la extensión "PlantUML" de Jebbs en Visual Studio Code.
- Descarga de la plantilla oficial de **arc42** (versión Markdown) y carga de su estructura de
  carpetas al repositorio como base de la documentación.

### 2. Gestión ágil del backlog

- Creación de una **épica** en Jira/Notion por cada módulo principal del ERP (en el
  documento base del taller: Compras, Facturación, Stock/Costos, Activos Fijos, Empleados y
  EIS).
- Redacción de **historias de usuario** (formato "Como \<rol\>, quiero \<acción\>, para que
  \<beneficio\>") a partir de las funcionalidades descritas para el módulo asignado, con un
  mínimo de 5 historias por módulo.
- Definición de al menos **3 criterios de aceptación** por historia de usuario, en formato
  Dado-Cuando-Entonces.
- **Priorización del backlog** de historias de usuario aplicando la técnica **MoSCoW** (Must
  have, Should have, Could have, Won't have).

### 3. Diagramas de arquitectura (C4 Model)

- **Diagrama de Contexto (C1)**: el sistema ERP representado como caja negra, mostrando su
  interacción con los actores/usuarios y con sistemas externos, modelado en PlantUML con la
  librería C4-PlantUML.
- **Diagrama de Contenedores (C2)**: "zoom" al interior del sistema para mostrar sus
  componentes principales (por ejemplo, aplicación web/frontend, API/backend, base de
  datos), a partir de una arquitectura plausible definida por cada grupo.

### 4. Diseño detallado con UML

A partir de una historia de usuario seleccionada:

- **Diagrama de Secuencia**: mostrando cómo interactúan los distintos contenedores/
  componentes del sistema para cumplir esa historia de usuario.
- **Diagrama de Entidad-Relación (MER)** o **Diagrama de Clases simplificado**: modelando
  las entidades de datos principales asociadas a esa historia de usuario y sus relaciones.

### 5. Documentación en arc42

- Organización del repositorio con una carpeta `docs/images` para alojar todas las imágenes
  de los diagramas generados (C1, C2, secuencia, MER).
- Diligenciamiento de los archivos Markdown de la plantilla arc42 directamente en GitHub:
  - `01_introduction_and_goals.md`: objetivo del sistema y requisitos de negocio del módulo
    trabajado.
  - `02_architecture_constraints.md`: decisiones tecnológicas tomadas (lenguaje, framework,
    base de datos, arquitectura).
  - `03_system_scope_and_context.md`: inserción y explicación del Diagrama de Contexto (C1).
  - `05_building_block_view.md`: inserción del Diagrama de Contenedores (C2) y descripción
    de la responsabilidad de cada contenedor.
  - `06_runtime_view.md`: escenario crítico elegido (por ejemplo, "Registrar un Producto") con
    su Diagrama de Secuencia y explicación del flujo.
  - `07_deployment_view.md` (opcional): descripción de cómo se desplegaría la arquitectura en
    un servidor.
  - `10_glossary.md`: definición de los términos clave del dominio del proyecto.

## 🛠️ Tecnologías

| Categoría              | Tecnología                              |
|-------------------------|-------------------------------------------|
| Lenguaje                | C# (.NET 8)                               |
| Interfaz gráfica        | WPF (Windows Presentation Foundation)     |
| Arquitectura            | Cliente-Servidor, por capas               |
| Base de datos           | Microsoft SQL Server                      |
| ORM                     | Entity Framework Core                     |
| Reportes                | Microsoft RDLC / FastReport               |
| Control de versiones    | Git / GitHub                              |
| Modelado                | PlantUML, StarUML / Visual Paradigm, Draw.io |
| Metodología              | Scrum                                     |

## 👤 Autores

- **Steven Ricardo Montenegro** — Desarrollo
- **Carlos Eduardo Mujica Reyes** — Docente, Arquitectura del Software
- Universidad Manuela Beltrán
