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

# zabbix in pod

## maak pod voor Zabbix
podman pod create --name zabbix --publish 8080:8080,10051:10051

## maak Mariadb container
```sh
podman run --name mariadb --detach --pod zabbix --env MARIADB_USER="admin" --env MARIADB_PASSWORD="podmanws" --env MARIADB_ROOT_PASSWORD="podmanws" mariadb:latest
```

## Open terminal in container
```sh
podman exec -ti mariadb /bin/bash
```

## check draaiende processen
```sh
top
```

## maak verbinding met database
```sh
mysql -uroot -p
```

# Zabbix server
```sh
podman run --detach --name zabbix-server --pod zabbix --env MYSQL_ROOT_PASSWORD="podmanws" --env DB_SERVER_HOST="127.0.0.1" --env MYSQL_USER="admin" --env MYSQL_PASSWORD="podmanws" zabbix/zabbix-server-mysql:alpine-trunk
```
## Logging volgen
```sh
podman logs -f zabbix-server
```

# Zabbix web frontend
```sh
podman run --detach --name zabbix-web --pod zabbix --env ZBX_SERVER_HOST="localhost" --env PHP_TZ="Europe/Amsterdam"  --env DB_SERVER_HOST="127.0.0.1" --env MYSQL_USER="admin" --env MYSQL_PASSWORD="podmanws" zabbix/zabbix-web-nginx-mysql:alpine-trunk
```

## test zabbix web
Open browser en ga naar http://localhost:8080, login met Admin/zabbix
