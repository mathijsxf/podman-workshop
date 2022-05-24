# Ansible
Er is een Ansible Galaxy collection beschikbaar voor Podman, de modules hierin geven je de mogelijkheid alles met betrekking tot container workloads te beheren op een host.  
Meer informatie over welke modules beschikbaar zijn kan gevonden worden in de Ansible documentatie op https://docs.ansible.com/ansible/latest/collections/containers/podman/index.html

# Installatie
Ansible installeer je met `dnf install ansible`, hierna heb je `ansible-galaxy` tot je beschikking, hiermee kan je de collection installeren met de volgende opdracht `ansible-galaxy collection install containers.podman`  
Hierna kan je bijvoorbeeld met `ansible -m containers.podman.podman_image_info localhost` informatie opvragen van de images die aanwezig zijn op de host.

[Cockpit >>>](13-cockpit.md)
