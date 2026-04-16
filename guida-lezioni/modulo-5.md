# Modulo 05 · Liste e lettura dei dati

---

## Autovalutazione

- Sai rappresentare dati ordinati con una lista?
- Sai usare le operazioni fondamentali sulle liste?
- Sai trasformare una stringa in lista con `split()`?
- Sai leggere sequenze di dati e accumularle in una lista?
- Sai ragionare sulla differenza tra lista e stringa?

---

## Due problemi che il `while` da solo non riesce a risolvere

### Problema 1: stampa i numeri al contrario

Scrivi un programma che legge numeri interi uno alla volta (terminati da `0`) e li stampa in ordine inverso rispetto a quello in cui sono stati inseriti.

Esempio:

```
Input:  3  7  2  5  0
Output: 5  2  7  3
```

Prova a risolverlo usando solo le variabili che conosci. Cosa manca?

Il problema è che quando arriva lo `0`, i numeri precedenti non esistono più: ogni nuova lettura sovrascrive la variabile. Per stampare al contrario bisogna prima raccogliere tutti i valori, poi scorrere la raccolta in senso inverso.

Con le sole variabili del modulo 4:

```python
numero = int(input())
while numero != 0:
    # qui vorremmo "ricordare" numero, ma dove?
    numero = int(input())
# a questo punto non sappiamo più cosa è stato inserito
```

Il `while` sa iterare, ma non sa ricordare una sequenza di valori.

---

### Problema 2: chi è sopra la media?

Scrivi un programma che legge numeri interi uno alla volta (terminati da `0`) e stampa quelli che superano la media di tutti i numeri inseriti.

Esempio:

```
Input:  4  8  2  6  0
Media:  5.0
Output: 8  6
```

Anche volendo, questo problema è impossibile da risolvere con una sola passata: per sapere se `4` è sopra la media, devi già conoscere anche `8`, `2` e `6`. La media si può calcolare solo dopo aver letto l'ultimo numero.

Servono due passate sugli stessi dati:

1. leggi tutti i numeri, calcola la media;
2. scorri di nuovo gli stessi numeri e stampa quelli sopra la media.

Per fare la seconda passata i numeri devono essere ancora disponibili — e con variabili singole non lo sono.

---

Entrambi i problemi hanno la stessa radice: il programma ha bisogno di **ricordare una sequenza di valori** per poterla usare dopo. Questa è esattamente la funzione di una lista.

<a id="mod5-liste"></a>
## Liste: creare e popolare

Una lista è una sequenza ordinata di valori tenuti insieme sotto un unico nome.

### Creare una lista

Lista con elementi già noti:

```python
voti = [28, 30, 24, 27]
nomi = ["Alice", "Bruno", "Carla"]
```

Lista vuota, da riempire dopo:

```python
numeri = []
```

La lista vuota è il punto di partenza quando non si conosce in anticipo quanti elementi ci saranno — esattamente la situazione dei problemi di apertura.

### Aggiungere elementi: `append`

```python
numeri = []
numeri.append(4)
numeri.append(8)
numeri.append(2)
print(numeri)   # [4, 8, 2]
```

Ogni chiamata ad `append` aggiunge un elemento **in coda**. L'ordine di inserimento viene conservato.

### Leggere la lunghezza: `len`

```python
voti = [28, 30, 24, 27]
print(len(voti))   # 4
```

### Accedere a un elemento: `lista[i]`

Gli indici partono da `0`.

```python
voti = [28, 30, 24, 27]
#        0   1   2   3

print(voti[0])   # 28  (primo)
print(voti[3])   # 27  (quarto)
print(voti[-1])  # 27  (ultimo, contando da destra)
```

```
indice:   0    1    2    3
        +----+----+----+----+
voti:   | 28 | 30 | 24 | 27 |
        +----+----+----+----+
```

### Modificare un elemento

```python
voti[0] = 29
print(voti)   # [29, 30, 24, 27]
```

