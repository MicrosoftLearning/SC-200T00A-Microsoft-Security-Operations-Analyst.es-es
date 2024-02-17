---
lab:
  title: "Ejercicio 2: conexión de dispositivos Windows a Microsoft\_Sentinel mediante conectores de datos"
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# Ruta de aprendizaje 6 - Laboratorio 1 - Ejercicio 2: conexión de dispositivos Windows a Microsoft Sentinel mediante conectores de datos

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex2.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a conectar los datos de registro de los numerosos orígenes de datos de la organización. El siguiente origen de datos es máquinas virtuales Windows dentro y fuera de Azure, como entornos locales u otras nubes públicas.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Connect%20Windows%20devices%20to%20Microsoft%20Sentinel%20using%20data%20connectors)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: crear una máquina virtual Windows en Azure

En este ejercicio, crearás una máquina virtual Windows en Azure.

1. Inicia sesión en la máquina virtual **WIN1** como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. Seleccione **+ Crear un recurso**. **Sugerencia:** si ya estabas en Azure Portal, es posible que tengas que seleccionar *Microsoft Azure* en la barra superior para ir a Inicio.

1. En el cuadro **Servicios de búsqueda y marketplace**, escribe *Windows 10* y selecciona **Microsoft Window 10** en la lista desplegable.

1. Selecciona el cuadro de **Microsoft Window 10**.

1. Abre la lista desplegable *Plan* y selecciona **Windows 10 Enterprise, versión 22H2**.

1. Selecciona **Iniciar con una configuración preestablecida** para continuar.

1. Selecciona **Desarrollo/pruebas** y luego, **Continuar para crear una máquina virtual**.

1. Selecciona **Crear nuevo** del *Grupo de recursos* y escribe RG-AZWIN01 como nombre y selecciona **Aceptar**.

    >**Nota:** este será un nuevo grupo de recursos con fines de seguimiento. 

1. En *Nombre de máquina virtual*, escribe AZWIN01.

1. Deja el valor predeterminado **(EE. UU.) Este de EE. UU.**  en *Región*.

1. Desplázate hacia abajo y revisa la *Imagen* de la máquina virtual. Si aparece vacío, selecciona **Windows 10 Enterprise, versión 22H2**.

1. Revisa el *Tamaño* de la máquina virtual. Si aparece vacío, selecciona **Ver todos los tamaños**, elige el primer tamaño de máquina virtual en *Más usados por los usuarios de Azure de Azure* y selecciona **Seleccionar**.

    >**Nota:** en caso de que veas el mensaje *Esta imagen no es compatible con Azure Automanage, para deshabilitar esta característica, ve a la pestaña Administración. De lo contrario, selecciona una imagen admitida.* Ve a la pestaña Administración y deshabilita "Automanage". El proceso de creación se realizará correctamente después.

1. Desplázate hacia abajo y escribe un *Nombre de usuario* que elijas. **Sugerencia:** evita palabras reservadas como admin o root.

1. Escribe una *contraseña* de tu preferencia. **Sugerencia:** puede ser más fácil volver a usar la contraseña del inquilino. Se puede encontrar en la pestaña recursos.

1. Desplázate hacia abajo hasta la parte inferior de la página y activa la casilla de *Licencias* para confirmar que tienes la licencia adecuada.

1. Selecciona **Revisar y crear** y espera a que se apruebe la validación.

    >**Nota:** si se produce un error de validación *Redes*, selecciona dicha pestaña, revisa su contenido y luego vuelve a seleccionar **Revisar y crear**.

1. Seleccione **Crear**. Espera hasta que se cree el recurso, lo que puede tardar unos minutos.

### Tarea 2: conectarte a una máquina virtual Windows de Azure

En esta tarea, conectarás una máquina virtual Windows de Azure a Microsoft Sentinel.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. 1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección *Administración de contenido* y selecciona **Centro de contenido**.

1. En el *Centro de contenido*, busca la solución **Eventos de seguridad de Windows** y selecciónala en la lista.

1. En la página de la solución *Eventos de seguridad de Windows*, selecciona **Instalar**.

1. Cuando se haya completado la instalación, selecciona **Siguiente**.

    >**Nota:** la solución *Eventos de seguridad de Windows* instala los *eventos de seguridad de Windows a través de AMA* y los *Eventos de seguridad a través del agente heredado*. Además de 2 libros, 20 reglas analíticas y 43 consultas de búsqueda.

1. Selecciona el conector de datos *Eventos de seguridad de Windows a través de AMA* y selecciona **Abrir página del conector** en la hoja de información del conector.

1. En la sección *Configuración*, en la pestaña *Instrucciones*, selecciona **Crear regla de recopilación de datos**.

1. Escribe **AZWINDCR** como Nombre de regla y luego selecciona **Siguiente: recursos**.

1. Selecciona **+Agregar recursos** para seleccionar la máquina virtual que hemos creado.

1. Expande **RG-AZWIN01** y selecciona **AZWIN01**.

1. Selecciona **Siguiente** y después, **Siguiente: recopilar**.

1. Revisa la opción de recopilación de eventos de seguridad diferente. Mantén *Todos los eventos de seguridad* y luego selecciona **Siguiente: revisar y crear**.

1. Selecciona **Crear** para crear la regla de recopilación de datos.

1. Espera un minuto y selecciona **Actualizar** para ver la nueva regla de recopilación de datos en la lista.

### Tarea 3: conectar máquinas Windows que no son de Azure

En esta tarea, agregarás una máquina virtual Windows que no sea de Azure Arc conectada a Microsoft Sentinel.  

   >**Nota:** el conector de datos *Eventos de Seguridad de Windows a través de AMA* requiere Azure Arc para dispositivos que no son de Azure.

1. Asegúrate de que estás en la configuración del conector de datos *Eventos de seguridad de Windows a través de AMA* en el área de trabajo de Microsoft Sentinel.

1. En la pestaña **Instrucciones**, en la sección *Configuración*, edita la *regla de recopilación de datos* **AZWINDCR** seleccionando el icono de *lápiz*.

1. Seleccione **Siguiente: Recursos**, y expanda la *Suscripción* en *Ámbito* en la pestaña *Recursos*.

    >**Sugerencia:** puede expandir toda la jerarquía de *Ámbito* seleccionando el signo ">" antes de la columna *Ámbito*.

1. Expande **RG-Defender** (o el grupo de recursos que has creado) y luego selecciona **WINServer**.

    >**Importante:** si no ves WINServer, consulta la ruta de aprendizaje 3, ejercicio 1, tarea 4 donde has instalado Azure Arc en este servidor.

1. Seleccione **Aplicar**.

1. Selecciona **Siguiente: recopilar** y **Siguiente: revisar y crear**.

1. Una vez que aparezca **Validación superada**, selecciona *Crear*.

## Continúa con el ejercicio 3
