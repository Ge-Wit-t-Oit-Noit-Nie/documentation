# Coding conventions

## Taal

De volgende taal is geadviseerd:

| Onderdeel   | Taal        | Reden |
| ---------   | ----------- | ----- |
| Source Code (+commentaar) | Engels (UK) | Dit is de defacto standaard. STM32 code is in Engels, voorbeelden zijn in Engels en documentation op Internet ook |
| Documentatie (buiten source code) | Nederlands | Ge Wit't Oit Noit Nie is een Nederlandse lokale vereniging. Standaard taal is Nederlands. De documentatie sluit daar beter op aan |

## Leesbaarheid

De code dient leesbaar geshreven te worden. Dit houdt in dat er zoveel mogelijk woorden uitgeschreven worden en geen afkortingen gebruikt worden.

Voorbeelden:

* **get_time**: Correct
* **gt_tm**: Niet correct

!!! note "Note"
    Wanneer een prefix gedaan wordt binnen een header om de functies uniek te maken, dan is dit toegestaan: ```is_get_time``` voor een functie binnen de ```internal_sensor``` header file.

## Bestandsnamen

### lower_case

Wanneer je eigen bestanden toevoegd (zoals in de `docs/` folder), dan wordt dit altijd in *lower_case* gedaan.

!!! warning "Waarschuwing"
    Als uitzondering zijn "CONTRIBUTING.md", "README.md" en "LICENSE". Deze volgen een algemene conventie.
    Bestanden die gemaakt zijn STM32CubeMX zijn ook uitgezonderd.

### Underscore

Wanneer een bestandsnaam uit meerdere woorden bestaad (zoals in dit bestand), dan wordt er altijd gebruik gemaakt van een *underscore*.

## Declaraties

### structure

Wanneer een structure aangemaakt wordt, dan wordt deze in lowercase geschreven. Geen toevoegingen, maar wel ```_``` om woorden te scheiden.

```c
typedef struct program_controller_registers
{
    uint8_t instruction_pointer;
    uint8_t shutdown_instruction_pointer;
};
```

### typdef defenities

Een typedef wordt geschreven in lowercase. Tevens wordt de toevoeging ```_t``` gedaan om te benadrukken dat het een typedef is.

```c
typedef struct
{
    uint8_t instruction_pointer;
    uint8_t shutdown_instruction_pointer;
} program_controller_registers_t;
```

### Enumeraties

Enumeraties worden in hoofdletters geschreven. Wanneer een typedef gemaakt wordt van een enumeratie dan wordt deze (in tegenstellign tot [typedef](#typdef-defenities)) met hoofdtellers geschreven en zonder ```_t```

```c
typedef enum
{
    // Control flow
    OPCODE_HALT = 0x00,
    OPCODE_JUMP = 0x01,
    OPCODE_STORE_SHUTDOWN_INDEX = 0x02,

    // Specific
    OPCODE_PIN_TOGGLE = 0x10,
    OPCODE_PIN_STATE = 0x11,

    // Program related
    OPCODE_DELAY = 0x20,
    OPCODE_LOG_PROGRAM_STATE = 0x21,

} OPCODE;
```

## Markdown

Voor de documentatie word gebruik gemaakt van Markdown. Meer specifiek de GitHub variant: [GitHub specificatie](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

Voor de callouts (WARNING, INFO, ...) wordt gebruik gemaakt van de [admonitations](https://jimandreas.github.io/mkdocs-material/reference/admonitions/) plugin. Deze heeft een speciale manier voor het maken van de waarschuwing, informatie of voorbeeld boxen. Zie de link voor meer informatie.
