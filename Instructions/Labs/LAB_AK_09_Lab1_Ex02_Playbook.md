---
lab:
  title: 'Ejercicio 2: creación de un cuaderno de estrategias'
  module: Learning Path 9 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 9 - Laboratorio 1 - Ejercicio 2: creación de un cuaderno de estrategias en Microsoft Sentinel

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a detectar y mitigar amenazas mediante Microsoft Sentinel. Ahora, quieres responder y corregir acciones que se pueden ejecutar desde Microsoft Sentinel como rutina.

Un cuaderno de estrategias puede ayudarte a automatizar y organizar la respuesta a las amenazas, se puede integrar con otros sistemas de manera interna y externa, y se puede configurar para ejecutarse automáticamente en respuesta a alertas o incidentes específicos, cuando se desencadena mediante una regla de análisis o una regla de automatización.

>**Importante:** Los ejercicios de laboratorio de la ruta de aprendizaje n.º 9 se encuentran en un entorno *independiente*. Si sales del laboratorio sin completarlo, deberás volver a ejecutar algunas configuraciones de nuevo.

### Tarea 1: Crear un cuaderno de estrategias de Microsoft Sentinel

En esta tarea, creas una aplicación lógica que se usa como cuaderno de estrategias en Microsoft Sentinel.

>**Nota:** Microsoft Sentinel se ha preimplementado en la suscripción a Azure con el nombre **defenderWorkspace** y se han instalado las soluciones de *Centro de contenido* necesarias.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona **defenderWorkspace** de Microsoft Sentinel.

1. En *Microsoft Sentinel*, navega hasta **Centro de contenido**.

1. En la barra de búsqueda, busca **Sentinel SOAR Essentials**.

1. Selecciona la solución que aparece en los resultados.

1. En los detalles de la solución, selecciona **Administrar**.

1. Busca el cuaderno de estrategias **Defender_XDR_Ransomware_Playbook_for_SecOps_Tasks** y selecciona el nombre.

1. Selecciona la plantilla **Tareas de incidentes: cuaderno de estrategias de ransomware de Microsoft Defender XDR para SecOps**.

1. En el panel de detalles, selecciona **Crear cuaderno de estrategias**.

1. En Grupo de recursos, selecciona **Crear nuevo**, escribe **RG- Playbooks** y selecciona Aceptar.

1. Quita **para** y los *caracteres de subrayado* extra del nombre del cuaderno de estrategias (superaría el límite de 64 caracteres). Debe decir **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**.

1. Seleccione **Conexiones**.

1. Seleccione **Siguiente: Revisar y crear**.

1. Ahora selecciona **Crear cuaderno de estrategias**.

    >**Nota**: espera a que la implementación se complete antes de continuar con la tarea siguiente.

### Tarea 2: Actualizar un cuaderno de estrategias en Microsoft Sentinel

En esta tarea, actualizas el nuevo cuaderno de estrategias que has creado con la información de conexión adecuada.

1. Cuando se complete la tarea anterior, debes estar en la página *Defender_XDR_Ransomware_Playbook_SecOps-Tasks | Diseñador de aplicación lógica*. Si no lo estás, completa los pasos 1 a 5 siguientes.

1. En la barra de búsqueda de Azure Portal, escribe Sentinel y luego selecciona Microsoft Sentinel.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Seleccione Automatización en el área Configuración y después seleccione la pestaña *Cuadernos de estrategias activos*.

1. Selecciona Actualizar en la barra de comandos en caso de que no veas ningún cuaderno de estrategias. Debería ver el cuaderno de estrategias creado a partir del paso anterior.

1. Selecciona el vínculo del nombre del cuaderno de estrategias **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**.

1. En la página del Diseñador de aplicación lógica de **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**, en el menú de comandos, selecciona Editar.

    >**Nota:**: es posible que tengas que actualizar la página.

1. Seleccione el primer bloque, incidente de Microsoft Sentinel.

1. Selecciona el vínculo **Cambiar conexión***.

1. Selecciona **Agregar nuevo** y selecciona **Iniciar sesión**. En la nueva ventana, selecciona las credenciales de administrador de la suscripción de Azure cuando se te solicite. La última línea del bloque ahora debería decir "Conectado a nombre-usuario-admin".

<!--- 1. Below within the logic split (+ sign), select Add an action to incident.--->

1. Seleccione **Guardar** en la barra de comandos.

1. Selecciona **X** de la ventana para cerrarla. La aplicación lógica se usará en un laboratorio futuro.

### Tarea 3: Crear una regla de automatización

1. En Microsoft Sentinel, expande *Configuración* en el menú de navegación y selecciona *Automatización*.

1. Selecciona **+ Crear** y elige **Regla de automatización**.

1. Asigna un nombre a la regla

1. Deja el *Desencadenante* en **Cuando se crea un incidente**.

1. En *Condiciones* deja el proveedor de incidentes en *Todo*.

1. Deje el *Nombre de la regla analítica* en *Todo*.

1. Selecciona **+ Agregar** y elige *Condición (AND)*.

1. En el menú desplegable, selecciona **Tácticas**.

1. Selecciona el operador **Contiene** en la lista desplegable.

1. Selecciona los siguientes *Valores* de tácticas:
    - Reconocimiento
    - Ejecución
    - Persistencia
    - Comando y control
    - Exfiltración
    - PreAttack

1. En Acciones, selecciona **Ejecutar cuaderno de estrategias**.

1. Selecciona el vínculo para **Administrar permisos del cuaderno de estrategias**.

1. En la página *Administrar permisos*, selecciona el grupo de recursos **RG-Playbooks** que has creado en el laboratorio anterior y después, **Aplicar**.

1. En la lista desplegable, selecciona el cuaderno de estrategias **Defender_XDR_Ransomware_Playbook_SecOps_Tasks**.

1. Seleccione **Aplicar** en la parte inferior.

1. Selecciona la **X** de la ventana *Crear nueva regla de automatización* para cerrarla.

Ahora has creado un cuaderno de estrategias y una regla de automatización en Microsoft Sentinel.

## Continúa con el ejercicio 3
