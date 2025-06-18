# Over 2025

Hier komt een beschrijving van de setup voor 2025.

## Hardware setup

!!! note
    Maak een schema met de verschillende componenten

### Component 1

### Component 2

## Programma

Beschrijf hier de programma die uitgevoerd moet worden in simpele stappen.

Voeg eventueel een tekening toe met uml:

```puml
@startuml

start
  :store exit index;
repeat
  :zet motor in vooruit;
  :start motor;
  :wacht voor 3 seconden;
  :stop motor;
  :wacht voor 4 seconden;
  :zet motor in reverse;
  :start motor;
  :wacht voor 3 seconden;
  :stop motor;
repeat while (more data?) is (yes) not (no)
  :zet motor in reverse;
  :start motor;
  :wacht voor 4 seconden;
  :stop motor;
    
stop
@enduml
```
