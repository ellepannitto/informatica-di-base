# Modulo 04 · Iterazione con sentinelle, convalida dell'input e liste

## A fine lezione

- Sai usare `while` quando non conosci in anticipo il numero di iterazioni?
- Sai progettare cicli con sentinelle e input ripetuto?
- Sai riconoscere errori tipici come loop infinito e stato non aggiornato?
- Sai applicare `while` a conteggi, validazione e piccoli automi?
- Sai rappresentare dati ordinati con una lista?
- Sai usare le operazioni fondamentali sulle liste?
- Sai trasformare una stringa in lista con `split()`?
- Sai leggere sequenze di dati e accumularle in una lista?
- Sai ragionare sulla differenza tra lista e stringa?

## Quando l'utente decide quando fermarsi

In alcuni esercizi il numero di iterazioni dipende da un valore noto in anticipo (es. `pagine = 120`).
Ma a volte il programma non sa quante volte dovrà ripetere: dipende dall'apparire di un valore in modo non determinabile a priori.

Esempio: sommare numeri finché l'utente non inserisce `-1`.

<details>

```python
numero = int(input("Numero (-1 per terminare): "))
somma = 0

while numero != -1:
    somma = somma + numero
    numero = int(input("Numero (-1 per terminare): "))
```

</details>

Lo schema è lo stesso dei due esempi visti prima:

- si legge il primo valore **prima** del ciclo (inizializzazione dello stato);
- la guardia controlla se continuare;
- nel corpo si fa il lavoro utile e si **rilegge** il valore (aggiornamento dello stato).

La differenza rispetto al contatore è che qui lo stato non cambia in modo prevedibile: cambia perché l'utente inserisce un valore diverso. Il programma si ferma quando quel valore soddisfa una condizione speciale concordata (`-1`, `"fine"`, ecc.).

## Esercizi

1. Scrivi un programma che chiede all'utente di inserire un numero. Il programma si ferma quando l'utente inserisce `0` e conta quanti numeri interi sono stati inseriti.
2. Scrivi un programma che chiede all'utente di inserire un numero. Il programma si ferma quando l'utente inserisce `0` e, per ogni numero inserito, se il numero è pari stampa `Hai inserito un numero pari!` altrimenti stampa `Hai inserito un numero dispari!`.
3. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce la parola `fine`. Per ogni parola inserita, se la parola è più lunga di 5 caratteri stampa `parola lunga` altrimenti stampa `parola breve`.
4. Scrivi un programma che legge un numero compreso tra 1 e 10 (controlla che il numero inserito sia lecito, altrimenti stampa un messaggio di errore) e stampa la tabellina di quel numero. Ad esempio, se viene inserito `3`:
    ```
    3 x 0 = 0
    3 x 1 = 3
    3 x 2 = 6
    ...
    3 x 10 = 30
    ```
