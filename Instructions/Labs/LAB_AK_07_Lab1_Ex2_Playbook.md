---
lab:
  title: 'Ejercicio 2: creación de un cuaderno de estrategias'
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 7 - Laboratorio 1 - Ejercicio 2: creación de un cuaderno de estrategias

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex2.png)

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a detectar y mitigar amenazas mediante Microsoft Sentinel. Ahora, quieres responder y corregir acciones que se pueden ejecutar desde Microsoft Sentinel como rutina.

Un cuaderno de estrategias puede ayudarte a automatizar y organizar la respuesta a las amenazas, se puede integrar con otros sistemas de manera interna y externa, y se puede configurar para ejecutarse automáticamente en respuesta a alertas o incidentes específicos, cuando se desencadena mediante una regla de análisis o una regla de automatización, respectivamente. 

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20a%20playbook)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos.

### Tarea 1: crear un equipo del Centro de operaciones de seguridad en Microsoft Teams

En esta tarea, crearás un equipo de Microsoft Teams para usarlo en el laboratorio.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, abre una nueva pestaña y ve al portal de Microsoft Teams en (https://teams.microsoft.com).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. Cierra los elementos emergentes de Teams que puedan aparecer.

    >**Nota:** Si se le pide que utilice **New Teams** acepte y continúe con el ejercicio.

1. Si aún no está seleccionado, selecciona **Teams** en el menú izquierdo y, en la parte superior, selecciona el ![icono de signo más](../Media/plus-sign-icon-lab.png).

1. Selecciona la opción **Crear equipo**.

1. Selecciona el botón **Desde cero**.

1. Selecciona el botón **Privado**.

1. Asigna al equipo el nombre: escribe **SOC** y selecciona el botón **Crear**.

1. En la pantalla Agregar miembros a SOC, selecciona el botón **Omitir**. 

1. Desplázate hacia abajo en la hoja de Teams para buscar el equipo de SOC recién creado, selecciona los puntos suspensivos **(...)** en el lado derecho del nombre y selecciona **Agregar canal**.

1. Escribe un nombre de canal de *Nuevas alertas* y selecciona el botón **Agregar**.


### Tarea 2: crear un cuaderno de estrategias de Microsoft Sentinel

En esta tarea, crearás una aplicación lógica que se usa como cuaderno de estrategias en Microsoft Sentinel.

1. En el explorador Microsoft Edge, ve a [Microsoft Sentinel en GitHub](https://github.com/Azure/Azure-Sentinel).

<!--- the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace you created earlier.

1. Select the **Community** page under the *Content management* area on the left side of the page.

1. On the right pane, select the **Onboard community content** link. This opens a new tab in the Microsoft Edge Browser for Microsoft Sentinel GitHub content. **Hint:** You might need to scroll right to see the link. Alternatively, follow this link instead: [Microsoft Sentinel on GitHub](https://github.com/Azure/Azure-Sentinel). --->

1. Desplázate hacia abajo y selecciona la carpeta **Soluciones**.

1. Después, selecciona la carpeta **SentinelSOARessentials**, luego la carpeta **Cuadernos de estrategias**.

1. Selecciona la carpeta **Post-Message-Teams**.

1. En el cuadro readme.md, desplázate hacia abajo hasta la sección *Implementación rápida*, **Implementar con desencadenador de incidentes (recomendado)** y selecciona el botón **Implementar en Azure**.  

1. Comprueba que has seleccionado Suscripción de Azure.

1. En Grupo de recursos, selecciona **Crear nuevo**, escribe *RG-Playbooks* y selecciona **Aceptar**.

1. Deja el valor predeterminado **(EE. UU.) Este de EE. UU.**  en *Región*.

1. Cambia el nombre del *Cuaderno de estrategias* por "PostMessageTeams-OnIncident" y selecciona **Revisar y crear**.

1. Ahora, selecciona **Crear**. 

    >**Nota**: espera a que la implementación se complete antes de continuar con la tarea siguiente.

### Tarea 3: actualizar un cuaderno de estrategias en Microsoft Sentinel

En esta tarea, actualizarás el nuevo cuaderno de estrategias que has creado con la información de conexión adecuada.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona **Automatización** en el área *Configuración* y luego selecciona la pestaña **Cuadernos de estrategias activos**.

1. Selecciona **Actualizar** en la barra de comandos en caso de que no veas ningún cuaderno de estrategias. Debería ver el cuaderno de estrategias creado a partir del paso anterior.

1. Seleccione el nombre del cuaderno de estrategias **PostMessageTeams**.

1. En la página Aplicación lógica de *PostMessageTeams*, en el menú de comandos, seleccione **Editar**.

    >**Nota:**: es posible que tengas que actualizar la página.

1. Seleccione el *primer* bloque, **incidente de Microsoft Sentinel**.

1. Selecciona el vínculo **Cambiar conexión**.

1. Selecciona **Agregar nuevo** y selecciona **Iniciar sesión**. En la nueva ventana, selecciona las credenciales de administrador de la suscripción de Azure cuando se te solicite. La última línea del bloque ahora debería decir "Conectado a nombre-usuario-admin".

1. Ahora seleccione el *segundo* bloque, **Publicar un mensaje (V3)**.

1. En la pestaña Prameters (Prameters), desplácese hacia abajo y seleccione el vínculo **Cambiar conexión** y, a continuación, seleccione **Agregar nuevo** e **Iniciar sesión**. Elija las credenciales de administrador de Azure cuando se le solicite. La pestaña Prameters debe leer ahora "Conectado a su nombre de usuario-administrador".

1. Al final del campo *Equipo*, seleccione la **X** para borrar el contenido. El campo cambia a una lista desplegable con una lista de los equipos disponibles de Microsoft Teams. Selecciona **SOC**.

1. Haz lo mismo para el campo *Canal*, selecciona la **X** al final del campo para borrar el contenido. El campo cambia a una lista desplegable con una lista de los canales de equipos de SOC. Selecciona **Nuevas alertas**.

1. Seleccione **Guardar** en la barra de comandos. La aplicación lógica se usará en un laboratorio futuro.

## Continúa con el ejercicio 3
