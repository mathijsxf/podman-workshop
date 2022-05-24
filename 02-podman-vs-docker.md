# Docker
Wat is Docker?
- de meest bekende container engine, mensen spreken ook veel over "Docker containers"
- bestaat uit een client en server daemon
- containers draaien standaard onder docker service en dus `root` user
- heeft een tool genaamd `docker-compose` om gehele applicatie stacks te bouwen
- maakt gebruik van de runc container runtime
# Podman
Wat is Podman?
- nieuwe container engine, als eerste beschikbaar in Fedora/Red Hat, nu ook in Ubuntu 22.04
- bestaat uit een client en een daemon maar gebruikt deze alleen voor de REST API
- kan containers draaien als meer users dan alleen `root`
- heeft zijn eigen `podman-compose` tool die vergelijkbaar werkt
- kan gebruik maken van OCI compatible runtimes zoals crun, runc, runv

# Bronnen
- https://podman.io/
- https://docs.podman.io/en/latest/
- https://opencontainers.org/

[Podman Installatie](03-podman-installatie.md)
