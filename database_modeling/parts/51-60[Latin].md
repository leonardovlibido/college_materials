## 51. Objasniti dilemu „entitet ili atribut“?
Ako imamo složen atribut, možemo da ga modeliramo kao:
- jedan složen atribut
- više prostih atributa
- jedan entitet
- Na osnovu čega donosimo odluku?
- Čak i za proste atribute može da se postavi pitanje da li su oni možda ipak entiteti?

Argumenti za “atribut”:
- ako jednom entitetu odgovara tačno jedna vrednost “atributa”
- ako predstavlja jednostavnu skalarnu vrednost koja opisuje entitet
- ako više entiteta može da ima iste vrednosti, a da one nisu međusobno uslovljene
  - tj. menjanje vrednosti za jedan entitet ne povlači njeno menjanje za drugi
- ako važi slično i kada je to “atribut” u različitim skupovima entiteta

Složen atribut može da ima smisla:
- ako želimo da sačuvamo internu strukturu, ali ona ima značaja samo interno
- ako više entiteta može da ima iste vrednosti, a da one nisu međusobno uslovljene
  - npr, ako “adresa” obuhvata grad, ulicu i broj, onda više zaposlenih može da ima istu adresu, a da
to ne znači da žive zajedno, pa se one i dalje mogu odvojeno menjati
- ako važi slično i kada je to atribut u različitim skupovima entiteta

“Atribut” mora da preraste u entitet:
- ako nekom drugom entitetu odgovara istovremeno više vrednosti tog atributa
- ako postoji međuzavisnost vrednosti atributa
- npr. ako više entiteta ima istu vrednost atributa i on se promeni za jedan entitet, onda mora da
se promeni i za ostale

## 52. Objasniti dilemu „entitet ili odnos“?
Odnos može da bude ”odnos”:
- Ako svi njegovi atributi odnose strikno na jednu instancu odnosa
  - tj. nema redundantnosti


- Odnos mora da preraste u “entitet”:
  - Ako se neki od njegovih atributa odnosi istovremeno na više instanci
odnosa
    - redundantnost povlači uočavanje/izdvajanje novog entiteta i podizanje složenosti
odnosa

- U velikom broju slučajeva je “jednako ispravno” da nešto bude bilo odnos
bilo entitet

## 53. Objasniti dilemu „složeni odnos ili više binarnih odnosa“?
Većina složenih odnosa može da se “podeli” na više binarnih
agregiranih odnosa
- Da li je bolje podeliti ih ili ih ostaviti?
- Složene odnose ima smisla podeliti na više jednostavnijih
isključivo ako svaki od dobijenih odnosa ima svoj semantički smisao
u posmatranom domenu
- Čak i tada, ako je semantika očiglednija iz složenog odnosa, onda bi
taj složeni odnos trebalo da ostane

## 54. Objasniti dilemu „agregacija ili ternarni odnos“?
- Ovo pitanje je slično prethodnom:
  - Agregirani odnos podrazumeva da se agregirani odnos može
posmatrati kao skup entiteta (ili skup odnosa)
  - No, to može da bude i veštački napravljeno
  - Šta je i kada bolje uraditi?

- Agregirani odnosi su bolje rešenje:
  - Ako nekada postoji samo deo odnosa, a nekada ceo (tj. nekada samo deo koji se
agregira, a nekada pun odnos)
  - Ako se deo atributa odnosa ne tiče celine odnosa već samo njegovog dela, koji
uključuje manje entiteta
- U ostalim slučajevima obično je bolje da se koriste složeni odnosi

## 55. Kako se entiteti i odnosi ER modela prevode u relacioni model?
Svaki entitet se prevodi u relaciju
- Atributi entiteta se prevode u atribute relacije
- Složeni atributi se prevode u više prostih atributa
- Ključni atributi se prevode u primarni ključ

Skoro svaki odnos se prevodi u relaciju
- Atributi odnosa se prevode u atribute relacije
- Dodaju se i ključni atributi uključenih entiteta
- Primarni ključ dobijene relacije čine primarni ključevi relacija koje
odgovaraju uključenim entitetima
- Primarnom ključu se dodaju i svi ključni atributi odnosa
- Strani ključevi su primarni ključevi učesnika

Ako je odnos 1:0..1
- onda ne mora da se pravi dodatna relacija za odnos
- atributi odnosa se dodaju relaciji koja odgovara entitetu sa kardinalnošću 1
- OPREZNO! Ako odnos nije 1:0..1 nego 0..1:0..1, onda se dobija potencijalno
redundantno rešenje

