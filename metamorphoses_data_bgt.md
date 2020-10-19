---
id: metamorphoses_data_bgt
title:  [RECEPT] Meetbaar - Voorbeeld dataset - Basisregistratie Grootschalige Topografie (BGT)
sidebar_label:  [RECEPT] Meetbaar - BGT
---

> Dit is een praktisch voorbeeld waarbij alle stappen van deze nieuwe manier van werken worden bezocht. Alle eerder genoemde onderwerpen zullen in meer of mindere mate aan bod komen met de nadruk op 'wateroverlast'

Een voorbeeld voor geodata is de Basisregistratie Grootschalige Topografie (BGT), een digital kaart van Nederland waarop gebouwen, wegen, waterlopen, terreinen en spoorlijnen eenduidig zijn vastgelegd. De kaart is op 20 centimeter nauwkeurig en bevat veel details, waaronder historie. Dit betekent wel dat deze dataset veel informatie bevat en dus groot is (een extract voor het gebied van de gemeente Den Haag is al ruim 4 GB).

## De verschillende lagen

Gelukkig is de BGT in lagen verdeeld en hoeft dus niet de hele dataset ingeladen te worden voor een specifiek onderwerp. Hoewel afhankelijk van het doel wel meerdere lagen noodzakelijk zijn om tot het gewenste resultaat te komen. Hieronder is een schematische weergaven van de verschillende types objecten die zich in de BGT bevinden ([bron](https://www.geonovum.nl/uploads/standards/downloads/BGTGegevenscatalogus111.pdf)). 

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/bgt.PNG" target="_blank" alt="imageStyle: BGT-objecten"/>

Dit overzicht bevat alleen de objecten die als vlak weergegeven worden. Daarnaast bevat de BGT ook nog punten, zoals putten, masten en vegetatieobjecten. Om een iets beter idee te geven van de verschillende lagen, zijn de belangrijkste hieronder kort toegelicht aangevuld met de definities zoals die in de BGT gegevenscatalogus zijn beschreven ([bron](https://www.geonovum.nl/uploads/standards/downloads/BGTGegevenscatalogus111.pdf)). Met name de 'ondersteunende' lagen zijn soms moeilijk te interpreteren, vaak omdat die grensgebieden beslaan die niet altijd even duidelijk zijn te definieren.

### Transport

| Naam | Definitie |
| ---- | --------- |
| Wegdeel | Kleinste functioneel onafhankelijk stukje van een NEN 3610 Weg met gelijkblijvende, homogene eigenschappen en relaties en primair bedoeld voor gebruik door weg-, spoor- en vliegverkeer te land. |
| OndersteunendWegdeel | Een deel van de weg dat niet primair bedoeld is voor gebruik door het verkeer. |
| Spoor | De as van het spoor, dat wil zeggen het midden van twee stalen staven op een onderling vaste afstand, waarover trein, tram, of sneltram rijdt. |

### Terrein

| Naam | Definitie |
| ---- | --------- |
| OnbegroeidTerreindeel | Kleinste functioneel onafhankelijk stukje van een terrein, dat er binnen het objecttype Terrein van NEN 3610 wordt onderscheiden, zonder aaneengesloten vegetatie. |
| BegroeidTerreindeel | Kleinste functioneel onafhankelijk stukje van een terrein dat er binnen het objecttype Terrein van NEN 3610 wordt onderscheiden, met aaneengesloten vegetatie. |

### Water

| Naam | Definitie |
| ---- | --------- |
| Waterdeel | Water van NEN 3610 wordt onderscheiden en dat permanent met water bedekt is. |
| OndersteunendWaterdeel | Object dat in het kader van de waterhuishouding periodiek gedeeltelijk of geheel met water is bedekt. |

### Bouwwerk

| Naam | Definitie |
| ---- | --------- |
| Pand | Een PAND is de kleinste bij de totstandkoming functioneel en bouwkundig-constructief zelfstandige eenheid die direct en duurzaam met de aarde is verbonden en betreedbaar en afsluitbaar is. |
| OverigBouwwerk | Met de aarde verbonden duurzaam bouwwerk, dat niet valt onder de definities van een pand of kunstwerk. |
| Scheiding | Kunstmatig, meestal lineair obstakel met een werende functie. |

#### Kunstwerk

| Naam | Definitie |
| ---- | --------- |
| Overbruggingsdeel | Onderdeel van een beweegbare of vaste verbinding tussen twee punten, die door water, een weg of anderszins gescheiden zijn, dat essentieel is voor de constructie. |
| Tunneldeel | Onderdeel van een kunstmatig aangelegde, kokervormige onderdoorgang dat essentieel is voor de constructie. |
| Kunstwerkdeel | Onderdeel van een civiel-technisch werk voor de infrastructuur van wegen, water, spoorbanen, waterkeringen en/of leidingen. |

## Vissershaven volgens de BGT

Om een idee te geven van de BGT zal in dit deel gekeken worden naar de Vissershaven ([Google Maps](https://www.google.com/maps/@52.0989073,4.2628015,15.5z)) in de gemeente Den Haag vanuit het oogpunt van de BGT. 

Hieronder is een kaartje gemaakt met [QGIS](https://qgis.org/nl/site/) (een vrij en open source geografisch informatiesysteem) waarop alle lagen zoals die in het objectenoverzicht staan. Op de hoek linksboven na, is er verder geen wit te zien wat betekent dat de BGT de gehele ruimte heeft toegekend aan een object. De hoek linksboven is het gebied van de Noordzee dat buiten de landsgrens valt.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/bgt_denhaag_with_legend.png" target="_blank" alt="imageStyle: Vissershaven"/>

## Van vlakken naar informatie

Het kaartje van de Vissershaven is leuk en aardig, maar er valt nog geen informatie uit te halen. Dit gebied bevat veel water, dus laten we daar wat mee doen. Door de laag `Pand` en `Waterdeel` te combineren kunnen we de afstand bepalen van elk gebouw naar het dichtsbijzijnde water. Voor we naar het resultaat gaan kijken is het goed om even te restricties te bespreken:

- Om de berekeningen snel te laten verlopen is er een extract gemaakt van de BGT met de grenzen zoals die hierboven zijn weergegeven. Dit betekent dus dat waterobjecten die daar net buiten vallen niet zijn meegenomen in de bepaling. De waardes aan de randen zullen dus niet representatief zijn.
- De definitie van een `Waterdeel` is best breed, wat dus betekent dat dit soort objecten flink kunnen varieren. Zo zijn er 28 objecten in deze laag met oppervlaktes van 22 m2 tot 2.2 km2.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/bgt_vissershaven_afstand_with_legend.png" target="_blank" alt="imageStyle: Vissershaven"/>

Op deze manier is er een beeld verkregen van de afstand van pand naar water. De gemiddelde afstand blijkt 350 meter te zijn.

Hetzelfde kan ook gedaan worden met de laag `BegroeidTerreindeel`, waardoor er een overzicht ontstaat van de afstand tussen grijs en groen. Dit overzicht is in het kaartje hieronder weergegeven. Dezelfde opmerkingen gelden wederom (4400 objecten, kleinste object is 60 cm2 en het grootsts object ruim 70000 m2):

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/bgt_vissershaven_afstand_plant_with_legend.png" target="_blank" alt="imageStyle: Vissershaven"/>

Dit beeld is een stuk gevarieerder door het grotere aantal objecten, waardoor de gemiddelde afstand ook een stuk korter is: 25 m.

Aan de hand van deze twee berekeningen kan simpel een composiet gemaakt worden. Stel dat er een beleidsplan ligt dat elke burger in staat wilt stellen om makkelijk toegang te krijgen tot 'natuur', in dit geval groen of blauw, dan kan door de combinatie van de bovenstaande berekeningen een overzicht gemaakt worden van welke gebieden in de Vissershaven de meeste aandacht vragen.

In dit geval is besloten om panden te klassificeren gebaseerd op de afstand in vergelijking met de gemiddelde afstand:

| Kleur | Klasse |
| ----- | ------ |
| Lightblauw | Zowel de afstand naar water en groen is kleiner of gelijk aan de gemiddelde afstand |
| Donkerblauw | Alleen afstand naar water is kleiner of gelijk aan de gemiddelde afstand |
| Lightgroen | Alleen afstand naar groen is kleiner of gelijk aan de gemiddelde afstand |
| Zwart | Geen van de standen is kleiner of gelijk aan de gemiddelde afstand |

Het resultaat is hieronder te zien.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/bgt_vissershaven_class.png" target="_blank" alt="imageStyle: Vissershaven"/>

Hoewel door de eerder genoemde beperkingen het lastig is om echt uitspraken te doen, blijkt wel dat de gebieden Oud Scheveningen en Statenkwartier aandacht kunnen gebruiken.