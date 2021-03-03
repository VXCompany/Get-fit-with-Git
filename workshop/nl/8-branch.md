# Branching

[Terug naar het Workshop Script](handson.md)

### 1. Branch

Samenwerken staat bij Git natuurlijk centraal. Waarschijnlijk zijn we allemaal wel bekend met "branches". Deze term komt niet van Git zelf, maar werd al veel langer gebruikt voor het separaat bij elkaar houden van wijzigingen. Bij Git is er wel een belangrijk verschil: branches zijn geen containers met files of commits, maar pointers naar commits. Dus op het moment, dat je een nieuwe branch maakt wordt er een pointer gemaakt naar de huidige commit met de naam van de branch.

We maken een nieuwe branch aan:

```bash
git branch feature/experiment1
```

we hebben nu alleen nog maar de pointer gemaakt. Als we de branch lokaal willen gebruiken:

```bash
git checkout feature/experiment1

#Switched to branch 'feature/experiment1'
```

Maak nu lokaal in je repo ook een nieuwe file aan (naam: test8.txt). Voeg deze daarna toe aan je Staging Area om deze vervolgens in een commit mee te nemen:

```
git add test8.txt
git commit -m "File nummer 8 toegevoegd"
```

Controleer de status:

```bash
git status

#On branch feature/experiment1
#nothing to commit, working tree clean
```

en ook het git log laat zien, dat we met onze HEAD wijzen naar de feature branch:

![](/images/branch1.png)

Met een "git push" willen we deze lokale wijzigingen nu ook doorzetten naar GitHub. Wanneer je dit zo probeert te doen, zul je merken dat dit niet gaat. Reden: deze branch bestaat alleen lokaal en we zullen Git moeten vertellen wat we met de "upstream" willen doen:

```bash
git push

#fatal: The current branch feature/experiment1 has no upstream branch.
#To push the current branch and set the remote as upstream, use
#
#    git push --set-upstream origin feature/experiment1

git push --set-upstream origin feature/experiment1
```

Omdat we gebruik maken van GitHub, stelt deze voor een Pull Request aan te maken worden voor deze branch. Wanneer je nu navigeert naar je GitHub repo, zie je daar bij "Pull requests" een alart voor onze nieuwe branch staan. Klik op "Compare & pull request" om deze aan te maken en maak deze direct aan.

Als alles goed is gegaan, kun je deze pull request nu zelf accepteren (het is tenslotte onze repo):

![](/images/pr1.png)

Als je nu lokaal wisselt naar de "main" branch zul je zien dat daar de file (test8.txt) nog ontbreekt.

```bash
git checkout main
```

Doe je nu vervolgens een nieuwe pull, dan zal git kunnen fast-forwarden (want er zijn lokaal geen andere commits dan remote).

```bash
git pull --ff-only

#Fast-forward
# test8.txt | 2 ++
# 1 file changed, 2 insertions(+)
# create mode 100644 test8.txt
```

[Naar stap 9: Finished](9-finished.md)

[Terug naar het Workshop Script](handson.md)