5. Chiedi all'utente di inserire una stringa e calcola quante vocali contiene.
6. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Per ogni parola inserita calcola quante vocali contiene. Alla fine, stampa il numero totale di vocali incontrate.
7. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Alla fine, stampa quante delle parole inserite finiscono per vocale.
8. Scrivi un programma che legge parole dall'input finché l'utente non scrive `fine`. Conta quante parole iniziano con una lettera maiuscola.
9. Scrivi un programma che legge parole dall'input e si ferma alla prima parola più lunga di 6 caratteri, stampandola. Se non compare nessuna parola così lunga prima di `fine`, stampa `nessuna`.
10. Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`, e al termine stampa il massimo tra quelli inseriti. (Se non viene inserito nessun numero prima dello zero, stampa un messaggio apposito.)
11. Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`. Al termine stampa quanti erano pari e quanti dispari, e quale delle due categorie era più numerosa.
12. Scrivi un programma che legge numeri interi finché l'utente non inserisce `0` e calcola la media dei valori inseriti. Se non viene inserito nessun valore prima dello zero, stampa `nessun dato`.
13. Scrivi un programma che legge una sequenza di numeri positivi terminata da `-1` e stampa ogni numero insieme al suo scarto rispetto al numero precedente. Per il primo numero lo scarto non esiste; per gli altri stampa `differenza: +3` o `differenza: -5` ecc.
14. Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`. Stampa `sì` se la sequenza è non-decrescente (ogni numero è ≥ al precedente), `no` altrimenti.
15. Scrivi un programma che chiede all'utente di inserire dei numeri interi e si ferma quando scrive `0`. Controlla se ogni `1` è seguito da un `2`. Esempi:
    - `9, 1, 2, 6, 1, 2, 0` → `Sequenza corretta`
    - `9, 1, 6, 1, 2, 0` → `Sequenza errata`
16. Scrivi un programma che chiede all'utente di inserire una parola e continua finché non scrive `fine`. Controlla se tra le parole inserite compare la parola `lingua`. Stampa `sì` o `no`.

## Esercizi

Gli esercizi con pattern di stampa costringono a distinguere il ciclo esterno (righe) dal ciclo interno (simboli per riga), e mostrano subito gli errori di guardia, inizializzazione e incremento.

1. Dati due numeri (es. `pagine = 3` e `righe = 5`), stampa tutte le combinazioni di pagine e righe come nell'esempio sopra.
2. Stampa la tavola pitagorica da 1 a 10:
    ```
    1 x 1 = 1
    1 x 2 = 2
    ...
    10 x 10 = 100
    ```
3. Chiedi all'utente `n` dall'input. Stampa un quadrato di asterischi `n x n`:
    ```
    ***
    ***
    ***
    ```
4. Scrivi un programma che legge un intero positivo `n` e stampa tutte le sue cifre, una per riga, partendo da quella meno significativa. (Es.: `n = 374` → `4`, `7`, `3`.) Non usare stringhe: estrai le cifre con divisione e modulo.
5. Scrivi un programma che legge un intero positivo `n` e stabilisce se è primo. Un numero è primo se è divisibile solo per 1 e per se stesso.
6. Scrivi un programma che legge un intero positivo `n` e stampa la sequenza di Collatz: se `n` è pari calcola `n // 2`, se è dispari calcola `3 * n + 1`; ripeti finché `n` non diventa `1`. Stampa ogni valore e, alla fine, quanti passi sono stati necessari.
7. Scrivi un programma che simula un gioco: il computer sceglie un numero tra 1 e 100 (es. `segreto = 42`), l'utente prova a indovinarlo inserendo tentativi. Dopo ogni tentativo il programma dice `troppo basso`, `troppo alto` oppure `esatto!`. Conta i tentativi.
8. Scrivi un programma che legge un intero positivo `n` e stampa il suo fattoriale (`n! = 1 × 2 × … × n`).
9. Scrivi un programma che verifica se una stringa letta dall'input è un palindromo usando un ciclo `while` e confrontando caratteri dalla testa e dalla coda, senza usare lo slicing `[::-1]`.
10. Scrivi un programma che legge parole finché l'utente non scrive `fine` e le stampa in ordine inverso rispetto all'ordine di inserimento. (Usa una lista per memorizzarle, poi scorri al contrario.)
11. Scrivi un programma che legge un intero positivo `n` e stampa i primi `n` numeri della sequenza di Fibonacci: `0, 1, 1, 2, 3, 5, 8, …`

## Automi a stati finiti e il `while`

In modulo 3 abbiamo usato gli automi per descrivere come un `if/elif/else` **partiziona** gli input:
dato un input, l'automa sceglie un ramo e raggiunge uno stato finale e si ferma lì.

Con il `while` cambia la natura dell'input: non un singolo valore o una sequenza determinata, ma una **sequenza** di cui non conosciamo necessariamente la lunghezza in anticipo. Il ciclo legge un elemento alla volta e aggiorna lo stato; si ferma quando la sequenza è esaurita o quando una condizione segnala la fine.

