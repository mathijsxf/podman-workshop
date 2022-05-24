# Kernel namespaces
Wat zijn kernel namespaces?
- kernel feature
- maakt het mogelijk om het systeem op te splitsen op verschillende onderdelen
- enkele voorbeelden van namespaces
  - PID namespaces voor scheiding van proces ID's
  - user namespaces voor de scheiding van userbeheer
  - mount namespaces voor mount points, vergelijkbaar met chroot
  - net namespaces voor de scheiding op netwerk niveau
  - andere namespaces: cgroup, IPC, UTS, time

## Handige commando's

- alle gebruikte kernel namespaces op een systeem zijn te vinden met `lsns`
- alle cgroups op het systeem kunnen bekeken worden met `systemd-cgls`
- met `systemd-cgtop` krijg je een `top` stijl overzicht van cgroups

## Network namespace voorbeeld

```sh
# maak nieuwe network namespace
ip netns add workshop

# voeg localhost interface toe en check of deze in network namespace bestaat
ip netns exec workshop ip link set dev lo up
ip netns exec workshop ip link

# maak virtuele interface aan
ip link add veth0 type veth peer name veth1
# beide interfaces bestaan nu nog alleen op het systeem
ip link

# voeg veth1 toe aan workshop namespace en check of deze verschijnt binnen de namespace
ip link set veth1 netns workshop
ip netns exec workshop ip link

# stel een IP in op de veth1 interface en breng deze naar up state
ip netns exec workshop ip addr add 10.1.1.1/24 dev veth1
ip netns exec workshop ip link set dev veth1 up

# stel een IP in op de veth0 interface en breng deze up
ip addr add 10.1.1.2/24 dev veth0
ip link set dev veth0 up

# check of je beide richtingen op kan pingen
ping -c3 10.1.1.1
ip netns exec workshop ping -c3 10.1.1.2

# verwijder network namespace
ip netns delete workshop
```

# Cgroups
Wat zijn Control Groups (cgroups)?
- kernel feature sinds 2007
- geven de mogelijkheid om systeemresources in te delen en om limieten en prioriteit te configureren

# Containers
Wat zijn containers?
- Containers zijn afgezonderde proces omgevingen
- de scheiding die Containers mogelijk maakt word verzorgd door kernel namespaces
- Containers hebben hun eigen mount points, network interfaces, user ID's, process ID's, etcetera
- Containers maken gebruik van vooraf gebouwde images als basis, deze bevatten bijvoorbeeld applicaties waarop mappen en bestanden gemount kunnen worden wanneer de container wordt uitgevoerd.

# Bronnen
- https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction
- https://thenewstack.io/linux-cgroups-v2-brings-rootless-containers-superior-memory-management/

[Podman vs Docker](02-podman-vs-docker.md)
