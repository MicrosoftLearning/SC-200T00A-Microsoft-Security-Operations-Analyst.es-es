# Módulo 10: Administración de incidentes en Microsoft Defender XDR

## Administración de incidentes en Microsoft Defender XDR

En esta tarea, explorará las funcionalidades de administración de incidentes en Microsoft Defender XDR, incluida la investigación de incidentes, las acciones de respuesta y las características de colaboración.

>**Importante:** Este laboratorio está diseñado para ejecutarse en el entorno de demostración *Zava/Alpine Ski House*. Se necesitan las credenciales adecuadas para el acceso.

### Áreas clave descritas

- Panel de incidentes
- Investigación de incidentes
- Accesiones de Evidencia y respuesta
- Flujos de trabajo de administración de incidentes
- Colaboración y documentación

1. Si aún no está en el portal de Microsoft Defender en el explorador, vaya al portal de Microsoft Defender en (<https://security.microsoft.com>) e inicie sesión con las credenciales asignadas.

1. En el panel de navegación de la izquierda, expanda la sección **Investigación y respuesta** y seleccione **Incidentes y alertas** > **Incidentes**. Esto mostrará la cola de incidentes con todos los incidentes activos en el entorno.

1. Revise la interfaz de cola de incidentes:
   - Opciones de filtro (Estado, Asignado a, Etiquetas, etc.)
   - Indicadores de prioridad y gravedad de incidentes
   - Orígenes de servicio (Defender para punto de conexión, Office 365, etc.)
   - Marcas de tiempo de última actividad

1. Seleccione un incidente en la lista para abrir la página de detalles del incidente. Observe la información general del incidente en la que se muestra lo siguiente:
   - Escala de tiempo de incidentes
   - Recursos afectados (usuarios, dispositivos, buzones)
   - Detalles y correlación de las alertas
   - Tácticas y técnicas de MITRE ATT&CK

## Proceso de la investigación del incidente

1. En los detalles del incidente, explore la pestaña **Alertas** para ver todas las alertas relacionadas que componen este incidente.
   - Revise la correlación y agrupación automática de alertas
   - Examine la evidencia de alertas y artefactos
   - Anote los niveles de confianza y los orígenes de detección

1. Seleccione la pestaña **Dispositivos** para ver todos los puntos de conexión afectados:
   - Nivel de riesgo del dispositivo
   - Puntuaciones de prioridad de la investigación
   - Escala de tiempo del dispositivo de las actividades
   - Acciones de respuesta disponibles

1. Vaya a la pestaña **Usuarios** para revisar las cuentas de usuario afectadas:
   - Evaluaciones de riesgos del usuario
   - Actividades y anomalías de inicio de sesión
   - Indicadores de peligro para cuentas

1. Examine en la pestaña **Buzones** (si procede) los incidentes relacionados con el correo electrónico:
   - Detalles de entrega y flujo de correo electrónico
   - Análisis de datos adjuntos y direcciones URL
   - Evaluación del impacto del destinatario

## Análisis de evidencia y acciones de respuesta

1. En la pestaña **Evidencia**, revise todas las pruebas recopiladas:
   - Archivos y códigos hash de archivos
   - Direcciones IP y dominios
   - Procesos y claves del Registro
   - Mensajes de correo electrónico y direcciones URL

1. Para cada elemento de evidencia, explore las acciones disponibles:
   - **Enviar para su análisis**: envío de archivos sospechosos a Microsoft para un análisis profundo
   - **Agregar a indicadores**: creación de indicadores de amenazas personalizados
   - **Bloquear o permitir**: realizar acciones de protección inmediatas

1. Para mostrar las acciones de respuesta, seleccione un dispositivo y elija entre las acciones disponibles:
   - **Aislar el dispositivo**: desconecte el dispositivo de la red al tiempo que mantiene la conectividad con Defender
   - **Ejecutar examen antivirus**: inicie el examen completo o rápido
   - **Recopilar paquete de investigación**: recopile datos forenses
   - **Restringir la ejecución de la aplicación**: limite la ejecución de la aplicación en el dispositivo

## Administración de incidentes y flujo de trabajo

1. Practique la asignación y administración de incidentes:
   - **Asignar incidente**: se asigna a analistas o equipos de seguridad específicos
   - **Cambiar estado**: actualice de Activo a Resuelto u otros estados
   - **Agregar etiquetas**: aplique etiquetas personalizadas para la categorización y el seguimiento
   - **Establecer clasificación**: marque como Verdadero positivo, Falso positivo o Informativo

1. Explore el flujo de trabajo de administración de incidentes:
   - Revise la pestaña **Comentarios** para la colaboración de analistas
   - Compruebe en la pestaña **Historial** todas las acciones realizadas
   - Use la pestaña **Resumen** para crear informes ejecutivos

1. Demuestre el proceso de calificación de incidentes:
   - **Verdadero positivo**: actividad malintencionada confirmada que requiere respuesta
   - **Informativo**: actividad esperada que ha desencadenado la detección
   - **Falso positivo**: actividad benigna marcada incorrectamente

## Características avanzadas de incidentes

1. Explore los resultados de **Investigación automatizada** (si está disponible):
   - Revisión de los resultados de la investigación controlada por IA
   - Examen de las acciones recomendadas
   - Aprobación o rechazo de la corrección automatizada

1. Vaya a la integración con **Análisis de amenazas**:
   - Vincule incidentes a campañas de amenazas conocidas
   - Revise el contexto de inteligencia sobre amenazas
   - Acceda a informes e IOC de analistas

1. Demuestre el impacto de las **reglas de detección personalizadas**:
   - Muestre cómo contribuyen las reglas personalizadas a la creación de incidentes
   - Revise la eficacia de las reglas y las oportunidades de optimización
   - Acceda a opciones de prueba y modificación de reglas

## Informes y métricas de incidentes

1. Acceda a funcionalidades de creación de informes de incidentes:
   - Vaya a **Informes** > **Informe de seguridad**
   - Revise tendencias y estadísticas de incidentes
   - Genere informes de resumen ejecutivos

1. Explore las métricas de incidentes y los KPI:
   - Tiempo medio de detección (MTTD)
   - Tiempo medio de respuesta (MTTR)
   - Tendencias de volumen de incidentes
   - Frecuencia de falsos positivos

1. Configure la notificación de incidentes:
   - Configure alertas por correo electrónico para incidentes de alta prioridad
   - Configure la integración de equipos para la respuesta colaborativa
   - Cree reglas de notificación personalizadas basadas en criterios de incidentes

## Procedimientos recomendados para la administración de incidentes

1. **Estrategia de priorización**:
   - Céntrese primero en incidentes de alta gravedad
   - Considere el impacto empresarial y la importancia de los recursos
   - Use la puntuación de riesgo para guiar los esfuerzos de investigación

1. **Estándares de documentación**:
   - Mantenga notas detalladas de la investigación
   - Documente todas las acciones de respuesta realizadas
   - Registre las lecciones aprendidas y las oportunidades de mejora

1. **Colaboración en equipo**:
   - Use esquemas de clasificación y etiquetado coherentes
   - Establezca procedimientos de escalación claros
   - Implemente procesos de revisión de incidentes periódicos

1. **Mejora continua:**
   - Revise periódicamente las tasas de falsos positivos
   - Ajuste las reglas de detección en función de los resultados de los incidentes
   - Actualice cuadernos de estrategias de respuesta a incidentes en función de los resultados

## integración con Microsoft Azure

1. Si Microsoft Sentinel está conectado, muestre la administración unificada de incidentes:
   - Correlación de incidentes multiplataforma
   - Experiencia de investigación unificada
   - Inteligencia sobre amenazas e indicadores compartidos

1. Muestre características del incidente específicas de Sentinel:
   - Visualización del grafo de investigación
   - Automatización de cuadernos de estrategias personalizados
   - Búsqueda avanzada de amenazas entre entornos

## Has completado la demostración

---

**Recursos adicionales:**

- [Administración de incidentes de Microsoft Defender XDR](https://docs.microsoft.com/microsoft-365/security/defender/manage-incidents)
- [Cuadernos de estrategias de respuesta ante incidentes](https://docs.microsoft.com/security/compass/incident-response-playbooks)
- [Marco MITRE ATT&CK](https://attack.mitre.org/)
