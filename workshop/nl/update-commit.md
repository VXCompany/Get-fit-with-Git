# Opdracht: Update commit message

[Terug naar het Workshop Script](handson.md)

### Update commit message

Soms is het een typo in de commit message, soms is het de referentie naar het workitem wat vergeten is. In de praktijk komt het nog al eens voor, dat je een commit message wilt aanpassen.
Een commit message aanpassen als de commit nog alleen lokaal staat (en dus nog niet gepushed is) is eenvoudig:

Ga naar de 2e repo: gfwg-demo-2

1. Pas hier de index.html aan: verander de HTML title in "Get fit with Git"
2. Voeg index.html toe aan de Staging Area, Commit met de message "Bug gefixet"
3. Zie de typo en besluit de commit message aan te passen

```bash
git commit --amend -m "Bug gefixed"
```

Controleer of de commit message is bijgewerkt met "git log".

Ook als de commit al wel gepushed is kun je deze bijwerken. Je gebruikt hier hetzelfde commando voor, alleen zul je daarna een "force push" moeten doen om je wijzigingen in de centrale/ remote repo bij te werken. Dit levert een nieuwe commit hash op en daarom moet je er zeker van zijn, dat andere projectleden deze wijzigingen nog niet hebben binnengehaald! Dit is vergelijkbaar met de gouden regel voor "rebase".

Daarnaast kun je commit messages ook bijwerken met de Interactive Rebase. Gebruik hier het "reword" keyword voor. Zie ook [Interactive Rebase](rebase-i.md).

[Terug naar het Workshop Script](handson.md)
