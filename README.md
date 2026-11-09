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
- **Odrađene države**, ocjene i red država spremaju se u `localStorage`. Na globusu su sive i više se ne mogu izvući.
  Tu su i brojač, reset liste i ručni unos (📝).
- **Način za snimanje**: 📱 prebacuje na format 9:16, a 🎬 uključuje čisti prikaz u kojem je vidljiv samo gumb ZAVRTI!.
  Iz čistog prikaza izlaziš tipkom H ili Esc, ili dvostrukim dodirom pozadine.
- **🎯 Odredi državu**: red država na kojima globus mora stati, npr. prijedlozi gledatelja (uz neobavezno ime, npr. `@marko`).
  Sljedeća vrtnja staje na prvu državu iz reda i izgleda isto kao nasumična. Ime gledatelja prikazuje se na kartici.
  Broj država u redu vidi se na gumbu (u čistom prikazu je skriven). Kad je red prazan, globus bira nasumično.
- **⭐ Ocjena**: nakon kuhanja ocijeniš jelo od 1 do 10, može i s dvije decimale (npr. 8,75). Ocijenjeno jelo se automatski označi kao odrađeno.
- **🛂 Putovnica**: svaka odrađena država dobije pečat sa zastavom, datumom i ocjenom (klik na pečat = promjena ocjene).
  Kartica **Top lista** prikazuje top 10 („Top 10 nakon N država”), a **▶️ Odbrojavanje** otkriva mjesta od 10. do 1.
  sa zvukom i konfetima, kao završni kadar ili zaseban video. Radi i u formatu 9:16 i u čistom prikazu.
- **📸 Spremi sliku**: kartica jela kao PNG, **story 1080×1920** ili **naslovna 1280×720**, s oznakom epizode
  (broj se sam predloži, a možeš ga promijeniti) i ocjenom. Na mobitelu se može i izravno podijeliti.
- Tipkovnica: razmak/Enter = zavrti, H = čisti prikaz, D = označi odrađeno, R = ocijeni, T = odredi državu,
  P = putovnica (u putovnici: 1/2 = pečati/top lista, razmak = odbrojavanje, Esc = zatvori).
- Reset liste briše i ocjene.

## Kako mijenjati

Sve je u `index.html`:

| Što | Gdje |
| --- | --- |
| Boje sučelja (pozadina, gumbi, obrubi) | CSS varijable u `:root` na vrhu |
| Trajanje vrtnje, broj okretaja, krivulja usporavanja, boje globusa, debljina obruba | objekt `CONFIG` |
| Podaci o državama i jelima | niz `COUNTRIES` (jedna država = jedan red) |

Polja u `COUNTRIES`: `id` (numerički ISO kod iz world-atlas), `iso2` (za zastavu), `ime`, `jelo`, `izvorno`,
`emoji`, `opis` i neobavezno `pin: [dužina, širina]` za države kojih nema na karti.
