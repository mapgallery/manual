---
title: "Search"
date: 2022-04-08T14:39:00+02:00
draft: true
weight: 3
---



Choose in Search which attributes has to be used in the search bar.&nbsp;  
Multiple attributes can be linked to a specific map.&nbsp;  
At the moment there are two possibilities to define search attributes: PDOK API and WFS

{{% panel theme="info" header="Example" %}}When search attributes for postal codes and tree numbers are selected.&nbsp;  
A user who entered "1234" in the search bar, will get results for both postal code "1234" and tree number "1234".&nbsp;  
If tree number is the only one selected, postal code "1234" will not be shown as a result.{{% /panel %}}




**PDOK**, automatically uses their address attribute for searching, but extra parameters can be applied.
- Extra URL params:&nbsp;  
Choose a specific parameter from source default is **`FQ=*:*`** (example: `FQ=type:gemeente&type=woonplaats`)

- Search param expression&nbsp;  
This field is used to add extra parameters into the search value (example: `gemeente=${value}`)

For more detailed documentation and list of all available parameters in PDOK, please refer to the following sites: &nbsp;  
`https://www.pdok.nl/restful-api/-/article/pdok-locatieserver-1`&nbsp;  
`https://github.com/PDOK/locatieserver/wiki/API-Locatieserver`

![PDOK_search.PNG](https://github.com/mapgallery/manual/blob/main/static/images/PDOK_search.PNG?raw=true)


**WFS**:
- Add base URL:&nbsp;  
Specify data source.&nbsp;  
Example: `http://example.com/geoserver/wfs?`

- Add URL param:&nbsp;  
Example: `CQL_Filter`

- Extra URL params:&nbsp;  
Example: `TYPENAMES=[WORKSPACE]:[TABLE]&MAXFEATURES=20`

- Search param expression: &nbsp;  
Example: `[COLUMN] ilike '%${value}'`

- Display param property&nbsp;  
*Text to display as topic for search results*

For more detailed documentation about the use of parameters, refer to the geoserver tutorial:&nbsp;  
`https://docs.geoserver.org/stable/en/user/tutorials/cql/cql_tutorial.html`

![WFS_search.PNG](https://github.com/mapgallery/manual/blob/main/static/images/WFS_search.PNG?raw=true)