---
title: "Search"
date: 2022-04-08T14:39:00+02:00
draft: true
weight: 3
---

Kies in "Zoeken" welke attributen gebruikt moeten worden in de zoekbalk.  
Aan een specifieke kaart kunnen meerdere attributen worden gekoppeld.  
Op dit moment zijn er twee mogelijkheden om zoekattributen te definiëren: PDOK API en WFS

{{% panel theme="info" header="example" %}}Als zoekattributen voor postcodes en boomnummers zijn geselecteerd.  
Een gebruiker die in de zoekbalk "1234" heeft ingevuld, krijgt resultaten voor zowel postcode "1234" als boomnummer "1234".  
Als boomnummer de enige geselecteerde is, zal postcode "1234" niet als resultaat worden getoond.{{% /panel %}}




**PDOK**, gebruikt automatisch hun adresattribuut voor het zoeken, maar extra parameters kunnen worden toegevoegd.
- Extra URL params:  
Kies een specifieke parameter uit de bron standaard is **`FQ=*:*`** (voorbeeld: `FQ=type:gemeente&type=woonplaats`)

- Zoek param expressie  
Dit veld wordt gebruikt om extra parameters toe te voegen aan de zoekwaarde (voorbeeld: `gemeente=${value}`)

Voor meer gedetailleerde documentatie en een lijst van alle beschikbare parameters in PDOK, zie onderstaande links:    
`https://www.pdok.nl/restful-api/-/article/pdok-locatieserver-1`  
`https://github.com/PDOK/locatieserver/wiki/API-Locatieserver`

![PDOK_search.PNG](https://github.com/mapgallery/manual/blob/main/static/images/PDOK_search.PNG?raw=true)


**WFS**:
- Add base URL:  
Specificeer databron.  
Voorbeeld: `http://example.com/geoserver/wfs?`

- Add URL param:  
Voorbeeld: `CQL_Filter`

- Extra URL params:  
Voorbeeld: `TYPENAMES=[WORKSPACE]:[TABLE]&MAXFEATURES=20`

- Search param expression:   
Voorbeeld: `[COLUMN] ilike '%${value}'`

- Display param property  
*Tekst om weer te geven als onderwerp voor zoekresultaten*

For more detailed documentation about the use of parameters, refer to the geoserver tutorial:  
`https://docs.geoserver.org/stable/en/user/tutorials/cql/cql_tutorial.html`

![WFS_search.PNG](https://github.com/mapgallery/manual/blob/main/static/images/WFS_search.PNG?raw=true)