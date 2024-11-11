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

### Multiplekser

- Kratek opis, kje se uporablja?
- implementacija z logičnimi vrati za 2:1 MUX...
- maybe kako se zgradi 4:1 MUX (in naprednejše MUX) iz osnovnih (2:1) MUX

## Metode

TODO - Tole je iz navodil, meni se sicer zdi malo neumno: 
V poglavju Metode opišite, ali ste uporabili ad hoc metodo ali ste formalizirali metodo snovanja QCA strukture. Navedite tudi, ali prosto določite urino cono vsaki posamezni QCA celici ali je vaša struktura zasnovana z uporabo strukturiranih pravokotnih urinih con.

### Zasnova logično reverzibilnega 2:1 MUX

- Maybe gre to poglavje pod UVOD?
- Najbolj preprosto da samo uporabimo Fredkinova vrata.
- Opišemo zakaj so Fredkinova vrata primerna za MUX

### Zasnova fizično reverzibilnega 2:1 MUX 

- različne implementacije Fredkinovih vrat s QCA
- zasnova v QCADesignerju
- treba je preverit ali dobimo na izhodih ustrezne vrednosti, določene z bijekcijo, če spremenimo vhodne funkcije v izhodne in obratno (to piše v navodilih)

### Zasnova fizično reverzibilnega 4:1 MUX

- ne vem a je treba najprej tudi zasnovat logično reverzibilno 4:1 MUX pa potem iz tega izhajat, ali lahko gremo kar direkt na fizično reverzibilno implementacijo ???
- različne implementacije Fredkinovih vrat s QCA
- zasnova v QCADesignerju
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


