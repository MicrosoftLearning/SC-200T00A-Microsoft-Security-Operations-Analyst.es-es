---
lab:
  title: 'Ejercicio 11: uso de repositorios en Microsoft Sentinel'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 11: uso de repositorios en Microsoft Sentinel

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Ya has creado reglas programadas y de análisis de seguridad de Microsoft.  Debes centralizar las reglas analíticas en un repositorio de Azure DevOps.  Luego conecta Sentinel al repositorio de Azure DevOps e importa el contenido. 

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tiempo estimado para completar este laboratorio: 30 minutos

### Tarea 1: crear y exportar una regla analítica

En esta tarea, habilitarás el análisis de comportamiento de entidades en Microsoft Sentinel.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. Selecciona **Análisis** en el área *Configuración* de la hoja izquierda.

1. Selecciona la regla **RegKey de inicio** que has creado anteriormente.

1. En la barra de herramientas, selecciona **Exportar**. **Sugerencia:** es posible que tengas que seleccionar el icono de puntos suspensivos **(...)** para verlo.

1. La regla se exporta a un archivo de texto denominado *Azure_Sentinel_analytic_rule.json*.

1. Selecciona **Abrir archivo** debajo del nombre del archivo descargado y luego selecciona **Más aplicaciones**.

1. Selecciona **Bloc de notas** y después, **Aceptar**.

1. Revisa la plantilla de Azure Resource Manager y ciérrala cuando hayas terminado.

### Tarea 2: crear nuestro entorno de Azure DevOps

En este caso, debes crear primero un repositorio de Azure DevOps.

1. Abre otra pestaña del explorador y ve a <https://aexprodcus1.vsaex.visualstudio.com/me?mkt=en-US>.

1. En la página *Necesitamos algunos detalles más*, selecciona **Continuar**.

1. En la página *Introducción a Azure DevOps*, selecciona **Crear nueva organización** y luego selecciona **Continuar**.

    >**Nota:** Si esta operación no se completa al cabo de un minuto o más, **actualiza (Ctrl-R)** la página del explorador.

1. En la página *Casi ha terminado...*, escribe un nombre para la organización de DevOps que no quieras usar en el futuro, como por ejemplo, el prefijo de inquilino.

    >**Sugerencia:** se puede encontrar en la pestaña Recursos del laboratorio (WWLx...).

1. *Escribe los caracteres que veas* y luego **Continuar**.

1. En la página *Cree un proyecto para empezar*, escribe **GroupCommon** y luego selecciona **Crear proyecto**.

1. Ve a **Repos** en el panel izquierdo.

1. En la parte inferior de la página del área *Inicializar rama principal con un archivo README o gitignore*, selecciona **Inicializar**.

1. La página debe mostrar los archivos del repositorio.  el único archivo es README.me.

1. En la hoja Archivos (lado derecho de la página), la barra de herramientas incluye opciones *Configurar compilación*, *Clonar*, ... Selecciona el icono de dos puntos **(:)** para mostrar más opciones.

1. Selecciona **Cargar archivos**.

1. Selecciona **Examinar**, selecciona el archivo **Azure_Sentinel_analytic_rule.json** en el directorio *Descargas* y selecciona **Abrir**.

1. Selecciona **Confirmar**.

1. Luego selecciona **Guardar** en la esquina superior izquierda de la página.  Esto muestra la organización y los proyectos.

1. En la esquina inferior, selecciona **Configuración de la organización**.

1. Selecciona **Directivas** en el área *Seguridad* de la hoja izquierda.

1. **Activa*** el acceso de aplicación de terceros a través de OAuth* en el área *Directivas de conexión de la aplicación*.


### Tarea 3: establecer una conexión de Sentinel a Azure DevOps.

1. Selecciona la pestaña *Azure Portal* / *Microsoft Sentinel* en el explorador.

1. En Microsoft Sentinel, selecciona **Repositorios (versión preliminar)** en la sección *Administración de contenido*.

1. Selecciona el botón **+ Agregar nuevo** en la barra de herramientas.

1. Para el nombre escribe **Mi contenido**.

1. En Control de código fuente, selecciona **Azure DevOps**.

1. Seleccione **Autorizar**. Desplázate hacia abajo en la solicitud de permisos y luego selecciona **Aceptar**.

1. Selecciona la organización que has creado anteriormente (por ejemplo, WWLx...).

1. Selecciona el proyecto que has creado anteriormente, *Mi contenido de Sentinel*.

1. Selecciona el repositorio que has creado anteriormente, *Mi contenido de Sentinel*. **Sugerencia:** es posible que tengas que desplazarte hacia abajo dentro de la lista desplegable para ver el repositorio.

1. Selecciona la Rama **principal**. **Sugerencia:** es posible que tengas que desplazarte hacia abajo dentro de la lista desplegable para ver la rama.

1. Selecciona todos los tipos de contenido.

1. Seleccione **Crear**.

1. Vuelve al área de trabajo de Microsoft Sentinel si es necesario.

1. Ve a la página *Repositorios (versión preliminar)* y selecciona **Actualizar**. Espera hasta que el *Estado de última implementación* sea *Error*.  

    >**Nota:** el estado *Error* se debe a limitaciones en el entorno de laboratorio hospedado. Normalmente, verás *Correcto*. Luego puedes ver en *Analytics* la regla importada *Regla de Azure DevOps*.

## Has completado el laboratorio.
