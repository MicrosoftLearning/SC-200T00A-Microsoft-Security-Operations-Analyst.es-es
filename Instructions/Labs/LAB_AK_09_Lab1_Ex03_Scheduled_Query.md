---
lab:
  title: 'Ejercicio 3: creación de una consulta programada a partir de una plantilla'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 3: creación de una consulta programada a partir de una plantilla

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a detectar y mitigar amenazas mediante Microsoft Sentinel. Después de conectar los orígenes de datos a Microsoft Sentinel, crea reglas de análisis personalizadas que te ayuden a detectar las amenazas y los comportamientos anómalos de tu entorno.

Las reglas de análisis buscan eventos o conjuntos de eventos específicos en tu entorno, te avisan cuando se alcanzan determinados umbrales de eventos o condiciones, generan incidentes para que el SOC evalúe e investigue, y responden a las amenazas con procesos de seguimiento y corrección automatizados.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: crear una consulta programada

En esta tarea crearás una consulta programada y la conectarás al canal de Teams que creaste en el ejercicio anterior.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. Selecciona **Análisis** del área de Configuración.

1. Asegúrate de que estás en la pestaña *Plantillas de reglas* de la barra de comandos y busca la regla **Nuevo usuario de CloudShell**.

1. En la hoja de resumen de reglas, asegúrate de que recibes datos revisando el icono verde en *Orígenes de datos: actividad de Azure*.

    >**Nota:** si no lo ves conectado, asegúrate de haber completado la tarea 3 del laboratorio de ruta de aprendizaje 6, ejercicio 1.

1. Selecciona **Crear regla** para continuar.

1. En el Asistente para reglas de análisis, en la pestaña *General*, cambia la *gravedad* a **Media**.

1. Selecciona el botón **Siguiente: establecer la lógica de la regla >**:

1. Para la consulta de regla, selecciona **Ver resultados de la consulta**. No debes recibir ningún resultado ni error.

1. Cierra la ventana *Registros* seleccionando la **X** del ángulo superior derecho y selecciona **Aceptar** para descartar los cambios para volver al asistente.

1. Desplázate hacia abajo y en *Programación de consultas*, establece lo siguiente:

    |Configuración|Valor|
    |---|---|
    |Ejecutar consulta cada|5 minutos|
    |Buscar datos del último|1 día|

    >**Nota:** estamos generando muchos incidentes a propósito para los mismos datos. Esto permite al laboratorio usar estas alertas.

1. En el área *Umbral de alerta*, deja el valor sin cambios, ya que queremos que la alerta registre todos los eventos.

1. En el área *Agrupación de eventos*, deja agrupar **todos los eventos en una sola alerta** como opción seleccionada, ya que queremos generar una sola alerta cada vez que se ejecuta, siempre y cuando la consulta devuelva más resultados que el umbral de alerta especificado anteriormente.

1. Selecciona el botón **Siguiente: configuración de los incidentes >**.

1. En la pestaña *Configuración de los incidentes*, revisa las opciones predeterminadas.

1. Selecciona el botón **Siguiente: respuesta automatizada >**.

1. Selecciona el botón **Siguiente: revisar y crear >**.
  
1. Seleccione **Guardar**.

### Tarea 2: editar tu nueva regla

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona **Análisis** del área de Configuración.

1. Asegúrate de que estás en la pestaña *Reglas activas* de la barra de comandos y selecciona la regla **Nuevo usuario de CloudShell**.

1. Haz clic con el botón secundario en la regla y selecciona **Editar** en el menú *emergente*.

1. Selecciona el botón **Siguiente: establecer la lógica de la regla >**.

1. Selecciona el botón **Siguiente: configuración de los incidentes >**.

1. Selecciona el botón **Siguiente: respuesta automatizada >**.

1. En la pestaña *Respuesta automatizada* en *Reglas de automatización*, selecciona **+ Agregar nuevo**.

1. En *Nombre de la regla de Automation*, escribe **Nivel 2**.

1. En *Acciones*, selecciona **Asignar propietario**.

1. Luego selecciona **Asignar a mí**.

1. Seleccione **Aplicar**.

1. Selecciona el botón **Siguiente: revisar y crear >**.
  
1. Seleccione **Guardar**.

### Tarea 3: probar tu nueva regla

En esta tarea probará la nueva regla de consulta programada.

1. En la barra superior de Azure Portal, selecciona el icono **>_** que corresponde a Cloud Shell. Es posible que tengas que seleccionar primero el icono de puntos suspensivos **(...)** si la resolución de pantalla es demasiado baja.

1. En la ventana *Le damos la bienvenida a Azure Cloud Shell*, seleccione **Powershell**.

1. En la página *Introducción*, seleccione la **cuenta de almacenamiento de montaje** y, después, seleccione **Pase para Azure: patrocinio** en el elemento de menú desplegable *Suscripción de la cuenta de almacenamiento* y seleccione el botón **Aplicar**.

    >**Importante:** No seleccione la opción de botón de radio *No se requiere ninguna cuenta de almacenamiento*. Esto hará que se produzca un error en la creación del incidente.

1. En la página *Cuenta de almacenamiento de montaje*, seleccione **Crearemos una cuenta de almacenamiento para usted** y, a continuación, seleccione **Siguiente**.

1. Espere hasta que se aprovisione Cloud Shell y cierre la ventana de Azure Cloud Shell.

1. En la barra de búsqueda de Azure Portal, escribe *Actividad* y luego selecciona **Registro de actividad**.

1. Asegúrate de que aparecen los siguientes elementos *Nombre de operación*: **enumerar claves de cuentas de almacenamiento** y **actualizar cuenta de almacenamiento Crear**. Estas son las operaciones con las que la consulta KQL que has revisado anteriormente coincidirá para generar la alerta. **Sugerencia:** puede que tengas que seleccionar **Actualizar** para ver el estado actualizado.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona la opción de menú **Incidentes** en *Administración de amenazas*.

1. Selecciona la alternancia **Incidentes de actualización automática**.

1. Deberías ver el servicio recién creado.

    >**Nota:** el evento que desencadena el incidente puede tardar más de 5 minutos en procesarse. Continúa con el ejercicio siguiente, volverás a esta vista más adelante.

1. Selecciona el incidente y revisa la información de la hoja derecha.

## Continúa con el ejercicio 4
