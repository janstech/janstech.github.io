# Portfolion visuaalinen uudistus – auditointi ja toteutussuunnitelma

**Päivämäärä:** 2026-07-30
**Tila:** auditointi ja suunnitelma. Mitään visuaalista uudistusta ei ole vielä toteutettu.
**Repo:** `C:\Dev\personal_portfolio` → `https://janstech.github.io/`
**Lähtötilanne:** commit `66a74b2` (working tree puhdas)

Tämä dokumentti on **suunnitelma, ei toteutuskuvaus**. Kaikki alla oleva jakautuu selvästi
havaintoihin (mitattua nykytilaa) ja suosituksiin (ehdotuksia, joita ei ole tehty).

---

## 1. Mitä auditoitiin

### Portfolion sivut ja tiedostot

| Kohde | Havainto |
|---|---|
| `index.html` (79 KB, 1185 riviä) | Yksisivuinen portfolio, 6 osiota, 22 korttia, 177 i18n-avainta |
| `gainsai/index.html` (54 KB) | Ainoa projektikohtainen sivu. Rakenteeltaan tuorein ja tekniseltä laadultaan paras sivu |
| `apps/index.html` (15 KB) | Erillinen Janstech Apps -listaussivu omalla CSS:llä ja omalla i18n-sanakirjalla |
| `kauppalista/join/`, `kauppalista/import-list/` | Deep link -laskeutumissivut, `noindex`, oma inline-CSS. Ei osa portfoliota |
| `css/style.css` (9 KB, 569 riviä) | Juuren ja GainsAI-sivun jaettu tyylitiedosto |
| `apps/css/style.css` (7 KB, 520 riviä) | Täysin erillinen tyylitiedosto, ei jaa tokeneita juuren kanssa |
| JavaScript / kielenvaihto | Inline `dict` per sivu, `data-i18n` / `-alt` / `-aria`, `localStorage: portfolio_lang` |
| Kuvat | 22 kuvatiedostoa, `index.html` lataa 2 437 KB kuvia |
| `sitemap.xml`, `robots.txt` | 3 URLia, jäsentyy, ei duplikaatteja |
| `manifest.json`, `.well-known/assetlinks.json` | Kunnossa |
| `README.md`, `AGENTS.md` | Ajan tasalla |
| `documents/` | 4 PDF:ää, 416 KB |

### Ulkoiset lähteet (vain luku, ei muutettu)

`C:\Dev\janstechapps_repo`, `C:\Dev\GainsAI`, `C:\Dev\SureKeep`, `C:\Dev\Tyotori`,
`C:\Dev\SomaFlow`, `C:\Dev\Janstech - Camera`, `C:\Dev\gains-ai-portfolio`.

### Git-historia

Tuoreimmat muutokset, joita **ei saa kumota**:

- `66a74b2` – AGENTS.md lisätty
- `c5667a6` – AI-työkalulista päivitetty (ChatGPT, Codex, Claude Code, GitHub Copilot)
- `caf51dd` – GainsAI-projekti lisätty (kortti, oma sivu, `data-i18n-alt`/`-aria`, sitemap, robots)

---

## 2. Nykytilan auditointi

### 2.1 Visuaalinen hierarkia

**Mitattua:**

| Mittari | Arvo |
|---|---|
| Sivun korkeus (1440 px) | 7 349 px |
| Sivun korkeus (390 px) | 15 741 px (~19 ruudullista) |
| `#projects`-osion korkeus | 4 120 px = **56 % koko sivusta** |
| Ensimmäinen projektikortti alkaa | y = 2 144 px (desktop), y = 4 205 px (mobiili) |
| Osioiden padding | **kaikilla identtinen 72 px / 72 px** |
| Kortteja yhteensä | 22 (10 projektia, 7 osaamista, 3 arkkitehtuuria, 2 yhteystietoa) |
| Listakohtia `<main>`-alueella | 94 |

**Ongelmat:**

1. **Ei todistusaineistoa yläosassa.** Ensimmäiset 2 144 px on pelkkää tekstiä. Rekrytoija näkee
   nimen, roolin ja kaksi pitkää tekstikappaletta ennen kuin mikään viittaa siihen, että Janilla on
   kolme julkaistua sovellusta.
2. **Kaikki osiot painavat saman verran.** Sama padding, sama korttityyli, sama listamuoto.
   Sivu on tasapaksu: mikään ei erotu tärkeimpänä.
3. **Hero ja Minusta-osio kertovat saman asian kahdesti.** Heron intro (8 riviä) ja `about_p1`
   ovat sisällöllisesti lähes identtiset. Toinen niistä on turha.
4. **Projektiosio on 10 kortin tasainen ruudukko.** Google Playssa julkaistu GainsAI ja
   "IT-laitteiden huolto ja optimointi" ovat visuaalisesti samanarvoisia.
5. **Osaamisruudukossa on orpo rivi.** 7 korttia neljän sarakkeen gridissä → viimeiselle riville jää
   3 korttia ja iso tyhjä aukko oikeaan alakulmaan.

### 2.2 Typografia

**Mitattua:**

| Elementti | Koko | Line-height | Fontti |
|---|---|---|---|
| `h1` | 48 px | 76.8 px (**1.6**) | system-ui |
| `h2.section-title` | 28.8 px | 46.08 px | system-ui |
| `h3` (korttiotsikko) | **16.8 px** | 26.88 px | system-ui |
| `p` | 16 px | 25.6 px | system-ui |
| `li` | 14.4 px | 23.04 px | system-ui |
| `.project-meta` | 12.8 px | 20.48 px | monospace |

**Ongelmat:**

1. **Minusta-osion rivinpituus on ~138 merkkiä** (1 100 px leveys, 16 px fontti). Luettavuuden
   optimi on 60–75 merkkiä. Tämä on sivun suurin yksittäinen typografiavirhe.
2. **`h3` on 16.8 px ja leipäteksti 16 px** – korttiotsikko on 5 % suurempi kuin leipäteksti.
   Hierarkia syntyy käytännössä vain lihavoinnista.
3. **`h1`:n line-height 1.6 on liian väljä** display-kokoiselle otsikolle (sopiva olisi 1.05–1.15).
4. **Fira Codea ei ladata.** `--font-mono` listaa `"Fira Code"`-fontin, mutta sitä ei ole linkitetty
   eikä self-hostattu (`document.fonts.size === 0`). Laskettu arvo on `monospace`, eli sivu
   renderöityy Windowsilla Consolasilla, macOS:llä Menlolla, Linuxilla DejaVulla. **Monospace-teksti
   näyttää eri koneilla eri levyiseltä** – ja sitä on paljon: nav, painikkeet, kaikki `.project-meta`,
   hero-koodilohko, footer.
5. Tyyppiskaala on selaimen oletusten johdannainen (48 / 28.8 / 19.2 / 16.8 / 16 / 14.4 / 12.8),
   ei harkittu skaala.

### 2.3 Värit ja kontrasti

**Mitattua – kaikki tekstit läpäisevät WCAG AA:n:**

| Kohde | Kontrasti | Vaatimus | Tulos |
|---|---|---|---|
| Kortin listakohta `#9ca3af` / `#0f172a` | 7.03:1 | 4.5 | PASS |
| Nav-linkki | 8.27:1 | 4.5 | PASS |
| Korostuslinkki `#64ffda` | 14.33:1 | 4.5 | PASS |
| Footer-huomautus | 7.95:1 | 4.5 | PASS |
| `.project-meta` 12.8 px | 7.03:1 | 4.5 | PASS |

**Tämä on nykysivuston selkein vahvuus ja se on säilytettävä.**

**Ongelmat:**

1. **Yksi ainoa korostusväri** (`--accent: #64ffda`) hoitaa linkit, painikkeet, otsikkoviivat,
   luetteloiden pisteet, aktiivisen kielen ja hover-tilat. Ei mitään keinoa erottaa
   "julkaistu sovellus" -tasoa "vanha harjoitustyö" -tasosta muuten kuin sijainnilla.
2. **Pintoja on vain kaksi** (`--bg #050816`, `--card-bg #0f172a`) ja niiden ero on hyvin pieni.
   Sivu näyttää yhdeltä tummansiniseltä massalta.
3. **Palettikonflikti JanstechApps.comin kanssa.** Brändisivusto käyttää
   `--bg:#060f1f` + `--accent:#8fd3ff` / `--accent-2:#8fffc8`. Portfolio käyttää
   `#050816` + `#64ffda`. Sivustot ovat niin lähellä toisiaan, että ne sekoittuvat, mutta
   eivät riittävän lähellä näyttääkseen tarkoitukselliselta perheeltä.
4. Statustietoa ei ole missään värikoodattuna – "julkaistu" vs. "kehityksessä" ei erotu.

### 2.4 Sommittelu ja rytmi

- Sisältöleveys `min(1100px, 100% - 3rem)` on kaikelle sama: 138 merkin tekstikappaleille ja
  3-sarakkeiselle korttigridille. Tekstille tarvitaan kapeampi rata.
- `.project-grid` on `repeat(auto-fit, minmax(260px, 1fr))` ja kortit `height: 100%`, joten
  **lyhyet kortit venytetään pitkien mittaan** → osaamisosiossa isoja tyhjiä alueita korttien pohjalla.
- Projektikortin leveys 1440 px:llä on ~330 px, ja siihen ladotaan 200+ sanaa. Rivinpituus tekstissä
  on liian lyhyt ja tekstimassa liian pitkä samaan aikaan.
- Kuvat tulevat vasta kortin **loppuun**, ~900 px otsikon alapuolelle.

### 2.5 Hero – tarkempi arvio

Nykyinen hero (545 px desktop / 1 053 px mobiili):

