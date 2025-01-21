---
lab:
  title: 'Ejercicio 4: exploración del análisis de comportamiento de entidades'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 4: exploración del análisis de comportamiento de entidades

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Ya has creado reglas programadas y de análisis de seguridad de Microsoft.

Debes configurar Microsoft Sentinel para realizar el análisis de comportamiento de entidades para detectar anomalías y dar páginas de análisis de entidades.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 15 minutos

### Tarea 1: explorar el comportamiento de la entidad

En esta tarea, explorarás el análisis de comportamiento de entidades en Microsoft Sentinel.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en <https://portal.azure.com>.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. Selecciona la página **Comportamiento de la entidad**.

1. En el elemento emergente de la *Configuración del comportamiento de la entidad*, selecciona **Establecer UEBA**.

1. En la pestaña *Configuración* debajo de *Análisis del comportamiento de entidades*, desplázate hacia abajo en la sección *Anomalías*, asegúrate de leer todo el párrafo y comprueba que el *modificador* está *activado*.

1. Selecciona el vínculo **Ir a Análisis para configurar las anomalías**.

### Tarea 2: confirmar y revisar reglas de anomalías

En esta tarea, confirmarás que las reglas de análisis de anomalías están habilitadas.

1. Ahora deberías estar en la página * Análisis*, pestaña * Anomalías*.

1. Confirma que la columna de estado de las reglas está *habilitada*.

1. Selecciona cualquier regla y luego, **Editar** en la hoja de reglas.

1. Revisa la información de la pestaña *General*. Observa que el *Modo* es **Producción** y luego selecciona **Siguiente: configuración**.

1. Revisa la información de la pestaña *Configuración*. Observa que no puedes cambiar el **Umbral de puntuación de anomalías**.

1. Después, selecciona **X** en la esquina superior derecha para salir del Asistente para reglas de Análisis.

1. Desplázate a la derecha a la regla de análisis que has seleccionado hasta que veas y selecciones el icono de puntos suspensivos **(...)**.

1. Selecciona **Duplicar** y desplázate a la izquierda para revisar la nueva regla con la pestaña **FLGT** al principio del nombre.

1. Selecciona **Regla FLGT** y luego, **Editar** en la hoja de reglas.

1. Revisa la información de la pestaña *General*. Observa que el *modo* es **Lanzamiento como paquete piloto** y luego selecciona **Siguiente: configuración**.

1. Revisa la información de la pestaña *Configuración*. Ten en cuenta que ahora puedes cambiar el **Umbral de puntuación de anomalías**.

1. Establece el valor en **1** y luego selecciona **Siguiente: enviar comentarios**.

1. Selecciona **Siguiente: revisar y crear** y luego **Guardar** para actualizar la regla.

    >**Nota:** puedes actualizar la regla **Lanzamiento como paquete piloto** a **Producción** cambiando la configuración de esta regla y guardando los cambios. La regla **Producción** se convertirá en la regla **Lanzamiento como paquete piloto** después.

## Continúa con el ejercicio 5
