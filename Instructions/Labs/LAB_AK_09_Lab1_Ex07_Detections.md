---
lab:
  title: 'Ejercicio 7: creación de detecciones'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 7: creación de detecciones

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex7.png)

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Vas a trabajar con consultas KQL de Log Analytics y, a partir de ahí, crearás reglas de análisis personalizadas para ayudar a descubrir amenazas y comportamientos anómalos en tu entorno.

Las reglas de análisis buscan eventos o conjuntos de eventos específicos en tu entorno, te avisan cuando se alcanzan determinados umbrales de eventos o condiciones, generan incidentes para que el SOC evalúe e investigue, y responden a las amenazas con procesos de seguimiento y corrección automatizados.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: detectar ataques de persistencia

>**Importante:** los pasos siguientes se realizan en una máquina diferente a la que trabajabas anteriormente. Busca las referencias de nombre de máquina virtual.

En esta tarea, crearás una detección para el primer ataque del ejercicio anterior.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. En la sección **Registros**, selecciona *General*.

1. **Ejecutar** la siguiente instrucción KQL para recuperar las tablas en las que tenemos estos datos:

    ```KQL
    search "temp\\startup.bat"
    ```

    >**Nota:** un resultado con el evento puede tardar hasta 5 minutos en aparecer. Espera hasta que lo haga. Si no aparece, asegúrate de haber reiniciado WINServer como se indica en el ejercicio anterior y de haber completado la Tarea nº 3 del Laboratorio de la Ruta de aprendizaje 6, Ejercicio 2.

1. La tabla *SecurityEvent* busca tener los datos ya normalizados y fáciles de consultar. Expande la fila para ver todas las columnas relacionadas con el registro.

1. A partir de los resultados, ahora sabemos que el actor de amenazas usa reg.exe para agregar claves a la clave del registro, y el programa se encuentra en C:\temp. **Ejecutar** la siguiente instrucción para reemplazar el operador *search* por el operador *where* de nuestra consulta:

    ```KQL
    SecurityEvent 
    | where Activity startswith "4688" 
    | where Process == "reg.exe" 
    | where CommandLine startswith "REG" 
    ```

1. Es importante ayudar al analista del Centro de operaciones de seguridad proporcionando la mayor cantidad posible de contexto sobre la alerta. Esto incluye la proyección de entidades para su uso en el gráfico de investigación. **Ejecuta** la siguiente consulta:

    ```KQL
    SecurityEvent 
    | where Activity startswith "4688" 
    | where Process == "reg.exe" 
    | where CommandLine startswith "REG" 
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = SubjectUserName
    ```

1. Ahora que tienes una buena regla de detección, en la ventana Registros, selecciona la **+ Nueva regla de alertas** en la barra de comandos y luego selecciona **Crear alerta de Microsoft Sentinel**. Esto creará una nueva regla programada. **Sugerencia:** es posible que tengas que seleccionar el botón de puntos suspensivos (...) en la barra de comandos.

1. Se abre el Asistente para reglas de análisis. Para el tipo de pestaña *General*:

    |Configuración|Valor|
    |---|---|
    |Nombre|RegKey de inicio|
    |Descripción|RegKey de inicio en c:\temp|
    |Tácticas|Persistencia|
    |Gravedad|Alto|

1. Selecciona el botón **Siguiente: establecer la lógica de la regla**.

1. En la pestaña *Establecer la lógica de la regla*, la *consulta de regla* debe estar ya rellenada con la consulta KQL.

1. Configura las entidades en *Mejora de alertas: asignación de entidades* mediante los parámetros de la tabla siguiente.

    |Entidad|Identifier|Campo de datos|
    |:----|:----|:----|
    |Cuenta|FullName|AccountCustomEntity|
    |administrador de flujos de trabajo|Nombre de host|HostCustomEntity|

1. En *Programación de consultas*, establece lo siguiente:

    |Configuración|Valor|
    |---|---|
    |Ejecutar consulta cada|5 minutos|
    |Buscar datos del último|1 día|

    >**Nota:** estamos generando muchos incidentes a propósito para los mismos datos. Esto permite al laboratorio usar estas alertas.

1. Deja el resto de las columnas con las opciones predeterminadas. Selecciona el botón **Siguiente: configuración de incidentes >**.

1. En la pestaña *Configuración de incidentes*, deja los valores predeterminados y selecciona el botón **Siguiente: respuesta automatizada >**.

1. En la pestaña *Respuesta automatizada* en *Reglas de automatización*, selecciona **Agregar nuevo**.

1. Usa la configuración de la tabla para configurar la regla de automatización.

    |Configuración|Valor|
    |:----|:----|
    |Nombre de la regla de Automation|RegKey de inicio|
    |Desencadenador|Al crear un incidente|
    |Acciones |Ejecución de playbooks|
    |guía |PostMessageTeams-OnIncident|

    >**Nota:** ya has asignado permisos en el cuaderno de estrategias, por lo que estará disponible.

1. Seleccione **Aplicar**.

1. Seleccione **Siguiente: Revisión y creación >**.
  
1. En la pestaña *Revisar y crear*, seleccione el botón **Guardar** para crear la nueva regla de Análisis programados.