- `hero_label` "Hei, olen"
- `h1` "Jan Sarivuo"
- `h2` "Junior Full Stack- ja Android-kehittäjä"
- 8 rivin intro
- 2 CTA:ta ("Katso projektit", "Ota yhteyttä")
- koodilohko, jossa `role: "Junior Full Stack -kehittäjä"`

**Arvio:**

- **"Junior" esiintyy kahdesti taitteen yläpuolella** – otsikossa ja koodilohkossa. Se on
  totuudenmukaista (valmistunut 11/2025), mutta se on nyt heron *pääviesti*. Vahvin todiste –
  kolme itsenäisesti julkaistua ja ylläpidettyä Play-sovellusta omine backendeineen – ei näy
  herossa lainkaan.
- Intro on liian pitkä. Se yrittää sanoa kaiken ja sanoo siksi vähän. Sama sisältö toistuu
  Minusta-osiossa.
- Koodilohko on sinänsä kelpo idea ja henkilökohtaisempi kuin geneerinen hero-kuva, mutta
  se on staattinen `const dev = {...}` -objekti, joka toistaa otsikon tiedot. Se ei todista mitään.
- CTA "Katso projektit" ei kerro mitään. "Katso julkaistut sovellukset" kertoisi.

**Johtopäätös: hero rakennetaan uudelleen, mutta koodi-/spec-idea säilytetään** – muutetaan
toistavasta esittelystä todennettavaksi faktalistaksi.

### 2.6 Projektien esittely

Nykyiset 10 korttia yhtenä ruudukkona:

Kauppalista · WaveIQ · GainsAI · Tuotehaku · Icecat · MySQL-recovery · Palvelinympäristöt ·
IT-laitteiden huolto · The Game (Unity) · The Game (selain)

**Ongelmat:**

1. **Ei ryhmittelyä eikä hierarkiaa.** Kolme tuotantoon julkaistua sovellusta hukkuu joukkoon.
2. **Toisteinen kirjoitustapa.** Kaikki kolme Android-korttia alkavat samalla kaavalla:
   "Kehitin … Sovellus on julkaistu Google Play -kaupassa tuotantoon. Toteutin kokonaisuuden
   end-to-end: …". Peräkkäin luettuna se kuulostaa mallipohjalta.
3. **Ei sovellusikoneita korteissa.** Logot ovat olemassa (`apps/images/GainsAI.png`,
   `AI.png`, `iq_kuv1.png`), mutta niitä ei käytetä juuren sivulla.
4. **Monospace-tekniikkarivi on visuaalisesti painavampi kuin projektin nimi.** Se kietoutuu
   4–5 riville ja vetää katseen ennen otsikkoa.
5. **Kaksi puuttuvaa projektia.** `SureKeep` (`com.janstech.warrantywallet` v0.1.3, suljettu
   testaus) ja `Työtori` (`com.janstech.tyotori` v0.7.6, ei tuotantovalmis) mainitaan AGENTS.md:ssä
   tärkeinä sovelluksina, mutta ne puuttuvat portfoliosta kokonaan.

### 2.7 Osaamisen esittely

7 identtistä korttia: Ohjelmointi & web · Tietokannat · Palvelinympäristöt & DevOps ·
Integraatiot & muut · Android & mobiili · Pelikehitys & Multimedia · AI-avusteinen kehitys.

**Ongelmat:**

1. **Kaikki on samanarvoista listaa.** "Kotlin & Jetpack Compose (UI)" ja "Sprite-animaatiot &
   partikkeliefektit" näyttävät yhtä painavilta. Ensimmäinen on hänen ammattinsa ydin,
   toinen vanha opiskeluprojektin yksityiskohta.
2. **Pelikehitys saa oman kortin** samalla painoarvolla kuin Android ja backend.
3. **Ei erottelua "olen käyttänyt" ja "olen vastannut tuotannossa" -välillä.** AGENTS.md vaatii
   nimenomaan tätä erottelua.
4. Kapeat sarakkeet rikkovat otsikot: "Ohjelmointi & web-kehitys" ja "Palvelinympäristöt & DevOps"
   katkeavat kahdelle riville.
5. "Integraatiot & muut" – *muut* on kaatoluokka, ja siinä on IT-laitehuolto teknisen
   integraatio-osaamisen seassa.

### 2.8 Luottamus ja uskottavuus

| Väite | Näkyykö sivulla | Arvio |
|---|---|---|
| Julkaissut Android-sovelluksia Google Playssa | Kyllä, mutta vasta 2 144 px alaspäin | **Alikorostettu** |
| Rakentanut omia backend-järjestelmiä | Kyllä, projektiteksteissä | Riittävä |
| Toteuttanut autentikoinnin ja tilausmaksut | Vain GainsAI-sivulla | **Puuttuu etusivulta** |
| Ylläpitänyt Linux/Hetzner-tuotantoympäristöä | Kyllä, oma projektikortti | Riittävä |
| Tietokanta- ja varmuuskopiointityö | Kyllä | Riittävä |
| Dokumentoinut arkkitehtuuria | Kyllä, mutta rikkinäisen näköisillä placeholder-korteilla | **Heikentää uskottavuutta** |
| AI-työkalut osana oikeaa kehitystyötä | Kyllä | Riittävä |
| Kykenee end-to-end-kokonaisuuteen | Implisiittisesti | **Ei sanota suoraan missään** |

**Suurin uskottavuusongelma ei ole liioittelu vaan aliarviointi.** Sivu kertoo totuuden mutta
hautaa sen. Toiseksi suurin on Arkkitehtuuri-osion kolme katkoviivalaatikkoa – ne näyttävät
latautumatta jääneiltä kuvilta.

### 2.9 Persoonallisuus

Nykyisin persoonallisuutta on kaksi asiaa: hero-koodilohko ja suomenkielinen suora sävy
("Haen junior-tason tehtäviä, joissa pääsen yhdistämään…"). Molemmat toimivat.

Puuttuu: mikään ei kerro **miten** Jan työskentelee – että hän kirjoittaa ADR-dokumentteja,
tekee release-gate-auditointeja, ajaa regressiomatriiseja ja pitää dokumentaation koodin tahdissa.
Se on GainsAI-repossa selvästi näkyvä työtapa ja aidosti erottava tekijä, mutta portfoliossa
siitä on vain rivi "dokumentoin mielelläni myös arkkitehtuurin".

### 2.10 Tekniset viat (todennetut)

| # | Vika | Todiste | Vakavuus |
|---|---|---|---|
| 1 | **`index.html`:ssä ei ole yhtään SEO-metatietoa** – ei description, canonical, OG, Twitter eikä robots | DOM-tarkistus palautti `null` kaikille | **Korkea** – tämä on sitemapin `priority 1.0` -sivu |
| 2 | **CV:n prefetch osoittaa väärään tiedostonimeen.** `href="documents/jan_sarivuo_cv.pdf"`, gitissä `documents/Jan_Sarivuo_cv.pdf` | `git ls-files documents/` | **Korkea** – 404 jokaisella sivulatauksella GitHub Pagesissa (kirjainkoko merkitsevä) |
| 3 | **`images/favicon.png` on 520 KB** | `ls -la` | **Korkea** – favicon ladataan joka sivulla |
| 4 | **Ankkurinavigaatio piilottaa otsikot headerin alle.** `scroll-margin-top: 0px` kaikilla osioilla, sticky header 66 px | DOM-mittaus | Keskisuuri |
| 5 | **Sticky headerin gradientti päättyy `transparent`iin** → sisältö näkyy headerin läpi | Kuvakaappaus (Arkkitehtuuri-otsikko leikkautuu headerin taakse) | Keskisuuri |
| 6 | **10 kuvaa ilman `width`/`height`- ja `loading="lazy"`-attribuutteja** | DOM-tarkistus | Keskisuuri – layout shift + 1,6 MB heti |
| 7 | **4 PDF:ää (416 KB) prefetchataan** jokaisella latauksella | `index.html` rivit 6–9 | Keskisuuri |
| 8 | `images/placeholder-architecture.png` (981 KB) ei ole käytössä missään | Referenssiskannaus | Matala |
| 9 | Ei skip-linkkiä, `<nav>`illa ei `aria-label`ia juuren sivulla | DOM-tarkistus | Matala |
| 10 | Ei omaa `:focus-visible`-tyyliä – selaimen oletusrengas on 1 px tumma tummalla | DOM-mittaus | Matala |
| 11 | `apps/index.html` sisältää 8 linkkiä repoihin, joita ei ole tässä reposssa (`../kauppalista-privacy-policy/` jne.) | Linkkiskannaus | **Selvitettävä** (ks. 3.3) |

---

## 3. Vahvuudet, jotka on säilytettävä

1. **Kontrasti läpäisee WCAG AA:n kauttaaltaan.** Ei saa rikkoa uudistuksessa.
2. **Kevyt arkkitehtuuri.** Ei buildia, ei riippuvuuksia, ei frameworkia. Sivu latautuu nopeasti
   heti kun kuvaongelmat korjataan.
3. **i18n-mekanismi on hyvä ja laajennettu oikein.** `data-i18n` / `-alt` / `-aria`, jaettu
   `portfolio_lang`, `aria-pressed`. Ei kosketa.
4. **GainsAI-sivun rakenne** on paras malli tuleville projektisivuille.
5. **Sisältö on rehellistä ja todennettavaa.** Ei keksittyjä lukuja. Tämä on harvinaista.
6. **Suomenkielinen sävy on luonteva**, ei käännöskukkasia.
7. **Hero-koodilohkon idea** – kehitä, älä poista.

---

## 4. Sisältöauditointi

### 4.1 Projektien todennettu tila

