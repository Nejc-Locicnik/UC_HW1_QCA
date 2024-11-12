# Implementacija MUX s QCA (začasen naslov)

## Abstract

(Napišemo čisto na koncu)

## Uvod

- Motivacija za kvantno procesiranje in QCA kot platformo.

### QCA

- QCA celica, ura, vodila...
- Osnovne QCA strukture (negacija, majoritetna vrata)

### Reverzibilno procesiranje

- kaj je? zakaj je dobro?
- osnovne (1,1) funkcije (identiteta, negacija)
- (3,3) funkcije ki predstavljajo poln fukncijski nabor (CC-NOT oz Toffolijeva vrata, C-SWAP oz Fredkinova vrata)
- nujno mora tukaj bit še pravilnostna tabela za Fredkinova vrata (ker jo bomo kasneje referencali)

### Multiplekser

Multiplekser (oziroma MUX) je logično vezje z 2^n vhodnimi signali, n adresnimi signali in enim izhodnim signalom. Deluje kot stikalo, ki omogoča izbiro enega izmed več vhodov, glede na adresne signale. Slika (REF) prikazuje najbolj osnoven 2:1 multiplekser z dvema vhodnima signaloma, enim adresnim signalom in enim izhodnim signalom.

[Slika: 2:1 multiplekser](images/mux-2-1.pdf)

Multiplekserji imajo več praktičnih primerov uporabe, med katerimi so: izbira podatkov iz različnih virov (pomnilniški čipi, strojne periferne naprave) v računalniških sistemih, časovno multipleksiranje (Time-Division Multiplexing) v digitalnih komunikacijah, usmerjanje analognih signalov in drugi.

Multiplekser predstavlja polni funkcijski nabor, torej je z njim mogoče implementirati poljubno logično funkcijo. Prav tako lahko osnovne (2:1) multiplekserje uporabimo za realizacijo kompleksnejših multiplekserjev (npr. 4:1 MUX, 8:1 MUX...), kot je prikazano na sliki (REF).

[Slika: Realizacija 4:1 multiplekserja z uporabo treh 2:1 multiplekserjev](images/mux-4-1.pdf)

Slika (REF) predstavlja najbolj osnovno logično predstavitev multiplekserja, izvedeno z uporabo osnovnih logičnih vrat AND, OR in NOT.

[Slika: Realizacija 2:1 multiplekserja z uporabo AND, OR in NOT vrat](images/mux-log-vezje-nereverzibilno.pdf)

Vseeno pa nam takšna realizacija multiplekserja ne ustreza, saj vezje ni reverzibilno, kar je očitno že iz neujemanja števila vhodov in števila izhodov. 
Za realizacijo logično reverzibilnega multiplekserja smo se odločili uporabiti Fredkinovo fukncijo (imenovano tudi Controlled SWAP oziroma C-SWAP), definirano s sledečimi logičnimi izrazi:

P = A

Q = (NOT A AND B) OR (A AND C)

R = (NOT A AND C) OR (A AND B)

Če na vhodni signal A vežemo adresni MUX signal in na vhodna signala B in C vežemo vhodna MUX signala, postane realizacija multiplekserja s Fredkinovo funkcijo trivialna: Na izhodu Q dobimo MUX izhodni signal, med tem ko P in R postaneta neuporabna (garbage) izhoda. Za lažjo predstavitev je realizacija 2:1 MUX z uporabo Fredkinovih vrat prikazana na Sliki (REF), kjer signal S0 predstavlja adresni signal multiplekserja in signala A in B predstavljata vhodna signala multiplekserja.

[Slika: Realizacija 2:1 multiplekserja z uporabo Fredkinovih vrat (C-SWAP)](images/mux-fredkin.pdf)

## Metode

TODO - Tole je iz navodil, meni se sicer zdi malo neumno: 
V poglavju Metode opišite, ali ste uporabili ad hoc metodo ali ste formalizirali metodo snovanja QCA strukture. Navedite tudi, ali prosto določite urino cono vsaki posamezni QCA celici ali je vaša struktura zasnovana z uporabo strukturiranih pravokotnih urinih con.

### Realizacija reverzibilnega 2:1 multiplekserja s QCA 

Kot smo ugotovili v poglavju (REF: Multiplekser), za realizacijo 2:1 multiplekserja potrebujemo zgolj eno instanco Fredkinovih vrat. V tem poglavju bomo implementirali različne realizacije Fredkinovih vrat v QCA z uporabo orodja QCADesigner.

#### Prva implementacija Fredkinovih vrat

Najprej smo z orodjem QCADesigner implementirali Fredkinova vrata iz članka (SinghSarinRaj). Postavitev celic je predstavljena na Sliki (REF). Za realizacijo smo uporabili 73 QCA celic in tri urine cikle. Vhodna celica S0 predstavlja adresni signal, vhodni celici A in B pa vhodna signala v multiplekser. Izhodni signal Q predstavlja izhod iz multiplekserja med tem ko izhodna signala P in R predstavljata neuporabna (garbage) izhoda.

[Slika: Realizacija prvih Fredkinovih vrat s QCA](images/fredkin1-layout.pdf)

Rezultati simulacije Fredkinovih vrat so prikazani na Sliki (REF). Primerjava teh rezultatov s pravilnostno tabelo Fredkinovih vrat (REF: pravilnostna tabela Fredkin) potrjuje, da vezje deluje pravilno.

[Slika: Rezultati simulacije prvih Fredkinovih vrat s QCA](images/fredkin1-results.pdf)

#### Druga implementacija Fredkinovih vrat

TODO:
- različne implementacije Fredkinovih vrat s QCA
- zasnova v QCADesignerju
- preveri ali se izhodi ujemajo s pravilnostno tabelo Fredkinovih vrat
- treba je preverit ali dobimo na izhodih ustrezne vrednosti, določene z bijekcijo, če spremenimo vhodne funkcije v izhodne in obratno (to piše v navodilih)

### Realizacija reverzibilnega 4:1 multiplekserja s QCA 

- povemo da je mogoče realizirati naprednejše MUX (npr. 4:1) z uporabo osnovnih 2:1 MUX (referenca na podpoglavje Multiplekser iz poglavja Uvod)
- realiziramo v QCADesignerju (združimo 3 fredkinova vrata in dobimo 4:1 MUX)
- treba je preverit ali dobimo na izhodih ustrezne vrednosti, določene z bijekcijo, če spremenimo vhodne funkcije v izhodne in obratno (to piše v navodilih)

## Rezultati

Primerjava različnih implementacij MUX:
- število QCA celic
- površina oz. ploščina vezja
- še kaj?

## Zaključek

(Napišemo čisto na koncu)

## Doprinosi avtorjev


## Literatura

[SinghSarinRaj](https://doi.org/10.1016/j.micpro.2017.05.017)
