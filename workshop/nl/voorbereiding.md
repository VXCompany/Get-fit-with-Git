# Voorbereidingen workshop

> Voor alle voorbereidingen en requirements geldt: heb je het al in orde, dan kun je een stap/onderdeel overslaan. Zorg in ieder geval, dat je de smoketest (zie onderaan de pagina) succesvol hebt kunnen afronden.

## Software requirements

In de workshop maken we uitsluitend gebruik van de Git CLI, dus deze zullen we geinstalleerd moeten hebben. Wellicht heb je deze al, maar dan is het toch handig om de versie te controleren (en zonodig bij te werken naar de laatste versie).

### Linux en WSL (Windows Subsystem for Linux)

Volg deze stappen of kijk op git-scm voor een uitbreide [handleiding](https://git-scm.com/download/linux):

```bash
sudo apt-get update
sudo apt-get install git
git --version
```

### Windows

Je kunt de software direct bij git-scm [downloaden](https://git-scm.com/download/win) of gebruik maken van Chocolatey:

```bash
choco install git
git --version
```

### MacOS

Volg deze stappen of kijk op git-scm voor een uitgebreide [handleiding](https://git-scm.com/download/mac)

```bash
brew install git
git --version
```

## Config

Git gebruikt lokaal een aantal instellingen voor het juist weergeven van de gebruikersnaam en emailadres. Op deze meeste platformen gaat dit automatisch (er wordt door Git gekeken naar de Username binnen het OS), maar uiteraard is het goed dit te controleren en zonodig aan te passen. Het volgende commando geeft de huidige instellingen weer voor gebruikersnaam en emailadres.

```bash
git config --global --list
```

Indien nodig, kun je de volgende commando's gebruiken om ze aan te passen:

```bash
git config --global user.name "Yuri Burger"
git config --global user.email "yburger@vxcompany.com"
```

## GitHub Account

In deze workshop zullen we gebruik maken van GitHub voor het opslaan van onze centrale repositories. Heb je al een account, dan kun je deze stap overslaan. Het maakt voor de workshop niet uit aan welk email adres je account gekoppeld is.

Heb je nog geen account, dan kun je gebruik maken van de GitHub Sign Up. Deze vindt je hier, rechtsboven: https://github.com/

## Smoketest

Bij deze test controleer je de versie van Git met het volgende commando:

```bash
git --version
```

Op het moment van het maken van de workshop is de laatste versie van Git: 2.30.x
