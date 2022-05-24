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

# Bronnen
- https://podman.io/getting-started/network

[Podman Compose >>>](06-podman-compose.md)