### Concatenare due liste

```python
a = [1, 2, 3]
b = [4, 5, 6]
print(a + b)   # [1, 2, 3, 4, 5, 6]
```

`+` non modifica `a` né `b`: produce una nuova lista.

### Riepilogo operazioni

| Operazione          | Sintassi         | Nota                          |
| ------------------- | ---------------- | ----------------------------- |
| Lista vuota         | `L = []`         |                               |
| Aggiunta in coda    | `L.append(x)`    | modifica `L` sul posto        |
| Lunghezza           | `len(L)`         |                               |
| Accesso per indice  | `L[i]`           | da `0` a `len(L)-1`           |
| Ultimo elemento     | `L[-1]`          |                               |
| Modifica elemento   | `L[i] = x`       | modifica `L` sul posto        |
| Concatenazione      | `L1 + L2`        | produce una nuova lista       |
| Conteggio occorr.   | `L.count(x)`     |                               |

> Python permette liste con elementi di tipo diverso, ma nella pratica conviene costruire liste omogenee (tutti interi, tutte stringhe, …): è più semplice applicare le stesse operazioni a tutti gli elementi.

### Tornare al Problema 1: numeri al contrario

Con `append` possiamo raccogliere i numeri mentre li leggiamo, e usarli dopo:

```python
numeri = []
numero = int(input())
while numero != 0:
    numeri.append(numero)
    numero = int(input())

# ora numeri contiene tutta la sequenza
i = len(numeri) - 1
while i >= 0:
    print(numeri[i])
    i = i - 1
```

Il `while` di lettura accumula; il secondo `while` scorre la lista al contrario.

## Esercizi: while e liste

### Costruire una lista

1. Crea una lista con i numeri da 1 a 5 usando `append` in un ciclo `while`. Stampa la lista.

2. Leggi numeri interi dall'input fino a `0` e salvali in una lista. Stampa la lista alla fine.

3. Leggi parole dall'input fino a `fine` e salvale in una lista. Stampa quante parole sono state inserite.

4. Leggi numeri fino a `0`. Costruisci due liste separate: una con i numeri pari e una con i numeri dispari. Stampa entrambe.

### Accedere agli elementi

5. Data la lista `voti = [24, 28, 30, 18, 27]`, stampa il primo e l'ultimo voto.

6. Data la lista `nomi = ["Alice", "Bruno", "Carla", "Dario"]`, stampa il secondo e il penultimo nome.

7. Data la lista `prezzi = [3.5, 1.2, 7.8, 4.0]`, stampa il prezzo più alto (senza usare `max()`): scorri la lista con un `while` e tieni traccia del massimo.

### Scorrere una lista con `while`

8. Data una lista di numeri, stampa solo quelli maggiori di 10.

9. Data una lista di parole, stampa solo quelle che iniziano per vocale.

10. Data una lista di numeri, calcola e stampa la somma di tutti gli elementi (senza usare `sum()`).

11. Leggi numeri fino a `0`, salvali in una lista, poi stampa la lista al contrario (come nel Problema 1).

### Collegamento al Problema 2

12. Leggi numeri fino a `0`, salvali in una lista, calcola la media e stampa quelli che superano la media.

---

## Esercizi: paradigmi di soluzione

### Paradigma 1 — verifica di proprietà sulla sequenza

Questi esercizi richiedono di raccogliere tutta la sequenza e poi rispondere a una domanda su di essa.

13. Scrivi un programma che chiede parole fino a `fine`. Alla fine stampa `Sequenza corretta` se la parola `lingua` è comparsa almeno una volta, `Sequenza errata` altrimenti.

    Esempi:
    - `ciao lingua quaderno fine` → `Sequenza corretta`
    - `ciao penna quaderno fine` → `Sequenza errata`

14. Scrivi un programma che legge 5 parole e le salva in una lista. Stampa `uguale` se la prima e l'ultima parola sono identiche, `diversa` altrimenti.

