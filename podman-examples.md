# nginx voorbeeld

```sh
podman run --name nginx --detach --volume ~/<git_repo_locatie>/data/nginx/www:/usr/share/nginx/html:ro --publish 8080:80 nginx
```

```sh
podman run --name nginx --rm --tty --interactive --volume ~/<git_repo_locatie>/data/nginx/www:/usr/share/nginx/html:rw --publish 8080:80 --entrypoint /bin/bash nginx
```

# busybox

```sh
podman run --tty --interactive --name busybox --pod zabbix busybox
```
