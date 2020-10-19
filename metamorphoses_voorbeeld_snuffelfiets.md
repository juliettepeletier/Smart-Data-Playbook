---
id: metamorphoses_voorbeeld_snuffelfiets
title:  Snuffelfiets
sidebar_label:  Snuffelfiets
---

Het snuffelfiets project is een initatief vanuit de provincie Utrecht om samen met burgers door middel van relatief goedkope sensoren een beeld te krijgen van de luchtkwaliteit in de provincie. Vaak is het onduidelijk hoe het nou staat met de luchtkwaliteit in een kwantitatieve manier en zijn de mogelijkheden om dit vast te stellen over het algemeen een flinke investering. Dit is een van veel voorkomende vicieuze cirkels, waarbij data nodig is om het probleem vast te stellen maar het probleem al duidelijk moet zijn om de juiste data te verzamelen.

In dit project is het idee dat burgers met deze simpele sensoren rond gaan fietsen, zodat met betrekkelijk weinig sensoren een grote dekking kan worden verkregen. Zodra deze dekking bekend is zouden dan eventueel meer exactere sensoren geplaatst kunnen worden op kritieke plekken, zodat er geen onnodige bestedingen worden gedaan.

## Van beleid naar meting

De provincie Utrecht voert een project uit om de luchtkwaliteit en fietsroutes in kaart te brengen. In 2019 krijgen 500 fietsers een meetkastje (mobiele sensor) waarmee elke 10 seconden de luchtkwaliteit en GPS-positie wordt gemeten. Elke 2 minuten wordt de data via een standaard protocol (NB-IoT of LTE) verstuurd naar een dataplatform. De data die wordt verzameld wordt ook naar het RIVM gezonden om de gegevens te valideren tov het officiële landelijke meetnet. De gecorrigeerde gegevens worden eveneens op een dataplatform opgeslagen en beschikbaar gesteld als open data.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/Voorbeeld_2_image1.png" target="_blank" alt="imageStyle: Wateroverlas"/>

In feite is het achterliggende proces voor elk sensorproject vergelijkbaar, zoals hieronder schematisch is weergegeven. Sensoren versturen de data via een gateway naar een dataplatform. Daar wordt de data in een herbruikbaar, open formaat omgezet, zodat het kan worden hergebruikt voor nieuwe toepassingen. 

Publicatie als open data is een keuze die de eigenaar van de data maakt. Op een vergelijkbare manier heeft de gemeente Utrecht bijvoorbeeld 50 invalideparkeerplaatsen voorzien van een sensor. Elke statuswijziging (vrij-bezet) wordt als nieuw record opgeslagen, zodat er een set historische data wordt opgebouwd die gebruikt kan worden voor analyse en eventuele aanpassing van beleid.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/Voorbeeld_2_image2.png" target="_blank" alt="imageStyle: Wateroverlas"/>

## Van meting naar data

Wat houd zo'n meting nou precies in? Simpel gezegd stuurt zo'n sensor elke 10 seconde een setje van meetwaardes die in die tijdspanne zijn waargenomen. Al deze metingen worden in een grote dataset verzamelt, die als bron kan worden gebruikt.

Hieronder is een overzicht gegeven van hoe zo'n set meetwaardes er in het echt uitziet. Wat op zal vallen is dat in sommige gevallen het veldnaam en veldwaarde meten duidelijk zijn, soms de veldnaam logisch klinkt maar de waarde erbij onlogisch lijkt, en soms is het helemaal onduidelijk wat een waarde voorstelt. 

| Veld | Waarde |   | Veld | Waarde |
| ---- | ------ |---| ---- | ------ |
| voc | 538 || pressure | 1025 |
| versionMajor | 1 || pm1_0 | 3 |
| errorCode | 0 || versionMinor | 3 |
| voltage | 122 || horizontalAccuracy | 67788 |
| accMax | 0 || entityId | 352...447 |
| verticalAccuracy | 49795 || pm10 | 3 |
| no2 | 84 || temp | 204 |
| location | 52.1052,5.1244 || humidity | 54 |
| pm2_5 | 3 || time | 1566333186 |

Met andere woorden: deze data bevat nog geen informatie. Zoals al eerder is aangegeven, is het niet alleen belangrijk dat de databron beschikbaar is, maar ook de nodige metadata bevat om daadwerkelijk gebruikt te worden.

## Van data naar informatie

Kijk maar naar de waarde voor het veld `temp`: gezien de soort metingen is het logisch om te bedenken dat dit voor temperatuur staat. Maar hoe zit het dan met die `204`? Dat is duidelijk geen graden Celsius, maar wat dan? Graden Fahrenheit? Kelvin? 