15. Scrivi un programma che legge una stringa e controlla se è palindroma (ignora spazi e maiuscole/minuscole). Esempi di stringhe palindrome: `anna`, `i topi non avevano nipoti`.

16. Scrivi un programma che chiede numeri interi fino a `0`. Controlla se ogni `1` nella sequenza è immediatamente seguito da un `2`. Stampa `Sequenza corretta` o `Sequenza errata`.

    Esempi:
    - `9 1 2 6 1 2 0` → corretta
    - `9 1 6 1 2 0` → errata (il primo `1` non è seguito da `2`)
    - `9 1 2 6 2 0` → corretta (il `2` extra non viola la regola)

### Paradigma 2 — serie multiple

Questi esercizi richiedono di ripetere lo stesso schema di lettura più volte, trattando ogni serie come un'unità.

17. Scrivi un programma che legge tre serie di numeri, ognuna terminata da `0`. Per ogni serie, stampa i numeri letti al contrario.

    Input:
    ```
    4
    12
    0
    9
    7
    6
    0
    4
    1
    -3
    8
    0
    ```

    Output:
    ```
    [12, 4]
    [6, 7, 9]
    [8, -3, 1, 4]
    ```

18. Scrivi un programma che legge una serie di numeri terminata da `0`. Per ogni numero `n` della serie stampa tutti i numeri pari compresi tra `0` (incluso) e `n` (escluso).

    Input: `6 10 0`
    Output: `0 2 4` poi `0 2 4 6 8`

### Paradigma 3 — conteggio e classificazione

Questi esercizi richiedono di leggere una sequenza e tenere traccia di conteggi per categoria.

19. Scrivi un programma che legge parole fino a `fine` e conta quante iniziano per ciascuna vocale (`a`, `e`, `i`, `o`, `u`). Stampa il conteggio per ogni vocale.

20. Scrivi un programma che legge 5 lettere, poi legge parole fino a `fine`. Per ogni lettera letta all'inizio, stampa quante parole iniziano con quella lettera.

### Paradigma 4 — operazioni su due liste

Questi esercizi lavorano su due liste e richiedono di confrontarle elemento per elemento. Non usare `set` né operatori insiemistici: l'obiettivo è costruire l'algoritmo con `while` e liste.

**Versione semplice: liste senza duplicati**

21. Date due liste di interi, costruisci una lista con gli elementi **in comune** (intersezione).

    ```python
    a = [3, 7, 1, 9, 4]
    b = [7, 2, 9, 5, 1]
    # risultato atteso: [7, 1, 9]  (ordine di apparizione in a)
    ```

22. Date due liste, costruisci una lista con tutti gli elementi che compaiono in almeno una delle due, **senza duplicati** (unione).

    ```python
    a = [3, 7, 1]
    b = [7, 2, 9]
    # risultato atteso: [3, 7, 1, 2, 9]
    ```

23. Date due liste `a` e `b`, costruisci una lista con gli elementi di `a` che **non** compaiono in `b` (differenza `a - b`).

    ```python
    a = [3, 7, 1, 9, 4]
    b = [7, 2, 9, 5]
    # risultato atteso: [3, 1, 4]
    ```

24. Date due liste, controlla se sono **disgiunte** (nessun elemento in comune). Stampa `True` o `False`.

**Versione con duplicati**

25. Stessi esercizi 21–23, ma le liste possono contenere duplicati. Decidi come gestirli: un elemento che compare due volte in `a` e una volta in `b` quante volte deve comparire nel risultato?

    ```python
    a = [1, 2, 2, 3]
    b = [2, 2, 4]
    # intersezione "con molteplicità": [2, 2]
    # differenza a - b: [1, 3]
    ```

**Versione con liste ordinate**

