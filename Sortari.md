- Test sapt 7 (quiz)
	- sa se scrie configuratia tabloului dupa fiecare pas al sortarii prin interschimbare (bubble sort) considerand ca parcugerea se face de la dreapta la stanga / st la dr si un pas contine o comparatie si max o interschimbare

# Sortari simple (pt quiz):
### Bubblesort (interschimbare) 
- ``stanga -> dreapta (crescator)`` (se poate schimba la test)
- ``39 15 71 25`` (asa se cere la test compararea pe pozitii, chiar daca asta nu e implementarea bubblesort)
	- ``15 39 71 25`` = Pas1 (am comparat 39 cu 15)
	- ``15 39 71 25`` = Pas2 (am comparat 39 cu 71)
	- ``15 39 25 71`` = Pas3 (am comparat 71 cu 25)
	- ``15 39 25 71`` = Pas4 (am comparat 15 cu 39)
	- ``15 25 39 71`` = Pas5 (am comparat 39 cu 25)

### Shakersort (sortare prin amestecare)
- primul for de la dreapta la stanga si aplicam bubble sort
- al doilea for de la st la dr si aplicam bubble sort
- ``crescator`` (poate varia la test)
- ``32 19 71 23``
	- Primul for:
	- ``32 19 23 71`` (am comparat 71 cu 23)
	- ``32 19 23 71`` (am comparat 23 cu 71)
	- ``19 32 23 71`` (am comparat 32 cu 19) = Acesta este considerat Pasul 1 (pt ca am ajuns la capat)
	- Al doilea for:
	- ``19 32 23 71`` (am comparat 19 cu 32)
	- ``19 23 32 71`` (am comparat 32 cu 23)
	- ``19 23 32 71`` (am comparat 32 cu 71) = Acesta este Pasul 2 (am ajuns la final)

### Inserstsort (insertie)
- comparam elementele din multimea sortata cu elementele din multimea nesortata si le inseram la locul potrivit
- pornim de la ``stanga crescator`` (poate varia la test)
- initial multimea sortata va fi goala, deci consideram ca fiind formata doar din primul element
- MN = ``39 11 73 29``; MS = ``39`` (multimea sortata)
	- MN = ``11 39 73 29``; MS = ``11 39`` -- Pas1
	- MN = ``11 39 73 29`` ; MS = ``11 39 73`` (nu este considerat un pas pt ca n a avut loc nicio interschimare)
	- MN = ``11 29 39 73`` -- Pas2

- ``stanga descrescator``
- MN = ``10 40 20 30``; MS = ``10``
- MN = ``40 10 20 30``; MS = ``40 10`` -- Pas1
- MN = ``40 20 10 30``; MS = ``40 20 10`` -- Pas2
- MN = ``40 30 20 10`` -- Pas3 (ne oprim pt ca card MS = card MN)

### Selectsort (selectie)

- ``crescator``
- caut minimul(in dreapta) si fac schimb de pozitii in sir
	- daca nu gasesc minimul, atunci scriu sirul identic si trec la elementul urmator (si acesta este pas)
	
- ``30 17 76 21`` (suntem la 30,  minimul este 17)
	- ``17 30 76 21``  = Pas1 (suntem la 30, minimul este 21)
	- ``17 21 76 39`` = Pas2 (suntem la 76, minimul este 39)
	- ``17 21 39 76`` = Pas3

- ``40 30 90 50`` (suntem la 40, minimul este 30)
	- ``30 40 90 50`` = Pas1 (suntem la 40, minimul este 40)
	- ``30 40 90 50`` = Pas2 (suntem la 90, minimul este 50)
	- ``30 40 50 90`` = Pas3


- ``descrescator``
- caut maximul(in dreapta) si fac schimb de pozitii in sir
- ``23 19 61 29`` (suntem la 23, maximul este 61)
	- ``61 19 23 29`` = Pas1 (suntem la 19, maximul este 29)
	- ``61 29 23 19`` = Pas2 (suntem la 23, maximul este 23)
	- ``61 29 23 19`` = Pas3


