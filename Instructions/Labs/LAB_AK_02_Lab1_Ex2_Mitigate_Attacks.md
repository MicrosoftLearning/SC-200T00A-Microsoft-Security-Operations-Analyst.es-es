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

1. Si todavía no estás en el portal de Microsoft 365 Defender en el explorador Microsoft Edge, ve a (https://security.microsoft.com) e inicia sesión como administrador para el inquilino.

1. En el menú de la izquierda, en el área **Recursos**, selecciona **Dispositivos**. Espere hasta que WIN1 aparezca en la página Dispositivos antes de continuar. De lo contrario, es posible que tengas que repetir esta tarea para ver las alertas que se generarán más adelante.

    >**Nota:** Si has completado el proceso de incorporación y no ves dispositivos en la lista Dispositivos después de una hora, podría indicar un problema de incorporación o conectividad.

1. Selecciona **Configuración** en la barra de menús de la izquierda. Después, en la página Configuración, selecciona **Puntos de conexión**.

1. Selecciona **Incorporación** en la sección Administración de dispositivos y asegúrate de que *"Windows 10 y 11"* esté seleccionado como sistema operativo. El mensaje *"Primer dispositivo incorporado"* ahora muestra *Completado*.

1. Desplázate hacia abajo y, en la sección *"2. Ejecutar una prueba de detección"*, copia el script de prueba de detección seleccionando el botón **Copiar**.  

1. En la barra de búsqueda de Windows de la máquina virtual WIN1, escribe **CMD** y elige **Ejecutar como administrador** en el panel derecho de la aplicación de símbolo del sistema. 

1. Cuando se muestre la ventana "Control de cuentas de usuario", selecciona **Sí** para permitir que se ejecute la aplicación. 

1. Pega el script haciendo clic con el botón derecho en las ventanas **Administrador: símbolo del sistema** y presiona **Entrar** para ejecutarlo. **Nota:** la ventana se cierra automáticamente después de ejecutar el script.


### Tarea 2: ataques simulados

En esta tarea, ejecutarás dos ataques simulados para explorar las funcionalidades de Microsoft Defender para puntos de conexión.

1. En el menú izquierdo, en **Puntos de conexión**, selecciona **Evaluación y tutoriales** y después, selecciona **Tutoriales y simulaciones** en el lado izquierdo.

1. Selecciona la pestaña **Tutoriales**.

1. En *Investigación automatizada (puerta trasera)* verás un mensaje que describe el escenario. Debajo de este párrafo, haz clic en **Leer el tutorial**. Se abre una nueva pestaña del explorador que incluye instrucciones para realizar la simulación.

1. En la nueva pestaña del explorador, busca la sección denominada **Ejecutar la simulación** (página 5, a partir del paso 2) y siga los pasos para ejecutar el ataque. **Sugerencia:** el archivo de simulación *RS4_WinATP-Intro-Invoice.docm* se puede encontrar en el portal, justo debajo de **Leer el tutorial** que has seleccionado en el paso anterior, seleccionando el botón **Obtener archivo de simulación**. 

<!--- 1. Repeat the last 3 steps to run another tutorial, *Automated investigation (fileless attack)*. This is no longer working due to win1 AV --->


### Tarea 3: investigar los ataques

1. En el portal de Microsoft 365 Defender, selecciona **Incidentes y alertas** en la barra de menús de la izquierda y luego selecciona **Incidentes**.

1. Un nuevo incidente denominado "Incidente de varias etapas..." está en el panel derecho. Selecciona el nombre del incidente para cargar sus detalles.

    >**Nota:** un incidente llamado "Sospechoso..." puede aparecer primero. Esto se reemplazará más adelante por el incidente mencionado anteriormente cuando Microsoft 365 Defender los correlaciona con un único problema de seguridad, incluida la alerta de prueba original creada en la tarea 1.

1. Selecciona el botón **Administrar incidente** y aparecerá una nueva hoja de ventana. 

1. En **Etiquetas de incidente**, escribe "Tutorial" y selecciona **Tutorial (Crear nuevo)** para crear una nueva etiqueta. 

1. Selecciona el botón de alternancia **Asignar a** y agrega tu cuenta de usuario (Me) como propietario del incidente. 

1. En **Clasificación**, expande el menú desplegable. 

1. En **Información, actividad esperada**, selecciona **Pruebas de seguridad**. 

1. Agrega los comentarios, si quieres, y selecciona **Guardar** para actualizar el incidente y finalizar.

1. Revisa el contenido de las pestañas *Ataque, Alertas, Activos, Investigaciones, Evidencia y Respuesta* y *Resumen*. Los dispositivos y los usuarios se encuentran en la pestaña *Recursos*. La pestaña *Historia de ataque* muestra el *Gráfico de incidentes*. **Sugerencia**: es posible que algunas pestañas estén ocultas debido al tamaño de la pantalla. Selecciona la pestaña de puntos suspensivos (...) para que aparezcan.

>**Advertencia:** las simulaciones y tutoriales aquí son una excelente fuente de aprendizaje a través de la práctica.  Las simulaciones y tutoriales se agregan y editan periódicamente en el portal.  Pero algunas de estas simulaciones y tutoriales pueden interferir con el rendimiento de los laboratorios diseñados para este curso de formación.  Realiza solo las simulaciones y los tutoriales recomendados en las instrucciones que se ofrecen para este laboratorio al usar el inquilino de Azure proporcionado por el curso.  Puedes realizar las otras simulaciones y tutoriales *después* de completar este curso de formación con este inquilino.

## Has completado el laboratorio.