### Esempio: valore speciale di stop

```python
numero = int(input("Numero (-1 per terminare): "))
somma = 0
while numero != -1:
    somma = somma + numero
    numero = int(input("Numero (-1 per terminare): "))
```

La struttura dell'automa è identica: uno stato `resta` con un cappio su sé stesso finché la guardia è vera, e una transizione verso `fine` quando arriva il valore speciale.

```
         ┌───────────────────┐
         │   numero ≠ -1,    │
         ▼                   │
──►  ┌──────────────┐        │
     │    resta     │────────┘
     └──────────────┘
           │  numero = -1
           ▼
        ╔══════╗
        ║ fine ║
        ╚══════╝
```

> La domanda da farsi sempre è: **quale valore dello stato porta la guardia a diventare falsa?**
> Se non esiste, il ciclo non termina mai.

## Esercizi: riconoscimento di stringhe

Un automa a stati finiti legge una sequenza **una lettera alla volta**.
A ogni passo:

1. guarda il carattere corrente;
2. segue la transizione corrispondente allo stato in cui si trova;
3. aggiorna lo stato.

Quando la sequenza è finita:
- se ci si trova in uno **stato finale** (╔══╗), la sequenza è accettata;
- se lo stato non è finale, la sequenza non è accettata.

### Come seguire un automa su una stringa concreta

Esempio: costruiamo un automa che controlla se nella sequenza è stata inserita almeno una vocale.

Due stati: `non_trovata` (nessuna vocale vista finora) e `trovata` (almeno una vocale letta — stato finale).

```
         ┌──── non_vocale ──────────────────┐
         ▼                                  │
     ┌──────────────────┐                   │
──►  │   non_trovata    │───────────────────┘
     └──────────────────┘
          │
          │ vocale
          ▼
        ╔══════════╗
        ║  trovata ║◄─── qualsiasi ───┐
        ╚══════════╝──────────────────┘
```

Se la sequenza finisce in `trovata` (╔══╗): accettata.
Se finisce in `non_trovata`: non accettata.

Tracciamento su `"bac"`:

| Passo | Carattere | Stato corrente | Transizione         | Stato successivo |
| ----- | --------- | -------------- | ------------------- | ---------------- |
| 1     | `b`       | `non_trovata`  | b non è vocale      | `non_trovata`    |
| 2     | `a`       | `non_trovata`  | a è vocale          | `trovata`        |
| 3     | `c`       | `trovata`      | già in stato finale | `trovata`        |
| fine  |           | `trovata` → ╔══╗ |                   | **sì**           |

Stessa stringa, risultato opposto: `"bcd"`.

| Passo | Carattere    | Stato corrente | Transizione    | Stato successivo        |
| ----- | ------------ | -------------- | -------------- | ----------------------- |
| 1     | `b`          | `non_trovata`  | b non è vocale | `non_trovata`           |
| 2     | `c`          | `non_trovata`  | c non è vocale | `non_trovata`           |
| 3     | `d`          | `non_trovata`  | d non è vocale | `non_trovata`           |
| fine  | fine stringa | `non_trovata`  | fine stringa   | `fine stringa` → **no** |

La regola è sempre la stessa: **l'accettazione dipende da dove porta la transizione fine stringa**,
non da cosa è successo durante il percorso.

Per ogni esercizio:

1. identifica gli **stati** necessari (cosa devo ricordare mentre scorro la stringa?);
2. disegna l'automa con stati, transizioni e **stati finali** (doppio bordo);
3. scrivi il programma con un `while`.


**Problema:** data una stringa, stampare `sì` se contiene almeno una vocale, `no` altrimenti.

**Stati:** due
— `non_trovata` (nessuna vocale vista finora) e
- `trovata` (stato finale ╔══╗).

**Programma:**

