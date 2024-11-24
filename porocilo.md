# Implementacija MUX s QCA (začasen naslov)

## Abstract

> [!NOTE]
> TODO:
>
> Napišemo čisto na koncu

## Uvod

S sodobnim razvojem nanotehnologij tako na tehnološkem (razvoj novih materialov in načinov njihove obdelave) kot na procesnem področju (implementacija nadzorljivih dinamičnih procesov) se posledično razvija tudi področje nanoračunalništva.
Trenutni kazalniki razvoja na področju nanoračunalništva dolgoročno nakazujejo na pospešen razvoj kvantnih računalnikov. Ti bodo ob adopciji v industriji prinesli prednosti, kot so energijska varčnost, pospešitev obstoječih algoritmov in minimizacija procesnih enot.

Ena izmed perspektivnih tehnologij, ki omogoča zgoraj opisane prednosti kvantnega računalništva je QCA (angl. _quantum-dot cellular automata_).

### QCA

Delovanje QCA procesne strukture temelji na zakonih delovanja kvantne fizike.
Najmanjša osnovna komponenta QCA je kvantna ali QCA celica.
Ta je laično predstavljena kot dvodimenzionalna struktura kvadratne oblike s štirimi kvantnimi pikami v robovih celice.
Vsaka kvantna pika ima pozitiven električni naboj, ki privlači dva elektrona, ki sta ujeta znotraj celične strukture.
Zaradi električnih odbojnih sil med obema elektronoma, se ta ne moreta istočasno nahajati v isti kvantni piki.
Kvantne pike so v celici povezane s štirimi tuneli, ki omogočajo prosto prehajanje ali tuneliranje elektronov med sosednjimi kvantimi pikami.
Shematski prikaz kvantne celice je prikazan na sliki (REF).

[Slika: Struktura kvantne celice]()

Elektrona v kvantni celici se vedno postavita v energetsko najbolj ugodno pozicijo, kar je ena izmed diagonalnih leg (polarizacija $P = +1$ ali $P = -1$).
S prostim prehodom elektronov v celici je omogočen prenos informacij med sosednjimi kvantnimi celicami.
Ker lega elektronov v celici vpliva na lego elektronov v sosednjih celicah, lahko s skrbno postavljenimi celicami izdelamo minimalne strukture, kot so vodila ali druge logične strukture.

Na sliki (REF) sta predstavljena osnovna gradnika za dvovrednostno procesiranje v QCA. To sta negacija (`NOT`) in majoritetna vrata (delimo jih na `AND` in `OR` del), ki skupaj tvorita poln funkcijski nabor, s katerim lahko izrazimo katerokoli poljubno funkcijo.

[Slika: Osnovna gradnika v QCA]()

Poleg gradnikov potrebujemo tudi strukturo za prenos informacij med gradniki.
Tu uporabimo vodila, ki so lahko realizirana v ortogonalni ali diagonalni izvedbi.
Pri slednji moramo paziti, da se z vsako celico prenešen podatek negira.
Slika (REF) prikazuje shematski prikaz obeh vrst vodil.

[Slika: Vodila]()

### Reverzibilno procesiranje

Za učinkovito realiazacijo kvantnega procesiranja potrebujemo vezje zasnovati z metodološkim pristopom reverzibilnosti.
Ta pristop sloni na definiciji logične reverzibilnosti, ki pravi, da mora biti njegova prevajalna funkcija bijektivna.

Pravilnostne tabele bijektivnih funkcij tipa (1,1) (funkcije z enim vhodom in enim izhodom) so predstavljene na sliki (REF).

[Slika: Funkcije (1,1)]()

Najboljšo osnovo za prehod na reverzibilno procesiranje naj bi predstavljale funkcije tipa (3,3).
Tu izmed vseh funkcij izpostavljamo Toffolijeva vrata (Controlled-controlled-not ali `CCNOT`), ki sama po sebi predstavljajo poln funkcijski nabor.
Shematski prikaz je prikazan na sliki (REF).

