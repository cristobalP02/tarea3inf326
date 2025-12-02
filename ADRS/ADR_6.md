# Titulo

Acoplamiento de componentes en el centro de alarmas

# Contexto

- El componente Publisher, el sistema de mensajes y el endpoint HTTP necesitan comunicarse rápidamente. 
- Se necesita disminuir la complejidad de despliegue.

# Decisión

Se despliegan los componentes core del sistema en la misma locación física. 

# Status

Aprobado e Implementado

# Consecuencias

## Positivas

1. Simplifica el despliegue inicial
2. Reduce la latencia entre los componentes core del sistema. 
 
## Neutras


## Negativas

1. El estar ejecutándose en la misma base física produce un único punto de falla.
2. Al estar todo junto, existe el riesgo de ser atacados por usuarios externos.