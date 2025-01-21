---
lab:
  title: "Ejercicio 2: conexión de dispositivos Windows a Microsoft\_Sentinel mediante conectores de datos"
  module: Learning Path 8 - Connect logs to Microsoft Sentinel
---

# Ruta de aprendizaje 8 - Laboratorio 1 - Ejercicio 2: conexión de dispositivos de Windows a Microsoft Sentinel mediante conectores de datos

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a conectar los datos de registro de los numerosos orígenes de datos de la organización. El siguiente origen de datos es máquinas virtuales Windows dentro y fuera de Azure, como entornos locales u otras nubes públicas.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 8 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: crear una máquina virtual Windows en Azure

En este ejercicio, crearás una máquina virtual Windows en Azure.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. Seleccione **+ Crear un recurso**. **Sugerencia:** si ya estabas en Azure Portal, es posible que tengas que seleccionar *Microsoft Azure* en la barra superior para ir a Inicio.

1. En el cuadro **Servicios de búsqueda y marketplace**, escribe *Windows 10* y selecciona **Microsoft Window 10** en la lista desplegable.

1. Selecciona el cuadro de **Microsoft Window 10**.

1. Abre la lista desplegable *Plan* y selecciona **Windows 10 Enterprise, versión 22H2**.

1. Selecciona **Iniciar con una configuración preestablecida** para continuar.

1. Selecciona **Desarrollo/pruebas** y luego, **Continuar para crear una máquina virtual**.

1. Selecciona **Crear nuevo** del *Grupo de recursos* y escribe RG-AZWIN01 como nombre y selecciona **Aceptar**.

    >**Nota:** este será un nuevo grupo de recursos con fines de seguimiento. 

1. En *Nombre de máquina virtual*, escribe AZWIN01.

1. Deja el valor predeterminado **(EE. UU.) Este de EE. UU.**  en *Región*.

1. Desplázate hacia abajo y revisa la *Imagen* de la máquina virtual. Si aparece vacío, selecciona **Windows 10 Enterprise, versión 22H2**.

1. Revisa el *Tamaño* de la máquina virtual. Si aparece vacío, selecciona **Ver todos los tamaños**, elige el primer tamaño de máquina virtual en *Más usados por los usuarios de Azure de Azure* y selecciona **Seleccionar**.

    >**Nota:** en caso de que veas el mensaje *Esta imagen no es compatible con Azure Automanage, para deshabilitar esta característica, ve a la pestaña Administración. De lo contrario, selecciona una imagen admitida.* Ve a la pestaña Administración y deshabilita "Automanage". El proceso de creación se realizará correctamente después.

1. Desplázate hacia abajo y escribe un *Nombre de usuario* que elijas. **Sugerencia:** evita palabras reservadas como admin o root.

1. Escribe una *contraseña* de tu preferencia. **Sugerencia:** puede ser más fácil volver a usar la contraseña del inquilino. Se puede encontrar en la pestaña recursos.

1. Desplázate hacia abajo hasta la parte inferior de la página y activa la casilla de *Licencias* para confirmar que tienes la licencia adecuada.

1. Selecciona **Revisar y crear** y espera a que se apruebe la validación.

    >**Nota:** si se produce un error de validación *Redes*, selecciona dicha pestaña, revisa su contenido y luego vuelve a seleccionar **Revisar y crear**.

1. Seleccione **Crear**. Espera hasta que se cree el recurso, lo que puede tardar unos minutos.

<!--- ### Task 2: Install Azure Arc on an On-Premises Server

In this task, you install Azure Arc on an on-premises server to make onboarding easier.

>**Important:** The next steps are done in a different machine than the one you were previously working. Look for the Virtual Machine name references.

1. Log in to **WINServer** virtual machine as Administrator with the password: **Passw0rd!** if necessary.  

1. Open the Microsoft Edge browser and navigate to the Azure portal at <https://portal.azure.com>.

1. In the **Sign in** dialog box, copy, and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy, and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Arc*, then select **Azure Arc**.

1. In the navigation pane under **Azure Arc resources** select **Machines**

1. Select **+ Add/Create**, then select **Add a machine**.

1. Select **Generate script** from the "Add a single server" section.

1. In the *Add a server with Azure Arc* page, select the Resource group you created earlier under *Project details*. **Hint:** *RG-Defender*

    >**Note:** If you haven't already created a resource group, open another tab and create the resource group and start over.

1. For *Region*, select **(US) East Us** from the drop-down list.

1. Review the *Server details* and *Connectivity method* options. Keep the default values and select **Next** to get to the Tags tab.

1. Review the default available tags. Select **Next** to get to the Download and run script tab.