# Sortari avansate:
### Heapsort (varianta heapify - miim)

```
- 57 59 53 52 54 56 58 55

Arbore initial:
                    57
		59     53
	52    54 56  58
55
Punem indexii: 57 = Index0, 59 = Index1, 53 = Index2, 52 = Index3, 54 = Index4, 56 = Index5, 58 = Index6, 55 = Index7

Verificam daca copilul este mai mare decat parintele. Parintele o sa faca schimb cu cel mai mic dintre copii. Daca nu face schimb, ne mutam pe indexul urmator.

Aplicam heapify pornind de la ultimul nod parinte (daca sunt mai multi, il luam pe cel cu indexul mai mare). 

-- Pas1 -- 
In caul nostru, ultimul nod parinte este 52 = Index3
(Index3) 55 > 52? (da), deci ne putem muta pe urmatorul index
(Index2) 56 > 53? (da) ; 58 > 53? (da), deci ne mutam pe urmatorul index
(Index1) 52 > 59? (nu) ; 54 > 59? (nu), deci il alegem pe cel mai mic, 52, deci interschimbam 59 cu 52, deci configuratia arborelui se schimba.

                    57
		52     53
	59    54 56  58
55
Punem din nou indexii... (se pun direct pe graf)

(IndexTemporar3 = 55, deoarece Indexul principal nu se schimba ca sa ne putem intoarce dupa la el) 55 > 59? (nu), deci interschimbam, iar arborele devine:
			57
		52     53
	55    54 56  58
59
Ne intoarcem la indexul principal, deoarece 59 nu mai are niciun fiu

(Index0) 52 > 57? (nu) ; 53 > 57? (nu), deci 57 face schimb cu 52
                    52
		57     53
	59    54 56  58
55

(IndexTemporar1 = 57) 55 > 57? (nu); 54 > 57? (nu), deci 57 face schimb cu 54
                    52
		54     53
	59    57 56  58
55
(IndexTemporar4 = 56) nu mai are niciun fiu, deci revenim la Indexul principal
nu mai putem traversa prin ascensiune de la Index0, deci aici se incheia pas1, deci pas1 = ``52, 54, 53, 55, 57, 56, 58, 59``
```

### Shellsort
- o sa avem un indice numit ``H[i]``, ceea ce ne specifica grupele de elemente pentru sir

- Fie ``H[i] = 4``, deci grupam elementele cate ``4``
- ``51 53 59 57 50 52 56 54 58``; sa se scria Pasul 1
	- G1(grupa 1) = ``51 53 59 57`` G2 = ``50 52 56 54`` G3 = ``58``, apoi le punem una sub alta 
	- ``51 53 59 57`` 
	- ``50 52 56 54``
	- ``58``
	- Le luam pe coloane si le sortam, deci devin =>
		- ``50 52 56 54`` 
		- ``51 53 59 57``
		- ``58``
	- Raspunsul final pentru exercitiul asta este: ``50 52 56 54 51 53 59 57 58``

- Nu se cere la test, dar urmatorul pas ar fi sa scadem indicele ``H[i]`` => ``H[i]=3``

### Binsort
- Punem numarul pe pozitia lui, deci ``20`` pe pozitia ``20``. Algoritmul functioneaza doar daca in tablou sunt toate numerele de la 0 la nr de elemente.
```
Ne uitam doar la primul element, si il punem pe pozitia lui, inteschimbandu-l cu cel care e deja pe pozitia lui.
Index = 0 1 2 3 4 5 6
		3 5 1 6 0 4 2
		6 5 1 3 0 4 2
		2 5 1 3 0 4 6
		1 5 2 3 0 4 6
		5 1 2 3 9 4 6
```

### Quicksort (cu pivot median)
- Nu intra la quiz, iar la examen intra doar implementarea lui

