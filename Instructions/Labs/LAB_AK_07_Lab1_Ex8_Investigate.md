---
lab:
  title: 'Ejercicio 8: investigación de incidentes'
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 7 - Laboratorio 1 - Ejercicio 8: investigación de incidentes

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex8.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Ya has creado reglas programadas y de análisis de seguridad de Microsoft. Las reglas de Fusion y de análisis de anomalías también están habilitadas en tu entorno. Ahora es el momento de investigar los incidentes que han creado.

Un incidente puede incluir varias alertas, Es una agregacion de todas las pruebas relevantes en una investigación en concreto. Las propiedades relacionadas con alertas, como la gravedad y el estado, se establecen en el nivel de incidente. Después de indicar a Microsoft Sentinel qué tipos de amenazas estás buscando y cómo detectarlas, puedes supervisar las amenazas que se detecten investigando cada incidente.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Investigate%20incidents)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: investigar un incidente

En esta tarea, investigarás un incidente.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. Selecciona la página **Incidentes**.

1. Revisa la lista de incidentes.

    >**Nota:** las reglas de análisis generan alertas e incidentes en la misma entrada de registro específica. Recuerda que esto se realizó en la *programación de consultas* para generar más alertas e incidentes que se usarán en el laboratorio.
  
1. Selecciona uno de los incidentes de **RegKey de inicio**.

1. Revisa los detalles del incidente en la hoja derecha que se ha abierto. Desplázate hacia abajo y selecciona el botón **Ver detalles completos**.

1. Si aparece la ventana emergente "Nueva experiencia de incidente", sigue las indicaciones leyendo la información seleccionando el botón **Siguiente**.

1. En la hoja izquierda del incidente, cambia el estado por **Activo** y luego selecciona **Aplicar**.

1. Desplázate hacia abajo hasta el área *Etiquetas*, selecciona **+** y escribe **RegKey** y selecciona **Aceptar**.

1. Desplázate hacia abajo y en el cuadro *Escribir un comentario...* escribe: *investigaré esto* y selecciona el icono **>** para enviar el nuevo comentario.

1. Oculte la hoja izquierda seleccionando el icono **<<** situado junto al propietario.

1. Revisa la ventana **Escala de tiempo del incidente**. Para la alerta *RegKey de inicio*, selecciona el icono de puntos suspensivos **(...)** y luego **Ejecutar cuaderno de estrategias**. Verás el cuaderno de estrategias *PostMessageTeams-OnAlert*. Esta opción te ayuda a ejecutar cuadernos de estrategias manualmente.

1. Cierra la hoja *Cuadernos de estrategias de alertas* seleccionando el icono ** x** en la parte superior derecha.

1. Revisa la ventana **Entidades**. Debería aparecer al menos la entidad *Host* que se ha asignado dentro de la consulta KQL del ejercicio anterior. **Sugerencia:** si no se muestran entidades, actualiza la página.

1. Selecciona el nuevo botón **Tareas (versión preliminar)** en la barra de comandos.

1. Selecciona **+ Agregar tarea**, escribe **Revisar quién es el propietario de la máquina** en el cuadro Título y selecciona **Guardar**.

1. Cierra la hoja *Tareas de incidentes (versión preliminar)* seleccionando el icono **x** en la parte superior derecha.

1. Selecciona el nuevo botón **Registro de actividad** en la barra de comandos.

1. Revisa las acciones que has realizado durante este ejercicio.

1. Cierra la hoja *Registro de actividad de incidentes* seleccionando el icono **x** en la parte superior derecha.

1. En la hoja izquierda casi oculta, selecciona el icono de usuario denominado **Sin asignar**. La nueva experiencia de incidente permite cambios rápidos desde aquí.

1. Selecciona **Asignar a mí** y desplázate hacia abajo para seleccionar **Aplicar** para guardar los cambios.

1. Expande la hoja izquierda seleccionando el icono **>>**. y luego selecciona el botón **Investigar**.

    >**Sugerencia:** si los iconos son demasiado pequeños para la pantalla, selecciona **(+)** para ampliarlos.

1. **Mueve el puntero sobre** el icono de entidad WINServer y espera a que se muestren nuevas *consultas de exploración*. Parece que *las alertas relacionadas* tienen más datos. Selecciona el nombre de la consulta de exploración **Alertas relacionadas** para llevarlas al gráfico de investigación o selecciona **Eventos >** para investigarlas con una consulta KQL.

1. Cierra la ventana de consulta seleccionando el icono **X** en la parte superior derecha para volver a la página *Investigación*.

1. Ahora, selecciona la entidad **WINServer**. Se abre una ventana a la derecha para obtener información más detallada. Revisa la página **Información**.

1. Selecciona el botón **Escala de tiempo**. Mantén el puntero sobre la escala de tiempo para ver qué elementos del gráfico se produjeron en un momento determinado.

1. Selecciona el botón **Entidades** y revisa las *entidades* y *alertas* relacionadas con *WINServer*.

1. Cierra el gráfico de investigación seleccionando el icono **X** situado en la parte superior derecha de la página.

1. En la página de incidente, en el panel izquierdo, selecciona **Estado activo** y selecciona **Cerrado**. 

1. En la lista desplegable *Seleccionar clasificación*, revisa las distintas opciones. Después, selecciona **Verdadero positivo: actividad sospechosa** y luego, **Aplicar**.

## Continúa con el ejercicio 9
