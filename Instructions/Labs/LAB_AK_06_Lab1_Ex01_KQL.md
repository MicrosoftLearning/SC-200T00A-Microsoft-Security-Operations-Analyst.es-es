---
lab:
  title: "Ejercicio 1: creación de consultas para Microsoft\_Sentinel mediante el Lenguaje de consulta de Kusto (KQL)"
  module: Learning Path 6 - Create queries for Microsoft Sentinel using Kusto Query Language (KQL)
---

# Ruta de aprendizaje 6 - Laboratorio 1 - Ejercicio 1: creación de consultas para Microsoft Sentinel mediante el Lenguaje de consulta Kusto (KQL)

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod4_L1_Ex1.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que va a implementar Microsoft Sentinel. Usted es responsable de analizar los datos de los registros para buscar actividad malintencionada, mostrar visualizaciones y buscar amenazas. Para consultar los datos de los registros, utiliza el lenguaje de consulta Kusto (KQL).

>**Importante:** el área de trabajo de Log Analytics de la [demostración de LA](https://aka.ms/lademo) que se usa para este laboratorio está experimentando una transición. Si no puedes acceder al entorno o si recibes un mensaje de error, puedes intentar ejecutar las consultas en tu propia suscripción a Azure con Microsoft Sentinel implementado. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?azure-portal=true) antes de empezar.

>**Nota:** si decides usar el área de trabajo de Log Analytics de la [demostración de LA](https://aka.ms/lademo) para este laboratorio, es necesario establecer un intervalo de tiempo personalizado en la ventana Consulta. Se recomienda establecer el intervalo de tiempo personalizado al 1 de abril de 2025.

<!--- 
>**Note:** Per Microsoft's *Secure Future Initiative* (SFI), any information that could be considered *Personally Identifiable Information* (PII), such as locations, usernames, IP addresses, resource IDs etc.. have been removed from the LA Demo tables such as *SigninLogs*. This may produce *No results were found* messages for some queries. --->

>**Importante:** este laboratorio implica escribir muchos scripts KQL en Microsoft Sentinel. Los scripts se han facilitado en un archivo al principio de este laboratorio. Una ubicación alternativa para descargarlos es: <https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Allfiles>

### Tiempo estimado para completar este laboratorio: 60 minutos

### Tarea 1: acceder al área de pruebas de KQL

En esta tarea, accederás a un entorno de Log Analytics donde podrás practicar la escritura de instrucciones KQL.

  >**Nota:** si recibes el mensaje que indica que *No se encontraron resultados* durante el período de tiempo predeterminado, cambia el *Intervalo de tiempo* a *Últimos 7 días*.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a <https://aka.ms/lademo> e inicia sesión con las credenciales de administrador.

1. Cierra la ventana emergente del vídeo de Log Analytics que aparece.

1. Explora las tablas disponibles y otras herramientas que aparecen en el *panel de esquemas y filtros* en el lado izquierdo de la pantalla.

1. En el editor de consultas, escribe la siguiente consulta y luego selecciona **Ejecutar**. Deberías ver los resultados de la consulta en la ventana inferior.

    ```KQL
    SecurityEvent
    ```

1. Observa que has alcanzado la cantidad máxima de resultados (30 000).

1. Cambia el valor de *Intervalo de tiempo* a **Últimos 7 días** en la ventana Consulta.

1. Junto al primer registro, selecciona **>** para expandir la información de la fila.

### Tarea 2: ejecutar las instrucciones KQL básicas

En esta tarea, crearás instrucciones KQL básicas.

>**Importante:** para cada consulta, borra la instrucción anterior de la ventana Consulta o abra una nueva ventana de consulta seleccionando **+** después de la última pestaña abierta (hasta 25).

1. En la siguiente instrucción se muestra el operador **search**, que busca en todas las columnas de la tabla el valor.

1. Cambia el *Intervalo de tiempo* por **Últimos 30 minutos** en la ventana de consulta.

1. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    search "location"
    ```

    >**Nota:** El uso del operador *Search* sin tablas específicas o cláusulas aptas es menos eficaz que el filtrado de texto específico de la tabla y específico de columna.

1. En la siguiente instrucción se muestra **search** en tablas enumeradas en la cláusula **in**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    search in (SecurityEvent,App*) "new"
    ```

1. Cambia el *Intervalo de tiempo* por **Últimas 24 horas** en la ventana de consulta.

1. Las instrucciones siguientes muestran el operador **where**, que filtra un predicado específico. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    >**Importante:** debes seleccionar **Ejecutar** después de escribir cada consulta en los bloques de código siguientes.

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    ```

    >**Nota:** el *Intervalo de tiempo* ahora muestra *Establecer en la consulta*, ya que estamos filtrando con la columna TimeGenerated.

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) and EventID == 4624
    ```

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | where EventID == 4624  
    | where AccountType =~ "user"
    ```

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) and EventID in (4624, 4625)
 
    ```

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar *variables*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    let timeOffset = 1h;
    let discardEventId = 4688;
    SecurityEvent
    | where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
    | where EventID != discardEventId
    ```

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar una *lista dinámica*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    let suspiciousAccounts = datatable(account: string) [
      @"NA\timadmin", 
      @"NT AUTHORITY\SYSTEM"
    ];
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | where Account in (suspiciousAccounts)
    ```

    >**Sugerencia:** puedes volver a dar formato a la consulta fácilmente seleccionando los puntos suspensivos (...) en la ventana Consulta y seleccionando **Dar formato a consulta**.

1. La siguiente instrucción muestra el uso de la instrucción **let** para declarar una *tabla dinámica*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    let LowActivityAccounts =
        SecurityEvent 
        | summarize cnt = count() by Account 
        | where cnt < 1000;
    LowActivityAccounts | where Account contains "sql"
    ```

1. Cambia el **Intervalo de tiempo** por **Última hora** en la ventana de consulta. Esto limita los resultados de las siguientes instrucciones.

1. La siguiente instrucción muestra el operador **extend**, que crea una columna calculada y la agrega al conjunto de resultados. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) 
    | where ProcessName != "" and Process != "" 
    | extend StartDir =  substring(ProcessName,0, string_size(ProcessName)-string_size(Process))
    ```

1. La siguiente instrucción muestra el operador **order by**, que ordena las filas de la tabla de entrada por una o varias columnas en orden ascendente o descendente. El operador **order by** es un alias para el operador **sort by**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) 
    | where ProcessName != "" and Process != "" 
    | extend StartDir =  substring(ProcessName,0, string_size(ProcessName)-string_size(Process)) 
    | order by StartDir desc, Process asc
    ```

1. Las instrucciones siguientes muestran el operador **project**, que selecciona las columnas que se van a incluir en el orden especificado. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) 
    | where ProcessName != "" and Process != "" 
    | extend StartDir =  substring(ProcessName,0, string_size(ProcessName)-string_size(Process)) 
    | order by StartDir desc, Process asc 
    | project Process, StartDir
    ```

1. Las siguientes instrucciones muestran el operador **project-away**, que selecciona las columnas que se van a excluir de la salida. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) 
    | where ProcessName != "" and Process != "" 
    | extend StartDir =  substring(ProcessName,0, string_size(ProcessName)-string_size(Process)) 
    | order by StartDir desc, Process asc 
    | project-away ProcessName
    ```

### Tarea 3: analizar resultados en KQL con el operador Summarize

En esta tarea, crearás instrucciones KQL para agregar datos. **Resumen** agrupa las filas según las columnas  **por** grupo y calcula agregaciones sobre cada grupo.

1. La siguiente instrucción muestra la función **count()**, que devuelve un recuento del grupo. En la ventana de consulta, escribe la siguiente instrucción y selecciona **Ejecutar**: 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) and EventID == 4688  
    | summarize count() by Process, Computer
    ```

