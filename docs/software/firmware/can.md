# CAN

Voor de communicatie tussen de verschillende borden, wordt gebruik gemaakt
van het CAN protocol.

## Sequence diagram

```puml
@startuml
participant master [
    =Controller
]
participant client_id1 [
    =Client
    ----
    ""device_id""
]

group Broadcast
    master -> client_id1: message[time]
    master -> client_id1: message[start]
    master -> client_id1: message[whoisthere]
    client_id1 --> master: ACK(device_id)
end

group Directed
    master -> client_id1: message[ping(device_id)]
    client_id1 --> master: ack(device_id)
    
    client_id1 -> master: message[fault(device_id, code)]
    master --> client_id1: ack(device_id)
end

@enduml

```

### Type bericht

Zoals zichtbaar in de sequence diagram, zijn er 2 soorten berichten

- **Broadcast**: Dit bericht is voor iedereen bestemd.
- **Directed**: Dit bericht is specifiek voor een bord.


## CAN bericht

Ieder bericht volgt een vast patroon:

- BERICHT_CODE (1 BYTE)
- (OPTIONEEL) BOARD_ID
- DATA (0-x BYTE)
- TERMINATION (0xFF, 0xFF, 0xFF)

## Bericht specificatie

Ieder bericht heeft een specifieke code. In dit hoofdstuk wordt
de specificatie van ieder bericht gegeven.

### TIME

Het tijd bericht verstuurd de actuele clocktijd. Dit bericht kan
gebruikt worden om de RTC te corrigeren.

| Type bericht | Bericht code | Data         |
| ------------ | ------------ | ------------ |
| BROADCAST    | 1            | encoded_time |
