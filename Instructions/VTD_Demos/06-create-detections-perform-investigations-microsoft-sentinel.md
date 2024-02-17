# Módulo 6: creación de detecciones y realización de investigaciones con Microsoft Sentinel

**Nota** La finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md). 

## Creación de una regla de consulta de NRT

En esta tarea, crearás una regla de consulta de análisis de NRT (casi en tiempo real).

1. Selecciona la página **Análisis** en *Configuración* en Microsoft Sentinel.

1. Selecciona la pestaña **Crear** y después **Regla de consulta de NRT**.

1. Esto inicia el "Asistente de reglas de análisis". Para el tipo de pestaña *General*:

    |Configuración|Value|
    |---|---|
    |Nombre|**Búsqueda de PowerShell NRT**|
    |Descripción|**Buscar PowerShell de NRT**|
    |Tácticas y técnicas|**Comando y control**|
    |Gravedad|**Alta**|

1. Selecciona el botón **Siguiente: establecer la lógica de la regla**. 

1. Para la *Consulta de regla*, escribe la siguiente instrucción KQL:

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

1. Selecciona **Ver los resultados de la consulta >** para asegurarte de que la consulta no tenga errores.

1. Cierra la ventana *Registros* seleccionando la **X** en la parte superior derecha de la ventana y selecciona **Aceptar** para descartar los cambios. 

1. Selecciona **Probar con datos actuales** en *Simulación de resultados*. Observa la cantidad prevista de *Alertas al día*.

1. En *Asignación de entidades*, selecciona:

    - En la lista desplegable *Tipo de entidad*, selecciona **Host**.
    - En la lista desplegable *Identificador*, selecciona **HostName**.
    - En la lista desplegable *Valor*, selecciona **Equipo**.

1. Desplázate hacia abajo y selecciona el botón **Siguiente: Configuración de incidentes>**.

1. En la pestaña *Configuración de incidentes*, deja los valores predeterminados y selecciona el botón **Siguiente: respuesta automatizada >**.

1. Selecciona **Siguiente: revisar + crear >**.

1. En la pestaña *Revisar y crear*, selecciona el botón **Guardar** para crear y guardar la nueva regla de Análisis programados.

## Windows de detección de ataques configurado con el agente de Azure Monitor (AMA)

En esta tarea, investigarás el incidente creado a partir de la regla `NRT` que has creado.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** del administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** del administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. En `Microsoft Sentinel`, ve a la sección de menú `Threat management` y selecciona **Incidentes**

**Nota** El `Incident` puede tardar varios minutos en aparecer.

1. Deberías ver un incidente que coincida con los `Severity` y `Title` que has configurado en la regla `NRT` que has creado

1. Selecciona el `Incident` y se abrirá el panel `detail`

1. Selecciona **Ver detalles completos** y selecciona el botón **Investigar**.

1. Explora el `Entities` asociado con el entonces incidente `NRT PowerShell Hunt`.

1. Cierra la ventana `Investigation` seleccionando la **X** en la parte superior derecha de la ventana.

1. Selecciona la pestaña `Logs` e introduce la siguiente instrucción KQL:

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam
    ```

**Nota** Puedes encontrar esta consulta en `Queries History` y **ejecutarla** desde allí.

1. Selecciona el botón **Listo** para cerrar la ventana `Logs`.

1. Cierra la ventana `Incident` seleccionando la **X** en la parte superior derecha de la ventana.

## Has completado la demostración
