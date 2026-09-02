# Huskalkylen

En hushållsbudget för husköp i Sverige. Vad kostar det egentligen att bo i hus,
hur mycket blir kvar varje månad, och håller kalkylen om räntan går upp?

`index.html` är en enda självständig fil: ingen build, inga beroenden, ingen
server. Öppna den i en webbläsare, eller lägg upp den var som helst som kan
servera en statisk fil. Alla siffror sparas i webbläsarens `localStorage` — inget
skickas någonstans.

Den ligger uppe på **<https://abbee1.github.io/huskalkylen/>**, och fungerar
lika bra lokalt:

```
git clone git@github.com:abbee1/huskalkylen.git
cd huskalkylen
open index.html
```

## Vad den räknar på

**Lånet**

- Kontantinsats och belåningsgrad utifrån pris och insats
- Amorteringskrav: 2 %/år över 70 % belåningsgrad, 1 %/år vid 50–70 %, 0 därunder,
  plus 1 %/år om lånet överstiger 4,5 × bruttoårsinkomsten (går att stänga av)
- Ränteavdrag: 30 % upp till 100 000 kr ränta per år, 21 % däröver
- Kontantbehov vid tillträde: kontantinsats, lagfart (1,5 % + 825 kr),
  nya pantbrev (2 % + 375 kr), besiktning, flytt och inflyttningsbudget

**Driften**

- El, uppvärmning, VA, sophämtning, försäkring, sotning, samfällighet
- Bredband, hemlarm, serviceavtal och snöröjning — abonnemang som följer huset
  och inte hushållet
- Slamtömning vid enskilt avlopp och tomträttsavgäld på arrenderad tomt
- Fastighetsavgift (takbelopp) och underhåll som andel av husets värde per år

**Livet**

- Mat, bil, barnomsorg, försäkringar, mobil och streaming, kläder, fritid,
  semester, andra lån och sparande
- Barnbidrag inkl. flerbarnstillägg räknas fram från antal barn

**Resultatet**

- Kvar per månad när allt är betalt, boendekvot och jämförelse mot nuvarande boende
- Fördelningen av nettoinkomsten och alla utgiftsposter sorterade efter storlek
- Räntekänslighet 1–8 % med bankens kalkylränta 7 % utmärkt

## Läsa in en annons

Kalkylen hämtar aldrig en annons själv: Booli och Hemnet tillåter inte att en
annan webbplats läser dem (CORS), och en API-nyckel i en öppen sida är en läckt
nyckel. Annonsen kommer in på två sätt i stället, båda genom din egen
webbläsare. Pris, boarea, driftkostnad, taxeringsvärde och adress plockas ut,
och varje träff visas tillsammans med det den lästes ur — så en feltolkning
syns innan den används.

**Bokmärket.** Öppna **Läs in från annons** och dra *Hämta huset till
Huskalkylen* till bokmärkesfältet. Stå sedan på huset — till exempel
<https://www.booli.se/bostad/2521054> — och klicka på bokmärket. Kalkylen
öppnas med siffrorna ifyllda, redo att granskas.

Bokmärket kör i annonssidans eget fönster, och kommer förbi CORS av samma skäl
som sidan själv gör det: det *är* sidan. Det läser husets egna data där de
ligger — sidans JSON-LD och `__NEXT_DATA__` — och tar med den synliga texten som
reserv när sidan inte lägger ut något. Allt skickas vidare i adressen till
kalkylen; ingenting passerar någon server.

Enstaka sajter med hård `Content-Security-Policy` kan hindra bokmärken från att
köra. Då finns inklistringen kvar.

**Inklistring.** Öppna huset på Booli, Hemnet eller hos mäklaren, markera hela
sidan och kopiera. Klistra in i **Läs in från annons**. Bara adressen till
annonsen räcker inte — det är sidan bakom den som ska läsas.

Driftkostnaden i en annons är en klumpsumma för el, värme, VA, sophämtning,
försäkring och sotning. Den ersätter därför de posterna i stället för att
läggas till dem — annars räknas de två gånger. Bocka ur rutan för att gå
tillbaka till egna siffror.

Taxeringsvärdet sätter fastighetsavgiften till 0,75 % per år, dock högst
takbeloppet.

## Kvar till var och en

Delar de gemensamma utgifterna mellan två personer på tre sätt: lika, efter
inkomst, eller en egen fördelning med reglage. Barnbidrag och övriga inkomster
räknas som hushållets och dras av innan delningen, så personernas överskott
alltid summerar till hushållets.

## Flera hus

Hushållet — löner, barn, levnadskostnader, ränta och hur ni delar utgifterna —
är gemensamt och följer med mellan husen. Pris, kontantinsats, köpkostnader och
hela driften hör till det enskilda huset.

Nya hus ärver siffrorna från det du står på, så det går snabbt att jämföra två
lika hus med olika pris. Med minst två hus dyker en jämförelse upp längst ner med
kvar per månad, boendekvot, kontantbehov och marginalen vid 7 % ränta.

## Dela och exportera

Ingen server, ingen databas — hela kalkylen får plats i adressen. Bara de fält
som skiljer sig från standardvärdena tas med, så en länk landar på ett par hundra
tecken.

- **Dela kalkylen som länk** — allt: hushållet och samtliga hus
- **Dela {huset}** — bara huset du står på. Den som öppnar länken får huset
  tillagt i sin egen kalkyl i stället för att få den överskriven
- **Spara som fil** / **Öppna fil** — samma innehåll som JSON

Öppnar du någon annans hela kalkyl visas en banner och din egen sparade kalkyl
lämnas orörd tills du antingen ändrar något eller väljer att behålla den delade.

## Viktigt

Riktvärdena i tabellen längst ner är vanliga nivåer för en svensk villa, inte
fakta om ett specifikt hus. Driftkostnader och taxeringsvärde ska hämtas från
mäklaren, och amorteringskraven har setts över de senaste åren — stäm av med
banken innan du litar på amorteringsraden. Kalkylen är ett underlag för att
tänka, inte ett lånelöfte.

## Under huven

Vanlig HTML, CSS och JavaScript i en fil. Inget ramverk, inga externa
beroenden, inga nätverksanrop — sidan fungerar offline och i en strikt CSP.
Bokmärket är samma sak: en `javascript:`-adress som byggs av sidan själv, med
kalkylens egen adress inbakad, och som bara körs när du klickar på det.

Diagramfärgerna är validerade för färgseendevariation och kontrast mot både
den ljusa och den mörka bakgrunden, och varje diagram har en tabellvy.
