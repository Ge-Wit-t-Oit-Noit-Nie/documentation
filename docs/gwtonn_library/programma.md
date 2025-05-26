# Programma

Het hele idee van de controller is om een progarmma uit te voeren. Om dit flexibel te maken, is er een basis [instructieset](#instuctieset) gemaakt. Met deze instructieset kan een programma gemaakt worden.

## Programmeren

Een programma wordt geschreven in een textfile. Deze kan een willekeurige extentie hebben, maar ```.gpc``` is de standaard.

Een programma bestaat uit een [instructie](#instructieset) per regel.

Als voorbeeld:

```txt
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

Op zichzelf kan ene prorgramma niet uitgevoerd worden. Deze moet gecompileerd worden, en vervolgens geladen worden. 

Voor het compileren van het programma kan ge bruik gemaakt worden van de De [Ge Wit't Oit Noit Nie Programma Compiler](https://github.com/Ge-Wit-t-Oit-Noit-Nie/gpc) (GPC). 

Het laden van het programma kan op 2 manieren:

1. Compileer het programma mee in de firmware
2. Laad het programma via een SD Card

### Compileer het programma mee in de firmware

Om het programma te laden via de firmware dien je het programma eerst te compileren. Hier staat beschreven hoe je kan compileren. 

Start een [python](#python-starten) sessie en type het volgende

```ps1
    python src/gpc.py -i <input_file> -o <output_file> -v
```

Met de volgende parameters:

* -i, --input: de broncode die gecompileerd moet worden
* -o, --output: het .bin bestand dat gemaakt wordt
* -v, --verbose: Volg de uitput


!!! info "Voorbeeld"
    Voer de onderstaande code uit in de folder waar je de [GPC](https://github.com/Ge-Wit-t-Oit-Noit-Nie/gpc) repository gedownload hebt. 
    ```ps1
      python src/gpc.py -i .\examples\simpel_programma_2.gpc -o .\binary_file.bin -v
    ```

Vervolgens moet het bestand ```binary_file.bin``` gecopieerd worden naar de root folder van het project wat de firmware bevat. Dan wordt deze automatisch meegenomen tijdes het compilen en uploaden van de firmware. 

### Laad het programma via een SD Card

Om het programma te laden via een SD Card dien je het programma eerst te compileren. Hier staat beschreven hoe je kan compileren. 

Start een [python](#python-starten) sessie en type het volgende

```ps1
    python src/gpc.py -i <input_file> -o <output_file> -v
```

Met de volgende parameters:

* -i, --input: de broncode die gecompileerd moet worden
* -o, --output: het .bin bestand dat gemaakt wordt
* -v, --verbose: Volg de uitput


!!! info "Voorbeeld"
    Voer de onderstaande code uit in de folder waar je de [GPC](https://github.com/Ge-Wit-t-Oit-Noit-Nie/gpc) repository gedownload hebt. 
    ```ps1
      python src/gpc.py -i .\examples\simpel_programma_2.gpc -o .\binary_file.bin -v
    ```

Vervolgens copieer het bestand naar de root van een SD Card. Deze kan je dan in de kaartlezer stoppen. Haal de stroom van de piggy bag en zet er opnieuw stroom op. Het programma wordt nu automatisch in het geheugen geladen. De SD Card kan nu verwijderd worden.

## Instructieset

De volgende instructies zijn beschikbaar:

- [STOPPEN](#stoppen)
- [BEGIN\_EINDE\_PROGRAMMA\_INDEX](#begin_einde_programma_index)
- [Wachten](#wachten)
- [ZET\_PORT\_AAN](#zet_port_aan)
- [ZET\_PORT\_UIT](#zet_port_uit)
- [FLIP\_POORT](#flip_poort)
- [BEWAAR\_STATUS](#bewaar_status)
- [SPRING](#spring)

### STOPPEN

De functie STOPPEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0000 0000 0000 0000 | 0x0000 |           |

Deze functie is by default ingevult in het geheugen.

### BEGIN_EINDE_PROGRAMMA_INDEX

De functie BEGIN_EINDE_PROGRAMMA_INDEX wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0001 0000 0000 0000 | 0x1000 |           |
| DELAY   | 0b0000 1111 1111 1111 | 0x0FFF | INDEX     |

De maximale index is dus 4095

### Wachten

De functie WACHTEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0010 0000 0000 0000 | 0x2000 |           |
| DELAY   | 0b0000 1111 1111 1111 | 0x0FFF | DELAY     |

De maximale delay is dus 4095 ms

### ZET_PORT_AAN

De functie ZET_PORT_AAN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0011 0000 0000 0000 | 0x3000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| HIGH    | 0b0000 0001 0000 0000 | 0x0100 |                   |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### ZET_PORT_UIT

De functie ZET_PORT_AAN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0100 0000 0000 0000 | 0x4000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| HIGH    | 0b0000 0001 0000 0000 | 0x0100 |                   |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### FLIP_POORT

De functie FLIP_POORT wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0101 0000 0000 0000 | 0x5000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### BEWAAR_STATUS

De functie BEWAAR_STATUS wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0110 0000 0000 0000 | 0x6000 |                   |

### SPRING

De functie BEWAAR_STATUS wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0110 0000 0000 0000 |        |                   |
| INDEX   | 0b0000 1111 1111 1111 | x0FFF  | Spring direct naar index                  |

## Geheugen

Voor het verwerken van het progamma heeft de firmware een stukje geheugen gereserveerd. Op de STM32F412xG zijn 11 sectoren in het geheugen aanwezig. Voor onze firmware reserveren we een sector om het programm in op te slaan. Door een hele sector te reserveren kunnen we Over-the-Air updates of updates vanaf de SD Card beter uitvoeren.

Binnen de F412xG zijn de eerste 5 sectoren 64Kb per stuk. De andere sectoren zijn 128Kb per stuk. Aangezien we ons programm aan het einde willen opslaan in de firmware, betekend dit dat we 128Kb tot onze beschikking hebben.

In de [linker script](https://github.com/Ge-Wit-t-Oit-Noit-Nie/2025-software/blob/main/STM32F412XX_FLASH.ld) is dit terug te vinden:

```ld
MEMORY
{
    RAM (xrw)      : ORIGIN = 0x20000000, LENGTH = 256K
    FLASH (rx)     : ORIGIN = 0x08000000, LENGTH = 1024K - 128k
    RESERVED (rw)  : ORIGIN = 0x080E0000, LENGTH = 128k
}
.program_data_block :
{
  _program_data_start = .;
  FILL(0x00); /* Fill the section with 0xFF */
  binary_file.o(.program_data_block)
  KEEP(*(.program_data_block))
  _program_data_end = .;
} > RESERVED 
```

### Geheugen vulling

Bij het reserveren van de sector (zie vorige paragraaf) wordt het geheugen gevult met 0x00. Doordat de HALT instructie de waarde 0x00 heeft, zal effectief het hele geheugen dus vol staan met HALT (totdat er een programma geladen wordt).

Bij het compileren wordt het binare bestand ```binary_file.o``` meegeladen in het geheugen. 

### Data gebruik

Na het linken van de code, wordt er een overzicht gegeven van het geheugen en de grote. De volgende 3 regio's zijn aanwezig:

- RAM
- FLASH
- RESERVED

Het programma wordt opgeslagen in het ```RESERVED``` blok. De volledige block is beschikbaar voor het maken van een programma.

Voorbeeld van een output. In deze output is te zien dat *5.49%* gebruikt is.

```sh
[build] Memory region         Used Size  Region Size  %age Used
[build]              RAM:       25872 B       256 KB      9.87%
[build]            FLASH:       55824 B    1044496 B      5.34%
[build]         RESERVED:         224 B       4080 B      5.49%
```