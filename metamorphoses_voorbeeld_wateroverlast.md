---
id: metamorphoses_voorbeeld_wateroverlast
title: Wateroverlast
sidebar_label: Wateroverlast
---

> Dit is een praktisch voorbeeld waarbij getracht is zoveel mogelijk stappen uitgebreid te behandelen. Daardoor zal dit niet altijd een goed beeld geven van de werkelijkheid en is dus puur illustratief bedoeld.

## Introductie

De impact van wateroverlast op de samenleving zal de komende jaren alleen maar toenemen zoals uitgebreid is beschreven in [Wateroverlast](metamorphoses_voorbeeld_wateroverlast.md). Hierin is ook de link gelegd naar de Meldingen Openbare Ruimte (MOR) als een bruikbare databron. In dit document zal hier verder op in worden gegaan en ook een combinatie gemaakt worden met de weersdata van het KNMI. Een uitgebreide kijk in de data van het KNMI is te vinden onder [Voorbeeld dataset - KNMI](kookboek_data_knmi.md)

## Aanleiding

De gemeente Utrecht gebruikt een applicatie Slim Melden waarmee zij meldingen van inwoners verzamelen. Eén van de categorieën waarover een melding gedaan kan worden, is wateroverlast.

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/Voorbeeld_1_image1.png" target="_blank" alt="imageStyle: Wateroverlas"/>

