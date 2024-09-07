# Módulo 1: mitigación de amenazas con Microsoft 365 Defender

**Nota**: la finalización correcta de esta demostración depende de completar todos los pasos del [documento de requisitos previos](00-prerequisites.md).

## Uso del portal de Microsoft Defender

En esta tarea, te familiarizarás con las funcionalidades del portal de Microsoft 365 Defender.

- Inicio (Panel)
- Incidentes y alertas
- Búsqueda
- Centro de actividades
- Análisis de amenazas
- Puntuación segura
- Puntos de conexión
- Administración de vulnerabilidades
- Correo electrónico y colaboración
- Aplicaciones de nube
- Informes
- Configuración
- Permisos

1. Si aún no estás en el Centro de seguridad de Microsoft Defender del explorador, ve al Centro de seguridad de Microsoft Defender en (https://security.microsoft.com) con la sesión iniciada como Administrador para el inquilino.

1. En el panel **Inicio**, puedes obtener una perspectiva general del estado seguro. Puedes personalizar la vista **agregando tarjetas** o quitándolas. Para quitar una tarjeta, selecciona los puntos suspensivos (...) de una tarjeta.
1. Luego, selecciona **Incidentes y alertas**. Esto expandirá las opciones de menú siguientes. Aquí es donde se realizan investigaciones.
1. Haz lo mismo con **Búsqueda** para exponer la página **Consulta de búsqueda avanzada**. 
    1. Puedes ejecutar consultas KQL aquí.
1. La selección de **acciones y envíos** expondrá el **Centro de actividades** y **Envíos**
1. Selecciona **Inteligencia sobre amenazas** y luego, **Análisis de amenazas**. En esta página se proporciona información sobre Vulnerabilidades y riesgos comunes (CVE) que necesitas para realizar el seguimiento1. Selecciona la **Puntuación de seguridad** y explora las pestañas. Echa un vistazo a **las acciones recomendadas** aquí.
1. Selecciona **Recursos** y **Dispositivos** para tu `Device Inventory`. Puedes incorporar dispositivos aquí o trabajar con un inventario existente.
1. En `Assets` también se encuentran **Identidades**
1. En la sección **Puntos de conexión** se encuentra **Administración de vulnerabilidades**. `Vulnerability management` tiene un `Dashboard` donde puedes ver tu puntuación de exposición.
1. Otra funcionalidad dentro de **Puntos de conexión** es **Evaluaciones y simulaciones**. El **laboratorio de evaluación** te permite configurar dispositivos aislados para explorar malware.
1. En la sección **Correo electrónico y colaboración** se encuentran las funciones de `Defender for Office 365`. **Investigaciones** es donde se ven los resultados de las investigaciones sobre amenazas Investigación y respuesta automatizadas (AIR).
1. Además, en **Correo electrónico y colaboración** están las **Directivas y reglas**. Configurarás las directivas sobre **Amenaza y alerta** aquí.
1. Desplázate hacia abajo hasta **Aplicaciones en la nube**. Se trata de la sección del servicio **Microsoft Defender for Cloud Apps**. En **Gobernanza de aplicaciones** es donde se establecen directivas de aplicaciones.
1. En la siguiente sección puedes encontrar **Informes** para los servicios de Microsoft 365 Defender. En **AUdit** puedes habilitar la grabación de la actividad de administración de usuarios y **Permisos** y **Configuración**.
1. En **Permisos**, puedes configurar roles de **Azure AD** y **Punto de conexión**.
1. **Configuración** es donde se especifica la configuración general, como la zona horaria y las notificaciones por correo electrónico, además de la configuración pormenorizada para puntos de conexión, identidades y detección de dispositivos.
1. Selecciona **Configuración** y luego **Puntos de conexión**. Puedes ver y agregar **Licencias** aquí. Luego selecciona **Características avanzadas**. Desplázate por la lista de características, pero no realices ningún cambio ahora.
1. Por último, deja **Configuración** y, en la lista de menús principal, selecciona **Más recursos**. Deberías ver tarjetas o iconos con vínculos para **Cumplimiento de Microsoft Purview**, **Azure Active Directory** y otras funcionalidades que no forman parte directamente de **Microsoft 365 Defender**. Selecciona el botón **Abrir** para **Cumplimiento de Microsoft Purview**. Se abrirá el portal de cumplimiento.

## Conexión de Microsoft Sentinel y Microsoft Defender XDR

En esta tarea, conectarás un área de trabajo de Microsoft Sentinel a Microsoft Defender XDR.

**Nota:** Existen diferencias de funcionalidad entre el portal de Microsoft Defender XDR y el portal de Microsoft Sentinel. La experiencia y los pasos de la interfaz de usuario pueden diferir de las instrucciones del laboratorio.

1. Inicia sesión en la máquina virtual **WIN1** como *Administrador* con la contraseña: **Pa55w.rd**.  

1. Abre el explorador Microsoft Edge.

1. En el navegador Edge, ve al portal de Microsoft Defender XDR en <https://security.microsoft.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

    >**Sugerencia:** la cuenta de correo electrónico del inquilino del administrador y la contraseña se pueden encontrar en la pestaña Recursos.

1. En la pantalla **Inicio** del portal de **Defender XDR**, deberías ver un banner en la parte superior con el mensaje *Obtener SIEM y XDR en un solo lugar*. Selecciona el botón **Conectar un área de trabajo**.

1. En la página *Elegir un área de trabajo*, selecciona el área de trabajo de **Microsoft Sentinel** que creaste anteriormente.

    >**Sugerencia:** debes tener un nombre como *uniquenameDefender*.

1. Haz clic en el botón **Siguiente**.

    >**Nota:** si el botón *Siguiente* está deshabilitado o atenuado, y ves un mensaje de error que indica que el área de trabajo de Microsoft Sentinel *no está incorporada* a Defender XDR, intenta actualizar la página del portal de Defender XDR, ya que puede tardar entre 5 y 10 minutos en sincronizarse.

1. En la página *Revisar cambios*, comprueba que la selección del *Área de trabajo* sea correcta y revisa los elementos con viñetas en la sección *Qué esperar cuando el área de trabajo esté conectada*. Selecciona el botón **Conectar**.

1. Deberías ver un mensaje *Conectar el área de trabajo* seguido de un mensaje *Área de trabajo conectada correctamente*.

1. Selecciona el botón **Cerrar**.

1. En la pantalla **Inicio** del portal de **Defender XDR**, deberías ver un banner en la parte superior con el mensaje, *Su SIEM unificado y XDR están listos*. Selecciona el botón **Iniciar búsqueda**.

1. En *Búsqueda avanzada*, deberías ver un mensaje para "Explorar el contenido de Sentinel". En el panel de menús izquierdo, observa las tablas, funciones y consultas de *Microsoft Sentinel* en las pestañas correspondientes.

1. Expande el panel de menús principal izquierdo si se contrae y expande los nuevos elementos de menú de **Microsoft Sentinel**. Deberías ver las selecciones *Administración de amenazas*, *Administración de contenido* y *Configuración*.

 >**Nota:** la sincronización entre Microsoft Sentinel y Microsoft Defender XDR puede tardar unos minutos en completarse, por lo que es posible que no veas todos los *Conectores de datos* instalados, por ejemplo.

## Has completado el laboratorio.