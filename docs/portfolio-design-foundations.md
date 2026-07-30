# Portfolion visuaalinen perusta ja design tokenit

**Vaihe:** 1 – visuaalinen perusta (auditointidokumentin vaiheistuksen mukaan)
**Lähde:** `docs/portfolio-redesign-audit.md`
**Toteutus:** `css/style.css` (`:root`-lohko + migroidut säännöt)

Tämä dokumentti on token-järjestelmän ylläpidettävä lähde: se kertoo *miksi* arvot
ovat mitä ovat. Varsinaiset arvot elävät CSS:ssä – tänne ei kopioida koko
tyylitiedostoa.

---

## 1. Valittu suunta: "Työpöytä" (Workbench)

Hyvin konfiguroidun työaseman rauha. Tumma, mutta **rakenteellinen**.

| Periaate | Käytännössä |
|---|---|
| Neutraali grafiitti, ei sinimusta | `--color-bg: #0e1013` – harmaa-, ei sinipainotteinen |
| Hillitty amber-korostus | `--color-accent: #e0a85c` – lämmin, ei neonoranssi eikä kulta |
| Litteät pinnat ja hiusviivat | Kortit: 1 px reuna, **ei varjoa** |
| Vähemmän kelluvia kortteja | `--shadow-soft` (0 18px 45px) poistettu käytöstä |
| Mono vain tekniseen metadataan | Nav, painikkeet ja logo siirtyivät sans-fonttiin |
| Ei AI-portfolion kliseitä | Ei neon-gradientteja, ei hehkuvia reunoja, ei lasikortteja |

**Korostusta käytetään vain:** CTA-painikkeissa, tärkeissä linkeissä, aktiivisessa
kielivalinnassa, fokusrenkaassa, osio-otsikon alleviivauksessa, hero-labelissa ja
luettelomerkeissä. **Ei** otsikoissa, ei reunoissa, ei taustoissa.

---

## 2. Väripaletti

### Pinnat

| Token | Arvo | Käyttö |
|---|---|---|
| `--color-bg` | `#0e1013` | Sivun perustausta |
| `--color-bg-alt` | `#121519` | Vuorotteleva osio (`.section-alt`) |
| `--color-surface` | `#16191e` | Kortit ja paneelit |
| `--color-surface-raised` | `#1c2027` | Hover-tila |
| `--color-surface-subtle` | `#111418` | Koodilohko, footer, arkkitehtuuripaikka |

### Reunat

| Token | Arvo | Kontrasti taustaa vasten | Käyttö |
|---|---|---|---|
| `--color-border` | `#2e3540` | 1.54:1 | Hiusviiva pintojen väliin (koristeellinen) |
| `--color-border-strong` | `#5e697b` | **3.43:1** | Kontrollien reuna – täyttää WCAG 1.4.11 |

### Teksti

| Token | Arvo | vs. `--color-bg` | vs. `--color-surface-raised` |
|---|---|---|---|
| `--color-text` | `#e9eaec` | 15.83:1 | 14.0:1 |
| `--color-text-secondary` | `#b4bac3` | 9.76:1 | 8.37:1 |
| `--color-text-muted` | `#a3abb8` | 8.23:1 | **7.06:1** |

> Vaimein sävy pidetään yli 7:1:n myös nostetulla pinnalla, jotta Vaihe 0:n
> mitattu taso (7.03:1) ei heikkene.

### Korostus ja tilat

| Token | Arvo | Kontrasti |
|---|---|---|
| `--color-accent` | `#e0a85c` | 9.00:1 taustaa vasten |
| `--color-accent-hover` | `#efbe7c` | 10.34:1 |
| `--color-accent-soft` | `rgba(224,168,92,.12)` | Taustatäyttö |
| `--color-on-accent` | `#17130c` | 8.75:1 amber-pinnalla |
| `--color-success` | `#7fc08f` | 8.25:1 – **varattu** |
| `--color-warning` | `#d9a441` | 7.83:1 – **varattu** |
| `--color-error` | `#e58b7b` | 6.97:1 – **varattu** |