| Projekti | Paketti / versio | Tila | Lähde |
|---|---|---|---|
| **GainsAI** | `com.janstech.gainsai` 1.0.0.0 | **Julkaistu Playssa (tuotanto)** | `docs/releases/gainsai-paid-release-go-no-go-2026-07-26.md` |
| **Kauppalista & Muistiinpanot** | `com.janstech.kauppalista` | **Julkaistu Playssa** | Play-linkki + janstechapps.com/apps/kauppalista/ |
| **WaveIQ Radio** | `com.janstech.radioplayer` | **Julkaistu Playssa** | Play-linkki + janstechapps.com/apps/waveiq/ |
| **SureKeep** | `com.janstech.warrantywallet` 0.1.3 | **Suljettu testaus** – legal-sivut olemassa, ei app-sivua | `SureKeep/docs/deployment.md` |
| **Työtori** | `com.janstech.tyotori` 0.7.6 | **Kehityksessä**, ei tuotantovalmis | `Tyotori/docs/release/README.md` |
| SomaFlow | – | Varhainen v1-perusta | `SomaFlow/README.md` |
| Janstech Camera | – | Henkilökohtainen WebView-MVP | `Janstech - Camera/README.md` |

> **Huom.** SureKeepiä ja Työtoria ei saa esittää julkaistuina. Ne kannattaa lisätä omana,
> selvästi merkittynä "kehityksessä" -ryhmänä – se kertoo aktiivisesta tekemisestä ilman
> liioittelua.

### 4.2 Ehdotettu projektien ryhmittely

**Ryhmä 1 – Julkaistut sovellukset (Google Play)** — suurin visuaalinen painoarvo
1. GainsAI · 2. Kauppalista & Muistiinpanot · 3. WaveIQ Radio

**Ryhmä 2 – Työn alla** — kompaktit rivit, selkeä tilamerkintä
4. SureKeep (suljettu testaus) · 5. Työtori (kehityksessä)

**Ryhmä 3 – Tuotantojärjestelmät ja integraatiot (työssäoppimisjakso)** — keskikokoiset kortit
6. Tuotehaku-järjestelmä · 7. Icecat → WooCommerce · 8. MySQL-korjaukset & recovery
9. Palvelinympäristöt, julkaisut ja varmuuskopiointi

**Ryhmä 4 – Aiemmat toteutukset** — tiiviit rivit, kuvat vain projektisivulla
10. The Game (Unity) · 11. The Game (selainversio)

**Siirrettäväksi pois projekteista:** "IT-laitteiden huolto ja optimointi" → rivi
työkokemuksen tai Minusta-osion yhteyteen. Se ei ole ohjelmistoprojekti.

### 4.3 Sisällön päällekkäisyydet ja pituudet

| Havainto | Ehdotus (ei toteutettu) |
|---|---|
| `hero_text` ja `about_p1` kertovat saman | Lyhennä hero 2 lauseeseen, jätä laajempi versio Minusta-osioon |
| 3 Android-korttia alkavat samalla kaavalla | Kirjoita jokaiselle oma kärki: GainsAI = AI + tilaukset, Kauppalista = yksityisyys + offline, WaveIQ = striimaus + suositukset |
| Kauppalista-kortissa 7 bullettia, WaveIQ:ssa 6, GainsAI:ssa 6 | Etusivulle 3 bullettia / sovellus, loput projektisivulle |
| Tuotehaku, Icecat, MySQL, Palvelinympäristöt ovat neljä erillistä korttia samasta jaksosta | Yhdistä yhden otsikon alle "Työssäoppimisjakso – tuotantojärjestelmät" + 4 tiivistä alakohtaa |
| `proj_it_*` (IT-huolto) on projektikortti | Siirrä pois projekteista |
| Arkkitehtuuri-osio on oma osionsa 3 katkoviivalaatikolla | Yhdistä dokumentit niihin projekteihin joihin ne liittyvät + yksi "Dokumentaatio"-rivi |
| Osaamisosiossa 7 korttia / 33 bullettia | Kolmitasoinen rakenne, ks. 4.4 |
| `apps/index.html` on käytännössä janstechapps.comin duplikaatti | ks. 3.3 / luku 12 |

### 4.4 Ehdotettu osaamisosion rakenne

Kolme *eriarvoista* tasoa yhden tasapaksun korttirivistön sijaan:

**Taso 1 – "Rakennan ja ylläpidän"** (mitä hän on oikeasti vienyt tuotantoon)
Android-sovellukset (Kotlin, Compose, Material 3) · FastAPI-backendit · MariaDB/MySQL ·
Autentikointi ja sovelluksen eheys (Firebase Auth, App Check, Play Integrity) ·
Tilausmaksut (Play Billing + palvelinvarmennus) · Linux-tuotantoympäristöt ja varmuuskopiointi

**Taso 2 – "Teknologiat"** (kompakti, ryhmitelty tekstirivi – ei badge-seinää)
Kielet · Android · Backend · Data · Infra · Integraatiot

**Taso 3 – "Työtavat"** (erottava tekijä, nyt lähes näkymätön)
Arkkitehtuuridokumentaatio ja ADR:t · Release-portit ja auditoinnit · Regressiomatriisit ·
Lokalisointivalidaattorit build-ketjussa · AI-avusteinen kehitys osana oikeaa työtä

Pelikehitys siirtyy Taso 2:n loppuun tai "Aiemmat toteutukset" -ryhmän yhteyteen.

---

## 5. Kolme visuaalista suuntaa

### Suunta A – "Työpöytä" (Workbench)

| | |
|---|---|
| **Tunnelma** | Hyvin konfiguroidun työaseman rauha. Tumma, mutta rakenteellinen: näkyvä grid, ohuet viivat, harkittu tiheys. Ei hehkua, ei lasia. |
| **Väripaletti** | Neutraali grafiitti, **ei sinimusta**: `#0E1013` → `#15181D` → `#1C2027`. Teksti `#E9EAEC`, vaimennettu `#9DA3AD`. Korostus **hiekka/amber `#E0A85C`** + tila-värit: vihreä = julkaistu, harmaa = kehityksessä. Korostusta käytetään säästeliäästi. |
| **Typografia** | Otsikot ja leipäteksti samassa groteskissa, mutta selvä skaala: 44 / 30 / 22 / 17 / 15. Mono **järjestelmällisesti** vain metadatalle, labeleille ja koodille – ei painikkeille eikä navigaatiolle. Tekstiradan maksimileveys 68ch. |
| **Kortit ja pinnat** | Kelluvat varjostetut kortit korvataan **litteillä paneeleilla, jotka erottuvat 1 px viivalla**. Enintään kaksi pintatasoa. Pyöristys 6–10 px, ei 14–999 px sekaisin. |
| **Hero** | Kaksipalstainen: vasemmalla nimi, yksirivinen rooli, 2 lauseen intro, 2 CTA:ta. Oikealla **spec-taulukko** (ei fake-koodia): `Julkaistut sovellukset 3 · Android Kotlin/Compose · Backend FastAPI + MariaDB · Infra Linux/Hetzner · Maksut Play Billing`. Korkeus ~420 px. |
| **Projektit** | Julkaistut sovellukset **leveinä vaakariveinä**: ikoni + nimi + tilamerkki + yksi lause + tekniikkarivi + linkit + kuvakaappausnauha. Muut ryhmät tiiviinä listariveinä. |
| **Kuvat** | Kuvakaappaukset omassa suhteessaan, ohut reunus, ei puhelinkehyksiä. Vaakanauha, jossa 3 kuvaa vierekkäin. |
| **Animaatio** | 120 ms hover, focus-rengas, ei muuta. |
| **Vahvuudet** | Jatkaa nykyistä tummaa identiteettiä → **vaiheistettavissa turvallisesti**, jokainen vaihe julkaisukelpoinen. Tummat sovelluskuvakaappaukset istuvat luontevasti. Amber + grafiitti erottaa selvästi janstechapps.comin sinicyan-paletista. Kestää paljon sisältöä. |
| **Riskit** | Tumma + mono voi lipsua "hakkeriteemaan", jos monoa käytetään liikaa – siksi mono rajataan tiukasti. Amber vaatii tarkkuutta kontrastissa (testattava ≥ 4.5:1). |
| **Miksi Janille** | Spec-taulukko-metafora sopii siihen, mitä hän oikeasti tekee: todennettuja faktoja, release-portteja, mittareita. Sivu näyttää siltä kuin sen olisi tehnyt insinööri, jolla on makua – ei markkinoija. |

### Suunta B – "Tekninen lehti" (Technical Editorial)

