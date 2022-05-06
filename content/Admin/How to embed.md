---
title: "How to embed"
date: 2022-04-08T14:39:00+02:00
draft: true
weight: 4
---

Finally, the map is finished and it's time to add it into your website.&nbsp;  
The best way to do it is to embed it into your website. Therefor an iframe must be created.
1. Open the map in published maps
2. Click on the share logo in the top right
3. press the </> Embed button.
4. Select whether you want to have extra parameters in in the code
5. Copy text
6. Paste in HTML of your website

Example simplified

    <iframe
        id="mapgallery1"
        title="testmap"
        name="mapgallery"
        width="100%"
        height="400px"
        src="https://baasgeo.mapgallery.info/app/embed/1">
    </iframe>

Example with parameters

    <iframe
        id="mapgallery1"
        title="testmap"
        name="mapgallery"
        width="100%"
        height="400px"
        src="https://baasgeo.mapgallery.info/app/embed/1?zoom=8&center=103012,488695&layerIds=5898634633768,4669125108797,5489791876754,8168927931755">
    </iframe>