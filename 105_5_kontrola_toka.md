# Kontrola toka: Kondicionali, petlje i pokušaji {#kontrola_toka}

U programiranju ne bismo daleko dogurali kada bismo jedino mogli po redu
izvršavati jedinične radnje. S jedne strane moramo moći prema određenim
uvjetima odabrati koje naredbe će se izvršiti, a koje ne. Ovo postižemo
*kondicionalima*. S druge strane moramo moći ponavljati iste naredbe.
Ovo postižemo *petljama*. U nastavku ćemo se upoznati s detaljima i
riječ je o standardnim komponentama gotovo svih programskih jezika. U
mnogim jezicima visoke razine postoji i treći koncept u kontroli toka, a
to je *pokušaj* provođenja određenih naredbi s jasno definiranim kôdom
koji će se izvršiti ako neka od naredbi ne uspije.

## Kondicionali: Ako \... onda \... {#kondicionali}

Kondicionali služe *odabiru* kôda koji će se izvršiti. Kada su neke
linije ovisne o kondicionalu, tada se neće izvršavati uvijek već samo
kada su određeni uvjeti zadovoljeni. Time dobivamo mogućnosti poput:
\"ako se neki izraz evaluira kao True, napravi nešto; a ako ne, napravi
nešto posve drugo\". Na taj način možemo reći stvari poput:

- Ako direktorij ne postoji, stvori ga.

- Ako datoteka postoji pitaj korisnika da li ju želi prepisati novom
  datotekom.

- Ako korisničko ime već postoji, javi da je zauzeto, a ako korisničko
  ime ne postoji, stvori novog korisnika.

- Ako je korisnik upisao odgovor \"a\", javi da je odgovor točan, a ako
  je korisnik upisao \"b\", \"c\" ili \"d\" javi da je odgovor netočan,
  a u svim ostalim slučajevima javi da odgovor nije prepoznat.

::: important
Kondicionali Kondicionali služe uvjetnom izvršavanju kôda. Oni prema
određenim uvjetima odabiru koji će se reci izvršiti, a koji ne.
:::

Kondicionale u programskim jezicima tipično reprezentiramo sa složenom
izjavom `if`{.python}, a minimalan oblik te izjave u Pythonu je:

``` python
Najjednostavniji oblik kondicionalalisting:kondicional1 if <izraz>: neka radnja
```

\"Neka radnja\" se izvršava samo ako izraz rezultira vrijednošću koja se
procjenjuje kao `True`{.python} (vidi poglavlje o booleovim
vrijednostima za detalje). Ova radnja se mora sastojati od barem jedne
linije kôda, ali može se sastojati i od više njih. Konkretnije, ispod
svake `if`{.python} izjave se očekuje uvučeni blok kôda. Taj blok koda,
kao što je već rečeno, se naznačuje tako što su sve linije u bloku
jednako uvučene i izvršava se samo ako je uvjet zadovoljen, a u
suprotnom se preskače.

Što se uvlačenja kôda tiče, u Pythonu se uvijek uvlači nakon dvotočke
koja se, između ostalog, koristi u kondicionalima i petljama. Općenito
je pravilo da Python nakon retka koji završava s dvotočkom očekuje barem
jednu uvučen redak kôda odnosno minimalan blok kôda.

Standard u Pythonu je kôd uvlačiti sa četiri razmaka koji se u
prilagođenom softveru dobivaju pritiskom na tipku \"tabulator\" odnosno
\"tab\". Ovaj koncept se naziva \"mekanim tabulatorom\" (eng. *soft
tab*) jer služi istome čemu služi i sam znak tabulator, ali izbjegava
taj znak (što ima i smisla jer je tabulator po definiciji razmak
varijabilne dužine). Moguće je koristiti i znak tabulator, ali se treba
pobrinuti da se ne miješaju tabulatori i razmaci. Navedeno zvuči
kompleksnije no što je slučaj u praksi jer se za ujednačenost uglavnom
pobrine softver u kojem programiramo.

