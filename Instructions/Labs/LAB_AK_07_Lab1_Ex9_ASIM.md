---
lab:
  title: 'Ejercicio 9: creación de analizadores de ASIMA'
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 7 - Laboratorio 1 - Ejercicio 9: implementación de analizadores de ASIM

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex9.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes modelar analizadores de ASIM para un evento de registro de Windows específico. Estos analizadores simplificados se finalizarán más adelante después de la [Referencia del esquema de normalización de eventos de proceso del Modelo de información de seguridad avanzada (ASIM)](https://docs.microsoft.com/en-us/azure/sentinel/registry-event-normalization-schema).

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20Advanced%20Security%20Information%20Model%20Parsers)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 

### Tarea 1: Implementación de analizadores de ASIM del esquema de registro

En esta tarea, implementarás los analizadores de esquemas del registro del repositorio de GitHub de Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. En el explorador Edge, abra una nueva pestaña (Ctrl+T) y vaya a la página ASIM <https://github.com/Azure/Azure-Sentinel/tree/master/ASIM> de GitHub de Microsoft Sentinel.

    <!--- 1. On the right pane, select the **Onboard community content** link. This will open a new tab in the Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

    >**Nota:** En la carpeta **ASIM** puede implementar plantillas que contengan todos los analizadores de ASIM, pero solo nos centraremos en el esquema de registro.

1. Desplázate hacia abajo y junto a **Registro**, selecciona el botón **Implementación en Azure**.

1. En *Grupo de recursos*, selecciona **RG-Defender** donde reside el área de trabajo de Sentinel.

1. En *Área de trabajo*, escribe el nombre del área de trabajo de Sentinel, como *uniquenameDefender*.

1. Deja el resto de valores predeterminados y selecciona **Revisar y crear**.

1. Seleccione **Crear** para implementar la plantilla. Observa los nombres de los distintos recursos.

1. Una vez completada la implementación, vuelva a la pestaña *Microsoft Sentinel*.

1. En el menú izquierdo, en **General**, selecciona *Registros*.

1. Abre la hoja *Esquema y filtro*; para ello, selecciona **>>** si es necesario.

1. Selecciona la pestaña **Funciones** (junto a las pestañas Tablas y consultas). **Sugerencia:** es posible que tengas que seleccionar el icono **(...)** para seleccionar la pestaña.

1. Expanda **Funciones del área de trabajo**. Observa que los nombres correspondan a las plantillas que acabas de implementar.

1. Mantenga el puntero sobre el *analizador del área de trabajo* **vimRegistryEventMicrosoftSecurityEvents** y, a continuación, seleccione **Cargar el código de función** en la ventana emergente.

1. Revisa el KQL que analiza el identificador de evento 4657 para simplificar el análisis de los datos en el área de trabajo de Microsoft Sentinel.

1. **Ejecute** la consulta. No debe obtener ningún resultado ni errores, es solo para fines de validación.

1. Vuelve a la hoja *Esquema y filtro* y pasa el ratón por encima del *analizador unificador* **inRegistry** y luego selecciona **Cargar el código de la función**.

1. Observa que los analizadores unificadores usan el operador *union* para ejecutar todos los analizadores del área de trabajo a la vez. Si desarrollas un analizador para el esquema del registro, deberás agregarlo aquí.

1. **Ejecute** la consulta. No debes obtener ningún resultado ni errores, es solo para fines de validación.

1. Este analizador unificador ahora se puede usar para reglas analíticas o consultas de búsqueda.

## Continúa con el ejercicio 10