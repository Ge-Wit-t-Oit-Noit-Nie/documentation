# Instructieset

De volgende instructies zijn beschikbaar:

<!-- no toc -->
- [STOPPEN](#stoppen)
- [BEGIN\_EINDE\_PROGRAMMA\_INDEX](#begin_einde_programma_index)
- [Wachten](#wachten)
- [ZET\_PORT\_AAN](#zet_port_aan)
- [ZET\_PORT\_UIT](#zet_port_uit)
- [FLIP\_POORT](#flip_poort)
- [BEWAAR\_STATUS](#bewaar_status)
- [SPRING](#spring)

## STOPPEN

De functie STOPPEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0000 0000 0000 0000 | 0x0000 |           |

Deze functie is by default ingevult in het geheugen.

### Voorbeeld

```c
STOPPEN;
```

## BEGIN_EINDE_PROGRAMMA_INDEX

De functie BEGIN_EINDE_PROGRAMMA_INDEX wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0001 0000 0000 0000 | 0x1000 |           |
| DELAY   | 0b0000 1111 1111 1111 | 0x0FFF | INDEX     |

De maximale index is dus 4095

### Voorbeeld

```c
BEGIN_EINDE_PROGRAMMA_INDEX(INDEX=0x0011);
```

## Wachten

De functie WACHTEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0010 0000 0000 0000 | 0x2000 |           |
| DELAY   | 0b0000 1111 1111 1111 | 0x0FFF | DELAY     |

De maximale delay is dus 4095 ms

### Voorbeeld

```c
WACHTEN(INDEX=1500);
```

## ZET_PORT_AAN

De functie ZET_PORT_AAN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0011 0000 0000 0000 | 0x3000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| HIGH    | 0b0000 0001 0000 0000 | 0x0100 |                   |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
ZET_PORT_AAN (PORTNR=0x00, HSIO=0x00);
```

## ZET_PORT_UIT

De functie ZET_PORT_AAN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0100 0000 0000 0000 | 0x4000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| HIGH    | 0b0000 0001 0000 0000 | 0x0100 |                   |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
ZET_PORT_UIT (PORTNR=0x00, HSIO=0x00);
```

## FLIP_POORT

De functie FLIP_POORT wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0101 0000 0000 0000 | 0x5000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| PORT    | 0b0000 0000 0001 1111 | 0x001F | PORTNR            |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
FLIP_POORT (PORTNR=0x01, HSIO=1);
```

## BEWAAR_STATUS

De functie BEWAAR_STATUS wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0110 0000 0000 0000 | 0x6000 |                   |

### Voorbeeld

```c
BEWAAR_STATUS;
```

## SPRING

De functie BEWAAR_STATUS wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0110 0000 0000 0000 |        |                   |
| INDEX   | 0b0000 1111 1111 1111 | x0FFF  | Spring direct naar index |

### Voorbeeld

```c
SPRING (index=0x0003);
```
