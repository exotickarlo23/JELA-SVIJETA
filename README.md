# Zavrti globus – jelo iz svake države 🌍🍽️

Web aplikacija u **jednoj HTML datoteci** (`index.html`). Klikni **ZAVRTI!**, cartoon globus se zavrti,
uspori i stane na nasumičnoj državi, a zatim se pojavi kartica s nacionalnim jelom te države.

## Pokretanje

Otvori `index.html` u pregledniku (dvoklik). Backend nije potreban. Potreban je internet za:

- D3.js, TopoJSON i kartu `world-atlas` (countries-50m) s jsdelivr CDN-a,
- zastave s `flagcdn.com` (ako se ne učitaju, prikazuje se emoji zastave),
- font Fredoka s Google Fonts.

## Što sve zna

- 195 država (193 članice UN-a + Vatikan i Palestina). Izvlačenje je ravnomjerno po državama, a ne po površini (`crypto.getRandomValues`).
- Vrtnja traje 4–6 s, s 3–5 punih okretaja. Usporava glatko i staje centrirana na odabranoj državi, bez skoka na kraju.
- Male države imaju točkicu na globusu, a nakon zaustavljanja dobiju i veliki pin s pulsirajućim krugom.
  Tuvalu, kojeg nema na karti 50m, prikazan je pinom na svojim koordinatama.
- Zvukovi se generiraju Web Audio API-jem: čegrtaljka koja usporava zajedno s globusom, „pop” i „ta-da!”.
- **Odrađene države** spremaju se u `localStorage`. Na globusu su sive i više se ne mogu izvući.
  Tu su i brojač, reset liste i ručni unos (📝).
- **Način za snimanje**: 📱 prebacuje na format 9:16, a 🎬 uključuje čisti prikaz u kojem je vidljiv samo gumb ZAVRTI!.
  Iz čistog prikaza izlaziš tipkom H ili Esc, ili dvostrukim dodirom pozadine.
- Tipkovnica: razmak/Enter = zavrti, H = čisti prikaz, D = označi odrađeno.

## Kako mijenjati

Sve je u `index.html`:

| Što | Gdje |
| --- | --- |
| Boje sučelja (pozadina, gumbi, obrubi) | CSS varijable u `:root` na vrhu |
| Trajanje vrtnje, broj okretaja, krivulja usporavanja, boje globusa, debljina obruba | objekt `CONFIG` |
| Podaci o državama i jelima | niz `COUNTRIES` (jedna država = jedan red) |

Polja u `COUNTRIES`: `id` (numerički ISO kod iz world-atlas), `iso2` (za zastavu), `ime`, `jelo`, `izvorno`,
`emoji`, `opis` i neobavezno `pin: [dužina, širina]` za države kojih nema na karti.
