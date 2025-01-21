---
lab:
  title: "Ejercicio\_1: habilitación de Microsoft\_Defender for Cloud"
  module: Learning Path 5 - Mitigate threats using Microsoft Defender for Cloud
---

# Ruta de aprendizaje 5 - Laboratorio 1 - Ejercicio 1: habilitación de Microsoft Defender for Cloud

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una compañía que está implementando protecciones de cargas de trabajo en la nube con Microsoft Defender for Cloud. En este laboratorio, habilitarás Microsoft Defender for Cloud.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 5 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 15 minutos

### Tarea 1: Habilitar Microsoft Defender for Cloud

En esta tarea, incorporarás y configurarás Microsoft Defender for Cloud.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.

1. En el explorador Microsoft Edge, ve a Azure Portal en <https://portal.azure.com>.
  
1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Microsoft Azure Portal, escribe *Defender*, luego selecciona **Microsoft Defender for Cloud**.

1. En el menú de navegación izquierdo de Microsoft Defender for Cloud, expande la sección *Administración* y selecciona **Configuración del entorno**.

1. Selecciona el botón **Expandir todo** para ver todas las suscripciones y recursos.

1. Selecciona la suscripción **MOC Subscription-lodxxxxxxxx** (o un nombre equivalente en tu idioma).

1. Revisa los recursos de Azure que ahora están protegidos con los planes de Defender for Cloud.

    >**Importante:** si todos los planes de Defender están *Desactivados*, selecciona **Habilitar todos los planes**. Selecciona el *Plan 1 de Microsoft Defender para API de 200 USD/mes* y, luego, **Guardar**. Selecciona **Guardar** en la parte superior de la página y espera a que la notificación *"Los planes de Defender (para la suscripción) se han guardado correctamente"* aparezca.

1. Selecciona la pestaña **Configuración y supervisión** en el área Configuración (junto a Guardar).

1. Revisa las extensiones de supervisión. Incluye configuraciones para máquinas virtuales, contenedores y cuentas de almacenamiento.

1. Selecciona el botón **Continuar** o cierra la página "Configuración y supervisión" seleccionando la "X" en la esquina superior derecha de la página.

1. Cierra la página de configuración seleccionando la "X" en la esquina superior derecha de la página para volver a la **Configuración del entorno**.

<!---1. Select the Log analytics workspace you created earlier *uniquenameDefender* to review the available options and pricing.

1. Select **Enable all plans** (to the right of Select Defender plan) and then select **Save**. Wait for the *"Microsoft Defender plan for workspace uniquenameDefender were saved successfully!"* notification to appear.

    >**Note:** If the page is not being displayed, refresh your Edge browser and try again.

1. Close the Defender plans page by selecting the 'X' on the upper right of the page to go back to the **Environment settings**. --->

### Tarea 2: Describir el panel de Microsoft Defender for Cloud

1. En la barra de búsqueda de Microsoft Azure Portal, escribe *Defender*, luego selecciona **Microsoft Defender for Cloud**.

1. En el menú de navegación izquierdo de Microsoft Defender for Cloud, en la sección *General*, selecciona **Información general**.

1. La hoja Información general proporciona una vista unificada de la posición de seguridad e incluye varios pilares de seguridad independientes de la nube, como la posición de seguridad, el cumplimiento normativo, las protecciones de cargas de trabajo, Firewall Manager, inventario e Information Protection (versión preliminar). Cada uno de estos pilares también tiene su panel dedicado, lo que permite obtener información y acciones más profundas en torno a esa vertical, lo que proporciona un acceso fácil y una mejor visibilidad para los profesionales de seguridad.

    >**Nota:** La barra de menús superior permite ver y filtrar suscripciones al seleccionar el botón Suscripciones. En este laboratorio, usaremos solo una, pero seleccionar suscripciones diferentes o adicionales ajustará la interfaz para reflejar la posición de seguridad de las suscripciones seleccionadas

1. Haz clic en el vínculo del icono **Novedades**: se abrirá una nueva pestaña con las notas de la versión más reciente, donde podrás mantenerte al día de las nuevas características, correcciones de errores y mucho más.

    >**Nota:** Los números de alto nivel en el menú superior; Esta vista te permite ver un resumen de las suscripciones, las recomendaciones activas y las alertas de seguridad junto con las cuentas en la nube conectadas.

1. En la barra de menú superior, selecciona **Subscripciones de Azure**. Esto te llevará a la configuración del entorno donde puedes seleccionar entre las suscripciones disponibles.

1. Vuelva a la página **Información general** y revisa el mosaico **Posición de seguridad**. Puedes ver tu *Puntuación de seguridad* actual junto con el número de controles y recomendaciones completadas. Al seleccionar este icono, se te redirigirá a una vista de exploración en profundidad entre suscripciones

1. En el mosaico **Cumplimiento normativo**, puedes obtener información sobre tu posición de cumplimiento en función de la evaluación continua de entornos de Azure y de nube híbrida. En este mosaico se muestran los siguientes estándares, que son el banco de pruebas de Microsoft Cloud Security y el estándar normativo de cumplimiento más bajo. Para ver los datos, primero es necesario agregar directivas de seguridad.

1. Al seleccionar este mosaico, se te redirigirá al panel **Cumplimiento normativo**, donde podrás agregar estándares adicionales y explorar los actuales.

1. Seguiremos explorando *Microsoft Defender for Cloud***Posición de seguridad** y **Cumplimiento normativo** en el próximo ejercicio.

## Continúa con el ejercicio 2
