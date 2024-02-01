---
lab:
  title: "Ejercicio 2: mitigación de amenazas con Microsoft\_Defender\_for\_Cloud"
  module: Learning Path 3 - Mitigate threats using Microsoft Defender for Cloud
---

# Ruta de aprendizaje 3 - Laboratorio 1 - Ejercicio 2: mitigación de amenazas mediante Microsoft Defender for Cloud

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod3_L1_Ex2.png)

Supongamos que eres un analista de operaciones de seguridad que trabaja en una empresa en la que se ha implementado Microsoft Defender para puntos de conexión. Debes responder a las recomendaciones y alertas de seguridad que ha generado Microsoft Defender for Cloud.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Mitigate%20threats%20using%20Microsoft%20Defender%20for%20Cloud)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: explorar el cumplimiento normativo

En esta tarea, revisarás la configuración del cumplimiento en Microsoft Defender for Cloud. 

>**Importante:** Los pasos siguientes se realizan en una máquina diferente a la que trabajabas anteriormente. Busca las referencias de nombre de máquina virtual.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, abre Azure Portal en (https://portal.azure.com).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Defender*, luego selecciona **Microsoft Defender for Cloud**.

1. En *Seguridad en la nube*, selecciona **Cumplimiento de regulaciones** en el menú del portal.

1. Selecciona **Administrar directivas de cumplimiento** en la barra de herramientas.

1. Seleccione su suscripción.

    >**Sugerencia:** seleccione **Expandir todo** para buscar la suscripción si es una jerarquía de grupos de administración.

1. En *Configuración*, seleccione **Directiva de seguridad** en el menú del portal.

1. Desplácese hacia abajo y revise los "Estándares de seguridad" disponibles de forma predeterminada.

1. Utilice el cuadro de búsqueda para buscar *ISO 27001:2013*.

1. Seleccione y mueva el control deslizante **Estado** a la derecha de *ISO 27001:2013* a **Activado**.

    >**Nota:** algunos estándares requieren asignar una iniciativa de Azure Policy.

1. Seleccione **Actualizar** en el menú de la página para confirmar que *ISO 27001:2013* está *Activado* para la suscripción.

1. Cierre la página *Directivas de seguridad* seleccionando la "X" en la esquina superior derecha de la página para volver a la **configuración del entorno**.

    >**Nota:** es posible que quieras volver más adelante al *Cumplimiento normativo* para revisar los nuevos controles y recomendaciones estándar.

### Tarea 2: explorar la posición de seguridad y las recomendaciones

En esta tarea, revisarás la administración de la posición de seguridad en la nube.  La información de puntuación de seguridad puede tardar 24 horas en recalcularse. Se recomienda volver a realizar esta tarea en 24 horas.

1. En *Seguridad en la nube*, selecciona **Posición de seguridad** en el menú del portal.

1. La puntuación de seguridad probablemente mostrará *N/A* hasta que se calcule la puntuación.

1. En *General*, selecciona **Recomendaciones** en el menú del portal.

1. Explora las recomendaciones dadas para tu suscripción y WINServer (Arc Server).

1. Selecciona cualquier recomendación en la que el estado no sea *"Completado"* para WINServer.

1. Lee la recomendación y desplázate hacia abajo para **seleccionar** la casilla WINServer. **Sugerencia:** es posible que tengas que seleccionar **Recursos afectados** para mostrarlos.

1. Selecciona **Asignar propietarios** y luego **Seleccionar propietario**.

1. En el cuadro *Dirección de correo electrónico*, anota el correo electrónico del administrador. **Sugerencia:** puedes copiarlo en las instrucciones de la pestaña *Recursos*.

1. Selecciona **Atrás**, cambia la *Fecha de vencimiento* por tu preferencia y haz clic en **Guardar**.

    >**Nota:** si ves el error *No se han podido crear asignaciones solicitadas*, vuelve a intentarlo más tarde.

1. Cierra la página de recomendación seleccionando la 'X' en la esquina superior derecha de la ventana.


### Tarea 3: mitigar alertas de seguridad

En esta tarea, cargarás alertas de seguridad de ejemplo y revisarás los detalles de la alerta.


1. En *General*, selecciona **Alertas de seguridad** en el menú del portal.

1. En la barra de comandos, selecciona **Alertas de ejemplo**. **Sugerencia:** es posible que tengas que seleccionar el botón de puntos suspensivos (...) de la barra de comandos.

1. En el panel Crear alertas de ejemplo (versión preliminar), asegúrate de que la suscripción esté seleccionada y de que todas las alertas de ejemplo estén seleccionadas en el área *Planes de Defender for Cloud*.

1. Seleccione **Create sample alerts** (Crear alertas de ejemplo).  

    >**Nota:** este proceso de creación de alertas de ejemplo puede tardar unos minutos en completarse; espera la notificación *"Alertas de ejemplo creadas correctamente"*. 

1. Una vez completado, selecciona **Actualizar** para ver las alertas en el área *Alertas de seguridad*.

1. Para las alertas que han llamado tu atención, realiza las siguientes acciones:

    - Selecciona la alerta. Debería aparecer información sobre ella. Seleccione **View full details** (Ver detalles completos).

    - Revisa y lee la pestaña *Detalles de alerta*.

    - Selecciona la pestaña **Realizar acción** o selecciona el botón **Siguiente: realizar acción** al final de la página.

    - Revisa la información *Realizar acción*. Examina las secciones disponibles para tomar medidas en función del tipo de alerta: Inspeccionar el contexto de recursos, Mitigar la amenaza, Evitar ataques futuros, Desencadenar respuesta automatizada y Suprimir alertas similares.

## Has completado el laboratorio.
