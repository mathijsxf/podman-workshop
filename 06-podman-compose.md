# Podman-compose
Het is natuurlijk heel simpel om een enkele container te maken en beheren maar wanneer er meerdere aan elkaar gekoppelde containers nodig zijn willen we dat graag automatiseren.  
Docker heeft daar de oplossing docker-compose voor gemaakt, deze tool maakt het mogelijk om een YAML manifest te schrijven waarin alle onderdelen van een deployment worden beschreven en geconfigureerd.

Omdat Podman naar compatibiliteit met Docker streeft bestaat er ook een podman-compose tool, deze tool streeft naar volledige compatibiliteit waar mogelijk.  
In een podman-compose file definieer je verschillende zaken, services oftewel containers, netwerken, volumes en nog veel meer.

# Voorbeeld YAML file (staat ook in examples)

```yaml
version: "3.9"  # optional since v1.27.0
services:
  webserver:
    image: nginx
    ports:
      - 8080:80
    networks:
      - frontend
      - backend
    volumes:
      - logvolume01:/var/log
  database:
    image: mariadb
    networks:
      - backend
    environment:
      MARIADB_ROOT_PASSWORD: example
networks:
  frontend: {}
  backend: {}
volumes:
  logvolume01: {}
```

## Bronnen
- https://docs.docker.com/compose/
- https://github.com/containers/podman-compose
- https://compose-spec.io/
- https://github.com/docker/awesome-compose

[Pods >>>](07-pods.md)
