---
lab:
  title: "Ejercicio 1: mitigación de ataques con Microsoft\_Defender para puntos de conexión"
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# Ruta de aprendizaje 2 - Laboratorio 1 - Ejercicio 2: mitigación de ataques con Microsoft Defender para puntos de conexión

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que está implementando Microsoft Defender para punto de conexión. El administrador tiene previsto incorporar algunos dispositivos para dar información sobre los cambios necesarios en los procedimientos de respuesta del equipo de SecOps.

Para explorar las funcionalidades de mitigación de ataques de Defender para punto de conexión, comprobará la incorporación correcta de dispositivos e investigará alertas e incidentes creados durante ese proceso.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos.

### Tarea 1: comprobar la incorporación de dispositivos

En esta tarea, confirmarás que el dispositivo se ha incorporado correctamente y crearás una alerta de prueba.

1. Si aún no está en el portal de Microsoft Defender XDR en el explorador Microsoft Edge, vaya a (https://security.microsoft.com) e inicie sesión como Administrador del inquilino.

1. En el menú de la izquierda, en el área **Recursos**, selecciona **Dispositivos**. Espere hasta que WIN1 aparezca en la página Dispositivos antes de continuar. De lo contrario, es posible que tengas que repetir esta tarea para ver las alertas que se generarán más adelante.

    >**Nota:** Si has completado el proceso de incorporación y no ves dispositivos en la lista Dispositivos después de una hora, podría indicar un problema de incorporación o conectividad.

1. Selecciona **Configuración** en la barra de menús de la izquierda. Después, en la página Configuración, selecciona **Puntos de conexión**.

1. Selecciona **Incorporación** en la sección Administración de dispositivos y asegúrate de que *"Windows 10 y 11"* esté seleccionado como sistema operativo. El mensaje *"Primer dispositivo incorporado"* ahora muestra *Completado*.

1. Desplázate hacia abajo y, en la sección *"2. Ejecutar una prueba de detección"*, copia el script de prueba de detección seleccionando el botón **Copiar**.  

1. En la barra de búsqueda de Windows de la máquina virtual WIN1, escribe **CMD** y elige **Ejecutar como administrador** en el panel derecho de la aplicación de símbolo del sistema.

1. Cuando se muestre la ventana "Control de cuentas de usuario", selecciona **Sí** para permitir que se ejecute la aplicación. 

1. Pega el script haciendo clic con el botón derecho en las ventanas **Administrador: símbolo del sistema** y presiona **Entrar** para ejecutarlo.

    >**Nota:** La ventana se cierra automáticamente después de ejecutar correctamente el script y después de unos minutos se generan alertas en el portal de Microsoft Defender XDR.

<!--- ### Task 2: Simulated Attacks

>**Note:** The Evaluation lab and the Tutorials & simulations section of the portal is no longer available. Please refer to the **[interactive lab simulation](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20attacks%20with%20Microsoft%20Defender%20for%20Endpoint)** for a demonstration of the simulated attacks.

1. From the left menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button.

    <!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### Tarea 2: Investigar alertas e incidentes

En esta tarea, investigará las alertas e incidentes generados por el script de prueba de detección de incorporación en la tarea anterior.

1. En el portal de Microsoft Defender XDR, seleccione **incidentes y alertas** en la barra de menús de la izquierda y, a continuación, seleccione **Alertas**.

1. En el panel **Alertas**, seleccione la alerta denominada *Línea de comandos sospechosa de PowerShell* para cargar sus detalles.

1. Revise la escala de tiempo de la *Historia de la alerta* y, a continuación, revise las pestañas *Detalles* y *Recomendaciones*.

    >**Nota:** En la pestaña *Detalles* de la alerta puede desplazarse hasta la sección *Detalles del incidente* y seleccionar el enlace *Incidente de ejecución en un punto de conexión* para abrir el incidente.

1. En el portal de Microsoft Defender XDR, seleccione **incidentes y alertas** en la barra de menús de la izquierda y, a continuación, seleccione **Incidentes**

1. Un nuevo incidente denominado *Incidente de ejecución en un punto de conexión* está en el panel derecho. Selecciona el nombre del incidente para cargar sus detalles.

1. Seleccione el vínculo **Administrar incidentes** (con un icono de lápiz) y aparecerá una nueva hoja de ventana.

1. En **Etiquetas de incidente**, escriba "Simulación" y seleccione **Simulación (Crear nueva)** para crear una nueva etiqueta.

1. Selecciona el botón de alternancia **Asignar a** y agrega tu cuenta de usuario (Me) como propietario del incidente.

1. En **Clasificación**, expande el menú desplegable.

1. En **Información, actividad esperada**, selecciona **Pruebas de seguridad**.

1. Agrega los comentarios, si quieres, y selecciona **Guardar** para actualizar el incidente y finalizar.

1. Revisa el contenido de las pestañas *Ataque, Alertas, Activos, Investigaciones, Evidencia y Respuesta* y *Resumen*. Los dispositivos y los usuarios se encuentran en la pestaña *Recursos*. En un incidente real, la pestaña *Historia de ataque* muestra el *gráfico del incidente*. **Sugerencia:** Es posible que algunas pestañas estén ocultas debido al tamaño de la pantalla. Selecciona la pestaña de puntos suspensivos (...) para que aparezcan.

<!---    >**Warning:** The simulated attacks here are an excellent source of learning through practice. Only perform the attacks in the instructions provided for this lab when using the course provided Azure tenant.  You may perform other simulated attacks *after* this training course is complete with this tenant. --->

## Has completado el laboratorio
