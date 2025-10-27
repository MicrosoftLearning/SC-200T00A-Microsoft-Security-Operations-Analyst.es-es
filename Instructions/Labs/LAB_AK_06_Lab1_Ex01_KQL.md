---
lab:
  title: "Ejercicio 1: creación de consultas para Microsoft\_Sentinel mediante el Lenguaje de consulta de Kusto (KQL)"
  module: Learning Path 6 - Create queries for Microsoft Sentinel using Kusto Query Language (KQL)
---

# Ruta de aprendizaje 6 - Laboratorio 1 - Ejercicio 1: creación de consultas para Microsoft Sentinel mediante el Lenguaje de consulta Kusto (KQL)

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod4_L1_Ex1.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que va a implementar Microsoft Sentinel. Usted es responsable de analizar los datos de los registros para buscar actividad malintencionada, mostrar visualizaciones y buscar amenazas. Para consultar los datos de los registros, utiliza el lenguaje de consulta Kusto (KQL).

>**Importante:** Los ejercicios de laboratorio de la Ruta de aprendizaje n.º 6 se encuentran en un entorno *independiente*. Si sale del laboratorio sin completarlo, tendrá que volver a ejecutar algunos pasos de configuración.

>**Nota:** Este perfil de laboratorio tarda >15 minutos en compilarse completamente a medida que Microsoft Sentinel se implementa previamente en la suscripción de Azure con el nombre **defenderWorkspace**.

<!--- >**Tip:** This lab involves entering many KQL scripts into Microsoft Sentinel. The scripts were provided in a file at the beginning of this lab. An alternate location to download them is:  <https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Allfiles> --->

### Tiempo estimado para completar este laboratorio: 60 minutos

### Tarea 1: Preparación del área de pruebas de KQL

En esta tarea, instalará la **solución de laboratorio de entrenamiento de Microsoft Sentinel** desde Marketplace, que rellenará un área de trabajo de Log Analytics con datos de ejemplo que puede usar para practicar la escritura de instrucciones KQL.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, navegue a <https://portal.azure.com> e inicie sesión con las credenciales asignadas.

1. En la barra de búsqueda de Azure, escriba **Solución de laboratorio de entrenamiento de Microsoft Sentinel** y selecciónela en los resultados.

    >**Sugerencia:** Estará en la sección Marketplace.

1. En la página **Solución de laboratorio de entrenamiento de Microsoft Sentinel**, seleccione **Crear** para instalar la solución.

1. En la página **Crear solución de laboratorio de entrenamiento de Microsoft Sentinel**, seleccione el grupo de recursos **defender-RG** y el área de trabajo **defenderWorkspace**.

1. Seleccione **Revisar y crear** para implementar la solución.

1. Una vez que se complete la validación, seleccione **Crear** para implementar la solución.

  >**Nota:** Se tardan aproximadamente 10 minutos en la implementación completa de la solución y en que todos los recursos estén disponibles.

1. Espere a que se complete la implementación y, después, seleccione **Inicio** en la ruta de navegación.

### Tarea 2: Exploración del área de trabajo de Log Analytics

1. En la barra de búsqueda de Azure Portal, busque **Microsoft Sentinel** y selecciónelo en los resultados.

1. En la página de Microsoft Sentinel, seleccione el área de trabajo **defenderWorkspace**.

1. En Microsoft Sentinel, expanda la sección **General** y seleccione **Registros** en el menú de navegación.

1. Cierra la ventana emergente del vídeo de Log Analytics que aparece.

1. Cierre el **centro Consultas**.

1. Use el menú desplegable para cambiar de **Modo simple** a **Modo KQL**.

1. Explora las tablas disponibles y otras herramientas que aparecen en el *panel de esquemas y filtros* en el lado izquierdo de la pantalla.

1. En el editor de consultas, escribe la siguiente consulta y luego selecciona **Ejecutar**. Deberías ver los resultados de la consulta en la ventana inferior.

    ```KQL
    SecurityEvent_CL
    ```

    >**Nota:** *SecurityEvent_CL* es una tabla personalizada creada por la solución de laboratorio de entrenamiento de Microsoft Sentinel. Contiene datos de ejemplo que puede usar para practicar la escritura de instrucciones KQL.

1. Observe que el filtro está establecido en **Mostrar: 1000 resultados**.

1. Junto al primer registro, selecciona **>** para expandir la información de la fila.

### Tarea 3: Ejecución de instrucciones KQL básicas

En esta tarea, crearás instrucciones KQL básicas.

>**Importante:** para cada consulta, borra la instrucción anterior de la ventana Consulta o abra una nueva ventana de consulta seleccionando **+** después de la última pestaña abierta (hasta 25).

