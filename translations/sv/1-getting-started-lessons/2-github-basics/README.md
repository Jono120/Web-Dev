<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "361249da70432ddfd4741c917d1a6f50",
  "translation_date": "2025-08-29T08:03:36+00:00",
  "source_file": "1-getting-started-lessons/2-github-basics/README.md",
  "language_code": "sv"
}
-->
# Introduktion till GitHub

Den här lektionen täcker grunderna i GitHub, en plattform för att hosta och hantera ändringar i din kod.

![Intro till GitHub](../../../../translated_images/webdev101-github.8846d7971abef6f947909b4f9d343e2a23778aa716ca6b9d71df7174ee5009ac.sv.png)
> Sketchnote av [Tomomi Imura](https://twitter.com/girlie_mac)

## Förberedande Quiz
[Förberedande quiz](https://ff-quizzes.netlify.app)

## Introduktion

I den här lektionen kommer vi att gå igenom:

- att spåra det arbete du gör på din dator
- att arbeta med projekt tillsammans med andra
- hur man bidrar till öppen källkod

### Förkunskaper

Innan du börjar, kontrollera om Git är installerat. Skriv i terminalen:  
`git --version`

Om Git inte är installerat, [ladda ner Git](https://git-scm.com/downloads). Ställ sedan in din lokala Git-profil i terminalen:
* `git config --global user.name "ditt-namn"`
* `git config --global user.email "din-epost"`

För att kontrollera om Git redan är konfigurerat kan du skriva:  
`git config --list`

Du behöver också ett GitHub-konto, en kodredigerare (som Visual Studio Code), och du behöver öppna din terminal (eller kommandotolken).

Navigera till [github.com](https://github.com/) och skapa ett konto om du inte redan har ett, eller logga in och fyll i din profil.

✅ GitHub är inte den enda kodförvaringen i världen; det finns andra, men GitHub är den mest kända.

### Förberedelser

Du behöver både en mapp med ett kodprojekt på din lokala dator (laptop eller PC) och ett offentligt repository på GitHub, som kommer att fungera som ett exempel på hur man bidrar till andras projekt.

---

## Kodhantering

Låt oss säga att du har en mapp lokalt med ett kodprojekt och du vill börja spåra dina framsteg med hjälp av git - versionshanteringssystemet. Vissa människor jämför att använda git med att skriva ett kärleksbrev till sitt framtida jag. Genom att läsa dina commit-meddelanden dagar, veckor eller månader senare kan du minnas varför du tog ett beslut, eller "rulla tillbaka" en ändring - det vill säga, om du skriver bra "commit-meddelanden".

### Uppgift: Skapa ett repository och commit:a kod  

> Se video  
> 
> [![Git och GitHub grunder video](https://img.youtube.com/vi/9R31OUPpxU4/0.jpg)](https://www.youtube.com/watch?v=9R31OUPpxU4)

1. **Skapa repository på GitHub**. På GitHub.com, i fliken repositories, eller från navigeringsfältet uppe till höger, hitta knappen **new repo**.

   1. Ge ditt repository (mapp) ett namn.
   1. Välj **create repository**.

1. **Navigera till din arbetsmapp**. I din terminal, byt till mappen (även kallad katalogen) du vill börja spåra. Skriv:

   ```bash
   cd [name of your folder]
   ```

1. **Initiera ett git-repository**. I ditt projekt, skriv:

   ```bash
   git init
   ```

1. **Kontrollera status**. För att kontrollera statusen för ditt repository, skriv:

   ```bash
   git status
   ```

   Utdata kan se ut ungefär så här:

   ```output
   Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   file.txt
        modified:   file2.txt
   ```

   Vanligtvis berättar kommandot `git status` saker som vilka filer som är redo att _sparas_ till repo:t eller har ändringar som du kanske vill bevara.

1. **Lägg till alla filer för spårning**  
   Detta kallas också att staga filer/lägga till filer i staging-området.

   ```bash
   git add .
   ```

   Argumentet `git add` plus `.` indikerar att alla dina filer och ändringar ska spåras.

1. **Lägg till utvalda filer för spårning**

   ```bash
   git add [file or folder name]
   ```

   Detta hjälper oss att lägga till endast utvalda filer i staging-området när vi inte vill commit:a alla filer på en gång.

1. **Avstaga alla filer**

   ```bash
   git reset
   ```

   Detta kommando hjälper oss att avstaga alla filer på en gång.

1. **Avstaga en specifik fil**

   ```bash
   git reset [file or folder name]
   ```

   Detta kommando hjälper oss att avstaga endast en specifik fil som vi inte vill inkludera i nästa commit.

1. **Spara ditt arbete**. Vid det här laget har du lagt till filerna i ett så kallat _staging-område_. En plats där Git spårar dina filer. För att göra ändringen permanent behöver du _commit:a_ filerna. För att göra det skapar du en _commit_ med kommandot `git commit`. En _commit_ representerar en sparpunkt i historiken för ditt repo. Skriv följande för att skapa en _commit_:

   ```bash
   git commit -m "first commit"
   ```

   Detta commit:ar alla dina filer och lägger till meddelandet "first commit". För framtida commit-meddelanden vill du vara mer beskrivande för att förmedla vilken typ av ändring du har gjort.

1. **Koppla ditt lokala Git-repo till GitHub**. Ett Git-repo är bra på din dator, men vid något tillfälle vill du ha en backup av dina filer någonstans och även bjuda in andra att arbeta med dig på ditt repo. En sådan bra plats är GitHub. Kom ihåg att vi redan har skapat ett repo på GitHub, så det enda vi behöver göra är att koppla vårt lokala Git-repo till GitHub. Kommandot `git remote add` gör just det. Skriv följande kommando:

   > Obs, innan du skriver kommandot, gå till din GitHub-repo-sida för att hitta repository-URL:en. Du kommer att använda den i kommandot nedan. Ersätt ```https://github.com/username/repository_name.git``` med din GitHub-URL.

   ```bash
   git remote add origin https://github.com/username/repository_name.git
   ```

   Detta skapar en _remote_, eller anslutning, med namnet "origin" som pekar på GitHub-repository:t du skapade tidigare.

1. **Skicka lokala filer till GitHub**. Hittills har du skapat en _anslutning_ mellan det lokala repo:t och GitHub-repo:t. Låt oss skicka dessa filer till GitHub med följande kommando `git push`, så här:  
   
   > Obs, ditt branch-namn kan vara annorlunda som standard från ```main```.

   ```bash
   git push -u origin main
   ```

   Detta skickar dina commits i din "main"-branch till GitHub.

2. **Lägg till fler ändringar**. Om du vill fortsätta göra ändringar och skicka dem till GitHub behöver du bara använda följande tre kommandon:

   ```bash
   git add .
   git commit -m "type your commit message here"
   git push
   ```

   > Tips, du kanske också vill använda en `.gitignore`-fil för att förhindra att filer du inte vill spåra dyker upp på GitHub - som den anteckningsfilen du lagrar i samma mapp men som inte har någon plats i ett offentligt repository. Du kan hitta mallar för `.gitignore`-filer på [.gitignore templates](https://github.com/github/gitignore).

#### Commit-meddelanden

Ett bra Git-commit ämnesrad kompletterar följande mening:  
Om det tillämpas, kommer denna commit att <din ämnesrad här>

För ämnet, använd imperativ, presens: "ändra" inte "ändrade" eller "ändringar".  
Precis som i ämnet, använd också imperativ, presens i kroppen (valfritt). Kroppen bör inkludera motivationen för ändringen och kontrastera detta med tidigare beteende. Du förklarar `varför`, inte `hur`.

✅ Ta några minuter och surfa runt på GitHub. Kan du hitta ett riktigt bra commit-meddelande? Kan du hitta ett riktigt minimalt? Vilken information tycker du är viktigast och mest användbar att förmedla i ett commit-meddelande?

### Uppgift: Samarbeta

Huvudsyftet med att lägga upp saker på GitHub var att göra det möjligt att samarbeta med andra utvecklare.

## Arbeta med projekt tillsammans med andra

> Se video  
>
> [![Git och GitHub grunder video](https://img.youtube.com/vi/bFCM-PC3cu8/0.jpg)](https://www.youtube.com/watch?v=bFCM-PC3cu8)

I ditt repository, navigera till `Insights > Community` för att se hur ditt projekt jämför med rekommenderade community-standarder.

   Här är några saker som kan förbättra ditt GitHub-repo:
   - **Beskrivning**. Har du lagt till en beskrivning för ditt projekt?
   - **README**. Har du lagt till en README? GitHub ger vägledning för att skriva en [README](https://docs.github.com/articles/about-readmes/?WT.mc_id=academic-77807-sagibbon).
   - **Riktlinjer för bidrag**. Har ditt projekt [riktlinjer för bidrag](https://docs.github.com/articles/setting-guidelines-for-repository-contributors/?WT.mc_id=academic-77807-sagibbon)?
   - **Uppförandekod**. En [uppförandekod](https://docs.github.com/articles/adding-a-code-of-conduct-to-your-project/).
   - **Licens**. Kanske viktigast av allt, en [licens](https://docs.github.com/articles/adding-a-license-to-a-repository/)?

Alla dessa resurser kommer att gynna onboarding av nya teammedlemmar. Och det är typiskt sådana saker nya bidragsgivare tittar på innan de ens tittar på din kod, för att ta reda på om ditt projekt är rätt plats för dem att spendera sin tid.

✅ README-filer, även om de tar tid att förbereda, förbises ofta av upptagna underhållare. Kan du hitta ett exempel på en särskilt beskrivande README? Obs: det finns några [verktyg för att skapa bra READMEs](https://www.makeareadme.com/) som du kanske vill prova.

### Uppgift: Slå ihop kod

Bidragsdokument hjälper människor att bidra till projektet. Det förklarar vilka typer av bidrag du letar efter och hur processen fungerar. Bidragsgivare måste gå igenom en serie steg för att kunna bidra till ditt repo på GitHub:

1. **Forka ditt repo**. Du kommer förmodligen vilja att folk ska _forka_ ditt projekt. Forking innebär att skapa en kopia av ditt repository på deras GitHub-profil.
1. **Klona**. Därefter klonar de projektet till sin lokala dator.
1. **Skapa en branch**. Du vill be dem att skapa en _branch_ för sitt arbete.
1. **Fokusera sin ändring på ett område**. Be bidragsgivare att koncentrera sina bidrag på en sak i taget - på så sätt är chansen att du kan _slå ihop_ deras arbete högre. Tänk dig att de skriver en buggfix, lägger till en ny funktion och uppdaterar flera tester - vad händer om du vill, eller bara kan implementera 2 av 3, eller 1 av 3 ändringar?

✅ Föreställ dig en situation där branches är särskilt kritiska för att skriva och leverera bra kod. Vilka användningsfall kan du tänka dig?

> Obs, var den förändring du vill se i världen och skapa branches för ditt eget arbete också. Alla commits du gör kommer att göras på den branch du för närvarande är "utcheckad" till. Använd `git status` för att se vilken branch det är.

Låt oss gå igenom en bidragsgivares arbetsflöde. Anta att bidragsgivaren redan har _forkat_ och _klonat_ repo:t så att de har ett Git-repo redo att arbeta med på sin lokala dator:

1. **Skapa en branch**. Använd kommandot `git branch` för att skapa en branch som kommer att innehålla de ändringar de avser att bidra med:

   ```bash
   git branch [branch-name]
   ```

1. **Byt till arbetsbranch**. Byt till den angivna branchen och uppdatera arbetskatalogen med `git switch`:

   ```bash
   git switch [branch-name]
   ```

1. **Utför arbete**. Vid det här laget vill du lägga till dina ändringar. Glöm inte att berätta för Git om det med följande kommandon:

   ```bash
   git add .
   git commit -m "my changes"
   ```

   Se till att du ger din commit ett bra namn, för din egen skull såväl som för underhållaren av repo:t du hjälper till med.

1. **Kombinera ditt arbete med `main`-branchen**. Vid något tillfälle är du klar med ditt arbete och vill kombinera det med `main`-branchen. `Main`-branchen kan ha ändrats under tiden, så se till att du först uppdaterar den till det senaste med följande kommandon:

   ```bash
   git switch main
   git pull
   ```

   Vid det här laget vill du se till att eventuella _konflikter_, situationer där Git inte enkelt kan _kombinera_ ändringarna, händer i din arbetsbranch. Kör därför följande kommandon:

   ```bash
   git switch [branch_name]
   git merge main
   ```

   Detta kommer att ta in alla ändringar från `main` till din branch och förhoppningsvis kan du bara fortsätta. Om inte, kommer VS Code att visa dig var Git är _förvirrad_ och du ändrar de berörda filerna för att ange vilket innehåll som är mest korrekt.

1. **Skicka ditt arbete till GitHub**. Att skicka ditt arbete till GitHub innebär två saker. Att pusha din branch till ditt repo och sedan öppna en PR, Pull Request.

   ```bash
   git push --set-upstream origin [branch-name]
   ```

   Kommandot ovan skapar branchen på ditt forkade repo.

1. **Öppna en PR**. Nästa steg är att öppna en PR. Du gör det genom att navigera till det forkade repo:t på GitHub. Du kommer att se en indikation på GitHub där det frågar om du vill skapa en ny PR, du klickar på det och tas till ett gränssnitt där du kan ändra commit-meddelandets titel, ge det en mer lämplig beskrivning. Nu kommer underhållaren av repo:t du forkade att se denna PR och _håller tummarna_ att de uppskattar och _slår ihop_ din PR. Du är nu en bidragsgivare, yay :)

1. **Städa upp**. Det anses vara god praxis att _städa upp_ efter att du framgångsrikt har slagit ihop en PR. Du vill städa upp både din lokala branch och branchen du pushade till GitHub. Först, låt oss ta bort den lokalt med följande kommando:

   ```bash
   git branch -d [branch-name]
   ```

   Se till att du går till GitHub-sidan för det forkade repo:t och tar bort den remote-branch du just pushade till det.
`Pull request` kan låta som ett konstigt uttryck eftersom du egentligen vill "pusha" dina ändringar till projektet. Men projektets ansvariga (ägare) eller kärnteamet behöver granska dina ändringar innan de slås ihop med projektets "main"-gren, så det handlar egentligen om att begära ett beslut om ändringen från en ansvarig.  

En pull request är platsen där du kan jämföra och diskutera skillnader som introducerats i en gren, med hjälp av recensioner, kommentarer, integrerade tester och mer. En bra pull request följer ungefär samma regler som ett commit-meddelande. Du kan lägga till en referens till ett ärende i ärendespåraren, till exempel när ditt arbete löser ett problem. Detta görs med ett `#` följt av ärendenumret. Till exempel `#97`.

🤞Håller tummarna för att alla kontroller går igenom och att projektägaren/ägarna slår ihop dina ändringar med projektet🤞

Uppdatera din nuvarande lokala arbetsgren med alla nya commits från motsvarande fjärrgren på GitHub:

`git pull`

## Hur man bidrar till öppen källkod

Först, hitta ett repository (eller **repo**) på GitHub som intresserar dig och som du vill bidra med en ändring till. Du kommer vilja kopiera dess innehåll till din dator.

✅ Ett bra sätt att hitta 'nybörjarvänliga' repos är att [söka efter taggen 'good-first-issue'](https://github.blog/2020-01-22-browse-good-first-issues-to-start-contributing-to-open-source/).

![Kopiera ett repo lokalt](../../../../translated_images/clone_repo.5085c48d666ead57664f050d806e325d7f883be6838c821e08bc823ab7c66665.sv.png)

Det finns flera sätt att kopiera kod. Ett sätt är att "klona" innehållet i repot, antingen via HTTPS, SSH eller med hjälp av GitHub CLI (Command Line Interface). 

Öppna din terminal och klona repot så här:
`git clone https://github.com/ProjectURL`

För att arbeta med projektet, byt till rätt mapp:
`cd ProjectURL`

Du kan också öppna hela projektet med [Codespaces](https://github.com/features/codespaces), GitHubs inbyggda kodredigerare/molnutvecklingsmiljö, eller [GitHub Desktop](https://desktop.github.com/).

Slutligen kan du ladda ner koden i en zip-fil. 

### Några fler intressanta saker om GitHub

Du kan stjärnmärka, bevaka och/eller "forka" vilket offentligt repository som helst på GitHub. Du hittar dina stjärnmärkta repos i rullgardinsmenyn uppe till höger. Det är som att bokmärka, fast för kod. 

Projekt har en ärendespårare, oftast på GitHub under fliken "Issues" om inget annat anges, där folk diskuterar problem relaterade till projektet. Fliken Pull Requests är där folk diskuterar och granskar ändringar som pågår.

Projekt kan också ha diskussioner i forum, e-postlistor eller chattkanaler som Slack, Discord eller IRC.

✅ Utforska ditt nya GitHub-repo och prova några saker, som att redigera inställningar, lägga till information i ditt repo och skapa ett projekt (som en Kanban-tavla). Det finns mycket att göra!

---

## 🚀 Utmaning 

Jobba tillsammans med en vän på varandras kod. Skapa ett projekt tillsammans, forka kod, skapa grenar och slå ihop ändringar.

## Efterföreläsningsquiz
[Efterföreläsningsquiz](https://ff-quizzes.netlify.app/web/en/)

## Granskning & Självstudier

Läs mer om [att bidra till öppen källkod](https://opensource.guide/how-to-contribute/#how-to-submit-a-contribution). 

[Git-fusklapp](https://training.github.com/downloads/github-git-cheat-sheet/).

Öva, öva, öva. GitHub har fantastiska inlärningsvägar tillgängliga via [skills.github.com](https://skills.github.com):

- [Första veckan på GitHub](https://skills.github.com/#first-week-on-github)

Du hittar också mer avancerade kurser. 

## Uppgift 

Slutför [kursen Första veckan på GitHub](https://skills.github.com/#first-week-on-github)

---

**Ansvarsfriskrivning**:  
Detta dokument har översatts med hjälp av AI-översättningstjänsten [Co-op Translator](https://github.com/Azure/co-op-translator). Även om vi strävar efter noggrannhet, vänligen notera att automatiska översättningar kan innehålla fel eller felaktigheter. Det ursprungliga dokumentet på dess originalspråk bör betraktas som den auktoritativa källan. För kritisk information rekommenderas professionell mänsklig översättning. Vi ansvarar inte för eventuella missförstånd eller feltolkningar som uppstår vid användning av denna översättning.