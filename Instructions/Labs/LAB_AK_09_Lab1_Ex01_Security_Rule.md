---
lab:
  title: 'Ejercicio 1: modificación de una regla de seguridad de Microsoft'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio - 1 Ejercicio 1: modificación de una regla de seguridad de Microsoft

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex1.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a detectar y mitigar amenazas mediante Microsoft Sentinel. En primer lugar, debes filtrar las alertas procedentes de Defender for Cloud en Microsoft Sentinel, por gravedad.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 10 minutos

### Tarea 1: activación de una regla de seguridad de Microsoft

En esta tarea, activarás una regla de seguridad de Microsoft.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en (<https://portal.azure.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. Selecciona **Análisis** del área de Configuración.

1. Selecciona el botón **+ Crear** en la barra de comandos y selecciona **Regla de creación de incidentes de Microsoft**.

1. En *Nombre*, escribe **Crear incidentes basados en Defender for Cloud**.

1. Desplázate hacia abajo y en *Servicio de seguridad de Microsoft*, selecciona **Microsoft Defender for Cloud**.

1. En *Filtrar por gravedad*, selecciona la opción *Personalizado* y selecciona **Baja**, **Media** y **Alta** para el nivel de gravedad y vuelva a la regla.

1. Selecciona el botón **Siguiente: respuesta automatizada** y luego selecciona el botón **Siguiente: revisar y crear**.

1. Revisa los cambios realizados y selecciona el botón **Guardar**. La regla de análisis se guardará y se crearán incidentes si hay una alerta en Defender for Cloud.

1. Ahora tendrás los tipos de alerta *Fusión* y *Seguridad de Microsoft*.

## Continúa con el ejercicio 2
