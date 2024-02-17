 **No usar. Temporalmente fuera de servicio.**

# Ruta de aprendizaje 6 - Laboratorio 1 - Ejercicio 4: conexión de inteligencia sobre amenazas a Microsoft Sentinel mediante conectores de datos

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod6_L1_Ex4.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Debes aprender a conectar los datos de registro de los numerosos orígenes de datos de la organización. Por último, conecta una fuente de inteligencia sobre amenazas para mejorar la capacidad de detectar y priorizar las amenazas conocidas.

### Tarea 1: establecer una conexión de Inteligencia sobre amenazas

En esta tarea, conectarás un proveedor de inteligencia sobre amenazas con el conector Inteligencia sobre amenazas - TAXII.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador, ve a Azure Portal en (<https://portal.azure.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel que has creado anteriormente.

1. En la pestaña Conectores de datos busca el conector **Inteligencia sobre amenazas - TAXII**.

1. En la hoja Azure Information Protection, selecciona **Abrir página del conector** en la hoja de información del conector.

1. En el área *Configuración*, en el campo **Nombre descriptivo (para servidor),** escribe *PhishURLs.*

1. Para la dirección URL raíz de la API, escribe <https://limo.anomali.com/api/v1/taxii2/feeds/>

1. Escribe **107** como Id. de colección.

1. Escribe **guest** como nombre de usuario.

1. Escribe **guest** para la contraseña.

1. Ahora selecciona el botón **Agregar**.  Las direcciones URL de suplantación de identidad se extraerán y rellenarán la tabla ThreatIntelligenceIndicator.

>**Nota:** Si quieres agregar otra colección, abre <https://limo.anomali.com/api/v1/taxii2/feeds/collections/> en el explorador Edge y usa el nombre de usuario y la contraseña guest para revisar los distintos identificadores disponibles.

## Has completado el laboratorio
