# 2. Restricciones de Arquitectura

## 2.1. Restricciones Técnicas

| Restricción                          | Explicación / Justificación                                                                 |
|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Lenguaje de programación: **C# (.NET 8)** | Plataforma robusta, orientada a objetos, ampliamente usada en aplicaciones empresariales y con excelente integración con Windows. |
| Interfaz gráfica: **WPF (Windows Presentation Foundation)** | Permite construir interfaces modernas y mantenibles, superando a WinForms en experiencia de usuario. |
| Arquitectura: **Cliente-Servidor por capas** (Presentación, Lógica de Negocio, Acceso a Datos) | Facilita la separación de responsabilidades, el mantenimiento y la incorporación de nuevos módulos. |
| Base de datos: **Microsoft SQL Server** | Integración nativa con .NET, buen rendimiento, seguridad y soporte transaccional.               |
| ORM: **Entity Framework Core**         | Reduce código repetitivo de acceso a datos y mejora la mantenibilidad.                          |
| Reportes: **Microsoft RDLC / FastReport** | Generación de reportes e indicadores de gestión integrados con .NET.                            |
| Compatibilidad: **Windows**            | El sistema se ejecuta sobre sistemas operativos Windows, ampliamente utilizados en oficinas administrativas. |

## 2.2. Restricciones Organizativas

| Restricción                 | Explicación                                                                                     |
|-------------------------------|---------------------------------------------------------------------------------------------------|
| Metodología: **Scrum**        | El desarrollo se organiza en sprints con entregas incrementales.                                  |
| Tiempo                        | El desarrollo se realiza dentro del tiempo del semestre académico, priorizando módulos esenciales antes de cada corte de parciales. |
| Costo                         | Se utilizan herramientas gratuitas o con licencia académica para minimizar costos de desarrollo.  |
| Control de versiones          | **Git** y **GitHub** como repositorio central del código fuente.                                  |
| IDE                           | **Visual Studio 2022**.                                                                            |
| Herramientas de modelado      | **StarUML / Visual Paradigm** para diagramas UML y **Draw.io** para diagramas de arquitectura y procesos. |

## 2.3. Convenciones

- El código debe seguir las convenciones de nomenclatura estándar de C#/.NET (PascalCase
  para clases y métodos, camelCase para variables locales).
- Toda entidad de negocio debe contar con su respectiva clase de acceso a datos gestionada
  mediante Entity Framework Core, evitando el acceso directo a SQL Server desde la capa de
  presentación.
- Toda acción relevante sobre residentes, PQRS, mantenimiento o documentos debe quedar
  registrada en el módulo de auditoría.
