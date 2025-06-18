# GPC

De Ge Wit't Oit Noit Nie Programma Compiler!

## Programma

Een programma wordt geschreven in een textfile. Deze kan een willekeurige
extentie hebben, maar ```.gpc``` is de standaard.
Een programma bestaat uit een [instructie](./program_specifications.md) per regel.
Iedere regel wordt afgesloten met een ';'.

In principe heeft een instructie 0, 1, 2 of 3 parameters. Iedere parameter wordt
voorzien van de volgende structuur: ```<<INSTRUCTIE>> (<<PARAM>>);```.

Wanneer een parameter gezet wordt, dan bestaad deze uit een identifier
en een numerieke waarde.

### Numerieke waarde

In een programma kan gebruikt worden van een numerieke waarde.
Deze waarde kan opgegeven worden in Hexadecimaal, binair en decimaal.

Standaard wordt decimaal gebruikt: **123**.

Wanneer er gebruik gemaakt wordt van hexadecimaal, dan wordt de
waarde voorzien van de prefic: ```0x```. Het getal wordt vervolgens
geschreven met normale hexadecimale getallen: **0-9A-F**.

Voor het gebruik van een binair getal wordt de prefix ```0b``` gebruikt.
De waarde wordt dan gezet met behulp van **1** en **0**.

De volgende getallen zijn dan allemaal hetzelfde:

- 163
- 0xA3
- 0b10100011

### Voorbeeld

Bekijk het volgende voorbeeld

```c
BEGIN_PROGRAMMA:
 ZET_POORT_AAN (POORT=0x00, HSIO=0x00);
 ZET_POORT_UIT (POORT=0x01, HSIO=0x00);
 WACHTEN (delay=0x05DC);
 FLIP_POORT (POORT=0x01, HSIO=1);
 BEWAAR_STATUS;
 SPRING (index=0x0003);

PAUZE_PROGRAMMA:
 ZET_POORT_AAN (POORT=0x0F, HSIO=0x00);
 PAUZE;

EINDE_PROGRAMMA:
 BEWAAR_STATUS;
 STOPPEN;
```

In dit programma, worden de volgende stappen uitgevoerd:

1. Identificeer het begin programma
   1. Zet de IO Port 0 aan
   2. Zet de IO Port 1 uit
   3. Wachten voor 0x05dc seconden
   4. Bewaar de status op dit moment
   5. Spring terug naar index 0x03
2. Identificeer het pauze programma
   1. Zet de IO Port 0x0F aan
3. Identifiveer het einde programma
   1. Bewaar de status
   2. Stop het programma

## Compileren

### Taskfile.dev

Voor het eenvoudig compileren is er een *taskfile* aangemaakt.
Deze kan aangeroepen worden met:

```p1
task board_01
```

In dit geval zal een bestand aangemaakt worden in de build directory met de naam
*board_01.bin*.

Uiteraard kan de naam board_01 vervangen worden door een van de andere programma's.

!!! note Opmerking
    Zorg wel dat je in een virtuele python omgeving zit (Zie [Python starten](#python-starten))

### Python

Start een [python](#python-starten) sessie en type het volgende

```ps1
python src/gpc.py -i <input_file> -o <output_file> -v
```

Met de volgende parameters:

- -i, --input: de broncode die gecompileerd moet worden
- -o, --output: het .bin bestand dat gemaakt wordt
- -v, --verbose: Volg de uitput

### Binair bestand

De output van de compiler is een binair bestand. Deze kan met speciale progarmma's
gelezen worden. [VSCode](https://code.visualstudio.com/) met een
[HEX Editor](https://marketplace.visualstudio.com/items?itemName=ms-vscode.hexeditor)
plugin kan dit bestand gelezen worden.

!!! note "Note"
    Het bestand wordt geschreven in een *big-endian* setup. Dit houdt in dat per
    byte de eerste 4 bits als laatste geschreven worden. Bijvoorbeeld ```WACHTEN(INDEX=1500);```
    wordt vertaald naar ```0x25DC```. Het wordt vervolgens geschreven als ```DC 25```.

## Toevoegen aan de firmware

Voor het gebruik van het programma in de firmware:

1. copieer het bestand ```binary_file.bin``` naar de repository **2025-software** in de root.
2. Maak de cache voor ```CMake``` leeg een compileer de firmware.
3. Upload de firmware.

### Voorbeeld

```ps1
python src/gpc.py -i .\examples\simpel_programma_2.gpc -o .\binary_file.bin -v
```

## Python starten

Voor de compiler gebruiken we een virtuele python omgeving.

```ps1
.\.venv\Scripts\activate.ps1
```

### Virtual env aanmaken

Dit kan gedaan worden met de volgende commande:

```ps1
python -m venv .venv
```
