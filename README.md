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

Diagramfärgerna är validerade för färgseendevariation och kontrast mot både
den ljusa och den mörka bakgrunden, och varje diagram har en tabellvy.
