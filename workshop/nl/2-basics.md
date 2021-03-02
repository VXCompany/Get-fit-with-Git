# Basics

[Terug naar het Workshop Script](handson.md)

### The Basics: een bestand toevoegen

Navigeer naar je de clone van je eerste repository: "gfwg-demo-1"

Vraag de status van deze repository op met:

```bash
git status
```

Als het goed is krijg je nu de melding, dat de branch up to date is. Logisch, we hebben hem net gecloned.

We gaan een eigen file toevoegen, gebruik hier voor een text editor naar keuze. Maak een nieuw bestand aan in de root van deze repo met als naam "index.html". Voeg onderstaande content toe:

```html
<html>
  <body>
    Test bestand
  </body>
  <html></html>
</html>
```

Herhaal nu het commando om de status van de repository op te vragen. Als het goed is, krijg je nu de melding dat er "Untracked files" zijn.

> Wat zijn "Untracked files"?
> Untracked files zijn bestanden in onze werk directory die zijn aangepast, maar nog niet door Git worden bijgehouden.
> Deze Untracked files worden in een volgende commit dus niet meegenomen.

We gaan deze file toevoegen aan de zogeheten "Staging Area", waarbij we Git vertellen dat dit bestand wel moet worden meegenomen bij de volgende commit.

```bash
git add index.html
```

Als alternatief kunnen we ook alle bestanden (die niet in de .gitignore file staan) mee laten nemen:

```bash
git add -A # of git add .
```

Vraag nogmaals de status op en zie het verschil. Git houdt deze file nu in de gaten, maar het is nog niet opgenomen in onze lokale repository. Omdat te doen, gebruiken we het volgende commando:

```bash
git commit -m "Dit is de eerste file die we toevoegen"
```

Je krijgt nu de terugkoppeling, waarbij we even in detail kijken naar de output:

"[main {hashcode}] Dit is de eerste file die we toevoegen"

- main is de branch waarop we deze file toevoegen
- hashcode is de SHA-1 hash die onze commit uniek identificeert
- gevolgd door onze eigen commit message

Vraag nogmaals de status op en zie het verschil.

### De lokale wijzigingen doorzetten naar de remote repository

Onze lokale Git repo is bijgewerkt (met dat laatste commit commando). Als we nu ook de remote repository willen bijwerken, moeten we onze wijzigingen "pushen"

```bash
git push
```

### Wijzigingen binnenhalen

Wanneer we met verschillende mensen aan hetzelfde project werken, kan het natuurlijk gebeuren, dat iemand anders wijzigingen heeft doorgezet die wij lokaal nog niet hebben. Om die ook binnen te halen maken we gebruik van "Git pull". Maar hier is gelijk iets bijzonders aan de hand:

"Git pull" is een shortcut voor "Git fetch" + "Git merge FETCH_HEAD". Fetch haalt de laatste stand van zaken binnen, maar houdt die nog even apart van onze lokale branch. Git doet dat door gebruik te maken van een nieuwe pointer: FETCH_HEAD. Wanneer er wijzigingen (nieuwe commits) zijn ten opzichte van de huidige branch, dan volgt er:

- een fast-forward: we hebben lokaal geen nieuwe commits => dan worden de commits van de remote branch zonder problemen toegevoegd aan onze branch (en dat zonder een nieuwe commit te maken);
- een merge, we hebben lokaal wel nieuwe commits => dan worden de commits van de remote branch aan onze branch toegevoegd in een nieuwe commit. Conflicten worden middels een merge conflict opgelost;
- een rebase, dit werkt de lokale branch bij met de centrale commits en past dan de lokale wijzigingen weer toe (er boven op).

> DEMO Mocht dit niet helemaal duidelijk zijn...
> Geen nood, we zullen in de volgende stap naar het verschil tussen deze 3 varianten kijken.

```bash
git pull
```

Vanaf deze laatste versie van de Git CLI is er een kans dat je hier nu de volgende melding te zien krijgt:

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

Deze melding geeft dus aan, dat de standaard strategie een "merge" is. Dit doet Git inderdaad standaard als er lokaal ook wijzigingen zijn. Zijn die er echter niet, dan zal Git eerst een "fast-forward" proberen (Git is "lui") ! Door je standaard strategie op "fast-forward only" te zetten, kun je er voor zorgen dat je alleen lokaal bijwerkt als dat zonder bijwerkingen kan.

[Naar stap 3: Fast-forward](3-fastforward.md)

[Terug naar het Workshop Script](handson.md)
