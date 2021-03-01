# Opdracht: Interactive Rebase

[Terug naar het Workshop Script](handson.md)

Je kunt rebase ook gebruiken om een serie aan lokale commits samen te voegen tot 1 commit. Je kent het wel:

1. Je past wat aan. Mooi, dat is klaar.
2. Commit. Message: "Bug gefixed".
3. Oh wacht.... ik ga het toch even anders doen.
4. Commit. Message: "Refactor bug fix".

Interactive Rebase to the rescue!

### Interactive Rebase

Ga naar de 2e repo: gfwg-demo-2

1. Pas hier de index.html aan: verander de HTML title in "Get fit with Git"
2. Voeg index.html toe aan de Staging Area, Commit met de message "Bug gefixed"
3. Pas de index.html wederom aan: verander de HTML title in "Get fit with Git!!!"
4. Voeg index.html toe aan de Staging Area, Commit met de message "Refactor bug fix"

Wanneer je nu de git log bekijkt, zie je de 2 losse commits staan. Deze gaan we samenvoegen in 1 enkele commit.

![](/images/rebase4.png)

```bash
git rebase -i HEAD~2
```

Dit opent de standaard editor weer:

![](/images/rebase5.png)

Pas nu de onderste commit aan (de laatste) en verander de "pick" naar "fixup", oftewel: voeg de commmit samen en laat deze commit message achterwege.

```
pick 43a9db5 Bug gefixed
fixup 5093fcd Refactor bug fix
```

Wanneer je nu opslaat en het git log bekijkt, is de refactor regel weg.

![](/images/rebase6.png)

Open de index.html file en controleer of de HTML titel nog wel de 2e aanpassing heeft ("Get fit with Git!!!").

[Terug naar het Workshop Script](handson.md)
