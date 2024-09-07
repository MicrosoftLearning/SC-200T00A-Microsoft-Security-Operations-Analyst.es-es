# Módulo 5: configuración del entorno de Microsoft Sentinel

**Nota**: La finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md).

**Importante:** esta demostración no es necesaria para VTD-5002-FY25.

## Exploración de la interfaz de Microsoft Sentinel

1. Vuelva a la instancia de Microsoft Sentinel que has creado anteriormente mientras completabas la [sección de requisitos previos](00-prerequisites.md#deploy-azure-sentinel-workspace-for-demo-in-module-4).

1. Navega por el área de trabajo de Microsoft Sentinel recién creada para familiarizarte con las opciones de la interfaz de usuario.

## Creación de una lista de reproducción

En esta tarea, crearás una lista de reproducción.

1. En el cuadro de búsqueda de la parte inferior de la pantalla, escribe `Notepad`.  Selecciona **Bloc de notas** en los resultados.

1. Escribe `Hostname` y luego Entrar para una nueva línea.

1. De la fila 2 a la 6, agrega los siguientes nombres de host:
    ```
    Host1
    Host2
    Host3
    Host4
    Host5
    ```

1. En el menú selecciona **Archivo - Guardar como**, asigna al archivo el nombre `HighValue.csv`.  Luego cambia el tipo de archivo a **Todos los archivos (*.*)**.  Después, seleccione **Guardar**.

1. Cierre el Bloc de notas.

1. En Microsoft Sentinel, selecciona la opción **Lista de control** en el área **Mis listas de control**.

1. Selecciona **Agregar nuevo** en la barra de comandos.

1. En el Asistente para listas de control, escribe lo siguiente: Nombre: HighValueHosts Descripción: hosts de alto valor Alias de lista de reproducción: HighValueHosts

1. Selecciona **Siguiente: Origen >**.

1. Busca el archivo `HighValue.csv` que acabas de crear. 

1. Una vez cargado el archivo CSV, selecciona **Nombre de host** en el cuadro desplegable **Campo SearchKey**.

1. Selecciona **Siguiente: Revisar y crear >**.

1. Seleccione **Crear**.

1. La pantalla vuelve a las listas de reproducción.

1. Selecciona la nueva lista de reproducción.  En la pestaña derecha, selecciona **Ver en Log Analytics**.

1. La siguiente instrucción KQL se ejecuta automáticamente con los resultados mostrados.

```KQL
_GetWatchlist('HighValueHosts')
```
**Nota**: puede tardar un minuto en completarse la importación.

Ahora puedes usar _GetWatchlist("HighValueHosts") en tus propias instrucciones KQL para acceder a la lista. La columna a la que se va a hacer referencia sería *Nombre de host*.

## Creación de un indicador de amenazas.

En esta tarea, crearás un indicador.

1. En Microsoft Sentinel, selecciona la opción **Inteligencia sobre amenazas** en el área **Administración de amenazas**.

1. Selecciona **Agregar nuevo** en la barra de comandos.

1. Revisa los distintos tipos de indicador disponibles en la lista desplegable Tipos.  Luego selecciona **Nombre de dominio**. Escribe las iniciales en el cuadro Dominio. Un ejemplo sería fmg.com.

1. Para el tipo de amenaza, selecciona **+ Agregar** y copia y pega **actividad malintencionada** en el campo.

1. Para el nombre, escribe el mismo valor usado para el dominio. Un ejemplo sería fmg.com.

1. Establece el campo **Válido del** hasta la fecha de hoy.

1. Seleccione **Aplicar**.

**Nota**: puede tardar un minuto en aparecer el indicador.

1. Selecciona la opción **Registros** en el área General.  Es posible que tengas que deshabilitar la opción "Mostrar siempre las consultas" para ir a la ventana de consulta.

1. Ejecuta la instrucción KQL siguiente:

```KQL
ThreatIntelligenceIndicator 
```
Desplázate a la derecha para ver la columna DomainName. También puedes ejecutar la siguiente instrucción KQL para ver simplemente la columna DomainName.  

```KQL
ThreatIntelligenceIndicator 
| project DomainName
```
## Has completado la demostración.