| | |
|---|---|
| **Tunnelma** | Insinööridokumentaatio kohtaa suomalaisen lehtitaiton. Vaalea, luottavainen, tiheä mutta hallittu. Kuin hyvin taitettu tekninen aikakauslehti. |
| **Väripaletti** | Lämmin paperinvalkoinen `#FBFAF8` / `#F2F0EC`, muste `#15181C`, vaimennettu `#5A6068`. Yksi korostus: **syvä signaalisininen `#1D4ED8`** tai oksidinoranssi. Tumma teema toissijaisena vaihtoehtona, ei identiteettinä. |
| **Typografia** | Kantava elementti. Leipäteksti 17–18 px, line-height 1.65, mitta 65–70ch. Otsikot tiiviillä line-heightilla (1.1). Pienet versaalilabelit väljällä kirjainvälillä osioiden merkitsemiseen. |
| **Kortit ja pinnat** | **Lähes ei kortteja lainkaan.** Hiusviivat, tyhjä tila ja vasen palstalinja hoitavat erottelun. Kortti vain siellä missä sisältö on aidosti korttimainen (sovellusrivi). |
| **Hero** | Yksi palsta, vasemmalle tasattu. Nimi, rooli, 2 lausetta, kolme faktachippiä, 2 CTA:ta. ~360 px. |
| **Projektit** | Toimituksellinen lista: iso kuva vasemmalla, teksti oikealla, vuorottelevat. Kuvat saavat kantaa. |
| **Kuvat** | Tummat sovelluskuvakaappaukset vaalealla pohjalla tarvitsevat harkitun kehyksen (ohut reunus + hienovarainen sisävarjo). |
| **Animaatio** | Käytännössä ei mitään. |
| **Vahvuudet** | **Kaikkein vähiten AI-generoidun näköinen.** Vaalea kehittäjäportfolio on harvinainen ja luetaan itsevarmuutena. Paras luettavuus ja paras Lighthouse. Sopii siihen, että Jan kirjoittaa dokumentaatiota työkseen. |
| **Riskit** | Suurin kertamuutos – tumma → vaalea ei vaiheistu hyvin, sivu näyttää välivaiheessa keskeneräiseltä. Vaatii kurinalaista typografiaa tai näyttää lattealta. Tummat kuvakaappaukset vaativat lisätyötä. Kauimpana JanstechApps.comin ilmeestä (voi olla hyvä tai huono). |
| **Miksi Janille** | Hänen työtapansa *on* dokumentoiva. Tämä tekee siitä visuaalisen identiteetin. Riski on toteutuksen kokoluokassa, ei suunnassa. |

### Suunta C – "Kenttämuistiinpano" (Field Notes)

| | |
|---|---|
| **Tunnelma** | Hillitty, kaksisävyinen, hieman kartografinen. Vaalea perusta, tumma "syvyysosio" projekteille. Konkreettinen, ei koristeellinen. |
| **Väripaletti** | Perusta murrettu vaalea `#F6F5F2`, projektiosio syvä `#181B1F`. Korostus **metsänvihreä `#2F6B4F`** + lämmin harmaa. Kahden sävyn vaihtelu luo rytmin, jota nykysivustolta puuttuu. |
| **Typografia** | Sama skaala kuin A:ssa, mutta numeroille ja mittareille tabulaariset numerot; osioiden numerointi (01 / 02 / 03) kuten kenttämuistiinpanoissa. |
| **Kortit ja pinnat** | Vaaleat osiot: viivat ja tyhjä tila. Tumma projektiosio: paneelit. Kaksi eri kohtelua, jotka merkitsevät sisällön lajia. |
| **Hero** | Vaalea, tyyni, yksi palsta + kapea faktarivi alareunassa. |
| **Projektit** | Tummalla pohjalla, numeroituina. Kuvakaappaukset loistavat. |
| **Animaatio** | Vain vaalea↔tumma-siirtymän reunaviiva, ei liikettä. |
| **Vahvuudet** | Ratkaisee "tasapaksu"-ongelman rakenteellisesti, ei koristeilla. Tummat kuvat saavat tumman taustan, tekstit vaalean. Erottuva ilman temppuja. |
| **Riskit** | Kaksi teemaa = kaksi tokensettiä = eniten CSS-ylläpitoa. Vaihtelu voi näyttää epäjohdonmukaiselta jos rajat eivät ole terävät. Kaksinkertainen kontrastitestaus. |
| **Miksi Janille** | Antaa julkaistuille sovelluksille oman "näyttämön" ilman että niitä tarvitsee koristella. |

---

## 6. Suositeltu suunta

## → **Suunta A – "Työpöytä"**, lainaten Suunta B:n typografista kuria

(mitta 68ch, selkeä tyyppiskaala, hiusviivat varjojen sijaan, mono vain metadatalle)

**Perustelut:**

1. **Sopii Janin osaamiseen.** Hänen vahvuutensa on todennettu, mitattava tuotantotyö:
   release-portit, migraatiot, varmuuskopiot, App Check, entitlementit. Spec-taulukko- ja
   tilamerkintä-kieli esittää ne sellaisinaan. Ei tarvita metaforia.

2. **Toimii työnhaussa.** Rekrytoija näkee ensimmäisen 500 px:n sisällä: nimi, rooli,
   *kolme julkaistua sovellusta*, oma backend, tuotantoinfra, kaksi CTA:ta. Nykyisin sama tieto
   on 2 144 px alempana.

3. **Tukee sovellusten esittelyä.** Leveä vaakarivi antaa jokaiselle julkaistulle sovellukselle
   ikonin, tilamerkin, kuvakaappausnauhan ja linkit yhdellä silmäyksellä – kolmen kapean
   tekstipalstan sijaan.

4. **Ei näytä AI-generoidulta.** Se välttää nimenomaan ne piirteet, jotka tekevät
   template-vaikutelman: gradienttihehku, lasikortit, kelluvat pallot, valtava tyhjä hero,
   badge-seinä. Litteät paneelit + hiusviivat + amber-korostus + tabulaarinen data on
   *harkitun näköinen* ratkaisu, ei generaattorin oletus.

5. **Eroaa geneerisistä kehittäjäportfolioista.** Tyypillinen kehittäjäportfolio on
   tummansininen, mint-korostuksella, kolme korttia rivissä. Nykyinen sivu on juuri sitä.
   Neutraali grafiitti + amber + tilamerkinnät + spec-taulukko ei ole.

6. **Erottuu JanstechApps.comista.** Brändisivu: `#060f1f` + `#8fd3ff`/`#8fffc8`,
   pyöreät (22–28 px) läpikuultavat paneelit, ambient-valot. Portfolio: `#0E1013` + amber,
   6–10 px, litteät paneelit, hiusviivat. Sukulaisuus säilyy (molemmat tummia), mutta
   sivustot eivät sekoitu.

7. **Toteutettavissa hallitusti.** Koska pohjaväri pysyy tummana, jokainen vaihe voidaan
   julkaista erikseen ilman että sivu näyttää keskeneräiseltä. Suunta B vaatisi käytännössä
   yhden ison teemanvaihdon.

**Suunta B on varteenotettava, jos Jan haluaa isomman irtioton** ja hyväksyy, että uudistus
tehdään yhtenä isompana kokonaisuutena eikä pieninä paloina.

---

## 7. Layout- ja komponenttisuunnitelma

### 7.1 Etusivun uusi rakenne

```
┌─ header ─ logo · nav (4) · kielivalinta ────────────────────────┐
│  desktop 64 px, mobiili tavoite ≤ 88 px (nyt 139 px)            │
├─ hero (~420 px) ────────────────────────────────────────────────┤
│  vasen: rooli-label · h1 · rooli · 2 lauseen intro · 2 CTA      │
│  oikea: spec-paneeli (6 riviä label/value)                      │
├─ 01 · Julkaistut sovellukset ───────────────────────────────────┤
│  3 × leveä app-row:                                             │
│    ikoni 56px │ nimi + tilamerkki │ 1 lause │ 3 bullettia       │
│                │ tekniikkarivi     │ linkit                     │
│    ────────────────────────────────────────────────             │
│    kuvakaappausnauha (3 kuvaa, ei kehystä)                      │
├─ JanstechApps-kaista (ks. luku 12) ─────────────────────────────┤
├─ 02 · Työn alla ────────────────────────────────────────────────┤
│  2 × kompakti rivi tilamerkinnällä                              │
├─ 03 · Osaaminen ────────────────────────────────────────────────┤
│  Taso 1: 6 kykyä (ikoni + otsikko + 1 rivi)                     │
│  Taso 2: teknologiat ryhmiteltynä tekstinä                      │
│  Taso 3: työtavat                                               │
├─ 04 · Tuotantojärjestelmät (työssäoppimisjakso) ────────────────┤
│  4 × keskikokoinen kortti + PDF-linkit kortin sisällä           │
├─ 05 · Aiemmat toteutukset ──────────────────────────────────────┤
│  2 × tiivis rivi                                                │
├─ 06 · Minusta ──────────────────────────────────────────────────┤
│  max 68ch teksti + lyhyt taustarivi                             │
├─ 07 · Yhteys ───────────────────────────────────────────────────┤
│  yhteystiedot · linkit · CV · JanstechApps                      │
└─ footer ────────────────────────────────────────────────────────┘
```

**Osiot 6 → 7, mutta sivun kokonaiskorkeus laskee** arviolta 7 350 px → ~5 200 px,
koska projektitekstit tiivistetään ja Arkkitehtuuri-osio sulautuu projekteihin.

### 7.2 Uudet / muuttuvat komponentit

| Komponentti | Kuvaus | Korvaa |
|---|---|---|
| `.spec-list` | label/value-parit tabulaarisesti | hero-koodilohko (`.hero-ascii`) |
| `.app-row` | leveä sovellusrivi: ikoni, otsikko, tila, tiiviste, tekniikka, linkit, kuvanauha | 3 × `.project-card` |
| `.status` | tilamerkki: piste + teksti (ei pelkkä väri) | – |
| `.shot-strip` | vaakasuora kuvakaappausnauha, `scroll-snap` mobiilissa | `.project-images` |
| `.capability` | Taso 1 -kyky: otsikko + yksi selittävä rivi | `.skills-grid .card` |
| `.tech-groups` | ryhmitelty teknologialista tekstinä | `.skills-grid .card ul` |
| `.entry` | tiivis projektirivi (ryhmät 2 ja 4) | `.project-card` |
| `.section-num` | osionumero 01–07 | – |
| `.brand-strip` | JanstechApps-kaista | – |
| `.skip-link` | saavutettavuus | puuttuu |

**Säilytetään sellaisenaan:** `.container`, `.site-header`, `.lang-switch`, `.site-footer`,
`setLang()` ja koko i18n-mekanismi, GainsAI-sivun `.shot`-galleria (siitä tulee `.shot-strip`:n pohja).