Moguće je napisati i kondicional koji će uvijek izvršiti neki kôd tako
što ga proširimo s komponentom `else`{.python} koja znači \"u svim
ostalim slučajevima\".

``` python
Kondicional koji će uvijek izvršiti radnjulisting:kondicional3 if <izraz>: neka radnja else: # u svim ostalim slučajevima neka druga radnja
```

U ovom obliku, \"neka radnja\" se izvršava kao i u prošlom, ali ako se
ne izvrši, tada će se izvršiti \"neka druga radnja\". Drugim riječima
ovakav kondicional će, za razliku od prošlog oblika, uvijek izvršiti
neke naredbe. Pogledajmo neke konkretne primjere:

Primjer prikazuje tri kondicionala. Prvi kondicional radi nešto samo ako
je uvjet zadovoljen. Druga dva kondicionala uvijek rade nešto jer imaju
komponentu `else`{.python} čiji kôd se izvršava kada niti jedan drugi
uvjet nije zadovoljen. Izvršavanje prikazanog koda, dakle, ispisati će
dvije ili tri rečenice jer prvi prikazani kondicional nema komponentu
`else`{.python} dok druga dva imaju. Koje su to?

::: pythonp
[\[listing:kondicional4\]](#listing:kondicional4){reference-type="ref"
reference="listing:kondicional4"} x je veće ili jednako y x + y je manje
od 10
:::

U prijašnjem primjeru svi izrazi koji se pojavljuju kao uvjeti se
evaluiraju u booleove vrijednosti. Kad želimo vidjeti rezultat određenog
izraza najjednostavnije je to probati u Python komandnoj liniji.

Što bi se dogodilo da smo koristili izraze koji se ne evaluiraju u
booleovu vrijednost poput `x + y`{.python}? U Pythonu je za potrebe
kondicionala moguće i implicitno pretvoriti bilo koju vrijednosti u
booleovu vrijednost. Drugim riječima, izjava `if vrijednost:`{.python}
se izvršava kao da smo pisali `if bool(vrijednost):`{.python}. Sjetimo
se, izraz se uvijek evaluira u vrijednost pa ranije napisano ujedno
znači i `if bool(izraz)`{.python}. Pogledajmo primjer:

::: pythonp
[\[listing:kondicional5\]](#listing:kondicional5){reference-type="ref"
reference="listing:kondicional5"} bool(b) se evaluira u True bool(x + y)
se evaluira u True
:::

Kako možemo napisati kondicional koji ima više od jednog eksplicitnog
uvjeta (ne računajući `else`{.python})? U kondicionalima se često
koriste dodatne komponente *else if* koje služe upravo ovome. Python te
riječi skraćuje u riječ `elif`{.python}. Kondicional sa svim dozvoljenim
komponentama izgleda ovako:

``` python
Kondicional sa svim komponentamalisting:kondicional6 if <izraz1>: radnja 1 elif <izraz2>: radnja 2 elif <izraz3>: radnja 3 ... else: radnja n
```

A evo i konkretnog primjera kondicionala sa svim komponentama:

::: pythonp
[\[listing:kondicional6\]](#listing:kondicional6){reference-type="ref"
reference="listing:kondicional6"} slučaj \"x je 3\"
:::

Drugim riječima, svaki kondicional ima nužno jedan `if`{.python} slučaj,
a može imati i bilo koji broj `elif`{.python} slučajeva i jedan
`else`{.python} slučaj. Ovakav kondicional smo već vidjeli u primjeru
[\[listing:kviz\]](#listing:kviz){reference-type="ref"
reference="listing:kviz"}, a u idućim poglavljima ćemo za vježbu
isprogramirati nešto konkretnije i iskoristiti kondicionale. Upoznajmo
se ipak prije toga i s petljama i pokušajima kako bismo zaokružili
koncept \"kontrole toka\".

## Petlje: ponavljanje naredbi

