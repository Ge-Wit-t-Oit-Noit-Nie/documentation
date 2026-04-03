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
verbind_event_met_functie(STOP, label=EINDE);
verbind_event_met_functie(PAUZE, label=PAUZE_PROGRAMMA);
verbind_event_met_functie(VERVOLG, label=RESET);
verbind_event_met_functie(INT06, label=PAUZE_PROGRAMMA);

BEWAAR_STATUS;
spring(label=RESET);

BLINKY:
    zet_poort_aan(poort=1, hsio=0);
    wachten(0xff);
    zet_poort_uit(poort=1, hsio=0);
    wachten(0xff);
    spring(label=BLINKY);

RESET:
    zet_poort_aan(poort=1, hsio=0);
    wachten(0xff);
    spring(label=BLINKY);

EINDE:
    zet_poort_uit(poort=1, hsio=0);
    STOPPEN;

PAUZE_PROGRAMMA:
    PAUZE;
    spring(RESET);
```

In dit programma, worden de volgende stappen uitgevoerd:

1. Verbind het can-event STOP met label EINDE
2. Verbind het can-event PAUZE met label PAUZE_PROGRAMMA
3. Verbind het can-event VERVOLG met label RESET
4. Verbind het can-event INT06 met label PAUZE_PROGRAMMA
5. Verzend de telemetry naar de CAN controller

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
