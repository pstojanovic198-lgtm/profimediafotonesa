# Postavljanje sajta na hosting

Sadržaj foldera `dist/` je ceo sajt. Na server ide sve što je u njemu, uključujući skrivene fajlove `.htaccess` i `_headers`.

## 1. Pre postavljanja: upišite pravi domen
Domen se koristi u canonical linku, Open Graph tagovima, podacima za Google (JSON-LD), `robots.txt` i `sitemap.xml`.

```
python3 build/dist.py --domain https://vas-domen.rs/
```
Ako se build pokrene bez `--domain`, ostaje `VAS-DOMEN.rs` i skripta to javlja upozorenjem.

## 2. Postavljanje (izaberite jedno)

**A. Klasičan hosting (cPanel, Apache)**
1. File Manager → `public_html`.
2. Otpremite sadržaj foldera `dist/` (ne sam folder). Uključite prikaz skrivenih fajlova da bi se videlo `.htaccess`.
3. Uključite SSL (Let's Encrypt u cPanelu), pa u `.htaccess` otkomentarišite tri reda za HTTPS preusmeravanje.

**B. Netlify (besplatno)**
1. app.netlify.com → Add new site → Deploy manually → prevucite folder `dist/`.
2. Domain management → Add domain → pratite uputstvo za DNS. SSL se uključuje sam. `_headers` se primenjuje automatski.

**C. Cloudflare Pages (besplatno)**
1. Workers & Pages → Create → Pages → Upload assets → otpremite `dist/`.
2. Custom domains → dodajte domen. `_headers` i `404.html` rade automatski.

## 3. Posle objave (Google)
1. Google Search Console → dodajte domen → potvrdite vlasništvo (DNS zapis).
2. Sitemaps → upišite `sitemap.xml` → Submit.
3. URL Inspection → početna strana → Request indexing.
4. Proverite podatke za Google: https://search.google.com/test/rich-results (treba da prepozna firmu i česta pitanja).
5. Proverite prikaz pri deljenju linka: https://developers.facebook.com/tools/debug/ (treba da se vidi OG slika).
6. Google Business Profile: napravite ili dopunite profil (isti naziv, telefon i oblasti rada kao na sajtu) i u njega upišite adresu sajta. Za lokalne pretrage („fotograf za venčanje Petrovac na Mlavi") ovo je najvažniji pojedinačni korak.
7. U Instagram profil (@profimedia.fotonesa) stavite link na sajt.

## 4. Zamena fotografija
Svaka ilustrativna fotografija je u kodu označena sa `<!-- ZAMENITI: pravi rad klijenta -->`. Kad stignu pravi radovi: dodati ih u `images.json`, napraviti WebP veličine (360/540/720 i 960–2048), ukloniti napomenu iznad galerije i pokrenuti build ponovo.