Petlje služe *ponavljanju* jedne ili više naredi. S petljama možemo dati
instrukcije poput \"ponovi kôd za svaki element u popisu\" ili
\"ponavljaj neki kôd sve dok uvjet nije zadovoljen\". Time možemo
izraditi programe koji na primjer crtaju geometrijske oblike, izrađuju
bibliografski zapis za svaku knjigu u nekoj bazi podataka ili čekaju
korisnički unos i ponavljaju se sve dok korisnik ne zatraži izlaz iz
programa.

::: important
Petlje Petlje ponavljaju naredbe. Iste naredbe treba ponavljati
petljama, a ne dupliciranjem kôda.
:::

### Za svaki

Petlja koja se vrlo često koristi u programiranju, a u Pythonu je se
najčešće koristi petlja `for`{.python}. Kao i kod kondicionala, ovo je
složena izjava. Python koristi *for each* varijantu ove petlje koju
skraćuje u naziv `for`{.python}. Drugim riječima, `for`{.python} u
Pythonu valja čitati \"za svaki\" i ova petlja ponavlja naredbe za svaki
element u nekom skupu elemenata[^1]. Do sada jedina vrsta vrijednosti
koju smo upoznali i koja se može raščlaniti na elemente je
`str`{.python}, odnosno niz znakova pa ćemo upravo tu vrstu vrijednosti
koristiti za primjere. Petlja `for`{.python} će postati korisnija kada
naučimo i strukture podataka o čemu je riječ u zasebnom poglavlju.

Petljom `for`{.python} je dakle moguće provesti jednu ili više radnji za
svaki znak u nekom tekstu. Pogledajmo kako:

::: pythonp
[\[listing:for_basic\]](#listing:for_basic){reference-type="ref"
reference="listing:for_basic"} t e k s t
:::

Koncept \"skupa vrijednosti po kojem se može prebirati\" vrlo je važan
pa ima i vlastitu terminologiju. Prebiranje po nekom skupu vrijednosti
često nazivamo *iteracija* (eng. *iteration*), a vrsta vrijednosti po
kojoj se može prebirati je *iterabilna* (eng. *iterable*) vrsta
vrijednosti. Petlja `for`{.python} se \"izvrti određen broj krugova\" pa
završi. Jedan \"krug\" nazivamo jednom iteracijom. Iteracija kao proces
je, dakle proces prebiranja, a jedna iteracija je individualno
izvršavanje naredbi koje se ponavljaju. Jednu iteraciju unutar petlje
često nazivamo i korakom eng. *step* petlje.

O finijim detaljima spomenutog će biti riječ kasnije kada dođemo do
struktura podataka, ali terminologiju vrijedi znati i ranije jer se
često koristi u Python dokumentaciji i literaturi kao i u samom Python
jeziku prilikom, na primjer, javljanja pogrešaka.

::: important
Iteracija Kada po nečemu iteriramo, tada po tome prebiremo jedan po
jedan element. Kada je nešto iterabilno tada se po tome može prebirati.
Ove riječi se često koriste u kôdu. Metode čiji naziv počinje s
prefiksom \"iter\" vraćaju rezultatu po kojem se može iterirati. Kada
Python javi grešku da nešto nije \"iterabilno\" tada pokušavamo
prebirati po vrsti vrijednosti koja se ne može raščlaniti na sastavne
elemente.
:::

U primjeru
[\[listing:for_basic\]](#listing:for_basic){reference-type="ref"
reference="listing:for_basic"} smo vidjeli kako možemo raditi sa svakim
znakom u nekom tekstu odnosno sa svakim elementom u nekom skupu
vrijednosti. U retku `for znak in tekst:`{.python}, `tekst`{.python} je
skup vrijednosti po kojem se prebire, a `znak`{.python} je proizvoljan
naziv varijable koji unutar petlje možemo koristiti kako bi se
referirali na element u \"ovoj iteraciji\". U prvoj iteraciji, varijabla
`znak`{.python} je jednaka vrijednosti `"t"`{.python}. U drugoj
iteraciji, jednaka je vrijednosti `"e"`{.python} i tako dalje.