### Tarea 2: detectar ataques de elevación de privilegios

En esta tarea, crearás una detección para el segundo ataque del ejercicio anterior.

1. En el portal de Microsoft Sentinel, selecciona **Registros** en la sección General en caso de que hayas salido de esta página.

1. **Ejecuta** la siguiente instrucción KQL para identificar cualquier entrada que haga referencia a los administradores:

    ```KQL
    search "administrators" 
    | summarize count() by $table
    ```

1. El resultado podría mostrar eventos de tablas diferentes, pero en nuestro caso, queremos investigar la tabla SecurityEvent. El EventID y Event que estamos buscando es "4732: se ha agregado un miembro a un grupo local habilitado para seguridad". Con esto, identificaremos cómo agregar un miembro a un grupo con privilegios. **Ejecuta** la siguiente consulta KQL para confirmar:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    ```

1. Expande la fila para ver todas las columnas relacionadas con el registro. El nombre de usuario de la cuenta agregada como administrador no aparece. El problema es que, en lugar de almacenar el nombre de usuario, tenemos el identificador de seguridad (SID). **Ejecuta** el siguiente KQL para que coincida el SID con el nombre de usuario que se ha agregado al grupo Administradores:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    ```

   ![Instantánea](../Media/SC200_sysmon_attack3.png)

1. Extiende la fila para ver las columnas resultantes. En la última, vemos el nombre del usuario agregado en la columna *UserName1* que *proyectamos* dentro de la consulta KQL. Es importante ayudar al analista de operaciones de seguridad proporcionando todo el contexto sobre la alerta que puedas. Esto incluye la proyección de entidades para su uso en el gráfico de investigación. **Ejecuta** la siguiente consulta:

    ```KQL
    SecurityEvent 
    | where EventID == 4732
    | where TargetAccount == "Builtin\\Administrators"
    | extend Acct = MemberSid, MachId = SourceComputerId  
    | join kind=leftouter (
        SecurityEvent 
        | summarize count() by TargetSid, SourceComputerId, TargetUserName 
        | project Acct1 = TargetSid, MachId1 = SourceComputerId, UserName1 = TargetUserName) on $left.MachId == $right.MachId1, $left.Acct == $right.Acct1
    | extend timestamp = TimeGenerated, HostCustomEntity = Computer, AccountCustomEntity = UserName1
    ```

1. Ahora que tienes una buena regla de detección, en la ventana Registros, selecciona **+ Nueva regla de alertas** en la barra de comandos y luego selecciona **Crear alerta de Microsoft Sentinel**. **Sugerencia:** es posible que tengas que seleccionar el botón de puntos suspensivos (...) en la barra de comandos.

1. Se abre el Asistente para reglas de análisis. Para el tipo de pestaña *General*:

    |Configuración|Valor|
    |---|---|
    |Nombre|**Agregación de usuario a administradores locales de SecurityEvent**|
    |Descripción|**Usuario agregado al grupo de administradores locales**|
    |Tácticas|**Elevación de privilegios**|
    |Gravedad|**Alta**|

1. Selecciona el botón **Siguiente: establecer la lógica de la regla**.

1. En la pestaña *Establecer lógica de regla*, la *consulta de regla* debe rellenarse ya con la consulta KQL, así como las entidades de *Mejora de alertas: asignación de entidades*.

    |Entity|Identifier|Campo de datos|
    |:----|:----|:----|
    |Cuenta|FullName|AccountCustomEntity|
    |administrador de flujos de trabajo|Nombre de host|HostCustomEntity|

1. Si **Nombre de host** no está seleccionado para Entidad de *host*, selecciónela en la lista desplegable y use los parámetros de la tabla anterior para rellenar los campos.

1. En *Programación de consultas*, establece lo siguiente:

    |Configuración|Valor|
    |---|---|
    |Ejecutar consulta cada|5 minutos|
    |Buscar datos del último|1 día|

    >**Nota:** estamos generando muchos incidentes a propósito para los mismos datos. Esto permite al laboratorio usar estas alertas.

1. Deja el resto de las columnas con las opciones predeterminadas. Selecciona el botón **Siguiente: configuración de incidentes >**.

1. En la pestaña *Configuración de incidentes*, deja los valores predeterminados y selecciona el botón **Siguiente: respuesta automatizada >**.

1. En la pestaña *Respuesta automatizada* en *Reglas de automatización*, selecciona **Agregar nuevo**.

1. Usa la configuración de la tabla para configurar la regla de automatización.

   |Configuración|Valor|
   |:----|:----|
   |Nombre de la regla de Automation|Agregación de usuario a administradores locales de SecurityEvent|
   |Desencadenador|Al crear un incidente|
   |Acciones |Ejecución de playbooks|
   |guía |PostMessageTeams-OnIncident|

   >**Nota:** ya has asignado permisos en el cuaderno de estrategias, por lo que estará disponible.

1. Seleccione **Aplicar**.

1. Selecciona el botón **Siguiente: revisar y crear >**.
  
1. En la pestaña *Revisar y crear*, selecciona el botón **Crear** para crear la nueva regla de Análisis programado.

## Continúa con el ejercicio 8
