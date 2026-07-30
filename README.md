# Jan Sarivuo – Portfolio

Tämä repository sisältää henkilökohtaisen portfoliosivustoni lähdekoodin. Sivusto esittelee osaamistani Full Stack -kehittäjänä, työssäoppimisjaksoni projekteja sekä teknisiä taitojani.

**[Avaa portfolio tästä (Live Demo)](https://janstech.github.io)**

## Teknologiat

Sivusto on rakennettu puhtaalla ja modernilla web-teknologialla ilman raskaita kirjastoja, tavoitteena nopea latausaika ja selkeä koodirakenne.

* **HTML5** – Semanttinen rakenne ja saavutettavuus.
* **CSS3** – Moderni ulkoasu, CSS Grid & Flexbox, responsiivisuus ja CSS-muuttujat (custom properties).
* **Git & GitHub** – Versionhallinta ja julkaisu (GitHub Pages).
* **VS Code** – Kehitysympäristö.

## Projektin rakenne

Tiedostot on organisoitu selkeisiin kokonaisuuksiin ylläpidettävyyden parantamiseksi:

* `index.html` – Pääsivu ja sisältö.
* `css/` – Tyylitiedostot ja visuaalinen ilme.
* `images/` – Projektikuvat, ikonit ja grafiikka.
* `documents/` – Ladattavat tiedostot (CV, arkkitehtuurikuvaukset).
* `gainsai/` – GainsAI-sovelluksen oma projektisivu (`/gainsai/`).
* `apps/` – Janstech Android -sovellusten koontisivu.
* `sitemap.xml`, `robots.txt` – Hakukoneille tarkoitetut tiedostot.

## Kaksikielisyys (FI/EN)

Sivusto käyttää kevyttä, riippuvuudetonta i18n-ratkaisua: jokaisella sivulla on
sivukohtainen `dict`-sanakirja (`fi` / `en`), ja näkyvät tekstit merkitään
HTML:ssä attribuuteilla:

* `data-i18n` – elementin sisältö
* `data-i18n-alt` – kuvan `alt`-teksti
* `data-i18n-aria` – elementin `aria-label`

Valittu kieli tallennetaan `localStorage`-avaimeen `portfolio_lang`, joten
kielivalinta säilyy myös projektisivuille siirryttäessä. Oletuskieli on suomi.

## Projektisivut

Sovellusprojektit esitellään etusivun projektikorteissa. Laajemmat kokonaisuudet
voivat saada oman sivun samalla rakenteella, tyylillä ja i18n-ratkaisulla:

* **GainsAI** – `gainsai/index.html`. Sisältää tuotekuvauksen, ominaisuudet,
  tekoälyn roolin, teknisen toteutuksen, kuvakaappaukset ja julkaisutilanteen
  molemmilla kielillä sekä omat SEO- ja Open Graph -metatiedot.

## Ominaisuudet

* **Täysin responsiivinen:** Toimii mobiilissa, tabletilla ja desktopilla.
* **Tumma teema:** Silmäystävällinen ja moderni "Dark Mode" -tyylinen värimaailma.
* **Latauslinkit:** Mahdollisuus ladata CV ja projektidokumentaatiot PDF-muodossa.
* **Projektigalleria:** Klikattavat kuvat avautuvat tarkasteltavaksi.

---

© 2026 Jan Sarivuo