26. Date due liste **già ordinate in modo crescente**, costruisci la lista unione ordinata **senza usare `sort()`**: scorri entrambe in parallelo con due indici e aggiungi l'elemento minore alla volta (algoritmo di merge).

    ```python
    a = [1, 3, 5, 7]
    b = [2, 3, 6, 8]
    # risultato atteso: [1, 2, 3, 3, 5, 6, 7, 8]
    ```

27. Come l'esercizio 26, ma costruisci solo l'intersezione ordinata (elementi presenti in entrambe, senza duplicati).

    ```python
    a = [1, 3, 5, 7]
    b = [2, 3, 6, 7]
    # risultato atteso: [3, 7]
    ```

---

## Liste di liste

Una lista può contenere qualsiasi tipo di valore — incluse altre liste. Questo permette di rappresentare strutture a due dimensioni come **matrici**, tabelle e griglie.

```python
matrice = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

`matrice` è una lista di 3 elementi, ognuno dei quali è una lista di 3 interi.

### Accesso agli elementi

Per accedere a un elemento servono due indici: prima la riga, poi la colonna.

```python
matrice[0]      # [1, 2, 3]  — prima riga intera
matrice[0][0]   # 1          — riga 0, colonna 0
matrice[1][2]   # 6          — riga 1, colonna 2
matrice[2][-1]  # 9          — ultima colonna della terza riga
```

```
         col 0  col 1  col 2
        +------+------+------+
riga 0  |  1   |  2   |  3   |
        +------+------+------+
riga 1  |  4   |  5   |  6   |
        +------+------+------+
riga 2  |  7   |  8   |  9   |
        +------+------+------+
```

### Stampare una matrice riga per riga

```python
i = 0
while i < len(matrice):
    print(matrice[i])
    i = i + 1
```

Output:
```
[1, 2, 3]
[4, 5, 6]
[7, 8, 9]
```

Per stampare elemento per elemento con due cicli annidati:

```python
i = 0
while i < len(matrice):
    j = 0
    while j < len(matrice[i]):
        print(matrice[i][j], end=" ")
        j = j + 1
    print()   # a capo alla fine di ogni riga
    i = i + 1
```

Output:
```
1 2 3
4 5 6
7 8 9
```

### Costruire una matrice con input

```python
righe = int(input("Righe: "))
colonne = int(input("Colonne: "))

matrice = []
i = 0
while i < righe:
    riga = []
    j = 0
    while j < colonne:
        val = int(input())
        riga.append(val)
        j = j + 1
    matrice.append(riga)
    i = i + 1
```

### Esercizi: liste di liste

28. Crea a mano (senza input) una matrice 3×3 con i numeri da 1 a 9 e stampala riga per riga nel formato sopra.

29. Data una matrice quadrata `n×n`, stampa solo la diagonale principale (gli elementi dove `riga == colonna`).

    ```python
    matrice = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    # output: 1  5  9
    ```

30. Data una matrice, calcola la somma di tutti gli elementi.

31. Data una matrice, costruisci la sua **trasposta**: una nuova matrice dove righe e colonne sono scambiate.

    ```python
    originale = [[1, 2, 3], [4, 5, 6]]
    # trasposta: [[1, 4], [2, 5], [3, 6]]
    ```

32. Leggi dall'input una matrice `n×m` (prima `n`, poi `m`, poi i valori riga per riga). Stampa per ogni riga la somma degli elementi di quella riga.

---

## `split()` e prime trasformazioni

Una nuova operazione importante sulle stringhe e' questa:

```python
incipit = "Era una notte incantevole, una di quelle notti..."
parole = incipit.split()
print(parole)
```

`split()` prende una stringa e restituisce una lista di sottostringhe.

Questo passaggio e' fondamentale per molti problemi:

- tokenizzare testo;
- leggere parole una per volta;
- passare da un dato "compatto" a una struttura manipolabile.

Questo passaggio e' cosi' importante per chi lavora su testi perche':

- un file o una stringa ci arrivano inizialmente come sequenza di caratteri;
- ma per molte analisi linguistiche vogliamo lavorare parola per parola;
- quindi abbiamo bisogno di una struttura in cui `era`, `una`, `notte` siano elementi distinti.

Per questo `split()` e' uno dei primi ponti concreti tra:

- testo grezzo;
- lista di token;
- analisi successiva con cicli e conteggi.

### Esempio

```python
frase = "uno due tre quattro"
pezzi = frase.split()
print(pezzi)
```

Risultato:

```python
['uno', 'due', 'tre', 'quattro']
```

### Attenzione: `split()` taglia dove gli diciamo di tagliare

Un punto molto importante e' questo: l'unita' che otteniamo dipende dalla regola di segmentazione che stiamo usando.

Con `split()` senza argomenti:

- il taglio avviene sugli spazi;
- quindi `"La Spezia"` diventa due elementi se c'e' uno spazio in mezzo;
- mentre `"andata,"` resta un unico elemento, perche' la virgola non viene separata automaticamente.

Questo e' utile da capire subito perche':

- `split()` e' semplice e spesso basta per iniziare;
- ma non coincide ancora con una tokenizzazione linguistica raffinata.

---

<a id="mod5-input-lista"></a>
## Leggere dati e accumularli in lista

Una volta che sappiamo costruire liste, possiamo usarle per raccogliere dati in ingresso.

Schema tipico:

```python
numeri = []

