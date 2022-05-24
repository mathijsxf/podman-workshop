# Container update

Met docker is het standaard om een complete container weg te gooien en opnieuw aan te maken wanneer er een image update beschikbaar is.  
Als alternatief wordt er veel van Watchtower gebruik gemaakt (https://github.com/containrrr/watchtower) om dit te automatiseren.

Podman kan dit echter helemaal zelf afhandelen.  
Voeg voor het mogelijk maken van automatische updates in podman het volgende toe aan de `podman run` opdracht waarmee je de container start.

`--label "io.containers.autoupdate=registry"`

Hierna is het mogelijk om met de `podman auto-update` opdracht alle containers met dit label automatisch te updaten.  
Met `podman auto-update --dry-run` kan je zien of er updates voor containers beschikbaar zijn.

Het updaten wordt ook automatisch uitgevoerd door de `podman-auto-update.service` systemd unit, deze kan met de `podman-auto-update.timer` ingepland worden, de planning staat dan standaard op dagelijks (middernacht) ingesteld.

Mocht het updaten niet goed verlopen kan er ook een rollback worden gedaan met `podman auto-update --rollback`

[Rootless containers >>>](11-rootless.md)
