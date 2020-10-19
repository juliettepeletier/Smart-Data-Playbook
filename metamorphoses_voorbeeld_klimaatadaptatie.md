---
id: metamorphoses_voorbeeld_klimaatadaptatie
title: Klimaatadaptatie
sidebar_label: Klimaatadaptatie
---

Klimaatadaptie is een belangrijk onderwerp met de huidige veranderingen in het milieu en de veranderingen die nog gaan komen in de toekomst. Wateroverlast hoort daar ook bij, maar denk ook aan hitte-eilanden, energieverbruik en -opwekking en luchtkwaliteit.

Wateroverlast en luchtkwaliteit zijn twee onderwerpen die al behandeld zijn in andere hoofdstukken, maar in dit stuk wordt vooral gebruik gemaakt van de openbare ruimte in het algemeen. Hiervan is al de nodige informatie beschikbaar, met name in de vorm van de BGT en de AHN.

Want over veel van deze problemen is de oorzaak wel bekend en om te laten zien dat met betrekkelijk weining data al een beeld van de realiteit getoond kan worden.

## Van data naar informatie

De datasets waar mee gewerkt gaat worden zijn goed gedocumenteerd. Vooral de BGT is een uitstekende dataset (zie [Rating datasets](../../Kookboek/kookboek_rating_datasets.md)), maar ook het AHN is zeer goed bruikbaar. Met andere woorden: de data is goed, nu nog de informatie.


### Laag voor laag

Zoals al eerder is aangegeven bevat de BGT een hoop lagen. Eigenlijk komen alle problemen in de openbare ruimte wat betreft het klimaat neer op verharding. Daarom zullen de volgende lagen gebruikt gaan worden om een eerste indruk te geven van het probleem qua klimaatadaptatie: verharding, groen, bomen, water en bebouwing. In alle gevallen wordt er simpel gekeken naar de betreffende hoeveelheid van elke laag per indeling, zeg per buurt of wijk.

Voor water speelt de hoogte ook mee, daarvoor is het AHN toegevoegd aan de andere lagen. Maar ook voor hitte-eilanden, omdat in smalle stegen warmte misschien meer blijft hangen. 

### Datamodellen

Om tot informatie te komen die betrekking hebben op de klimaatadaptatie zal nog wel een model gemaakt moeten worden die gebruik maakt van de data die vanuit de BGT en de AHN komt. De informatie kan enigzins intimiderend overkomen, maar dit is noodzakelijk om tot een representatie te komen van de werkelijkheid. Hiervoor gaan we een aantal definities gebruik: constantes en elementen uit de BGT.

Constantes zijn waardes die uit documentatie komt, vaak gemiddelde waardes die nog wel eens verschillen afhankelijk van de bron. Deze waardes hoeven dus zeker niet als absoluut gezien te worden, maar worden hier gebruikt als startpunt.

| Symbool | Definitie | Waarde | Eenheid |
| --- | --- | --- | --- |
| `R` | Gemiddelde regen per vierkante meter per jaar | 0.9475 | m<sup>3</sup> |
| `A_boom` | Gemiddelde oppervlakte van een boom | 65.61 | m<sup>2</sup> |
| `p_boom` | Percentage 'waterconsumptie' per boom | 60 | % |
| `co2_hh` | CO<sub>2 per huishouden per jaar | 1500 | kg |
| `co2_weg` | CO<sub>2 per meter weg per jaar | 105 | kg |
| `co2_boom` | CO<sub>2 'consumptie' per boom per jaar | 21.77 | kg |
| `T` | Gemiddelde temperatuursverhoging door verharding | 6 | ℃ |

Met behulp van de lagen ui de BGT kunnen de volgende elementen bepaald worden, die per wijk/buurt of wat dan ook berekend kunnen worden.

| Symbool | Definitie | Eenheid |
| --- | --- | --- |
| `A_bebouwd` | Oppervlakte dat bebouwd is (gebouwen) | m<sup>2</sup> |
| `A_verhard` | Oppervlakte dat verhard is | m<sup>2</sup> |
| `A_onverhard` | Oppervlakte dat noch verhard noch bebouwd is | m<sup>2</sup> |
| `A_totaal` | Totale oppervlakte | m<sup>2</sup> |
| `bomen_verhard` | Aantal bomen in verharde gebieden | - |
| `bomen_totaal` | Totaal aantal bomen | - |
| `huishoudens` | Totaal aantal huishoudens | - |
| `len_weg` | Totale lengte aan weg | m |

Hieronder zijn per subthema (lucht, water, hitte) de precieze modellen weergegeven plus een korte opmerking met het idee erachter.

#### Lucht

> Bij ontbreken van gegevens over industrieen, zijn huishoudens en verkeer de grootste boosdoeners. Bomen vangen daarentegen CO2 op.

            co2_hh*huishoudens + co2_weg*len_weg - co2_boom*bomen_totaal
    Lucht = ------------------------------------------------------------
                                        A_totaal

| Oorzaak | Formule |
| ------- | ------ |
| Huishoudens | `co2_hh*huishoudens/A_totaal` |
| Verkeer | `co2_weg*len_weg/A_totaal` |
| Bomen | `co2_boom*bomen_totaal/A_totaal` |

#### Water

> Het water dat op gebouwen valt, zal via de verharding weg moeten vloeien. Verder vangen bomen een deel van het water op.

            R*(A_verhard + A_bebouwd) - R*A_boom*p_boom*bomen_verhard
    Water = ---------------------------------------------------------
                                    A_verhard

| Oorzaak | Formule |
| ------- | ------ |
| Verharding | `R*A_verhard` |
| Bebouwing | `R*A_bebouwd` |
| Bomen | `R*A_boom*p_boom*bomen_verhard/A_verhard` |

#### Hitte

> Zonlicht warmt verharding op. Hoe meer verharding des te meer deze bijdrage. Bomen vangen een deel van het zonlicht op en zorgen voor actieve verkoeling door verdamping.

De verkoeling door bomen is met de huidige constantes zodanig minimaal dat die weggelaten zijn uit de formule. Ook is de impact van de hoogte van straten en stegen niet meegenomen omdat dit te uitgebreid wordt.

            T*A_verhard - T*A_boom*bomen_verhard
    Hitte = ------------------------------------
                  A_verhard + A_onverhard

| Oorzaak | Formule |
| ------- | ------ |
| Verharding | `T*A_verhard/(A_verhard + A_onverhard)` |
| Bomen | `T*A_boom*bomen_verhard/(A_verhard + A_onverhard)` |

## Van informatie naar presentatie

### Het model

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kam.png" target="_blank" alt="imageStyle: Wateroverlas"/>
<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kam_buurt.png" target="_blank" alt="imageStyle: Wateroverlas"/>
<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kam_lucht.png" target="_blank" alt="imageStyle: Wateroverlas"/>
<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kam_water.png" target="_blank" alt="imageStyle: Wateroverlas"/>    
<img class="imageStyle shadowing" src="/docs/assets/Kookboek/kam_hitte.png" target="_blank" alt="imageStyle: Wateroverlas"/>    

### Uitgebreid

<img class="imageStyle shadowing" src="/docs/assets/Kookboek/heat.png" target="_blank" alt="imageStyle: Wateroverlas"/>
<img class="imageStyle shadowing" src="/docs/assets/Kookboek/twi.png" target="_blank" alt="imageStyle: Wateroverlas"/>
