amazon-techon-challenge-tdc
===========================
Problema
Tower Defense Combinatorial (TDC) reprezintă o îmbinare între jocul clasic de "tower defense" și exprimarea faptului că războiul purtat pe teren propriu are mereu victime colaterale.
Axat pe a distruge gândacii care vor să invadeze fragila noastră casă, scopul jocului este de a supraviețui cât mai multor hărți utilizând cât mai puține resurse. În acest sens, regulile pentru TDC pornesc de la un set simplu:

Acțiunea are loc pe o hartă bidimensională, pe care se află un drum ce leagă două puncte: poziția de intrare a gândacilor și destinația lor. Harta este reprezentată printr-o matrice, pe care sunt marcate punctul de intrare al inamicilor prin "E", iar punctul de ieșire prin "X". Drumul este marcat prin 1, iar restul matricii prin 0.
Pentru o hartă iți este dat inițial un total de viață și unul de bani. De asemenea specificate sunt costul pentru construcția unui turn de apărare, raza unui turn și recompensa pentru uciderea unui gândac. Raza unui turn reprezintă diferența maximă în modul pe X sau Y între poziția turnului și a inamicului (metrică supremum, sau Cebisev).
Atunci când un gândac își atinge destinația finală - pozitia marcată prin X - din viața ta se va scade viața totală ramasă a inamicului. Dacă viața iți ajunge la zero, jocul pe hartă se încheie.
Poți plasa la orice moment oricate turnuri iți permit resursele. Nu pot fi construite două turnuri suprapuse. Nu poate fi construit un turn pe drumul gândacilor.
În fiecare cadru ("frame"), fiecare gândac aflat pe hartă se deplasează cu un pătrățel. Deplasarea se face fie pe verticală fie pe orizontală, dar nu pe amândouă simultan. La aceeași poziție se pot afla mai mulți gândaci simultan.
În fiecare cadru, fiecare turn poate să tragă în maxim un inamic aflat în raza sa.
Dacă viața unui gândac ajunge la zero, moare și primești o recompensă în resurse.
Setul de reguli ce diferențiază această variantă a jocului față de instanțele clasice sunt:

Un gândac poate avea una sau mai multe culori, fiecare cu o viață specifică. Viață totală a unui inamic este dată de totalul pe toate culorile.
Turnurile pot fi specificate oricum, în orice combinație de culori disponibile pe hartă jucată. Un turn va trage mereu doar folosind combinația înițial asignată. Odată construit, un turn nu mai poate fi modificat sau dărâmat.
Unul dintre cele mai importante aspecte ale jocului este penalitatea pentru exces de fortă ("overkill"): dacă un turn face mai mult prejudiciu ("damage") pe o culoare decât are gandacul vizat pe respectiva culoare, diferența dintre viața gândacului pe acea culoare și damage-ul realizat de turn va fi scazută din totalul tău de viața. Dacă viața ta ajunge la 0 în acest punct, jocul pe hartă se încheie.
Scor
Sistemul de scor este specificat astfel:
Dacă nu ai oferit o soluție validă pentru o hartă, nu primești nici-un punct.
Dacă ai oferit o soluție validă pentru o hartă, punctele asociate cu acea soluție sunt reprezentate de restul de bani ramași după ce toți gândacii și-au încheiat activitatea.
Dintre toate soluțiile oferite pentru o hartă, va fi luată în considerare cea cu cel mai ridicat scor asociat.
Punctajul total este dat de suma scorurilor pentru hărțile prezentate.
Câstigator va fi jucatorul cu cel mai mare scor.

Intrare
Vor fi date mai multe hărți, fiecare cu specificațiile proprii. Fiecare hartă va avea un nume unic. Fișierele cu soluții trebuie prefixate cu numele fișierului hărții pe care o rezolvă.

Starea inițială este dată de o serie de parametrii numerici specificați la începutul fișierului cu soluții:

starting_life=<Viața cu care pornește jucătorul>
starting_money=<Banii cu care pornește jucătorul>
tower_range=<Raza în care poate trage turnul>
tower_cost=<Costul contruirii unui nou turn>
reward_per_bug=<Banii câștigați în urma omorârii unui gândac>
Parametrii fiecărui gândac, împreună cu valoarea cadrului în care întră, sunt dați după parametrii stării înițiale (o linie pentru fiecare gândac)

<Nume Gândac> <Culoare1>=<Valoare Culoare 1> ... <CuloareN>=<Valoare Culoare n> frame=<Cadrul în care întră gândacul>
Ultima secțiune din fișierul de intrare o reprezintă specificația hărții. Aceasta va fi descrisă de o matrice pătratică unde "0" reprezintă o casuță goală, "1" reprezintă o casuță parte din drum, "E" reprezintă punctul de întrare al gândacilor, iar "X" destinația lor.

Solutia
Fișierul în sine va fi compus dintr-o serie de acțiuni. Fiecare acțiune poate fi de două tipuri:

Construcție turn
action=new_tower
Salvă turn
action=shoot
Fiecare tip de acțiune are un set de parametri. Aceștia sunt:

Construcția de turn

