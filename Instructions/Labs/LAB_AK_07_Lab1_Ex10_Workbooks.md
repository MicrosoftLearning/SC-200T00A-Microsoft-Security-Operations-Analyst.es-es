---
lab:
  title: 'Ejercicio 10: creación de libros'
  module: Learning Path 7 - Create detections and perform investigations using Microsoft Sentinel
---

# Ruta de aprendizaje 7 - Laboratorio 1 - Ejercicio 10: creación de libros

## Escenario del laboratorio

![Introducción al laboratorio.](../Media/SC-200-Lab_Diagrams_Mod7_L1_Ex10.png)

Usted es un analista de operaciones de seguridad que trabaja en una empresa que ha implementado Microsoft Sentinel. Después de que haya conectado los orígenes de datos a Microsoft Sentinel, puede visualizar y supervisar los datos mediante la adopción de Microsoft Sentinel de Workbooks de Azure Monitor, lo que proporciona versatilidad al crear paneles personalizados. 

Microsoft Azure Sentinel permite crear libros personalizados en los datos y también incluye plantillas de libro integradas que permiten obtener información rápidamente en los datos en cuanto se conecta con un origen de datos.

>**Nota:** Hay disponible una **[simulación de laboratorio interactiva](https://mslabs.cloudguides.com/guides/SC-200%20Lab%20Simulation%20-%20Create%20workbooks)** que le permite realizar sus propias selecciones a su entera discreción. Es posible que encuentre pequeñas diferencias entre la simulación interactiva y el laboratorio hospedado, pero las ideas y los conceptos básicos que se muestran son los mismos. 


### Tarea 1: explorar plantillas de libros

En esta tarea, descubrirás las plantillas de libros de Microsoft Sentinel.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. En el explorador Edge, ve a Azure Portal en https://portal.azure.com.

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta **Correo electrónico de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la **Contraseña de inquilino** que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Iniciar sesión**.

1. En la barra de búsqueda de Azure Portal, escribe *Sentinel* y luego selecciona **Microsoft Sentinel**.

1. Selecciona el área de trabajo de Microsoft Sentinel.

1. Selecciona **Libros** en la hoja de la izquierda *Administración de amenazas*. La pestaña *Plantillas* está seleccionada de forma predeterminada.

1. Busca y selecciona el libro de plantilla **Actividad de Azure**. En el panel derecho, desplázate hacia abajo y selecciona el botón **Ver plantilla**.

1. Revisa el contenido del libro. Muestra información de las operaciones de suscripción de Azure mediante la recopilación y el análisis de los datos del registro de actividad.

1. Cierra el libro seleccionando **X** en la esquina superior derecha.


### Tarea 2: guardar y modificar una plantilla de libro

En esta tarea, guardarás una plantilla de libro y la modificarás.

1. Debes volver a la pestaña **Microsoft Sentinel - Libros - Plantillas**. Desplázate hacia abajo de nuevo y selecciona el botón **Guardar** del libro * Actividad de Azure*. 

1. Deja **Este de EE. UU** como valor predeterminado para *Región* y selecciona **Aceptar**.

1. Selecciona el botón **Ver libro guardado**.

1. Selecciona **Editar** en la barra de comandos para habilitar los cambios en el libro.

1. Desplázate hacia abajo hasta el área *Actividades del autor de la llamada a lo largo del tiempo*. Examina el color de la columna *Actividades*, ya que vamos a dar formato a esas columnas. Selecciona el botón **Editar** debajo de la cuadrícula.

1. Selecciona el botón **Configuración de columna**, que se encuentra a la derecha de la barra de comandos *Ejecutar consulta*. **Sugerencia:** este botón solo aparece si hay datos de la consulta KQL.

1. En la hoja *Editar configuración de columna* que aparece, en *Columnas*, selecciona **Actividades**.

1. Cambia el valor de *Representador de columnas* por **Mapa térmico**. En *Paleta de colores*, desplázate hacia abajo para seleccionar **Categorías de 32 colores**.

1. Seleccione **Guardar y cerrar**. Observa el cambio en la columna *Actividades*.

1. Selecciona **Edición finalizada** en la parte inferior de la consulta (no en el menú superior).

1. Ahora selecciona **Edición finalizada** en el menú superior y selecciona el icono **Guardar**. 

1. Cierra el libro seleccionando **X** en la esquina superior derecha.


### Tarea 3: crear un libro

En esta tarea, crearás un nuevo libro con visualizaciones avanzadas.

1. Debes volver al área **Libros** del portal de Microsoft Sentinel.

1. Selecciona **Agregar libro** para crear un nuevo libro desde cero. 

    >**Nota:** aunque es un nuevo libro, se usa una plantilla de inicio.

1. Para editar el libro, seleccione **Editar**.

1. Selecciona el botón **Editar** situado debajo del primer párrafo del libro.

1. Escribe *# Mi libro* en una nueva línea encima de *## Nuevo libro*.

1. Selecciona **Edición finalizada** en la parte inferior de esta sección, *Edición de elemento de texto: texto - 2*. Observa que el encabezado ahora es más grande y que el nombre cambió.

1. Selecciona **Editar** debajo del único gráfico del gráfico de barras visible.

1. Revisa la instrucción KQL que proporciona una instrucción *union* de recuentos en todas las tablas.

1. Desplázate hacia abajo y selecciona **Edición finalizada** en el menú inferior, para *Editando el elemento de consulta: consulta - 2*.

1. Selecciona los puntos suspensivos **...** junto al botón *Editar* del gráfico del gráfico de barras. Selecciona **+ Agregar** y luego, **Agregar consulta**.

1. Escribe **SecurityEvent** en el cuadro de consulta.

1. Cambia el *Intervalo de tiempo* por **Última hora**.

1. Cambia la *Visualización* por **Gráfico de tiempo**.

1. Selecciona la pestaña **Estilo** en la barra de comandos de la consulta.

1. Selecciona la casilla **Ajustar este elemento a un ancho personalizado**.

1. Establece el *Ancho porcentual* en **25** y el *Ancho máximo* en **25**.

1. Ahora, selecciona la pestaña **Configuración avanzada** en la barra de comandos de la consulta.

1. Selecciona el cuadro **Mostrar icono de actualización cuando no se edite**. 

1. Desplázate hacia abajo y selecciona **Edición finalizada** en el menú inferior, para el nuevo elemento de *Editando el elemento de consulta: consulta - 2*.

1. Desplázate hacia abajo y, en la parte inferior del libro, selecciona **+ Agregar** y después **Agregar consulta**.

1. Escribe **SecurityEvent** en el cuadro de consulta.

1. Cambia el *Intervalo de tiempo* por **Última hora**.

1. Cambia la *Visualización* por **Cuadrícula**:

1. Selecciona **Estilo** en la barra de comandos de la consulta.

1. Selecciona el cuadro **Ajustar este elemento a un ancho personalizado**.

1. Establece el *ancho porcentual* en **75** y el *Ancho máximo* en **75**.

1. Desplázate hacia abajo y selecciona **Edición finalizada** en el menú inferior, para la nueva opción *Editando el elemento de consulta: consulta - 3*.

1. Selecciona **Edición finalizada** en la barra de comandos superior del Libro.

1. Selecciona el icono **Guardar** y cambia el *Título* por **Mi libro**.

1. Selecciona el grupo de recursos **RG-Defender** si es necesario y deja otros valores como predeterminados.

1.  Para confirmar los cambios, selecciona **Aplicar**. 

1. Para cerrar el libro, selecciona la **X** en la parte superior derecha o selecciona **Libros** en el portal de Microsoft Sentinel.

1. En la página *Libros*, selecciona la pestaña **Mis libros**.

1. Selecciona el libro que acabas de crear, **Mi libro**.

1. En el panel derecho, selecciona **Ver libro guardado** para revisar el libro.

## Continúa con el ejercicio 11