```
indexi: 0  1  2 3  4
chei : 77 79 73 72 74

Luam mijlocul -> m = 2 (index pt 73)

Pentru crescator - elementele din stanga mai mici, cele din dreapta mai mari.
Deci modificam in stanga pana nu exista elem mai mari decat mijl, in dreapta pana nu mai exista mai mici

stanga: 77 > 73, 79 > 73
dreapta: 72 < 73, 74 > 73

77 face schimb cu 72 (cel mai mare din st cu cel mai mic din dr)
72 79 73 77 74 (pas 1)

m -> 2 (index pt 73)
stanga: 72 < 73, 79 > 73
dreapta: 77 > 73, 74 > 73 
pt ca in dreapta se respecta regula, il interschimbam pe 79 cu pivotul (mijlocul)

73 face schimb cu 79
72 73 79 77 74 (pas2)

deoarece indexul s a schimbat, tabloul se imparte in 2 in jurul fostului pivot:
Tablou 1: 72
Tablou 2: 79 77 74

Luam tabloul 2:
index: 0 1  2
chei: 79 77 74

m = 1 (index pt 77)
stanga: 79 > 77
dreapta: 74 < 77
=> 74 77 79

=> Pas3 = 72 73 74 77 79 (concatenam sub-tablourile cu fostul pivot 73)

* Daca avem 2 mai mari in stanga si 2 mai mici in dreapta, acestea fac schimb in acelasi pas.

```

### Radix sort prin interschimbare (bitul cel mai semnificativ)

```
5 3 2 6 1

Scriem nr pe biti:
5 = 101
3 = 011
2 = 010
6 = 110
1 = 001

Bitii de 1 coboara, bitii de 0 urca.
Primul bit de 1 intalnit se schimba cu ultimul bit de 0 intalnit.
Daca nu are cu cine sa faca schimb, ramane pe loc si facem o delimitare. Aceasta delimitare mai apare si cand interschimbam 2 numere.

Pasul 1 (pentru 2^2)
Schimbam 5 cu 1
1 = 001
3 = 011
2 = 010
--------- (delimitare)
6 = 110
5 = 101
Deci, pentru 2^2, configuratia obtinuta este 1 3 2 6 5

Pasul 2 (pentru 2^1)
Schimbam 5 cu 6
1 = 001
---------
3 = 011
2 = 010
---------
5 = 101
---------
6 = 110
Deci, pentru 2^1, am obtinut 1 3 2 5 6

Pasul 3 (pentru 2^0)
Schimbam 2 cu 3
1 = 001
---------
2 = 010
---------
3 = 011
---------
5 = 101
---------
6 = 110

```

### Radix sort direct (m = masca)
- Masca se da la fiecare exercitiu

```
Fie m = 2

8 = 1000
9 = 1001
6 = 0110
5 = 0101
4 = 0100
1 = 0001
3 = 0011
7 = 0111
2 = 0010

Avem 2 tabele:
```

- T1 (pornim de la dreapta spre stanga, adica ne uitam la ultimii 2 biti ai numerelo)

| 00       | 01       | 10       | 11       |
| -------- | -------- | -------- | -------- |
| 8 = 1000 | 9 = 1001 | 6 = 0110 | 3 = 0011 |
| 4 = 0100 | 5 = 0101 | 2 = 0010 | 7 = 0111 |
|          | 1 = 0001 |          |          |

- => Primul pas este ``8 4 9 5 1 6 2 3 7`` (luam numerele de pe coloanele tabelului 1)


- T2 (ne uitam in primul tabel; pornim de la stanga la dreapta, deci la primii 2 biti; incepem cu 8, in acceasi ordine in care am scris rezultatul de la primul pas)

| 00       | 01       | 10       | 11  |
| -------- | -------- | -------- | --- |
| 1 = 0001 | 4 = 0100 | 8 = 1000 |     |
| 2 = 0010 | 5 = 0101 | 9 = 1001 |     |
| 3 = 0011 | 6 = 0110 |          |     |
|          | 7 = 0111 |          |     |
- => Al doilea pas este ``1 2 3 4 5 6 7 8 9`` (radix direct este obtine tabloul sortat la al doilea pas)
- Daca masca era 3, mai adugam 2 biti in fata, de obicei se foloseste pt nr mai mari => masca * 2 ne spune ope cati biti scriem numerele 
