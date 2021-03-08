# Setup

[Terug naar het Workshop Script](handson.md)

### 1. Maak een eigen Git repository

Login op GitHub met je eigen account (bestaand account, zie eventueel de [voorbereiding](voorbereiding.md)). Wanneer je bent ingelogd, maak je een nieuwe repository aan door bijvoorbeeld op het "+"-teken rechtsboven te klikken.

![new repo image](/images/newrepo1.png)

- Gebruik de naam gfwg-demo-1;
- Kies zelf een omschrijving en maak het een Public repo;
- Kies voor "Add a README file".

### 2. Clone deze Git repository

We gaan van deze repository nu lokaal een kopie maken, zodat we er straks mee aan de slag kunnen.

![](/images/clone2.png)

We beginnen met het opslaan van de "clone" URL op ons clipboard. We klikken hiervoor op "Code" en dan op het clipboard icon achter de HTTP URL:

![clone URL image](/images/cloneurl1.png)

Maak vervolgens lokaal via een shell een werkdirectory aan voor de training, bijvoorbeeld: ~/training/get-fit en navigeer naar deze directory. Daarna kun je de clone maken met:

```bash
git clone {plak de URL van het clipboard}
```

Controleer bijvoorbeeld met "ls" of "dir" de inhoud van je clone (je zult hier in ieder geval een README.mg bestand zien staan):

![ls clone image](/images/ls1.png)

### 3. Maak een 2e eigen Git repository

Maak nu via de GitHub UI een 2e public repository aan (met de naam "gfwg-demo-2"), maar kies nu NIET voor het initialiseren van de repo met een README bestand.

Je komt nu in een ander scherm terecht en we kunnen de repository nog niet clonen.

### 4. Koppel een lokale repo aan deze Git repository

We gaan lokaal nu een repository maken en koppelen aan de zojuist aangemaakte Git repo.

![](/images/remote1.png)

Maak lokaal via een shell in de werkdirectory een nieuwe folder aan met de naam "gfwg-demo-2" (let op, dat je niet nog in de clone directory staat van de 1e repository). Navigeer naar die directory en vul deze met de bestanden uit deze [demo file](/demo/demo.zip).

Tip: als je in de juiste directory staat, kun je deze oneliner proberen:

```bash
# Voor MacOS, Linux en Windows Subsystem for Linux
curl -L https://github.com/VXCompany/Get-fit-with-Git/raw/main/demo/demo.zip | jar -xv

# Voor PowerShell
Invoke-WebRequest https://github.com/VXCompany/Get-fit-with-Git/raw/main/demo/demo.zip -OutFile demo.zip
Expand-Archive demo.zip .
```

Als het goed is heb je nu een directory met een aantal demo bestanden (index.html, css en wat afbeeldingen). Nu zijn we zover deze bestanden in een lokale repository te zetten en dan te koppelen aan de 2e Git repo op GitHub:

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin {plak de URL van de 2e repo}
git push -u origin main
```

Wanneer je nu op GitHub deze 2e repo bekijkt, zul je daar de demo bestanden terug zien.

### 5. Fork en clone een bestaande repository

![](/images/fork1.png)

Soms wil je aanpassingen doen of een bug fixen op een project van iemand anders. In dat geval maak je van die repository van iemand anders eerst een zogeheten "Fork". Deze Fork is daarmee jouw kopie geworden van die repository en we zullen in een latere stap zien hoe je wijzigingen kunt voorstellen in de vorm van een "Pull Request".

Navigeer naar de repository van deze workshop, daar zullen we een eigen Fork van gaan maken: https://github.com/VXCompany/Get-fit-with-Git

Rechtsboven zie je daar de optie Fork:

![fork image](/images/fork2.png)

Klik je daar op, dan regelt de GitHub UI de kopie naar je eigen repository. Heb je meer eigen accounts, let dan even op, dat je de juiste kiest.

Maak na de Fork weer lokaal een Clone, dat zijn vergelijkbare stappen zoals je die ook bij de 1e repo hebt gedaan.

Als het goed is heb je nu in je werkdirectory 3 Clones van repositories:

![workdir image](/images/ls2.png)

[Naar stap 2: Basics](2-basics.md)

[Terug naar het Workshop Script](handson.md)
