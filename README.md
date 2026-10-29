# sbpaulsen.no

Min personlige nettside, der jeg samler prosjektene mine. Mest for moro skyld.

Siden er bygget som et lite filsystem: et mappetre til venstre, en filsti øverst og innholdet til høyre. Den har to deler:

- **Hjem** – kort intro om meg og de mest aktuelle prosjektene.
- **Prosjekter** – alle prosjektene samlet, med status og sist oppdatert.

> Status: under oppbygging. Repoet inneholder foreløpig bare denne filen og `.gitignore`. SvelteKit-oppsettet kommer i neste steg.

## Prosjekter

| Prosjekt | Hva det er | Status |
| --- | --- | --- |
| `fond-100k` | Et makro-/aksjefond på 100 000 kr, drevet etter Stanley Druckenmiller og George Soros. Regler, posisjoner og investeringsdagbok. Ingenting her er investeringsråd. | aktiv |
| `nm-i-ai` | Forberedelser og logg mot Norgesmesterskapet i AI. | aktiv |
| `pokerbot` | Heads-up no-limit Texas Hold'em-bot, inspirert av Citadels pokerbot-turnering. | planlegges |

## Teknologi

- [SvelteKit](https://svelte.dev/docs/kit) med `@sveltejs/adapter-static` (siden bygges til vanlige statiske filer)
- Hostes gratis på GitHub Pages
- Publiseres automatisk med GitHub Actions ved push til `main`
- Domene: sbpaulsen.no

## Kjøre siden lokalt

Du trenger [Node.js](https://nodejs.org/) (LTS-versjonen).

```sh
npm install      # installerer avhengigheter (første gang)
npm run dev      # starter siden på http://localhost:5173
npm run build    # bygger den ferdige siden til mappen build/
```

## Publisere en endring

```sh
git add .
git commit -m "Kort beskrivelse av endringen"
git push
```

Når endringen er pushet til `main`, bygger GitHub Actions siden og legger den ut på sbpaulsen.no etter et par minutter.

## Mappestruktur (planlagt)

```
src/
├── routes/
│   ├── +layout.svelte         felles layout: mappetre, filsti, bunntekst
│   ├── +page.svelte           hjem
│   └── prosjekter/            oversikt og hvert prosjekt
└── lib/
    ├── components/            gjenbrukbare deler
    └── data/
        └── prosjekter/        én datafil per prosjekt
static/
└── CNAME                      kobler GitHub Pages til sbpaulsen.no
```

## Legge til et nytt prosjekt

Lag en ny datafil i `src/lib/data/prosjekter/` med navn, kort beskrivelse, status, dato og filer. Prosjektet dukker da opp i mappetreet og i oversikten uten at layouten må endres.

## Python-prosjekter

Analyse og kode (f.eks. for fondet og pokerboten) lages i Jupyter notebooks og vanlige `.py`-filer, med samme struktur i hvert prosjekt:

```
<prosjekt>/
├── notebooks/   utforsking og analyse
├── src/         gjenbrukbar Python-kode
├── data/        rådata og bearbeidede data
└── README.md    hva prosjektet er og hvordan det kjøres
```

Nettsiden viser bare de ferdige resultatene; den regner ingenting ut selv.
