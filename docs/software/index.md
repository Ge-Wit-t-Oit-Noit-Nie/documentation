# Software

Voor het schrijven van de software is er voor gekozen om de **firmware** (aansturing van de hardware) te scheiden van het **programma**. 

Hierbij gelden de volgende definities:

| Component | Omschrijving | Meer info |
| --- | --- | --- |
| Firmware | De code die op alle piggyback hetzelfde is. Dit vormt de laag naar de hardware en voert het programma stap voor stap uit |  [Firmware](./firmware/index.md) |
| Programma | Dit is de set van instructies die een piggyback moet uitvoeren op de dag van de optocht. Deze is eenvoudig te programmeren en kan makkelijk geladen worden vanaf een SD Card | [Programma](./gpc/index.md) |

## Verantwoording

Er is voor dit onderscheid gekozen voor verschillende reden:

1. Het is eenvoudiger om in het Nederlands een programma te maken
2. Het programma is vaak niet meer als het aanzetten van een output, wachten en weer intrekken. De hele firmware specifiek maken is dan complex voor deze taak
3. Op de bouw is het eenvoudiger een SD Card te vervangen dan een volledige flash uit te voeren.