1. En la siguiente instrucción se muestra la función **count(),** pero en este ejemplo, se asigna un nombre a la columna como *cnt*. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d) and EventID == 4624  
    | summarize cnt=count() by AccountType, Computer
    ```

1. La siguiente instrucción muestra la función **dcount(),** que devuelve un recuento distinto aproximado de los elementos del grupo. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | summarize dcount(IpAddress)
    ```

1. La siguiente instrucción es una regla para detectar errores de contraseña no válida en varias aplicaciones para la misma cuenta. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    let timeframe = 30d;
    let threshold = 1;
    SigninLogs
    | where TimeGenerated >= ago(timeframe)
    | where ResultDescription has "Invalid password"
    | summarize applicationCount = dcount(AppDisplayName) by UserPrincipalName, IPAddress
    | where applicationCount >= threshold
    ```

1. La siguiente instrucción muestra la función **arg_max()**, que devuelve una o varias expresiones cuando se maximiza el argumento. La siguiente instrucción devuelve la fila más actual de la tabla SecurityEvent para el equipo SQL10.NA.contosohotels.com. El asterisco (*) en la función arg_max solicita todas las columnas de la fila. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where Computer == "SQL10.na.contosohotels.com"
    | summarize arg_max(TimeGenerated,*) by Computer
    ```

