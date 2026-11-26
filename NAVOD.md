# Zpěvník – návod

Celá aplikace je jeden soubor `index.html` (~65 kB). Nic se neinstaluje, nepotřebuje internet ani server.
Písně se ukládají v prohlížeči (localStorage), sto písní zabere řádově stovky kB.

## Na počítači
Otevři `index.html` v prohlížeči (Chrome, Edge, Firefox, Safari). Doporučuju si ho dát do záložek.

## Na mobilu – dvě možnosti

**A) Jeden soubor (nejjednodušší, Android)**
V aplikaci *⇅ Data → Stáhnout aplikaci i s písněmi (.html)*. Vznikne jeden soubor s aplikací i všemi písněmi.
Pošli si ho do telefonu a otevři v Chrome/Firefoxu. Při dalším otevření novější verze se písně sloučí.
(Na iPhonu se HTML ze Souborů otevírá jen jako náhled – tam použij variantu B.)

**B) Jako „aplikace na ploše“ s offline režimem (Android i iPhone)**
Nahraj celou složku (`index.html`, `sw.js`, `manifest.webmanifest`, `icon.svg`) na libovolný statický hosting
zdarma (např. Netlify Drop – stačí přetáhnout složku, nebo GitHub Pages). Adresu otevři v mobilu
a dej *Přidat na plochu*. Po prvním otevření funguje i bez internetu.
Písně si do mobilu dostaneš importem zálohy (.json) – na hostingu žádné písně nejsou, zůstávají jen v zařízení.

## Přenos mezi zařízeními
*⇅ Data → Záloha (.json)* na jednom zařízení, *Importovat* na druhém. U každé písně vyhrává novější verze
(takže poznámky připsané v mobilu se přenesou zpět do počítače).

## Automatická synchronizace (Mac ↔ iPhone)
Tlačítko **☁** nahoře → podle návodu si na GitHubu vytvoř přístupový klíč jen s oprávněním *gist* a vlož ho → *Připojit*.
Na dalších zařízeních vlož stejný klíč, aplikace si svůj gist najde sama. Pak se synchronizuje samo:
při spuštění, pár sekund po každé změně, při návratu do aplikace, po připojení k internetu a každých 5 minut.
U každé písně vyhrává novější verze, smazaná píseň zmizí všude (pokud ji mezitím jinde neupravíš).
Ikona ukazuje stav: ☁ ✓ aktuální, ☁ … probíhá, ☁ ⨯ offline, ☁ ! chyba (klikni pro detail).
Gist je zároveň automatická záloha – na GitHubu je u něj celá historie verzí.
Klíč zůstává jen v zařízení (nejde do zálohy ani do exportu aplikace).

## Formát písní (ChordPro)
```
{title: Název}
{artist: Interpret}
{key: G}
{capo: 2}

{sov: 1.}
[G]Text s [D]akordy v [Emi]závorkách
{eov}

{soc: R:}
[C]Refrén [G]…
{eoc}

{chorus: R:}          ← odkaz „zopakuj refrén“
{c: 2× dokola}        ← komentář
{x_note: ⏸ stopka}    ← moje poznámka k následujícímu řádku
{new_page}            ← při tisku vynutí novou stránku
```
Text zkopírovaný z webu ve tvaru „akordy na řádku nad textem“ převede tlačítko *⇄ Akordy nad textem → ChordPro*
v editoru (a automaticky i při importu .txt).

## Tisk / PDF
*🖨 Tisk / PDF* → zvol papír, sloupce, písmo a písně → *Vytvořit náhled* → *Tisk / Uložit jako PDF*
(v dialogu tisku zvol „Uložit jako PDF“, okraje „Žádné“/„Výchozí“, měřítko 100 %).
Aplikace sama rozloží stránky: sloka se nikdy nerozdělí, píseň, která se vejde na sloupec/stránku,
se nerozdělí, a obsah dostane čísla stran.