Što ukoliko samo želimo ponoviti neku radnju određen broj puta nevezano
za neki već postojeći skup vrijednosti poput vrijednosti
`"tekst"`{.python}? Za ovo nam je korisna funkcija `range`{.python} koja
stvara niz brojeva od nekog minimuma do nekog maksimuma. Ova funkcija je
korisnija no što se na prvi pogled možda čini pa ćemo je često
susretati. Na primjer, često se koristi u kombinaciji s petljom
`for`{.python} kako bi odredila koliko puta će se naredbe unutar petlje
ponoviti. Pogledajmo primjer:

::: pythonp
[\[listing:for_range\]](#listing:for_range){reference-type="ref"
reference="listing:for_range"} 0 tekst 1 tekst 2 tekst 3 tekst 4 tekst
:::

Kao što vidimo, kada funkciji `range`{.python} pošaljemo jedan broj, ona
stvara niz brojeva od nule do poslanog broja, ne uključujući i taj broj.
Ovdje smo to iskoristili da bismo ponovili radnju 5 puta. Kako bi bilo
jasnije što se zbiva, ispisali smo i vrijednost varijable `i`{.python}
svaki put, ali varijablu `i`{.python} uopće ne moramo koristiti unutar
petlje ako nam nije potrebna.

### Dok se uvjet ne zadovolji

Druga vrsta petlje u Pythonu je petlja `while`{.python} koja je također
često vrlo korisna. Ova petlja ne prebire po nečemu već se izvršava sve
dok neki uvjet nije zadovoljen. Njome možemo izvesti isto što i u
prošlom primjeru:

::: pythonp
[\[listing:while_basic\]](#listing:while_basic){reference-type="ref"
reference="listing:while_basic"} 0 tekst 1 tekst 2 tekst 3 tekst 4 tekst
:::

Primjer [\[listing:for_basic\]](#listing:for_basic){reference-type="ref"
reference="listing:for_basic"} također možemo postići ovom petljom, ali
nešto zaobilaznijim putem:

::: pythonp
[\[listing:while_index\]](#listing:while_index){reference-type="ref"
reference="listing:while_index"} t e k s t
:::

U prikazanim primjerima svejedno je da li koristimo petlju
`for`{.python} ili petlju `while`{.python}, ali petlja `while`{.python}
zahtijeva nešto više komponenata. Također, ova petlja krije jednu
opasnost koja se u `for`{.python} petlji može teško dogoditi: lako je
moguće da se `while`{.python} petlja krene izvršavati zauvijek! Idući
primjer prikazuje ovakvu grešku i ako ga pokrenete pripremite se da će
te morati nasilno ugasiti Python, jer se ovaj program neće nikad
završiti.

U prošlom primjeru je greškom ispuštena naredba `i += 1`{.python} pa se
uvjet za završetak ponavljanja kôda nikad neće zadovoljiti. Naredba
`print("nema kraja")`{.python} će se stoga pokušati izvrtiti beskonačan
broj puta. Izvršavanje ovog programa će završiti tek kad ga nasilno
ugasimo tako što smo prekinuli sistemski proces ili ugasili računalo.

Prikazana beskonačna petlja je rezultat greške i njezino ponašanje je
nepoželjno. Ipak, postoje situacije u kojem su beskonačne petlje zapravo
vrlo korisne i puno ih je lakše postići petljom `while`{.python} no
petljom `for`{.python}. Tipičan primjer su aplikacije koje kad se
pokrenu čekaju korisničke naredbe koje zatim izvršavaju na zahtjev.
Navedeno stoji za gotovo sve aplikacije s grafičkim sučeljem. U ovom
slučaju, petlja se nikad neće sama po sebi završiti, ali postoji
mehanizam koji ju u posebnim slučajevima može prekinuti. Pogledajmo prvo
kako funkcioniraju mehanizmi za prekidanje petlje, a konkretni primjeri
korištenja `while`{.python} petlji u ovom smislu su preneseni kasnije u
tekstu.

Postoje dvije jednostavne Python izjave koje služe upravljanju petljama
i koje se smiju koristiti samo unutar petlji. Te izjave su
`break`{.python}, koja služi prekidanju petlje i `continue`{.python},
koja služi prelasku na idući korak petlje.

