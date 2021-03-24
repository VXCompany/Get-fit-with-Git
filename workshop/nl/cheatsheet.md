# Get fit with Git - Cheat Sheet

- [Git concepten](#git-concepten)
- [Git setup](#git-setup)
- [Git basics](#git-basics)
- [Wijzigingen verwerken](#wijzigingen-verwerken)
- [Wijzigingen ongedaan maken](#wijzigingen-ongedaan-maken)
- [Gouden Regel](#gouden-regel)

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

### Git log

Vraag het log op met:

```bash
git log

# of als oneliner

git log --pretty=oneline
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

### Branch

Samenwerken in Git loopt via branches. Een nieuwe branch met de naam "feature1" maken en lokaal aan werken:

```bash
git branch feature/feature1
git checkout feature/feature1
```

Wanneer je de lokale wijzigingen centraal wil doorvoeren:

```bash
git push

#fatal: The current branch feature/feature1 has no upstream branch.
#To push the current branch and set the remote as upstream, use
#
#    git push --set-upstream origin feature/feature1

git push --set-upstream origin feature/experiment1
```

## Wijzigingen verwerken

## Fast-forward

Fast-forward is dus een eenvoudige manier om zonder bijwerkingen centrale wijzigingen lokaal te integreren. Sterker nog, het is misschien daarom wel aan te raden om je standaard strategie "--ff-only" te maken!

```bash
git pull --ff-only
```

Wil je standaard je "git pull" op die manier laten reageren?

```bash
hint: Pulling without specifying how to reconcile divergent branches is
hint: discouraged. You can squelch this message by running one of the following
hint: commands sometime before your next pull:
hint:
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
```

### Merge

Bij een "merge" worden beide wijzigingen verwerkt en wordt er een nieuwe commit gedaan. We hebben eerder gezien, dat "git pull" een "merge" doet als een "fast-forward" niet mogelijk is.

```bash
git pull
```

Wil je een specifieke branch in de huidige mergen?

```bash
git merge [branch naam]
```

Als Git meldt, dat er een conflict is (en er geen auto-merge kan plaatsvinden) kun je dat direct oplossen door het de file(s) in kwestie te bewerken en er voor te zorgen, dat alleen de wijzigingen overblijven die behouden moeten blijven. Git zet er in commentaar bij, wat waar vandaan komt.

Voorbeeld: De "HEAD" die bovenin staat, verwijst naar de pointer lokaal. De commit hash die onderin staat, verwijst naar 1 specifieke commit in de history uit de branch samengevoegd wordt:

```
#Auto-merging test3.txt
#CONFLICT (content): Merge conflict in test3.txt
#Automatic merge failed; fix conflicts and then commit the result.

<<<<<< HEAD
lokale wijziging 1
lokale wijziging 2

=======
remote wijziging 1
>>>>>> 11f1820c232f2450450b74579e2264ae41f4cdab
```

Om dit op te lossen, kun je de file bewerken, opslaan en afsluiten. In het voorbeeld van hierboven: alles verwijderen behalve de regels die je wilt behouden:

```
lokale wijziging 1
remote wijziging 1
```

Dit levert lokaal een wijziging op, die zul je moeten via add/commit/push moeten verwerken.

### Rebase

Je kunt een specifieke branch mergen in je huidige branch om de wijzigingen door te voeren, maar we hebben ook een "rebase" dat functioneel vergelijkbaar is. Belangrijk verschil: we krijgen geen nieuwe "merge commit" met de wijzigingen op onze feature branch en onze historie ("git log") is daarmee veel cleaner en makkelijker te begrijpen.

Gegeven ons voorbeeld: we hebben na commit "B" een feature branch gemaakt en hierop zijn we aan de slag gegaan. Inmiddels bevat de main branch een wijziging "C", die we ook graag in onze feature branch zouden willen integreren. Een "rebase" maakt dit mogelijk.

![](/images/rebase7.png)

Dus in plaats van een "merge commit" met de wijzigingen, krijgen we nu de wijziging "C" als commit in onze feature branch. We krijgen ook een nieuwe commit voor onze wijzigingen op de feature branch zelf "D accent", dus er is wel een impact.

```bash
git checkout feature
git rebase main
```

## Wijzigingen ongedaan maken

### Reset

Het kan natuurlijk gebeuren, dat we een lokale commit toch niet meer willen: we kunnen daarom een commit "resetten".

```bash
# een soft reset, HEAD min 1
# haalt commit lokaal weg, maar laat wijzigingen staan (worden "Staged changes")
git reset --soft HEAD~1

# een hard reset, HEAD min 1
# haalt commit + wijzigingen lokaal weg
git reset --hard HEAD~1
```

### Revert

Willen we het terugdraaien in de historie opnemen (als aparte commit), bijvoorbeeld omdat de wijzigingen al op de remote/centrale repo zijn toegepast, dan gebruiken we "git revert".

```bash
git revert 21e2988 #hash van de commit die je in een nieuwe commit wil terugdraaien
```

## Gouden regel

### Don’t rebase a public branch!

We hebben gezien, dat "git rebase" de historie herschrijft. Alleen wanneer je dit doet op een branch die je alleen zelf lokaal hebt (of waarvan je zeker weet dat niemand anders deze gebruikt) kun je dit veilig doen.

We hanteren daarom altijd de regel: rebase is prima, maar niet op een publieke branch!

Ter illustratie:

1. John en Jane clonen dezelfde repo met daarin een feature branch;
2. Er is een wijziging "C" die John graag in zijn feature branch wil hebben, dus kiest hij voor een "git rebase" van zijn feature branch;
3. Hij "pushed" zijn feature branch naar de centrale repo en maakt daarbij dus een nieuwe commit voor "D" ("D accent") met een compleet nieuwe hash;
4. Jane heeft commit "E" toegevoegd en wil haar feature branch ook central verwerken en doet een "git push";
5. Git kan haar nu niet meer helpen, want de hash voor commit "D" bestaat helemaal niet meer in de feature branch!

![](/images/rebase8.png)
