---
lab:
  title: "Ejercicio 4: mitigación de ataques con Microsoft\_Defender para punto de conexión"
  module: Learning Path 4 - Mitigate threats using Microsoft Defender for Endpoint
---

# Ruta de aprendizaje 4 - Laboratorio 1 - Ejercicio 2: mitigación de ataques con Microsoft Defender para punto de conexión

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod2_L1_Ex2_10_19.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que está implementando Microsoft Defender para punto de conexión. El administrador tiene previsto incorporar algunos dispositivos para dar información sobre los cambios necesarios en los procedimientos de respuesta del equipo de SecOps.

Para explorar las funcionalidades de mitigación de ataques de Defender para punto de conexión, comprobará la incorporación correcta de dispositivos e investigará alertas e incidentes creados durante ese proceso.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: comprobar la incorporación de dispositivos

En esta tarea, confirmarás que el dispositivo se ha incorporado correctamente y crearás una alerta de prueba.

1. Si aún no estás en el portal de Microsoft Defender XDR en el explorador Microsoft Edge, ve a (<https://security.microsoft.com>) e inicia sesión como administrador del inquilino.

1. En el menú de la izquierda, en el área **Recursos**, selecciona **Dispositivos**. Espere hasta que WIN1 aparezca en la página Dispositivos antes de continuar. De lo contrario, es posible que tengas que repetir esta tarea para ver las alertas que se generarán más adelante.

    >**Nota:** Si has completado el proceso de incorporación y no ves dispositivos en la lista Dispositivos después de una hora, podría indicar un problema de incorporación o conectividad.

1. En la barra de menús izquierda del portal de Microsoft Defender XDR, expanda la sección **Sistema** y seleccione **Configuración** y, a continuación, en la página *Configuración*, seleccione **Puntos de conexión**.

1. Selecciona **Incorporación** en la sección Administración de dispositivos y asegúrate de que *"Windows 10 y 11"* esté seleccionado como sistema operativo. El mensaje *"Primer dispositivo incorporado"* ahora muestra *Completado*.

1. Desplázate hacia abajo y, en la sección *"2. Ejecutar una prueba de detección"*, copia el script de prueba de detección seleccionando el botón **Copiar**.  

1. En la barra de búsqueda de Windows de la máquina virtual WIN1, escribe **CMD** y elige **Ejecutar como administrador** en el panel derecho de la aplicación de símbolo del sistema.

1. Cuando se muestre la ventana "Control de cuentas de usuario", selecciona **Sí** para permitir que se ejecute la aplicación. 

1. Pega el script haciendo clic con el botón derecho en las ventanas **Administrador: símbolo del sistema** y presiona **Entrar** para ejecutarlo.

    >**Nota:** La ventana se cierra automáticamente después de ejecutar correctamente el script y después de unos minutos se generan alertas en el portal de Microsoft Defender XDR.

### Tarea 2: Investigar alertas e incidentes

En esta tarea, investigará las alertas e incidentes generados por el script de prueba de detección de incorporación en la tarea anterior.

1. En el portal de Microsoft Defender XDR, expanda **investigación y respuesta** en la barra de menús de la izquierda, expanda **Incidentes y alertas** y seleccione **Alertas**.

    >**Nota:** En las versiones actualizadas de la página del portal de Microsoft Defender XDR, se encuentra la opción *Incidentes y alertas* en el encabezado de menú *Investigaciones y respuesta*.

1. En el panel **Alertas**, seleccione la alerta denominada *[TestAlert] Línea de comandos sospechosa de PowerShell* para cargar sus detalles.

1. Revise la escala de tiempo de la *Historia de la alerta* y, a continuación, revise las pestañas *Detalles* y *Recomendaciones*.

    >**Nota:** En la pestaña *Detalles* de la alerta puede desplazarse hasta la sección *Detalles del incidente* y seleccionar el enlace *Incidente de ejecución en un punto de conexión* para abrir el incidente.

1. En el portal de Microsoft Defender XDR, seleccione **incidentes y alertas** en la barra de menús de la izquierda y, a continuación, seleccione **Incidentes**

1. Para desactivar el filtro *Gravedad de la alerta*, seleccione la **X** situada a la derecha del filtro.

1. Aparece un nuevo incidente denominado *Incidente de ejecución en un punto de conexión* en el panel derecho. Selecciona el nombre del incidente para cargar sus detalles.

1. Seleccione el vínculo **Administrar incidentes** (con un icono de lápiz) y aparecerá una nueva hoja de ventana.

1. En **Etiquetas de incidente**, escriba "Simulación" y seleccione **Simulación (Crear nueva)** para crear una nueva etiqueta.

1. Selecciona el botón de alternancia **Asignar a** y agrega tu cuenta de usuario (Me) como propietario del incidente.

1. En **Clasificación**, expande el menú desplegable.

1. En **Información, actividad esperada**, selecciona **Pruebas de seguridad**.

1. Selecciona **Guardar** para actualizar el incidente y finalizar.

1. Revisa el contenido de las pestañas *Ataque, Alertas, Activos, Investigaciones, Evidencia y Respuesta* y *Resumen*. Los dispositivos y los usuarios se encuentran en la pestaña *Recursos*. En un incidente real, la pestaña *Historia de ataque* muestra el *gráfico del incidente*. **Sugerencia:** Es posible que algunas pestañas estén ocultas debido al tamaño de la pantalla. Selecciona la pestaña de puntos suspensivos (...) para que aparezcan.

### Tarea 3: Simulación de un ataque

>**Advertencia:** Este ataque simulado es una excelente forma de aprendizaje mediante práctica. Cuando use el inquilino de Azure proporcionado en el curso, realice solo el ataque indicado en las instrucciones facilitadas para este laboratorio.  Podrá realizar otros ataques simulados *después* de que este curso de entrenamiento se complete con este inquilino.

En esta tarea, simularás un ataque en la máquina virtual WIN1 (mediante la ejecución de un script de PowerShell) y comprobarás que Microsoft Defender para punto de conexión detecta y mitiga el ataque.

1. En la máquina virtual WIN1, escribe **PowerShell** en la barra de búsqueda, a continuación, *haz clic con el botón derecho* en **Windows PowerShell** y selecciona *Ejecutar como administrador*.

1. Cuando se muestre la ventana "Control de cuentas de usuario", selecciona **Sí** para permitir que se ejecute la aplicación.

1. Para ejecutar el script, en **Windows PowerShell (Administrador)** ve a la carpeta *\Users\Admin\Desktop\Allfiles*, escribe *.\AttackScript.ps1* y presiona **Entrar** para ejecutarlo. A continuación, escribe **R** y presiona **Entrar** para *Ejecutar una vez*.

1. El script generará varias líneas de salida y un mensaje que indica que *no se pudieron resolver los controladores de dominio en el dominio*. Al cabo de unos segundos, se abrirá la aplicación *Bloc de notas*. Aquí se insertará un código de ataque simulado. Mantenga abierta la instancia del Bloc de notas generada automáticamente para experimentar el escenario completo. El código de ataque simulado intentará comunicarse con una dirección IP externa (simulando un servidor C2).

### Tarea 4: Investigación del ataque simulado como incidente aislado

1. En el portal de Microsoft Defender XDR, expanda **investigación y respuesta** en la barra de menús de la izquierda, expanda **Incidentes y alertas** y seleccione **Incidentes**.

    >**Nota:** En las versiones actualizadas de la página del portal de Microsoft Defender XDR, se encuentra la opción *Incidentes y alertas* en el encabezado de menú *Investigaciones y respuesta*.

1. Un nuevo incidente llamado *incidente de varias fases que implica la evasión de la defensa y detección en un punto de conexión* aparece en el panel derecho. Selecciona el nombre del incidente para cargar sus detalles.

    >**Nota:** Si no ve el incidente, asegúrese de borrar el filtro *Gravedad de la alerta*; para ello, seleccione la **X** situada a la derecha del filtro.

1. En la pestaña *Historia de ataque*, contraiga los paneles **Alertas** y **Detalles del incidente** para ver el **grafo de incidentes** completo.

1. Pase el mouse y seleccione los **nodos del grafo de incidentes** para revisar las *entidades*.

1. Vuelve a expandir el panel **Alertas** (lado izquierdo) y selecciona el icono de **Reproducir historia de ataque***Ejecutar*. Se muestra la alerta de escala de tiempo del ataque por alerta y se rellena dinámicamente el *grafo de incidentes*.

1. Revisa el contenido de las pestañas *Ataque, Alertas, Activos, Investigaciones, Evidencia y Respuesta* y *Resumen*. Los dispositivos y los usuarios se encuentran en la pestaña *Recursos*. **Sugerencia:** Es posible que algunas pestañas estén ocultas debido al tamaño de la pantalla. Selecciona la pestaña de puntos suspensivos (...) para que aparezcan.

1. En la pestaña **Evidencia y respuesta**, seleccione **Direcciones IP** y, luego, seleccione la *dirección IP* mostrada. En la ventana emergente, revise los detalles de la dirección IP y desplácese hacia abajo y seleccione el botón **Abrir página de dirección IP**.

1. Revise el contenido de las pestañas *Información general, Incidentes y alertas y Observado en las organizaciones* de la página *Dirección IP*. Es posible que algunas pestañas no contengan información de la dirección IP.

## Has completado el laboratorio