### Prekini petlju

Jednostavna izjava `break`{.python} čim se izvrši završava petlju u
kojoj se nalazi. Ova izjava se koristi kada je potrebno izaći iz petlje
prije no što bi ona završila sama po sebi.

::: pythonp
[\[listing:for_break\]](#listing:for_break){reference-type="ref"
reference="listing:for_break"} n e k i
:::

Izjava \"prekini petlju\", odnosno `break`{.python}, je nužna u prije
spomenutim beskonačnim `while`{.python} petljama. Pogledajmo praktičan
primjer:

Izvrši ovaj program. Kako se ponaša? Ne radi ništa korisno, ali je
program koji se ponaša bliže računalnim aplikacijama. Naš \"prvi
program\" odnosno primjer [\[kviz\]](#kviz){reference-type="ref"
reference="kviz"} se mogao izvršiti samo jednom i onda je izašao.
Prikazani mehanizam omogućuje da se program nastavlja, odnosno ponavlja,
sve dok korisnik ne odluči prestati raditi s njim.

Jedna zanimljivost kod prekida petlje u Pythonu je što petlja
`for`{.python} podržava i komponentu `else`{.python} koja se izvršava
samo ako petlja nije prekinuta s naredbom `break`{.python}. Ova
mogućnost je često korisna prilikom pretraživanja. Pogledajmo primjer
koji provjerava da li se u nekom tekstu nalazi traženo slovo:

::: pythonp
[\[listing:for_else\]](#listing:for_else){reference-type="ref"
reference="listing:for_else"} kada je slovo pronađeno Unesi neki tekst:
riba ribi grize rep Unesi slovo koje se traži: a Slovo \"a\" JE
pronađeno!
:::

::: pythonp
[\[listing:for_else\]](#listing:for_else){reference-type="ref"
reference="listing:for_else"} kada slovo nije pronađeno Unesi neki
tekst: riba ribi grize rep Unesi slovo koje se traži: x Slovo \"x\" NIJE
pronađeno!
:::

Za vježbu pokušajte izvesti prijašnji program bez da koristite
komponentu `else`{.python} petlje `for`{.python}!

### Preskoči korak u petlji

Jednostavna izjava `continue`{.python} čim se izvrši prelazi na idući
korak petlje u kojoj se nalazi. Ova izjava se koristi kada je potrebno
preskočiti korak u petlji.

::: pythonp
[\[listing:for_continue\]](#listing:for_continue){reference-type="ref"
reference="listing:for_continue"} n k t k s t
:::

Na prikazani način možemo izvršiti petlju koja se izvršava za određen
broj slučajeva, ali se preskaču slučajevi koji (ne) zadovoljavaju
određene uvjete.

Pogledajmo još pobliže u pogreške i upravljanje njima pa se možemo
baciti i na konkretnije programe.

## Pogreške i pokušaji

Javljanje pogrešaka je normalna stvar u programiranju, a kod programskih
jezika viših razina se pokušava čim jasnije korisniku dati do znanja što
je i gdje je pošlo po krivu. Python omogućava i presretanje pogrešaka
što nam pruža nove mogućnosti za kontrolu toka programa. Pogledajmo prvo
pobliže Python pogreške, a zatim i kako ih presretati.

Što se dogodi kad Python prilikom izvršavanja kôda naiđe na pogrešku?
Recimo da smo pokušali izvršiti izraz `n + 1`{.python}, a varijabli
`n`{.python} nije pridružena vrijednost.

