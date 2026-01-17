# Logger

De logger wordt gebruikt om cruciale informatie op te slaan over de staat van de
STM32 en het programma.

Voor het opslaan wordt een bestand aangemaakt op de SD Kaart met de naam "logger.txt".

## Voorbeeld

Kijk naar de volgende entry:

```csv
[00:00:01],18,458,2826,288,0
```

De volgende gegevens worden weergegeven:

* **[00:00:01]**: Tijd van het bericht
* **18**: De instructiepointer
* **458**: *shutdown_index* op moment van loggen
* **2826**: Interne temperatuur van de STM32
* **288**: Actuele voltage op moment van schrijven van de STM32
* **0**: De hardware trigger die deze log genereerde (indien beschikbaar, anders 0)

!!! note Opmerking
    Er is een beperking in de firmware dat een **float** niet goed geformateerd word.
    De temperatuur en de voltage worden weggeschreven als integers.
    Om de actuele waarde te hebben, moet de temperatuur en voltage
    door 100 gedeeld worden.
    ```float temp = temperature / 100```

## Logbericht sturen

Om een bericht te loggen dient er een bericht op de queue gezet te worden. 
Volgende stukje code is een voorbeeld:

```c
telemetry_t telemetry = {
    program_controller_registers->instruction_pointer,
    program_controller_registers->shutdown_instruction_pointer,
    0,
};
if (osOK != osMessageQueuePut(loggerQueueHandle, &telemetry, 0, 0U))
{
printf("Error: Could not send message to loggerQueueHandle\n\r");
}
```

Zoals je kan zien wordt er eerst een bericht aangemaakt.
Daarna wordt deze op de queue gezet (```loggerQueueHandle```).
Voor de exacte details van het queue mechanisme kan je kijken bij [ST](https://arm-software.github.io/CMSIS_6/latest/RTOS2/group__CMSIS__RTOS__Message.html).

### Log bericht

Voor het versturen van een log bericht wordt gebruik gemaakt van een *structure*.

```c
typedef struct
{
    uint16_t instruction_pointer;
    uint16_t shutdown_index_register;
    uint8_t trigger;
} telemetry_t;
```

Hiervoor geld de volgende definitie:

| Kolom                   | Type     | Omschrijving |
| -----                   | -------- | ------------ |
| instruction_pointer     | uint32_t | De huidige waare van de *instruction_pointer* |
| shutdown_index_register | uint16_t | De huidige waarde van de *shutdown_index_register* |
| trigger                 | uint8_t | Het event dat de log initieerde |