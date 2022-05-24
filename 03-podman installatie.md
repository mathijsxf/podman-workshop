# Podman installatie

## Mac OS
Installatie van Podman op Mac OS loopt heel simpel via `brew install podman`

Omdat containers niet native op Mac OS draaien zal er net als bij Docker Desktop voor Podman een Virtuele Machine moeten draaien.  
De Podman VM kan aangemaakt worden met `podman machine init` en gestart worden met `podman machine start`

## Fedora
Podman wordt al een tijd standaard meegeleverd met Fedora, hier voldoet een `dnf install podman`

## Ubuntu
Ubuntu heeft een tijd Podman via een externe repo beschikbaar gehad, sinds versie 22.04 is deze echter rechtstreeks beschikbaar vanuit Ubuntu, hier voldoet een `apt install podman`

## Windows
Podman op Windows heeft een nogal complexe installatie, volledige uitleg staat hier, mijn advies is om gewoon lekker een VM te installeren.  
De installatie handleiding voor Windows staat hier https://github.com/containers/podman/blob/main/docs/tutorials/podman-for-windows.md

# Testen na installatie
Na installatie kan je checken of Podman werkt door `podman run --rm hello-world` te draaien.

[Dockerfiles >>>](04-dockerfiles.md)