Usredotočimo se na zadnju liniju. Python javlja `NameError`{.python} s
`name 'n' is not defined`{.python} kao detaljima pogreške. U trenutku
kad je naišao na pogrešku Python je stvorio objekt vrste
`Exception`{.python} (u ovom slučaju `NameError`{.python}) s nekom
porukom. Zatim je prijavio grešku opisanu tim objektom korisniku te
prekinuo izvršavanje. Sve linije prije zadnje su ispis koda u kojemu se
dogodila greška. Ovaj dio može biti vrlo dugačak, ali važno je zapamtiti
da nam je za opis greške najvažnija zadnja linija i u mnogim slučajevima
je dovoljno pročitati samo nju uz informacije u kojoj se točno liniji
kôda javlja pogreška. Ispis ranijeg kôda služi lakšem pronalaženju
greške u vlastitom ili tuđem kôdu i posebno je koristan kod većih
programa.

Također, postoji više vrsta grešaka koje je najlakše pronaći u
interaktivnom radu:

Dapače, ukoliko prilikom učenja Pythona ne vidite često kojekakve
pogreške, šanse su da trebate promijeniti pristup! Upravo prikazana
greška pojednostavljeno kaže \"Greška u vrsti podataka: brojevi i tekst
se ne mogu zbrajati\".

Najčešće pogreške koje Python javlja su:

- **SyntaxError** ---javlja se kada kôd nije dobro formiran; najčešće
  pogreške ovog tipa su neujednačene zagrade ili navodnici, manjak
  zareza ili dvotočki na mjestima na kojima se moraju pojavljivati i
  slično

- **NameError** ---javlja se kada koristimo neki naziv čija vrijednost
  nije poznata; na primjer pokušavamo koristiti varijablu `x`{.python}
  prije no što smo toj varijabli pridružili neku vrijednost

- **TypeError** ---javlja se kada se operacija ili funkcija pokuša
  provesti s krivom vrstom vrijednosti; na primjer `"1" + 1`{.python}
  ili `round("tekst")`{.python}

- **ValueError** ---javlja se kada se operacija ili funkcija pokuša
  provesti s točnom vrstom vrijednosti, ali s vrijednosti s kojom nije
  moguće provesti tu operaciju ili funkciju; na primjer
  `math.sqrt(-1)`{.python}

- **ImportError** ---javlja se kada korisnik pokuša uvesti modul koji ne
  postoji (ili ga Python ne zna pronaći, što dođe na isto); na primjer
  **import nisamtu** (pod uvjetom da niste sami napisali Python modul
  koji se zove \"nisamtu\")

- **IndexError** ---javlja se kada pokušamo dohvatiti element popisa
  koji nije prisutan; na primjer osmi znak iz stringa koji se sastoji od
  sedam znakova

- **KeyError** ---javlja se kada pokušamo dohvatiti element rječnika
  koji nije prisutan; na primjer element pod nazivom \"title\" iz
  rječnika koji ne sadrži takav ključ[^2]

Kroz iskustvo rada u Pythonu, postaje sve lakše identificirati probleme
kroz vrste pogreški koje Python javlja. Uz to, kroz presretanje
pogrešaka možemo upravljati pogreškama u programiranju što je katkad
korisno. Ipak, dok su kondicionali i petlje standardan i prihvaćen dio
kontrole toka u programskim jezicima, presretanje pogrešaka nije do te
mjere. Ipak, može biti vrlo korisno i to pogotovo u slučaju kada želimo
presresti korisničke greške kako bi mu javili jasnije poruke i
spriječili \"rušenje\" programa. Na primjer, sljedeći program računa i
ispisuje drugi korijen iz unesenog broja.

Kada pokrenemo program i upišemo broj \"2\", program će ispisati:

::: pythonp
[\[listing:pogreske_input_raw\]](#listing:pogreske_input_raw){reference-type="ref"
reference="listing:pogreske_input_raw"} Program je započeo s radom.

Unesi broj: 9 Drugi korijen: 3.0

Pritisni \<enter\> za kraj
:::

Prikazani program jednostavno računa drugi korijen iz korisničkog unosa.
Ali što ako korisnik unese nešto što se ne može interpretirati kao broj
ili unese negativan broj? Evo kako bi izgledao loš unos kada bismo ovaj
program pokrenuli u IDLE-u ili u komandnoj liniji.

::: pythonp
[\[listing:pogreske_input_raw\]](#listing:pogreske_input_raw){reference-type="ref"
reference="listing:pogreske_input_raw"} Program je započeo s radom.

Unesi broj: neću

Traceback (most recent call last): File \"C:/code/try_except_a.py\",
line 7, in \<module\> broj = int(broj) ValueError: invalid literal for
int() with base 10: 'neću'
:::

U prikazanom slučaju vidimo \"sirovu\" grešku koju je javio Python.
Međutim, da smo ovaj program pokrenuli duplim klikom, program bi
jednostavno završio prije no što korisnik može pročitati poruku o
grešci! Iz korisniče perspektive \"program se srušio\". U svakom
slučaju, što želimo postići je: 1) da korisnik uvijek vidi grešku koja
se dogodila i 2) da se korisniku ne prikazuje sirova greška kako ju
javlja programski jezik, već neka poruka specifično namijenjena za naš
program. Kako bismo postigli ovo, Python nam omogućuje korištenje riječi
`try`{.python}. Pogledajmo primjer:

