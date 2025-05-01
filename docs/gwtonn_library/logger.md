# Logger

De logger wordt gebruikt om cruciale informatie op te slaan over de staat van de STM32 en het programma.

## Voorbeeld

Kijk naar de volgende entry:

```csv
[13:18:16],16,3,9,64100,149
```

De volgende gegevens worden weergegeven:

* **[13:18:16]**: Tijd van het bericht
* **16**: Bericht soort (MSG_PROGRAM_COUNTER)
* **3**: *instruction_pointer* op moment van loggen
* **9**: *shutdown_index* op moment van loggen
* **64100**: Interne temperatuur van de STM32
* **149**: Actuele voltage op moment van schrijven van de STM32

## Logbericht sturen

Om een bericht te loggen dient er een bericht op de queue gezet te worden. Volgende stukje code is een voorbeeld:

```c
MSGQUEUE_OBJ_t msg = {
	MSG_PROGRAM_COUNTER,
	pcr.instruction_pointer,
	pcr.shutdown_instruction_pointer,
	get_temperature(),
	get_vref(),
	};
if (osOK != osMessageQueuePut(loggerQueueHandle, &msg, 0, 0U))
{
	printf("Error: Could not send message to loggerQueueHandle\n\r");
}
```

Zoals je kan zien wordt er eerst een bericht aangemaakt. Daarna wordt deze op de queue gezet (```loggerQueueHandle```). Voor de exacte details van het queue mechanisme kan je kijken bij [ST](https://arm-software.github.io/CMSIS_6/latest/RTOS2/group__CMSIS__RTOS__Message.html).

### Log bericht

Voor het versturen van een log bericht wordt gebruik gemaakt van een structure. 

```c
typedef struct
{
    uint8_t message;
    uint32_t program_counter;
    uint16_t shutdown_index_register;
    uint16_t temperature;
    uint16_t vrefint;
} MSGQUEUE_OBJ_t;
```

Hiervoor geld de volgende definitie:

| Kolom                   | Type     | Omschrijving |
| -----                   | -------- | ------------ |
| message                 | uint8_t  | Een waarde die aangeeft wat het bericht betekened (*MSG_PROGRAM_COUNTER*) |
| program_counter         | uint32_t | De huidige waare van de *instruction_pointer* |
| shutdown_index_register | uint16_t | De huidige waarde van de *shutdown_index_register* |
| temperature             | uint16_t | De huidige temperatuur van de STM32 in graden celcius * 1000 |
| vrefint                 | uint16_t | De huidige voltage van de STM32 in mV |