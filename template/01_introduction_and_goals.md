# 1. Introducción y Objetivos

## 1.1. Objetivo del Sistema

El **ERP de Gestión de Propiedad Horizontal** es una aplicación de escritorio pensada para
centralizar y automatizar la administración operativa de conjuntos residenciales. Actualmente
esta labor se realiza mediante canales dispersos (WhatsApp, llamadas, correos, hojas de
cálculo y documentos físicos), lo que genera pérdida de información, falta de trazabilidad y
retrasos en la atención de los residentes.

El sistema busca resolver este problema integrando en una sola plataforma la gestión de
residentes y propietarios, el registro y seguimiento de PQRS (peticiones, quejas, reclamos y
solicitudes), la administración de mantenimiento preventivo y correctivo, la gestión documental,
la generación de reportes e indicadores, y la auditoría de todas las acciones realizadas sobre
el sistema.

## 1.2. Resumen de Requisitos (Requirements Overview)

A continuación se listan los requisitos de negocio más relevantes, agrupados por módulo.
Se destaca el **Módulo de Gestión Documental**, que es el módulo con mayor nivel de detalle
de diseño hasta el momento (ver historia de usuario de carga de documentos).

### Módulo de Gestión Documental (prioridad alta)

- El sistema debe permitir a un auxiliar administrativo **subir documentos** (actas, contratos,
  manuales) indicando obligatoriamente **categoría** y **fecha**.
- El sistema debe **validar el tipo de archivo** antes de aceptar la carga y mostrar un error si
  el tipo no está permitido.
- El sistema debe permitir **consultar** un documento y visualizar **quién lo subió y cuándo**.
- Los documentos cargados deben quedar **centralizados** y accesibles para los roles
  autorizados.

### Módulo de Gestión de Usuarios y Roles

- El sistema debe permitir el registro, edición y desactivación de usuarios.
- Cada usuario debe tener un rol (Administrador, Auxiliar Administrativo, Personal de
  Mantenimiento, Personal de Vigilancia, Residente/Propietario) que determina las funciones a
  las que tiene acceso.

### Módulo de Gestión de Residentes

- El sistema debe permitir registrar residentes, propietarios y sus apartamentos/unidades
  asociadas.

### Módulo de Gestión de PQRS

- El sistema debe permitir registrar una solicitud, asignarle un responsable, hacer seguimiento
  de su estado y cerrarla.

### Módulo de Mantenimiento

- El sistema debe permitir programar y registrar actividades de mantenimiento preventivo y
  correctivo, y asociarlas a un responsable.

### Módulo de Reportes y Auditoría

- El sistema debe generar reportes e indicadores de gestión (tiempos de atención, solicitudes
  resueltas, etc.).
- El sistema debe registrar un historial de auditoría de las acciones relevantes realizadas por
  los usuarios.

## 1.3. Metas de Calidad (Quality Goals)

| Prioridad | Meta de calidad     | Escenario / Motivación                                                                 |
|-----------|----------------------|------------------------------------------------------------------------------------------|
| 1         | Seguridad            | La información de residentes y documentos es sensible; se requiere autenticación, roles y permisos. |
| 2         | Confiabilidad        | No se debe perder información de PQRS ni de documentos cargados; se requieren respaldos. |
| 3         | Usabilidad           | El personal administrativo no siempre es experto en tecnología; la interfaz debe ser intuitiva. |
| 4         | Rendimiento          | Las consultas y registros deben responder en menos de 3 segundos.                        |
| 5         | Mantenibilidad       | La arquitectura por capas debe facilitar la incorporación de nuevos módulos.             |
| 6         | Escalabilidad        | El sistema debe poder administrar múltiples conjuntos residenciales sin degradar el rendimiento. |

## 1.4. Stakeholders

| Rol / Nombre                              | Contacto                | Expectativas                                                                 |
|--------------------------------------------|--------------------------|--------------------------------------------------------------------------------|
| Administrador del conjunto                 | Administración del conjunto | Contar con visibilidad y control total de la operación del conjunto residencial. |
| Auxiliar administrativo                    | Oficina de administración | Registrar y dar seguimiento ágil a solicitudes, residentes y documentos.       |
| Personal de mantenimiento                  | Área de mantenimiento    | Recibir y actualizar el estado de las actividades asignadas.                   |
| Personal de vigilancia                     | Área de vigilancia       | Consultar la información permitida según su rol, sin acceso a datos sensibles.  |
| Residentes y propietarios                  | Conjunto residencial     | Registrar PQRS y consultar el estado de sus solicitudes de forma transparente.  |
| Steven Ricardo Montenegro (Desarrollador)  | Universidad Manuela Beltrán | Cumplir los objetivos académicos y funcionales del proyecto.                   |
| Carlos Eduardo Mujica Reyes (Docente)      | Universidad Manuela Beltrán | Evaluar la calidad arquitectónica y técnica del proyecto.                      |
