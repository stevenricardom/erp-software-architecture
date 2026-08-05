# 7. Vista de Despliegue

## 7.1. Infraestructura Nivel 1

![Diagrama de Despliegue](./images/deployment_diagram.png)

**Motivación:**

El ERP se despliega bajo un esquema cliente-servidor dentro de la red local (LAN) del
conjunto residencial. Los equipos de cómputo de la administración (administrador, auxiliar
administrativo, personal de mantenimiento y vigilancia) ejecutan la aplicación de escritorio
WPF, mientras que un único servidor centraliza tanto la base de datos como el repositorio de
documentos cargados.

**Características de calidad y/o rendimiento:**

- La concentración de la información en un servidor central facilita los respaldos (backups)
  periódicos y reduce el riesgo de pérdida de información, en línea con la meta de
  confiabilidad.
- Al mantenerse la comunicación dentro de una red local, se favorece el cumplimiento del
  requisito no funcional de rendimiento (respuestas en menos de 3 segundos).
- El esquema es compatible con Windows, cumpliendo la restricción de compatibilidad
  definida para el proyecto.

**Mapeo de bloques de construcción a infraestructura:**

| Bloque de construcción                         | Elemento de infraestructura                          |
|---------------------------------------------------|----------------------------------------------------------|
| Capa de Presentación                               | PC Administrador, PC Auxiliar Administrativo, PC Mantenimiento/Vigilancia |
| Capa de Lógica de Negocio                          | Se ejecuta embebida dentro de la aplicación WPF en cada PC cliente |
| Capa de Acceso a Datos (Entity Framework Core)     | Se ejecuta embebida dentro de la aplicación WPF en cada PC cliente, conectándose remotamente al servidor |
| Base de Datos (Microsoft SQL Server)               | Servidor de Base de Datos (Windows Server)                |
| Repositorio de Documentos                          | Servidor de Base de Datos (Windows Server), en el sistema de archivos |

## 7.2. Infraestructura Nivel 2

### 7.2.1. PC Cliente (Administrador / Auxiliar Administrativo / Mantenimiento / Vigilancia)

Equipos de cómputo con sistema operativo Windows 10/11 sobre los cuales se instala la
aplicación de escritorio del ERP (WPF, .NET 8). Cada equipo se conecta al servidor central a
través de la red local mediante el puerto 1433 (SQL Server) usando Entity Framework Core.

### 7.2.2. Servidor de Base de Datos

Servidor con Windows Server que aloja:

- **Microsoft SQL Server**: motor de base de datos donde se almacena de forma centralizada
  toda la información transaccional del ERP (usuarios, residentes, PQRS, mantenimiento,
  metadatos de documentos y auditoría).
- **Repositorio de Documentos**: carpeta del sistema de archivos donde se almacenan
  físicamente los archivos cargados (actas, contratos, manuales) referenciados desde la base
  de datos.

Sobre este servidor se ejecutan rutinas periódicas de respaldo (backup) tanto de la base de
datos como del repositorio de documentos, para garantizar la confiabilidad de la información
ante fallos de hardware o errores humanos.
