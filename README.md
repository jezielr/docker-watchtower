## Propósito

Watchtower es un servicio de automatización de ciclo de vida de contenedores. Se encarga de monitorear continuamente el demonio de Docker en busca de nuevas versiones de las imágenes en los registros remotos (Docker Hub, GHCR, etc.), actualizando automáticamente los contenedores en ejecución e inyectando las nuevas capas sin perder configuraciones ni volúmenes.


## Consumo de recursos

Impacto en Recursos: Ultra ligero. Consumo aproximado de 10 a 15 MB de RAM y 0% CPU en estado de reposo.


## Optimización

Optimización de Almacenamiento: Con la directiva WATCHTOWER_CLEANUP=true, elimina de forma inmediata las imágenes obsoletas (dangling images), evitando que la tarjeta SD o disco SSD se llene de espacio desperdiciado.

## Monitoreo

Para monitorear los contenedores se debe agregar esta linea

```bash
labels:
  - "com.centurylinklabs.watchtower.enable=true"
```

## Verificar versión actualizada de las imagenes
```bash
docker logs watchtower | grep -E "Found new|Updated"
```

## Verificar la versión de la imagen

```bash
# Para MeTube u otros proyectos en GHCR/DockerHub
docker inspect --format '{{ index .Config.Labels "org.opencontainers.image.version" }}' metube

# Si el desarrollador usó etiquetas personalizadas de build
docker inspect --format '{{ json .Config.Labels }}' metube | jq
```
