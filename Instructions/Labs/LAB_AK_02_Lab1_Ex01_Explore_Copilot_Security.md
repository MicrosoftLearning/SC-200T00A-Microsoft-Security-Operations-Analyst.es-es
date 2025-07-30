---
lab:
  title: 'Ejercicio1: exploración de casos de uso en Microsoft Security Copilot'
  module: Learning Path 2 - Mitigate threats using Microsoft Security Copilot
---

# Ruta de aprendizaje 2 - Laboratorio 1 - Ejercicio 1: exploración de Microsoft Security Copilot

## Escenario del laboratorio

La organización para la que trabajas quiere aumentar la eficacia y las capacidades de sus analistas de operaciones de seguridad y mejorar los resultados en materia de seguridad. La oficina de CISO determinó que la implementación de Microsoft Security Copilot es un paso clave hacia ese objetivo. Como administrador de seguridad de tu organización, te han encomendado la tarea de configurar Copilot.

En este ejercicio, pasarás por la *primera experiencia de ejecución* de Microsoft Copilot Security para aprovisionar Copilot con una unidad computacional de seguridad (SCU).

>**Nota:**  El entorno de este ejercicio es una simulación generada a partir del producto. Al ser una simulación limitada, es posible que los vínculos de alguna página no estén habilitados y que no se admiten las entradas de texto que se encuentren fuera del script especificado. Se mostrará el siguiente mensaje emergente: "Esta característica no está disponible dentro de la simulación".  Cuando esto ocurra, selecciona Aceptar y continúa con los pasos del ejercicio.  

![Mensaje de error emergente](../Media/simulation-pop-up-error.png)

### Tiempo estimado para completar este laboratorio: 45 minutos

### Tarea 1: aprovisionar Microsoft Security Copilot.

En este ejercicio, ha iniciado sesión como Avery Howard y tiene el rol de administrador global en Microsoft Entra. Trabajarás tanto en Azure Portal como en Microsoft Security Copilot.

Este ejercicio debería tardar aproximadamente **15** minutos en completarse.

>**Nota:** Cuando una instrucción del laboratorio requiere que se abra un vínculo para el entorno simulado, por lo general se recomienda abrir el vínculo en una nueva ventana del explorador para poder ver las instrucciones y el entorno del ejercicio a la vez. Para ello, pulse la tecla derecha del mouse y seleccione la opción.

Para que los usuarios puedan empezar a usar Copilot, los administradores deben aprovisionar y asignar capacidad. Para aprovisionar capacidad:

- Debe tener una suscripción de Azure.
- Debes ser propietario de Azure o colaborador de Azure, en un nivel de grupo de recursos, como mínimo.

En esta tarea se le muestra el proceso de asegurarse de que tiene los permisos de rol adecuados. Para comenzar, se habilita la administración de acceso para los recursos de Azure.

Una vez que se le haya asignado el rol Administrador de acceso de usuario en Azure, puede asignar a un usuario el acceso necesario para aprovisionar SCUs para Copilot.  Solo a efectos de este ejercicio, que consiste en mostrarte los pasos necesarios, tu mismo te asignarás el acceso necesario.  Los pasos siguientes le guiarán por el proceso.