---

## 3. Mitatut kontrastit (renderöidystä sivusta)

Kaikki 43 mitattua tekstiparia molemmilla sivuilla läpäisevät WCAG AA:n; **matalin
arvo on 7.45:1**, eli koko sivusto on käytännössä AAA-tasolla normaalille tekstille.

| Pari | Ennen (0cb6845) | Jälkeen | Huomio |
|---|---|---|---|
| Leipäteksti | 16.67:1 | 15.83:1 | ~sama |
| Hero-intro | 14.25:1 | 15.83:1 | parani |
| Kortin lista / bullet / metarivi | 7.03:1 | 7.61:1 | parani |
| Nav-linkki | 7.92:1 | 8.23:1 | parani |
| Footer | 7.95:1 | 7.98:1 | ~sama |
| Korostuslinkit | 14.33:1 | 8.33:1 | laski – ks. alla |
| Ensisijainen CTA | 15.41:1 | 8.75:1 | laski – ks. alla |
| Hero-label | 16.86:1 | 9.00:1 | laski – ks. alla |
| Koodilohko | 16.83:1 | 9.46:1 | laski – ks. alla |

**Miksi korostusvärin luvut laskivat:** vanha `#64ffda` on neonmintunvihreä, jonka
kontrasti lähes mustaa vastaan on 16.9:1 – käytännössä maksimi. Amber `#e0a85c` on
9.0:1. Lasku on suora seuraus hyväksytystä lämpimästä korostuksesta, ei virhe.
Jokainen arvo on edelleen **yli AAA-rajan (7:1)**. Luettavan leipätekstin kontrasti
ei laskenut.

---

## 4. Typografia

Ei ulkoisia fontteja. `--font-sans` on järjestelmäpino, `--font-mono` sisältää vain
fontteja, jotka joko löytyvät käyttöjärjestelmästä tai päätyvät `monospace`-varalle.

| Rooli | Token | Renderöity (1440 px) |
|---|---|---|
| Hero-otsikko | `--font-size-2xl` | 42 px / lh 1.12 / 600 |
| Osio-otsikko | `--font-size-xl` | 28 px / lh 1.12 / 600 |
| Hero-alaotsikko | `--font-size-lg` | 21 px / 500 |
| Korttiotsikko | `--font-size-md` | 18 px / 600 |
| Leipäteksti | `--font-size-base` | 17 px / lh 1.6 |
| Kortin teksti, listat, nav | `--font-size-sm` | 15 px |
| Tekninen metadata (mono) | `--font-size-xs` | 13 px |

**Ratkaistut auditointihavainnot:**

- Hero-otsikko 48 px → 42 px, line-height 1.6 → 1.12. Ei enää jättimäinen.
- Korttiotsikko oli 16.8 px ja leipäteksti 16 px (ero 5 %). Nyt 18 px vs. kortin
  15 px – **ero 20 %** plus paino- ja väriero.
- Leipätekstin rivinpituus oli ~138 merkkiä. `--width-reading: 68ch` rajaa sen nyt
  osioiden tekstikappaleissa.
- Mono ei enää hallitse: navigaatio, painikkeet ja logo käyttävät sans-fonttia.
  Mono on jäljellä vain metadatassa, labeleissa ja koodilohkossa.

---

## 5. Spacing, leveydet ja muoto

**Spacing** on 4 px:n kerrannaisia `--space-1` … `--space-9` (4 → 96 px). Kaikki
korttien padding, grid-gap, osioiden pystyrytmi ja headerin välit tulevat tästä.

**Leveydet:** `--width-site: 1120px` (oli 1100 px), `--width-reading: 68ch`,
`--gutter` 1.25 rem mobiilissa → 2 rem yli 640 px.

