# Versionamiento de Objetos (Views, SP, Triggers, etc.)

El Problema actual es que si bien se versiona los cambios, no existe un rastro como tal de lo que
se esta cambiando; ya que lo que se hace actualmente es simplemente crear nuevas clases a criterio propio.

> El objetivo es lograr ordenar los objetos por modulo y tipo, para lograr un mejor versionado y lectura de nuestros archivos.

## Estructura de carpetas
1. Custom
   1. Conciliacion | Monitoreo | Seguimiento | Generador
      1. Views
      2. StoredProcedures
      3. Functions
      4. Triggers
      5. Indexes
      6. ...
## Pasos para nombrar y versionar nuestros objetos

1. Nombrar los archivos de la siguiente manera : `{TipoObjeto}_{Producto}_{NombreObjeto}_{Version}.cs`
   1. Tipo de Objeto: [VW] View, [SP] StoredProcedure, [FN] Functions, [TR] Triggers, [IX] Indexes
   2. Producto:: CIP, SYNDEO
   3. Nombre del Objeto:: UpperCamelCase ó PascalCase
   4. Versión:: v1, v2, v3 ....
* Ejemplo : `VW_SYNDEO_ProcesarConciliacion_v1`  

2. Versión LATEST, considerar lo siguiente :
   1. Está será nuestra versión actual.
   2. Todos los objetos deben de tener está versión, pues nos permitirá saber de forma clara cuál es la versión en curso/actual.
   3. Cuando sea un objeto nuevo, probablemente exista solo un archivo con esta versión; es decir obviaremos lo siguiente del punto `1. - > iii.`  
   

3. Modificación de objetos y reestructuración de archivos
* **Si en caso tenemos solo un archivo.** Por ejemplo: `VW_SYNDEO_ProcesarConciliacion_LATEST.cs`
  * Debemos de copiar el archivo y nombrarlo de la siguiente manera `{TipoObjeto}_{Producto}_{NombreObjeto}_v1.cs` ->`VW_SYNDEO_ProcesarConciliacion_v1.cs`  


* **Si en caso nos encontramos con archivos ya versionados.** Por ejemplo: 
   > VW_SYNDEO_ProcesarConciliacion_v1.cs, VW_SYNDEO_ProcesarConciliacion_v2.cs, VW_SYNDEO_ProcesarConciliacion_LATEST.cs
   * Debemos de copiar el archivo `{..}_LATEST.cs` y nombrarlo de la siguiente manera `{TipoObjeto}_{Producto}_{NombreObjeto}_v{IncrementarVersion}.cs` ->`VW_SYNDEO_ProcesarConciliacion_v3`

Finalmente, debemos de incluir nuestros cambios dentro del archivo `{..}_LATEST.cs`; así tendremos mayor claridad en nuestros cambios

**¡IMPORTANTE!** : Solo se versiona archivos que ya han pasado a producción, para archivos que están en ambientes inferiores trabajar sobre la última versión `{..}_LATEST.cs`
 