Gelukkig is dit veld te vergelijken met de standaard weersmetingen, zodat te beredeneren is dat het staat voor 20.4 graden Celsius. Maar dit is niet voor elke meetwaarde te doen, juist omdat dit het hele doel is van het project! Ook is het fijn dat er een versie nummer wordt meegestuurd, maar is het wel belangrijk dat bekend is wat eventuele verschillen zijn in versies.

Hieronder is de data omgeschreven naar informatie. Een aantal velden zijn daarbij weggelaten om het overzichtelijk te houden, maar het idee is dus dat vastligt wat een waarde representeert.

| Veld | Betekenis | Waarde |
| ---- | --------- | ------ |
| pressure | Luchtdruk | 1025 hPa |
| horizontalAccuracy | Afwijking GPS | 67.788 meter |
| pm10 | Concentratie fijnstof | 3 µg/m³ |
| temp | Temperatuur | 20.4 graden Celsius |
| location | GPS locatie (lat, lon)| (52.105156,5.124354) |
| humidity | Relatieve luchtvochtigheid | 54 procent |
| time | Tijd sinds Unix Epoch | 1566333186 secondes |

Nu spreken we over informatie: de data is begrepen en ligt eenduidig vast, zodat vergelijkingen met andere datasets of bronnen gemaakt kunnen worden. Deze 3 miljoen setjes meetwaardes zijn nu een grote set met informatie, klaar voor gebruik.

Als extra stap wordt deze informatie ook nog eens gevalideerd door het RIVM. Dat houd in dat alle metingen ook naar het RIVM worden gestuurd, die deze vergelijkt met metingen van hun eigen meetopstellingen. Ook hebben ze een aantal sensoren onder observatie om de precieze (langetermijn) werking te bestuderen. Op deze manier kunnen ze correcties uitvoeren op de meetwaardes, zodat deze accuraat blijven ook al vertonen de sensoren naar verloop van tijd enige verloop. 

## Van informatie naar presentatie

Nu de informatie aanwezig is kan de stap gemaakt worden naar daadwerkelijke kennis. Met andere woorden, hoe presenteer je deze informatie. De informatie over de luchtkwaliteit bevat twee dimensies: een ruimtelijke dimensie (waar is wat gemeten) en een temporale dimensie (wanneer is wat gemeten). Vaak zal er in een presentatie een keuze gemaakt moeten worden voor een dimensie. Deze dimensionaliteit betekent ook dat er er niet alleen op veel plekken gemeten moet worden, maar ook vaak op dezelfde plek gemeten moet worden.

Hieronder zijn een aantal voorbeelden gegeven, elk met hun voordelen en nadelen. 

### Routes

Een route is een reeks aaneengesloten punten van een bepaalde sensor. Onderstaande kaart geeft dus weer hoe fietsers zijn gereden en wat luchtkwaliteit er gemeten is onderweg. Kort gezegd: puntjes tekenen en lijntjes trekken.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kookboek_example_snuffelfiets_routes.png" target="_blank" alt="imageStyle: 
Residential Breakdown"/>

| Voordelen | Nadelen |
| - | - |
| Duidelijk inzicht in waar men gefietst heeft zonder bewerkingen. | Geen inzicht in de tijdsverdeling en de ruimtelijke onzekerheid. |

### Grid

In het geval van het grid, is het gebied in stukken geknipt (vierkanten, zeshoeken, etc) en is per gebied de gemiddelde luchtkwaliteit bepaald. Belangrijke parameter van een grid is de celgrootte: wat is de maat van de kleinste verdeling.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kookboek_example_snuffelfiets_grid.png" target="_blank" alt="imageStyle: Residential Breakdown"/>

| Voordelen | Nadelen |
| - | - |
| Goed globaal beeld van de situatie zonder naar precieze punten te kijken, minimale bewerking | Geen inzicht in de tijdsverdeling en bepalen van celgrootte heeft invloed |

### Wegvakken

In plaats van de routes uit de metingen te halen, is er in dit geval voor gekozen om de punten te matchen aan wegvakken zoals die door het NDW zijn bepaald. Op deze manier kunnen metingen op wegvakkniveau bekeken worden. Tevens is er voor elk wegvak een uitsplitsing gemaakt naar uurvak.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kookboek_example_snuffelfiets_wegvak.png" target="_blank" alt="imageStyle: Residential Breakdown"/>

| Voordelen | Nadelen |
| - | - |
| Het beeld bevat nu daadwerkelijk de bestaande infrastructuur, wat het mogelijk maakt de luchtkwaliteit te vergelijken met andere informatie over de weg | Elk punt hoort bij een wegvak, terwijl de onzekerheid andere wegvakken niet uit kan sluiten. Vraagt veel bewerking. |