**Poistetaan:** `.arch-placeholder` (katkoviivalaatikot), `.hero-ascii` (korvautuu `.spec-list`illä),
`.project-images` (korvautuu `.shot-strip`illä).

---

## 8. Väri- ja typografiasuositus

### 8.1 Väritokenit (ehdotus)

```css
:root{
  /* Pinnat – neutraali grafiitti, ei sinimusta */
  --bg:        #0E1013;
  --bg-raised: #15181D;
  --bg-panel:  #1A1E24;
  --line:      #262B33;   /* hiusviiva */
  --line-soft: #1E232A;

  /* Teksti */
  --fg:        #E9EAEC;   /* 15.6:1 vs --bg */
  --fg-muted:  #A2A8B2;   /*  8.1:1 vs --bg */
  --fg-faint:  #767D88;   /*  4.6:1 – vain ei-kriittinen */

  /* Korostus */
  --accent:      #E0A85C;      /* amber, 8.9:1 vs --bg */
  --accent-weak: rgba(224,168,92,.14);
  --on-accent:   #17130C;

  /* Tilat – aina teksti mukana, ei pelkkä väri */
  --ok:      #63B37F;   /* julkaistu   */
  --pending: #C9A227;   /* testaus     */
  --idle:    #8B929C;   /* kehityksessä */
}
```

> Kaikki arvot on **testattava** `--bg`- ja `--bg-panel`-taustoja vasten ennen käyttöönottoa.
> Nykyinen AA-taso ei saa laskea.

### 8.2 Typografia

**Fonttipäätös:** pysytään järjestelmäfonteissa (ei ulkoista latausta, ei privacy-ongelmaa,
ei FOUT) – **mutta monospace korjataan**:

```css
--font-sans: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
--font-mono: ui-monospace, "SF Mono", "Cascadia Mono", "Segoe UI Mono",
             "Roboto Mono", Menlo, Consolas, monospace;
```

`"Fira Code"` poistetaan listalta, koska sitä ei ladata eikä sitä ole tarkoitus ladata.
Nykyinen tilanne lupaa fontin, jota ei ole.

**Tyyppiskaala** (1.28-suhde, `clamp` responsiivisuuteen):

| Rooli | Koko | Line-height | Paino |
|---|---|---|---|
| `h1` | `clamp(2.25rem, 4.5vw, 2.75rem)` | **1.08** | 650 |
| `h2` osio | `clamp(1.5rem, 2.6vw, 1.75rem)` | 1.2 | 650 |
| `h3` kortti | **1.125rem** (18 px) | 1.3 | 600 |
| leipäteksti | **1.0625rem** (17 px) | **1.6** | 400 |
| lista | 1rem (16 px) | 1.55 | 400 |
| meta / label | 0.8125rem (13 px) | 1.4 | 500, mono, +0.02em |

**Mitat:** `--measure: 68ch` leipätekstille, `--shell: 1120px` gridille.
Tämä korjaa nykyisen 138 merkin rivinpituuden.

### 8.3 Muotokieli

| Token | Arvo | Nyt |
|---|---|---|
| `--r-sm` | 6 px | – |
| `--r-md` | 10 px | 5 / 10 / 14 px sekaisin |
| `--r-pill` | 999 px (vain tilamerkit ja kielivalinta) | 999 px |
| Varjot | **Poistetaan lähes kokonaan**, tilalle `1px solid var(--line)` | `0 18px 45px rgba(0,0,0,.65)` joka kortissa |
| Spacing | 4 px -pohjainen: 4/8/12/16/24/32/48/64/96 | ad hoc rem-arvot |

---

## 9. Vaiheistettu toteutussuunnitelma

> Jokainen vaihe on itsenäisesti julkaisukelpoinen ja peruutettavissa yhdellä revertillä.

### Vaihe 0 – Korjaukset (suunnasta riippumaton)

| | |
|---|---|
| **Tavoite** | Korjata todennetut viat, jotka pitää korjata joka tapauksessa – riippumatta siitä, mikä visuaalinen suunta valitaan |
| **Sisältö** | (1) SEO-metatiedot `index.html`:ään: description, canonical, OG, Twitter, robots · (2) CV-prefetchin tiedostonimi `Jan_Sarivuo_cv.pdf` · (3) `images/favicon.png` 520 KB → ≤ 15 KB · (4) `scroll-margin-top` osioille · (5) headerin gradientti umpinaiseksi · (6) `width`/`height` + `loading="lazy"` 10 kuvalle · (7) 4 PDF-prefetchin poisto · (8) `placeholder-architecture.png` (981 KB) poisto · (9) skip-link + `<nav aria-label>` · (10) `:focus-visible`-tyyli |
| **Tiedostot** | `index.html`, `css/style.css`, `images/favicon.png`, `images/placeholder-architecture.png` (poisto) |
| **Riskit** | Hyvin matalat. Kohta 8 on tiedoston poisto → vaatii Janin hyväksynnän (AGENTS.md) |
| **Validointi** | Lighthouse ennen/jälkeen, kuvapainon mittaus, ankkurilinkkien klikkaus, `git diff --check` |
| **Commit** | `Fix portfolio metadata, asset weight and anchor offsets` |

**Arvioitu vaikutus:** kuvapaino 2 437 KB → ~700 KB ensilatauksella, +SEO-metatiedot,
–1 kpl 404-pyyntö per sivulataus.

### Vaihe 1 – Perusta (tokenit)

| | |
|---|---|
| **Tavoite** | Uusi tokenisto käyttöön ilman rakennemuutoksia. Sivu näyttää samalta rakenteeltaan mutta uudelta väriltään ja typografialtaan |
| **Sisältö** | `:root`-tokenit (värit, tyyppiskaala, spacing, radii, `--measure`), `--font-mono`-korjaus, painike- ja linkkityylit, focus-tilat, varjot → hiusviivat |
| **Tiedostot** | `css/style.css` (ylin kolmannes), `index.html` ja `gainsai/index.html` inline-`<style>`-lohkot |
| **Riskit** | **Suurin riski koko projektissa:** `css/style.css` on jaettu → muutos vaikuttaa myös GainsAI-sivuun. Molemmat sivut on tarkistettava jokaisen muutoksen jälkeen |
| **Validointi** | Kontrastimittaus kaikille tekstipareille (AA ei saa laskea), 5 leveyttä × 2 kieltä × 2 sivua, ei overflowta |
| **Commit** | `Introduce portfolio design tokens and type scale` |

### Vaihe 2 – Header ja hero

| | |
|---|---|
| **Tavoite** | Todistusaineisto taitteen yläpuolelle, mobiiliheaderin kutistus |
| **Sisältö** | Header 139 px → ≤ 88 px mobiilissa · `.spec-list` korvaa `.hero-ascii` · uusi hero-copy FI/EN (luku 13) · CTA-tekstit |
| **Tiedostot** | `index.html` (hero-lohko + `dict` fi/en), `css/style.css` |
| **Riskit** | Uudet i18n-avaimet – FI/EN-pariteetti tarkistettava. Vanhat avaimet (`hero_text`, `hero_code`) poistuvat → poistettava molemmista sanakirjoista |
| **Validointi** | i18n-avainten kattavuusskripti, mobiiliheaderin korkeus, spec-paneelin rivitys suomeksi |
| **Commit** | `Rebuild portfolio hero around verifiable production work` |

### Vaihe 3 – Projektihierarkia

| | |
|---|---|
| **Tavoite** | 10 tasapaksusta kortista neljä eriarvoista ryhmää |
| **Sisältö** | `.app-row` × 3 julkaistulle sovellukselle (ikonit `apps/images/`-hakemistosta) · `.status`-merkinnät · SureKeep + Työtori omana "työn alla" -ryhmänä · työssäoppimisjakson 4 korttia yhden otsikon alle · Arkkitehtuuri-osion PDF:t projektien sisään · IT-huolto pois projekteista · projektitekstien tiivistys 3 bullettiin |
| **Tiedostot** | `index.html` (koko `#projects` + `#architecture`), `css/style.css`, ehkä uudet ikonikopiot `images/`-hakemistoon |
| **Riskit** | **Suurin sisältöriski.** Poistetaan/siirretään olemassa olevaa sisältöä → vaatii Janin hyväksynnän per kohta (AGENTS.md: "Do not remove a project without explicit approval"). Kaikki nykyiset linkit säilytettävä |
| **Validointi** | Linkkiskannaus (kaikki 42 linkkiä), kuvasuhteet, i18n-pariteetti, ei rikkinäisiä ankkureita |
| **Commit** | Jaetaan 2–3 committiin: `Group published applications into a dedicated section` · `Consolidate work-placement projects` · `Add in-development applications` |

### Vaihe 4 – Osaaminen, JanstechApps, Minusta, Yhteys

| | |
|---|---|
| **Tavoite** | Osaaminen kolmitasoiseksi, brändi näkyviin, tekstit 68ch-rataan |
| **Sisältö** | `.capability` / `.tech-groups` / työtavat · `.brand-strip` (luku 12) · Minusta-osion mitta ja tiivistys · yhteystiedot |
| **Tiedostot** | `index.html`, `css/style.css` |
| **Riskit** | Matalat. Osaamisen uudelleenryhmittely muuttaa 33 bullettia → sisältö säilytettävä, vain järjestys ja painotus muuttuu |
| **Validointi** | Rivinpituusmittaus (≤ 70ch), FI/EN-korttien korkeuserot |
| **Commit** | `Restructure skills by production capability` · `Add JanstechApps brand section` |

### Vaihe 5 – Projektisivut

