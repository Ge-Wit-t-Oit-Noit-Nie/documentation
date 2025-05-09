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
BEGIN_EINDE_PROGRAMMA_INDEX (index=0x0007);
ZET_PORT_AAN (PORTNR=0x00, HSIO=0x00);
ZET_PORT_UIT (PORTNR=0x01, HSIO=0x00);
WACHTEN (delay=0x05DC);
FLIP_POORT (PORTNR=0x01, HSIO=1);
BEWAAR_STATUS;
SPRING (index=0x0003);
BEWAAR_STATUS;
STOPPEN;
```

In dit programma, worden de volgende stappen uitgevoerd:

1. Bewaar de positie van voor het einde van de programma (instructie 8)
2. Wacht voor 1500ms
3. Zet de IO port 1 op hoog
4. Zet de IO port 1 op laag
5. Flip de high-speed IO port 1
6. bewaar de status (telemetry)
7. spring terug naar de 2de instructie
8. stop het programma

## Compileren

Start een [python](#python-starten) sessie en type het volgende

```ps1
python src/gpc.py -i <input_file> -o <output_file> -v
```

Met de volgende parameters:

* -i, --input: de broncode die gecompileerd moet worden
* -o, --output: het .bin bestand dat gemaakt wordt
* -v, --verbose: Volg de uitput

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
