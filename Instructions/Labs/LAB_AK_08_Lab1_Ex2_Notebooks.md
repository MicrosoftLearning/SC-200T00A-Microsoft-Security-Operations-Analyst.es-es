---
lab:
  title: "Ejercicio 2: búsqueda de amenazas mediante cuadernos con Microsoft\_Sentinel"
  module: Learning Path 8 - Perform threat hunting in Microsoft Sentinel
---

# Ruta de aprendizaje 8 - Laboratorio 1 - Ejercicio 2: búsqueda de amenazas mediante cuadernos con Microsoft Sentinel

## Escenario del laboratorio

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes explorar las ventajas de la búsqueda de amenazas con cuadernos de Microsoft Sentinel. Puedes usar cuadernos para implementar:

- Realiza análisis que no se incluyan de forma preestablecida en Microsoft Sentinel, como algunas características de aprendizaje automático de Python.
- Crea visualizaciones de datos que no se incluyan de forma preestablecida en Microsoft Sentinel, como escalas de tiempo personalizadas y árboles de proceso.
- Integrar orígenes de datos fuera de Microsoft Sentinel, como un conjunto de datos local.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Hunt%20for%20threats%20using%20notebooks%20in%20Microsoft%20Sentinel)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 

### Tarea 1: explorar cuadernos

En esta tarea, explorarás el uso de cuadernos en Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. En el área de trabajo de Microsoft Sentinel, selecciona **Cuadernos** en el área *Administración de amenazas*.

1. Debes crear un área de trabajo de AzureML. Selecciona **Configurar Azure Machine Learning** y luego **Crear un área de trabajo de Azure ML** en la barra de comandos.

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

1. Una vez que hayas guardado, selecciona el botón **Iniciar cuaderno**. Esto te llevará a Microsoft Azure Machine Learning Studio.

1. Selecciona **Cerrar** si aparece una ventana informativa en Microsoft Azure Machine Learning Studio.

1. En la barra de comandos, a la derecha del selector **Instancia de proceso:**, selecciona el símbolo **+** para crear una nueva instancia de proceso. **Sugerencia:** puede estar oculto dentro del icono de puntos suspensivos **(...)**.

     >**Nota:** para tener más espacio en pantalla, oculta la hoja izquierda de Azure ML Studio seleccionando las 3 líneas de la parte superior izquierda, así como los archivos de cuadernos seleccionando el icono **<<**.

1. En el campo *Nombre del proceso*, escribe un nombre único. Esto identificará la instancia de proceso.

1. Desplázate hacia abajo y selecciona la primera opción disponible. **Sugerencia**: el tipo de carga de trabajo debería ser Desarrollo en cuadernos y pruebas ligeras.

1. Seleccione el botón **Crear** en la parte inferior de la pantalla. Cierra cualquier ventana de comentarios que pueda aparecer. Esto tardará unos minutos. Verás una notificación (icono de campana) cuando haya terminado y el icono izquierdo de la *Instancia de proceso* cambie de azul a verde.

1. Una vez creado el proceso y cuando esté en ejecución, comprueba que el kernel que se vaya a usar sea *Python 3.8 - AzureML*. **Sugerencia:** esto aparece a la derecha de la barra de comandos.

1. Selecciona el botón **Autenticar** y espera a que se complete la autenticación.

1. Para borrar todos los resultados del cuaderno, selecciona **Borrar todas las salidas** de la barra de comandos y sigue el tutorial *Introducción*. **Sugerencia:** para ello, selecciona los puntos suspensivos (...) en la barra de comandos.

>**Nota:** si no puedes completar los pasos anteriores para acceder al cuaderno, puedes ver dichos pasos en tu página de GitHub. [Introducción a Azure ML Notebooks y Microsoft Sentinel](https://nbviewer.org/github/Azure/Azure-Sentinel-Notebooks/blob/master/A%20Getting%20Started%20Guide%20For%20Azure%20Sentinel%20ML%20Notebooks.ipynb) 

## Has completado el laboratorio.