In de afgelopen 2,5 jaar zijn in totaal meer dan 160.000 meldingen verzameld. Deze meldingen zijn beschikbaar als open data en kunnen dus door iedereen gebruikt worden (en worden gecombineerd met andere data. Hieronder staat een voorbeeld van een dashboard van de gemeente Utrecht, waarbij de categorie wateroverlast is geselecteerd. 

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/Voorbeeld_1_image2.png" target="_blank" alt="imageStyle: Wateroverlas"/>

## Stappenplan

Aan de hand van de vraagstelling hierboven zullen we nu het stappenplan doorlopen

### Stap 1: Concretiseren
> Maak het vraagstuk concreet [[zie stap 1]](../metamorphoses_stap_1)

In dit scenario definieren we overlast als overlast waar een burger melding van maakt, waarbij we verwachten dat er een samenhang is tussen de hoeveelheid regen en het aantal meldingen om een verwachting te kunnen maken van waar overlast zal optreden.

### Stap 2: Formuleren
> Vertaal de sleutelelementen in 1 of meerdere meetbare indicatoren [[zie stap 2]](../metamorphoses_stap_2)

Uit onze definitie is er maar 1 KPI te formuleren:

- Het aantal meldingen in de openbare ruimte met betrekking tot wateroverlast per buurt per week verminderen met 20% over een periode van 4 jaar.

Met als extra actiepunt het bijhouden van de neerslag in deze periode.

### Stap 3: Verzamelen
> Hoe vind je de gewenste data om deze indicatoren te berekenen [[zie stap 3]](../metamorphoses_stap_3)

Vaak begint de zoektocht bij een van de algemene databibliotheken zoals data.overheid.nl of pdok.nl, maar soms is ook al bekend bij wat voor andere instanties de data te vinden is. Afhankelijk van het gebied kan dat een of meerdere gemeentes zijn.

Vanwege ons uitgangspunt zijn de databronnen al bekend:

- Meldingen Openbare Ruimte (in categorieen betreffende wateroverlast)
- Weersdata van het KNMI
- Buurtverdelingen volgens het CBS

Deze databronnen zullen als leidraad genomen worden in de vervolgstappen.

### Stap 4: Waarderen
> Vind je in de data de juiste gegevens voor het beantwoorden van je vraagstuk [[zie stap 4]](../metamorphoses_stap_4)

Alle databronnen hebben hun specifieke eigenschappen die in de gaten gehouden moeten worden bij het gebruik ervan:

#### Weersdata van het KNMI

Het KNMI heeft maar een beperkt aantal weerstations verdeelt over Nederland. Het is dus niet altijd even duidelijk welke weerstations nou representatief zijn voor een bepaald gebied. Met name zeer plaatselijke buien kunnen gemist worden met dergelijke meetstations. Ook kunnen stations in de loop van de tijd van locatie gewijzigd zijn of een andere meetstrategie zijn gaan toepassen. Deze laatste informatie te vinden via het KNMI, dus die kunnen in de verdere berekeningen worden meegenomen.

#### Meldingen Openbare Ruimte

Deze databron kan verschillen per gemeente of instantie, maar over het algemeen bevatten deze een locatie, een tijdstip van de melding en een categorie. De locatie kan een adres of GPS locatie zijn, het tijdstip kan varieren tussen de melding of de oorzaak van de melding en de categorieren kunnen verschillen per overheid. Ook is dit een subjectieve dataset, in de zin van dat een melding altijd gedaan wordt door een burger die daar een reden voor heeft. Met andere woorden, niet elke melding betekent dat er ook echt overlast is en geen meldingen betekent ook niet altijd dat er geen overlast is. Net als de dataset van het KNMI zal deze ook onderhevig aan interne of externe veranderingen (manieren van verwerken, makkerlijkere interface voor de burgers, etc.).

#### Buurtverdelingen CSB

Vanzelfsprekende dataset, waarbij hooguit gelet moet worden op variaties in buurten over tijd door veranderingen in samenstellingen. 

### Stap 5: Prepareren
> Maak de data gereed voor gebruik [[zie stap 5]](../metamorphoses_stap_5)

In dit geval nemen we aan dat de buurtverdelingen gelijk zijn gebleven in onze periode. 

#### Weersdata van het KNMI

In het geval er meerdere meetstations moeten worden meegenomen voor het gebied van interesse, zullen deze geaggregeerd moeten worden of in ieder geval bepaald worden welk stations geldt voor welke buurt. Dus er zal moeten bepaald worden welk station verantwoordelijk is voor welke buurt of de gegegevens van de stations zal moeten gemiddelde worden (wel of niet rekeninghoudend met de afstand tot een buurt).

#### Meldingen Openbare Ruimte

Deze dataset zal meer werk kosten. Zo zullen de categorieen niet altijd even eenvoudig in te delen zijn op wateroverlast (niet elke gemeente heeft zo'n categorie). Ook zullen in het geval van adressen deze 'vertaald' moeten worden naar een locatie om te kunnen combineren met de buurtverdelingen. Ook hoeft de tijd van melding niet het tijdstip van oorzaak te zijn. Denk aan een kelder die volgestroomd is, waarvan de eigenaar 's ochtends melding doen terwijl de oorzaak de hevige regenbui in de avond van de dag ervoor was.

### Stap 6: Combineren
> Combineer de data als dat nodig is [[zie stap 6]](../metamorphoses_stap_6)

Match elke melding aan de bijbehorende buurt gebaseerd op de locatie.

### Stap 7: Verwerken
> Bereken de KPI's [[zie stap 7]](../metamorphoses_stap_7)

Aggregeer deze meldingen per buurt over een bepaalde periode (bijvoorbeeld per week)

### Stap 8: Documenteren
> Leg vast hoe het resultaat tot stand is gekomen [[zie stap 8]](../metamorphoses_stap_8)

Dit document zou beschouwd kunnen worden als documentatie. In het geval van een datacatalogus zou je deze bronnen toevoegen. Uiteindelijk is het belangrijk dat men weet wat er is gebeurd en welke beredeneringen en aannames zijn gedaan om bij het resultaat te komen. Dit om transparantie en reproduceerbaarheid te verbeteren.

### Stap 9: Monitoren
> Herhaal het proces [[zie stap 9]](../metamorphoses_stap_9)

Herhaal de bovenstaande stappen om een tijdsbeeld te krijgen van het verloop om het beleid te monitoren. Denk hierbij ook aan het maken van een script dat dit proces geautomatiseerd doet. Hou in dat geval rekening met eventuele veranderingen van databronnen (bijvoorbeeld datasets per jaar die elk jaar een nieuwe naam krijgen) of aanpassingen in de berekeningen.

### Stap 10: Presenteren
> Maak een rapport/dashboard/presentatie [[zie stap 10]](../metamorphoses_stap_10)

Nu bekend is wat de precieze informatie is (namelijk meldingen van problemen in de openbare ruimte door burgers die dit probleem ook waarnemen en vervelend vinden) kan deze informatie worden omgezet naar kennis. Of in ieder geval gepresenteert worden. Hieronder zijn een aantal voorbeelden uitgewerkt, waar ook de inzichten van de vorige stap aan bod komen. 

#### Verdeling meldingen

Een eerste stap om een idee te krijgen van de impact van wateroverlast is bekijken waar deze overlast nou voorkomt. Hieronder is een verdeling weergegeven van de meldingen in Utrecht in de categorie wateroverlast in de periode 9-8-2018 t/m 21-8-2019. Hoe minder transparant de blauwe kleur, des te minder meldingen er in dat gebied zijn gemaakt. Duidelijk is met name de Binnenstad en in mindere mate Vleuten, De Meern en Lunetten plekken zijn waar veel meldingen gemaakt worden. Hoe meer mensen ergens wonen, des te groter de kans dat er iemand is die alle 4 de stappen doorloopt om tot een melding te komen. Dus is deze verdeling zo wel representatief?

![Verdeling van de meldingen in Utrecht over wateroverlast in de periode 9-8-2018 t/m 21-8-2019](assets/Kookboek/kookboek_example_wateroverlast_wateroverlast_slimmelden_meldingen_cropped.png)

#### Verdeling stemmen

Hieronder staat een soortgelijke verdeling, maar nu in plaats van meldingen het aantal stemmen. Dit zijn dus meldingen waarvan andere burgers vinden dat ze dit ook een probleem vinden. Wat opvalt is dat dit tot een ander beeld leidt; nog steeds staat de Binnenstad bovenaan, maar Leidsche Rijn is nu ook opeens duidelijk aanwezig. 

![Verdeling van de stemmen in Utrecht over wateroverlast in de periode 9-8-2018 t/m 21-8-2019](assets/Kookboek/kookboek_example_wateroverlast_wateroverlast_slimmelden_stemmen_cropped.png)

#### Meldingen en het weer

Een andere aanpak is het vergelijken van de melden met weersgegevens, bijvoorbeeld de hoeveelheid regen op een dag versus het percentage meldingen over wateroverlast op die dag. In dit geval is het percentage een betere meetwaarde, om zo schommelingen per dag eruit te halen. Een dag met 100 meldingen in totaal waarvan 20 over wateroverlast telt dus in dat geval net zo zwaar als een dag met 25000 meldingen waarvan 5000 over wateroverlast. 

Elk punt in de grafiek stelt hieronder stelt een dag voor met op de x-as het aantal mm regen dat die dag is gevallen en op de y-as het percentage meldingen over wateroverlast. In de periode 9-8-2018 t/m 21-8-2019 ligt het percentage dus tussen de 0% en de 18% en de etmaalsom tossen de 0 mm en de 42 mm.

![Verdeling van de stemmen in Utrecht over wateroverlast in de periode 9-8-2018 t/m 21-8-2019](assets/Kookboek/kookboek_example_wateroverlast_regenval_vs_meldingen.png)

Wat opvalt is dat er geen duidelijke lijn te zien is tusen de meldingen en de neerslag. Het gros van de punten ligt linksonderin (geen regen, geen meldingen) en tussen de 10 en 15 mm regen lijkt het percentage meldingen toe te nemen, maar dit zet niet door. Sterker nog, voor alle dagen met meer dan 30 mm regen komt het percentage niet boven die met 0 mm regen. Maar wellicht is dit de verkeerde vergelijking: 30 mm op een dag kan betekenen dat het de hele dag zachtjes heeft geregend heeft (1 mm per uur) of dat er een korte maar heftige wolkbreuk is geweest (bv. 60 mm in een half uur). 

### Stap 11: Evalueren
> Evalueer de impact van het beleid op de data [[meer informatie]](../metamorphoses_stap_11)

In de context van MOR zal de data bestaan uit een lijst van meldingen met minimaal een locatie, tijdstip en een beschrijving. In het geval van Slim Melden is dit nog eens uitgebreid met categorieen en eventuele foto's en stemmen. Stemmen betekent in dit geval burgers die dezelfde melding ook belangrijk vinden.

Maar belangrijk is natuurlijk een kwalitatief begrip: wat voor de een belangrijk is, geldt niet voor een ander. Daarom is het goed om de totstandkoming van deze dataset te begrijpen. Een sensor stuurt gewoon een meting zonder enig motief; een burger is echter een heel ander verhaal. Hieronder staat een overzicht van de stappen die worden doorlopen om tot een melding te komen:

1. Er *is* een **probleem in de Openbare Ruimte**.
2. De burger *neemt* dit **probleem in de Openbare Ruimte** *waar*.
3. De burger *vind* dit een **probleem voor de burger**.
4. De burger neemt de moeite om dit **probleem voor de burger** te melden.

Er wordt expres een onderscheid gemaakt tussen **probleem in de Openbare Ruimte** (vanuit het oogpunt van de gemeente) en een **probleem voor de burger** (vanuit het oogpunt van de burger). Deze zijn namelijk niet per definitie gelijk, omdat de gemeente een andere agenda heeft dan de burger. Bijvoorbeeld omdat de gemeente met een langere termijn visie werkt, in tegenstelling tot een burger die vooral niet gehinderd wilt worden in zijn of haar dagelijkse gang van zaken.

Het is dus belangrijk om te zien hoe een dataset tot stand is gekomen. Het feit dat er geen meldingen zijn, betekent dus niet dat er geen probleem is. En de mate van burgerparticipatie heeft een belangrijke impact op hoe deze dataset eruit ziet.

#### Aandachtspunten Meldingen Openbare Ruimte
* dit is de data van één gemeente en categorieën verschillen per gemeente (hetgeen de vergelijkbaarheid bemoeilijkt)
* het aantal meldingen hoeft niet te corresponderen met de werkelijke overlast (alleen gemotiveerde/gedupeerde inwoners hebben een melding gedaan)
* VNG Realisatie is bezig met een standaard voor Meldingen Openbare Ruimte. Wanneer alle data van elke gemeente in hetzelfde formaat beschikbaar is, ontstaan er meer mogelijkheden om de data met elkaar te vergelijken.

#### Aandachtspunten Weergegevens
- Juiste maatstaf: wat is een goede voorspeller voor wateroverlast? Is dat toch de etmaalsom, of is het toch beter om de maximale regenval per uur te gebruiken. En hoe vergelijk je die met meldingen? Als het de avond ervoor zwaar geregend heeft, moeten de meldingen van de dag erop dan meegenomen worden met de dag ervoor? Maar in welke mate dan?
- Gebrek aan metingen: het aantal dagen met een hoge etmaalsom zijn schaarser, waardoor het lastig is om het gedrag van de burgers in te schatten vanuit de beschikbare gegevens.
- Verwachting van de burger: hoe ervaart een burger een bui? Het zou kunnen zijn dat een burger bij een heftige bui wateroverlast als vanzelfsprekend beschouwt en het dan dus niet als een probleem ervaart, terwijl een relatief kleinere bui die wateroverlast veroorzaakt meer opvalt en dus eerder zal worden gemeld.
- Geen waarnemingen: mensen blijven misschien binnen met slecht weer en nemen daardoor minder waar.