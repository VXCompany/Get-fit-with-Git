# Get fit with Git - Cheat Sheet

- [Git concepten](#git-concepten)
- [Git setup](#git-setup)
- [Git basics](#git-basics)

## Git concepten

### Workflow

Wanneer je een bestand toevoegt of wijzigt, gebruikt Git de volgende workflow om deze wijzigingen centraal door te voeren:

![](/images/workflow1.png)

1. Een nieuw bestand (of gewijzigd bestand) bevindt zich in de "Working Directory";
2. "git add" zorgt er voor, dat deze wijziging klaar gezet wordt in de "Staging Area";
3. "git commit" past de wijziging toe in de lokale repo;
4. "git push" voert de wijziging door op de centrale repo;

### Data Transport

Naast de standaard workflow voor het verwerken van wijzigingen, zijn er nog meer commando's die data (of beter: "state") verplaatsen:

![](/images/datatransport1.png)

- "git fork": maakt een centrale kopie repo van een upstream repo;
- "git clone": maakt en configureert een lokale kopie van een repo;
- "git add, commit en push": zie "Workflow";
- "git commit -a": voegt de stappen "git add en git commit" samen;
- "git pull of rebase": verwerkt centrale branch wijzigingen lokaal;
- "git fetch": haalt alle centrale wijzigingen op;
- "git checkout": wisselt van branch (en werkt de lokale index bij);
- "pull request": proces om eigen centrale wijzigingen verwerkt te krijgen in een upstream repo.

### HEAD

HEAD is in Git een referentie ("pointer") naar de laatste commit in de huidige branch. We gebruiken dit vaak als "shortcut", zodat we niet steeds hashes hoeven op te zoeken.

### Hash

Wijzigingen in een Git repo (de feitelijke "commits") worden in het log bijgehouden met een SHA-1 hash van 40 karakters. We kunnen in onze Git commando's verwijzen naar dergelijke commits door een deel (minimaal 4) van deze karakters te gebruiken. Voorwaarde is, dat Git genoeg karakters heeft om een commit uniek te kunnen identificeren in de repository.

### Origin, remote

In Git wordt vaak verwezen naar "origin". Dit is een referentie naar de remote repository waar de lokale repository van ge-cloned is. De naam "origin" is overigens een conventie, dus je kunt andere namen tegenkomen.

![](/images/remote2.png)

## Git setup

### Clone

Maakt en configureert een lokale kopie van een repo. Doet achter de schermen gelijk een "git fetch" en een "git pull" om de default branch lokaal te "mergen". Checked als laatste stap de default branch uit. Je hebt hier dus centraal (bijvoorbeeld op GitHub of Azure DevOps) een geinitialiseerde repository voor nodig.

![](/images/clone2.png)

```bash
git clone {de URL van de remote repository}
```

### Add remote

Koppelt een lokale repository aan een niet-geinitialiseerde centrale repository (repository bestaat wel, maar is nog helemaal leeg/ongebruikt).

![](/images/remote1.png)

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin {de URL van de remote repository}
git push -u origin main
```

- "git init": initialiseer een lokale directory als lokale repository;
- "git branch -M": hernoem ("Move") een lokale branch (in dit geval van "master" naar "main");
  "git remote add origin": koppel de centrale (lege) repo toe als remote (met de referentie "origin").

### Fork

Wanneer we een upstream repo hebben, bijvoorbeeld in de vorm van een community Open Source Software project, kunnen we hier een eigen kopie van maken. Dit is gebruikelijk wanneer je wijzigingen wilt kunnen voorstellen op die Open Source repository. Een dergelijke eigen kopie wordt een "Fork" genoemd.

![](/images/fork1.png)

## Git basics

### Status

Vraag de status van een repository op met:

```bash
git status
```

### Add

> Wat zijn "Untracked files"?
> Untracked files zijn bestanden in onze werk directory die zijn aangepast, maar nog niet door Git worden bijgehouden.
> Deze Untracked files worden in een volgende commit dus niet meegenomen.

Een file (nieuw of met wijzigingen) toevoegen aan de zogeheten "Staging Area", waarbij we Git vertellen dat dit bestand wel moet worden meegenomen bij de volgende commit.

```bash
git add index.html
```

Als alternatief kunnen we ook alle bestanden (die niet in de .gitignore file staan) mee laten nemen:

```bash
git add -A # of git add .
```

### Commit

Git houdt de Stating Area in de gaten, maar eventuele wijzigingen zijn nog niet opgenomen in onze lokale repository. Omdat te doen, gebruiken we het volgende commando:

```bash
git commit -m "Dit is het commentaar dat in de history wordt opgenomen"
```

### Push

Onze lokale Git repo is bijgewerkt (met het commit commando). Als we nu ook de remote repository willen bijwerken, moeten we onze wijzigingen "pushen"

```bash
git push
```

### Pull

"git pull" is een shortcut voor "git fetch" + "git merge FETCH_HEAD". Fetch haalt de laatste stand van zaken binnen, maar houdt die nog even apart van onze lokale branch. Git doet dat door gebruik te maken van een nieuwe pointer: FETCH_HEAD. Wanneer er wijzigingen (nieuwe commits) zijn ten opzichte van de huidige branch, dan volgt er:

- een fast-forward: we hebben lokaal geen nieuwe commits => dan worden de commits van de remote branch zonder problemen toegevoegd aan onze branch (en dat zonder een nieuwe commit te maken);
- een merge, we hebben lokaal wel nieuwe commits => dan worden de commits van de remote branch aan onze branch toegevoegd in een nieuwe commit. Conflicten worden middels een merge conflict opgelost;
- een rebase, dit werkt de lokale branch bij met de centrale commits en past dan de lokale wijzigingen weer toe (er boven op).

Wanneer je niets meegeeft, dan zal de standaard strategie een "merge" zijn. Dit doet Git dan ook als er lokaal ook wijzigingen zijn. Zijn die er echter niet, dan zal Git eerst een "fast-forward" proberen (Git is "lui") ! Door je standaard strategie op "fast-forward only" te zetten, kun je er voor zorgen dat je alleen lokaal bijwerkt als dat zonder bijwerkingen kan.

```bash
git pull
```
