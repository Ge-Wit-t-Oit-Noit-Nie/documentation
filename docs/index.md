# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Prerequisites

De volgende applicaties zijn nodig:

* VSCode: 1.98.2 of hoger
* [STM32CubeCLT](https://www.st.com/en/development-tools/stm32cubeclt.html#st-get-software): >= 1.18.0
* [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html): >= 6.14.0
* [ST-MCU-FINDER-PC](https://www.st.com/en/development-tools/st-mcu-finder-pc.html): >= 6.1.0
* [STM32 VSCode Extension](https://marketplace.visualstudio.com/items?itemName=STMicroelectronics.stm32-vscode-extension)

Verder worden de volgende extenties aangeraden voor VSCode:

### GitHub Suport

* [GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)

### Markdown support

* [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
* [Markdown Table](https://marketplace.visualstudio.com/items?itemName=TakumiI.markdowntable)
* [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

### CMake

* [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)

### C/C++

* [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
* [C/C++ Extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack)

## Hardware

Voor het ontwikkelen van de software wordt gebruik gemaakt van de **Nucleo-F412ZG Development** board

## Middlewares

Voor het schrijven van de log op de SD card wordt gebruik gemaakt van een stukje code in `Middlewares/gwtonn/sd_logger.c`.
Deze code is betrekkelijk simpel. In het vervolg moet hier de logica zitten om de juiste info in de file te krijgen.

> [!IMPORTANT]
> Voor de `startLogTask` is *3000 WORDS* gereserveerd op de stack. We moeten dus opletten met de code (en dus ook wat opschonen).

De functie `startLogTask` wacht op een item in de queue. Wanneer deze binnen komt, dan wordt er een string gemaakt. Deze string wordt naar de UART gestuurd en ook naar de SD_LOGGER.
Voor de sd_logger wordt ook gebruik gemaakt van een MUTEX om te voorkomen dat er 2 schrijfacties tegelijk plaatsvinden.

Voor mee details kan je kijken in de beschrijving van de [bibliotheek](./docs/gwtonn_library.md).

## Tips & Tricks

### Hoe vindt ik mijn STM32 Nuleo USB port in Windows 11 met PowerShell

```ps
Get-PnpDevice -PresentOnly | Where-Object { $_.InstanceId -match '^USB' }
```

### Debug of upload geeft een foutmelding

![Debug settings](docs/images/set_debugger.png)

### Mijn VSCode can de code niet compileren

Controleer of the juiste instellingen voor STM32 zijn gemaakt.

![STM32 Extension settings](docs/images/stm32_extention_settings.png)
