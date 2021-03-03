# Fast-forward, merge, rebase

[Terug naar het Workshop Script](handson.md)

In de vorige stap haalden we (mogelijke) wijzigingen van de centrale/ remote repo lokaal. Het doel was daarbij natuurlijk onze lokale repo bij te werken en eventuele lokale aanpassingen te behouden. We zullen in een latere stap kijken naar branches en Pull Requests, waar dit een belangrijk onderwerp is, maar eerst even de 3 verschillende strategieen bekijken.

### 1. De Fast-forward

De eenvoudigste is de Fast-forward en het doet precies wat het zegt: snel vooruit spoelen. Dit is alleen van toepassing als:

- Er zijn wijzigingen in de centrale / remote repository;
- De lokale repo heeft nog geen wijzigingen (je kunt wel lokaal bestanden hebben gewijzigd, maar je hebt ze nog niet ge-commit).

Ga naar je GitHub account en kies de 1e repository die we aangemaakt hebben ("gfwg-demo-1"). Als je nu rechtsboven op "Add file" & "Create a new file" klikt, kun je via de GUI een file aanmaken. Hiermee simuleren we een andere gebruiker van de repository, die een nieuwe file heeft toegevoegd.

![](/images/ff1.png)

Noem de file "test1.txt" en stop er wat inhoud in (de inhoud zelf doet er niet zoveel toe, als er maar wat in zit). Kies onderin voor "Commit new file".

![](/images/commit1.png)

We gaan nu deze wijziging naar lokaal halen, maar eerst bekijken we even naar de "before" situatie. Klik in GitHub op de commits om naar de Commit History te gaan:

![](/images/commit2.png)

Dit geeft een overzicht (log) van de commits in deze repo. Let hierbij vooral op de zogeheten "commit hash", die gaan we straks vergelijken met wat we lokaal zien.

![](/images/commit3.png)

Wanneer je nu lokaal ditzelfde overzicht opvraagt, zie je aan de commit hashes de verschillen:

```bash
git log
```

![](/images/commit4.png)

We hebben dus lokaal 1 commit minder, maar we hebben lokaal ook geen eigen commits extra. Dus in dit geval zal Git bij een "git pull" een fast-forward proberen.

Probeer dit nu zelf met:

```
git pull
git log
```

De nieuwe git history toont de binnengekomen commit, deze is er zonder bijwerkingen lokaal aan toegevoegd!

![](/images/commit5.png)

### 2. Fast-forward only

Fast-forward is dus een eenvoudige manier om zonder bijwerkingen centrale wijzigingen lokaal te integreren. Sterker nog, het is misschien wel aan te raden om de standaard strategie "--ff-only" te maken... eens even zien wat daar het effect van zou zijn:

Ga hiervoor weer terug naar GitHub en maak een tweede file aan (naam: test2.txt). Commit deze file ook, net zoals je dat bij die eerste file hebt gedaan.

Maak nu lokaal in je repo ook een nieuwe file aan (naam: test3.txt). Voeg deze daarna toe aan je Staging Area om deze vervolgens in een commit mee te nemen:

```
git add test3.txt
git commit -m "File nummer 3 toegevoegd"
```

Bekijk vervolgens de "git log" lokaal en de commit history op GitHub. Wat valt je op? Als het goed is zie je dat de eerste 3 commits nog overeenkomen, maar dat ze beiden een andere laatste commit hash hebben:

![](/images/commit6.png)

(dit is overigens de output van "git log --pretty=oneline")

Als we nu de wijzigingen centraal zouden willen binnenhalen, zonder bijwerkingen, dan zouden we het volgende commando dus uit moeten voeren:

```
git pull --ff-only
```

Dit haalt de laatste status van de centrale / remote repo op en breekt dan af met de melding: "fatal: Not possible to fast-forward, aborting.". Dit klopt natuurlijk, want vooruit spoelen is niet mogelijk omdat we lokaal ook nog een wijziging hebben staan!

In de volgende stap, zullen we deze commit gaan samenvoegen met behulp van "git merge".

[Naar stap 4: Merge](4-merge.md)

[Terug naar het Workshop Script](handson.md)