1. En la siguiente instrucción se muestra el operador **search**, que busca en todas las columnas de la tabla el valor.

1. El valor predeterminado de *Intervalo de tiempo* debe se **Últimas 24 horas** en la ventana de consulta.

1. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    search "Computer"
    ```

    >**Nota:** El uso del operador *Search* sin tablas específicas o cláusulas aptas es menos eficaz que el filtrado de texto específico de la tabla y específico de columna.

1. En la siguiente instrucción se muestra **search** en tablas enumeradas en la cláusula **in**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    search in (SecurityEvent_CL,App*) "new"
    ```

1. Cambia el *Intervalo de tiempo* por **Últimas 24 horas** en la ventana de consulta.

1. Las instrucciones siguientes muestran el operador **where**, que filtra un predicado específico. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    >**Importante:** debes seleccionar **Ejecutar** después de escribir cada consulta en los bloques de código siguientes.

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    ```

    >**Nota:** el *Intervalo de tiempo* ahora muestra *Establecer en la consulta*, ya que estamos filtrando con la columna TimeGenerated.

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d) and EventID_s == 4624
    ```

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | where EventID_s == 4624  
    | where AccountType_s =~ "user"
    ```

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d) and EventID_s in (4624, 4625)
 
    ```

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar *variables*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    let timeOffset = 10m;
    let discardEventID = 4688;
    SecurityEvent_CL
    | where TimeGenerated > ago(timeOffset*60) and TimeGenerated < ago(timeOffset)
    | where EventID_s != discardEventID
    ```

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar una *lista dinámica*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    let suspiciousAccounts = datatable(account: string) [
      @"NA\timadmin", 
      @"NT AUTHORITY\SYSTEM"
    ];
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | where Account_s in (suspiciousAccounts)
    ```

    >**Sugerencia:** puedes volver a dar formato a la consulta fácilmente seleccionando los puntos suspensivos (...) en la ventana Consulta y seleccionando **Dar formato a consulta**.

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar una *tabla dinámica*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    let LowActivityAccounts =
        SecurityEvent_CL 
        | summarize cnt = count() by Account_s 
        | where cnt < 1000;
    LowActivityAccounts | where Account_s contains "sql"
    ```

### Tarea 4: Análisis de resultados en KQL con el operador de resumen

En esta tarea, crearás instrucciones KQL para agregar datos. **Resumen** agrupa las filas según las columnas  **por** grupo y calcula agregaciones sobre cada grupo.

1. La siguiente instrucción muestra la función **count()**, que devuelve un recuento del grupo. En la ventana de consulta, escribe la siguiente instrucción y selecciona **Ejecutar**:

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d) and EventID_s == 4688  
    | summarize count() by Computer
    ```

1. En la siguiente instrucción se muestra la función **count(),** pero en este ejemplo, se asigna un nombre a la columna como *cnt*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d) and EventID_s == 4624  
    | summarize cnt=count() by AccountType_s, Computer
    ```

1. La siguiente instrucción muestra la función **dcount(),** que devuelve un recuento distinto aproximado de los elementos del grupo. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SigninLogs_CL  
    | where TimeGenerated > ago(7d)
    | summarize dcount(IpAddress)
    ```

1. La siguiente instrucción es una regla para detectar errores que indican *La cuenta del usuario está deshabilitada* en varias aplicaciones para la misma cuenta. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    let timeframe = 30d;
    let threshold = 1;
    SigninLogs_CL
    | where TimeGenerated >= ago(timeframe)
    | where ResultDescription has "User account is disabled"
    | summarize applicationCount = dcount(AppDisplayName_s) by UserPrincipalName_s, IPAddress
    | where applicationCount >= threshold
    ```

1. La siguiente instrucción muestra la función **arg_max()**, que devuelve una o varias expresiones cuando se maximiza el argumento. La siguiente instrucción devuelve la fila más actual de la tabla SecurityEvent_CL para el equipo *VictimPC2*. El asterisco (*) en la función arg_max solicita todas las columnas de la fila. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SecurityEvent_CL  
    | where Computer == "VictimPC2"
    | summarize arg_max(TimeGenerated,*) by Computer
    ```