```python
stringa = input("Stringa: ")
stato = "non_trovata"
i = 0
while i < len(stringa) and stato == "non_trovata":
    if stringa[i] in "aeiouAEIOU":
        stato = "trovata"
    i = i + 1

if stato == "trovata":
    print("sì")
else:
    print("no")
```

La guardia del `while` ha due condizioni: non aver finito la stringa **e** non aver già trovato la vocale. Appena una vocale viene trovata, il ciclo si interrompe senza leggere il resto.

</details>

### Esempio svolto: ogni `a` seguita da `b`

**Problema:** data una stringa, stampare `sì` se ogni `a` è immediatamente seguita da `b`, `no` altrimenti

**Cosa mi aspetto:**

- `"abxab"` → sì
- `"axb"` → no
- `"a"` → no
- `""` → sì

**Stati:** tre
— `ok` (finora tutto corretto),
- `dopo_a` (l'ultimo carattere letto era `a`, aspettiamo `b`),
- `errore` (trovata una `a` non seguita da `b`). Da `errore` non si esce.

```
     ┌ ≠ a ─┐                               ┌───── 'a' ──┐
     ▼      |                               ▼            │
──►  ╔═══════╗              'a'        ┌──────────┐      │
     ║  ok   ║ ──────────────────────► │  dopo_a  │──────┘
     ╚═══════╝                         └──────────┘
       ▲                                  │ |
       └──────────── b ───────────────────┘ |
                                            │ ≠ a, b
                                            ▼
                                       ┌─────────┐◄── qualsiasi ──┐
                                       │ errore  │                |
                                       └─────────┘────────────────┘
```

Il diagramma diventa denso: è normale per automi con tre stati e transizioni incrociate.
Guardiamo la tabella delle transizioni:

| Stato corrente | Carattere letto        | Stato successivo |
| -------------- | ---------------------- | ---------------- |
| `ok`           | `a`                    | `dopo_a`         |
| `ok`           | tutto tranne `a`       | `ok`             |
| `dopo_a`       | `b`                    | `ok`             |
| `dopo_a`       | `a`                    | `dopo_a`         |
| `dopo_a`       | tutto tranne `a` e `b` | `errore`         |
| `errore`       | qualsiasi carattere    | `errore`         |

**Traccia su `"abxab"`:**

| Passo | Carattere | Stato corrente | Stato successivo |
| ----- | --------- | -------------- | ---------------- |
| 1     | `a`       | `ok`           | `dopo_a`         |
| 2     | `b`       | `dopo_a`       | `ok`             |
| 3     | `x`       | `ok`           | `ok`             |
| 4     | `a`       | `ok`           | `dopo_a`         |
| 5     | `b`       | `dopo_a`       | `ok`             |
| fine  |           | `ok` → ╔══╗    |                  |

**Traccia su `"axb"`:**

| Passo | Carattere | Stato corrente        | Stato successivo |
| ----- | --------- | --------------------- | ---------------- |
| 1     | `a`       | `ok`                  | `dopo_a`         |
| 2     | `x`       | `dopo_a`              | `errore`         |
| 3     | `b`       | `errore`              | `errore`         |
| fine  |           | `errore` → non finale |                  |

**Programma:**

```python
stringa = input("Stringa: ")
stato = "ok"
i = 0
while i < len(stringa) and stato != "errore":
    c = stringa[i]
    if stato == "ok":
        if c == "a":
            stato = "dopo_a"
    elif stato == "dopo_a":
        if c == "b":
            stato = "ok"
        else:
            stato = "errore"
    i = i + 1

# attenzione: se la stringa finisce con 'a' siamo ancora in dopo_a → errore
if stato == "dopo_a":
    stato = "errore"

if stato == "ok":
    print("sì")
else:
    print("no")
```

## Esercizi

Per ciascun esercizio:

1. Definisci gli stati dell'automa e indica quale è quello iniziale e quali sono quelli finali (accettanti).
2. Elenca le transizioni: per ogni stato, cosa succede leggendo ciascun tipo di carattere.
3. Scegli due stringhe di test — una che produce `sì` e una che produce `no` — e mostra il percorso di riconoscimento in una tabella (come nelle tracce viste sopra).

1. **Almeno una vocale.** Data una stringa, stampa `sì` se contiene almeno una vocale (`a`, `e`, `i`, `o`, `u`), `no` altrimenti.
2. **Tutte maiuscole.** Data una stringa, stampa `sì` se tutti i caratteri sono lettere maiuscole, `no` altrimenti.
3. **Termina con vocale.** Data una stringa, stampa `sì` se l'ultimo carattere è una vocale, `no` altrimenti. (Lo stato finale dell'automa, non il primo carattere trovato, determina il risultato.)
4. **Numero pari di vocali.** Data una stringa, stampa `sì` se il numero totale di vocali è pari (zero è pari), `no` altrimenti.
5. **Nessuno spazio doppio.** Data una stringa, stampa `sì` se non contiene due spazi consecutivi, `no` altrimenti.
6. **Due vocali consecutive.** Data una stringa, stampa `sì` se contiene almeno due vocali consecutive (es. `"piaue"` → sì, `"cane"` → no), `no` altrimenti.
7. **Ogni `a` seguita da `b`.**
8. **Il numero di `a` è uguale al numero di `b`.** Data una stringa, stampa `sì` se il numero di occorrenze di `a` è uguale al numero di occorrenze di `b`, `no` altrimenti.
9. **Contiene sia una `a` che una `b`.** Data una stringa, stampa `sì` se contiene almeno una `a` e almeno una `b` (in qualsiasi ordine), `no` altrimenti. (Servono quattro stati: `nessuna`, `solo_a`, `solo_b`, `entrambe`.)
10. **`ab` mai seguita da `c`.** Data una stringa, stampa `sì` se ogni volta che compare la sottostringa `ab`, il carattere immediatamente successivo non è `c` (es. `"xabx"` → sì, `"abc"` → no).
11. **Alternanza obbligata.** Data una stringa composta solo da lettere, stampa `sì` se vocali e consonanti si alternano rigorosamente (es. `"banana"` → sì, `"cane"` → no, `"aei"` → no).
12. **Numero intero ben formato.** Data una stringa, stampa `sì` se rappresenta un intero valido: un segno opzionale (`+` o `-`) seguito da almeno una cifra (es. `"-42"` → sì, `"3"` → sì, `"+"` → no, `"1a2"` → no).

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


