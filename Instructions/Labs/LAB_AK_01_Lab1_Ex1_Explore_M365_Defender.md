---
lab:
  title: "Ejercicio 1: exploración de Microsoft\_365\_Defender"
  module: Learning Path 1 - Mitigate threats using Microsoft 365 Defender
---

# Ruta de aprendizaje 1 - Laboratorio 1 - Ejercicio 1: exploración de Microsoft 365 Defender

## Escenario del laboratorio

![M365 Defender](../Media/SC-200-Lab_M1_L1_Ex1.png)

Eres analista de operaciones de seguridad y trabajas en una empresa que está implementando Microsoft 365 Defender para puntos de conexión. Empieza asignando directivas de seguridad preestablecidas en EOP y Microsoft Defender para Office 365.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Explore%20Microsoft%20365%20Defender)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos.

>**Nota:** **Inquilinos de WWL: términos de uso** Si, como parte de un curso impartido por un instructor, se te facilita un inquilino, ten en cuenta que el inquilino está a tu disposición con el fin de apoyar los laboratorios prácticos en los cursos dirigidos por un instructor. Los inquilinos no deben compartirse ni usarse para otros fines que no sean los de los laboratorios prácticos. El inquilino usado en este curso es un inquilino de prueba y no se puede usar ni tener acceso a él después de que la clase haya terminado y no sea apto para la extensión. Los inquilinos no se deben convertir a suscripciones de pago. Los inquilinos obtenidos como parte de este curso siguen siendo propiedad de Microsoft Corporation y nos reservamos el derecho de acceso y recuperación en cualquier momento. 


### Tarea 1: obtener tus credenciales de Microsoft 365

Una vez que inicies el laboratorio, se pondrá a tu disposición un inquilino de evaluación gratuita para acceder al entorno de laboratorio virtual de Microsoft. A este inquilino se le asignará automáticamente un nombre de usuario y una contraseña únicos. Debes recuperar este nombre de usuario y contraseña para poder iniciar sesión en Azure y Microsoft 365 en el entorno de laboratorio virtual de Microsoft. 

Dado que los asociados de aprendizaje pueden ofrecer este curso mediante cualquiera de varios proveedores de hospedaje de laboratorio autorizado (ALH), los pasos reales necesarios para recuperar el identificador de inquilino asociado al inquilino pueden variar según el proveedor de hospedaje de laboratorio. Por lo tanto, tu instructor te dará las instrucciones necesarias para recuperar esta información para tu curso. La información que debes tener en cuenta para uso posterior incluye:

- **Id. de sufijo de inquilino.** Este identificador es para las cuentas de onmicrosoft.com que usarás para iniciar sesión en Microsoft 365 en todos los laboratorios. Se trata del formato **{username}@ZZZZZZ.onmicrosoft.com**, donde ZZZZZZ es el identificador de sufijo de inquilino único que ha facilitado el proveedor de hospedaje de laboratorio. Anota este valor ZZZZZZ para más adelante. Cuando cualquiera de los pasos del laboratorio te dirija a iniciar sesión en los portales de Microsoft 365, debes escribir el valor ZZZZZZ que obtuviste aquí.
- **Contraseña de inquilino.** Escribe la contraseña de administrador que te ha facilitado tu proveedor de hospedaje de laboratorio.

### Tarea 2: aplicar directivas de seguridad preestablecidas en Microsoft Defender para Office 365

En esta tarea, asignarás directivas de seguridad preestablecidas para Exchange Online Protection (EOP) y Microsoft Defender para Office 365 en el portal de seguridad de Microsoft 365.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. Abre el explorador Microsoft Edge.

