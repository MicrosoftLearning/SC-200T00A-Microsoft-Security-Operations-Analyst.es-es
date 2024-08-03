---
lab:
  title: "Ejercicio 1: realización de la búsqueda de amenazas en Microsoft\_Sentinel"
  module: Learning Path 8 - Perform threat hunting in Microsoft Sentinel
---

# Ruta de aprendizaje 8 - Laboratorio 1 - Ejercicio 1: realización de búsqueda de amenazas en Microsoft Sentinel

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod8_L1_Ex1.png)

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Has recibido inteligencia sobre amenazas referente a una técnica de comando y control (C2 o C&C). Debes realizar una búsqueda y vigilar la amenaza.

>**Importante:** los datos de registro usados en el laboratorio se han creado en el módulo anterior. Consulta **Ataque 3** en el servidor WIN1 en el ejercicio 5.

>**Nota:** puesto que ya has experimentado el proceso de exploración de datos en un módulo anterior, este laboratorio facilita una instrucción KQL para empezar.

>**Nota:** hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Perform%20threat%20hunting%20in%20Microsoft%20Sentinel)** que te permite realizar tus propias selecciones a tu entera discreción. Es posible que encuentres pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: crear una consulta de búsqueda

En esta tarea, crearás una consulta de búsqueda, marcarás un resultado y crearás una secuencia en vivo.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona **Registros** 

1. Escribe la siguiente instrucción KQL en el espacio *Nueva consulta 1*:

   >**Importante:** pega primero las consultas de KQL en el Bloc de notas y luego copia de allí a la ventana de registro *Nueva consulta 1* para evitar errores.

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. Revisa los distintos resultados. Ahora has identificado las solicitudes de PowerShell que se ejecutan en tu entorno.

1. Activa la casilla de los resultados que muestra "*-file c2.ps1"*.

1. En la barra de comandos central del panel *Resultados*, selecciona el botón **Agregar marcador**.

1. Selecciona **+ Agregar nueva entidad** en *Asignación de entidades*.

1. En *Entidad*, selecciona **Host ** y después, **Nombre de host** y **Equipo** para los valores.

1. En *Tácticas y técnicas*, selecciona **Comando y control**.

1. En la hoja *Agregar marcador*, selecciona **Crear**. Asignaremos este marcador a un incidente más adelante.

1. Cierra la ventana *Registros* seleccionando la **X** en la parte superior derecha de la ventana y selecciona **Aceptar** para descartar los cambios. 

1. Selecciona de nuevo el área de trabajo de Microsoft Sentinel y después, la página **Búsqueda** en el área *Administración de amenazas*.

1. Selecciona la pestaña **Consultas** y luego **+ Nueva consulta** en la barra de comandos.

1. En la ventana *Crear consulta personalizada*, en *Nombre*, escribe **Búsqueda de PowerShell**.

1. Para la *Consulta personalizada*, escribe la siguiente instrucción KQL:

    ```KQL
    let lookback = 2d; 
    SecurityEvent 
    | where TimeGenerated >= ago(lookback) 
    | where EventID == 4688 and Process =~ "powershell.exe"
    | extend PwshParam = trim(@"[^/\\]*powershell(.exe)+" , CommandLine) 
    | project TimeGenerated, Computer, SubjectUserName, PwshParam 
    | summarize min(TimeGenerated), count() by Computer, SubjectUserName, PwshParam 
    | order by count_ desc nulls last 
    ```

1. Desplázate hacia abajo y en *Asignación de entidades*, selecciona:

    - En la lista desplegable *Tipo de entidad*, selecciona **Host**.
    - En la lista desplegable *Identificador*, selecciona **HostName**.
    - En la lista desplegable *Valor*, selecciona **Equipo**.

1. Desplázate hacia abajo y en *Tácticas y técnicas*, selecciona **Comando y control** y luego selecciona **Crear** para crear la consulta de búsqueda.

1. En la hoja *"Microsoft Sentinel - Búsqueda",* busca la consulta que acabas de crear en la lista, *Búsqueda de PowerShell*.

1. Selecciona **Búsqueda de PowerShell** en la lista.

1. Revisa el número de resultados en el panel central en la columna *Resultados*.

1. Selecciona el botón **Ver resultados** en el panel derecho. La consulta KQL se ejecutará automáticamente.

