# Titulo
Estilo Event-Driven con Topología Broker

## Contexto
El sistema de alerta temprana de sismos debe notificar de forma rápida y asíncrona la detección de un evento sísmico a múltiples nodos regionales distribuidos geográficamente en Chile (Arica, Coquimbo, Valparaíso, Concepción y Punta Arenas).  
Las fuerzas principales son:  
- Necesidad de baja latencia en la notificación inicial (segundos son críticos en early warning).  
- Desacoplamiento entre el productor central de eventos y los consumidores regionales.  
- Optimización de ancho de banda: solo se envía información mínima al principio.  
- Existencia de un único componente central “Messaging System” que recibe la publicación y distribuye a todos los suscriptores (evidenciado en el diagrama de despliegue).  
No se observan alternativas como request/response directo o colas punto a punto.

## Decisión
Se adopta el estilo arquitectónico **event-driven** utilizando una **topología broker**, donde el componente “Messaging System” actúa como broker central para mediar la comunicación publish/subscribe entre el “Notificador de Sismos” y los cinco suscriptores regionales.

## Status
Aceptada e implementada

## Consecuencias

### Positivas
- Alto desacoplamiento espacial y temporal entre publicador y suscriptores.
- Facilita la adición futura de nuevos nodos regionales sin modificar el publicador.
- Permite notificación push inmediata con payload mínimo.

### Neutras
- La elección tecnológica del broker no está especificada (podría ser RabbitMQ, Kafka, NATS, etc.), dejando abierta la futura evolución.

### Negativas
- El broker (“Messaging System”) se convierte en single point of failure crítico.
- Compromete el objetivo de 99.9997 % de uptime si no se implementa alta disponibilidad.
- Depende totalmente de la conectividad de red hacia el Warning Center.