## Basa
Tlačítko **𝄢** v písni zapne basové taby (EADG). Generují se z akordů podle zvoleného vzoru – jeden akord = jeden takt,
tab je nad každým řádkem textu (nebo souhrnně u sloky – volba v liště basy). Když řádek začíná bez akordu,
doplní se na začátek akord, který pokračuje z předchozího řádku – označený v závorce, např. (G). Vzor se vybírá nahoře nad písní
(kořen–kvinta, oktávy, rozklad, walking, valčík…) nebo se napíše vlastní:
`1` kořen, `3` tercie, `5` kvinta, `7` septima, `8` oktáva, `5,` = o oktávu níž, `>` = přechodový tón k dalšímu akordu, `-` = drž.
Uloží se do písně jako `{x_bass_pattern: 1 - 5, -}`.
Vzory jsou rozdělené do skupin **Základní**, **Walking** (rozklady, stupnice, chromatické přechody, dvoutaktové varianty),
**Blues a boogie** (boogie-woogie v osminách, shuffle, blues walking, pomalé a mollové blues),
**Swing a ragtime** (two-beat, charleston, ragtime, stride, swing walking – zapnou swing), **Polka (2/4)**
(um-pa kořen–kvinta / tercie, dechovka – nastaví písni takt `{time: 2/4}`; běh do dalšího akordu jde přes poslední dva takty) a **Valčík**.
Ve vlastním vzoru navíc: `2` `4` `6` stupně, `b`/`#` = o půltón níž/výš (`1 #2 3 5`), `>5` = přechod přes kvintu dalšího akordu,
`>s` = celým tónem k dalšímu akordu, `|` = střídání variant takt po taktu (`1 2 3 5 | 6 5 3 >`).
**Takt** písně se volí roletkou v liště basy (2/4, 3/4, 4/4, 2/2, 5/4, 6/8, 9/8, 12/8) a uloží se jako `{time: 6/8}`.
Ve 6/8, 9/8 a 12/8 se počítá po houpavých dobách (tečkovaná čtvrťová, tempo ♩.=). Když vzor do nového taktu nesedí,
nahradí se základním vzorem taktu; vzory valčíku, polky a 6/8 nastaví takt samy.
Vzor s 8 kroky se hraje v osminách. Zaškrtávátko **swing** (uloží se do písně jako `{x_swing: ano}`) hraje osminy houpavě
(triolově) – blues vzory ho zapnou samy.

**Chytré přechody** (zaškrtávátko v liště basy, standardně zapnuté):
- *Dva akordy v taktu* (½, ¼): u walking a boogie vzorů zahraje kořen a hned vede do dalšího akordu – po stupnici,
  chromaticky, nebo obklíčením cílového tónu (tón nad a pod) – a druhý akord stejně vede do toho následujícího.
- *Akord přes víc taktů* (`×2`, `×4` nebo stejný akord víckrát za sebou, i přes konec řádku): poslední takt dostane
  **turnaround** – běh do dalšího akordu (folk G×2 → C: `G - A H`, walking: `G A B H`, boogie dojede osminami k dalšímu kořeni).
  Ve walking vzorech se prostřední takty obmění (z oktávy dolů) a místo opakovaného tónu jde přechod zpět na vlastní kořen.
- Bez zaškrtnutí se vzor hraje doslova, jak je napsaný.
Vlastní basový vzor nad konkrétní řádek: režim ✎ → klik na řádek → „Basový vzor nad řádkem“ (uloží se jako `{x_bass: …}`).
Při tisku zaškrtni „Basové taby“.
Počet taktů akordu: klikni v písni na basový tab nad řádkem a u každého akordu vyber ¼, ½, 1, 2, 3, 4, 6 nebo 8 taktů.
Uloží se nad řádek jako `{x_bars: 2 1 ½}` (pořadí = akordy v tabu, včetně pokračujícího akordu v závorce).
Přechodový tón `>` se hraje jen v posledním taktu akordu, půl taktu = první polovina vzoru, čtvrt taktu = první čtvrtina (u vzoru na 4 doby jedna doba).
Kontrabas: v liště basy přepni „Baskytara“ → „Kontrabas“. Tab pak drží ruku v nízkých polohách (do 4.–5. pražce),
upřednostňuje prázdné struny a hlubší oktávu a pod tabem ukáže řádek **P** s prstokladem 1-2-4 (0 = prázdná struna).

### Přehrání tabu
**▶ Přehrát basu** v liště basy zahraje celou píseň (s jedním taktem odpočítávání; refrén `{chorus}` se přehraje znovu).
Tlačítko **▶** vedle tabu přehraje jen ten řádek, kurzor ukazuje právě hraný tón. Tempo `♩=` se ukládá do písně (`{tempo: 96}`),
takt bere z `{time: 3/4}` (jinak 4/4). Zaškrtávátka: *metronom* (klik na každou dobu), *řádek dokola* (pro cvičení).
Zvuk (volba *zvuk: kontrabas / baskytara*) se syntetizuje přímo v prohlížeči, funguje i offline. Nejhlubší tóny kontrabasu z reproduktoru mobilu skoro neuslyšíš – na sluchátka nebo reprák je to mnohem lepší. Na iPhonu hraje i s tichým režimem (Safari 17+), jinak vypni přepínač ticha.

### Ruční úprava tabu
Tlačítko **✎** vedle tabu otevře mřížku: každý takt má řádky G D A E a políčka pro doby. Klikni do políčka a napiš
číslo pražce (0 = prázdná struna) – tón hned zazní. Prázdné políčko = drž předchozí tón. Šipky přesouvají, mezerník přehraje.
U taktu jde změnit název akordu, dělení (4 kroky = čtvrtky, 8 = osminy…) a délku (celý / ½ / ¼), přidat nebo smazat takt.
*↺ Ze vzoru* vrátí vygenerovaný tab. Uloží se nad řádek jako `{x_btab: D: A5 - E0 - | G: E3 - D5 -}`
(struna + pražec, `-` drž, `|` další takt) a jde to psát i ručně v editoru. Vlastní tab je v písni označený „✎ vlastní“
a při transpozici se posune spolu s akordy.
