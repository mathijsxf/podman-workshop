# Dockerfiles

Je kan zelf container images bouwen, dit doe je met een bouw manifest hierin geef je aan hoe de container er uit moet zien.

De filename voor deze manifests is `Dockerfile`, hierin plaats je de instructies die door Docker of in ons geval Podman worden uitgevoerd.

## Simpele nginx container
Als eerste hebben we een geprepareerde `Dockerfile` klaarstaan in `examples/nginx-container`  
Deze container heeft als sources de standaard nginx container, dit doe je met `FROM nginx`  
Tijdens het bouwen van de container willen we ook de inhoud van de `www` map vullen, dit doen we met de `COPY www /usr/share/nginx/html` opdracht.

De container kan je bouwen door in de directory waar de `Dockerfile` staat de volgende opdracht uit te voeren.

`podman build -t workshop/nginx .`

Na het bouwen zal je zien dat deze verschijnt in de lijst van container images (`podman image ls`), deze zal als registry naam `localhost`

## Starten container

Deze container kunnen we nu ook starten door `podman run --detach --publish 8080:80 localhost/workshop/nginx` uit te voeren.  
Met `podman container ls` zal je zien dat deze container actief is, hij heeft een random containernaam gekregen en hostpoort 8080 is doorgelusd naar containerpoort 80

## Configureren (issues op Mac OS met mount)

Meestal wil je ook nginx configureren, het beste is om deze dan te mounten op het moment dat je de container gaat draaien maar we willen dan wel even de bestaande configuratie lenen.  
Deze kopieren we dan gewoon lekker uit de draaiende container naar onze lokale opslag met `podman cp <containernaam>:/etc/nginx/nginx.conf nginx.conf`

Nadat we deze naar het lokale filesysteem hebben gekopieerd kunnen we de container weggooien met `podman rm -f <containernaam>`  
En kunnen we de container opstarten met onze eigen configuratie die we kunnen aanpassen zonder iedere keer het image opnieuw te hoeven bouwen door nogmaals een container uit te voeren met `podman run --detach --publish 8080:80 --volume $PWD/nginx.conf:/etc/nginx/nginx.conf:ro localhost/workshop/nginx`

## Bronnen
- https://docs.docker.com/engine/reference/builder/

[Netwerken en Volumes](05-netwerken-volumes.md)
