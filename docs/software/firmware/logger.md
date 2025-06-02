# Logger

De logger wordt gebruikt om cruciale informatie op te slaan over de staat van de
STM32 en het programma.

Voor het opslaan wordt een bestand aangemaakt op de SD Kaart met de naam "logger.txt".

## Voorbeeld

Kijk naar de volgende entry:

```csv
[00:00:09],0x00000005,0x00000007,0x00001A9E,0x00000633,0x000000F0
```

De volgende gegevens worden weergegeven:

* **[13:18:16]**: Tijd van het bericht
* **0x00000005**: De instructiepointer
* **0x00000007**: *shutdown_index* op moment van loggen
* **0x00001A9E**: Interne temperatuur van de STM32
* **0x00000633**: Actuele voltage op moment van schrijven van de STM32
* **0x000000F0**: De hardware trigger die deze log genereerde (indien beschikbaar, anders 0)

## Logbericht sturen

Om een bericht te loggen dient er een bericht op de queue gezet te worden. 
Volgende stukje code is een voorbeeld:

```c
telemetry_t telemetry = {
	program_controller_registers->instruction_pointer,
	program_controller_registers->shutdown_instruction_pointer,
	is_get_temperature(),
	is_get_vref(),
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
    uint16_t temperature;
    uint16_t vrefint;
    uint8_t trigger;
} telemetry_t;
```

Hiervoor geld de volgende definitie:

| Kolom                   | Type     | Omschrijving |
| -----                   | -------- | ------------ |
| instruction_pointer     | uint32_t | De huidige waare van de *instruction_pointer* |
| shutdown_index_register | uint16_t | De huidige waarde van de *shutdown_index_register* |
| temperature             | uint16_t | De huidige temperatuur van de STM32 in graden celcius * 1000 |
| vrefint                 | uint16_t | De huidige voltage van de STM32 in mV |
| trigger                 | uint8_t | Het event dat de log initieerde |