Frame-ul la care are loc
frame=<numarul cadrului>
Numele turnului construit, unic pe această hartă
name=<numele turnului>
Poziția la care se construiește turnul. Aceasta este specificată într-un sistem de coordonate cu (0,0) în colțul din stânga sus al hărții
position=<X>,<Y>
Culorile salvei pe care o produce turnul și valoarea pe fiecare culoare
colors=<Nume Culoare>:<Valoare Culoare>,...
Tragerea unei salve

Frame-ul la care are loc
frame=<Numarul Cadrului>
Numele turnului care trage
tower_name=<Numele Turnului>
Numele gândacului în care trage turnul
bug_name=<Numele Gândacului>
Exemple scurte
Exemplu 1

Fie "Bug1" cu următoarea specificație:

Bug1 red=10 blue=14 frame=0
Fie "Tower1" cu următoarea specificație:

colors=red:6,blue:9
Să presupunem că "Bug1" se găsește în raza turnului "Turn1" pentru minim 2 cadre. După prima salvă, viața rămasă pentru "Bug1" va fi:

10Red	14Blue - 
6Red	9Blue
=
4Red	5Blue
    
Dacă se trage înca o salvă, atunci viața rămasă pentru "Bug1" va fi:

4Red	5Blue -
6Red	9Blue
= 
0Red	0Blue
    
Dar, deoarece damage-ul făcut de turn a depășit viața rămasă a gândacului, totalul de viață al jucătorului va avea de suferit.

Cantitatea aceasta este de:

2Red	4Blue
Ceea ce înseamnă un total de 6 scăzut din viața jucătorului.

Exemplu 2

Fie gândacul:

Bug1 red=10
și turnul:

Tower1 colors=red:13,blue:11
Dacă "Tower1" ar trage măcar o dată în "Bug1", atunci penalitatea de overkill ar fi 14. Ori, aceasta ar însemna mai mult decât are gândacul în sine - 10.

În această situație este mai avantajos ca "Tower1" sâ nu tragâ deloc în "Bug1".

Exemplu 3

Fie gândacii

Bug1 red=12 blue=30
Bug2 red=16 blue=40
Pentru a omorî acești gândaci, am putea construi:

Tower1 colors=red:2,blue:5
Acest turn ar necesita 14 salve pentru a omorî ambii inamici. Dacă aceștia se află în raza pentru mai puțin de 14 frame-uri, acest turn nu mai reprezintă o soluție.

O alegere mai bună în această situație ar fi:

Tower2 colors=red:4,blue=10
Acest turn ar necesita doar 7 salve pentru a omori cei doi gândaci.

Exemplu Complet
Având harta de intrare

starting_life=3
starting_money=50
tower_range=2
tower_cost=10
reward_per_bug=4
 
B1 red=57 blue=39 frame=0
B2 red=32 blue=26 frame=3
B3 red=35 blue=64 frame=6
 
0 0 0 0 0
0 1 1 1 E
0 1 0 0 0
0 1 1 0 0
0 0 1 0 0
0 0 1 X 0
O soluție validă ar putea fi:

action=new_tower
frame=0
name=tower_0
position=2,2
colors=red:9
 
action=new_tower
frame=0
name=tower_1
position=3,2
colors=red:7,blue:13
 
action=shoot
frame=0
tower_name=tower_0
bug_name=B1
 
action=shoot
frame=1
tower_name=tower_0
bug_name=B1
 
action=shoot
frame=1
tower_name=tower_1
bug_name=B1
 
action=shoot
frame=2
tower_name=tower_0
bug_name=B1
 
action=shoot
frame=2
tower_name=tower_1
bug_name=B1
 
action=shoot
frame=3
tower_name=tower_0
bug_name=B2
 
action=shoot
frame=3
tower_name=tower_1
bug_name=B1
 
action=shoot
frame=4
tower_name=tower_0
bug_name=B2
 
action=shoot
frame=4
tower_name=tower_1
bug_name=B2
 
action=shoot
frame=5
tower_name=tower_1
bug_name=B2
 
action=shoot
frame=6
tower_name=tower_0
bug_name=B1
 
action=shoot
frame=7
tower_name=tower_1
bug_name=B3
 
action=shoot
frame=8
tower_name=tower_1
bug_name=B3
 
action=shoot
frame=9
tower_name=tower_1
bug_name=B3
 
action=shoot
frame=10
tower_name=tower_1
bug_name=B3
 
action=shoot
frame=11
tower_name=tower_1
bug_name=B3
Anexă: Secvenționarea Evenimentelor și Limite
În cadrul unui "frame", acțiunile au loc în ordinea următoare:

Se construiesc turnurile
Se miscă gândacii
Intră gândacii pe hartă
Turnurile trag în gândaci
Se calculează gândacii morți
Se calculează damage-ul (direct + colateral)
Se validează dacă utilizatorul moare. În caz afirmativ, soluția este declarată invalidă.
Se acordă recompensele obținute
Se verifică terminarea execuției pe această hartă.
Limite generale al soluțiilor:

Un turn poate trage cu maxim 5 culori (nici gândacii nu pot avea mai mult de 5 culori)
Fișierele cu soluții pot avea maxim 100Mb
Numele unui turn poate avea maxim 16 caractere
O linie poate avea maxim 128 caractere
Damage-ul maxim pe culoare al unui turn este de 100,000
Un turn nu poate trage cu damage negativ.



