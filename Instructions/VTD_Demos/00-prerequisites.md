
# Microsoft Security Operations Analyst
Guía de preparación del instructor

## Propósito

Este documento está dirigido a los moderadores que se preparan para impartir el Día de aprendizaje virtual de seguridad de Microsoft para `Defend Against Threats with Extended Detection and Response` y `Configure Security Operations Using Microsoft Sentinel`. Este material es un subconjunto del curso de certificación SC-200: Microsoft Security Operations Analyst.

## Requisitos previos de demostración

Los laboratorios de este curso requieren un inquilino con licencia de Microsoft 365 E5 con una licencia de Microsoft Defender para punto de conexión P2 y una suscripción a Azure.

* Al igual que en el curso SC-200 Microsoft Security Operations Analyst, estas demostraciones se han diseñado para ejecutarse en un entorno de hospedaje de laboratorio autorizado.
* Las instrucciones para el laboratorio están en el [repositorio SC-200 de Microsoft Learning en GitHub](https://github.com/MicrosoftLearning/SC-200T00A-Microsoft-Security-Operations-Analyst/tree/master/Instructions/VTD_Demos/).
* Asegúrate de que el equipo que vas a usar para las demostraciones tenga instalado el nuevo explorador Microsoft Edge.

>**Nota:** como se indicó anteriormente, hay demostraciones que requieren una suscripción a Azure conectada a un inquilino de Microsoft 365 E5. Puedes usar tu propia suscripción a Azure y el inquilino de Microsoft 365 E5. Visita el sitio web del [Programa para desarrolladores de Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program/) para solicitar la suscripción y configurar una suscripción gratuita para desarrolladores de Microsoft 365 E5.

## Implementación de Defender para punto de conexión

### Obtención de tus credenciales de Microsoft 365

Una vez que inicias el laboratorio alojado, tienes a tu disposición un inquilino de prueba gratuito al que podrás acceder en el entorno de Laboratorio virtual de Microsoft. Automáticamente, se le asigna un nombre de usuario y una contraseña únicos a este inquilino. Debes recuperar este nombre de usuario y contraseña para que puedas iniciar sesión en Azure y Microsoft 365 en el entorno de Microsoft Virtual Lab.

Dado que los asociados de aprendizaje pueden ofrecer este curso mediante cualquiera de los diversos proveedores de hospedaje de laboratorio autorizados, los pasos reales necesarios para recuperar el identificador de inquilino asociado al inquilino pueden variar según el proveedor de hospedaje de laboratorio. Por lo tanto, tu instructor te dará las instrucciones necesarias sobre cómo recuperar esta información para tu curso. La información que debes tener en cuenta para uso posterior incluye:

-**Id. de sufijo de inquilino.** Este identificador es para las cuentas de onmicrosoft.com que usarás para iniciar sesión en Microsoft 365 en todos los laboratorios. Se trata del formato **{username}@M365xZZZZZZ.onmicrosoft.com**, donde ZZZZZZ es el identificador de sufijo de inquilino único que ha facilitado el proveedor de hospedaje de laboratorio. Anota este valor ZZZZZZ para más adelante. Cuando cualquiera de los pasos del laboratorio te dirija a iniciar sesión en los portales de Microsoft 365, debes escribir el valor ZZZZZZ que has obtenido aquí.

-**Contraseña de inquilino.** Escribe la contraseña de administrador que te ha facilitado tu proveedor de hospedaje de laboratorio.

### Inicialización de Microsoft Defender para punto de conexión

En esta tarea, realizarás la inicialización de Microsoft Defender para punto de conexión.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve al portal de Microsoft Defender en (https://security.microsoft.com)).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

En el portal de **Microsoft Defender** en el menú de navegación, selecciona **Inicio** a la izquierda.

    >**Note:** You may need to scroll all the way to the menu top.

1. En la página del portal **Inicio**, se muestra **Bienvenido a Microsoft Defender**.

1. Desplázate por los elementos del menú hasta **Recursos** y selecciona **Dispositivos**.

1. El proceso para implementar el área de trabajo de Defender XDR debería comenzar y deberías ver mensajes que digan *cargando e Inicializando* brevemente en la parte superior de la página, y luego vas a ver una imagen de una taza de café y un mensaje que dice: **¡Espera! Preparamos nuevos espacios para tus datos y los conectamos.** Tarda aproximadamente 5 minutos en finalizar. *Deja abierta la página y asegúrate de que finaliza, ya que es necesario para el siguiente laboratorio.*

    >**Nota:** ignora los mensajes de error emergentes que indican que *algunos de los datos no se pueden recuperar*. Si el mensaje "Espera, se están preparando nuevos espacios para tus datos y conectándolos" no aparece, o bien se abre la página "Configuración > Microsoft Defender XDR > Cuenta", pero aparece el mensaje *Error al cargar la ubicación del almacenamiento de datos. Inténtalo de nuevo más tarde*, selecciona "Configuración del servicio de alertas" en el menú "General".

1. Cuando la nueva inicialización del área de trabajo se complete correctamente, la página **Inicio** del portal principal mostrará un banner de **Obtención de SIEM y XDR en un solo lugar**. Además, en **Configuración**, la configuración general de Microsoft Defender XDR para la cuenta, las notificaciones por correo electrónico, las **características en versión preliminar**, la configuración del servicio de alertas, los permisos y los roles y la API de streaming están ahora activadas.

1. Cuando el nuevo espacio se complete correctamente, verás la configuración general de Microsoft 365 Defender para la cuenta, las notificaciones por correo electrónico, la configuración del servicio de alertas, los permisos y los roles y la API de streaming. También verás las **características en versión preliminar** activadas.

    >**Nota**: en el entorno de laboratorio hospedado, la ubicación de almacenamiento de datos debe seleccionarse automáticamente. Además, debe estar en la geografía adecuada para el lugar donde se administra este inquilino de entrenamiento. Todavía puedes seleccionar la longitud de retención de datos, pero no es necesaria.

1. Mientras estés en **Configuración**, selecciona **Puntos de conexión**.

1. Selecciona **Incorporación** en la sección Administración de dispositivos.

    >**Nota:** también puedes realizar la incorporación de dispositivos en la sección **Recursos** de la barra de menús de la izquierda. Expande Recursos y selecciona Dispositivos. En la página Inventario de dispositivos, con equipos y móviles seleccionados, desplázate hacia abajo hasta **Incorporar dispositivos.** De esta forma pasas a la página **Configuración > Puntos de conexión**.

1. En el "1. Al incorporar un área de dispositivo asegúrate de que, en el menú desplegable Método de implementación, aparezca "Script local (para un máximo de 10 dispositivos)" y selecciona el botón **Descargar paquete de incorporación**.

1. Extrae en una carpeta local como la carpeta Documentos el contenido del archivo zip descargado.

1. Haz clic con el botón derecho en el archivo extraído WindowsDefenderATPLocalOnboardingScript.cmd y elige **Ejecutar como administrador**.  Si encuentras Windows SmartScreen, elige Ejecutar de todos modos.

**Nota** de forma predeterminada, el archivo debe estar en el directorio c:\users\admin\downloads.
    
1. Responde **Y** a las preguntas presentadas por el script. Cuando hayas terminado, deberías ver un mensaje en la pantalla de comandos que dice algo parecido a "Máquina incorporada correctamente..." 

1. En la página Incorporación del portal, copia el script de prueba de detección y ejecútalo en una ventana de comandos abierta.  Es posible que tengas que abrir una nueva ventana **Administrador: símbolo del sistema** escribiendo *CMD* en la barra de búsqueda de Windows y elegir **Ejecutar como administrador**.

1. En el menú del portal de Microsoft 365 Defender, selecciona **Inventario de dispositivos**. Deberías ver ahora tu dispositivo en la lista.

**Nota**: el dispositivo puede tardar hasta 5 minutos en aparecer en el portal.


### Configurar rol

En esta tarea, configurarás roles para su uso con grupos de dispositivos.

1. En el portal de Microsoft 365 Defender, en el menú de navegación, selecciona **Configuración** a la izquierda. 

1. Selecciona **Puntos de conexión** y luego selecciona **Roles** en el área de permisos.

1. Selecciona el botón **Activar roles**.

1. Selecciona **Agregar elemento**.

1. En el cuadro de diálogo Añadir rol, escribe lo siguiente:

    |Configuración general|Value|
    |---|---|
    |Nombre de rol|**Soporte técnico de nivel 1**|
    |Permisos|Funciones avanzadas de respuesta dinámica|

1. Selecciona **Siguiente**.

1. En la pestaña Grupos de usuarios asignados. Selecciona **sg-IT** y luego selecciona **Agregar grupos seleccionados**.

1. Selecciona **Guardar**.

### Configuración de los grupos de dispositivos

En esta tarea, configurarás los grupos de dispositivos que permiten el control de acceso y la configuración de automatización.

1. Selecciona **Configuración** en el menú de navegación izquierdo. 

1. Selecciona **Puntos de conexión** y, en el área de permisos, selecciona **Grupos de dispositivos**.

1. Selecciona **Agregar** grupo de dispositivos.

1. En la pestaña General, escribe la siguiente información:

    |Configuración general|Value|
    |---|---|
    |Nombre del grupo de dispositivos|**Regular**|
    |Nivel de automatización|Completo: corregir las amenazas automáticamente|

1. Selecciona **Siguiente**.

1. . En la pestaña Dispositivos, para la condición del sistema operativo, selecciona **Windows 10** y **Siguiente**.

1. En la pestaña Vista previa de dispositivos, selecciona **Mostrar vista previa** para ver la máquina virtual WIN1. Selecciona **Siguiente**. 
**Sugerencia:** si no ves la máquina virtual en la lista de vista previa, vuelve y selecciona también *Ninguno* para la condición del sistema operativo. Los datos de la máquina virtual todavía no están rellenados.

1. En la pestaña Acceso de usuario, selecciona **sg-IT** y después, **Agregar grupos seleccionados**

1. Selecciona **Listo**.

1. La configuración del grupo de dispositivos ha cambiado. Selecciona **Aplicar cambios** para comprobar las coincidencias y recalcular las agrupaciones.

1. Ahora tendrás dos grupos de dispositivos; "Normal" que acabas de crear y "Dispositivos sin agrupar (valor predeterminado)" con el mismo nivel de corrección.

<!--- 
## Deploy sample alerts for Demo in Module 3

In this task, you will load sample security alerts and review the alert details.

1. In the Edge browser, open the Azure portal at https://portal.azure.com.

1. In the **Sign in** dialog box, copy and paste in the **Tenant Email** account provided by your lab hosting provider and then select **Next**.

1. In the **Enter password** dialog box, copy and paste in the **Tenant Password** provided by your lab hosting provider and then select **Sign in**.

1. In the Search bar of the Azure portal, type *Defender*, then select **Microsoft Defender for Cloud**.

1. In the **Getting Started** menu the default selection is **Upgrade**, select or **Skip** for now.

1. Select **Security alerts** in the portal menu.

1. Select **Sample Alerts** from the command bar.

1. In the Create sample alerts (Preview) pane make sure your subscription is selected.  Make sure all sample alerts are selected and select **Create sample alerts**.  

**Note** This may take a few minutes to complete. --->

## Implementación del área de trabajo de Microsoft Sentinel para demo en el módulo 4

En esta tarea, crearás un área de trabajo de Microsoft Sentinel.

 >**Nota:** deberás tener una suscripción a Azure activa para la siguiente demostración.

1. En el explorador Microsoft Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **+ Crear**.

1. Selecciona **+ Crear una nueva área de trabajo**.

**Nota**: primero, crea una nueva área de trabajo de Log Analytics

1. Selecciona la suscripción adecuada.

1. Selecciona el vínculo **Crear nuevo** para el grupo de recursos y escribe un nuevo nombre para el grupo de recursos de tu elección.

1. En Detalles de la instancia del campo de nombre, escribe un nombre de tu preferencia para el área de trabajo de Log Analytics.

**Nota:** este nombre debe ser único y también será el nombre del área de trabajo de Microsoft Sentinel.

1. Selecciona la región que sea apropiada para ti.  La región adecuada puede ser predeterminada o el instructor puede tener consejos específicos sobre qué región seleccionar.  

1. Selecciona **Revisar + crear**.

1. Selecciona **Crear**. Espera a que la nueva área de trabajo de Log Analytics aparezca en la lista de la página Agregar Microsoft Sentinel a un área de trabajo.  Esta operación puede tardar unos minutos.

1. Selecciona el área de trabajo recién creada cuando aparezca y luego selecciona **Agregar**.

## Implementación de soluciones y conectores de datos del Centro de contenido para Microsoft Sentinel

### Tarea 1: Acceso al área de trabajo de Microsoft Sentinel

En esta tarea, accederás al área de trabajo de Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. Abre el explorador, busca, descarga e instala el nuevo explorador Microsoft Edge. Abre el nuevo explorador Microsoft Edge.

1. En el explorador Microsoft Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado en la tarea anterior.

### Tarea 2: Establecimiento de conexión con el conector de datos de actividad de Azure

En esta tarea, conectarás el conector de datos de *Actividad de Azure*.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Actividad de Azure** y selecciónala en la lista.

1. En la página de la solución *Microsoft Defender for Cloud*, selecciona **Instalar**.

1. Cuando se haya completado la instalación, selecciona **Siguiente**.

    >**Nota:** la solución *Actividad de Azure* instala el conector de datos *Actividad de Azure*, 12 reglas analíticas, 14 consultas de búsqueda y 1 libro.

1. Selecciona el conector de datos *Actividad de Azure* y luego selecciona **Abrir página del conector**.

1. En el área *Instrucciones*, en la pestaña *Instrucciones*, desplázate hacia abajo hasta "2. Conecta las suscripciones..." y selecciona **Iniciar asistente para asignación de directivas de Azure>**.

1. En la pestaña **Datos básicos**, selecciona el botón de puntos suspensivos (...) en **Ámbito**, elige la suscripción a Azure alojada en la lista desplegable y selecciona **Seleccionar**.

1. Selecciona la pestaña **Parámetros** y elige el área de trabajo de la lista desplegable **Área de trabajo de Log Analytics principal** Esta acción aplica la configuración de la suscripción para enviar la información al área de trabajo de Log Analytics.

1. Selecciona la pestaña **Corrección** y activa la casilla **Crear una tarea de corrección**. Esta acción aplica la directiva a los recursos de Azure ya existentes.

1. Selecciona el botón **Revisar y crear** para revisar la configuración.

1. Selecciona **Crear** para finalizar.

### Tarea 3: Creación de una máquina virtual Windows en Azure

En este ejercicio, crearás una máquina virtual Windows en Azure.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. Selecciona **+ Crear un recurso**. **Sugerencia:** si ya estabas en Azure Portal, es posible que tengas que seleccionar *Microsoft Azure* en la barra superior para ir a Inicio.

1. En el cuadro **Servicios de búsqueda y marketplace**, escribe *Windows 10* y selecciona **Microsoft Window 10** en la lista desplegable.

1. Selecciona el cuadro de **Microsoft Window 10**.

1. Abre la lista desplegable *Plan* y selecciona **Windows 10 Enterprise, versión 22H2**.

1. Selecciona **Iniciar con una configuración preestablecida** para continuar.

1. Selecciona **Desarrollo/pruebas** y luego, **Continuar para crear una máquina virtual**.

1. Selecciona **Crear nuevo** para *Grupo de recursos*, escribe el nombre `RG-AZWIN01` y selecciona **Aceptar**.

    >**Nota:** este será un nuevo grupo de recursos con fines de seguimiento. 

1. En *Nombre de la máquina virtual*, escribe `AZWIN01`.

1. Deja el valor predeterminado **(EE. UU.) Este de EE. UU.**  en *Región*.

1. Desplázate hacia abajo y revisa la *Imagen* de la máquina virtual. Si aparece vacío, selecciona **Windows 10 Enterprise, versión 22H2**.

1. Revisa el *Tamaño* de la máquina virtual. Si aparece vacío, selecciona **Ver todos los tamaños**, elige el primer tamaño de máquina virtual en *Más usados por los usuarios de Azure de Azure* y selecciona **Seleccionar**.

    >**Nota:** en caso de que veas el mensaje *Esta imagen no es compatible con Azure Automanage, para deshabilitar esta característica, ve a la pestaña Administración. De lo contrario, selecciona una imagen admitida.* Ve a la pestaña Administración y deshabilita "Automanage". El proceso de creación se realizará correctamente después.

1. Desplázate hacia abajo y escribe un *Nombre de usuario* que elijas. **Sugerencia:** evita palabras reservadas como admin o root.

1. Escribe una *contraseña* de tu preferencia. **Sugerencia:** puede ser más fácil volver a usar la contraseña del inquilino. Se puede encontrar en la pestaña recursos.

1. Desplázate hacia abajo hasta la parte inferior de la página y activa la casilla de *Licencias* para confirmar que tienes la licencia adecuada.

1. Selecciona **Revisar y crear** y espera a que se apruebe la validación.

    >**Nota:** si se produce un error de validación *Redes*, selecciona dicha pestaña, revisa su contenido y luego vuelve a seleccionar **Revisar y crear**.

1. Selecciona **Crear**. Espera hasta que se cree el recurso, lo que puede tardar unos minutos.

### Tarea 4: Conexión a una máquina virtual de Azure Windows

En esta tarea, conectarás una máquina virtual Windows de Azure a Microsoft Sentinel.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. 1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Eventos de seguridad de Windows** y selecciónala en la lista.

1. En la página de la solución *Eventos de seguridad de Windows*, selecciona **Instalar**.

1. Cuando se haya completado la instalación, selecciona **Siguiente**.

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

### Tarea 5: Instalación de Azure Arc y conexión de un servidor local

En esta tarea, instalarás Azure Arc en un servidor local para facilitar la incorporación.

>**Importante:** los pasos siguientes se realizan en una máquina diferente a la que trabajabas anteriormente. Busca las referencias de nombre de máquina virtual.

1. Inicia sesión en la máquina virtual **WINServer** como administrador con la contraseña: **Passw0rd!** si es necesario.  

1. Abre el explorador Microsoft Edge y ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Arc* y luego selecciona **Azure Arc**.

1. En el panel de navegación, en **Infraestructura**, selecciona **Máquinas.**

1. Selecciona **+ Agregar o crear** y después, **Agregar una máquina**.

1. Selecciona **Generar script** en la sección "Agregar un solo servidor".

1. Lee la pestaña *Requisitos previos* y selecciona **Siguiente** para continuar.

1. En la página *Agregar un servidor con Azure Arc*, selecciona el grupo de recursos que has creado anteriormente en *Detalles del proyecto*. **Sugerencia: ***RG-Defender*

    >**Nota:** si todavía no has creado un grupo de recursos, abre otra pestaña y crea el grupo de recursos y vuelve a empezar.

1. Revisa los *Detalles del servidor* y las opciones *Método de conectividad*. Mantén los valores predeterminados y selecciona **Siguiente** para ir a la pestaña Etiquetas.

1. Revisa las etiquetas disponibles predeterminadas. Selecciona **Siguiente** para ir a la pestaña Descargar y ejecutar script.

1. Desplázate hacia abajo y selecciona el botón **Descargar**. **Sugerencia:** si el explorador bloquea la descarga, realiza una acción en el explorador para permitirla. En el explorador Microsoft Edge, selecciona el botón de puntos suspensivos (...) si es necesario y luego selecciona **Mantener**.

1. Haz clic con el botón derecho en Inicio de Windows y selecciona **Windows PowerShell (Administrador)**.

1. Escribe *Administrador* como nombre de usuario y *Passw0rd!* para "Contraseña" si recibes un mensaje de UAC.

1. Escribe: cd C:\Users\Administrator\Downloads

    >**Importante:** si no tienes este directorio, lo más probable es que estés en la máquina incorrecta. Vuelve al principio de la tarea 4, cambia a WINServer y vuelve a empezar.

1. Escribe *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* y presiona Entrar.

1. Escribe **A** para Sí a todo y presiona entrar.

1. Escribe *.\OnboardingScript.ps1* y presiona entrar.  

    >**Importante:** si recibes el error *"El término .\OnboardingScript.ps1 no se reconoce..."*, asegúrate de que estás siguiendo los pasos de la tarea 4 en la máquina virtual WINServer. Otro problema podría ser que el nombre del archivo ha cambiado debido a varias descargas, busca *".\OnboardingScript (1).ps1"* u otros números de archivo en el directorio en ejecución.

1. Escribe **R** para ejecutar una vez y presiona entrar (esto puede tardar un par de minutos).

1. El proceso de configuración abrirá una nueva pestaña del explorador Microsoft Edge para autenticar al agente de Azure Arc. Selecciona la cuenta de administrador, espera el mensaje "Autenticación completada" y vuelve a la ventana de Windows PowerShell.

1. Cuando finalice la instalación, vuelve a la página de Azure Portal donde has descargado el script y selecciona **Cerrar**. Cierra la página **Agregar servidores con Azure Arc** para volver a la página **Máquinas** de Azure Arc.

1. Selecciona **Actualizar** hasta que aparezca el nombre del servidor WINServer y el estado sea *Conectado*.

    >**Nota:** esto puede tardar varios minutos.

### Tarea 6: Protección de un servidor local

En esta tarea, agregarás una máquina virtual Windows que no sea de Azure Arc conectada a Microsoft Sentinel.  

   >**Nota:** el conector de datos *Eventos de Seguridad de Windows a través de AMA* requiere Azure Arc para dispositivos que no son de Azure.

1. Asegúrate de que estás en la configuración del conector de datos *Eventos de seguridad de Windows a través de AMA* en el área de trabajo de Microsoft Sentinel.

1. En la pestaña **Instrucciones**, en la sección *Configuración*, edita la *regla de recopilación de datos* **AZWINDCR** seleccionando el icono de *lápiz*.

1. Selecciona **Siguiente: recursos** y **+Agregar recursos**.

1. Expande el grupo de recursos que has creado y selecciona **WINServer**.

    >**Importante:** si no ves WINServer, consulta la ruta de aprendizaje 3, ejercicio 1, tarea 4 donde has instalado Azure Arc en este servidor.

1. Seleccione **Aplicar**.

1. Selecciona **Siguiente: recopilar** y **Siguiente: revisar y crear**.

1. Una vez que aparezca **Validación superada**, selecciona *Crear*.

### Tarea 7: Conexión de Defender XDR

En esta tarea, implementará el conector de Microsoft Defender XDR.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en (<https://portal.azure.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección **Administración de contenido** y selecciona **Centro de contenido**.

1. En *Centro de contenido*, busca la solución ** Microsoft Defender XDR** y selecciónala en la lista.

1. En la página de detalles de la solución de *Microsoft Defender XDR*, selecciona **Instalar**.

1. Cuando se complete la instalación, busca la solución **Microsoft Defender XDR** y selecciónala.

1. En la página de detalles de la solución de *Microsoft Defender XDR*, selecciona **Administrar**

1. Activa la casilla Conector de datos de *Microsoft Defender XDR* y selecciona la **página Abrir conector**.

1. En la sección *Configuración*, en la pestaña *Instrucciones*, **anula la selección** de la casilla *Desactivar todas las reglas de creación de incidentes de Microsoft para estos productos. Recomendado*, y selecciona el botón **Conectar incidentes y alertas**.

1. Deberías recibir un mensaje que indique que la conexión ha sido satisfactoria.

<!--- ### Task 4: Connect the Microsoft Defender for Cloud connector.

In this task, you will connect the Microsoft Defender for Cloud connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Cloud** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 5: Connect the Microsoft Defender for Cloud Apps connector.

In this task, you will connect theMicrosoft Defender for Cloud Apps connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Cloud Apps** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the **Instructions** tab in the **Configuration** section, select **Alerts** and then select **Apply Changes**.

### Task 6: Connect the Microsoft Defender for Office 365 connector.

In this task, you will connect the Microsoft Defender for Office 365 connector.

1. From the Data Connectors tab, select the **Microsoft Defender for Office 365** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select **Connect**.

### Task 7: Connect the Microsoft Defender for Identity connector.

In this task, you will connect the Microsoft Defender for Identity connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Identity** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Review the Connecting Options. Don't connect. This is for informational purposes only.

### Task 8: Connect the Microsoft Defender for Endpoint connector.

In this task, you will connect the Microsoft Defender for Endpoint connector.

1. From the Data Connectors Tab, select the **Microsoft Defender for Endpoint** connector from the list.

1. Select Open connector page on the connector information blade.

1. Select **Connect**.

### Task 9: Connect the Microsoft 365 Defender connector.

In this task, you will connect the Microsoft 365 Defender connector.

1. From the Data Connectors Tab, select the **Microsoft 365 Defender** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. Select all the checkboxes for Microsoft Defender for Endpoint.

1. Select **Apply Changes**. 

### Task 3: Connect a non-Azure Windows Machine.

In this task, you will connect a non-Azure Windows virtual machine to Microsoft Sentinel.

1. Login to WIN2 virtual machine as Admin with the password: **Pa55w.rd**.  

1. Open the browser, search for, download, and install the new Microsoft Edge browser. Start the new Edge browser.

1. Open a browser and log into the Azure Portal at https://portal.azure.com with your credentials.

1. In the Search bar of the Azure Portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. Select your Microsoft Sentinel Workspace.

1. From the Data Connectors tab, select the **Security Events via Legacy Agent** connector from the list.

1. Select **Open connector page** on the connector information blade.

1. In the Select which events to stream area, select **All Events**, then select **Apply Changes**.

1. Select the **Install agent on a non-Azure Windows  Machine**.

**Note:** The instructions for Install agent on a Windows Virtual Machine and Install agent on a non-Azure Windows Machine may be reversed. The links take you to the proper location even with the reversed text.

1. Select **Download & install agent for non-Azure Windows machines**. 

1. Select the link for **Download Windows Agent (64 bit)**.

1. Run the .exe file that is downloaded and confirm and User Account Control prompt that may appear.

1. Select **Next** on the Welcome dialog.

1. Select **I Agree** on the Microsoft Software License Terms page.  On the Destination prompt select **Next**.

1. On the Agent Setup Options prompt, select **Connect the agent to Azure Log Analytics (OMS)** option, then select **Next**.

1. In the browser, copy the **Workspace ID** from the Agents Management page and paste into the Workspace ID in the dialog. 

1. In the browser, copy the **Primary key** from the Agents Management page and paste into the Primary key in the dialog. 

1. Select **Next**.

1. Select **Next** on the Microsoft Update page.

2. Then select **Install**.

### Task 4: Install and collect Sysmon logs.

In this task, you will install and collect Sysmon logs.

You should still be connected to the WIN2 virtual machine.  The following instructions will install Sysmon with the default configuration.  You should research community based configurations for Sysmon to be used on production machines.

1. In the browser, go to https://docs.microsoft.com/sysinternals/downloads/sysmon

1. Download Sysmon from the page by select **Download Sysmon**.

1. Open the downloaded file and extract the files to a new directory c:\sysmon

1. In the Windows Taskbar for WIN2 search box, enter *command*.  The search results will show command prompt app.  Right-click on the command prompt app and select **Run as Administrator**.  Confirm any User Account Control prompts that appear.

1. Enter *cd \sysmon*

1. type *notepad sysmon.xml* to create a new file.

1. Open a tab in the browser and navigate to: https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml

1. Copy the contents of that file from Github to the sysmon.xml notepad file you just created and save the file.

1. In the command prompt type the following and press enter:
    sysmon.exe -accepteula -i sysmon.xml

1. In the browser, navigate to the Azure portal at https://portal.azure.com 

1. In the Search bar of the Azure portal, type *Sentinel*, then select **Microsoft Sentinel**.

1. In Microsoft Sentinel, select **Settings** from the Configuration area and then select **Workspace settings** tab.

1. Make sure your Microsoft Sentinel Workspace is selected.

1. Select **Agents configuration** in Settings.

1. Select the **Windows Event logs** tab.

1. Select **Add windows event log** button.

1. Enter **Microsoft-Windows-Sysmon/Operational** in the Log name field.

1. Select **Apply**. --->

## Realización de ataques

### Tarea 1: Ataque a Windows configurado con Defender para punto de conexión

En esta tarea, realizarás ataques en un host con Microsoft Defender para punto de conexión configurado.

1. Inicia sesión en la máquina virtual `WIN1` como administrador con la contraseña: **Pa55w.rd**.  

1. En la búsqueda de la barra de tareas, escribe *Comando*.  El símbolo del sistema se muestra en los resultados de la búsqueda.  Haz clic con el botón derecho en el símbolo del sistema y selecciona **Ejecutar como administrador**. Confirma las indicaciones del Control de cuentas de usuario que aparezcan.

1. En el símbolo del sistema, escribe el comando en cada fila presionando la tecla Entrar después de cada fila:

    ```CommandPrompt
    cd \
    mkdir temp
    cd temp
    ```

1. Copia y ejecuta este comando:

    ```CommandPrompt
    REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "SOC Test" /t REG_SZ /F /D "C:\temp\startup.bat"
    ```

### Tarea 2: Creación de un ataque C2 (comando y control)

1. Inicia sesión en la máquina virtual `WIN1` como administrador con la contraseña: **Pa55w.rd**.  

1. En la búsqueda de la barra de tareas, escribe *Comando*.  El símbolo del sistema se muestra en los resultados de la búsqueda.  Haz clic con el botón derecho en el símbolo del sistema y selecciona **Ejecutar como administrador**. Confirma las indicaciones del Control de cuentas de usuario que aparezcan.

1. Ataque 2: Copia y ejecución de este comando:

    ```CommandPrompt
    notepad c2.ps1
    ```

Selecciona **Sí** para crear un nuevo archivo y copia el siguiente script de PowerShell en c2.ps1 y selecciona **Guardar**.

>**Nota:** pegar en la máquina virtual puede tener una longitud limitada.  Pégalo en tres secciones para asegurarte de que todo el script se pegue en la máquina virtual.  Asegúrate de que el script tiene el mismo aspecto que en estas instrucciones en el archivo c2.ps1 del Bloc de notas.

    ```PowerShell
    
    param(
        [string]$Domain = "microsoft.com",
        [string]$Subdomain = "subdomain",
        [string]$Sub2domain = "sub2domain",
        [string]$Sub3domain = "sub3domain",
        [string]$QueryType = "TXT",
            [int]$C2Interval = 8,
            [int]$C2Jitter = 20,
            [int]$RunTime = 240
    )
    
    
    $RunStart = Get-Date
    $RunEnd = $RunStart.addminutes($RunTime)
    
    $x2 = 1
    $x3 = 1 
    Do {
        $TimeNow = Get-Date
        Resolve-DnsName -type $QueryType $Subdomain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
    
        if ($x2 -eq 3 )
        {
            Resolve-DnsName -type $QueryType $Sub2domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
            
            $x2 = 1
    
        }
        else
        {
            $x2 = $x2 + 1
        }
        
        if ($x3 -eq 7 )
        {
    
            Resolve-DnsName -type $QueryType $Sub3domain".$(Get-Random -Minimum 1 -Maximum 999999)."$Domain -QuickTimeout
    
            $x3 = 1
            
        }
        else
        {
            $x3 = $x3 + 1
        }
    
    
        $Jitter = ((Get-Random -Minimum -$C2Jitter -Maximum $C2Jitter) / 100 + 1) +$C2Interval
        Start-Sleep -Seconds $Jitter
    }
    Until ($TimeNow -ge $RunEnd)
    ```

En el símbolo del sistema, escribe lo siguiente: Escribe el comando en cada fila presionando la tecla ENTRAR después de cada fila:

    ```PowerShell
    .\c2.ps1
    ```

>**Nota:** verás que se resuelven errores. Esto es lo que se espera.
Deja que este comando o script de PowerShell se ejecute en segundo plano. No cierres la ventana.  El comando debe generar entradas de registro durante algunas horas.  Puedes continuar con la siguiente tarea y los ejercicios siguientes mientras se ejecuta este script.  Los datos creados por esta tarea se usarán en el laboratorio de búsqueda de amenazas más adelante.  Este proceso no creará cantidades considerables de datos o procesamiento.

### Tarea 2: Ataque de Windows configurado con el agente de Azure Monitor (AMA)

En esta tarea, realizarás ataques en un host con el conector de eventos de seguridad y Sysmon configurado.

1. Selecciona la red virtual `AZWIN01` que has creado antes.  

1. En el menú de navegación izquierdo desplázate hacia abajo hasta **Operaciones** y selecciona **Ejecutar comando**

1. En el panel **Ejecutar comando**, selecciona **RunPowerShellScript.**

1. Copia los comandos siguientes para simular la creación de una cuenta de administrador en el formulario `PowerShell Script` y selecciona **Ejecutar**

    ```CommandPrompt
    net user theusernametoadd /add
    net user theusernametoadd ThePassword1!
    net localgroup administrators theusernametoadd /add
    ```

    >**Nota**: asegúrate de que solo haya un comando por línea y que puedes volver a ejecutar los comandos cambiando el nombre de usuario.

1. En la ventana `Output` deberías ver `The command completed successfully` tres veces