1. La siguiente instrucción muestra la función **arg_min()**, que devuelve una o varias expresiones cuando se minimiza el argumento. En esta instrucción, se devolverá el elemento SecurityEvent más antiguo para el equipo SQL12.NA.contosohotels.com como conjunto de resultados. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where Computer == "SQL10.na.contosohotels.com"
    | summarize arg_min(TimeGenerated,*) by Computer
    ```

1. Las siguientes instrucciones muestran la importancia de comprender los resultados en función del orden de la *canalización*. En la ventana Consulta, escribe las siguientes consultas y ejecuta cada consulta por separado: 

    1. **Consulta 1** tiene las cuentas cuya última actividad haya sido un inicio de sesión. La tabla SecurityEvent se resumirá primero y devolverá la fila más reciente de cada cuenta. Después, se devolverán únicamente las filas con EventID igual a 4624 (inicio de sesión).

        ```KQL
        SecurityEvent  
        | summarize arg_max(TimeGenerated, *) by Account 
        | where EventID == 4624  
        ```

    1. **Consulta 2** tiene el inicio de sesión más reciente para las cuentas que han iniciado sesión. La tabla SecurityEvent se filtra para incluir solo EventID = 4624. Después, estos resultados se resumen para ofrecer la fila de inicio de sesión más reciente por cuenta.

        ```KQL
        SecurityEvent  
        | where EventID == 4624  
        | summarize arg_max(TimeGenerated, *) by Account
        ```

    >**Nota:** también puedes revisar el vínculo "CPU total" y "Datos usados para la consulta procesada" seleccionando el vínculo "Detalles de la consulta" en la parte inferior derecha y comparando los datos entre ambas instrucciones.

1. La siguiente instrucción muestra la función **make_list()**, que devuelve una *lista* de todos los valores del grupo. Esta consulta KQL filtrará primero el elemento EventID con el operador where. A continuación, para cada equipo (Computer), los resultados son una matriz JSON de las cuentas (Account). La matriz JSON resultante incluirá cuentas duplicadas. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | where EventID == 4624  
    | summarize make_list(Account) by Computer
    ```

1. La siguiente instrucción muestra la función **make_set()**, que devuelve un conjunto de valores *distinct* dentro del grupo. Esta consulta KQL filtrará primero el elemento EventID con el operador where. A continuación, para cada equipo (Computer), los resultados son una matriz JSON de las cuentas (Account) únicas. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | where EventID == 4624  
    | summarize make_set(Account) by Computer
    ```


### Tarea 4: crear visualizaciones en KQL con el operador Render

En esta tarea, usarás la función que permite generar visualizaciones con instrucciones KQL.

1. En la siguiente instrucción se muestra el operador **render** (que representa los resultados como una salida gráfica), mediante una visualización de **gráficos de barras**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | summarize count() by Account
    | render barchart
    ```