1. En el explorador Edge, ve al portal de Microsoft 365 Defender en (https://security.microsoft.com).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino para el nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que facilita el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

    >**Nota:** si recibes un mensaje "La operación no se ha podido completar. Inténtelo de nuevo más tarde. Si el persiste el problema, ponte en contacto con el Soporte técnico de Microsoft." y haz clic en **Aceptar** para continuar.  

1. Si se muestra, cierra la ventana emergente de introducción a Microsoft 365 Defender. **Sugerencia:** más adelante en este laboratorio, tendrás que esperar hasta que se aprovisione el área de trabajo de Defender. Puede aprovechar este tiempo para tomar las visitas guiadas y obtener más información sobre Microsoft 365 Defender.

1. En el menú de navegación, en el área *Correo electrónico y colaboración*, selecciona **Directivas y reglas**.

1. En el panel *Directiva y reglas*, selecciona **Directivas de amenazas**.

1. En el panel *Directivas de amenazas*, selecciona **Directivas de seguridad preestablecidas**.

    >**Nota:** si recibes el mensaje *"Error de cliente - Error al obtener la regla bip",* selecciona **Aceptar** para continuar. El error se debe al estado de hidratación del inquilino en Office 365, que no está habilitado de forma predeterminada.

    >**Nota:** si recibes el mensaje *"Error de cliente: error al recuperar directivas de seguridad preestablecidas. Vuelve a intentarlo más tarde".* Selecciona **Aceptar** para continuar. Actualiza el explorador mediante **Ctrl+F5**.

1. En la página *emergente* **Información sobre las directivas de seguridad preestablecidas**, selecciona **Cerrar**.

1. En *Protección estándar*, selecciona **Administrar configuración de protección**. **Sugerencia:** si ves esta opción atenuada, actualiza el explorador mediante **Ctrl+F5**.

1. En la sección *Aplicar protección de Exchange Online*, selecciona **Destinatarios específicos** y en **Dominios**, empieza a escribir el nombre de dominio del inquilino, selecciónalo y luego selecciona **Siguiente**.

    >**Sugerencia:** el nombre de dominio del inquilino es el mismo que tienes para tu cuenta de administrador. Podría ser algo parecido a *WWLx####.onmicrosoft.com*. Ten en cuenta que esta configuración aplica directivas para antispam, filtro de correo no deseado saliente, antimalware, protección contra suplantación de identidad.

1. En la sección *Aplicar protección de Defender para Office 365*, aplica la misma configuración que el paso anterior y selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para protección contra suplantación de identidad, datos adjuntos seguros, vínculos seguros.

1. En la sección *Protección contra suplantación*, selecciona **Siguiente** cuatro veces (4x) para continuar.

1. En la sección *Modo de directiva*, asegúrate de que está seleccionado el botón de selección **Activar la directiva al finalizar** y luego selecciona **Siguiente**.

1. Lee el contenido en *Revise y confirme los cambios* y selecciona **Confirmar** para aplicar los cambios y luego selecciona **Listo** para finalizar.

    >**Nota:** si recibes el mensaje *"El URI https://outlook.office365.com/psws/service.svc/AntiPhishPolicy" no es válido para la operación PUT. El URI debe dirigir a un único recurso para las operaciones PUT".* simplemente selecciona **Aceptar** y **Cancelar** para volver a la página principal. Verás que la opción *La protección estándar está activada* está habilitada.

1. En *Protección estricta*, selecciona **Administrar la configuración de protección**. **Sugerencia:** *protección estricta* se encuentra en "Correo electrónico y colaboración - Directivas y reglas - Directivas de amenazas - Directivas de seguridad preestablecidas".

1. En *Aplicar Exchange Online Protection*, selecciona **Destinatarios específicos** y en **Grupos** empieza a escribir **Liderazgo**, selecciónalo y luego selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para antispam, filtro de correo no deseado saliente, antimalware, protección contra suplantación de identidad.

1. En la sección *Aplicar protección de Defender para Office 365*, aplica la misma configuración que el paso anterior y selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para protección contra suplantación de identidad, datos adjuntos seguros, vínculos seguros.

1. En la sección *Protección contra suplantación*, selecciona **Siguiente** cuatro veces (4x) para continuar.

1. En la sección *Modo de directiva*, asegúrate de que está seleccionado el botón de selección **Activar la directiva al finalizar** y luego selecciona **Siguiente**.

1. Lee el contenido en *Revise y confirme los cambios* y selecciona **Confirmar** para aplicar los cambios y luego selecciona **Listo** para finalizar.

    >**Nota:** si recibes el mensaje *"El URI https://outlook.office365.com/psws/service.svc/AntiPhishPolicy" no es válido para la operación PUT. El URI debe dirigir a un único recurso para las operaciones PUT".* simplemente selecciona **Aceptar** y **Cancelar** para volver a la página principal. Verás que la opción *Protección estricta está activada* está habilitada.

### Tarea 3: preparar el área de trabajo de Microsoft 365 Defender

1. En el portal de **Microsoft 365 Defender**, en el menú de navegación, selecciona **Inicio** a la izquierda.

    >**Nota:** es posible que tengas que desplazarte hasta la parte superior del menú.

1. En la página del portal **Inicio**, se muestra **Bienvenido a Microsoft 365 Defender**.

1. Desplázate hacia abajo por los iconos hasta que encuentres el icono con la etiqueta **Microsoft 365 Defender** con el mensaje, **Activar Microsoft 365 Defender.**

    >**Sugerencia:** debe estar en la parte inferior derecha de los iconos.

1. Selecciona el botón que indica **Activar nuevas características.**

1. Verás mensajes que indican *cargando e inicializando* brevemente en la parte superior de la página y luego verás una imagen de una taza de café y un mensaje que indica: **estamos preparando nuevos espacios para tus datos y conectándolos.** Este proceso puede tardar 5 minutos aproximadamente en finalizar. *Deja abierta la página y asegúrate de que finaliza, ya que es necesario para el siguiente laboratorio.*

    >**Nota:** si no aparece el mensaje " Estamos preparando nuevos espacios para tus datos y conectándolos" o se abre la página "Configuración > Cuenta de microsoft 365 Defender >", pero ves el mensaje "No se ha podido cargar la ubicación de almacenamiento de datos. Vuelve a intentarlo más tarde", selecciona "Configuración del servicio de alertas" en el menú "General" o ve al menú de navegación. Desplázate hacia abajo hasta la sección "Recursos" y selecciona "Dispositivos".

1. Cuando el nuevo espacio se complete correctamente, verás la configuración general de Microsoft 365 Defender para la cuenta, las notificaciones por correo electrónico, la configuración del servicio de alertas, los permisos y los roles y la API de streaming. También verás **Características en vista previa** activadas.

## Has completado el laboratorio
