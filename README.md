# Documentation

Al het goede heeft documentatie nodig.

## Prerequisites

De volgende applicaties zijn nodig:

- mkdocs: >= 1.6.1

## Documentatie lokaal bekijken

Voor het testen van de site gebruik de volgende commando:

```ps1
.\venv\Scripts\activate.ps1
mkdocs serve
```

## Documentatie deployen

Om de documentatie te deployen, kan je handmatig een deploy starten:

```ps1
.\venv\Scripts\activate.ps1
mkdocs gh-deploy
```

Dit script al dan een statische site maken en beschikbaar maken op de gh-pages branch. 

## Prepareren van het systeem

### Installeren van python virtual environment

Voor het gebruik van mkdocs kan het best gebruik gemaakt worden van een virtuele python omgeving. Deze kan je als volgt maken:

```ps1
python -m venv venv
```

Op een windows machine kan je deze activeren met:

```ps1
.\venv\Scripts\activate.ps1
```

Op MaOS or Linux kan je deze activeren met:

```bash
source ./venv/bin/activate
```

### Installatie mkdocs

Voor het gebruik van ```mkdocs``` kan gebruikt worden van een virtuele python omgeving. Zie voor het opzetten van de omgeving [mkdocs website](https://www.mkdocs.org/getting-started/)

```ps1
.\venv\Scripts\activate.ps1
pip install -r requirements.txt
```