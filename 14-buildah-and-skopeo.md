# Containers
Podman is onderdeel van een verzameling tools die ontwikkeld wordt vanuit een centrale "Containers" organisatie, deze organisatie richt zich op het ontwikkelen van tools om met containers te werken.

# Buildah
Het is met `podman build` mogelijk om containers te bouwen, een meer gespecialiseerde tool om OCI compliant containers te bouwen is echter Buildah.  
https://github.com/containers/buildah/blob/main/README.md

Podman en Buildah hebben dus verschillende usecases, een duidelijk verschil tussen Podman en Buildah is dat wanneer je `buildah run` aanroept je de Dockerfile RUN actie uitvoert terwijl je met Podman een nieuwe container opstart.  
Met Buildah kan je via terminal opdrachten stap voor stap dezelfde acties uitvoeren die je anders in een Dockerfile zou beschrijven, buildah kan echter ook gewoon containers bouwen vanuit Dockerfiles.

# Skopeo
Skopeo is een tool waarmee je met images en registries kan werken, bijvoorbeeld het kopieren van images tussen registries of het inspecteren van images en informatie vergaren over lagen waar deze uit bestaan.

# Bronnen
- https://github.com/containers
- https://opencontainers.org/
- https://docs.docker.com/engine/reference/builder/#run
- https://buildah.io/
- https://github.com/containers/skopeo
