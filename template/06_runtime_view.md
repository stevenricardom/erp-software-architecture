# 6. Vista de Ejecución (Runtime View)

## 6.1. Escenario: Cargar un Documento en el Módulo de Gestión Documental

**Historia de usuario relacionada:** Como auxiliar administrativo, quiero subir documentos
(actas, contratos, manuales) con categoría y fecha, para que queden centralizados y
accesibles.

![Diagrama de Secuencia - Cargar y Consultar Documento](./images/c3_secuencia_cargar_documento.png)

**Descripción del flujo:**

1. El **auxiliar administrativo** selecciona el archivo a cargar desde la interfaz WPF del
   Módulo de Gestión Documental y diligencia los metadatos obligatorios (categoría y fecha).
2. La **Capa de Presentación** envía la solicitud a la **Capa de Lógica de Negocio**, que
   primero valida la extensión del archivo contra el catálogo de tipos permitidos.
   - Si el tipo de archivo **no está permitido**, el sistema retorna un error y la interfaz lo
     muestra al usuario, sin persistir ningún dato (criterio de aceptación 2).
3. Si el tipo de archivo es válido, se valida que los **metadatos obligatorios** (categoría y
   fecha) estén completos.
   - Si faltan metadatos obligatorios, el sistema retorna un error y la interfaz lo muestra al
     usuario.
4. Si el archivo y los metadatos son válidos, la **Capa de Acceso a Datos** guarda el
   documento en la base de datos y registra la acción en `Auditoria_Documento`, dejando
   constancia de qué usuario realizó la carga y en qué momento (criterio de aceptación 1 y 3).
5. La interfaz actualiza el listado de documentos y confirma al usuario que el documento
   quedó guardado y disponible.
6. En un segundo momento, cualquier usuario autorizado puede **consultar** un documento del
   listado: el sistema recupera el documento junto con la información de auditoría (usuario que
   lo subió y fecha de carga) y la muestra en pantalla (criterio de aceptación 3).

**Aspectos notables de la interacción:**

- La validación de tipo de archivo ocurre **antes** de cualquier persistencia, evitando guardar
  archivos no permitidos en el repositorio documental.
- El guardado del documento y el registro de auditoría se realizan como parte del mismo flujo
  transaccional, garantizando que todo documento cargado tenga siempre su historial asociado.
- La consulta de un documento reutiliza la información de auditoría en lugar de duplicar los
  datos de "quién" y "cuándo" dentro de la tabla de documentos, favoreciendo la trazabilidad
  ante futuras acciones (ej. reemplazo o eliminación de un documento).
