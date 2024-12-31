---
lab:
  title: 'Ejercicio 1: exploración de registros de Auditoría de Microsoft Purview'
  module: Learning Path 3 - Mitigate threats using Microsoft Purview
---

# Ruta de aprendizaje 3 - Laboratorio 1 - Ejercicio 1: exploración de registros de Auditoría de Microsoft Purview

## Escenario del laboratorio

Eres un analista de operaciones de seguridad que trabaja en una empresa que está implementando Microsoft Defender XDR y Microsoft Purview. Estás ayudando a los compañeros del equipo de cumplimiento de TI a configurar Purview Audit (Estándar) y Auditoría (Premium). El objetivo es garantizar que todos los accesos y modificaciones de los datos de los pacientes en nuestra red de centros sanitarios se registren con precisión para cumplir las normativas de protección de datos sanitarios.

### Tiempo estimado para completar este laboratorio: 15 minutos

### Tarea 1: habilitar registros de Auditoría de Purview

En esta tarea, asignará directivas de seguridad preestablecidas para Exchange Online Protection (EOP) y Microsoft Defender para Office 365 en el portal de seguridad de Microsoft 365.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. Abre el explorador Microsoft Edge.

1. En el explorador Microsoft Edge, ve al portal de Microsoft Defender XDR en (<https://security.microsoft.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

1. En el menú de navegación, expande *Tecnología operativa* y selecciona **Más recursos**.

1. En el panel **Más recursos**, selecciona el botón **Abrir** en el icono de *Microsoft Purview portal*.

1. Cuando se abra Microsoft Purview portal, aparecerá un mensaje sobre el *nuevo Microsoft Purview portal* en la pantalla. Selecciona la opción para aceptar los términos de divulgación del flujo de datos y la declaración de privacidad y, después, selecciona **Probar ahora**.

    ![Captura de pantalla que muestra la pantalla de bienvenida al nuevo Microsoft Purview portal.](../Media/welcome-purview-portal.png)

1. Selecciona **Soluciones** en la barra lateral izquierda y, después, selecciona **Auditar**.

1. En la página de **búsqueda**, selecciona la barra azul **Iniciar grabación de usuarios y actividad de administrador** para habilitar el registro de auditoría.

    ![Captura de pantalla que muestra el botón Iniciar grabación de usuarios y actividad de administrador.](../Media/enable-audit-button.png)

1. Una vez que selecciones esta opción, la barra azul debe desaparecer de esta página.

    >**Nota:** Puede tardar 60 minutos en iniciar la grabación de actividades.

## Has completado el laboratorio