1. Para abrir el entorno simulado, seleccione este vínculo: **[Azure portal](https://app.highlights.guide/start/6d7270b9-7187-456a-ac16-97bc227d5c27?token=045faae1-1078-4eac-bf56-e12472eddaf9&link=1&azure-portal=true)**.

1. Para comenzar, habilite la administración de acceso para los recursos de Azure. Para acceder a esta configuración:
    1. En Azure Portal, seleccione **Microsoft Entra ID**.
    1. En el panel de navegación izquierdo, expanda **Administrar**.
    1. En el panel de navegación izquierdo, desplácese hacia abajo y seleccione **Propiedades**.
    1. Habilite el botón de alternancia para **Administración de acceso para los recursos de Azure** y, a continuación, seleccione **Guardar**.

1. Ahora que puede ver todos los recursos y asignar acceso en cualquier suscripción o grupo de administración del directorio, asígnese el rol Propietario para la suscripción de Azure.
    1. En el banner azul de la parte superior de la página, seleccione **Microsoft Azure** para volver a la página de aterrizaje de Azure Portal.
    1. Seleccione **Suscripciones**, a continuación, seleccione la suscripción **Woodgrove - GTP Demos (Exernal/Sponsored)**.
    1. Seleccione **Access Control (IAM)** .
    1. Seleccione **Agregar** y, a continuación, **Agregar asignación de roles**.
    1. En la pestaña Rol, seleccione **roles de administrador con privilegios**.
    1. Seleccione **Propietario** y, después, **Siguiente**.
    1. Seleccione **+ Seleccionar integrantes**.
    1. Avery Howard es el primer nombre de esta lista; seleccione **+** a la derecha del nombre.  Avery Howard aparece ahora en la lista de miembros seleccionados. Seleccione el botón **Seleccionar** y, a continuación, seleccione **Siguiente**.
    1. Seleccione **Permitir que el usuario asigne todos los roles excepto los roles de administrador con privilegios, propietario, UAA, RBAC (recomendado)**.
    1. Seleccione **Revisar y asignar** y, después, **Revisar y asignar** una última vez.

Como propietario de la suscripción de Azure, ahora podrá aprovisionar capacidad en Copilot.

#### Subtarea 1: aprovisionar la capacidad

Esta tarea le permite conocer los pasos de la capacidad de aprovisionamiento de la organización. Hay dos opciones para la capacidad de aprovisionamiento:

- Aprovisionamiento de capacidad en Security Copilot (recomendado)
- Aprovisionamiento de capacidad mediante Azure

En este ejercicio, aprovisiona la capacidad a través de Security Copilot. Cuando abra Security Copilot por primera vez, un asistente le guiará por los pasos necesarios para configurar la capacidad de su organización.

1. Para abrir el entorno simulado, seleccione este vínculo: **[Microsoft Security Copilot](https://app.highlights.guide/start/6d7270b9-7187-456a-ac16-97bc227d5c27?token=045faae1-1078-4eac-bf56-e12472eddaf9&azure-portal=true)**.

1. Siga los pasos del Asistente, seleccione **Introducción**.
1. En esta página, configurará la capacidad de seguridad. Para cualquiera de los campos que se enumeran a continuación, puede seleccionar el icono de información para obtener más información.
    1. Suscripción de Azure: En la lista desplegable, seleccione **Woodgrove - GTP Demos (Externo/Patrocinado)**.
    1. Grupo de recursos: En la lista desplegable, seleccione **RG-1**.
    1. Nombre de capacidad: Escriba un nombre de capacidad.
    1. Ubicación de evaluación del aviso [Geo]: En la lista desplegable, seleccione la región.
    1. Si lo desea, puede elegir la opción "Si esta ubicación tiene demasiado tráfico, permita que Copilot evalúe las indicaciones en cualquier lugar del mundo (recomendado para un rendimiento óptimo).
    1. La región de capacidad se establece en función de la ubicación seleccionada.
    1. Proceso de seguridad: Este campo se rellena automáticamente con las unidades de SCU mínimas necesarias, que es 1. Deja el campo con el valor de **1**.
    1. Seleccione la casilla **Reconozco que he leído, comprendido y acepto los Términos y Condiciones**.
    1. Seleccione **Continuar** en la esquina inferior derecha de la página.

1. El asistente muestra información sobre dónde se almacenarán los datos del cliente. La región que se muestra se basa en la región seleccionada en el campo Evaluación del aviso. Seleccione **Continuar**.

1. Puede seleccionar opciones para ayudar a mejorar Copilot. Puede seleccionar el botón de alternancia en función de sus preferencias.  Seleccione **Continuar**.

1. Como parte de la configuración inicial, Copilot proporciona acceso de colaborador a todos los usuarios de manera predeterminada e incluye administradores globales y administradores de seguridad como propietarios de Copilot. En el entorno de producción, puede cambiar quién tiene acceso a Copilot una vez que haya completado la configuración inicial. Seleccione **Continuar**.
1. ¡Ya está a punto! Seleccione **Finalizar**.
1. Cierre la pestaña del explorador, ya que el ejercicio siguiente usará un vínculo independiente al entorno similar al laboratorio.

### Tarea 2: explorar la experiencia independiente de Microsoft Security Copilot.

El administrador de seguridad de su organización aprovisionó Copilot. Al ser el analista sénior del equipo, el administrador le ha agregado como propietario de Copilot y le ha pedido que se familiarice con la solución.

En este ejercicio, explorarás todos los puntos de referencia clave de la página de aterrizaje de la experiencia independiente de Microsoft Security Copilot.

Has iniciado sesión como Avery Howard y tienes el rol de propietario de Copilot. Trabajará en la experiencia independiente de Microsoft Security Copilot.

Este ejercicio debería tardar aproximadamente **15** minutos en completarse.

#### Subtarea 1: explorar las opciones de menú

En esta tarea, la exploración comienza en el menú Inicio.

1. Para abrir el entorno simulado, seleccione este vínculo: **[Microsoft Security Copilot](https://app.highlights.guide/start/7608581a-ee3a-4fe0-be03-309a58b78c60?token=045faae1-1078-4eac-bf56-e12472eddaf9&azure-portal=true)**.

1. Selecciona el icono de **Menú** ![icono de menú de inicio](../Media/home-menu-icon.png), que a veces se conoce como icono de hamburguesa.

1. Seleccione **Mis sesiones** y anote las opciones disponibles.
    1. Seleccione reciente para ver las sesiones más recientes
    1. Seleccione filtrar y anote las opciones disponibles y cierre el archivador.
    1. Seleccione el icono de menú inicio para abrir el menú principal.

1. Seleccione **Biblioteca de secuencia de consultas**.
    1. Seleccione Mis secuencias de consultas. Una tarea posterior profundiza en las secuencias de consultas.
    1. Seleccione Woodgrove.
    1. Seleccione Microsoft.
    1. Seleccione filtrar para ver las opciones disponibles y, a continuación, seleccione la X para cerrar.
    1. Seleccione el icono de menú inicio para abrir el menú principal.

1. Seleccione **Configuración del propietario**. Esta configuración está disponible para usted como propietario de Copilot. Un colaborador de Copilot no tiene acceso a estas opciones de menú.
    1. Para complementos para Security Copilot, seleccione la lista desplegable Quién puede agregar y administrar sus propios complementos personalizados para ver las opciones disponibles.
    1. Seleccione la lista desplegable Quién puede agregar y administrar complementos personalizados para todos los usuarios de la organización para ver las opciones disponibles. Tenga en cuenta que esta opción está atenuada si Quién puede agregar y administrar sus propios complementos personalizados está establecido en solo propietarios.
    1. Selecciona el icono de información situado junto a "Permitir que Security Copilot acceda a los datos de los servicios de Microsoft 365".   Esta configuración debe estar habilitada si quieres usar el complemento de Microsoft Purview. Trabajará con esta configuración en un ejercicio posterior.
    1. Seleccione la lista desplegable de quién puede cargar archivos para ver las opciones disponibles.
    1. Seleccione el icono de menú inicio para abrir el menú principal.

1. Seleccione **Asignación de roles**.
    1. Seleccione Agregar miembros y, a continuación, cierre.
    1. Expanda propietario.
    1. Expanda colaborador.
    1. Seleccione el icono de menú inicio para abrir el menú principal.

1. Seleccione **Supervisión de uso**.
    1. Seleccione el filtro de fecha para ver las opciones disponibles.
    1. Seleccione el icono de menú inicio para abrir el menú principal.

1. Haga clic en **Configuración**.
    1. Seleccione las preferencias. Desplácese hacia abajo para ver las opciones disponibles.
    1. Seleccione datos y privacidad.
    1. Seleccione Acerca de.
    1. Seleccione la X para cerrar la ventana de preferencias.

1. Seleccione dónde dice **Woodgrove**, en la parte inferior izquierda del menú Inicio.
    1. Si selecciona esta opción, verá sus inquilinos. A esto se le denomina modificador de inquilino. En este caso, Woodgrove es el único inquilino disponible.
    1. Seleccione **Inicio** para volver a la página de aterrizaje.

#### Subtarea 2: Explorar el acceso a sesiones recientes

En el centro de la página de aterrizaje, hay tarjetas que representan las sesiones más recientes.

1. La tarjeta más grande es la última sesión. Al seleccionar el título de cualquier tarjeta de sesión, se le llevará a esa sesión.
1. Seleccione **Ver todas las sesiones** para ir a la página Mis sesiones.
1. Seleccione **Microsoft Copilot para seguridad**, que se encuentra junto al icono de menú Inicio, para volver a la página de aterrizaje.

#### Subtarea 3: explorar el acceso a las secuencias de consultas

La siguiente sección de la página de aterrizaje de Copilot gira en torno a las secuencias de consultas. En la página de aterrizaje se muestran los iconos de algunas secuencias de consultas de Microsoft. Aquí explorará el acceso a las secuencias de consultas y a la biblioteca de secuencias de consultas. En un ejercicio posterior, explorará la creación y ejecución de una secuencia de consultas.

1. A la derecha de donde dice "Introducción a etas secuencias de consultas" hay una tecla de flecha izquierda y derecha que le permite desplazarse por los iconos de las secuencias de consultas de Microsoft. Selecciona la **flecha derecha >**

1. Cada icono muestra el título de la secuencia de consultas, una breve descripción, el número de avisos y un icono de ejecución. Seleccione el título de cualquiera de los iconos de la secuencia de indicaciones para abrirla. Seleccione **evaluación de impacto de vulnerabilidad**, como ejemplo.
    1. La ventana de la secuencia de consultas seleccionada proporciona información, incluido quién creó la secuencia de consultas, las etiquetas, una breve descripción, las entradas necesarias para ejecutar la secuencia de consultas y una lista de las indicaciones.
    1. Anote la información sobre la secuencia de indicaciones y las opciones disponibles. Para esta simulación no puede iniciar una nueva sesión, lo hará en un ejercicio posterior. 
    1. Seleccione **X** para cerrar la ventana.

1. Seleccione **Ver la biblioteca de secuencia de consultas**.
    1. Para ver las secuencias de consultas que posee, seleccione Mis secuencias de consultas.
    1. Seleccione Woodgrove para obtener una lista de secuencias de consultas propiedad de Woodgrove, el nombre de una organización ficticia.
    1. Para ver las secuencias de consultas integradas, propias o desarrolladas por Microsoft, seleccione Microsoft.
    1. Seleccione el icono de filtro. Aquí puede filtrar en función de las etiquetas asignadas al libro. Cierre la ventana de filtro seleccionando la X en la pestaña Nuevo filtro.
    1. Seleccione **Microsoft Copilot para seguridad**, que se encuentra junto al icono de menú Inicio, para volver a la página de aterrizaje.

#### Subtarea 4: explorar las indicaciones y el icono de orígenes en la barra de indicaciones

En el centro inferior de la página se encuentra la barra de indicaciones. La barra de indicaciones incluye las indicaciones y el icono de orígenes, que usted explora en esta tarea. En los ejercicios posteriores, escribirá las entradas directamente en la barra de indicaciones.

1. En la barra de indicaciones puede seleccionar el icono de indicaciones para seleccionar una indicación integrada o una libro de indicaciones. Selecciona el **icono de indicaciones**![icono de indicaciones](../Media/prompt-icon.png).
    1. Seleccione **Ver todas las secuencias de consultas**
        1. Desplácese para ver todas las secuencias de consultas disponibles.
        1. Seleccione la **flecha atrás** junto a la barra de búsqueda para volver.
    1. Selecciona **Ver todas las funcionalidades del sistema**. En la lista se muestran todas las funcionalidades del sistema disponibles (estas funcionalidades son, en efecto, indicaciones que se pueden ejecutar). Muchas funcionalidades del sistema están asociadas a complementos específicos y, como tal, solo se mostrarán si el complemento correspondiente está habilitado.
        1. Desplácese para ver todas las secuencias de consultas disponibles.
        1. Seleccione la **flecha atrás** junto a la barra de búsqueda para volver.

1. Selecciona el **icono de orígenes**![](../Media/sources-icon.png).
    1. El icono de orígenes abre la ventana Administrar orígenes. Desde aquí, puede acceder a complementos o archivos. La pestaña **Complementos** está seleccionada de forma predeterminada.
        1. Seleccione si desea ver todos los complementos, los que están habilitados (on) o los que están deshabilitados (off).
        1. Expanda o contraiga la lista de complementos personalizados de Microsoft o de otros fabricantes.
        1. Algunos complementos requieren la configuración de parámetros. Seleccione el botón **Configurar** del complemento de Microsoft Sentinel para ver la ventana de configuración. Seleccione **cancelar** para cerrar la ventana de configuración. En un ejercicio independiente, configurará el complemento.
    1. Todavía debe estar en la ventana Administrar orígenes. Seleccione **Archivos**.
        1. Revise la descripción.
        1. Copilot puede cargar y usar archivos como knowledge base. En un ejercicio posterior, trabajará con cargas de archivos.
        1. Seleccione **X** para cerrar la ventana Administrar orígenes.

#### Subarea 5: explorar la característica de ayuda

En la esquina inferior derecha de la ventana se encuentra el icono de ayuda donde puede acceder fácilmente a la documentación y encontrar soluciones a problemas comunes. En el icono de ayuda, también puede enviar un caso de soporte técnico al equipo de soporte técnico de Microsoft si tiene los permisos de rol adecuados.

1. Seleccione el icono **Ayuda (?)**.
    1. Seleccione **Documentación**. Esta selección abre una nueva pestaña del explorador en la documentación de Microsoft Security Copilot. Vuelva a la pestaña del explorador Microsoft Security Copilot.
    1. Seleccione **Ayuda**.
        1. Cualquier persona con acceso a Security Copilot puede acceder al widget de autoayuda al seleccionar el icono de ayuda y, luego, la pestaña Ayuda. Aquí puede encontrar soluciones a problemas comunes escribiendo algo sobre el problema.
        1. Los usuarios con un rol mínimo de administrador de soporte técnico de servicio o administrador del departamento de soporte técnico pueden enviar un caso de soporte técnico al equipo de soporte técnico de Microsoft. Si tiene este rol, se muestra un icono de auriculares con micrófono. Cierre la página de contacto del soporte técnico.

### Tarea 3 : Explorar la experiencia integrada de Microsoft Security Copilot

En este ejercicio, investigará un incidente en XDR de Microsoft Defender. Como parte de la investigación, explorará las características clave de Microsoft Copilot en Microsoft Defender XDR, incluido el resumen de incidentes, el resumen del dispositivo, el análisis de scripts, etc. También dinamiza la investigación a la experiencia independiente y usa la placa de anclaje como una manera de compartir detalles de la investigación con sus compañeros.

Has iniciado sesión como Avery Howard y tienes el rol de propietario de Copilot. Trabajará en Microsoft Defender, con la nueva plataforma de operaciones de seguridad unificadas, para acceder a las funcionalidades de Copilot insertadas en XDR de Microsoft Defender. Al final del ejercicio, se dirige a la experiencia independiente de Microsoft Security Copilot.

Este ejercicio debería tardar en completarse **30** minutos aproximadamente.

#### Subtarea 1: Explorar el resumen de incidentes y respuestas guiadas

1. Para abrir el entorno simulado, seleccione este vínculo: **[Portal de Microsoft Defender](https://app.highlights.guide/start/be8a91c3-3979-4048-ad38-fd38deaf7117?token=045faae1-1078-4eac-bf56-e12472eddaf9&azure-portal=true)**.

1. Del portal de Microsoft Defender:
    1. Expanda **Investigación y respuesta**.
    1. Expande **Incidentes y alertas**.
    1. Seleccione **Incidentes**.

1. Seleccione el primer incidente de la lista, **Id. de incidente: 185856** denominado El ataque de ransomware operado por humanos se lanzó desde un recurso comprometido (interrupción del ataque).

1. Se trata de un incidente complejo. Defender XDR proporciona una gran cantidad de información, pero con 50 alertas puede ser un desafío saber dónde centrarse. En el lado derecho de la página del incidente, Copilot genera automáticamente un **resumen** de incidentes que ayuda a guiar su enfoque y respuesta. Seleccione **Ver más**.
    1. El resumen de Copilot describe cómo ha evolucionado este incidente, incluido el acceso inicial, el movimiento lateral, la recopilación, el acceso a credenciales y la filtración. Identifica dispositivos específicos e indica que la herramienta PsExec se usó para iniciar archivos ejecutables y más.
    1. Estos son todos los elementos que puede aprovechar para una investigación más detallada. Puede explorar algunos de estos en tareas posteriores.

1. Desplácese hacia abajo en el panel de Copilot y justo debajo del resumen son **respuestas guiadas**. Las respuestas guiadas recomiendan acciones que admiten la evaluación de prioridades, la contención, la investigación y la corrección.
    1. Primer elemento de la categoría de evaluación de prioridades para clasificar este incidente. Seleccione **Clasificar** para ver las opciones. Revise las respuestas guiadas en las otras categorías.
    1. Seleccione el botón **Estado** situado encima de *Resumen* y filtre por **Completado**. Cuatro actividades completadas se muestran etiquetadas como *Interrupción de ataques*. La interrupción automática de ataques está diseñada para contener ataques en curso, limitar el impacto en los recursos de una organización y proporcionar más tiempo para que los equipos de seguridad corrijan el ataque por completo.
1. Mantenga abierta la página del incidente, la usará en la siguiente tarea.

#### Subtarea 2: explorar el resumen de dispositivos e identidades

1. En la página del incidente, en la pestaña *Caso de ataque*, desplácese hacia abajo por las alertas y seleccione la alerta **Sesión de RDP sospechosa**.

1. Copilot genera automáticamente un **resumen de alertas**, que proporciona una gran cantidad de información para su posterior análisis. Por ejemplo, el resumen identifica actividades sospechosas, identifica actividades de recopilación de datos, acceso a credenciales, malware, actividades de detección, etc.

1. Hay mucha información en la página, por lo que para obtener una mejor vista de esta alerta, seleccione **Abrir página de alertas**. Se encuentra en el tercer panel de la página de alertas, junto al gráfico de incidentes y debajo del título de la alerta.

1. En la parte superior de la página, es la tarjeta para el dispositivo **parkcity-win10v**. Seleccione los puntos suspensivos y anote las opciones. Seleccione **Resumir**. Copilot genera un **resumen del dispositivo**. No vale la pena que haya muchas maneras de acceder al resumen del dispositivo y esta es solo un método práctico. El resumen muestra que el dispositivo es una máquina virtual, identifica al propietario del dispositivo, muestra su estado de cumplimiento con las directivas de Intune y mucho más.

1. Junto a la tarjeta del dispositivo es una tarjeta para el propietario del dispositivo. Seleccione **PARKCITY\jonaw**. El tercer panel de la página se actualiza de mostrar los detalles de la alerta para proporcionar información sobre el usuario Jonathan Wolcott, un ejecutivo de cuenta, cuyo riesgo de Microsoft Entra ID y gravedad de riesgo interno se clasifican como altos. Esto no es sorprendente dado lo que ha aprendido del incidente de Copilot y los resúmenes de alertas. Selecciona los puntos suspensivos y, después, selecciona **Resumir** para obtener un resumen de identidades generado por Copilot.

1. Mantén abierta la página de alertas, la utilizarás en la siguiente tarea.

#### Subarea 3: explorar el análisis de scripts

1. Vamos a centrarnos en la historia de alertas. Selecciona **Maximizar ![icono de maximizar](../Media/maximize-icon.png)**, situado en el panel principal de la alerta, justo debajo de la tarjeta que lleva la etiqueta "partycity\jonaw" para obtener una mejor vista del árbol de procesos. Desde la vista maximizada, comienza a obtener una vista más clara de cómo llegó a ser este incidente. Muchos elementos de línea indican que powershell.exe ejecutaron un script. Dado que el usuario Jonathan Wolcott es un ejecutivo de cuentas, es razonable suponer que la ejecución de scripts de PowerShell no es algo que es probable que este usuario esté haciendo con regularidad.

1. Expanda la primera instancia de **powershell.exe ejecutar un script**, es la que muestra la marca de tiempo de 4:57:11 a. m. Copilot tiene la capacidad de analizar scripts. Seleccione **Analizar**.
    1. Copilot genera un análisis del script y sugiere que podría ser un intento de suplantación de identidad (phishing) o se usa para entregar una vulnerabilidad de seguridad basada en web.
    1. Seleccione **Mostrar código**. El código muestra una dirección URL desfangada.

1. Hay otros elementos que indican powershell.exe ejecutar un script. Expanda la etiqueta **powershell.exe -EncodedCommand...**. El script original estaba codificado en base 64, pero Defender lo ha descodificado. Para la versión descodificada, seleccione **Analizar**. El análisis resalta la sofisticación del script usado en este ataque.

1. En el análisis de script de Copilot, hay botones para Mostrar código y Mostrar técnicas de MITRE.

1. Seleccione el botón **Mostrar técnicas de MITRE** y seleccione el vínculo etiquetado: T1105: Transferencia de herramientas de entrada

1. Se abre la página del sitio *MITRE | ATT&CK* en la que se describe la técnica con detalle.

1. Cierre la página del artículo de alertas seleccionando la **X** (la X situada a la izquierda del panel de Copilot). Ahora use la ruta de navegación para volver al incidente. Seleccione **El ataque de ransomware operado por humanos se lanzó desde un activo comprometido (interrupción del ataque)**.

#### Subtarea 4: explorar el análisis de archivos

1. Vuelve a la página del incidente. En el resumen de la alerta, Copilot ha identificado el archivo mimikatz.exe, que está asociado con el malware "Mimikatz". Puede usar la funcionalidad de análisis de archivos en XDR de Defender para ver qué otras conclusiones puede obtener. Hay varias maneras de acceder a los archivos. En la parte superior de la página, seleccione la pestaña **Evidencia y respuesta**.

1. En el lado izquierdo de la pantalla, seleccione **Archivos**.
1. Seleccione el primer elemento de la lista con la entidad denominada **mimikatz.exe**.
1. En la ventana que se abre, seleccione **Abrir página de archivo**.
1. Seleccione el icono de Copilot (si el análisis de archivos no se abre automáticamente) y Copilot genera un análisis de archivos.
1. Revise el análisis detallado de archivos que genera Copilot.
1. Cierre la página Archivo y use la ruta de navegación para volver al incidente. Seleccione **El ataque de ransomware operado por humanos se lanzó desde un activo comprometido (interrupción del ataque)**.

#### Subtarea 5: dinamización de la experiencia independiente

Esta tarea es compleja y requiere la participación de más analistas de alto nivel. En esta tarea, dinamizará la investigación y ejecutará el libro de mensajes de incidentes de Defender para que los demás analistas tengan un inicio en ejecución en la investigación. Ancla las respuestas al panel de anclaje y genera un vínculo a esta investigación que puede compartir con miembros más avanzados del equipo para ayudar a investigar.

1. Vuelva a la página del incidente seleccionando la pestaña **Historia de ataque** en la parte superior de la página.

1. Seleccione los puntos suspensivos junto al resumen de incidentes de Copilot y seleccione **Abrir en Security Copilot**.

1. Copilot se abre en la experiencia independiente y muestra el resumen de incidentes. También puede ejecutar más mensajes. En este caso, ejecutará la secuencia de indicaciones para un incidente. Selecciona el **icono de indicación**![icono de indicación](../Media/prompt-icon.png). 
    1. Seleccione **Ver todos los mensajes**.
    1. Seleccione **Investigación de incidentes**de Microsoft 365 Defender.
    1. La página del libro de mensajes se abre y solicita el identificador de incidente de Defender. Escriba **185856** y, después, seleccione **Enviar**.
    1. Revise la información que se proporciona. Al dinamizar la experiencia independiente y ejecutar el promptbook, la investigación puede invocar funcionalidades desde una solución de seguridad de conjunto más amplia, más allá de solo Defender XDR, en función de los complementos habilitados.

1. Selecciona el **icono de cuadro ![icono de cuadro](../Media/box-icon.png)** situado junto al icono de anclaje para seleccionar todas las indicaciones y las respuestas correspondientes y, después, selecciona el **icono de anclaje![icono de anclaje](../Media/pin-icon.png)** para guardar esas respuestas en el panel de anclaje.

1. El panel de anclaje se abre automáticamente. La placa de anclaje contiene los mensajes y respuestas guardados, junto con un resumen de cada uno. Para abrir y cerrar el panel de anclaje, selecciona el **icono de panel de anclaje ![icono de panel de anclaje](../Media/pinboard-icon.png)**.

1. En la parte superior de la página, seleccione **Compartir** para ver las opciones. Al compartir el incidente a través de un vínculo o correo electrónico, las personas de su organización con acceso a Copilot pueden ver esta sesión. Cierre la ventana seleccionando la **X**.

#### Subtarea 6: Creación y ejecución de una consulta de KQL

A continuación, se usará Copilot para crear una consulta de KQL (Lenguaje de consulta Kusto) para usarla con la búsqueda avanzada de amenazas en Defender XDR.

1. Mientras todavía está en Security Copilot independiente, escriba la siguiente indicación en el formulario de indicación: *En función de este incidente, cree una consulta para buscar proactivamente este tipo de ataque de malware. Use el espacio de trabajo woodgrove-loganalytics.*

1. Presione el icono Enviar mensaje para ejecutar el mensaje.
Copilot elige Lenguaje natural para KQL para la búsqueda avanzada de amenazas.

1. Copilot genera una consulta KQL y una respuesta:

    1. Lea la explicación de la consulta Kusto.

    1. Revise el desglose de la consulta Kusto. Esto es muy útil si acaba de empezar a trabajar con KQL.

1. Copie la consulta KQL que ha generado Copilot y vuelva al portal de Defender XDR.
***Se recomienda copiar la consulta en el Bloc de notas u otro editor primero para reducir los problemas de formato***.

1. Defender XDR todavía debe tener abierta la sección Investigaciones y respuesta. Seleccione **Búsqueda** y después **Búsqueda avanzada de amenazas** en el menú de navegación.

1. En Búsqueda avanzada de amenazas, seleccione **Nueva consulta +** para abrir una nueva ventana y pegue la consulta KQL generada por Copilot en el formulario.
***Se recomienda copiar la consulta en el Bloc de notas u otro editor primero para reducir los problemas de formato***.

1. Después de ejecutar la consulta KQL, puede volver a Copilot para refinar la consulta o seleccionar el icono de Copilot en la página Consulta de búsqueda avanzada de amenazas para ajustar las consultas.

1. Ahora puede cerrar la pestaña del navegador para salir de la simulación.

## Resumen y recursos adicionales

En este ejercicio, has explorado la primera experiencia de ejecución de Microsoft Security Copilot, has aprovisionado la capacidad y has explorado las experiencias independientes e integradas de Copilot. Has investigado un incidente en Microsoft Defender XDR, has explorado el resumen de incidentes, el resumen de dispositivos, el análisis de scripts, etc. También has dinamizado la investigación hacia la experiencia independiente y has usado el panel de anclaje como una manera de compartir detalles de la investigación con tus compañeros.

Para ejecutar simulaciones adicionales de casos de uso de Microsoft Security Copilot, ve a [Explorar simulaciones de casos de uso de Microsoft Security Copilot.](/training/modules/security-copilot-exercises/)
