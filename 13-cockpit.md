# Cockpit
Cockpit is een web beheer omgeving die standaard met Fedora en Red Hat Linux beschikbaar is, dit project heeft de afgelopen jaren aardig wat vooruitgang geboekt.
Het is dus heel simpel om Cockpit te installeren, mocht het nog niet in de VM geinstalleerd zijn kan dat met onderstaande opdrachten gedaan worden.

```sh
# installeer cockpit en cockpit-podman
dnf install cockpit cockpit-podman
# schakel socket in
systemctl enable --now cockpit.socket

# open firewall voor cockpit service
firewall-cmd --permanent --add-service=cockpit
firewall-cmd --reload
```

Browse na installatie naar https://<VM IP>:9090, accepteer tijdens het verbinden self signed certificaat van Cockpit, login met root of andere user, cockpit heeft een Podman Containers sectie waarin je Podman kan beheren.
Het enige wat hier nog ontbreekt is het aanmaken van Pods, dit dient te gebeuren op de command-line waarna de Pod zal verschijnen in Cockpit.

# Bronnen
- https://cockpit-project.org/

[Buildah en Skopeo >>>](14-buildah-and-skopeo.md)
