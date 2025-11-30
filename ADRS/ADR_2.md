# Titulo
Patrón Publish-Subscribe

## Contexto
El sistema requiere difundir eventos de sismo desde un único punto de detección (“Notificador de Sismos”) hacia múltiples consumidores regionales que deben reaccionar de forma independiente.  
Fuerzas principales:  
- Cada región solo debe procesar eventos relevantes (distancia < 500 km), por lo que necesita recibir la notificación inicial de forma universal pero decidir localmente.  
- Necesidad de escalabilidad horizontal en consumidores sin impactar al productor.  
- El diagrama muestra explícitamente relaciones <<publisher>> → Messaging System ← <<subscriber>> desde los cinco nodos regionales.  
No existen mecanismos alternativos visibles (ni RPC directo, ni message queue punto a punto, ni broadcasting físico).

## Decisión
Se adopta el patrón **Publish-Subscribe** mediado por un broker central: el publicador envía un único mensaje con datos mínimos al tópico/tema gestionado por el “Messaging System”, y todos los suscriptores regionales están suscritos a dicho tópico para recibir la notificación de forma asíncrona.

## Status
Aceptada e implementado

## Consecuencias

### Positivas
- Comunicación uno-a-muchos eficiente y desacoplada.
- Los suscriptores pueden filtrar localmente sin cargar al publicador ni al broker.
- Soporta fácilmente la adición o eliminación de regiones.

### Neutras
- El patrón no fuerza una tecnología concreta (Kafka, RabbitMQ, Cloud Pub/Sub, etc.), permitiendo migración futura.
- No resuelve por sí solo la tolerancia a particiones de red entre regiones y el centro.

### Negativas
- Single point of failure en el broker y en la red hacia el Warning Center.
- Sin mecanismos visibles de autenticación/autorización, existe riesgo de suscripciones o publicaciones maliciosas.
- Posible pérdida de mensajes si el broker no garantiza durabilidad o exactly-once semantics.

