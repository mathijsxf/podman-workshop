# Podman REST API en client
Zoals eerder verteld heeft Podman geen daemon die de containers beheert, echter heeft deze wel een REST API die vergelijkbaar is met die van Docker.

Je kan met de Podman client op afstand verbinding maken met een Podman instance op een server, één methode om dit te doen is om dit via SSH te tunnelen naar de podman socket, dit kan als volgt.  
Schakel op de VM de `podman.socket` in met `systemctl enable --now podman.socket`.  
Voeg een verbinding toe op je lokale systeem, dit doe je met de volgende opdracht `podman system connection add workshop ssh://root@<VM IP>:22/run/podman/podman.sock`  
Hierna kan je met `podman --connection workshop info` informatie van het remote systeem opvragen.  
Aanwezige remote connections kan je inzien met `podman system connection list`, met `podman system connection default <naam>` kan je een andere standaard remote verbinding selecteren.

## Podman REST API service
Het is ook mogelijk om de Podman REST API service via een TCP poort beschikbaar te maken, dit kan bijvoorbeeld handmatig met de opdracht `podman system service --time=0 tcp://localhost:8888`

[Podman systemd units en Kubernetes manifests >>>](09-systemd-units-kube-manifests.md)