1. En la siguiente instrucción se muestra el operador **render** que permite visualizar los resultados con una serie temporal. La función **bin()** redondea todos los valores en un período de tiempo y los agrupa. Se usa con frecuencia en combinación con **summarize**. Si tiene un conjunto de valores dispersos, estos se agrupan en un conjunto más pequeño de valores específicos. Al combinar los resultados generados y canalizarlos a un operador **render** con el tipo **timechart**, se obtiene una visualización de serie temporal. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where TimeGenerated > ago(7d)
    | summarize count() by bin(TimeGenerated, 1m)
    | render timechart
    ```


### Tarea 5: crear instrucciones de varias tablas en KQL

En esta tarea, crearás instrucciones KQL de varias tablas.

>**Importante:** se han quitado las entradas de la tabla *SigninLogs*, por lo que algunas de las siguientes consultas *no generan actualmente resultados* en el entorno de demostración de LA usado para este laboratorio. Sin embargo, las consultas KQL muestran conceptos y casos de uso importantes, así que tómate tu tiempo para revisarlas.

1. Cambia el **Intervalo de tiempo** por **Últimos 7 días** en la ventana Consulta. Esto limita los resultados de las siguientes instrucciones.

1. La siguiente instrucción muestra el operador **union**, que toma dos o más tablas y devuelve todas sus filas. Es fundamental comprender cómo se pasan los resultados y cómo les afecta la barra vertical. En la ventana Consulta, escribe las siguientes instrucciones y selecciona **Ejecutar** para cada consulta por separado para ver los resultados:

    1. **Consulta 1** devuelve todas las filas de SecurityEvent y todas las filas de SigninLogs.

        ```KQL
        SecurityEvent  
        | union SigninLogs  
        ```

    1. **Consulta 2** devuelve una fila y una columna, que es el recuento total de todas las filas de SigninLogs y todas las filas de SecurityEvent.

        ```KQL
        SecurityEvent  
        | union SigninLogs  
        | summarize count() 
        ```

    1. **Consulta 3** devuelve todas las filas de SecurityEvent y una (última) fila de SigninLogs. La última fila de SigninLogs tiene el recuento resumido del número total de filas.

        ```KQL
        SecurityEvent  
        | union (SigninLogs | summarize count() | project count_)
        ```

    >**Nota:** la "fila vacía" en los resultados mostrará el recuento resumido de SigninLogs.

1. En la siguiente instrucción se muestra la compatibilidad del operador **union** para unir varias tablas con caracteres comodín. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    union App*  
    | summarize count() by Type
    ```

1. La siguiente instrucción muestra el operador **join**, que combina las filas de dos tablas para formar una nueva tabla haciendo coincidir los valores de las columnas especificadas de cada tabla. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SecurityEvent  
    | where EventID == 4624 
    | summarize LogOnCount=count() by  EventID, Account
    | project LogOnCount, Account
    | join kind = inner( 
     SecurityEvent  
    | where EventID == 4634 
    | summarize LogOffCount=count() by  EventID, Account
    | project LogOffCount, Account
    ) on Account
    ```

    >**Importante:** la primera tabla especificada en la instrucción join se considera la tabla izquierda. La tabla después del operador **join** está situada a la derecha. Al trabajar con las columnas de las tablas, los nombres $left.Column y $right.Column sirven para distinguir a qué tablas hacen referencia las columnas. El operador **join** admite una amplia gama de tipos: fullouter, inner, innerunique, leftanti, leftantisemi, leftouter, leftsemi, rightanti, rightantisemi, rightouter y rightsemi.

1. Puedes dejar el **Intervalo de tiempo** en **Últimos 7 días** en la ventana Consulta.

### Tarea 6: trabajar con datos de cadena en KQL

En esta tarea, trabajarás con campos de cadena estructurados y no estructurados con instrucciones KQL.

1. La siguiente instrucción muestra la función **extract**, que obtiene una coincidencia para una expresión regular de una cadena de origen. Tiene la opción de convertir la subcadena extraída en el tipo indicado. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    print extract("x=([0-9.]+)", 1, "hello x=45.6|wo") == "45.6"
    ```