1. Cierra la ventana *Registros* seleccionando la **X** en la parte superior derecha de la ventana y selecciona **Aceptar** para descartar los cambios. 

1. Haz clic con el botón secundario en la consulta **Búsqueda de PowerShell** y selecciona **Agregar a retransmisión en directo**. **Sugerencia:** esto también se puede hacer deslizando hacia la derecha y seleccionando los puntos suspensivos **(...)** al final de la fila para abrir un menú contextual.

1. Revisa que el *estado* sea ahora *En ejecución*. Esto se ejecutará cada 30 segundos en segundo plano y recibirás una notificación en Azure Portal (icono de campana) cuando se encuentre un nuevo resultado. 

1. Selecciona la pestaña **Marcadores** en el panel central.

1. Selecciona el marcador que acabas de crear en la lista de resultados.

1. En el panel derecho, desplázate hacia abajo y selecciona el botón **Investigar**. **Sugerencia:** puede tardar un par de minutos en mostrar el gráfico de investigación.

1. Explora el gráfico de investigación al igual que lo hiciste con el módulo anterior. Observa el gran número de *Alertas relacionadas* para *WINServer*.

1. Cierra la ventana del gráfico *Investigación* seleccionando la **X** de la esquina superior derecha de la ventana. 

1. Oculta la hoja derecha seleccionando el icono **>>** y desplazándote a la derecha hasta que veas el icono de puntos suspensivos **(...).**

1. Selecciona **Agregar a incidente existente**. Todos los incidentes aparecen en el panel derecho.

1. Selecciona un incidente y después, **Agregar**.

1. Desplázate a la izquierda para observar que la columna *Gravedad* se rellena ahora con los datos del incidente.


### Tarea 2: crear una regla de consulta NRT

En esta tarea, en lugar de usar LiveStream, crearás una regla de consulta de análisis NRT. Las reglas NRT se ejecutan cada minuto y retroceden un minuto. Una ventaja de las reglas NRT es que pueden usar la lógica de creación de alertas e incidentes.

1. Selecciona la página **Análisis** en *Configuración* en Microsoft Sentinel. 

1. Selecciona la pestaña **Crear** y después **Regla de consulta de NRT**.

1. Esto inicia el "Asistente de reglas de análisis". Para el tipo de pestaña *General*:

    |Configuración|Value|
    |---|---|
    |Nombre|**Búsqueda de PowerShell NRT**|
    |Descripción|**Búsqueda de PowerShell NRT**|
    |Tácticas|**Comando y control**|
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

1. Selecciona el botón *Respuesta automatizada* y luego selecciona el botón **Siguiente: revisar y crear**.

1. En la pestaña *Revisar y crear*, selecciona el botón **Guardar** para crear y guardar la nueva regla de Análisis programado.

### Tarea 3: crear un trabajo de búsqueda

En esta tarea, usarás un trabajo de búsqueda para buscar un C2.

>**Nota:** la operación *Restaurar* incurre en costes que pueden agotar los créditos de suscripción de Azure Pass. Por este motivo, no realizarás la operación de restauración en este laboratorio. Pero puedes hacer lo siguiente para realizar la operación de restauración en tu propio entorno.

1. Selecciona la página **Buscar** en *General* en Microsoft Sentinel.

1. En el cuadro de búsqueda, escribe **reg.exe** y luego selecciona **Iniciar**.

1. Se abre una nueva ventana que ejecuta la consulta. Selecciona el icono de puntos suspensivos **(...)** en la parte superior derecha y luego cambia al **Modo de trabajo de búsqueda**.

1. Selecciona el botón **Buscar trabajo** en la barra de comandos. 

1. El trabajo de búsqueda crea una nueva tabla con los resultados en cuanto llegan. Los resultados se pueden consultar en la pestaña *Búsquedas guardadas*.

1. Cierra la ventana *Registros* seleccionando la **X** en la parte superior derecha de la ventana y selecciona **Aceptar** para descartar los cambios.

1. Selecciona la pestaña **Restauración** en la barra de comandos y luego el botón **Restaurar**.

1. En *Seleccionar una tabla para restaurar*, busca y selecciona **SecurityEvent**.

1. Revisa las opciones disponibles y luego selecciona el botón **Cancelar**.

    >**Nota:** si estabas ejecutando el trabajo, la restauración se ejecutará durante un par de minutos y los datos estarán disponibles en una nueva tabla.

## Continúa con el ejercicio 2