Kada izvršimo program vidjet ćemo da se on ne gasi \"sam od sebe\"
prilikom pogreške, a povratna informacija korisniku nije više interna
poruka od programskog jezika već nešto dizajnirano za ovu specifičnu
namjenu.

::: pythonp
[\[listing:pogreske_input_try\]](#listing:pogreske_input_try){reference-type="ref"
reference="listing:pogreske_input_try"} Program je započeo s radom.

Unesi broj: neću Iz vrijednosti \"neću\" nije moguće izračunati drugi
korijen.

Pritisni \<enter\> za kraj
:::

Slično se ponaša i kada unesemo negativan broj.

::: pythonp
[\[listing:pogreske_input_try\]](#listing:pogreske_input_try){reference-type="ref"
reference="listing:pogreske_input_try"} Program je započeo s radom.

Unesi broj: -1 Iz vrijednosti \"-1\" nije moguće izračunati drugi
korijen.

Pritisni \<enter\> za kraj
:::

Ovaj primjer demonstrira korištenje naredbe `try`{.python} u praksi.
Najjednostavnije korištenje ove naredbe može se sažeti na sljedeći
način:

::: pythonp
Najjednostavniji oblik pokušajalisting:pokusaj_1 try: \<naredbe koje će
se pokušati izvršiti\> except VrstaGreške: \<ako se dogodi bilo kakva
greška u kôdu napisanom pod try, izvršiti će se kôd napisan ovdje\>
:::

`except`{.python} dio može i ne mora primiti neku vrstu pogreške (poput
ValueError). Ako ne napišemo niti jednu vrstu pogreške tada će se kôd
pod `except`{.python} izvršiti u slučaju bilo koje greške. Ako pak
specificiramo neku vrstu greške, kao u primjeru
[\[listing:pogreske_input_try\]](#listing:pogreske_input_try){reference-type="ref"
reference="listing:pogreske_input_try"}, tada će se kôd napisan pod
`except`{.python} izvršiti samo u slučaju te vrste greške. Ne
specificirati vrstu greške je dopušteno, ali se u načelu smatra lošom
praksom jer na taj način naredba `try`{.python} može \"sakriti\" greške
za koje nismo pretpostavili da se mogu dogoditi što znatno otežava
traženje problema u programima. Zato je dijelu `except`{.python} dobro
specificirati točno koje vrste pogreške hvata. Ako želimo hvatati više
vrsta pogrešaka, možemo ponoviti `except`{.python} komponentu naredbe
`try`{.python}. Kao što smo vidjeli, ovoj naredbi je moguće dodati i
`else`{.python} komponentu koja služi odvajanju kôda koji će se izvršiti
samo ako su naredbe u `try`{.python} komponenti uspješno provedene,
odnosno suprotan slučaj od onog u kojem se izvršava `except`{.python}
dio kôda. Zadnja komponenta naredbe `try`{.python} je komponenta
`finally`{.python}. Naredbe napisane u ovom dijelu će se uvijek izvršiti
bez obzira da li je kôd pod `try`{.python} prouzročio grešku ili ne.

