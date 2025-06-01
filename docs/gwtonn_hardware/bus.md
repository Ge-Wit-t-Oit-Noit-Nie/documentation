# Bus architectuur
Er is voor een bus architectuur gekozen waarbij alle benodigde draden in een kabel gecombineerd zijn. Een bus architectuur gebruikt minimale bekabeling waarbij alle apparaten in een lijn aan elkaar zitten met een kop aan de ene kant en een staart aan de andere kant, zoals te zien is op de afbeelding hieronder. Hiervoor is gekozen zodat er zo min mogelijk losse kabels door de wagen gaan.

![afbeelding van een bus architectuur. Een lijn met aan de ene kant een kop en aan de andere kant een staart. Tussen de kop en de staart zijn apparaten aan de bus verbonden.](./afbeeldingen/bus_architectuur.png)

Deze bus architectuur is galvanisch geisoleerd tot alle individuele modules tot 2 kV, waardoor een module die aan de bus hangt catastrofaal kan falen zonder de rest van het netwerk mee te nemen.

## Fysieke laag
De fysieke aansluiting van de bus is een CAT-5 kabel. Over deze kabel gaan de volgende signalen:

- CAN
- Spanning
- Noodstop

De draad functies worden hieronder gegeven.

| **draadnummer** 	| **kleur**  	| **functie**       	|
|-------------------|---------------|-----------------------|
| 1               	| wit/groen  	| CAN positief      	|
| 2               	| groen      	| CAN negatief      	|
| 3               	| wit/oranje 	| Noodstop positief 	|
| 4               	| blauw      	| Spanning            	|
| 5               	| wit/blauw  	| Spanning          	|
| 6               	| oranje     	| Noodstop negatief 	|
| 7               	| wit/bruin  	| Aarde             	|
| 8               	| bruin      	| Aarde             	|

## Aansluitingen

![ploatje](./afbeeldingen/detailed_bus.png)

### CAN
CAN is een automotive communicatie standaard die bekend staat om zijn robuustheid. Het heeft een positieve en negatieve draad nodig die het liefst een twisted pair vormen.

## Spanning
De CAN bus is een bepaald hardware protocol en heeft dus een driver chip nodig. De CAN bus is galvanisch geisoleerd van de modules en heeft dus aparte spanning nodig. Deze spanning is volgens Power-over-Ethernet standaard gestuurd.

### Noodstop
De noodstop is geimplementeerd met twee kabels, spanning en aarde. Op de kop van de bus wordt een spanning gecreëerd, die de hele bus op en neer gaat, om vervolgens in de kop zelf een relais aanstuurt. Alle noodstoppen staan in serie met elkaar en dus als er een wordt ingedrukt, opent de stroomkring zich. Hierdoor opent de relais die de modules 