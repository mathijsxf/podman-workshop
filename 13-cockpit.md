# Cockpit
Mocht Cockpit nog niet in de VM geinstalleerd zijn kan dat met onderstaande opdrachten gedaan worden.

`dnf install cockpit cockpit-podman`

`systemctl enable cockpit.socket`

Browse na installatie naar https://<VM IP>:9090, mocht deze niet werken dan zal de firewall open gezet moeten worden, dit kan met `firewall-cmd`.

Accepteer tijdens het verbinden self signed certificaat van Cockpit, login met root of andere user, cockpit heeft een Podman Containers sectie waarin je Podman kan beheren.

[Buildah en Skopeo](14-buildah-skopeo.md)
