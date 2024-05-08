---
lab:
  title: 'Ejercicio 4: Conexión de Defender XDR a Microsoft Sentinel mediante conectores de datos'
  module: Learning Path 6 - Connect logs to Microsoft Sentinel
---

# Ruta de aprendizaje 6: Laboratorio1: Ejercicio 4: Conexión de Defender XDR a Microsoft Sentinel mediante conectores de datos

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

Es analista de operaciones de seguridad que trabaja en una empresa que implementó Microsoft Defender XDR y Microsoft Sentinel. Debe prepararse para la plataforma de operaciones de seguridad unificada que conecta Microsoft Sentinel a Defender XDR. El siguiente paso será instalar la solución centro de contenido de Defender XDR e implementar el conector de datos de Defender XDR en Microsoft Sentinel.

### Tarea 1: Conexión de Defender XDR

En esta tarea, implementará el conector de Microsoft Defender XDR.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Microsoft Edge, vaya a Azure Portal en (<https://portal.azure.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. En el menú izquierdo de Microsoft Sentinel, desplázate hacia abajo hasta la sección **Administración de contenido** y selecciona **Centro de contenido**.

1. En *Centro de contenido*, busque la solución ** Microsoft Defender XDR** y selecciónela en la lista.

1. En la página de detalles de la solución *Microsoft Defender XDR*, seleccione **Instalar**.

1. Cuando se complete la instalación, busque la solución **Microsoft Defender XDR** y selecciónela.

1. En la página de detalles de la solución de *Microsoft Defender XDR*, seleccione **Administrar**

>**Nota:** La solución *Microsoft Defender XDR* instala el conector de datos de *Microsoft Defender XDR*, las consultas de búsqueda, los libros y las reglas de análisis.

1. Active la casilla Conector de datos de *Microsoft Defender XDR* y seleccione la **página Abrir conector**.

1. En la sección *Configuración*, en la pestaña *Instrucciones*, **anule la selección** de la casilla para *Desactivar todas las reglas de creación de incidentes de Microsoft para estos productos. Recomendado*, y seleccione el botón **Conectar incidentes y alertas**.

1. Debería recibir un mensaje que indique que la conexión ha sido satisfactoria.

## Has completado el laboratorio
