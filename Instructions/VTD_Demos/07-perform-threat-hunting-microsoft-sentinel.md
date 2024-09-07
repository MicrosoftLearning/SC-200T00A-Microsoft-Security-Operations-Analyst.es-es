# Módulo 7: Búsqueda de amenazas en Microsoft Sentinel

**Nota**: la finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md).

**Importante:** esta demostración no es necesaria para VTD-5002-FY25.

## Crear una consulta de búsqueda

En esta tarea, crearás una consulta de búsqueda, marcarás un resultado y crearás una secuencia en vivo.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona **Registros** 

1. Escribe la siguiente instrucción KQL en el espacio Nueva consulta 1:

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize count() by bin(TimeGenerated, 3m), c2
| where count_ > 5
| render timechart 
```

1. El objetivo de esta instrucción es proporcionar una visualización para comprobar si hay un señal C2 en una base coherente.  Tómese el tiempo para ajustar la configuración de 3 m a 30 s y más.  Cambie la configuración de count_ > 5 por otros recuentos de umbrales para presenciar el impacto.

1. Ahora ha identificado las solicitudes DNS que están señalizando a un servidor C2.  A continuación, determine qué dispositivos están señalizando.  Escriba la siguiente instrucción KQL:

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),".")) 
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

**Nota** Los datos de registro generados proceden únicamente del dispositivo incorporado.

1. Cierra la ventana *Registros* seleccionando la **X** en la parte superior derecha de la ventana y selecciona **Aceptar** para descartar los cambios. 

1. Seleccione la página **Búsqueda** en el área Administración de amenazas del portal de Microsoft Sentinel.

1. Seleccione **Nueva consulta** en la barra de comandos.

1. En la ventana *Crear consulta personalizada*, para el tipo *Nombre*, escriba **C2 Hunt**

1. Para la *Consulta personalizada*, escribe la siguiente instrucción KQL:

```KQL
let lookback = 2d;
DeviceEvents | where TimeGenerated >= ago(lookback) 
| where ActionType == "DnsQueryResponse"
| extend c2 = substring(tostring(AdditionalFields.DnsQueryString),0,indexof(tostring(AdditionalFields.DnsQueryString),"."))
| where c2 startswith "sub"
| summarize cnt=count() by bin(TimeGenerated, 5m), c2, DeviceName
| where cnt > 15
```

1. Desplácese hacia abajo y, en *Asignación de entidades (versión preliminar)* seleccione:

    - En la lista desplegable *Tipo de entidad*, selecciona **Host**.
    - En la lista desplegable *Identificador*, selecciona **HostName**.
    - En la lista desplegable *Valor*, seleccione **DeviceName**.

1. Desplázate hacia abajo y en *Tácticas y técnicas*, selecciona **Comando y control** y luego selecciona **Crear** para crear la consulta de búsqueda.

1. En la hoja *"Microsoft Sentinel: Búsqueda",* busque la consulta que acaba de crear en la lista, *C2 Hunt*.

1. Seleccione **C2 Hunt** en la lista.

1. En el panel derecho, desplácese hacia abajo y seleccione el botón **Ejecutar consulta**.

1. El número de resultados se muestra en el panel central de la columna *Resultados*. Como alternativa, desplácese hacia arriba para ver el recuento sobre el cuadro *Resultados*.

1. Seleccione **Ver resultados**.

1. Seleccione la primera fila en los resultados. 

1. Seleccione **Agregar marcador**.

1. Seleccione **Crear** en el panel que aparece.

1. Vuelva a la página Búsqueda en el portal de Microsoft Sentinel.

1. Seleccione la pestaña **Marcadores**.

1. Seleccione el marcador en la lista de resultados.

1. Seleccione **Investigar** en el panel flotante.

1. Explore el grafo Investigación.

1. Vuelva a la página Búsqueda en el portal de Microsoft Sentinel.

1. Seleccione la pestaña **Consultas**

1. Seleccione la consulta **C2 Hunt**.

1. Seleccione el **...** al final de la fila para abrir el menú contextual.

1. Seleccione **Agregar a livestream**.

## Ha completado la demostración.