Entrambi i problemi hanno la stessa radice: il programma ha bisogno di **ricordare una sequenza di valori** per poterla usare dopo.
Questa è esattamente la funzione di una lista.

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

La lista vuota è il punto di partenza quando non si conosce in anticipo quanti elementi ci saranno, la situazione dei problemi di apertura.

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

<details>
Questa è una differenza rispetto alle stringhe!
</details>

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

## Esercizi base

1. Crea una lista con i numeri da 1 a 5 usando `append` in un ciclo `while`. Poi stampa la lista.
2. Data la lista `voti = [24, 28, 30, 18, 27]`, stampa il primo e l'ultimo voto.
3. Data la lista `nomi = ["Alice", "Bruno", "Carla", "Dario"]`, stampa il secondo e il penultimo nome.
4. Leggi numeri interi dall'input fino a `0` e salvali in una lista. Stampa la lista alla fine.
5. Leggi parole dall'input fino a `fine` e salvale in una lista. Stampa quante parole sono state inserite.
6. Data una lista di numeri, calcola e stampa la somma di tutti gli elementi senza usare `sum()`.
7. Data una lista di numeri, stampa solo quelli maggiori di 10.
8. Data una lista di parole, stampa solo quelle che iniziano per vocale.
9. Data la lista `prezzi = [3.5, 1.2, 7.8, 4.0]`, stampa il prezzo più alto senza usare `max()`: scorri la lista con un `while` e tieni traccia del massimo.
10. Leggi numeri fino a `0`, salvali in una lista, poi stampa la lista al contrario (come nel Problema 1).
11. Data una frase letta dall'input, usa `split()` per ottenere la lista delle parole e stampane la lunghezza.

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

