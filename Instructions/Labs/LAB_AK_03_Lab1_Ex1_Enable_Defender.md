---
lab:
  title: "Ejercicio\_1: habilitación de Microsoft\_Defender for Cloud"
  module: Learning Path 3 - Mitigate threats using Microsoft Defender for Cloud
---

# Ruta de aprendizaje 3 - Laboratorio 1 - Ejercicio 1: habilitación de Microsoft Defender for Cloud

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex1.png)

Usted es analista de operaciones de seguridad que trabaja en una empresa que va a implementar la protección de cargas de trabajo en la nube con Microsoft Defender for Cloud.  En este laboratorio, descubrirás Microsoft Defender for Cloud.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Enable%20Microsoft%20Defender%20for%20Cloud)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: acceder a Azure Portal y configuración de una suscripción

En esta tarea, configurarás una suscripción de Azure necesaria para completar este y futuros laboratorios.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. Abre el explorador Microsoft Edge o una nueva pestaña si ya está abierta.

1. En el explorador, ve a Azure Portal en (https://portal.azure.com).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

1. En Azure Portal, escribe *Suscripción* en el cuadro de búsqueda y luego selecciona **Suscripciones**. 

1. Selecciona la suscripción *"Pase para Azure - Patrocinio"* que se muestra (o el nombre equivalente en el idioma seleccionado).

    >**Nota:** Si no aparece la suscripción, pregunta al instructor cómo crear la suscripción de Azure con tus credenciales de usuario administrador de inquilinos. **Nota:** el proceso de creación de suscripciones puede tardar hasta 10 minutos. 

1. Selecciona **Control de acceso (IAM)** y luego **Agregar asignación de roles** del cuadro * Conceder acceso a este recurso*.

1. Selecciona la pestaña **Roles de administrador con privilegios** y después, **Propietario**. Seleccione **Siguiente** para continuar.

1. En la pestaña *Miembros*, selecciona **+ Seleccionar miembros**, la cuenta **Administrador MOD** y **Seleccionar** para continuar.

    >**Nota:** Si la pestaña **Condiciones** muestra un punto rojo, seleccione **Siguiente** y, o bien seleccione **No restringido** si aparece el tipo *Delegación*, o bien seleccione **Permitir al usuario asignar todos los roles (con privilegios elevados)** aparece *Lo que el usuario puede hacer*.

1. Selecciona **Revisar y asignar** dos veces para asignar el rol de propietario a la cuenta de administrador.

>**Importante:** estos laboratorios se han diseñado para usar menos de 10 USD de servicios de Azure durante la clase.


### Tarea 2: crear un área de trabajo de Log Analytics

Ahora puedes seleccionar el área de trabajo de Log Analytics creada manualmente para usarla con Microsoft Defender for Cloud.

1. En la barra de búsqueda de Azure Portal, escribe *Áreas de trabajo* de Log Analytics y luego selecciona el mismo nombre de servicio.

1. En la barra de comandos, selecciona **+Crear**.

1. Selecciona **Crear nuevo** para el grupo de recursos.

1. Escribe *RG-Defender* y selecciona **Aceptar**.

1. En Nombre, escribe algo único como: *uniquenameDefender*.

1. Seleccione **Revisar + crear**.

1. Una vez que pase la validación del área de trabajo, selecciona **Crear**. Espera a que se provisione el área de trabajo. Esta operación puede tardar unos minutos.


### Tarea 3: habilitar Microsoft Defender for Cloud

En esta tarea, incorporarás y configurarás Microsoft Defender for Cloud.

1. En la barra de búsqueda de Azure Portal, escribe *Defender*, luego selecciona **Microsoft Defender for Cloud**.

1. En la página **Introducción**, en la pestaña **Actualizar**, asegúrate de que la suscripción está seleccionada y luego selecciona el botón ** Actualizar** situado en la parte inferior de la página. Espera a que aparezca la notificación *Inicio de prueba*, que tarda aproximadamente 2 minutos. 

    >**Sugerencia:** puedes hacer clic en el botón de campana de la barra superior para revisar las notificaciones de Azure Portal.

    >**Nota:** si ves el error *"No se ha podido iniciar la prueba de Azure Defender en la suscripción",* continúa con los pasos siguientes para habilitar todos los planes de Defender en el paso 5.

1. En el menú izquierdo de Microsoft Defender for Cloud, en Administración, selecciona **Configuración del entorno**.

1. Selecciona la suscripción **"Pase para Azure - Patrocinio"** (o el nombre equivalente en tu idioma). 

1. Revisa los recursos de Azure que ahora están protegidos con los planes de Defender for Cloud.

    >**Importante:** si todos los planes de Defender están desactivados**, selecciona **Habilitar todos los planes** y haz clic en **Guardar**. Espera a que la notificación *"Plan de recursos en la suscripción Pase para Azure se ha guardado correctamente"* aparezca.

1. Selecciona la pestaña **Configuración y supervisión** en el área Configuración (junto a Guardar).

1. Revisa las extensiones de supervisión. Incluye configuraciones para máquinas virtuales, contenedores y cuentas de almacenamiento. Cierra la página "Configuración y supervisión" seleccionando la X en la esquina superior derecha de la página.

1. Cierra la página de configuración seleccionando la "X" en la esquina superior derecha de la página para volver a la **Configuración del entorno** y selecciona la opción ">" a la izquierda de la suscripción.

1. Selecciona el área de trabajo de Log Analytics que has creado anteriormente *uniquenameDefender* para revisar las opciones y los precios disponibles.

1. Selecciona **Habilitar todos los planes** (a la derecha de Seleccionar plan de Defender) y luego, **Guardar**. Espera a que el *"plan de Microsoft Defender para workspace uniquenameDefender se ha guardado correctamente."* aparezca.

    >**Nota:** si la página no se muestra, actualiza el explorador Edge y vuelve a intentarlo.

1. Cierra la página Planes de Defender seleccionando la "X" en la esquina superior derecha de la página para volver a la **configuración del entorno**


### Tarea 4: instalar Azure Arc en un servidor local

En esta tarea, instalarás Azure Arc en un servidor local para facilitar la incorporación.

>**Importante:** Los pasos siguientes se realizan en una máquina diferente a la que trabajabas anteriormente. Busca las referencias de nombre de máquina virtual.

1. Inicia sesión en la máquina virtual **WINServer** como administrador con la contraseña: **Passw0rd!** si es necesario.  

1. Abre el explorador Microsoft Edge y ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Arc* y luego selecciona **Azure Arc**.

1. En el panel de navegación, en **Infraestructura**, selecciona **Máquinas.**

1. Selecciona **+ Agregar o crear** y después, **Agregar una máquina**.

1. Selecciona **Generar script** en la sección "Agregar un solo servidor".

    <!--- 1. Read through the *Prerequisites* tab and then select **Next** to continue.--->

1. En la página *Agregar un servidor con Azure Arc*, selecciona el grupo de recursos que has creado anteriormente en *Detalles del proyecto*. **Sugerencia: ***RG-Defender*

    >**Nota:** si todavía no has creado un grupo de recursos, abre otra pestaña y crea el grupo de recursos y vuelve a empezar.

1. Para *Región*, selecciona **(Estados Unidos) Este de EE. UU.** de la lista desplegable.

1. Revisa los *Detalles del servidor* y las opciones *Método de conectividad*. Mantén los valores predeterminados y selecciona **Siguiente** para ir a la pestaña Etiquetas.

1. Revisa las etiquetas disponibles predeterminadas. Selecciona **Siguiente** para ir a la pestaña Descargar y ejecutar script.

1. Desplázate hacia abajo y selecciona el botón **Descargar**. **Sugerencia:** si el explorador bloquea la descarga, realiza una acción en el explorador para permitirla. En el explorador Edge, selecciona el botón de puntos suspensivos (...) si es necesario y luego selecciona **Mantener**.

1. Haz clic con el botón derecho en Inicio de Windows y selecciona **Windows PowerShell (Administrador)**.

1. Escribe *Administrador* como nombre de usuario y *Passw0rd!* para "Contraseña" si recibes un mensaje de UAC.

1. Escribe: cd C:\Users\Administrator\Downloads

    >**Importante:** si no tienes este directorio, lo más probable es que estés en la máquina incorrecta. Vuelve al principio de la tarea 4, cambia a WINServer y vuelve a empezar.

1. Escribe *Set-ExecutionPolicy -ExecutionPolicy Unrestricted* y presiona Entrar.

1. Escribe **A** para Sí a todo y presiona entrar.

1. Escribe *.\OnboardingScript.ps1* y presiona entrar.  

    >**Importante:** si recibes el error *"El término .\OnboardingScript.ps1 no se reconoce..."*, asegúrate de que estás siguiendo los pasos de la tarea 4 en la máquina virtual WINServer. Otro problema podría ser que el nombre del archivo ha cambiado debido a varias descargas, busca *".\OnboardingScript (1).ps1"* u otros números de archivo en el directorio en ejecución.

1. Escribe **R** para ejecutar una vez y presiona entrar (esto puede tardar un par de minutos).

1. El proceso de configuración abrirá una nueva pestaña del explorador Edge para autenticar al agente de Azure Arc. Selecciona la cuenta de administrador, espera el mensaje "Autenticación completada" y vuelve a la ventana de Windows PowerShell.

1. Cuando finalice la instalación, vuelve a la página de Azure Portal donde has descargado el script y selecciona **Cerrar**. Cierra la página **Agregar servidores con Azure Arc** para volver a la página **Máquinas** de Azure Arc.

1. Selecciona **Actualizar** hasta que aparezca el nombre del servidor WINServer y el estado sea *Conectado*.

    >**Nota:** esto puede tardar varios minutos.


### Tarea 5: proteger un servidor local

En esta tarea, instalarás manualmente el *agente de Azure Monitor* agregando una *regla de recopilación de datos (DCR)* en la **máquina virtual WINServer**.

1. Ve a **Microsoft Defender for Cloud** y selecciona la página **Introducción** en el menú de la izquierda.

1. Seleccione la pestaña **Comenzar**.

1. Desplázate hacia abajo y selecciona **Configurar** en la sección *Agregar servidores que no son de Azure*.

1. Selecciona **Actualizar** junto al área de trabajo que has creado antes. Esto puede tardar unos minutos. Espera hasta que veas la notificación *"El plan de Microsoft Defender para el área de trabajo se uniquenameDefender se ha guardado correctamente"*.

1. Selecciona **+ Agregar servidores** junto al área de trabajo que has creado anteriormente.

1. Selecciona **Reglas de recopilación de datos**

1. Seleccione **+ Create** (+ Crear).

1. Escribe **WINServer** como Nombre de regla.

1. Selecciona la suscripción *Pase para Azure - Patrocinio* y selecciona un grupo de recursos. **Sugerencia: ***RG-Defender*

1. Puedes mantener la región *Este de EE. UU.* predeterminada o seleccionar otra ubicación preferible.

1. Selecciona el botón de radio **Windows** para *Tipo de plataforma* y selecciona **Siguiente: recursos**.

1. En la pestaña **Recursos**, selecciona **+Agregar recursos**.

1. En la página **Seleccionar un ámbito**, expande la columna *Ámbito* de **RG-Defender** (o el grupo de recursos que has creado), luego selecciona **WINServer** y selecciona **Aplicar**.

    >**Nota:** es posible que tengas que establecer el filtro de columna para *Tipo de recurso* en *Server-Azure Arc* si **no se muestra WINServer**.

1. Selecciona **Siguiente: recopilar y entregar**.

1. En la pestaña **Recopilar y entregar**, selecciona **+ Agregar origen de datos**.

1. En la página **Agregar un origen de datos**, selecciona **Contadores de rendimiento** en *Tipo de origen de datos*.

    >**Nota:** para fines de este laboratorio, puedes seleccionar *Registros de eventos de Windows*. Estas selecciones se pueden revisar más adelante.

1. Selecciona **Agregar origen de datos** y selecciona **Revisar y crear.**

1. Una vez que aparezca **Validación superada**, selecciona *Crear*.

1. La creación **Regla de recopilación de datos** inicia la instalación de la extensión *AzureMonitorWindowsAgent* en **WINServer**.

1. Cuando se complete la creación de la *Regla de recopilación de datos*, escribe **WINServer **en la barra de búsqueda *Buscar recursos, servicios y documentos* y selecciona **WINServer** en *Recursos*.

1. En **WINServer**, desplázate hacia abajo por el menú izquierdo hasta *Configuración* y *Extensiones*.

1. **AzureMonitorWindowsAgent ** debe aparecer con un *Estado* **Correcto**.

1. Puedes pasar al siguiente laboratorio y volver más adelante para revisar la sección **Inventario** de **Microsoft Defender for Cloud** para comprobar que **WINServer** está incluido.

## Continúa con el ejercicio 2
