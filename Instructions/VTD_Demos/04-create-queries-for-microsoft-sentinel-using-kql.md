# Módulo 4: creación de consultas para Microsoft Sentinel mediante el Lenguaje de consulta de Kusto (KQL)

<!--- **Note** Successful completion of this demo depends on completing all of the steps in the  [Pre-requisites document](00-prerequisites.md). --->

>**Importante:** Se recomienda realizar las consultas para este laboratorio en el entorno de demostración Zava (anteriormente Alpine Ski House). La alternativa es usar el entorno de laboratorio SC-200 con el Laboratorio 06: [Creación de consultas para Microsoft Sentinel mediante Lenguaje de consulta Kusto (KQL)](https://microsoftlearning.github.io/SC-200T00A-Microsoft-Security-Operations-Analyst/Instructions/Labs/LAB_AK_06_Lab1_Ex01_KQL.html/). Para este último se necesitan 30 minutos de tiempo de implementación.

## Acceso al área de pruebas de KQL

En esta tarea, accederá a un entorno de Log Analytics de Microsoft Sentinel donde podrá practicar la escritura de instrucciones KQL.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador, vaya a <https://security.microsoft.com>. Inicie sesión con las credenciales de usuario de Zava o Alpine Ski House.

1. Expanda la **sección Investigación y respuesta** en el panel de navegación de la izquierda.

1. Expanda la **sección Búsqueda** y seleccione **búsqueda avanzada de amenazas**.

1. Explore las tablas disponibles que aparecen en la pestaña *Esquema* del lado izquierdo de la pantalla. Observe las tablas de *Microsoft Sentinel* y de*Security and Audit*.

1. En el editor de consultas, escribe la siguiente consulta y luego selecciona Ejecutar.  Deberías ver los resultados de la consulta en la ventana inferior.

    ```KQL
    SecurityEvent
    ```

1. Junto al primer registro, selecciona **>** para expandir la información de la fila.

### Tarea 2: ejecutar las instrucciones KQL básicas

En esta tarea, crearás instrucciones KQL básicas.

1. El operador `search` da una experiencia de búsqueda de varias tablas o varias columnas. En el siguiente ejemplo se muestra el uso del operador `search`.

    > **Nota:** El operador `search` consume muchos recursos. Limite el valor *Intervalo de tiempo* a *Últimas 3 horas* y use *límite | 100*.

```KQL
search "err" 

search in (SecurityEvent,SecurityAlert,A*) "err"
```

1. El operador `where` filtra una tabla para el subconjunto de filas que cumplen un predicado. En el siguiente ejemplo se muestra el uso del operador `where`.

```KQL
SecurityEvent | where EventID in (4624, 4625)

SecurityEvent 
| where TimeGenerated > ago(1d) 

SecurityEvent 
| where TimeGenerated > ago(1h) and EventID == "4624" 

SecurityEvent 
| where TimeGenerated > ago(1h) 
| where EventID == 4624 
| where AccountType =~ "user" 
```

1. La siguiente instrucción muestra el uso de la instrucción `let` para declarar variables. En la ventana de consulta, escribe la siguiente instrucción y luego selecciona **Ejecutar**: 

```KQL
let timeOffset = 7d;
let discardEventId = 4688;
SecurityEvent
| where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset)
| where EventID != discardEventId
```

1. La siguiente instrucción muestra el uso de la instrucción `let` para declarar una lista dinámica. En la ventana de consulta, escribe la siguiente instrucción y selecciona **Ejecutar**: 

```KQL
let suspiciousAccounts = datatable(account: string) [
    @"\administrator", 
    @"NT AUTHORITY\SYSTEM"
];
SecurityEvent | where Account in (suspiciousAccounts)
```

1. En la siguiente instrucción se muestra la búsqueda en todas las tablas y columnas de los registros dentro del intervalo de tiempo de consulta en la ventana correspondiente. En la ventana de consulta antes de ejecutar este script, cambia el intervalo de tiempo por "Última hora". Escribe la siguiente instrucción y selecciona **Ejecutar**:

```KQL
search "err"
```

**Advertencia:** asegúrate de cambiar el intervalo de tiempo por "Últimas 24 horas" para los siguientes scripts.

### Creación de visualizaciones en KQL con el operador Render

En esta tarea, usarás la función que permite generar visualizaciones con instrucciones KQL.

1. En la siguiente instrucción se muestra la función render que visualiza los resultados con un gráfico de barras. En la ventana de consulta. Escribe la siguiente instrucción y selecciona **Ejecutar**: 

```KQL
SecurityEvent 
| summarize count() by Account
| render barchart
```

1. En la siguiente instrucción se muestra la función de representación para ver los resultados con una serie temporal.

La función bin() redondea valores a la baja a un número entero múltiplo del tamaño binario dado.  Se usa a menudo en combinación con summarize by... Si tiene un conjunto de valores dispersos, estos se agrupan en un conjunto más pequeño de valores específicos.  Al combinar la serie temporal generada y canalizarla a un operador render con un tipo timechart, se obtiene una visualización de serie temporal. En la ventana de consulta. Escribe la siguiente instrucción y selecciona **Ejecutar**: 

```KQL
SecurityEvent 
| summarize count() by bin(TimeGenerated, 1d) 
| render timechart
```

## Has completado la demostración