## 56. Kako se hijerarhije ER modela prevode u relacioni model?
Hijerarhije mogu da se reše na tri osnovna načina:
- Cela hijerarhija u jednu relaciju
- Svaki entitet u posebnu relaciju
  - tj. kao da se radi o “običnom” osnosu entiteta
- Svaki entitet-list u posebnu relaciju, ali tako da uključi sve nasleđene
atribute

Sve u jednu relaciju
- Jedna relacija koja obuhvata sve atribute koji postoje u hijerarhiji
  - Za svaki entitet se koristi samo deo atributa
  - ...ostali imaju nedefinisane (prazne) vrednosti
- Efikasna upotreba
- Ako je hijerarhija sa preklapanjem(može instanca da bude član dve'potklase') onda mora da postoji način da se za svaki
konkretan skup entiteta hijerarhije proveri da li mu entitet pripada
  - ili po jedan dodatan atribut
  - ili se proverava da li su ostali odgovarajući atributi neprazni
- Ako je hijerarhija sa pokrivanjem(mora da pripada bar jednoj potklasi) onda je potreban uslov da svaka torka relacije
pripada bar jednom konkretnom skupu entiteta
  - obično nije problem definisati

Svaki entitet posebno
- Za svaki entitet se pravi po relacija, sa stranim ključem na neposrednu baznu
relaciju
  - Svaka relacija obuhvata samo one atribute koji su za nju specifični
    - ...i još atribute ključa bazne relacije
    - ...koji se koriste kao strani ključ
- Upotreba zahteva česta spajanja i potencijalno je neefikasna
  - ali je na nivou konceptualnog i logičkog modela prihvatljiva
- Ako je hijerarhija sa pokrivanjem onda mora da se obezbedi dodatno sredstvo za
proveru pokrivenosti

Listovi posebno
- Za svaki entitet se pravi po relacija, sa stranim ključem na neposrednu baznu
relaciju
  - Svaka relacija obuhvata atribute koji su za nju specifični
    - ...i SVE atribute SVIH baznih klasa
    - ... atributi ključa bazne relacije se koriste kao strani ključ
- Upotreba pojedinačnih entiteta je efikasna
- Pretraživanje baznog skupa entiteta je neefikasno (unija)
- Ako je hijerarhija sa preklapanjem onda ovakvo rešenje može da napravi probleme
  - mogu da se redundantno ponavljaju delovi entiteta...


Poslednja dva metoda mogu da se kombinuju u različitim delovima hijerarhije


## 57. Kako se slabi entiteti ER modela prevode u relacioni model?
- Slab entitet i odgovarajući odnos se modeliraju jednom relacijom
- Dodaje se i ključni atribut vezanog jakog entiteta, kao deo primarnog ključa

## 58. Šta su „dijagrami tabela (relacija)“?
Dijagram tabela je uglavnom relacioni model/dijagram. Pokazuje veze između tabela - primarne i strane ključeve.
- Često se pogrešno nazivaju „ER dijagrami“
- To nisu ER dijagrami nego dijagrami tabela (relacija)
- Oznake i termini su obično tabele/kolone/ključevi
- Prilagođeni su logičkom i (posebno) fizičkom nivou relacionog modela
- Semantika odnosa je predstavljena u meri u kojoj to
dopušta relacioni model

## 59. U čemu se dijagrami tabela suštinski razlikuju od ER dijagrama? Koji se kada koriste?
(Nema nigde baš odgovor u slajdovima, ali cenim da je ovo fino.)

Dijagram tabela je prilagođen logičkom i (posebno) fizičkom nivou relacionog modela, dok je ER dijagram bolje prilagođen najvišem nivou
posmatranja informacija, tj. semantičkom i konceptualnom modeliranju.

Iz tabele dijagrama je teže zaključiti odnose među tabelama, dok je u ER modelu lakše.

Zato se generalno počinje ER-dijagramom, koji se posle prevodi u Dijagram tabela.

## 60. Kako se označavaju ključevi u dijagramima tabela?
ako kolona pripada primarnom ključu, onda se ona obeležava sa
- simbolom +
- oznakom PK
- crtežom ključa

ako kolona pripada stranom ključu
- simbol #
- oznaka FK (ili PF, ako je i primarni i strani, tzv. slabi entitet)
- crtež ključa sa strelicom
- obično i iskošen naziv