**Muoto:** `--radius-sm: 4px`, `--radius-md: 8px`, `--radius-lg: 12px`,
`--radius-pill: 999px`. Kortit 14 px → 8 px, painikkeet 999 px → 8 px.
Ei 20–30 px pyöristyksiä.

**Elevation:** `--shadow-sm` ja `--shadow-md` ovat olemassa, mutta pinnat erotetaan
ensisijaisesti reunaviivalla. Varjoa käytetään vain skip-linkissä, joka kelluu
sisällön päällä.

**Kontrollit:** `--control-height: 2.75rem` (44 px kosketuskohde),
`--control-radius`, `--control-padding-x`, `--control-font-size`. Hover muuttaa vain
väriä – ei `transform`ia, ei mittoja, ei layout shiftia.

**Liike:** `--transition-fast: 120ms`, `--transition-normal: 200ms`,
`--ease-standard`. `prefers-reduced-motion` nollaa kaikki siirtymät globaalisti.

**Z-index:** `--z-base: 0`, `--z-elevated: 10`, `--z-header: 20`,
`--z-skip-link: 100`. Ei satunnaisia suuria arvoja.

---

## 6. Varatut tokenit

Nämä on määritelty tehtävänannon vaatiman täyden asteikon vuoksi, mutta niitä ei
vielä käytetä. Ne ovat sopimus tuleville vaiheille, eivät kuollutta koodia:

| Token(it) | Varattu |
|---|---|
| `--color-success`, `--color-warning`, `--color-error` | Vaihe 3: tilamerkinnät (julkaistu / testaus / kehityksessä) |
| `--width-wide`, `--width-narrow` | Vaihe 3: leveät sovellusrivit |
| `--shadow-sm` | Elevation-linjan toinen porras |
| `--radius-lg` | Asteikon ylin porras |
| `--z-base`, `--z-elevated` | Z-index-asteikon täydennys |
| `--space-9`, `--line-height-relaxed`, `--font-weight-normal`, `--font-weight-bold` | Asteikkojen täydet portaat |

---

## 7. Rajaukset – mitä Vaihe 1 **ei** tehnyt

- Hero-rakennetta ei muutettu. Koodilohko on yhä paikallaan; vain sen pinta ja
  värit tulevat tokeneista. Spec-paneeli on Vaihe 2.
- Projektien järjestystä, ryhmittelyä tai sisältöä ei muutettu.
- Osaamiskorttien rakennetta (7 korttia) ei muutettu.
- SureKeepiä, Työtoria eikä JanstechApps-kaistaa ei lisätty.
- `apps/index.html` ja `apps/css/style.css` jäivät koskematta – oma tyylitiedosto,
  ei jaettuja tokeneita. Yhtenäistäminen on erillinen päätös.
- Sisältötekstejä ei muutettu.

## 8. Tiedossa olevat ristiriidat

- **`apps/css/style.css` on erillinen järjestelmä.** Sillä ei ole yhteisiä
  tokeneita eikä se peri mitään `css/style.css`:stä. Sivu näyttää nyt eri
  sukupolvelta kuin muu sivusto. Ehdotus: käsitellään auditoinnin luvun 12.5
  päätöksen yhteydessä, ei tässä vaiheessa.
- **`gainsai/index.html` sisältää yhä oman `<style>`-lohkon** (~95 riviä
  sivukohtaisia sääntöjä). Ne käyttävät nyt jaettuja tokeneita, joten ristiriitaa
  ei ole – mutta säännöt kuuluisivat pitkällä tähtäimellä jaettuun CSS:ään
  komponentteina (`.status-pill`, `.shot-grid`, `.info-grid`). Tämä tehdään
  Vaiheessa 5, kun komponenttien lopullinen muoto on päätetty.
- Yksi kertaluonteinen inline-tyyli (`style="padding-top:0"`) jätettiin
  `gainsai/index.html`:ään; se ei ole osa perusjärjestelmää.
