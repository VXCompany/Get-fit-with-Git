# Fast-forward, merge, rebase

[Terug naar het Workshop Script](handson.md)

### 1. Rebase

Van de eerder genoemde typen is "rebase" misschien het lastigst. Laten we eerst eens kijken hoe hij werkt....

Volg de stappen:

1. Voeg lokaal een bestand toe met de naam test4.txt (inhoud maakt niet uit);
2. Voeg dit bestand aan de Staging Area toe en doe een "commit" (hint: git add + git commit);

3. Voeg ook op GitHub een bestand toe met de naam test5.txt (inhoud maakt niet uit) en commit deze file via de knop "Commit this file".

We hebben nu een vergelijkbare situatie als eerder: lokaal een wijziging, centraal een (andere) wijziging. Fast-forward is dus geen optie, merge en rebase blijven over.

In dit specifieke geval zou een merge prima kunnen, maar dat levert dus een nieuwe commit op. We kunnen ook kiezen voor een "rebase", vrij vertaald: we kunnen onze lokale repo herbaseren op de originele centrale/ remote repo. In dat geval worden onze lokale wijzigingen er bovenop "geplakt".

Laten we, voordat we rebase-en, eerst lokaal kijken:

```bash
git log --pretty=oneline
```

![](/images/rebase1.png)

En de commit history op GitHub:

![](/images/rebase2.png)

We zien dus inderdaad uiteenlopende repo's (beide repo's hebben andere wijzigingen).

Wanneer we nu kiezen voor een "git pull" met een rebase als strategie, zal eerst de commit van de centrale repo worden toegepast en daarna onze eigen lokale commit.

```bash
git pull --rebase

#Successfully rebased and updated refs/heads/main.
```

Gaan we weer lokaal kijken:

```bash
git log --pretty=oneline
```

Zien we inderdaad de commit van de centrale/ remote repo eerst toegepast worden, daarna onze eigen commit (maar wel met een nieuwe commit hash):

![](/images/rebase3.png)

Push als afsluitende stap deze lokale state naar de remote repo:

```bash
git push
```

Rebase herschrijft de git history en doet dat dus eerst lokaal (er ontstaat daarbij een nieuwe commit). Nu je weet hoe het werkt, is het belangrijk te beseffen wanneer je het NIET moet gebruiken. De regel hierbij is: ben ik de enige die deze branch gebruikt? Als dat zo is, dan mag je rebasen. Als anderen ook de branch gebruiken, dan mag je niet rebasen!

> Gouden regel: “No one shall rebase a shared branch” !

[Naar stap 6: Reset](6-reset.md)

[Terug naar het Workshop Script](handson.md)