| | |
|---|---|
| **Tavoite** | GainsAI-sivu uuteen ilmeeseen; malli tuleville projektisivuille |
| **Sisältö** | `gainsai/index.html` inline-`<style>` → jaettuun CSS:ään · `.shot-strip` · sivukohtaiset tyylit karsitaan |
| **Tiedostot** | `gainsai/index.html`, `css/style.css` |
| **Riskit** | Matalat, sivu on tuore ja hyvin rakennettu |
| **Validointi** | Sama QA kuin etusivulle |
| **Commit** | `Align GainsAI project page with the new design system` |

### Vaihe 6 – Viimeistely ja QA

| | |
|---|---|
| **Tavoite** | Mikrointeraktiot, saavutettavuus, suorituskyky, SEO |
| **Sisältö** | `prefers-reduced-motion` · kosketuskohteet ≥ 44 px · Lighthouse · sitemap · OG-kuva etusivulle (puuttuu) |
| **Tiedostot** | `css/style.css`, `index.html`, `sitemap.xml` |
| **Riskit** | Matalat |
| **Validointi** | Koko luvun 11 QA-suunnitelma |
| **Commit** | `Polish responsive behaviour and accessibility` |

---

## 10. Tiedostokohtainen muutoslista

### `index.html`

| Kohta | Muutos | Vaihe |
|---|---|---|
| `<head>` rivit 6–9 | Poista 4 PDF-prefetchiä; korjaa CV:n tiedostonimi jos prefetch säilytetään | 0 |
| `<head>` | **Lisää:** meta description, canonical, robots, OG (title/description/image/url/type/locale), Twitter-kortti | 0 |
| `<head>` inline `<style>` (rivit 19–67) | Siirrä `.lang-switch`-tyylit `css/style.css`:ään; poista duplikaatti | 1 |
| `<body>` alku | Lisää `.skip-link` | 0 |
| `.site-header` | `<nav aria-label>`; mobiilikorkeus | 0 / 2 |
| `.hero-inner` | `.hero-ascii` → `.spec-list`; uusi copy | 2 |
| `#about` | Siirrä osion loppuun; mitta 68ch; poista päällekkäisyys heron kanssa | 4 |
| `#skills` | 7 korttia → 3 tasoa | 4 |
| `#projects` | 10 korttia → 4 ryhmää; `.app-row`; tilamerkit; ikonit | 3 |
| `#architecture` | Poista omana osionaan; PDF:t projektikorttien sisään | 3 |
| `#contact` | JanstechApps-linkki listaan | 4 |
| `<script>` `dict` | Uudet avaimet FI+EN; poista käytöstä poistuvat (`hero_text`, `hero_code`, `proj_it_*`, `arch_card_*`) | 2–4 |
| `setLang()` | **Ei muutoksia.** Mekanismi on kunnossa | – |
| Kuvat | `width`/`height`/`loading="lazy"` 10 kuvalle | 0 |

### `css/style.css`

| Kohta | Muutos | Vaihe |
|---|---|---|
| `:root` (rivit 11–24) | **Korvaa kokonaan** uudella tokenistolla (luku 8) | 1 |
| `body` | Radial-gradient → tasainen `--bg` + valinnainen hyvin hienovarainen ylägradientti | 1 |
| `.container` | `--shell: 1120px`; lisää `.measure`-apuluokka (68ch) | 1 |
| `.section` | Vaihteleva padding-rytmi identtisen 4.5rem sijaan | 1 |
| `.section-alt` | Säilytä, mutta ero pintasävynä (`--bg-raised`) gradientin sijaan | 1 |
| `.site-header` (72–84) | Gradientti → umpinainen tausta + alaraja; korkeus | 0 |
| `.nav` | Mono → sans; koko 15 px | 1 |
| `.lang-switch` | Yhdistä `index.html`:n ja `gainsai/index.html`:n inline-versiot tänne | 1 |
| `.hero-*` | Uudelleenkirjoitus; `.hero-ascii` poistuu | 2 |
| `.btn-primary` / `.btn-ghost` | Mono → sans; radius 999 px → 8 px; korkeus ≥ 44 px | 1 |
| `.card` | Varjo → `1px solid var(--line)`; radius 14 → 10 px | 1 |
| `.project-card`, `.project-images`, `.project-*` | Korvataan `.app-row` / `.entry` / `.shot-strip` -komponenteilla | 3 |
| `.skills-grid` | Korvataan `.capability` + `.tech-groups` | 4 |
| `.arch-placeholder`, `.arch-card` | **Poistetaan** | 3 |
| Lopun media queryt (513–569) | Kirjoitetaan uudelleen uuden rakenteen mukaan | 1–4 |
| **Uutta** | `:focus-visible`, `.skip-link`, `.status`, `.spec-list`, `.section-num`, `.brand-strip`, `prefers-reduced-motion` | 0–6 |

### `gainsai/index.html`

| Kohta | Muutos | Vaihe |
|---|---|---|
| Inline `<style>` (~150 riviä) | Siirrä jaettuun CSS:ään; jätä sivulle vain aidosti sivukohtainen | 5 |
| `.shot-grid` | → `.shot-strip` | 5 |
| Meta/OG | **Ei muutoksia**, on jo kunnossa | – |

### `apps/index.html` ja `apps/css/style.css`

Ks. luku 12. **Vaatii erillisen päätöksen** – ei kuulu tähän uudistukseen.

### Uudet tiedostot

| Tiedosto | Perustelu |
|---|---|
| `images/og-portfolio.png` (1200×630) | Etusivulta puuttuu OG-kuva kokonaan |
| `images/favicon-*.png` uudelleen | Nykyinen `favicon.png` on 520 KB |
| `images/icon-kauppalista.png`, `-waveiq.png` | App-rivien ikonit (kopiot `apps/images/`-hakemistosta, optimoituina) |
| `docs/portfolio-redesign-audit.md` | Tämä dokumentti |

**Ei uusia CSS- tai JS-tiedostoja.** Yksi jaettu `css/style.css` riittää; useampi tiedosto lisäisi
pyyntöjä ilman hyötyä tämän kokoisella sivustolla.

### Miten vältetään kertarysäys

1. Vaihe 0 ensin – se ei riipu mistään suunnasta ja tuottaa mitattavan hyödyn heti.
2. Vaihe 1 muuttaa **vain tokenit**, ei rakennetta → jos ilme ei miellytä, revert on yksi commit.
3. Vaiheet 2–5 koskevat kukin yhtä osiota kerrallaan.
4. Jokaisen vaiheen jälkeen ajetaan sama QA-skripti (luku 11).
5. Ei yhtäkään committia, joka koskee sekä tokeneita että rakennetta.

---

## 11. Riskit

| # | Riski | Todennäköisyys | Vaikutus | Hallinta |
|---|---|---|---|---|
| 1 | `css/style.css` on jaettu → etusivun muutos rikkoo GainsAI-sivun | **Korkea** | Korkea | Molemmat sivut jokaisessa QA-ajossa; ei koskaan muuteta jaettua tyyliä tarkistamatta molempia |
| 2 | Kontrastitaso laskee uuden paletin myötä | Keskisuuri | Korkea (saavutettavuus) | Automaattinen kontrastimittaus jokaisen tokenimuutoksen jälkeen; AA on ehdoton alaraja |
| 3 | i18n-avaimia jää orvoiksi tai puuttumaan rakennemuutoksissa | **Korkea** | Keskisuuri | Avainkattavuusskripti pakollisena jokaisessa vaiheessa |
| 4 | Sisällön tiivistäminen poistaa jotain, minkä Jan haluaa säilyttää | Keskisuuri | Keskisuuri | Ei poisteta mitään ilman hyväksyntää; kaikki tiivistetty teksti siirretään projektisivulle, ei roskiin |
| 5 | Amber-korostus näyttää halvalta jos sitä käytetään liikaa | Keskisuuri | Keskisuuri | Korostusväri rajataan: CTA:t, aktiiviset tilat, otsikkoviivat. Ei ikoneille, ei reunoille |
| 6 | Uudistus alkaa muistuttaa janstechapps.comia | Matala | Keskisuuri | Vertailukuvat rinnakkain jokaisen vaiheen jälkeen |
| 7 | Mono-fontin vaihto muuttaa leveyksiä yllättävästi | Keskisuuri | Matala | Mono rajataan metadataan; leveydet mitataan 360 px:llä |
| 8 | `git diff --check` ilmoittaa "trailing whitespace" `index.html`:ssä | **Varma** | Ei mitään | **Tunnettu, ei korjattavaa:** tiedosto on tallennettu gitiin CRLF-päätteillä, joten *jokainen* lisätty rivi merkitään. Sama toistuu koko historiassa (esim. `9f2de75`: 9 lisättyä riviä → 9 havaintoa). Tarkistetaan sen sijaan, ettei aitoa rivinloppuista välilyöntiä ole: `git diff -U0 \| grep '^+' \| sed 's/\r$//' \| grep -E '[ \t]+$'` |
| 9 | Vanhat URLit rikkoutuvat | Matala | Korkea | `#about`, `#skills`, `#projects`, `#architecture`, `#contact` säilytetään ankkureina vaikka osiot ryhmittyisivät uudelleen |

---

## 12. JanstechApps.com portfoliossa

### 12.1 Lähtökohta

Sivustoilla on eri tehtävä, ja se on säilytettävä:

- **janstech.github.io** – *Jan Sarivuo kehittäjänä.* Osaaminen, tekniset ratkaisut, työtapa, CV.
  Yleisö: työnantajat, rekrytoijat, yhteistyökumppanit.
- **janstechapps.com** – *Julkaistut sovellukset tuotteina.* Esittely, hinnat, legal-sivut, tuki.
  Yleisö: sovellusten käyttäjät.

