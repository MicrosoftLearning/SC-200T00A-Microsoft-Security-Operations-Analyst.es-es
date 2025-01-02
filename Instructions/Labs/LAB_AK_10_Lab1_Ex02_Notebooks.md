---
lab:
  title: "Ejercicio 2: búsqueda de amenazas mediante cuadernos con Microsoft\_Sentinel"
  module: Learning Path 10 - Perform threat hunting in Microsoft Sentinel
---

# Ruta de aprendizaje 10 - Laboratorio 1 - Ejercicio 2: búsqueda de amenazas mediante Notebooks con Microsoft Sentinel

## Escenario del laboratorio

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes explorar las ventajas de la búsqueda de amenazas con cuadernos de Microsoft Sentinel. Puedes usar cuadernos para implementar:

- Realice análisis que no se proporcionan de forma predeterminada en Microsoft Sentinel, como algunas características de aprendizaje automático de Python.
- Cree visualizaciones de datos que no se proporcionan de forma predeterminada en Microsoft Sentinel, como escalas de tiempo personalizadas y árboles de procesos.
- Integrar orígenes de datos fuera de Microsoft Sentinel, como un conjunto de datos local.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 10 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: explorar cuadernos

En esta tarea, explorará el uso de cuadernos en Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. En el área de trabajo de Microsoft Sentinel, selecciona **Cuadernos** en el área *Administración de amenazas*.

1. A continuación, debe crear un área de trabajo de Azure Machine Learning. Selecciona **Configurar Azure Machine Learning** y luego **Crear un área de trabajo de Azure ML** en la barra de comandos.

1. En el cuadro Suscripción, seleccione la suscripción.

1. Selecciona **Crear nuevo** para el grupo de recursos, escribe *RG-MachineLearning* para el nombre y selecciona **Aceptar**. 

1. En la sección Detalles del área de trabajo, haz lo siguiente:

     - Asigne un nombre único al área de trabajo.
     - Deja **Este de EE. UU** como valor predeterminado para *Región*.
     - Guarda la cuenta de almacenamiento predeterminada, el almacén de claves e información de Application Insights.
     - La opción Registro de contenedor puede permanecer como **Ninguno**.

1. En la parte inferior de la página, seleccione **Revisar y crear**. Cuando recibas el mensaje *"Validación superada"*, selecciona **Crear**. 

     >**Nota:** la implementación del área de trabajo de Machine Learning puede tardar unos minutos.

1. Una vez que aparezca el mensaje *Se completó la implementación*, vuelves al portal de Microsoft Sentinel.

1. Selecciona **Cuadernos** y luego selecciona la pestaña **Plantillas** en la barra de comandos central. 

1. Selecciona una **Guía de introducción a los cuadernos de aprendizaje automático de Microsoft Sentinel**.

1. En el panel derecho, desplázate hacia abajo y selecciona el botón **Crear desde la plantilla**. Revisa las opciones predeterminadas y luego selecciona **Guardar**.

1. Una vez que hayas guardado, selecciona el botón **Iniciar cuaderno**. Esto le lleva a Microsoft Azure Machine Learning Studio.

1. Seleccione **Cerrar** si aparece una ventana informativa en Microsoft Azure Machine Learning Studio.

1. En la barra de comandos, a la derecha del selector **Proceso:**, selecciona el símbolo **+** para la instancia *Crear proceso de Azure ML*. **Sugerencia:** puede estar oculto dentro del icono de puntos suspensivos **(...)**.

     >**Nota:** Para tener más espacio en pantalla, oculte la hoja izquierda de Azure ML Studio; para ello, seleccione el *menú de hamburguesa* (3 líneas horizontales en la parte superior izquierda), así como si contrae los archivos de Notebooks seleccionando el icono **<<**.

1. En el campo *Nombre del proceso*, escribe un nombre único. Esto identifica la instancia de proceso.

1. Desplázate hacia abajo y selecciona la primera opción disponible. **Sugerencia:** Tipo de carga de trabajo: Desarrollo en Notebooks (u otros IDE) y pruebas ligeras.

1. Seleccione el botón **Revisar y crear** en la parte inferior de la pantalla y, a continuación, desplácese hacia abajo y seleccione **Crear**. Cierra cualquier ventana de comentarios que pueda aparecer. Esto tarda unos minutos, verá una notificación (icono de campana) cuando haya terminado y el icono izquierdo de la *instancia de proceso* cambie de azul a verde.

1. Una vez creado y ejecutado el proceso, compruebe que el kernel que se va a usar es *Python 3.8: Pytorch y Tensorflow*. **Sugerencia:** esto aparece a la derecha de la barra de comandos.

1. Selecciona el botón **Autenticar** y espera a que se complete la autenticación.

1. Para borrar todos los resultados del cuaderno, seleccione **borrar todas las salidas** (icono de borrador) en la barra de comandos y siga el tutorial *Introducción*. **Sugerencia:** para ello, selecciona los puntos suspensivos (...) en la barra de comandos.

1. Revise la sección *1 Introducción* en el cuaderno y continúe con la sección *2 Inicializar el cuaderno y MSTICPy*.

1. En la sección *2 Inicializar el cuaderno y MSTICPy*, revise el contenido sobre la inicialización del cuaderno e instale el paquete MSTICPy.

1. Ejecute el *código de Python* para inicializar la celda seleccionando el botón **Ejecutar celda** (icono Reproducir) a la izquierda del código.

1. Debe tardar aproximadamente 15 segundos en ejecutarse. Una vez que haya terminado, revise los mensajes de salida e ignore las advertencias sobre la versión del kernel de Python. El código se ejecutó correctamente si *msticpyconfig.yaml* se creó en la carpeta *utils* del panel *explorador de archivos* de la izquierda. El archivo puede tardar otros 30 segundos en aparecer.

    >**Sugerencia:** puedes borrar los mensajes de salida seleccionando los puntos suspensivos (...) situados a la izquierda de la ventana de código del *menú de salida* y seleccionando el icono de *Borrar salida* (cuadrado con una x*).

1. Seleccione el archivo **msticpyconfig.yaml** en el panel *explorador de archivos* de la izquierda para revisar el contenido del archivo y, a continuación, cerrarlo.

1. Continúe con la sección *3 Consulta de datos con MSTICPy* y revise el contenido. No ejecute la celda de código de *varias áreas de trabajo de Microsoft Sentinel*, ya que se produce un error, pero las demás celdas de código se pueden ejecutar correctamente.

>**Nota:** si no puedes completar los pasos anteriores para acceder al cuaderno, puedes ver dichos pasos en tu página de GitHub. [Introducción a Azure ML Notebooks y Microsoft Sentinel](https://nbviewer.org/github/Azure/Azure-Sentinel-Notebooks/blob/master/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## Has completado el laboratorio
