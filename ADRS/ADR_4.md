# Título

Mensajes de alerta estructurados con tipo

# Contexto

- En Chile ocurren a diario varios sismos, por lo que hay una gran cantidad de mensajes todos los días para cada ciudad que esté esperando las alertas.
- Cada nodo suscriptor de las ciudades es casi igual, variando solo el nombre y ubicación geográfica del nodo.
- Los mensajes de alerta contienen poca información, en el caso de que la distancia entre el nodo y el sismo es menor a 500 kilometros, el nodo pide mayor información.
- Se sabe la ubicación de los nodos iniciales que esperaran mensajes del Centro de Alarmas de Sismo.
  
# Decisión

El mensaje de alerta solo contendrá la hora y la distancia del sismo con respecto al nodo y opcionalmente la ubicación del sismo, si es que no se tiene la ubicación del nodo al que se envía el mensaje.

Además, si los nodos de las ciudades están a menos de 500 kilometros, piden más información a una API del Centro de Alerta, esta contendra la siguiente información:

- Ciudad más cercana al sismo
- Ubicación geográfica del sismo
- Hora del sismo
- Magnitud del sismo
  
# Status

Implementado y en revisión

# Consecuencias

## Positivas

1. Eficiencia de entrega de mensajes, pues solo se ajusta un dato en los mensajes por cada nodo.
2. Se envia mensajes a todos los nodos que estén esperando al Centro de Alarmas, pero no todos solicitarán información extra al Centro, lo que es positivo en el caso de que aumente la cantidad de nodos.


## Neutras

1. Pese a que los mensajes contienen poca información, si aumentan la cantidad de nodos, por cada sismo se envía una gran cantidad de mensajes.

## Negativas

1. Si se tiene la ubicación geografica de cada nodo, se puede enviar la distancia con respecto al nodo, en cambio si no se considera guardar la ubicación en el centro, el calculo de la distancia entre el nodo y el sistema se realizará en cada nodo, lo que aumenta la carga en cada nodo, lo que reduce la escalabilidad.
