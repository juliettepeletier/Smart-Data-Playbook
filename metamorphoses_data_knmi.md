---
id: metamorphoses_data_knmi
title: [RECEPT] Meetbaar - Voorbeeld dataset - KNMI
sidebar_label: [RECEPT] Meetbaar - KNMI
---

> Dit is een praktisch voorbeeld waarbij alle stappen van deze nieuwe manier van werken worden bezocht. Alle eerder genoemde onderwerpen zullen in meer of mindere mate aan bod komen met de nadruk op 'wateroverlast'

In dit voorbeeld behandelen we data die verkrijgbaar is bij het KNMI. Als het gaat om het weer en het klimaat, biedt het KNMI waardevolle open data. We laten in dit voorbeeld de voorspellingen links liggen en kijken alleen naar de meetwaarden die het KNMI verzamelt met alle weerstations. Deze data, met uitgebreide opties zoals uur-, dag- en bodemwaarden, zijn te vinden op de site van het KNMI: [Klimatologie - Metingen en waarnemingen](https://www.knmi.nl/nederland-nu/klimatologie-metingen-en-waarnemingen).   

## Uurwaarden van weerstations

> Van detail naar globaal is altijd mogelijk, maar andersom niet.

De uurwaarden die het KNMI aanbiedt, geven het meest gedetailleerde beeld. Met deze gegevens is het altijd mogelijk om alsnog de geaggregeerde gegevens per dag/maand/jaar of per gebied te maken. Van detail naar globaal is altijd mogelijk, maar andersom niet.

De [Uurgegevens van het weer in Nederland](https://www.knmi.nl/nederland-nu/klimatologie/uurgegevens) bieden een uitgebreid overzicht van allerlei opties om gegevens van temperatuur, zon, bewolking en zicht, luchtdruk, wind en neerslag per station in te zien. Ook is er de mogelijkheid om een interactieve selectie te maken. Deze optie biedt de meeste keuze. De interactieve selectie op [Uurgegevens van het weer in Nederland - Download](http://projects.knmi.nl/klimatologie/uurgegevens/selectie.cgi) geeft meteen al een indruk van de data die opvraagbaar is. Het leidt ook tot een aantal vragen:

### Welk periode?

Wat is de periode waar we geinteresseerd zijn? En dan gaat het niet alleen om het moment waarop een beleidsmaatregel wordt ingevoerd, maar misschien juist ook om de periode daarvoor. Deze laatste fungeert in dat geval als controle om te kunnen zien wat voor impact een maatregel wel of niet heeft. Daarbij moeten dus ook eerdere maatregelen misschien in beschouwing genomen worden om de juiste conclusies te trekken. Gelukkig is het aanbod van het KNMI ruim, met metingen vanaf 1951. 

### Welke meetwaardes?

Er zijn een hoop verschillende kenmerkingen van het klimaat die gemeten worden door het KNMI. In de onderstaande table staat een overzicht van al deze elementen. Maar of al deze elementen ook nuttig zijn is uiteaard een tweede vraag. Hoewel meer data altijd handig is, kan een teveel aan data weer het zicht op de kern belemmeren. Zorg ook dat de eenheden bekend zijn, zodat de waardes van de gekozen elementen ook in de juiste context geplaatst kunnen worden.

| Element |	Omschrijving | Eenheid |
|---|---|---|
|DD|Windrichting gemiddeld over de laatste 10 minuten|°|
|FH|Uurgemiddelde windsnelheid|0.1 m/s|
|FF|Windsnelheid gemiddeld over de laatste 10 minuten|0.1 m/s|
|FX|Hoogste windstoot|0.1 m/s|
|T|Temperatuur op 1.50 m hoogte|0.1 ℃|
|T10N|Minimumtemperatuur op 10 cm hoogte in de afgelopen 6 uur|0.1 ℃|
|TD|Dauwpuntstemperatuur op 1.50 m hoogte|0.1 ℃|
|SQ|Duur van de zonneschijn|0.1 uren|
|Q|Globale straling|J/cm²|
|DR|Duur van de neerslag|0.1 uur|
|RH|Uursom van de neerslag|0.1 mm|
|P|Luchtdruk herleid naar zeeniveau|0.1 hPa|
|VV|Horizontaal zicht tijdens de waarneming||
|N|Bewolking|⅛|
|U|Relatieve vochtigheid op 1.50 m hoogte|%|
|WW|Weercode||
|IX|Weercode indicator voor de wijze van waarnemen||
|M|Mist|0=niet/1=wel|
|R|Regen|0=niet/1=wel|
|S|Sneeuw|0=niet/1=wel|
|O|Onweer|0=niet/1=wel|
|Y|IJsvorming|0=niet/1=wel|

### Welk meetstation?

> Waarschuwing: de data zijn niet gecorrigeerd voor inhomogeniteiten ontstaan door stationsverplaatsingen en veranderingen in de observatiemethodieken

De laatste keuze die gemaakt moet worden is gebaseerd op locatie, namelijk welke meetstations moeten worden meegenomen in de toepassing. Op dit moment heeft het KNMI 50 stations verdeelt over Nederland. Daarbij moet wel de opmerking gemaakt worden dat niet alle stations altijd op dezelfde locatie hebben gestaan of dezelfde methodieken hebben gebruikt. Vandaar dat het KNMI de waarschuwing geeft: de data zijn niet gecorrigeerd voor inhomogeniteiten ontstaan door stationsverplaatsingen en veranderingen in de observatiemethodieken.

Houd er rekening mee dat de locatie van deze stations zelden samenvallen met het gebied van interesse aangezien deze vaak op locaties liggen waar externe invloeden minimaal zijn (zoals steden, wegen, etc). Dus vaak zal een combinatie nodig zijn om het juiste beeld te krijgen.

## Een simpele toepassing van deze uurwaarden

Stel dat men bezig is met een beleid om meer forenzen op de fiets te krijgen, maar dat deze vaak klagen over regen of wind als grootste redenen om niet de fiets te pakken. Hoewel wind en regen zeker bij het Nederlandse klimaat horen, is het een goed idee om te controleren in hoeverre deze redenen ook correct zijn. Zo kunnen tegenstanders geinformeerd worden of kunnen er extra maatregelen in het beleid worden opgenomen om deze gevoelens weg te nemen.

In dit geval wordt gebruik gemaakt van het station in De Bilt in de periode van 1 januari 1951 t/m 31 december 2018 en gebruiken de meetwaarde elementen `DD` (windrichting) en `R` (heeft het geregend). 

> Dit is slecht bedoeld om een eerste beeld te schetsen. Er zijn nog een hoop extra elementen waar wellicht rekening mee moet worden gehouden. Voor beide voorbeelden zijn er een aantal van deze extra elementen opgenomen, maar probeer ook zelf er een paar te bedenken.

### Het regent altijd

Hiervoor bepalen we de kans op verschillende situaties, door `R` te vergelijken op verschillende tijdstippen op dezelfde dag en deze te tellen en te delen door het totale aantal metingen voor die combinaties.

| Situatie | Kans | Uitleg situatie |
|:---|---:|:---|
| Geen regen | 67.4 % | de forens kan zonder regen van en naar zijn en/of haar werk komen |
| Heen en terug regen | 9.6 % | de forens heeft zowel heen als terug regen ondervonden |
| Heen regen | 11.5 % | alleen op de heenweg was er sprake van regen |
| Terug regen | 11.5 % | alleen op de terugweg was er sprake van regen |
| Onbekend | < 0.1 % | de waarde van `R` was onbekend op de heen- en/of terugweg  |

Met andere woorden, tweederde van de dagen kan de forens zonder regen reizen. Als men ook nog zegt dat men vooral heen droog wilt blijven, verhoogt dit tot bijna 80% oftewel 4 van de 5 dagen.

> 1. Er is geen rekening gehouden met de hoeveelheid regen, dus 0.1 mm of 60 mm regen worden als gelijk beschouwt. Dit zal echter anders worden beleefd door een fietser
> 2. Er is geen rekening gehouden met de verschillende seizoenen


### Ik heb altijd wind tegen

Hiervoor bepalen we het verschil in windrichting, door `DD` te vergelijken op verschillende tijdstippen op dezelfde dag. In dit geval wordt een verschil van meer dan 90 graden beschouwd als een gedraaide wind. Wederom worden deze geteld en gedeeld door het totale aantal metingen voor die dag.

| Situatie | Kans | Uitleg situatie |
|:---|---:|:---|
| Zelfde wind | 84.2 % | De windrichting is niet drastisch veranderd |
| Gedraaide wind | 7.3 % | De windrichting is van richting veranderd  |
| Onbekend | 8.5 % | De waarde van `DD` was onbekend op de heen- en/of terugweg |

Redenen waarom `DD` onbekend is, zijn onder andere ontbrekende meetwaardes, zeer varierende windrichtingen, of momenten waarop het windstil was en dus geen richting bepaald kan worden.

> 1. Er is geen rekening gehouden met de windsnelheid. Een verwaarloosbare windsnelheid tegen telt wellicht niet als wind tegen.
> 2. Er is geen rekening gehouden met de rijrichting van de forens; misschien zijn de windrichtingen niet uniform verdeeld.
