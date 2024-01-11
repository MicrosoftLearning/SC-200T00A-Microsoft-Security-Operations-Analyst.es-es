# Módulo 4: creación de consultas para Microsoft Sentinel mediante el Lenguaje de consulta de Kusto (KQL)

**Nota**: la finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md). 

## Acceso al área de pruebas de KQL

En esta tarea, accederás a un entorno de Log Analytics donde podrás practicar la escritura de instrucciones KQL.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador, vaya a https://aka.ms/lademo. Inicia sesión con credenciales de administrador MOD. 

1. Explora las tablas disponibles que aparecen en la pestaña del lado izquierdo de la pantalla.

1. En el editor de consultas, escribe la siguiente consulta y luego selecciona Ejecutar.  Deberías ver los resultados de la consulta en la ventana inferior.

    ```KQL
    SecurityEvent
    ```

1. Junto al primer registro, selecciona **>** para expandir la información de la fila.

### Tarea 2: ejecutar las instrucciones KQL básicas

En esta tarea, crearás instrucciones KQL básicas.

1. El operador `search` da una experiencia de búsqueda de varias tablas o varias columnas. En el siguiente ejemplo se muestra el uso del operador `search`.

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
