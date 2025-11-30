# Titulo

Arquitectura monolítica en el sistema de Mensajeria

# Contexto

- Los componentes principales deben estar en el Centro de Alertas de Sismo, el centro se encargará de su mantención y funcionamiento.
- Todas las ciudades que necesiten utilizar el servicio deben ejecutar su propio componente para que se conecte al Centro de Alertas.
- Los datos de sismos deben ser similares en todas las ciudades que reciban los mensajes de alerta, lo único que debería cambiar es la distancia con respecto del sismo de la ciudad.

# Decisión

Un notificador de sismos en el Centro de Alerta que, por medio de un sistema de mensajería, envía un mensaje a cada componente que esté esperando en el canal de mensajes y que, de ser necesario, solicita más información al Centro.

# Status

Aprobado e Implementado

# Consecuencias

## Positivas

1. Todo el sistema, excepto los que reciben los mensajes en las ciudades, está en un mismo ambiente, lo que hace que la mantención sea sencilla.
2. Los datos son consistentes al solo estar en el Centro de Alerta.


## Neutras

1. El sistema es rápido en la entrega de mensajes, pues es simple y solo se maneja en un lugar, en vez de comunicarse en varios componentes separados.
2. Si deja de funcionar el componente de una ciudad, no afecta al resto de ciudades.


## Negativas

1. El rendimiento se puede ver afectado es cuanto más ciudades tengan un componente que espere mensajes de alerta, pues el Centro debe enviar un mensaje a cada componente.
2. Si muchas ciudades piden mayor información después de recibir el mensaje, puede haber un cuello de botella, pues solo hay un componente HTTP que recibe las peticiones.
3. Si no hay un respaldo para los sistemas del Centro de Alarmas, si se caen compromente el **uptime steady**, pues gran parte del sistema se concentra en el centro.
