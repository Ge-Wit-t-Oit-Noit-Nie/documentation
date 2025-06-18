# Instructieset

De volgende instructies zijn beschikbaar:

<!-- no toc -->
- [STOPPEN](#stoppen)
- [PAUZE](#pauze)
- [Wachten](#wachten)
- [ZET\_POORT\_AAN](#zet_poort_aan)
- [ZET\_POORT\_UIT](#zet_poort_uit)
- [FLIP\_POORT](#flip_poort)
- [BEWAAR\_STATUS](#bewaar_status)
- [SPRING](#spring)

## STOPPEN

De functie STOPPEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0000 0000      | 0x00   |           |

Deze functie is by default ingevult in het geheugen.

### Voorbeeld

```c
STOPPEN;
```

## PAUZE

De functie PAUZE wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0001 0000           | 0x10   |           |

Deze functie is by default ingevult in het geheugen.

### Voorbeeld

```c
PAUZE;
```

## Wachten

De functie WACHTEN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0010 0000           | 0x2000 |           |
| OPCODE  | 0b0000 1111 1111 1111 | 0x0FFF |           |

De maximale delay is dus 4095 seconden

### Voorbeeld

```c
WACHTEN(INDEX=1500);
```

## ZET_POORT_AAN

De functie ZET_PORT_AAN wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0011 0000 0000 0000 | 0x3000 |                   |
| STATUS  | 0b0000 0001 0000 0000 | 0x0100 |                   |
| HSIO    | 0b0000 0001 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| POORT   | 0b0000 0000 0001 1111 | 0x001F | POORT             |

De PORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
ZET_POORT_AAN (POORTNR=0x00, HSIO=0x00);
```

## ZET_POORT_UIT

De functie ZET_POORT_UIT wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0100 0000 0000 0000 | 0x3000 |                   |
| STATUS  | 0b0000 0000 0000 0000 | 0x0000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| POORT   | 0b0000 0000 0001 1111 | 0x001F | POORT             |

De POORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
ZET_POORT_UIT (POORTNR=0x00, HSIO=0x00);
```

## FLIP_POORT

De functie FLIP_POORT wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter         |
| ------- | --------------------- | ------ | ----------------- |
| OPCODE  | 0b0100 0000 0000 0000 | 0x4000 |                   |
| HSIO    | 0b0000 0010 0000 0000 | 0x0200 | HSIO (0x0 / 0x01) |
| POORT   | 0b0000 0000 0001 1111 | 0x001F | POORT             |

De POORT is een van de 13 (0-12) gewone IO Poorten of 0-8 HSIO poorten.

### Voorbeeld

```c
FLIP_POORT (POORTNR=0x01, HSIO=1);
```

## BEWAAR_STATUS

De functie BEWAAR_STATUS wordt als volgt gecodeerd:

| Element | Bitmask               | Hex    | Parameter |
| ------- | --------------------- | ------ | --------- |
| OPCODE  | 0b0110 0000           | 0x50   |           |

### Voorbeeld

```c
BEWAAR_STATUS;
```

## SPRING

De functie SPRING wordt als volgt gecodeerd:

| Element | Bitmask                         | Hex      | Parameter         |
| ------- | ------------------------------- | ------   | ----------------- |
| OPCODE  | 0b0111 0000 0000 0000 0000 0000 | 0x600000 |                   |
| INDEX   | 0b0000 0001 1111 1111 1111 1111 | 0x01FFFF | INDEX             |

### Voorbeeld

```c
SPRING (index=0x0003);
```