1. La siguiente instrucción muestra la función **arg_min()**, que devuelve una o varias expresiones cuando se minimiza el argumento. En esta instrucción, se devolverá el elemento SecurityEvent_CL más antiguo para el equipo *VictimPC2* como conjunto de resultados. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SecurityEvent_CL  
    | where Computer == "VictimPC2"
    | summarize arg_min(TimeGenerated,*) by Computer
    ```

1. Las siguientes instrucciones muestran la importancia de comprender los resultados en función del orden de la *canalización*. En la ventana Consulta, escribe las siguientes consultas y ejecuta cada consulta por separado:

    1. **Consulta 1** tiene las cuentas cuya última actividad haya sido un inicio de sesión. Primero se resumirá la tabla SecurityEvent_CL y se devolverá la fila más reciente de cada cuenta. Después, se devolverán únicamente las filas con EventID_s igual a 4624 (inicio de sesión).

        ```KQL
        SecurityEvent_CL  
        | summarize arg_max(TimeGenerated, *) by Account_s 
        | where EventID_s == 4624  
        ```

    1. **Consulta 2** tiene el inicio de sesión más reciente para las cuentas que han iniciado sesión. La tabla SecurityEvent_CL se filtra para incluir solo EventID_s = 4624. Después, estos resultados se resumen para ofrecer la fila de inicio de sesión más reciente por cuenta.

        ```KQL
        SecurityEvent_CL  
        | where EventID_s == 4624  
        | summarize arg_max(TimeGenerated, *) by Account_s
        ```

    >**Nota:** también puedes revisar el vínculo "CPU total" y "Datos usados para la consulta procesada" seleccionando el vínculo "Detalles de la consulta" en la parte inferior derecha y comparando los datos entre ambas instrucciones.

1. La siguiente instrucción muestra la función **make_list()**, que devuelve una *lista* de todos los valores del grupo. Esta consulta KQL filtrará primero el elemento EventID_s con el operador where. A continuación, para cada equipo (Computer), los resultados son una matriz JSON de las cuentas (Account). La matriz JSON resultante incluirá cuentas duplicadas. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | where EventID_s == 4624  
    | summarize make_list(Account_s) by Computer
    ```

1. La siguiente instrucción muestra la función **make_set()**, que devuelve un conjunto de valores *distinct* dentro del grupo. Esta consulta KQL filtrará primero el elemento EventID_s con el operador where. A continuación, para cada equipo (Computer), los resultados son una matriz JSON de las cuentas (Account) únicas. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | where EventID_s == 4624  
    | summarize make_set(Account_s) by Computer
    ```

### Tarea 5: Creación de visualizaciones en KQL con el operador Render

En esta tarea, usarás la función que permite generar visualizaciones con instrucciones KQL.

1. En la siguiente instrucción se muestra el operador **render** (que representa los resultados como una salida gráfica), mediante una visualización de **gráficos de barras**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | summarize count() by Account_s
    | render barchart
    ```

1. En la siguiente instrucción se muestra el operador **render** que permite visualizar los resultados con una serie temporal. La función **bin()** redondea todos los valores en un período de tiempo y los agrupa. Se usa con frecuencia en combinación con **summarize**. Si tiene un conjunto de valores dispersos, estos se agrupan en un conjunto más pequeño de valores específicos. Al combinar los resultados generados y canalizarlos a un operador **render** con el tipo **timechart**, se obtiene una visualización de serie temporal. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent_CL  
    | where TimeGenerated > ago(7d)
    | summarize count() by bin(TimeGenerated, 1m)
    | render timechart
    ```

### Tarea 6: Creación de instrucciones de varias tablas en KQL

En esta tarea, crearás instrucciones KQL de varias tablas.

1. Cambia el **Intervalo de tiempo** por **Últimos 7 días** en la ventana Consulta. Esto limita los resultados de las siguientes instrucciones.

1. La siguiente instrucción muestra el operador **union**, que toma dos o más tablas y devuelve todas sus filas. Es fundamental comprender cómo se pasan los resultados y cómo les afecta la barra vertical. En la ventana Consulta, escribe las siguientes instrucciones y selecciona **Ejecutar** para cada consulta por separado para ver los resultados:

    1. La **consulta 1** devuelve todas las filas de SecurityEvent_CL y de SigninLogs_CL.

        ```KQL
        SecurityEvent_CL  
        | union SigninLogs_CL  
        ```

    1. La **consulta 2** devuelve una fila y una columna, que es el recuento total de todas las filas de SigninLogs_CL y de SecurityEvent_CL.

        ```KQL
        SecurityEvent_CL  
        | union SigninLogs_CL  
        | summarize count() 
        ```

    1. La **consulta 3** devuelve todas las filas de SecurityEvent_CL y una fila de SigninLogs_CL (la última). La última fila de SigninLogs_CL tiene el recuento resumido del número total de filas.

        ```KQL
        SecurityEvent_CL  
        | union (SigninLogs_CL | summarize count() | project count_)
        ```

    >**Nota:** La "fila vacía" en los resultados mostrará el recuento resumido de SigninLogs_CL.

1. En la siguiente instrucción se muestra la compatibilidad del operador **union** para unir varias tablas con caracteres comodín. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    union Sec*  
    | summarize count() by Type
    ```