## `split()` e prime trasformazioni

Una nuova operazione importante sulle stringhe e' questa:

```python
incipit = "Era una notte incantevole, una di quelle notti..."
parole = incipit.split()
print(parole)
```

`split()` prende una stringa e restituisce una **lista** di sottostringhe.


### Attenzione: `split()` taglia dove gli diciamo di tagliare

Con `split()` senza argomenti:

- il taglio avviene sugli spazi;
- quindi `"La Spezia"` diventa due elementi se c'è uno spazio in mezzo;
- mentre `"andata,"` resta un unico elemento, perché la virgola non viene separata automaticamente.

## Esercizi avanzati

### Sequenze e proprietà

1. Leggi numeri fino a `0`. Costruisci due liste separate: una con i numeri pari e una con i dispari. Stampa entrambe.
2. Leggi numeri fino a `0`, salvali in una lista, calcola la media e stampa quelli che superano la media (come nel Problema 2).
3. Scrivi un programma che legge 5 parole e le salva in una lista. Stampa `uguale` se la prima e l'ultima parola sono identiche, `diversa` altrimenti.
4. Scrivi un programma che legge una stringa e controlla se è palindroma (ignora spazi e maiuscole/minuscole). Esempi: `anna`, `i topi non avevano nipoti`.
5. Scrivi un programma che chiede numeri interi fino a `0`. Controlla se ogni `1` nella sequenza è immediatamente seguito da un `2`. Stampa `Sequenza corretta` o `Sequenza errata`.
    - `9 1 2 6 1 2 0` → corretta
    - `9 1 6 1 2 0` → errata
6. Data una stringa letta dall'input, stampa la frequenza di ogni lettera che compare almeno una volta.

### Serie multiple e conteggio per categoria

7. Scrivi un programma che legge parole fino a `fine` e conta quante iniziano per ciascuna vocale (`a`, `e`, `i`, `o`, `u`). Stampa il conteggio per ogni vocale.
8. Scrivi un programma che legge 5 lettere, poi legge parole fino a `fine`. Per ogni lettera letta all'inizio, stampa quante parole iniziano con quella lettera.
9. Scrivi un programma che legge tre serie di numeri, ognuna terminata da `0`. Per ogni serie, stampa i numeri al contrario.
    ```
    Input:  4 12 0 / 9 7 6 0 / 4 1 -3 8 0
    Output: [12, 4] / [6, 7, 9] / [8, -3, 1, 4]
    ```
10. Scrivi un programma che legge una serie di numeri terminata da `0`. Per ogni numero `n`, stampa tutti i numeri pari compresi tra `0` (incluso) e `n` (escluso).
    ```
    Input: 6 10 0   Output: 0 2 4  /  0 2 4 6 8
    ```

### Due liste

11. Date due liste di interi, costruisci una lista con gli elementi **in comune** (intersezione, in ordine di apparizione in `a`).
    ```python
    a = [3, 7, 1, 9, 4]; b = [7, 2, 9, 5, 1]  # → [7, 1, 9]
    ```
12. Date due liste, costruisci una lista con tutti gli elementi che compaiono in almeno una delle due, **senza duplicati** (unione).
    ```python
    a = [3, 7, 1]; b = [7, 2, 9]  # → [3, 7, 1, 2, 9]
    ```
13. Date due liste `a` e `b`, costruisci una lista con gli elementi di `a` che **non** compaiono in `b` (differenza `a − b`).
    ```python
    a = [3, 7, 1, 9, 4]; b = [7, 2, 9, 5]  # → [3, 1, 4]
    ```