Nykyisin portfolio **ei mainitse JanstechAppsia kertaakaan**. Se on menetetty tilaisuus: brändi on
konkreettinen todiste itsenäisestä sovellusliiketoiminnasta – ei vain "harrasteprojekteja",
vaan julkaistuja tuotteita, joilla on tietosuojasivut, tukikanava ja tilausmalli.

### 12.2 Suositus: kolme kosketuspistettä, kaikki kevyitä

**1. Ensisijainen – kaista heti julkaistujen sovellusten jälkeen**

Sijoitus on tässä olennainen: kaista tulee **kun kävijä on juuri nähnyt kolme sovellusta** ja
kysyy luonnostaan "missä nämä ovat tuotteina?". Ei heron alle, ei omaksi isoksi osiokseen.

Toteutus: **yksi vaakakaista, ei korttiruudukko.** Vasemmalla 2–3 riviä tekstiä, oikealla
yksi CTA. Ei logolockuppia, ei sovellusikoneita (ne näkyivät juuri yllä), ei taustakuvaa.
Korkeus ~140 px. Erottuu ympäristöstään pintasävyllä (`--bg-raised`), ei kehyksellä.

**2. Toissijainen – yksi rivi heron spec-paneelissa**

Spec-paneelin viimeinen rivi: `Julkaisut · JanstechApps → janstechapps.com`.
Tämä on koko brändinosto herossa. **Ei logoa, ei brändiväriä, ei erillistä lohkoa** – muuten
portfolio alkaa näyttää yrityksen etusivulta.

**3. Kolmas – yhteystiedot ja footer**

Rivi `#contact`-osion linkkilistaan, GitHubin ja LinkedInin rinnalle. Sekä yksi rivi footeriin.

### 12.3 Mitä ei kannata tehdä

| Ei | Miksi |
|---|---|
| JanstechApps-logo headeriin tai brändilockup heroon | Portfoliosta tulee yrityssivu; sekoittaa henkilön ja brändin |
| Oma "Tuotteemme" -ruudukko sovelluskorteilla | Duplikoi sekä oman projektiosion että janstechapps.comin |
| janstechapps.comin visuaalisen ilmeen kopiointi | Sivustot sulautuisivat yhdeksi; kumpikin menettäisi tunnistettavuutensa |
| Me-muoto ("Rakennamme sovelluksia…") | Jan on yksi kehittäjä; monikko kuulostaa keksityltä |
| Liiketoimintaväitteet (asiakasmäärät, liikevaihto) | AGENTS.md kieltää; ei todennettavissa |

### 12.4 Ehdotetut tekstit

**Kaista – otsikko**
- FI: `JanstechApps – julkaistut sovellukseni`
- EN: `JanstechApps — where my apps live`

**Kaista – leipäteksti**
- FI: *"Julkaisen sovellukseni omalla JanstechApps-nimellä. Saman katon alta löytyvät
  sovellusten esittelyt, tietosuojaselosteet, käyttöehdot ja tuki. Vastaan itse koko ketjusta:
  suunnittelusta ja toteutuksesta julkaisuun, ylläpitoon ja käyttäjätukeen."*
- EN: *"I publish my applications under my own JanstechApps name. The site brings together the
  app pages, privacy policies, terms and support in one place. I handle the whole chain myself —
  design and development, release, maintenance and user support."*

**Kaista – CTA**
- FI: `Siirry JanstechApps.comiin →` (`aria-label`: `Avaa JanstechApps.com uudessa välilehdessä`)
- EN: `Visit JanstechApps.com →` (`aria-label`: `Open JanstechApps.com in a new tab`)

**Hero-spec-rivi**
- FI: label `Julkaisut` / value `JanstechApps`
- EN: label `Published under` / value `JanstechApps`

**Yhteystietolinkki**
- FI: `JanstechApps – julkaistut sovellukset`
- EN: `JanstechApps — published applications`

**Footer**
- FI: `Sovellukset: janstechapps.com`
- EN: `Apps: janstechapps.com`

Kaikki ulkoiset linkit: `target="_blank" rel="noopener noreferrer"`.

### 12.5 `apps/index.html` – erillinen päätös

`janstech.github.io/apps/` on **käytännössä janstechapps.comin varhaisempi versio**: sama
sovelluslistaus, oma CSS, oma i18n-sanakirja. Lisäksi siinä on **8 linkkiä repoihin, joita ei ole
tässä reposssa** (`../kauppalista-privacy-policy/`, `../waveiq-radio-privacy-policy/` alasivuineen).
En pystynyt varmentamaan niitä tuotannosta – verkkoyhteys on tässä ympäristössä estetty.

Kolme vaihtoehtoa, **Janin päätettäväksi** (ei toteuteta ilman hyväksyntää):

| Vaihtoehto | Sisältö | Arvio |
|---|---|---|
| **A. Silta** *(suositus)* | Säilytä URL, korvaa sisältö lyhyellä sivulla, joka ohjaa janstechapps.comiin ja portfolion projektiosioon | Ei riko olemassa olevia linkkejä, poistaa duplikaatin ja rikkinäiset legal-linkit, poistaa toisen i18n-sanakirjan ylläpidon |
| B. Korjaa | Päivitä legal-linkit osoittamaan `janstechapps.com/legal/*`, päivitä ilme | Jää silti duplikaatiksi ja toiseksi ylläpidettäväksi ilmeeksi |
| C. Ennallaan | Ei tehdä mitään | Rikkinäiset linkit jäävät, mutta riski on nolla |

---

## 13. Ehdotetut FI/EN-sisältöparannukset

> **Ehdotuksia, ei toteutettuja muutoksia.** Mitään tekstiä ei ole korvattu tiedostoissa.

### 13.1 Hero

**Rooli-label (h1:n yläpuolella)**
- FI: `Ohjelmistokehittäjä · Android & backend`
- EN: `Software developer · Android & backend`

**h1** – `Jan Sarivuo` (ei muutosta)

**Roolikuvaus (h2)**
- FI: `Rakennan sovelluksia käyttöliittymästä palvelimeen asti`
- EN: `I build applications from the interface to the server`

> **"Junior"-kysymys:** nykyisin sana esiintyy kahdesti taitteen yläpuolella. Ehdotus on siirtää se
> pois heron pääviestistä Minusta- ja Yhteys-osioihin, joissa se on relevantti
> (*"Haen junior-tason tehtäviä…"*). Otsikko `Ohjelmistokehittäjä` on tarkka ja totuudenmukainen:
> hän on valmistunut, julkaissut kolme sovellusta ja ylläpitää niiden backendejä.
> **Tämä on Janin päätös** – vaihtoehtona `Junior-ohjelmistokehittäjä · Android & backend`.

**Intro (2 lausetta nykyisen 8 rivin sijaan)**
- FI: *"Rakennan sovelluksia kokonaisuutena: Android-käyttöliittymästä FastAPI-backendiin,
  tietokantaan ja palvelimelle asti. Kolme sovellustani on julkaistu Google Playssa, ja ylläpidän
  niiden taustapalvelut itse."*
- EN: *"I build software end to end — from the Android interface to the FastAPI backend, the
  database, and the server it runs on. Three of my applications are published on Google Play, and
  I run the backends behind them myself."*

**Spec-paneeli (korvaa koodilohkon)**

| Label FI | Label EN | Arvo |
|---|---|---|
| Sovellukset | Applications | 3 julkaistua Google Playssa / 3 published on Google Play |
| Android | Android | Kotlin · Jetpack Compose · Material 3 |
| Backend | Backend | FastAPI · Python · MariaDB |
| Tunnistus | Authentication | Firebase Auth · App Check · Play Integrity |
| Maksut | Payments | Google Play Billing |
| Infra | Infrastructure | Linux · Hetzner · varmuuskopiointi / backups |
| Julkaisut | Published under | JanstechApps |

**CTA:t**
- FI: `Julkaistut sovellukset` (ensisijainen) · `Ota yhteyttä` (toissijainen)
- EN: `Published applications` · `Get in touch`

### 13.2 Osioiden otsikot

| Osio | FI | EN |
|---|---|---|
| 01 | `Julkaistut sovellukset` | `Published applications` |
| 02 | `Työn alla` | `In development` |
| 03 | `Osaaminen` | `What I do` |
| 04 | `Tuotantojärjestelmät` | `Production systems` |
| 05 | `Aiemmat toteutukset` | `Earlier work` |
| 06 | `Minusta` | `About` |
| 07 | `Yhteys` | `Contact` |

### 13.3 Sovellusten kärkilauseet (poistavat nykyisen toiston)

**GainsAI**
- FI: *"Tekoälyavusteinen kuntosalisovellus, jossa on oma backend, tilausmaksut ja
  pilvivarmuuskopiointi."*
- EN: *"AI-assisted gym training app with its own backend, subscription billing and cloud backup."*

**Kauppalista & Muistiinpanot**
- FI: *"Yksityisyys edellä rakennettu ostoslista, joka toimii ilman kirjautumista ja offline-tilassa
  – valinnaisilla AI-toiminnoilla."*
- EN: *"A privacy-first shopping list that works offline and without an account, with optional
  AI features on top."*

**WaveIQ Radio**
- FI: *"Internet-radio, joka oppii kuunteluhistoriasta ja selittää, miksi se suosittelee tiettyä
  asemaa."*
- EN: *"An internet radio app that learns from listening history and explains why it recommends
  a station."*

### 13.4 Tilamerkinnät

| Tila | FI | EN |
|---|---|---|
| Julkaistu | `Julkaistu Google Playssa` | `Published on Google Play` |
| Testaus | `Suljettu testaus` | `Closed testing` |
| Kehityksessä | `Kehityksessä` | `In development` |
| Tuotantokäytössä | `Tuotantokäytössä` | `Running in production` |