for token in ["3", "5", "8"]:
    numeri.append(int(token))
```

Più avanti questo schema si combinera' con:

- lettura da standard input;
- lettura da file;
- cicli `while` con sentinella.

Per ora il punto chiave e' questo:

> una lista e' il contenitore naturale quando non sappiamo in anticipo quanti dati dovremo raccogliere.

---

## Esercizi

1. Crea una lista di 5 parole e stampa il primo e l'ultimo elemento.
2. Data una lista di numeri, stampa la sua lunghezza.
3. Aggiungi un elemento in coda con `append`.
4. Data una frase, usa `split()` per ottenere la lista delle parole.
5. Scrivi un programma che costruisce una lista di numeri e ne stampa gli elementi in ordine inverso usando gli indici.
6. Leggi una sequenza di numeri da standard input o da file e salvala in una lista fino alla sentinella.
7. Leggi tre serie di numeri separate da `0` e stampa ogni serie al contrario.
8. Chiedi all'utente di inserire una stringa e calcola quante vocali ci sono nella stringa.
9. Leggi una parola dall'input e stampa solo le lettere in posizione pari (0, 2, 4, …).
10. Data una stringa letta dall'input (es. `adoro programmare in Python!`), scrivi un programma che stampa la frequenza di ogni lettera all'interno della stringa.
11. Scrivi un programma che fa giocare l'utente al gioco dell'impiccato.
    - Nel gioco, un giocatore (A) pensa a una parola segreta. L'altro giocatore (B) propone una lettera alla volta. Se la lettera è presente, tutte le sue posizioni vengono svelate.
    - Nella cartella `impiccato/` trovi i file `parola_segreta.py` e `impiccato.py` con la struttura di partenza. Salva entrambi nella stessa cartella.
    - `parola_segreta.py` contiene la variabile `PAROLA_SEGRETA` che puoi modificare. `impiccato.py` contiene la funzione `update(guess, parola, lettera)` che aggiorna la stringa di underscore:
      ```python
      update("____", "casa", "a")  # → "_a_a"
      update("_a_a", "casa", "c")  # → "ca_a"
      ```
12. Estendi l'impiccato aggiungendo un numero massimo di tentativi (6 nella versione classica, oppure dipendente dalla lunghezza della parola), e la possibilità di indovinare l'intera parola in un turno.

---

## Riepilogo

Questo modulo raccoglie il nucleo sulle liste:

- definizione di lista come collezione ordinata;
- operazioni elementari;
- relazione tra stringhe e liste tramite `split()`;
- accumulo di dati in una struttura ordinata.
