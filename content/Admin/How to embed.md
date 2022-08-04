---
title: "Insluiten in website"
date: 2022-04-08T14:39:00+02:00
draft: true
weight: 4
---

Eindelijk, de kaart is af en het is tijd om deze toe te voegen aan de website;  
De beste manier om dit te doen is door het in te sluiten in uw website. Daarvoor moet een iframe gemaakt worden.
1. Open de kaart in gepubliceerde kaarten
2. Klik op het share logo in de rechterbovenhoek
3. Druk op de </> Embed knop.
4. Selecteer of extra parameters in de code meegenomen moeten worden
5. Kopieer tekst
6. Plak in HTML van de website

Voorbeeld vereenvoudig (simplified)

    <iframe
        id="mapgallery1"
        title="testmap"
        name="mapgallery"
        width="100%"
        height="400px"
        src="https://baasgeo.mapgallery.info/app/embed/1">
    </iframe>

Voorbeeld met parameters

    <iframe
        id="mapgallery1"
        title="testmap"
        name="mapgallery"
        width="100%"
        height="400px"
        src="https://baasgeo.mapgallery.info/app/embed/1?zoom=8&center=103012,488695&layerIds=5898634633768,4669125108797,5489791876754,8168927931755">
    </iframe>