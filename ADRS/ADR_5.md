# Titulo

Suscriptores filtran mensajes localmente 

# Contexto

- No todos los sismos son relevantes en cada ciudad. 

# Decisión

Los suscriptores reciben todos los mensajes, pero estos se encargan de filtrarlos basados en la proximidad del sismo (500 km). 

# Status

Aprobado e Implementado

# Consecuencias

## Positivas

1. Se reduce el tráfico en la red al enviar mensajes compactos. 

## Neutras

1. Favorece la latencia al solicitar información al endpoint HTTP.

## Negativas

1. Aumenta el procesamiento computacional de los suscriptores

