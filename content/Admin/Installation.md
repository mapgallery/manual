---
title: "Installatie"
date: "`r format(Sys.time(), '%d %B, %Y')`"
draft: false
weight: 1
---
## Deployment

Dit is een docker image dat het opzetten van MapGallery voor organisaties vergemakkelijkt. Deze image is gebaseerd op de officiële [nginx](https://hub.docker.com/_/nginx) image.  Haal de image eenvoudig op van de docker hub.

```bash
$ docker pull baasgeo/mapgallery:tagname
```

Als alternatief kunt u de image lokaal opbouwen

```bash
$ git clone https://github.com/baasgeo/docker-mapgallery.git
$ cd mapgallery-docker
$ docker build -t "baasgeo/mapgallery:tagname" .
```

### Snelle start

Maak een data map aan op uw host:

```bash
$ sudo mkdir /var/mapgallery/
```

Start vervolgens de container:

```bash
$ docker run \
    --name=mapgallery \
    --publish=8080:8081 \
    --volume /var/mapgallery:/usr/share/nginx/assets \
    --memory 32mb \
    baasgeo/mapgallery:4
```

Ga met uw browser naar `http://localhost:8080/` en log in met de standaard gebruikersnaam en wachtwoord van MapGallery:

- Gebruikersnaam: admin
- Wachtwoord: admin

### **Hoe kunt u verschillende versies gebruiken**

Er is hoofdzakelijk één versie-tag van deze image voor elke minor **MapGallery** versie.

- 4.0.x -> baasgeo/mapgallery:4.0
- 4.1.x -> baasgeo/mapgallery:4.1
- 4.2.x -> baasgeo/mapgallery:4.2
- 5.0.x -> baasgeo/mapgallery:5.0

...enzovoort.  

Patches worden toegepast op de minor versie wanneer een update van MapGallery beschikbaar is. U kunt eenvoudig updaten naar de laatste versie door de image opnieuw te trekken.

```bash
$ docker pull baasgeo/mapgallery:tagname
$ docker restart mapgallery
```

## Configuratie

### Gegevensvolume

Deze MapGallery container bewaart zijn configuratiegegevens op in  
`/usr/share/nginx/assets` die als volume in een dockerfile wordt getoond.
Het volume maakt het mogelijk om nieuwe containers van hetzelfde image te stoppen en te starten zonder alle gegevens en aangepaste configuratie te verliezen.

Mogelijk wil je dit volume mappen naar een directory op de host. Volumes kunnen gemount worden door de `-v` of `--volume` flag mee te geven aan het docker run commando:

```bash
--volume /var/mapgallery:/usr/share/nginx/assets
```

Dit zal ook het upgrade proces in de toekomst vergemakkelijken. 


### Beperkingen van de bronnen

Standaard heeft de container geen resource restricties en kan zoveel van een gegeven resource gebruiken als de kernel scheduler van de host toestaat. Om te bepalen hoeveel geheugen, of CPU een container kan gebruiken, pas je runtime configuratie flags toe van het `docker run` commando zoals hier beschreven: [Runtime options with Memory, CPUs, and GPUs](https://docs.docker.com/config/containers/resource_constraints/)

### Database

MapGallery gebruikt de PostgREST api met PostgreSQL database

#### PostgREST container

Om de [PostgREST](https://postgrest.org) container in te stellen, gebruik de officiële [postgrest](https://registry.hub.docker.com/r/postgrest/postgrest) image:


```bash
$ docker run -d --name="postgrest" postgrest/postgrest
```

Voor meer informatie zie [Docker Hub](https://registry.hub.docker.com/r/postgrest/postgrest)

Start nu de MapGallery instantie door de `--link` optie toe te voegen aan het docker run commando:

```bash
--link postgrest:postgrest
```

#### PostgreSQL container

Als u een [PostgreSQL](https://www.postgresql.org/) container wilt gebruiken, dan kunt u die aan deze image koppelen. U bent vrij om eender welke PostgreSQL container te gebruiken.
Een voorbeeld met het officiële [postgres](https://registry.hub.docker.com/_/postgres/) image:


```bash
$ docker run -d --name="postgis" postgres
```

Voor meer informatie zie [Docker Hub](https://registry.hub.docker.com/_/postgres/)

Start nu de MapGallery instantie door de `--link` optie toe te voegen aan het docker run commando:

```bash
--link postgres:postgis
```