1. Scroll down and select the **Download** button. **Hint:** if your browser blocks the download, take action in the browser to allow it. In Microsoft Edge Browser, select the ellipsis button (...) if needed and then select **Keep**.

1. Right-click the Windows Start button and select **Windows PowerShell (Admin)**.

1. Enter *Administrator* for "Username" and *Passw0rd!* for "Password" if you get a UAC prompt.

1. Enter: cd C:\Users\Administrator\Downloads

    >**Important:** If you do not have this directory, most likely means that you are in the wrong machine. Go back to the beginning of Task 4 and change to WINServer and start over.

1. Type *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* and press enter.

1. Enter **A** for Yes to All and press enter.

1. Type *.\OnboardingScript.ps1* and press enter.  

    >**Important:** If you get the error *"The term .\OnboardingScript.ps1 is not recognized..."*, make sure you are doing the steps for Task 4 in the WINServer virtual machine. Other issue might be that the name of the file changed due to multiple downloads, search for *".\OnboardingScript (1).ps1"* or other file numbers in the running directory.

1. Enter **R** to Run once and press enter (this may take a couple minutes).

1. The setup process opens a new Microsoft Edge browser tab to authenticate the Azure Arc agent. Select your admin account, wait for the message "Authentication complete" and then go back to the Windows PowerShell window.

1. When the installation finishes, go back to the Azure portal page where you downloaded the script and select **Close**. Close the **Add servers with Azure Arc** to go back to the Azure Arc **Machines** page.

1. Select **Refresh** until WINServer server name appears and the Status is *Connected*.

    >**Note:** This could take a couple of minutes. --->

### Tarea 2: conectarte a una máquina virtual Windows de Azure

En esta tarea, conectarás una máquina virtual Windows de Azure a Microsoft Sentinel.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Eventos de seguridad de Windows** y selecciónala en la lista.

1. En la página de la solución *Eventos de seguridad de Windows*, selecciona **Administrar**.

    >**Nota:** la solución *Eventos de seguridad de Windows* instala los *eventos de seguridad de Windows a través de AMA* y los *Eventos de seguridad a través del agente heredado*. Además de 2 libros, 20 reglas analíticas y 43 consultas de búsqueda.

1. Selecciona el conector de datos *Eventos de seguridad de Windows a través de AMA* y selecciona **Abrir página del conector** en la hoja de información del conector.

1. En la sección *Configuración*, en la pestaña *Instrucciones*, selecciona **Crear regla de recopilación de datos**.

1. Escribe **AZWINDCR** como Nombre de regla y luego selecciona **Siguiente: recursos**.

1. Selecciona **+Agregar recursos** para seleccionar la máquina virtual que hemos creado.

1. Expande **RG-AZWIN01** y selecciona **AZWIN01**.

1. Selecciona **Siguiente** y después, **Siguiente: recopilar**.

1. Revisa la opción de recopilación de eventos de seguridad diferente. Mantén *Todos los eventos de seguridad* y luego selecciona **Siguiente: revisar y crear**.

1. Selecciona **Crear** para crear la regla de recopilación de datos.

1. Espera un minuto y selecciona **Actualizar** para ver la nueva regla de recopilación de datos en la lista.

### Tarea 4: conectar una máquina Windows que no es de Azure

En esta tarea, agregarás una máquina virtual Windows que no sea de Azure Arc conectada a Microsoft Sentinel.  

   >**Nota:** el conector de datos *Eventos de Seguridad de Windows a través de AMA* requiere Azure Arc para dispositivos que no son de Azure.

1. Asegúrate de que estás en la configuración del conector de datos *Eventos de seguridad de Windows a través de AMA* en el área de trabajo de Microsoft Sentinel.

1. En la pestaña **Instrucciones**, en la sección *Configuración*, edita la *regla de recopilación de datos* **AZWINDCR** seleccionando el icono de *lápiz*.

1. Seleccione **Siguiente: Recursos**, y expanda la *Suscripción* en *Ámbito* en la pestaña *Recursos*.

    >**Sugerencia:** puede expandir toda la jerarquía de *Ámbito* seleccionando el signo ">" antes de la columna *Ámbito*.

1. Expande **RG-Defender** (o el grupo de recursos que has creado) y luego selecciona **WINServer**.

    >**Importante:** si no ves WINServer, consulta la ruta de aprendizaje 3, ejercicio 1, tarea 4 donde has instalado Azure Arc en este servidor.

1. Seleccione **Aplicar**.

1. Selecciona **Siguiente: recopilar** y **Siguiente: revisar y crear**.

1. Una vez que aparezca **Validación superada**, selecciona *Crear*.

## Continúa con el ejercicio 3