14. Date due liste, controlla se sono **disgiunte** (nessun elemento in comune). Stampa `sì` o `no`.
15. Stessi esercizi 11–13, ma le liste possono contenere duplicati. Decidi come gestirli.
    ```python
    a = [1, 2, 2, 3]; b = [2, 2, 4]
    # intersezione con molteplicità: [2, 2]; differenza a − b: [1, 3]
    ```
16. Date due liste **già ordinate in modo crescente**, costruisci la lista unione ordinata **senza usare `sort()`** (algoritmo di merge).
    ```python
    a = [1, 3, 5, 7]; b = [2, 3, 6, 8]  # → [1, 2, 3, 3, 5, 6, 7, 8]
    ```
17. Come l'esercizio 16, ma costruisci solo l'**intersezione ordinata** (elementi presenti in entrambe, senza duplicati).
    ```python
    a = [1, 3, 5, 7]; b = [2, 3, 6, 7]  # → [3, 7]
    ```

### Matrici

18. Crea a mano una matrice 3×3 con i numeri da 1 a 9 e stampala riga per riga.
19. Data una matrice quadrata `n×n`, stampa solo la diagonale principale (elementi dove `i == j`).
    ```python
    matrice = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  # output: 1  5  9
    ```
20. Data una matrice, calcola la somma di tutti gli elementi.
21. Leggi dall'input una matrice `n×m` (prima `n`, poi `m`, poi i valori riga per riga). Stampa la somma degli elementi di ogni riga.
22. Data una matrice, costruisci la sua **trasposta**: una nuova matrice dove righe e colonne sono scambiate.
    ```python
    originale = [[1, 2, 3], [4, 5, 6]]  # trasposta: [[1, 4], [2, 5], [3, 6]]
    ```
23. Data una matrice quadrata `n×n`, stampa la **diagonale secondaria** (elementi con `i + j == n − 1`).
24. Data una matrice di interi, trova la posizione `(riga, colonna)` del valore massimo.
25. Data una matrice di interi, stampa `sì` se ogni riga è ordinata in modo non-decrescente (ogni elemento è ≥ al precedente nella stessa riga), `no` altrimenti.
26. Data una matrice quadrata `n×n`, stampa `sì` se è **simmetrica** (`matrice[i][j] == matrice[j][i]` per ogni `i`, `j`), `no` altrimenti.
27. Data una matrice, stampa per ogni coppia di righe adiacenti `i` e `i+1` se la **somma** della riga `i+1` è maggiore della somma della riga `i`.
28. Data una matrice, stampa `sì` se per ogni indice `i` compreso tra `0` e `len(matrice) − 2`, tutti gli elementi di `matrice[i+1]` sono **pari**, `no` altrimenti.
29. Data una matrice quadrata `n×n`, verifica che la **somma di ogni riga** sia uguale alla somma della colonna con lo stesso indice (somma riga 0 == somma colonna 0, ecc.). Stampa `sì` o `no`.
30. Data una matrice di interi, stampa `sì` se per ogni cella `matrice[i][j]` (con `i < len(matrice) − 1`), la cella sottostante `matrice[i+1][j]` è strettamente maggiore, `no` altrimenti (la matrice è strettamente crescente per colonne dall'alto verso il basso).

### Progetto: impiccato

31. Scrivi un programma che fa giocare l'utente al gioco dell'impiccato.
    - Il giocatore B propone una lettera alla volta. Se la lettera è presente nella parola segreta, tutte le sue posizioni vengono svelate.
    - Nella cartella `impiccato/` trovi i file `parola_segreta.py` e `impiccato.py` con la struttura di partenza. `impiccato.py` contiene la funzione `update(guess, parola, lettera)` che aggiorna la stringa di underscore:
      ```python
      update("____", "casa", "a")  # → "_a_a"
      update("_a_a", "casa", "c")  # → "ca_a"
      ```
32. Estendi l'impiccato aggiungendo un numero massimo di tentativi (6 nella versione classica, oppure dipendente dalla lunghezza della parola) e la possibilità di indovinare l'intera parola in un turno.