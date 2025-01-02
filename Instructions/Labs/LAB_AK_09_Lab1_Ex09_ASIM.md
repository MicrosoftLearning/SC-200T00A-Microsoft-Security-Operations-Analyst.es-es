---
lab:
  title: 'Ejercicio 9: creación de analizadores de ASIMA'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 9: implementación de analizadores de ASIM

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes modelar analizadores de ASIM para un evento de registro de Windows específico. Estos analizadores se finalizarán más adelante siguiendo la [Referencia del esquema de normalización de eventos del registro del Modelo de información de seguridad avanzada (ASIM)](https://docs.microsoft.com/azure/sentinel/registry-event-normalization-schema).

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: Implementación de analizadores de ASIM del esquema de registro

En esta tarea, revisarás los analizadores de esquemas del registro que se incluyen con la implementación de Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

<!--- 1. In the Edge browser, open a new tab (Ctrl+T) and navigate to the Microsoft Sentinel GitHub ASIM page <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM>.

 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel).

    >**Note:** In the **ASIM** folder you can deploy templates that contain all ASIM parsers, but we will only focus on the Registry Schema.

1. Scroll down and next to **Registry Event**, select the **Deploy to Azure** button.

1. For *Resource Group*, select **RG-Defender** where your Sentinel workspace resides.

1. For *Workspace*, type your Sentinel workspace name, like *uniquenameDefender*.

1. Leave the other default values and select **Review + create**.

1. Select **Create** to deploy the template. Notice the Names of the different resources. 

1. After the deployment completes return to the *Microsoft Sentinel* tab. --->

1. En el menú izquierdo, en **General**, selecciona *Registros*.

1. Abre la hoja *Esquema y filtro*; para ello, selecciona **>>** si es necesario.

1. Selecciona la pestaña **Funciones** (junto a las pestañas Tablas y consultas). **Sugerencia:** es posible que tengas que seleccionar el icono **(...)** para seleccionar la pestaña.

1. En la barra de *Búsqueda*, escribe **registro** y desplázate hacia abajo por las funciones del analizador de ASIM hasta que veas el siguiente *_Im_RegistryEvent_MicrosoftWindowsEventxxx* para Microsoft Windows en el encabezado *Microsoft Sentinel*.

    >**Nota:** usamos las letras xxx en el nombre de la función del analizador de ASIM para tener en cuenta los cambios de versión. En el momento en que se actualizó este laboratorio, la función era *_Im_RegistryEvent_MicrosoftWindowsEventV02*.

1. Mantén el puntero sobre la función de ASIM **_Im_RegistryEvent_MicrosoftWindowsEventxxx** y, después, selecciona **Cargar el código de función** en la ventana emergente.

1. Revisa el KQL que analiza el identificador de evento 4657 para simplificar el análisis de los datos en el área de trabajo de Microsoft Sentinel.

    >**Sugerencia:** al escribir Ctrl+F en la ventana de código, se abre *Buscar* y se realiza la búsqueda de *EventID: 4657* de forma mucho más sencilla.

1. En *Registros*, abre una pestaña de nueva consulta.

1. Vuelve a la hoja *Esquema y filtro* y mantén el puntero sobre el *analizador de filtrado de eventos del Registro ASIM para eventos de Microsoft Windows y eventos de seguridad* **_Im_RegistryEvent_MicrosoftWindowsEventxxx** y, después, selecciona **Usar en el editor**.

1. **Ejecutar** la consulta de función ASIM. Si has completado los ejercicios de laboratorio anteriores, deberías ver los resultados y los mensajes noerror.

## Continúa con el ejercicio 10
