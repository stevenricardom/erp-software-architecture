# 3. Alcance y Contexto del Sistema

## 3.1. Contexto de Negocio

El **ERP de Gestión de Propiedad Horizontal** interactúa con cinco tipos de actores de negocio:
el administrador del conjunto, el auxiliar administrativo, el personal de mantenimiento, el
personal de vigilancia y los residentes/propietarios. Cada uno de ellos utiliza la aplicación de
escritorio (WPF) para realizar operaciones acordes a su rol, mientras que el sistema centraliza
la información en una base de datos SQL Server y delega la generación de reportes a un motor
de reportes especializado.

![Diagrama de Contexto](./images/c1_context.png)

**Explicación de interfaces de dominio externas:**

| Actor / Sistema externo         | Interacción con el ERP                                                                 |
|----------------------------------|--------------------------------------------------------------------------------------------|
| Administrador del conjunto       | Administra usuarios, PQRS, mantenimiento, documentos y reportes.                           |
| Auxiliar administrativo          | Registra residentes, solicitudes (PQRS) y documentos.                                      |
| Personal de mantenimiento        | Consulta y actualiza las actividades de mantenimiento que le fueron asignadas.             |
| Personal de vigilancia           | Consulta información permitida de acuerdo con su rol (permisos restringidos).              |
| Residente / Propietario          | Registra y consulta el estado de sus PQRS.                                                 |
| Microsoft SQL Server             | Almacena de forma centralizada toda la información del sistema.                            |
| Motor de Reportes (RDLC/FastReport) | Genera los reportes e indicadores de gestión solicitados desde el ERP.                  |

## 3.2. Contexto Técnico

El ERP se distribuye como una aplicación de escritorio (WPF) que se instala en los equipos de
cómputo de la administración y se conecta, dentro de la red local del conjunto residencial, a un
servidor centralizado de base de datos.

| Canal / Interfaz técnica                | Protocolo               | Descripción                                                              |
|-------------------------------------------|---------------------------|-----------------------------------------------------------------------------|
| Aplicación WPF → SQL Server                | TCP/IP (puerto 1433) vía Entity Framework Core | Lectura y escritura de la información transaccional del ERP.            |
| Aplicación WPF → Motor de Reportes         | Llamada local / API interna .NET | Generación de reportes e indicadores a partir de la información consultada. |
| Aplicación WPF → Repositorio de documentos | Sistema de archivos del servidor | Almacenamiento físico de los documentos cargados (actas, contratos, manuales). |

**Mapeo de entradas/salidas a canales:**

- Las solicitudes de creación/edición de residentes, PQRS, mantenimiento y documentos se
  envían desde la capa de presentación (WPF) hacia la capa de lógica de negocio, la cual
  persiste los cambios en SQL Server a través de Entity Framework Core.
- Las consultas de reportes e indicadores se resuelven combinando datos de SQL Server con
  el motor de reportes (RDLC/FastReport), y se presentan al usuario dentro de la misma
  aplicación de escritorio.