[Slika: Shematski prikaz Toffolijevih vrat]()

Prav tako izpostavljamo univerzalno Fredkinovo funkcijo (Controlled-swap ali `CSWAP`), katere pravilnostna tabela je napisana v tabeli (REF).
Ta funkcija prav tako predstavlja poln funkcijski nabor.

[Tabela: Pravilnostna tabela Fredkinove funkcije tipa (3,3)]()

### Multiplekser

Multiplekser (oziroma MUX) je logično vezje z $2^n$ vhodnimi signali, $n$ adresnimi signali in enim izhodnim signalom.
Deluje kot stikalo, ki omogoča izbiro enega izmed več vhodov, glede na adresne signale.
Slika (REF) prikazuje najbolj osnoven 2:1 multiplekser z dvema vhodnima signaloma, enim adresnim signalom in enim izhodnim signalom.

[Slika: 2:1 multiplekser](images/mux-2-1.pdf)

Multiplekserji imajo več praktičnih primerov uporabe, med katerimi so: izbira podatkov iz različnih virov (pomnilniški čipi, strojne periferne naprave) v računalniških sistemih, časovno multipleksiranje (Time-Division Multiplexing) v digitalnih komunikacijah, usmerjanje analognih signalov in drugi.
Multiplekser predstavlja polni funkcijski nabor, torej je z njim mogoče implementirati poljubno logično funkcijo.
Prav tako lahko osnovne 2:1 multiplekserje uporabimo za realizacijo kompleksnejših multiplekserjev (npr. 4:1 MUX, 8:1 MUX...), kot je prikazano na sliki (REF).

[Slika: Realizacija 4:1 multiplekserja z uporabo treh 2:1 multiplekserjev](images/mux-4-1.pdf)

Slika (REF) predstavlja najbolj osnovno logično predstavitev multiplekserja, izvedeno z uporabo osnovnih logičnih vrat `AND`, `OR` in `NOT`.

[Slika: Realizacija 2:1 multiplekserja z uporabo AND, OR in NOT vrat](images/mux-log-vezje-nereverzibilno.pdf)

Vseeno pa nam takšna realizacija multiplekserja ne ustreza, saj vezje ni reverzibilno, kar je očitno že iz neujemanja števila vhodov in števila izhodov.
Za realizacijo logično reverzibilnega multiplekserja smo se odločili uporabiti Fredkinovo fukncijo (imenovano tudi Controlled SWAP oziroma C-SWAP), definirano s sledečimi logičnimi izrazi (za vhodne signale $S0$, $A$ in $B$):

$$
\begin{align}
P &= S0 \\
Q &= (\text{NOT } S0 \text{ AND } A) \text{ OR } (S0 \text{ AND } B) \\
R &= (\text{NOT } S0 \text{ AND } B) \text{ OR } (S0 \text{ AND } A)
\end{align}
$$

Realizacija multiplekserja s Fredkinovo funkcijo je trivialna: Na izhodu $Q$ dobimo MUX izhodni signal, med tem ko $P$ in $R$ postaneta neuporabna (garbage) izhoda.
Za lažjo predstavitev je realizacija 2:1 MUX z uporabo Fredkinovih vrat prikazana na Sliki (REF), kjer signal $S0$ predstavlja adresni signal multiplekserja in signala $A$ in $B$ predstavljata vhodna signala multiplekserja.

[Slika: Realizacija 2:1 multiplekserja z uporabo Fredkinovih vrat (C-SWAP)](images/mux-fredkin.pdf)

## Metode

TODO - Tole je iz navodil, meni se sicer zdi malo neumno:
V poglavju Metode opišite, ali ste uporabili ad hoc metodo ali ste formalizirali metodo snovanja QCA strukture. Navedite tudi, ali prosto določite urino cono vsaki posamezni QCA celici ali je vaša struktura zasnovana z uporabo strukturiranih pravokotnih urinih con.

### Realizacija reverzibilnega 2:1 multiplekserja s QCA

