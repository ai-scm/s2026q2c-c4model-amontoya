# Ejercicio de Modelado Arquitectónico: C4 Model para Control de Dailies en MS Teams

## Introducción

### ¿Qué entendí de los niveles C1, C2 y C3 del modelo C4?

El modelo C4 es una forma de representar una arquitectura de software utilizando distintos niveles de detalle. Su objetivo es facilitar la comprensión del sistema tanto para perfiles técnicos como no técnicos, permitiendo analizar la solución desde una visión general hasta una visión más interna de su funcionamiento.

**C1 - Contexto:** muestra el sistema desde una perspectiva de alto nivel, identificando los actores que interactúan con él y los sistemas externos con los que se comunica. Su propósito es responder qué hace el sistema y quién lo utiliza.

**C2 - Contenedores:** descompone el sistema principal en sus grandes bloques de ejecución o almacenamiento, tales como aplicaciones, bases de datos, APIs o servicios externos. Su propósito es mostrar cómo se distribuyen las responsabilidades dentro de la solución.

**C3 - Componentes:** profundiza en uno de los contenedores definidos en el nivel anterior y muestra los principales componentes internos que implementan la lógica del negocio. Permite comprender cómo colaboran las diferentes partes para cumplir los requerimientos funcionales.

---

## Justificación de la arquitectura propuesta

La arquitectura fue diseñada buscando simplicidad, facilidad de implementación y una integración natural con Microsoft Teams. Debido a que todos los usuarios interactúan diariamente desde Teams, se decidió utilizar esta plataforma como único punto de contacto con el sistema, evitando la necesidad de desarrollar una aplicación web adicional y reduciendo la complejidad para los usuarios finales.

Para la infraestructura se optó por servicios administrados de AWS, utilizando API Gateway para recibir las solicitudes provenientes de Teams, AWS Lambda para implementar la lógica de negocio, DynamoDB para almacenar reportes y usuarios, y EventBridge para programar tareas automáticas como recordatorios, validaciones de cumplimiento y publicación de resúmenes diarios. Esta arquitectura serverless minimiza la administración de infraestructura, reduce costos operativos y resulta adecuada para una solución cuyo volumen de procesamiento depende principalmente de eventos puntuales durante la jornada laboral.

Dentro del backend se separaron claramente las responsabilidades mediante componentes especializados. El sistema cuenta con módulos para recibir reportes, validar incumplimientos, detectar posibles bloqueos cuando un integrante reporta la misma actividad durante varios días consecutivos, generar resúmenes y enviar notificaciones. Esta separación facilita el mantenimiento, mejora la comprensión de la solución y permite extender funcionalidades futuras sin afectar significativamente el resto del sistema.

