# Cockpit
Cockpit is een web beheer omgeving die standaard met Fedora en Red Hat Linux beschikbaar is, dit project heeft de afgelopen jaren aardig wat vooruitgang geboekt.
Het is dus heel simpel om Cockpit te installeren, mocht het nog niet in de VM geinstalleerd zijn kan dat met onderstaande opdrachten gedaan worden.

`dnf install cockpit cockpit-podman`

`systemctl enable cockpit.socket`

Browse na installatie naar https://<VM IP>:9090, mocht deze niet werken dan zal de firewall open gezet moeten worden, dit kan met `firewall-cmd --permanent --add-service=cockpit` en `firewall-cmd --reload`.

Accepteer tijdens het verbinden self signed certificaat van Cockpit, login met root of andere user, cockpit heeft een Podman Containers sectie waarin je Podman kan beheren.

# Bronnen
- https://cockpit-project.org/

[Buildah en Skopeo >>>](14-buildah-and-skopeo.md)
