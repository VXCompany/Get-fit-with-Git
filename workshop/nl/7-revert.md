# Undo: reset en revert

[Terug naar het Workshop Script](handson.md)

### Revert

Wanneer we een commit met "git reset" terugdraaien, maken we de commit in zijn geheel ongedaan. Deze verdwijnt dus ook uit de git history. We kunnen een commit ook terugdraaien, maar de git history intact laten. Hiervoor gebruiken we de "git revert".

Vraag nogmaals het git log op en zoek daarbij naar de hash voor het test2.txt bestand.

```bash
git log --pretty=oneline

#...
#21e2988b809d12bfc200ed3ec9b9989ab2700b1b Create test2.txt
#0b287995cc855e200e9e7383b0e0dc2000cb5921 Create test1.txt
#93b5f503450c5a6189d64a3604f4b5b45bf72355 Dit is de eerste file die we toevoegen
#abb262114af5fdcc62f8f473c35ab0217fb948f7 Initial commit
#...
#...
```

In mijn geval begint dat met "21e2988". Ik wil graag deze commit (met daarin het bestand test3.txt) terugdraaien, maar wel zichtbaar laten in de git history. Andere projectleden kunnen dus ook nog terugkijken wat er in die file stond.

```bash
git revert 21e2988
```

Omdat er nu wijzigingen worden doorgevoerd in een nieuwe commit, zal de standaard geconfigureerde text editor opspringen en om een "commit message" vragen. Geven we die, dan is er verder niets meer nodig en wordt de nieuwe commit gemaakt.

En als we de inhoud van de directory controleren.... zien we dat de file ook verwijderd is.

Doe een "git push" om de wijzigingen te verwerken in de centrale/ remote repository.

[Naar stap 8: Branch](8-branch.md)

[Terug naar het Workshop Script](handson.md)
