# Fast-forward, merge, rebase

[Terug naar het Workshop Script](handson.md)

### Merge

We zijn nu dus op het punt, dat we zowel lokaal als centraal/ remote een wijziging hebben en daarom niet vooruit kunnen spoelen. Git heeft hier 2 oplossingen voor: merge en rebase. We beginnen met de eerste:

Bij een "merge" worden beide wijzigingen verwerkt en wordt er een nieuwe commit gedaan. We hebben eerder gezien, dat als we nu een "git pull" uitvoeren zonder iets mee te geven de standaard strategie dus een "merge" is.

```bash
git pull
```

Omdat er nu wijzigingen worden samengevoegd in een nieuwe commit, zal de standaard geconfigureerde text editor opspringen en om een "commit message" vragen. Geven we die, dan is er verder niets meer nodig en wordt de nieuwe commit gemaakt.

```bash
git log --pretty=oneline
```

![](/images/commit7.png)

Deze wijziging is nu alleen nog lokaal, dus met een "git push" zetten we dit door naar centraal.

```bash
git push
```

Controleer nu zelf de commit history op GitHub en zie ook daar de nieuwe commit verschijnen.

### Merge conflict

Uiteraard is het voorgaande scenario eenvoudig, dat komt vooral omdat we de wijzigingen in aparte bestanden hebben zitten. Wat gebeurt er als we wijzigingen hebben in dezelfde file?

Pas lokaal het bestand "test3.txt" aan door bijvoorbeeld een regel tekst toe te voegen. Sla dit op, voeg het aan de Staging Area toe en commit het met een commit message.

```bash
git add test3.txt
git commit -m "Lokale aanpassing"
```

Ga nu naar GitHub en pas daar ook de file aan. Je doet dit door eerst de file "test3.txt" te selecteren en daarna te kiezen voor "Edit this file":

![](/images/editfile1.png)

Voeg een andere tekst of regel toe en commit ook deze wijziging.

Voer nu een git pull uit en zie dat git een merge conflict detecteert:

```bash
git pull

#Auto-merging test3.txt
#CONFLICT (content): Merge conflict in test3.txt
#Automatic merge failed; fix conflicts and then commit the result.
```

Als je nu de file "test3.txt" in een editor opent, dan zie je dat git het conflict zichtbaar heeft gemaakt:

```
<<<<<< HEAD
test
test

=======
test bla
>>>>>> 11f1820c232f2450450b74579e2264ae41f4cdab
```

> Het kan zijn, dat je editor al gelijk met een git integratie komt en je helpt de juiste keuze te maken.

De "HEAD" die bovenin staat, verwijst naar de pointer lokaal. De commit hash die onderin staat, verwijst naar 1 specifieke commit in de history op GitHub.

Het commentaar dat git er bij heeft gezet is gewoon tekst. Om een merge conflict op te lossen, zorg je er gewoon voor dat je alleen de tekst overhoudt die je wilt behouden. Dit betekent dus ook, dat je het git commentaar moet verwijderen.

```
test
test
test bla
```

Dit mag je nu opslaan, in de Staging Area zetten, committen (met als commit message "Conflict opgelost") en pushen naar de centrale/ remote repo.

```bash
git add test3.txt
git commit -m "Conflict opgelost"
git push
```

Van de 3 typen (fast-forward, merge en rebase) is er nog 1 over:

[Naar stap 5: Rebase](5-rebase.md)

[Terug naar het Workshop Script](handson.md)