### 13.5 Osaamisen Taso 1 -kyvyt

| FI | EN |
|---|---|
| Android-sovellukset tuotantoon asti | Android apps all the way to production |
| Omat FastAPI-backendit ja REST-rajapinnat | My own FastAPI backends and REST APIs |
| MariaDB/MySQL: suunnittelu, migraatiot, palautukset | MariaDB/MySQL: design, migrations, restores |
| Tunnistautuminen ja sovelluksen eheys | Authentication and app integrity |
| Tilausmaksut ja palvelinvarmennus | Subscription billing and server-side verification |
| Linux-tuotantoympäristöt ja varmuuskopiointi | Linux production environments and backups |

### 13.6 Työtapa (uusi, Taso 3) – nyt lähes näkymätön vahvuus

- FI: *"Kirjoitan arkkitehtuuridokumentit ja päätöskirjaukset työn rinnalla, ajan release-portit
  ja regressiomatriisit ennen julkaisua ja pidän dokumentaation koodin tahdissa."*
- EN: *"I write architecture documents and decision records alongside the work, run release gates
  and regression matrices before shipping, and keep the documentation in step with the code."*

### 13.7 Kaksikielisyyden layout-huomiot

| Havainto | Vaikutus suunnitteluun |
|---|---|
| Suomi on 10–20 % pidempää | Painikkeille `min-width`, ei kiinteää leveyttä |
| Yhdyssanat: `Palvelinympäristöt`, `varmuuskopiointi`, `harjoitusohjelmat` | `hyphens: auto` + `lang`-attribuutti; testattava 360 px:llä |
| `Ohjelmistokehittäjä` (19 merkkiä) vs `Software developer` (18) | Rooli-label mahtuu molemmilla |
| Spec-paneelin labelit: `Tunnistus` / `Authentication` | Label-sarakkeelle kiinteä leveys, arvo rivittyy |
| Osioiden otsikot eri pituisia | Numeroitu prefiksi (`01 ·`) vakauttaa vasemman reunan |
| Nykyinen mekanismi | **Ei muutoksia.** `data-i18n` + `dict` + `portfolio_lang` riittää; erillisiä FI/EN-sivustoja ei tarvita eikä suositella |

---

## 14. Validointisuunnitelma

Sama sarja ajetaan **jokaisen vaiheen jälkeen**. Playwright + Chromium on jo käytettävissä
scratchpad-hakemistossa (ei repossa, ei riippuvuutena).

### 14.1 Automaattinen

| # | Tarkistus | Kynnys |
|---|---|---|
| 1 | Leveydet 360 / 390 / 768 / 1024 / 1440 px × sivut `/`, `/gainsai/` | Ei vaakasuuntaista overflowta |
| 2 | Sama × kielet FI/EN | Ei leikkautuvaa tekstiä (`overflow:hidden` + `scrollWidth > clientWidth`) |
| 3 | Konsolivirheet ja epäonnistuneet pyynnöt | 0 uutta |
| 4 | Kuvasuhteet vs. `naturalWidth/Height` | Poikkeama < 2 % |
| 5 | Kontrasti kaikille tekstiväri/tausta-pareille | **AA (4.5:1 / 3:1) ei saa laskea** |
| 6 | i18n: puuttuvat avaimet, orvot avaimet, FI/EN-pariteetti | 0 poikkeamaa |
| 7 | Kielenvaihto: FI→EN→sivunvaihto→FI, `<html lang>`, `document.title`, `aria-pressed`, alt-tekstit | Kaikki vaihtuvat |
| 8 | Paikalliset linkit ja kuvapolut | 0 rikkinäistä |
| 9 | Ankkurit vs. `id`:t (myös sivujen väliset) | 0 puuttuvaa |
| 10 | HTML-rakenne: sulkemattomat/väärin sisäkkäiset tagit, `<h1>`-määrä, otsikkojärjestys | 0 virhettä, 1 × `h1` |
| 11 | Kuvapaino per sivu | `/` alle 900 KB |
| 12 | `sitemap.xml` jäsentyy, ei duplikaatteja, canonical-vastaavuus | OK |
| 13 | Salaisuusskannaus lisätyistä riveistä | 0 osumaa |
| 14 | `git diff --check` + aidon rivinloppuisen välilyönnin tarkistus | 0 aitoa havaintoa (ks. riski 8) |

### 14.2 Manuaalinen

| # | Tarkistus |
|---|---|
| 15 | Näppäimistökierros: Tab koko sivun läpi, focus näkyy joka askeleella, skip-link toimii |
| 16 | `prefers-reduced-motion: reduce` – sivu käytettävissä ilman animaatioita |
| 17 | Kosketuskohteet ≥ 44 × 44 px (kielivalinta, CTA:t, kuvalinkit) |
| 18 | Firefox-tarkistus (Chromium-testien lisäksi) – erityisesti `backdrop-filter`, `clamp()`, `hyphens` |
| 19 | Silmämääräinen vertailu janstechapps.comin rinnalla – erottuvatko sivustot |
| 20 | Lighthouse: Performance / Accessibility / Best Practices / SEO, ennen ja jälkeen |

### 14.3 Tunnetut validoinnin rajoitteet

- **Ulkoisia URLeja ei voi varmentaa tässä ympäristössä.** Verkkopyynnöt palauttivat `000`
  (esim. `janstechapps.com`, `play.google.com`). Ulkoisten linkkien toimivuus on tarkistettava
  selaimessa manuaalisesti.
- Lighthouse ajetaan paikallista staattista palvelinta vasten, ei GitHub Pagesia vasten →
  verkkoviive ja välimuistiotsakkeet poikkeavat tuotannosta.
- Firefox- ja Safari-testaus on manuaalista; automaatio kattaa Chromiumin.

---

## 15. Päätös: mitä tehdään ensin

### Suositus

**Aloita Vaiheesta 0 (korjaukset) heti** – se ei riipu siitä, mikä visuaalinen suunta valitaan.

Perustelut:

1. Se korjaa **todennettuja vikoja**, ei makuasioita: puuttuvat SEO-metatiedot, 404:ää tuottava
   prefetch, 520 KB:n favicon, 981 KB:n käyttämätön kuva, laiskasti lataamattomat kuvat.
2. Se on **matalariskisin** muutos koko projektissa – ei mitään, mikä voisi näyttää huonolta.
3. Se **hyödyttää sivustoa vaikka uudistus viivästyisi** tai suunta vaihtuisi.
4. Se tuottaa **mitattavan tuloksen** (Lighthouse ennen/jälkeen), joka kertoo QA-putken toimivan
   ennen kuin sillä validoidaan isompia muutoksia.

Arvioitu vaikutus: kuvapaino ~2 437 KB → ~700 KB, SEO-metatiedot etusivulle, yksi 404 vähemmän
jokaisella latauksella, ankkurinavigaatio toimivaksi.

### Ennen Vaihetta 1 tarvitaan Janin päätökset

| # | Päätös | Vaihtoehdot |
|---|---|---|
| 1 | **Visuaalinen suunta** | A "Työpöytä" *(suositus)* / B "Tekninen lehti" / C "Kenttämuistiinpano" |
| 2 | **Korostusväri**, jos A | Amber `#E0A85C` *(suositus)* / vaimennettu teal / muu |
| 3 | **"Junior" otsikossa** | Pois otsikosta, säilyy Minusta- ja Yhteys-osioissa *(suositus)* / säilyy otsikossa |
| 4 | **SureKeep ja Työtori portfolioon** | Kyllä, "Työn alla" -ryhmänä *(suositus)* / ei vielä |
| 5 | **IT-laitteiden huolto pois projekteista** | Siirretään Minusta-osioon *(suositus)* / säilyy projektikorttina |
| 6 | **Arkkitehtuuri-osion PDF:t projektien sisään** | Kyllä *(suositus)* / oma osio säilyy |
| 7 | **`placeholder-architecture.png` poisto** (981 KB, ei käytössä) | Poistetaan *(suositus)* / säilytetään |
| 8 | **`apps/index.html`** | A silta *(suositus)* / B korjataan / C ennallaan |

### Mitä ei tehdä

- Ei frameworkia. Ei build-järjestelmää. Ei CSS-kirjastoa.
- Ei erillisiä FI/EN-sivustoja.
- Ei i18n-mekanismin korvaamista.
- Ei kaiken kerralla uudelleenkirjoittamista.
- Ei projektien poistamista ilman Janin hyväksyntää.
- Ei GitHubiin pushaamista.

---

## Liite: mittausmenetelmät

Kaikki tämän dokumentin numerot on mitattu, ei arvioitu.

| Mittaus | Menetelmä |
|---|---|
| Sivun korkeudet, osioiden korkeudet, paddingit | Playwright + `getBoundingClientRect()` / `getComputedStyle()`, Chromium 1440×900 ja 390×844 |
| Typografia | `getComputedStyle()` renderöidyistä elementeistä |
| Kontrastisuhteet | WCAG 2.1 -relatiivinen luminanssi tekstiväristä ja lähimmästä läpinäkymättömästä taustasta |
| Rivinpituus | Elementin leveys / (fonttikoko × 0.5) |
| Kuvapainot | Tiedostojärjestelmä + HTML-referenssiskannaus |
| Fonttien lataus | `document.fonts.size`, `getComputedStyle().fontFamily` |
| Tiedostonimien kirjainkoko | `git ls-files` (Windowsin tiedostojärjestelmä ei paljasta tätä) |
| Projektien julkaisutila | Lähderepojen dokumentaatio ja `build.gradle.kts` |
| Käyttämättömät kuvat | Kaikkien HTML-tiedostojen `src`/`href`-referenssien vertailu hakemistolistaukseen |
