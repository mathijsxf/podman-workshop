# Podman generate

## podman generate systemd
Omdat Podman containers niet onder een centrale service draaien zullen ze ook niet automatisch starten wanneer het systeem opstart, hier is echter een makkelijke oplossing voor.

Met `podman generate systemd` kan er een systemd manifest voor een container gemaakt worden, dit kan rechtstreeks in een systemd unit file geplaatst worden zoals hieronder te zien.

```
podman generate systemd --new voorbeeldcontainer > /etc/systemd/system/voorbeeldcontainer.service
systemctl daemon-reload
systemctl status voorbeeldcontainer
```

Opvallend is dat hier `--new` gebruikt wordt, hiermee schakel je de systemd unit tussen het starten/stoppen van een bestaande container en het iedere keer opnieuw aanmaken en verwijderen van een container.

## podman generate kube
Naast het genereren van systemd unit files kan je met `podman generate kube` ook Kubernetes manifests genereren, hiermee kan je op een simpele manier een gebouwde pod vanuit Podman exporteren naar Kubernetes.

[Images updaten >>>](10-images-updaten.md)
