# Pods
Pods zijn binnen Kubernetes en Podman de kleinste basiseenheid voor deployments, pods bestaan uit één of meerdere containers.

De basis van een pod bestaat uit een enkele container, namelijk de pause container.  
Deze container reserveert de namespaces die door alle containers in de pod worden gedeeld.

Containers binnen pods delen meerdere namespaces, een daarvan is de network namespace.  
Voordeel hiervan is dat containers elkaar kunnen bereiken via `localhost` of `127.0.0.1`

# Poorten buiten pod bereikbaar maken
Om poorten buiten een pod bereikbaar te maken moeten deze worden toegevoegd aan de opdracht waarmee de pod wordt gemaakt, dus bijvoorbeeld.  
`podman pod create --name webapplication --publish 80:80,443:443`
Wat opvalt bij deze opdracht is dat de poorten ieder twee keer worden vermeld, wanneer er een enkele poort staat zal er een random host poort worden gekozen die naar de opgegeven poort in de pod wordt doorgestuurd.

# Zabbix in pod
## Pod
Maak een pod voor Zabbix
```sh
podman pod create --name zabbix --publish 8080:8080,10051:10051
```

## MariaDB
Maak binnen de pod een Mariadb container aan voor Zabbix
```sh
podman run --name mariadb --detach --pod zabbix --env MARIADB_USER="admin" --env MARIADB_PASSWORD="podmanws" --env MARIADB_ROOT_PASSWORD="podmanws" mariadb:latest
```
Open terminal in container
```sh
podman exec -ti mariadb /bin/bash
```
Binnen de container draaien er heel weinig processen
```sh
top
```
Maak verbinding met database, gebruik het wachtwoord `podmanws`
```sh
mysql -uroot -p
```
Dit werkt allemaal naar behoren, als je met Ctrl+D de container verlaat kan je met `podman logs mariadb
` de logging van de container inzien.

## Zabbix server
Maak nu de Zabbix server container, deze zal verbinden naar de Mariadb container op 127.0.0.1
```sh
podman run --detach --name zabbix-server --pod zabbix --env MYSQL_ROOT_PASSWORD="podmanws" --env DB_SERVER_HOST="127.0.0.1" --env MYSQL_USER="admin" --env MYSQL_PASSWORD="podmanws" zabbix/zabbix-server-mysql:alpine-trunk
```
Na het aanmaken kan je meteen de logging volgen met onderstaande opdracht
```sh
podman logs -f zabbix-server
```

## Zabbix web
Als laatste zal de Zabbix web container toegevoegd moeten worden, wat opvalt is dat er in deze Pod setup geen poort opengezet hoeft te worden aangezien we dat al bij het aanmaken van de Pod hebben gedaan.
```sh
podman run --detach --name zabbix-web --pod zabbix --env ZBX_SERVER_HOST="localhost" --env PHP_TZ="Europe/Amsterdam"  --env DB_SERVER_HOST="127.0.0.1" --env MYSQL_USER="admin" --env MYSQL_PASSWORD="podmanws" zabbix/zabbix-web-nginx-mysql:alpine-trunk
```
Nadat deze container opgestart is kan je deze openen in de browser door naar http://localhost:8080 of het IP adres van de VM te gaam, hier kan eventueel nog een firewall tussen zitten, dit is op te lossen met `firewall-cmd --permanent --add-port=8080/tcp` en dan `firewall-cmd --reload`.
Je kan bij Zabbix inloggen met Admin/zabbix

# Bronnen
- https://www.ianlewis.org/en/almighty-pause-container

[Podman API en Remote Client >>>](08-podman-api-remote-client.md)
