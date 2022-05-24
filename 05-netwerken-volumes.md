# Netwerken en Volumes

## Netwerken
Containers draaien standaard afgezonderd in virtuele netwerken, binnen deze netwerken kunnen containers elkaar bereiken op basis van naam.  
Deze netwerken hebben hun eigen netwerk subnet en er zijn allerlei andere opties in te stellen.

Er is één default netwerk aanwezig, namelijk het `podman` netwerk, deze is niet te verwijderen om te zorgen dat er altijd een netwerk beschikbaar is .

## Poorten van buiten bereikbaar maken
Om een containerpoort van buiten bereikbaar te maken moet je deze opgeven in de opdracht waarmee je de container aanmaakt, een nginx webserver is bijvoorbeeld met `podman run --name nginx --detach --publish 80:80,443:443 nginx` van buiten bereikbaar, hier kan eventueel nog wel een firewall aanpassing voor nodig zijn.

## Poort ranges
Wanneer een container rootless draait kan deze alleen poorten boven 1024 van buiten bereikbaar maken, root containers kunnen het volledige bereik gebruiken zolang deze beschikbaar zijn.

## Network mode host
In speciale usecases kan het nodig zijn om een container rechtstreeks aan het host netwerk te hangen, dit betekent dat alle poorten die op de container actief zijn van buiten bereikbaar zijn op het adres van de host.  
Dit kan gedaan worden door `--network host` mee te geven in plaats van poorten te publiceren.

# Volumes
Wanneer je in Podman een container aanmaakt zonder volumes te gebruiken zal alle data weg zijn op het moment dat je de container weggooit, om dit op te lossen kan je volumes aanmaken en mounten in een container, wanneer je de container weggooit zal het volume nog steeds bestaan en kan deze weer gekoppeld worden aan de nieuwe aangemaakte container.

De meest simpele manier om je data op te slaan is om een directory te maken voor je applicaties zoals bijvoorbeeld in `/srv/podman/<container>/<directory>` en deze te mounten in de container.

Je kan in Podman ook named volumes maken die je aan containers knoopt, data voor deze volumes wordt opgeslagen in `/var/lib/containers/storage/volumes/`  
Een nieuw volume kan je aanmaken met `podman volume create <naam>`, dit volume kan je bij het starten van een container aankoppelen zoals bijvoorbeeld met `podman run --detach --volume <volumenaam>:/home/testvolume:ro nginx`  
Wanneer je `podman volume rm <naam>` uitvoert zal dit niet mogelijk zijn omdat deze in gebruik is, wanneer je de container verwijdert zal het volume er nog steeds staan en kan deze weer opnieuw gebruikt worden.

# Exporteren/Importeren/Mounten/Kopieren
Volumes kunnen net als volledige containers worden geexporteerd naar tarballs en terug geimporteerd worden.  
Daarnaast is het ook mogelijk om checkpoints te maken van draaiende containers of data naar en vanuit draaiende containers te kopieren.  
Ook is het mogelijk om een filesystem van een volume of container te mounten op het host systeem, bijvoorbeeld met `podman volume mount <volumenaam>`
# Bronnen
- https://podman.io/getting-started/network
- https://docs.podman.io/en/latest/markdown/podman-volume.1.html
- https://docs.podman.io/en/latest/markdown/podman-container-checkpoint.1.html

[Podman Compose >>>](06-podman-compose.md)
