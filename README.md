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
* `gainsai/`, `kauppalista/`, `waveiq/` – julkaistujen sovellusten omat
  projektisivut (`/gainsai/`, `/kauppalista/`, `/waveiq/`).
* `apps/` – Janstech Android -sovellusten koontisivu, joka kokoaa sovellusten
  Google Play-, tietosuoja- ja tukilinkit. Sivu käyttää omaa tyylitiedostoaan
  (`apps/css/style.css`) eikä jaettuja design tokeneita.
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

Jokaisella julkaistulla Android-sovelluksella on oma sivunsa, joka noudattaa
samaa rakennetta: hero + tekninen yhteenvetopaneeli (`<dl>`), tuotekuvaus,
keskeiset ominaisuudet, sovelluskohtainen syventävä osio, tekninen toteutus,
tietoturva ja tietosuoja, kuvakaappaukset ja julkaisutilanne. Kaikki sisältö on
FI/EN, ja jokaisella sivulla on omat SEO- ja Open Graph -metatiedot.

* **GainsAI** – `gainsai/index.html` (`/gainsai/`)
* **Kauppalista & Muistiinpanot** – `kauppalista/index.html` (`/kauppalista/`)
* **WaveIQ Radio** – `waveiq/index.html` (`/waveiq/`)

Projektisivujen yhteiset tyylit ovat `css/style.css`-tiedoston osiossa
*13. PROJEKTISIVUT*; sivuilla ei ole omia inline-tyylilohkoja.

## Sivustojen työnjako

Kolme osoitetta palvelee eri tarkoitusta, ja jokainen linkittää kahteen muuhun:

* **janstech.github.io** – tämä portfolio: kehittäjäprofiili, projektit ja
  tekninen dokumentaatio.
* **janstech.github.io/apps/** – julkaistujen sovellusten koontisivu Google
  Play-, tietosuoja- ja tukilinkkeineen.
* **janstechapps.com** – sovellusten varsinainen tuotesivusto.

## Dokumentit

Arkkitehtuuri- ja dokumentaatio-osio (`#architecture`) listaa `documents/`-kansion
PDF:t dokumenttihakemistona: formaatti, tekninen aihealue, nimi ja yhden virkkeen
kuvaus. CV linkitetään yhteysosiosta. Dokumentti lisätään vain, jos tiedosto on
todella olemassa.

## Ominaisuudet

* **Täysin responsiivinen:** Toimii mobiilissa, tabletilla ja desktopilla.
* **Tumma teema:** Silmäystävällinen ja moderni "Dark Mode" -tyylinen värimaailma.
* **Latauslinkit:** Mahdollisuus ladata CV ja projektidokumentaatiot PDF-muodossa.
* **Projektigalleria:** Klikattavat kuvat avautuvat tarkasteltavaksi.

---

© 2026 Jan Sarivuo
