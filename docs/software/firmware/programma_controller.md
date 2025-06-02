# Programma

Het hele idee van de controller is om een progarmma uit te voeren.
Op deze pagina beschrijven hoe dit werkt.

## Programmeren

Voor het programmeren is een eigen ontwikkeltaal gemaakt. Deze hier beschreven:
[programma speccificatie](../gpc/program_specifications.md).
Na het programmeren moet het programma gecompileerd worden.

Na het compileren moet de programma geschreven worden in het geheugen.
Dat kan op 2 manieren zoals beschreven in de volgende paragrafen.

## Programma laden in de firmware

De eerste methode is het laden van het programma in de firmware.
In basis kan hiervoor de volgende stappenplan gevolgt worden:

1. Schrijf een programma.
2. Compileer het programma met de [gpc](../gpc/index.md)
3. Copieer het bestand dat gemaakt is als output naar de root van de firmware folder
   1. Zorg er voor dat het programma ```binary_file.bin``` heet
4. Compileer en laad de firmware

## Programma laden via de SD Card

Een andere mogelijkheid is het laden van een programma via de SD Card.
Hiervoor dient een bestand met de name ```binary_file.bin``` in de root van
de SD Card staan. Volg de volgende stappen:

1. Schrijf een programma.
2. Compileer het programma met de [gpc](../gpc/index.md)
3. Copieer het bestand dat gemaakt is als output naar de root van een SD Card
   1. Zorg er voor dat het programma ```binary_file.bin``` heet
   2. de SD Card moet FAT32 geformateerd zijn
4. Herstart de STM32 piggybord.

## Werking van de controller

De controller kan gezien worden als een virtuele omgeving. We simuleren een hardware die verschillende instructies (OPCODES) kan uitvoeren.
Deze instructies staan in het geheugen en worden stuk voor stuk uitgevoerd. 

```puml
@startuml
autoactivate on

participant FreeRTOS as RTOS
participant "program_controller" as PC

== Initialization ==
RTOS -> PC : program_controller_task()
PC -> "internal_sensors" : is_set_time
return VM_OK

== Main loop ==

loop
    PC -> PC : fetch_instruction_from_memory
    alt opcode STOPPEN
        PC -> PC: vm_exit
        return terminate_thread
        autoactivate off
        PC -> RTOS : terminate_thread
        autoactivate on
    else opcode BEGIN_EINDE_PROGRAMMA_INDEX
        PC -> PC: vm_store_shutdown_index
        return VM_OK
    else opcode WACHTEN
        PC -> PC: vm_delay
        return VM_OK
    else opcode ZET_POORT_AAN
        PC -> PC: vm_pin_on
        return VM_OK
    else opcode ZET_POORT_UIT
        PC -> PC: vm_pin_off
        return VM_OK
    else opcode FLIP_POORT
        PC -> PC: vm_pin_toggle
        return VM_OK
    else opcode BEWAAR_STATUS
        PC -> PC: vm_pin_toggle
        PC -> Logger : osMessageQueuePut(telemetry)
        return VM_OK
        return VM_OK
    else opcode SPRING
        PC -> PC: vm_pin_toggle
        return VM_OK
    end
end

@enduml
```
