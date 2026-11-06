# Atrodi savu dīķi

Hokeja nodarbību portāls (LV / EN / RU). Izstrādātājs: Prime IT.

## Lomas
- **Administrators** (`#administracija`): izveido un aptur nodarbību rīkotāju profilus (vārds, e-pasts, parole, komanda). Pirmajā atvēršanas reizē izveido pirmo administratora kontu.
- **Nodarbību rīkotājs** (`#rikotajs`): saglabā komandas profilus (nosaukums, vieta, halle), veido nodarbības ar vietu skaitu, aktivizē tās, apstiprina, noraida vai atceļ (dzēš) pieteikumus.
- **Spēlētājs** (`#nodarbibas`): redz aktīvās nodarbības (kārtotas no jaunākās pēc datuma, tad laika), piesakās bez konta (obligāts tikai vārds), redz savu statusu un adresi, var atcelt pieteikumu.

## Tehnika
- Viens fails `index.html`, bez bibliotēkām.
- Dati: modulis `Store` ar adapteri. Izstrādē tiek izmantota claude.ai Artifact `db` krātuve. Ja tā nav pieejama, dati glabājas pārlūka localStorage. Pārejai uz Azure Database for PostgreSQL jānomaina tikai adapteris.
- Kolekcijas: `admins`, `organizers`, `templates`, `sessions`, `applications`, `meta/counters`.
- Paroles glabājas tikai kā PBKDF2-SHA256 jaucējvērtība ar sāli (150 000 iterāciju).

## Statusi
- Nodarbība: `draft` (melnraksts), `active` (aktīva). "Pilna" un "Notikusi" tiek aprēķināti.
- Pieteikums: `signed` (pieteicies), `approved` (apstiprināts), `rejected` (noraidīts). Atcelšana dzēš ierakstu, un vieta atbrīvojas.