::: pythonp
Širi oblik pokušajalisting:pokusaj_2 try: \<naredbe koje će se pokušati
izvršiti\> except VrstaGreške1: \<ako se dogodi greška vrste
VrstaGreške1 u kôdu napisanom pod try, izvršiti će se kôd napisan
ovdje\> \... except VrstaGreške2: \<ako se dogodi greška vrste
VrstaGreške2 u kôdu napisanom pod try, izvršiti će se kôd napisan
ovdje\> else: \<naredbe koje se izvršavaju samo ako je kôd napisan pod
try uspješno izvršen\> finally: \<naredbe koje se uvijek izvršavaju, bez
obzira da li je došlo do greške ili ne\>
:::

Ipak, potpuno raspisanu `try`{.python} naredbu se rijetko vidi i dapače,
primjer koji prikazuje sve ove komponente u praksi bi bio ili vrlo
specijaliziran ili umjetno osmišljen samo kako bi postojao takav
primjer. Također, neke situacije u kojima se tipično koristila
komponenta `finally`{.python} je Python 3 riješio na bolji način. U
daleko najčešćem slučaju, naredba `try`{.python} će koristiti samo jednu
`except`{.python} komponentu i potencijalno `else`{.python} komponentu
kao u primjeru
[\[listing:pogreske_input_try\]](#listing:pogreske_input_try){reference-type="ref"
reference="listing:pogreske_input_try"}.

Kao što vidimo, složena izjava `try`{.python} ima dosta naprednih
mogućnosti. Ipak, ovaj mehanizam se koristi znatno manje nego
kondicionali i petlje. Dapače, ukoliko je nešto moguće izvesti s izjavom
`try`{.python}, ali i s kondicionalima i/ili petljama, kao općenito
pravilo se izbjegava `try`{.python} jer za razliku od kondicionala i
petlja ima više sitnica na koje treba paziti i detalja koji mogu poći po
krivu.

## Korištenje više mehanizama kontrole toka

Proučimo sljedeći jednostavan primjer:

Iako korisniku javljamo `'Unesi broj: '`{.python}, ništa ga ne sprječava
da unese tekst ili bilo što drugo što se ne može interpretirati kao
broj. Česta greška na hrvatskim tipkovnicama je, na primjer, unos \"7ž\"
gdje je slovo \"ž\" slučajno utipkano radi smještaja uz tipku enter, a
na nekim tipkovnicama čak i zauzima dio te tipke. Ako se ovo dogodi,
program će se srušiti jer će redak `n = int(n)`{.python} javiti grešku i
komandna linija će se odmah ugasiti. Kako bismo spriječili takvo
ponašanje i korisniku javili grešku možemo koristiti izjavu
`try`{.python}.

Sada smo presreli pogrešku i prikazali korisniku odgovarajuću poruku.
Ipak, nakon pogreške moramo prekinuti izvršavati program jer bi
hipotetski ostatak programa očekivao da je n broj. Kako bismo ovo
spojili s petljom `while`{.python} da korisniku ponavljamo pitanje sve
dok ne unese cijeli broj?

::: pythonp
[\[listing:input_number_try_while\]](#listing:input_number_try_while){reference-type="ref"
reference="listing:input_number_try_while"} Unesi broj: neću neću se ne
može interpretirati kao cijeli broj, pokušaj ponovo. Unesi broj: 17ž 17ž
se ne može interpretirati kao cijeli broj, pokušaj ponovo. Unesi broj:
17
:::

Prikazani mehanizam možemo koristiti kada želimo osigurati unos cijelog
broja i ponavljati pitanje korisniku sve dok ne unese validan broj. Sada
znamo dovoljno o mehanizmima kontrole toka kako bismo ih iskoristili u
konkretnijim primjerima.

[^1]: U mnogim drugim jezicima se petlja `for`{.python} ponaša
    drugačije, a petlja o kojoj je sada riječ se naziva
    `foreach`{.python}, `for_each`{.python} ili što slično.

[^2]: Rječnici su prikazani kasnije u tekstu.
