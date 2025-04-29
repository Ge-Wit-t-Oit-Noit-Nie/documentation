# Welkom bij de documentatie van GWTONN

Voor algemene informatie over Ge Wit't Oit Noit Nie kijk op onze [website](https://gewittoitnoitnie.nl/).

## Project layout

```bash
    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        year/
            2025/ # All about the year 2025 setup
        gwtonn_library/ # Specific information about the general GWTONN Library support

```

## Prerequisites

De volgende applicaties zijn nodig:

* [VSCode](https://code.visualstudio.com/): 1.98.2 of hoger
* [Python](https://www.python.org/)
* [mkdocs](https://www.mkdocs.org/): >= 1.6.1

Verder worden de volgende extenties aangeraden voor VSCode:

### GitHub Suport

* [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)

### Markdown support

* [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
* [Markdown Table](https://marketplace.visualstudio.com/items?itemName=TakumiI.markdowntable)
* [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

### YAML Support

* [YAML Language Support by Red Hat](https://marketplace.visualstudio.com/items/?itemName=redhat.vscode-yaml)

## Basis MKDocs gebruik

### Markdown smaak

Voor deze site word gebruik gemaakt van de [admonitations](https://jimandreas.github.io/mkdocs-material/reference/admonitions/) plugin. Deze heeft een speciale manier voor het maken van de waarschuwing, informatie of voorbeeld boxen. Zie de link voor meer informatie. 

### Lokaal bekijken

Voor het testen van de site gebruik de volgende commando:

```ps1
.\venv\Scripts\activate.ps1
mkdocs serve
```

### Documentatie deployen

Om de documentatie te deployen, kan je handmatig een deploy starten:

```ps1
.\venv\Scripts\activate.ps1
mkdocs gh-deploy
```

Dit script al dan een statische site maken en beschikbaar maken op de gh-pages branch. 

!!! Warning "Waarschuwing"
    Als er niet-getrackte bestanden of niet-gecommit werk zijn in de lokale repository waar ```mkdocs gh-deploy``` wordt uitgevoerd, zullen deze worden opgenomen in de pagina's die worden gedeployed.

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