1. En el ejemplo siguiente, se usa la función **extract** para extraer el nombre de cuenta del campo de cuenta de la tabla SecurityEvent. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SecurityEvent  
    | where EventID == 4672 and AccountType == 'User' 
    | extend Account_Name = extract(@"^(.*\\)?([^@]*)(@.*)?$", 2, tolower(Account))
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

    >**Importante:** las siguientes consultas *no generan actualmente resultados* en el entorno de demostración de LA usado para este laboratorio. Se han eliminado las entradas de la tabla *SigninLogs*. Sin embargo, las consultas KQL muestran conceptos y casos de uso importantes, así que tómate tu tiempo para revisarlas.

1. En la siguiente instrucción se muestra cómo trabajar con campos **dinámicos**, que son especiales, ya que pueden asumir cualquier valor de otros tipos de datos. En este ejemplo, el campo DeviceDetail de la tabla SigninLogs es de tipo **dinámico**. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**. 

    ```KQL
    SigninLogs 
    | extend OS = DeviceDetail.operatingSystem
    ```

1. En el ejemplo siguiente se muestra cómo dividir campos empaquetados para SigninLogs. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SigninLogs 
    | extend OS = DeviceDetail.operatingSystem, Browser = DeviceDetail.browser 
    | extend StatusCode = tostring(Status.errorCode), StatusDetails = tostring(Status.additionalDetails) 
    | extend Date = startofday(TimeGenerated) 
    | summarize count() by Date, Identity, UserDisplayName, UserPrincipalName, IPAddress, ResultType, ResultDescription, StatusCode, StatusDetails 
    | sort by Date
    ```

    >**Importante:** aunque el tipo dinámico tiene un aspecto similar al formato JSON, puede contener valores que el modelo JSON no representa porque no existen en JSON. Por lo tanto, al serializar valores en una representación JSON, los valores que JSON no puede representar se serializan como valores de cadena. 

1. En las instrucciones siguientes aparecen los operadores para manipular JSON almacenado en campos de cadena. Muchos registros envían datos en formato JSON, por lo que es necesario saber cómo transformar datos JSON en campos que se pueden consultar. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**.

    ```KQL
    SigninLogs 
    | extend AuthDetails =  parse_json(AuthenticationDetails) 
    | extend AuthMethod =  AuthDetails[0].authenticationMethod 
    | extend AuthResult = AuthDetails[0].["authenticationStepResultDetail"] 
    | project AuthMethod, AuthResult, AuthDetails 
    ```

1. En la siguiente instrucción se muestra el operador **mv-expand**, que convierte matrices dinámicas en filas (expansión de varios valores).

    ```KQL
    SigninLogs 
    | mv-expand AuthDetails = parse_json(AuthenticationDetails) 
    | project AuthDetails
    ```

1. Expande la primera fila seleccionando ">" y luego de nuevo junto a *AuthDetails* para revisar los resultados expandidos.

1. La siguiente instrucción muestra el operador **mv-apply**, que aplica una subconsulta a cada registro y devuelve la unión de los resultados de todas las subconsultas.

    ```KQL
    SigninLogs 
    | mv-apply AuthDetails = parse_json(AuthenticationDetails) on
    (where AuthDetails.authenticationMethod == "Password")
    ```

1. Una **función** es una consulta de registro que se puede usar en otras consultas de registro como si se tratase de un comando. Para crear una **función**, después de ejecutar la consulta, selecciona el botón **Guardar** y luego selecciona **Guardar como función** en la lista desplegable. Escribe el nombre que quieras (por ejemplo: *PrivLogins*) en el cuadro **Nombre de la función** y escribe una **Categoría heredada** (por ejemplo: *General*) y selecciona **Guardar**. La función está disponible en KQL mediante el alias de la función:

    >**Nota:** no podrás hacerlo en el entorno lademo usado para este laboratorio, ya que tu cuenta solo tiene permisos de lector, pero es un concepto importante para hacer que las consultas sean más eficaces y efectivas. 

    ```KQL
    PrivLogins  
    ```

## Has completado el laboratorio
