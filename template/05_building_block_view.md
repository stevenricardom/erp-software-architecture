# 5. Vista de Bloques de Construcción

## 5.1. Caja Blanca del Sistema General

![Diagrama de Contenedores](./images/c2_containers.png)

**Motivación:**

El ERP se estructura como una aplicación cliente-servidor por capas, ejecutada como
aplicación de escritorio (WPF) que se comunica con una base de datos centralizada. Esta
separación permite que cada capa evolucione de forma independiente y facilita las pruebas y
el mantenimiento del sistema.

**Bloques de construcción contenidos:**

- Capa de Presentación
- Capa de Lógica de Negocio
- Capa de Acceso a Datos
- Módulo de Reportes
- Base de Datos

**Interfaces importantes:**

- Presentación → Lógica de Negocio: llamadas internas .NET (invocación directa de servicios).
- Lógica de Negocio → Acceso a Datos: llamadas internas .NET.
- Acceso a Datos → Base de Datos: TCP/IP mediante Entity Framework Core.
- Presentación → Módulo de Reportes: llamadas internas .NET para solicitar la generación de reportes.

### 5.1.1. Capa de Presentación

*Propósito/Responsabilidad*: Interfaz gráfica de escritorio construida en WPF. Gestiona el
inicio de sesión, la validación de roles y permisos, y expone los módulos funcionales:
Usuarios, Residentes, PQRS, Mantenimiento, Gestión Documental, Reportes y Auditoría.

*Interfaz(es)*: Invoca a la Capa de Lógica de Negocio y al Módulo de Reportes mediante
llamadas internas .NET.

*Requisitos que cumple*: Usabilidad, control de acceso por rol.

### 5.1.2. Capa de Lógica de Negocio

*Propósito/Responsabilidad*: Contiene las reglas de negocio del ERP: asignación de
responsables, seguimiento de solicitudes, validación de metadatos y tipos de archivo
permitidos en la gestión documental, cálculo de indicadores y control de auditoría.

*Interfaz(es)*: Expone servicios a la Capa de Presentación y consume la Capa de Acceso a
Datos.

*Requisitos que cumple*: Trazabilidad, confiabilidad, mantenibilidad.

### 5.1.3. Capa de Acceso a Datos

*Propósito/Responsabilidad*: Traduce las operaciones de negocio en consultas hacia SQL
Server utilizando Entity Framework Core, y gestiona las transacciones.

*Interfaz(es)*: Entity Framework Core hacia SQL Server (TCP/IP).

*Requisitos que cumple*: Rendimiento, confiabilidad.

### 5.1.4. Módulo de Reportes

*Propósito/Responsabilidad*: Genera reportes e indicadores de gestión (PQRS, tiempos de
atención, estadísticas de mantenimiento) a partir de la información almacenada.

*Interfaz(es)*: Microsoft RDLC / FastReport, consumido por la Capa de Presentación.

*Requisitos que cumple*: Elaboración de reportes automáticos, control administrativo.

### 5.1.5. Base de Datos

*Propósito/Responsabilidad*: Almacena de forma centralizada a los residentes, propietarios,
PQRS, actividades de mantenimiento, documentos, usuarios, roles y el historial de auditoría.

*Interfaz(es)*: Microsoft SQL Server, accedido vía TCP/IP mediante Entity Framework Core.

*Requisitos que cumple*: Confiabilidad, seguridad, escalabilidad.

## 5.2. Nivel 2 — Caja Blanca: Módulo de Gestión Documental

Como ejemplo de descomposición de un módulo de negocio, se detalla el **Módulo de Gestión
Documental**, responsable de permitir a los auxiliares administrativos subir, clasificar y
consultar documentos (actas, contratos, manuales).

Componentes internos:

- **Validador de Archivos**: valida la extensión del archivo contra el catálogo de tipos
  permitidos antes de aceptar la carga.
- **Servicio de Documentos**: aplica las reglas de negocio (metadatos obligatorios: categoría y
  fecha) y coordina el guardado del archivo y del registro de auditoría correspondiente.
- **Repositorio de Documentos**: componente de acceso a datos (Entity Framework Core) que
  persiste el documento y su metadata en SQL Server, y el archivo físico en el repositorio de
  documentos del servidor.

El detalle de este módulo, incluyendo el modelo entidad-relación (`DOCUMENTO`,
`CATEGORIA_DOCUMENTO`, `TIPO_ARCHIVO_PERMITIDO`, `AUDITORIA_DOCUMENTO`) y el
diagrama de secuencia de la carga de documentos, se encuentra documentado en la
[Vista de Ejecución (Runtime View)](./06_runtime_view.md).
