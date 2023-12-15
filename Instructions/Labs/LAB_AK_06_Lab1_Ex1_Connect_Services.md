---
lab:
  title: "Ejercicio 1: Conexión de datos a Microsoft\_Sentinel mediante conectores de datos"
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# Ruta de aprendizaje 6 - Laboratorio 1 - Ejercicio 1: Conexión de datos a Microsoft Sentinel mediante conectores de datos

## Escenario del laboratorio

![Descripción general del laboratorio.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex1.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a conectar los datos de registro de los numerosos orígenes de datos de tu organización. La organización tiene datos de Microsoft 365, Microsoft 365 Defender, recursos de Azure, máquinas virtuales que no son de Azure, etc. Primero empezarás conectando los orígenes de Microsoft.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Connect%20data%20to%20Microsoft%20Sentinel%20using%20data%20connectors)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: Acceso al área de trabajo de Microsoft Sentinel

En esta tarea, accederás al área de trabajo de Microsoft Sentinel.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. Abra el explorador Microsoft Edge.

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico del inquilino** que te ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña del inquilino** que te ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y después selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que creaste en el laboratorio anterior.

1. En el menú de navegación, selecciona Análisis.

1. Selecciona *Crear incidentes basados en Microsoft Defender for Cloud* en las plantillas de reglas.

1. Selecciona **Crear regla** en la hoja de información del conector.

1. En el Asistente para reglas de análisis, selecciona **Siguiente: Respuesta automatizada** y luego selecciona **Siguiente: Revisar y crear**.

1. Seleccione **Guardar**.

### Tarea 2: Conexión al conector de datos de Microsoft Defender for Cloud

En esta tarea, conectarás el conector de datos de Microsoft Defender for Cloud.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Microsoft Defender for Cloud** y selecciónala en la lista.

1. En la página de la solución de *Microsoft Defender for Cloud*, selecciona **Instalar**.

1. Cuando se haya completado la instalación, selecciona **Administrar**.

    >**Nota:** la solución de *Microsoft Defender for Cloud* instala el conector de datos de *Microsoft Defender for Cloud basado en suscripciones (heredado)*, el conector de datos *Microsoft Defender for Cloud basado en inquilinos (versión preliminar)* y una regla analítica.

1. Selecciona la casilla del conector de datos *Microsoft Defender for Cloud basado en suscripciones (heredado)* y haz clic en **Abrir página del conector**.

1. En la sección *Configuración*, en la pestaña *Instrucciones*, **selecciona** la casilla de la suscripción "Pase para Azure: Patrocinio" y desliza la opción **Estado** a la derecha.

    >**Nota:** si vuelve al estado desconectado, revisa la Ruta de aprendizaje 3, Ejercicio 1, Tarea 1 para asignar los permisos adecuados a tu cuenta.

1. Ahora, el *estado* debe ser **Conectado** y la "Sincronización bidireccional" debe estar *Habilitada*.

1. Desplázate hacia abajo y en el área *Crear incidentes: ¡recomendado!* verifica que *Crear incidentes automáticamente a partir de todas las alertas generadas en este servicio conectado * esté **Habilitado**.

### Tarea 3: Conexión del conector de datos Actividad de Azure

En esta tarea, configurarás Sentinel para usar el conector de datos *Actividad de Azure*.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Actividad de Azure** y selecciónala en la lista.

1. En la página de la solución *Actividad de Azure*, selecciona **Instalar**.

1. Cuando se haya completado la instalación, selecciona **Administrar**.

    >**Nota:** la solución *Actividad de Azure* instala el conector de datos *Actividad de Azure*, 12 reglas analíticas, 14 consultas de búsqueda y 1 libro.

1. Selecciona el conector de datos *Actividad de Azure* y luego selecciona **Abrir página del conector**.

1. En el área *Configuración*, en la pestaña *Instrucciones*, desplázate hacia abajo hasta "2. Conecta las suscripciones..." y selecciona **Iniciar asistente para asignación de Azure Policy>**.

1. En la pestaña **Aspectos básicos**, selecciona el botón de puntos suspensivos (...) en **Ámbito** y selecciona la suscripción "Pase para Azure: Patrocinio" en la lista desplegable y haz clic en **Seleccionar**.

1. Seleccione la pestaña **Parámetros** y elija el área de trabajo *uniquenameDefender* en la lista desplegable **Área de trabajo de Log Analytics**. Esta acción aplicará la configuración de la suscripción para enviar la información al área de trabajo de Log Analytics.

1. Seleccione la pestaña **Corrección** y active la casilla **Crear una tarea de corrección**. Esta acción aplicará la directiva a los recursos de Azure ya existentes.

1. Seleccione el botón **Revisar y crear** para revisar la configuración.

1. Seleccione **Crear** para finalizar.

## Continúa con el ejercicio 2