1. La siguiente instrucción muestra el operador **join**, que combina las filas de dos tablas para formar una nueva tabla haciendo coincidir los valores de las columnas especificadas de cada tabla. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SecurityEvent_CL  
    | where EventID_s == 4624 
    | summarize LogOnCount=count() by  EventID_s, Account_s
    | project LogOnCount, Account_s
    | join kind = inner( 
     SecurityEvent_CL  
    | where EventID_s == 4634 
    | summarize LogOffCount=count() by  EventID_s, Account_s
    | project LogOffCount, Account_s
    ) on Account_s
    ```

    >**Importante:** la primera tabla especificada en la instrucción join se considera la tabla izquierda. La tabla después del operador **join** está situada a la derecha. Al trabajar con las columnas de las tablas, los nombres $left.Column y $right.Column sirven para distinguir a qué tablas hacen referencia las columnas. El operador **join** admite una amplia gama de tipos: fullouter, inner, innerunique, leftanti, leftantisemi, leftouter, leftsemi, rightanti, rightantisemi, rightouter y rightsemi.

1. Puedes dejar el **Intervalo de tiempo** en **Últimos 7 días** en la ventana Consulta.

### Tarea 7: Trabajo con datos de cadena en KQL

En esta tarea, trabajarás con campos de cadena estructurados y no estructurados con instrucciones KQL.

1. La siguiente instrucción muestra la función **extract**, que obtiene una coincidencia para una expresión regular de una cadena de origen. Tiene la opción de convertir la subcadena extraída en el tipo indicado. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    print extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"
    ```

1. En las instrucciones siguientes, se usa la función **extract** para extraer el nombre de Account_s del campo Account_s de la tabla SecurityEvent_CL. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent_CL  
    | where EventID_s == 4672 and AccountType_s == 'User' 
    | extend Account_Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account_s))
    | summarize LoginCount = count() by Account_Name
    | where Account_Name != "" 
    | where LoginCount < 10
    ```

1. La siguiente instrucción muestra el operador **parse**, que evalúa una expresión de cadena y analiza su valor en una o varias columnas calculadas. Úselo para estructurar datos no estructurados. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    let Traces = datatable(EventText:string)
    [
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=23, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=15, lockTime=02/17/2016 08:40:00, releaseTime=02/17/2016 08:40:00, previousLockTime=02/17/2016 08:39:00)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=20, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=22, lockTime=02/17/2016 08:41:01, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 08:41:00, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:00)"
    ];
    Traces   
    | parse EventText with * "resourceName=" resourceName ", totalSlices=" totalSlices:long * "sliceNumber=" sliceNumber:long * "lockTime=" lockTime ", releaseTime=" releaseTime:date "," * "previousLockTime=" previousLockTime:date ")" *  
    | project resourceName, totalSlices, sliceNumber, lockTime, releaseTime, previousLockTime
    ```

1. En las instrucciones siguientes aparecen los operadores para manipular JSON almacenado en campos de cadena. Muchos registros envían datos en formato JSON, por lo que es necesario saber cómo transformar datos JSON en campos que se pueden consultar. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SigninLogs_CL 
    | extend AuthDetails =  parse_json(AuthenticationDetails_s) 
    | extend AuthMethod =  AuthDetails[0].authenticationMethod 
    | extend AuthResult = AuthDetails[0].["authenticationStepResultDetail"] 
    | project AuthMethod, AuthResult, AuthDetails 
    ```

1. En la siguiente instrucción se muestra el operador **mv-expand**, que convierte matrices dinámicas en filas (expansión de varios valores).

    ```KQL
    SigninLogs_CL 
    | mv-expand AuthDetails = parse_json(AuthenticationDetails_s) 
    | project AuthDetails
    ```

1. Expande la primera fila seleccionando ">" y luego de nuevo junto a *AuthDetails* para revisar los resultados expandidos.

1. La siguiente instrucción muestra el operador **mv-apply**, que aplica una subconsulta a cada registro y devuelve la unión de los resultados de todas las subconsultas.

    ```KQL
    SigninLogs_CL 
    | mv-apply AuthDetails = parse_json(AuthenticationDetails_s) on
    (where AuthDetails.authenticationMethod == "Password")
    ```

1. Una **función** es una consulta de registro que se puede usar en otras consultas de registro como si se tratase de un comando. Para crear una **función**, después de ejecutar la consulta, selecciona el botón **Guardar** y luego selecciona **Guardar como función** en la lista desplegable. Escribe el nombre que quieras (por ejemplo: *PrivLogins*) en el cuadro **Nombre de la función** y escribe una **Categoría heredada** (por ejemplo: *General*) y selecciona **Guardar**. La función está disponible en KQL mediante el alias de la función:

    ```KQL
    PrivLogins  
    ```

## Has completado el laboratorio
