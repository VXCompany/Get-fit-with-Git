# Undo: reset en revert

[Terug naar het Workshop Script](handson.md)

Het kan natuurlijk gebeuren, dat we een lokale commit toch niet meer willen. Omdat er 2 manieren zijn om een commit te "resetten" is het belangrijk eerst te bepalen of we de wijzigingen lokaal willen behouden of in zijn geheel verwijderen.

### Soft reset

Een soft reset haalt de commit weg, maar laat de wijzigingen (edits, nieuwe bestanden, etc.) wel staan. Dit worden dan "Staged changes".

We voegen nu als eerste weer een nieuw bestand toe, maar nu met de naam "test6.txt". Daarna het gebruikelijke:

```bash
git add test6.txt
git commit -m "Bestand 6 toegevoegd"
```

We voegen nu direct weer een nieuw bestand toe, naam "test7.txt".

```bash
git add test7.txt
git commit -m "Bestand 7 toegevoegd"
```

Als we nu naar de log kijken zien we 2 losse commits:

```bash
git log --pretty=oneline

#1c723e49a55a61ec69e99e9e021bb1f39bf116fb (HEAD -> main) Bestand nummero 7
#5036ee0917ff380355344b2ab781d79c05285e10 Bestand 6 toegevoegd
#89065a017afc6945a725f5f4a81ae79f7221c4b0 (origin/main, origin/HEAD) Test 4 toegevoegd
#35bd34ac8124b33d7462445044ab48e6a4ec5d1c Create test5.txt
#7ad1577b6ebf3feafca8d5c6e51c681506d9e7d5 Conflict opgelost
#11f1820c232f2450450b74579e2264ae41f4cdab Update test3.txt
#ccafb2af625aca0fd8d83fdae74b186ae6eb162b Lokale aanpassing
#aed3ac367d3517400185a7aa555d6111a23c9b8b Merge branch 'main'
#a3bcc7d79bcd29cd7dc555c5b1cb886420ce9a51 File nummer 3 toegevoegd
#21e2988b809d12bfc200ed3ec9b9989ab2700b1b Create test2.txt
#b287995cc855e200e9e7383b0e0dc2000cb5921 Create test1.txt
#93b5f503450c5a6189d64a3604f4b5b45bf72355 Dit is de eerste file die we toevoegen
#abb262114af5fdcc62f8f473c35ab0217fb948f7 Initial commit
```

We zullen nu de laatste commit gaan terugdraaien, maar het bestand laten staan:

```bash
# een soft reset, HEAD min 1
git reset --soft HEAD~1
```

Als je nu de status opvraagt, zie je dat het laatste bestand uit de commit is gehaald en in de Staging Area is gezet:

```bash
git status

#On branch main
#Your branch is ahead of 'origin/main' by 1 commit.
#  (use "git push" to publish your local commits)

#Changes to be committed:
#  (use "git restore --staged <file>..." to unstage)
#        new file:   test7.txt
```

Ook het git log toont in de history, dat HEAD nu 1 stap is teruggezet.

We voegen nu deze laatste file weer toe aan onze lokale commit:

```bash
git commit -m "Bestand 7 toegevoegd"
```

### Hard reset

Wanneer we besluiten om dit laatste bestand niet alleen uit de commit te halen, maar eigenlijk compleet te verwijderen (ongedaan te maken), kiezen we voor een harde reset. Voor we dit doen, controleer nog even de git log en zie de laatste commit weer staan. We gaan deze nu weer terugdraaien, inclusief het verwijderen van het bestand:

```bash
# een hard reset, HEAD min 1
git reset --hard HEAD~1

#HEAD is now at 5036ee0 Bestand 6 toegevoegd
```

En als we de inhoud van de directory controleren.... zien we dat de file ook verwijderd is.

Doe een "git push" om de wijzigingen te verwerken in de centrale/ remote repository.

[Naar stap 7: Revert](7-revert.md)

[Terug naar het Workshop Script](handson.md)
