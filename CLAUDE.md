# sbpaulsen.no – personlig nettside

## Om meg
- Sander Paulsen, Oslo.
- Siden skrives på norsk (bokmål).

## Hva siden er
En personlig nettside med **kun to hoveddeler**:
1. **Hjem** – kort intro om meg og et utvalg av prosjektene.
2. **Prosjekter** – alle prosjektene mine samlet på ett sted. Man skal kunne bla gjennom alle og åpne hvert enkelt.

Prosjektene foreløpig:
- **fond-100k** – mitt eget makro-/aksjefond på 100 000 kr, drevet etter Stanley Druckenmiller og George Soros.
- **nm-i-ai** – jeg er påmeldt Norgesmesterskapet i AI. Forberedelser og logg.
- **pokerbot** – heads-up no-limit Texas Hold'em-bot, inspirert av Citadels pokerbot-turnering.

Alle prosjekter er likestilte. Fondet og NM i AI er prosjekter på lik linje med pokerboten, ikke egne seksjoner.

## Teknisk oppsett
- Bygges med SvelteKit og `@sveltejs/adapter-static` (ferdig bygget til statiske filer).
- Ruter: `/` (Hjem), `/prosjekter` (oversikt over alle), `/prosjekter/<prosjekt>/...` (filer i hvert prosjekt).
- Hvert prosjekt er definert i én datafil (navn, kort beskrivelse, status, dato, filer), slik at et nytt prosjekt kun krever en ny datafil.
- Felles layout (meny og bunntekst) i `+layout.svelte`. Gjenbrukbare deler som komponenter.
- Data (posisjoner, dagbok, prosjekter) ligger i egne filer, f.eks. `src/lib/data/`, så innhold kan oppdateres uten å røre layout.
- Hostes gratis på GitHub Pages. Publiseres automatisk med GitHub Actions ved push til `main`.
- Krever Node.js (LTS) lokalt. Kjør `npm run dev` for å se siden lokalt.
- Domene: sbpaulsen.no (kjøpt oktober 2026). Skal pekes til GitHub Pages via DNS (CNAME-fil i repoet + DNS-oppføringer hos registraren).
- Jeg ser endringer lokalt med `npm run dev`, og publiserer med commit + push.

## Design
- Første versjon var for stygg. Designet skal gjøres om.

### Konsept: nettsiden som et filsystem
Siden skal føles som et elegant, moderne filsystem man navigerer i, ikke en vanlig nettside med meny.

- **Mappetre** til venstre (som en filutforsker). Kun to toppnivåer: hjem og prosjekter.
  ```
  sbpaulsen/
  ├── hjem.md
  └── prosjekter/
      ├── fond-100k/
      │   ├── oversikt
      │   ├── regler.md
      │   ├── posisjoner
      │   └── dagbok/
      ├── nm-i-ai/
      │   ├── forberedelser.md
      │   └── logg/
      └── pokerbot/
          ├── veikart.md
          └── kode/
  ```
- **prosjekter/** åpnet viser alle prosjektene som en oversikt man kan bla gjennom: navn, kort beskrivelse, status (f.eks. «aktiv», «planlegges», «ferdig») og sist oppdatert. Man skal kunne sortere eller filtrere på status.
- Inne i et prosjekt skal det være lett å gå til forrige/neste prosjekt.
- **hjem.md** viser en kort intro og de mest aktuelle prosjektene, med lenke til hele oversikten.
- Mapper kan åpnes og lukkes. Aktiv fil er markert i treet.
- **Brødsmulesti** øverst som en filsti, f.eks. `~/sbpaulsen/prosjekter/fond-100k/regler.md`, der hver del er klikkbar.
- **Innholdsfeltet** til høyre viser filen som er åpnet. Ulike filtyper kan vises ulikt: tekst (`.md`), tabeller (posisjoner), lister (dagbok/logg).
- Når en mappe åpnes, vises innholdet som en oversikt (filer med navn, type, sist endret og en kort beskrivelse).
- URL-en følger filstien (`sbpaulsen.no/prosjekter/fond-100k/regler`), så hver fil kan lenkes direkte og tilbakeknappen fungerer.
- Tastatur: piltaster i treet, Enter for å åpne. Gjerne en hurtigsøk (`Ctrl+K` / `/`) for å hoppe til en fil.
- På mobil: treet blir en skuff som skyves inn fra siden, eller en mappevisning man trykker seg nedover i.
- Nye prosjekter skal kunne legges til bare ved å legge til en mappe/datafil, uten å endre layouten.

### Stil
- «Fancy», men ryddig: følelsen av et godt verktøy (tenk moderne kodeeditor eller Finder), ikke en retro-terminal.
- Monospace-skrift for filnavn og stier, en lesbar skrift for selve teksten.
- Subtile animasjoner når mapper åpnes og filer byttes. Respekter `prefers-reduced-motion`.
- Må fungere på mobil og ha lys og mørk modus.
- Ingen emojier som pynt. Bruk enkle ikoner for mappe og filtyper.
- Ønsket retning ellers: (fyll inn – f.eks. sider du liker, farger, stemning)

## Fondet – innhold og regler
- Start: 100 000 kr, 100 % kontanter. Ingen posisjoner ennå.
- Regler:
  1. Skriv en hypotese før hver handel, og hva som beviser at jeg tar feil.
  2. Start lite, øk når markedet bekrefter tesen, kutt når det motsier den.
  3. Se etter selvforsterkende prosesser (Soros' refleksivitet).
  4. Kontanter er en posisjon – ikke finn på teser når markedet er støy.
  5. Før dagbok i sanntid.
  6. Følg likviditeten (sentralbanker og kreditt).
- Siden skal ha: statusoversikt, regler, posisjonstabell og investeringsdagbok.
- Leser nå: The Alchemy of Finance (George Soros).
- Siden skal ha teksten «Ingenting her er investeringsråd».

## Pokerbot – plan
1. Spillmotor (kortstokk, håndevaluering, innsatsrunder, simulator)
2. Odds og equity (Monte Carlo, pot odds)
3. Regelbasert bot
4. Selvspill med CFR (Counterfactual Regret Minimization)
5. Tilpasning til turneringsformat

## Python, data og analyse
- Utforsking og analyse skjer i Jupyter notebooks (`.ipynb`), slik at jeg ser resultatet under hver celle og forstår hva koden gjør.
- Kode som fungerer og skal brukes om igjen flyttes til vanlige `.py`-filer og importeres tilbake i notebooken.
- Hvert prosjekt har sin egen mappe med samme struktur:
  ```
  <prosjekt>/
  ├── notebooks/   utforsking og analyse
  ├── src/         gjenbrukbar Python-kode
  ├── data/        rådata og bearbeidede data
  └── README.md    hva prosjektet er og hvordan det kjøres
  ```
- Notebooks skal være pedagogiske: korte celler, en forklarende tekstcelle før hver kodecelle, og tydelige tabeller og grafer.
- Nettsiden (Svelte) viser bare ferdige resultater; den regner ingenting ut selv.

## Arbeidsmåte
- Gjør ett steg om gangen og forklar kort hva du endret.
- Forklar ting enkelt; jeg er ny på Git og webutvikling.