Kot smo ugotovili v poglavju (REF: Multiplekser), za realizacijo 2:1 multiplekserja potrebujemo zgolj eno instanco Fredkinovih vrat.
V tem poglavju bomo implementirali različne realizacije Fredkinovih vrat v QCA z uporabo orodja (REF: `QCADesigner`).

#### Prva implementacija Fredkinovih vrat

Najprej smo z orodjem `QCADesigner` implementirali Fredkinova vrata iz članka (SinghSarinRaj).
Postavitev celic je predstavljena na sliki (REF).
Za realizacijo smo uporabili 73 QCA celic in tri urine cikle.
Vhodna celica $S0$ predstavlja adresni signal, vhodni celici $A$ in $B$ pa vhodna signala v multiplekser.
Izhodni signal $Q$ predstavlja izhod iz multiplekserja medtem ko, izhodna signala $P$ in $R$ predstavljata neuporabna (garbage) izhoda.

[Slika: Realizacija prvih Fredkinovih vrat s QCA](images/fredkin1-layout.pdf)

Rezultati simulacije Fredkinovih vrat so prikazani na sliki (REF).
Primerjava teh rezultatov s pravilnostno tabelo Fredkinovih vrat (REF: pravilnostna tabela Fredkin) potrjuje, da vezje deluje pravilno.

[Slika: Rezultati simulacije prvih Fredkinovih vrat s QCA](images/fredkin1-results.pdf)

#### Druga implementacija Fredkinovih vrat

Za drugo različico implementacije Fredkinovih vrat smo si izbrali članek (SasamalSinghGhanekar). Postavitev celic je predstavljena na sliki (REF). Tokrat smo za realizacijo uporabili 68 celic in tri urine cikle. Vhodni in izhodni signali imajo zopet enaka poimenovanja.

[Slika: Realizacija drugih Fredkinovih vrat s QCA](images/fredkin2-layout.pdf)

Rezultati simulacije so predstavljeni na sliki (REF). Po podrobnem pregledu lahko ugotovimo, da se rezultati ne ujemajo popolnoma s pravilnostno tabelo Fredkinovih vrat. Napaka se pojavi, ko so vhodni signali S0, A in B nastavljeni na 1, 1, in 0, v tem zaporedju. Izhodni signal R bi v tem primeru moral biti nastavljen na 1, mi pa smo dobili izhodno vrednost 0.
Kljub ugotovljeni napaki bi to vezje lahko uporabili za implementacijo multiplekserja, saj se napaka pojavi zgolj na neuporabnem (garbage) izhodnem signalu. Glavni izhodni signal Q, ki predstavlja izhod multiplekserja, ostaja "nepokvarjen" in deluje skladno s pričakovanji.

[Slika: Rezultati simulacije drugih Fredkinovih vrat s QCA](images/fredkin2-results.pdf)


#### Tretja implementacija Fredkinovih vrat

Za tretjo različico implementacije Fredkinovih vrat smo si izbrali članek (https://link.springer.com/article/10.1007/s11227-022-04939-w). Postavitev celic je predstavljena na sliki (REF). Tokrat smo za realizacijo uporabili 30 celic v treh slojih (za prehod), ki se izvede v dveh urinih ciklih. Vhodni in izhodni signali imajo zopet enaka poimenovanja.

Ta realizacija je v primerjavi s prvima dvema bistveno bolj kompaktna. Dobra je tudi njena simetričnost, ki dovoljuje različne orientacije/konfiguracije na površini iste velikosti.

[Slika: Realizacija tretjih Fredkinovih vrat s QCA](images/fredkin3-layout.pdf)

Rezultati simulacije Fredkinovih vrat so prikazani na sliki (REF).
Primerjava teh rezultatov s pravilnostno tabelo Fredkinovih vrat (REF: pravilnostna tabela Fredkin) potrjuje, da vezje deluje pravilno.

[Slika: Rezultati simulacije tretjih Fredkinovih vrat s QCA](images/fredkin3-results.pdf)

> [!NOTE]
> TODO:
>
> - različne implementacije Fredkinovih vrat s QCA
> - zasnova v QCADesignerju
> - preveri ali se izhodi ujemajo s pravilnostno tabelo Fredkinovih vrat
> - treba je preverit, ali dobimo na izhodih ustrezne vrednosti, določene z bijekcijo, če spremenimo vhodne funkcije v izhodne in obratno (to piše v navodilih)

### Realizacija reverzibilnega 4:1 multiplekserja s QCA

Realizacija 4:1 RMUX je kot je opisano (ref nazaj na 2.2 k je standard 4:1 slika) iz vidika logike enostavna, saj lahko kaskadno dodajamo 2:1 multipleksorje (npr. 3x 2:1 MUX za 4:1 MUX, 7x 2:1 MUX za 8:1 MUX).

Na voljo imamo prvo in tretjo različico 2:1 RMUX realizacije, saj druga ni delovala. Za poizkus smo se odločili za tretjo različico, saj je bistveno bolj kompaktna in se izvede v samo dveh urinih fazah. V teoriji bi se potem 4:1 RMUX lahko izvedel v enem urinem ciklu (4 fazah).

Na koncu se je izkazalo, da je kompaktnost, za katero smo mislili da je prednost, dejansko slabost. Nikakor nam ni uspelo povezati izhod enega 2:1 RMUX-a na vhod drugega. Problem je pri poziciji vhodov. Edina možnost, kjer konstanta ob strani ne popači vhoda ali vhod ne popači izhoda za kontrolni signal ($P$) je, da signal pripeljemo po diagonali (negacija), ki pa žal ni dovolj močan (pade nazaj v nevtralno stxanje oz. nima dovolj moči, da deluje kot vhod/konstanta). To je prikazano na sliki (REF spodaj), kjer vidimo da sta vhodna signala na srednjem RMUX-u dovolj šibka, da vse celice srednjega RMUX-a konvergirajo v stanje 0 (-1 polarizacija), zaradi konstant. 

[Slika: Poizkus realizacije 4:1 RMUX](images/4_to_1_MUX_attempt.pdf)

Če bi takšna konfiguracija delovala bi jo lahko enostavno razširili na 8:1 RMUX. Iz teh poskusov smo ugotovili, da ob preveč kompaktnih realizacijah nimamo dovolj fleksibilnosti za vodila in jih je težko uporabiti kot bloke za bolj kompleksne logične funkcije. V tem primeru je bolje ustvariti čisto drugo realizacija QCA.


> [!NOTE]
> TODO:
>
> - povemo, da je mogoče realizirati naprednejše MUX (npr. 4:1) z uporabo osnovnih 2:1 MUX (referenca na podpoglavje Multiplekser iz poglavja Uvod)
> - realiziramo v QCADesignerju (združimo 3 fredkinova vrata in dobimo 4:1 MUX)
> - treba je preverit, ali dobimo na izhodih ustrezne vrednosti, določene z bijekcijo, če spremenimo vhodne funkcije v izhodne in obratno (to piše v navodilih)

## Rezultati

> [!NOTE]
> TODO:
>
> Primerjava različnih implementacij MUX:
>
> - tip mux (2:1 ali 4:1)
> - število QCA celic
> - površina oz. ploščina vezja
> - razpršitev energije (dunno kje to pogledas)
> - število urinih con

## Zaključek

> [!NOTE]
> TODO:
>
> Napišemo na koncu

## Doprinosi avtorjev

> [!NOTE]
> TODO
>
> **Anže Arhar:**
>
> - Uvod
> - Izdelava slik
>
> **Kristjan Kostanjšek:**
>
> - Podpoglavje Multiplekser
> - Prvi dve implementaciji fredkinovih vrat
>
> **Nejc Ločičnik:**
>
> - Tretja implementacija fredkinovih vrat
> - Poskus reverzibilnega 4-to-1 MUX na podlagi tretjih fredkinovih vrat
## Literatura

[Reference](references.bib)
