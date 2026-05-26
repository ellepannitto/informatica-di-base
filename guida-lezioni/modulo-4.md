# Modulo 04 · Paradigmi di programmazione con while e liste

## A fine lezione

- Sai progettare cicli con sentinelle e input ripetuto?
- Sai riconoscere errori tipici come loop infinito e stato non aggiornato?
- Sai applicare `while` a conteggi, validazione e sequenze di lunghezza variabile?
- Sai rappresentare dati ordinati con una lista?
- Sai usare le operazioni fondamentali sulle liste?
- Sai trasformare una stringa in lista con `split()`?
- Sai leggere sequenze di dati e accumularle in una lista?

## Paradigmi del `while`

La condizione del `while` può dipendere da cose molto diverse. Ecco cinque schemi ricorrenti.

### 1 · Contatore

> Stampa i numeri da 1 a 10.

**Indizi nel testo:** c'è un numero (**contatore**) preciso di ripetizioni ("da 1 a 10", "5 volte", "per ogni elemento"). Si sa già quante volte il ciclo dovrà girare.

Come scorre l'esecuzione:

```
i:    1    2    3    4    5    6    7    8    9   10   11
    ──────────────────────────────────────────────────────
≤10?  ✓    ✓    ✓    ✓    ✓    ✓    ✓    ✓    ✓    ✓    ✗
      ↓    ↓    ↓    ↓    ↓    ↓    ↓    ↓    ↓    ↓   STOP
    stampa ...
```

| passo | `i` | `i <= 10`? | stampa | `i` dopo |
|-------|-----|------------|--------|----------|
| 1     | 1   | ✓          | 1      | 2        |
| 2     | 2   | ✓          | 2      | 3        |
| …     | …   | ✓          | …      | …        |
| 10    | 10  | ✓          | 10     | 11       |
| 11    | 11  | ✗ → stop   | —      | —        |

<details>

```python
i = 1                # inizializza il contatore
while i <= 10:       # condizione: non abbiamo ancora raggiunto il limite
    print(i)
    i = i + 1        # aggiorna il contatore — senza questa riga, loop infinito
```

</details>

### 2 · Soglia su accumulatore

> Chiedi numeri all'utente e sommali. Fermati quando la somma supera 100.

**Indizi nel testo:** c'è un valore (**accumulatore**) che cresce ad ogni passo ("somma", "totale", "prodotto") e una soglia da raggiungere ("finché non supera", "almeno", "fino a raggiungere"). Non si sa in anticipo quante iterazioni servono ma la guardia del while non dipende direttamente dall'input inserito dall'utente.

Come scorre l'esecuzione (esempio con input `30, 25, 20, 40`):

```
input:    30      25      20      40
        ──────────────────────────────────────
somma:   0 → 30 → 55 → 75 → 115
             <100  <100  <100   ≥100
              ✓     ✓     ✓      ✗
                                STOP
```

| passo | `n` letto | `somma` prima | `somma < 100`? | `somma` dopo |
|-------|-----------|---------------|----------------|--------------|
| 1     | 30        | 0             | ✓              | 30           |
| 2     | 25        | 30            | ✓              | 55           |
| 3     | 20        | 55            | ✓              | 75           |
| 4     | 40        | 75            | ✓              | 115          |
| 5     | —         | 115           | ✗ → stop       | —            |

A differenza del contatore, non si può sapere in anticipo quante righe avrà la tabella: dipende dai valori inseriti.

<details>

```python
somma = 0             # inizializza l'accumulatore
while somma < 100:    # condizione: il risultato non ha ancora raggiunto la soglia
    n = int(input("Numero: "))
    somma = somma + n # aggiorna l'accumulatore
print("Totale:", somma)
```

</details>

### 3 · Proprietà matematica

> Dato un numero intero positivo, scopri se è divisibile per 5 usando solo la sottrazione.

**Indizi nel testo:** la condizione riguarda una proprietà del numero stesso ("finché è positivo", "finché è pari", "finché non è 0", "se è divisibile"). Non c'è un contatore né un input da attendere: il valore si trasforma da solo ad ogni passo. Il risultato emerge solo alla fine, dal valore rimasto.

Come scorre l'esecuzione:

```
n = 15               n = 13
15 → 10 → 5 → 0     13 → 8 → 3 → -2
 ✓    ✓    ✓   ✗      ✓    ✓    ✓    ✗
           STOP                  STOP
n == 0 → divisibile  n < 0 → non divisibile
```

| passo | `n` prima | `n > 0`? | `n` dopo |
|-------|-----------|----------|----------|
| 1     | 15        | ✓        | 10       |
| 2     | 10        | ✓        | 5        |
| 3     | 5         | ✓        | 0        |
| 4     | 0         | ✗ → stop | —        |

Dopo il ciclo, `n == 0` significa che le sottrazioni si sono fermate esattamente a zero: il numero era divisibile per 5.

<details>

```python
n = int(input("n: "))
while n > 0:         # condizione: proprietà del valore corrente
    n = n - 5        # trasforma il valore secondo la regola
if n == 0:
    print("divisibile per 5")
else:
    print("non divisibile per 5")
```

</details>

### 4 · Sentinella

> Chiedi numeri all'utente e conta quanti numeri sono stati inseriti. L'utente inserisce `0` per terminare.

**Indizi nel testo:** l'utente inserisce una sequenza di lunghezza non nota ("finché l'utente vuole", "uno per riga", "fino a quando inserisce X"). C'è un valore speciale (**sentinella**) che segnala la fine (`0`, `-1`, `"fine"`, …).

Come scorre l'esecuzione (esempio con input `7, 3, 9, 0`):

```
input:    7       3       9       0
        ──────────────────────────────────────
         ≠0      ≠0      ≠0      =0
          ✓       ✓       ✓       ✗
                                 STOP
```

| passo | `numero` letto | `numero != 0`? | `contatore` |
|-------|----------------|----------------|-------------|
| —     | 7              | (prima lettura) | 0          |
| 1     | —              | ✓              | 1           |
| —     | 3              | (rilettura)    | 1           |
| 2     | —              | ✓              | 2           |
| —     | 9              | (rilettura)    | 2           |
| 3     | —              | ✓              | 3           |
| —     | 0              | (rilettura)    | 3           |
| 4     | —              | ✗ → stop       | 3           |

La prima lettura va fatta **prima** del ciclo, così la guardia ha già un valore da controllare. Lo `0` viene letto ma non contato: la condizione lo blocca prima di entrare nel corpo.

<details>

```python
numero = int(input("Numero (0 per terminare): "))  # prima lettura — fuori dal ciclo
contatore = 0
while numero != 0:        # condizione: il valore letto non è la sentinella
    contatore = contatore + 1
    numero = int(input("Numero (0 per terminare): "))  # rileggi prima di controllare
print("Numeri inseriti:", contatore)
```

</details>

### 5 · Validazione (retry)

> Chiedi un voto all'utente. Se il voto non è compreso tra 0 e 30, ripeti la richiesta.

**Indizi nel testo:** il programma deve accettare solo certi valori ("controlla che sia valido", "se non è nel range", "ripeti finché l'utente non inserisce un valore corretto").

A differenza della sentinella, qui non c'è un valore speciale di uscita: il ciclo finisce non appena l'input soddisfa i vincoli.

<details>

```python
voto = int(input("Voto (0-30): "))
while voto < 0 or voto > 30:   # condizione: il valore non è accettabile
    print("Valore non valido.")
    voto = int(input("Voto (0-30): "))
print("Voto accettato:", voto)
```

</details>

## Esercizi - livello base

**1.** `[M4-WB-01]` *(sentinella)* Scrivi un programma che chiede all'utente di inserire una serie di numeri. Il programma si ferma quando l'utente inserisce `0` e stampa il prodotto di tutti i numeri inseriti.

```
Input:  2  3  4  0
Output: 24
```

<details>
Leggi il primo numero <strong>prima</strong> del ciclo. La guardia controlla se il numero è diverso da <code>0</code>. Nel corpo: aggiorna il prodotto, poi rileggi il prossimo numero. Lo <code>0</code> non va contato.
</details>

**2.** `[M4-WB-02]` *(sentinella)* Scrivi un programma che chiede all'utente di inserire un numero. Il programma si ferma quando l'utente inserisce `0` e, per ogni numero inserito, stampa `pari` o `dispari`.

```
Input:  3  4  7  0
Output: dispari
        pari
        dispari
```

<details>
Schema identico all'esercizio 1: leggi fuori dal ciclo, controlla la sentinella nella guardia, fai il lavoro nel corpo prima di rileggere. Qui il "lavoro" è un'istruzione <code>if</code>.
</details>

**3.** `[M4-WB-03]` *(contatore)* Scrivi un programma che legge un intero positivo `n` e stampa il suo fattoriale (`n! = 1 × 2 × … × n`).

```
Input:  5
Output: 120
```

<details>
Inizializza un accumulatore <code>prodotto = 1</code> e un contatore <code>i = 1</code>. La guardia è <code>i &lt;= n</code>. Nel corpo moltiplica <code>prodotto</code> per <code>i</code>, poi incrementa <code>i</code>.
</details>

**4.** `[M4-WB-04]` *(contatore)* Chiedi all'utente di inserire una stringa e calcola quante vocali contiene.

```
Input:  informatica
Output: 5
```

<details>
Usa un indice <code>i = 0</code> che scorre da <code>0</code> a <code>len(stringa) - 1</code>. Ad ogni passo controlla se <code>stringa[i]</code> è una vocale e aggiorna un contatore.
</details>

**5.** `[M4-WB-05]` *(soglia su accumulatore)* Chiedi numeri interi all'utente e sommali. Smetti di chiedere quando la somma raggiunge o supera 100. Alla fine stampa la somma.

```
Input:  30  25  20  40
Output: 115
```

<details>
Inizializza <code>somma = 0</code>. La guardia è <code>somma &lt; 100</code>. Nel corpo: leggi un numero e aggiungilo alla somma. Non serve leggere fuori dal ciclo: qui la condizione dipende dalla somma, non dall'input.
</details>

**6.** `[M4-WB-06]` *(soglia su accumulatore)* Chiedi all'utente di inserire parole una alla volta. Smetti di chiedere quando la lunghezza totale delle parole inserite supera 20 caratteri. Stampa una stringa che contiene tutte le parole lette separate da spazio.

```
Input:  casa  libro  sole  mare  notte
Output: casa libro sole mare notte
```

*(casa=4, libro=5, sole=4, mare=4 → totale 17; notte=5 → totale 22 > 20, stop)*

<details>
L'accumulatore non è una somma di numeri ma la somma delle lunghezze: <code>totale = totale + len(parola)</code>. La guardia è <code>totale &lt;= 20</code>. Accumula anche le parole lette in una stringa separata da aggiornare ad ogni passo.
</details>

**7.** `[M4-WB-07]` *(proprietà matematica)* Leggi un numero intero positivo `n`. Conta quante volte si può dividere per 2 prima che diventi dispari. Stampa il conteggio.

```
Input:  24
Output: 3
```

*(24 → 12 → 6 → 3, tre divisioni)*

<details>
La guardia controlla una proprietà di <code>n</code>: <code>n % 2 == 0</code>. Nel corpo dividi <code>n</code> per 2 e incrementa un contatore. Non serve input dentro il ciclo: <code>n</code> si trasforma da solo.
</details>

**8.** `[M4-WB-08]` *(proprietà matematica)* Data una stringa letta dall'input, stampa tutti i caratteri che precedono la prima vocale. Se la stringa non contiene vocali, stampa tutta la stringa.

```
Input:  stringa
Output: str

Input:  bcdf
Output: bcdf
```

<details>
Usa un indice <code>i = 0</code>. La guardia ha due condizioni collegate da <code>and</code>: non aver superato la lunghezza della stringa (<code>i &lt; len(s)</code>) e il carattere corrente non essere una vocale (<code>s[i] not in "aeiouAEIOU"</code>). Nel corpo stampa <code>s[i]</code> e incrementa <code>i</code>.
</details>

**9.** `[M4-WB-09]` *(validazione)* Chiedi all'utente di inserire un anno compreso tra 1900 e 2100. Alla fine stampa `Anno accettato: <anno>`.

```
Input:  1800  2050
Output: Anno accettato: 2050
```

<details>
Leggi il primo anno prima del ciclo. La guardia è la condizione di <em>rifiuto</em>: <code>anno &lt; 1900 or anno &gt; 2100</code>. Nel corpo stampa un messaggio di errore e rileggi. Quando il ciclo finisce, il valore è già quello valido.
</details>

**10.** `[M4-WB-10]` *(validazione)* Chiedi all'utente di inserire una parola. Ripeti la richiesta finché la parola non inizia con una lettera maiuscola. Stampa `Parola accettata`.

```
Input:  ciao  Ciao
Output: Parola accettata
```

<details>
La guardia è la condizione di rifiuto: <code>parola[0]</code> non è maiuscolo. Puoi controllarlo confrontando <code>parola[0]</code> con la sua versione maiuscola: <code>parola[0] != parola[0].upper()</code>.
</details>

**11.** `[M4-WB-11]` Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce la parola `fine`. Per ogni parola inserita, se la parola è più lunga di 5 caratteri stampa `parola lunga` altrimenti stampa `parola breve`.

```
Input:  gatto  programmazione  sole  fine
Output: parola breve
        parola lunga
        parola breve
```

<details>
Paradigma: <em>sentinella</em>. La sentinella è la stringa <code>"fine"</code>. Leggi la prima parola prima del ciclo. La guardia controlla <code>parola != "fine"</code>. Usa <code>len(parola)</code> per decidere cosa stampare.
</details>

**12.** `[M4-WB-12]` Scrivi un programma che chiede all'utente di inserire una parola e continua finché non scrive `fine`. Controlla se tra le parole inserite compare la parola `informatica`. Stampa `sì` o `no`.

```
Input:  python  informatica  matematica  fine
Output: sì

Input:  python  algebra  fine
Output: no
```

<details>
Paradigma: <em>sentinella</em>. Tieni una variabile booleana <code>trovata = False</code>. Nel corpo, se la parola corrente è <code>"informatica"</code> aggiorna <code>trovata</code>. Dopo il ciclo, stampa in base al valore di <code>trovata</code>.
</details>

**13.** `[M4-WB-13]` Leggi un intero positivo `n` e stampa tutti i multipli di 3 da 3 fino a `n`.

```
Input:  15
Output: 3  6  9  12  15
```

<details>
Paradigma: <em>contatore</em>. Usa un contatore <code>i = 3</code>. La guardia è <code>i &lt;= n</code>. Nel corpo stampa <code>i</code> e incrementa di 3.
</details>

**14.** `[M4-WB-14]` Chiedi all'utente di inserire numeri interi. Smetti quando il prodotto di tutti i numeri inseriti supera 1000. Stampa quanti numeri hai letto.

```
Input:  4  5  6  9
Output: 4
```

*(4×5=20, 20×6=120, 120×9=1080 > 1000, stop dopo 4 numeri)*

<details>
Paradigma: <em>soglia su accumulatore</em>. L'accumulatore è un prodotto, non una somma: inizializza <code>prodotto = 1</code> e aggiorna con <code>prodotto = prodotto * n</code>. La guardia è <code>prodotto &lt;= 1000</code>. Non serve leggere fuori dal ciclo.
</details>

**15.** `[M4-WB-15]` Leggi un intero positivo `n`. Applica ripetutamente la regola: se `n` è divisibile per 3, dividilo per 3; altrimenti fermati. Stampa il valore finale di `n`.

```
Input:  27
Output: 1

Input:  12
Output: 4
```

*(27 → 9 → 3 → 1; 12 → 4, poi 4 % 3 ≠ 0 stop)*

<details>
Paradigma: <em>proprietà matematica</em>. La guardia controlla <code>n % 3 == 0</code>. Nel corpo <code>n = n // 3</code>. Il valore si trasforma da solo, senza leggere input nel ciclo.
</details>

**16.** `[M4-WB-16]` Chiedi all'utente di inserire un numero intero dispari. Stampa `Numero dispari accettato`.

```
Input:  4  6  7
Output: Numero dispari accettato
```

<details>
Paradigma: <em>validazione</em>. La guardia è la condizione di rifiuto: <code>n % 2 == 0</code> (il numero è pari, quindi non accettabile). Leggi prima del ciclo, rileggi nel corpo.
</details>

## Esercizi - livello intermedio

**1.** `[M4-WI-01]` Scrivi un programma che legge un numero compreso tra 1 e 10 (controlla che il numero inserito sia lecito, altrimenti ripeti la richiesta) e stampa la tabellina di quel numero. Ad esempio, se viene inserito `3`:

```
3 x 0 = 0
3 x 1 = 3
3 x 2 = 6
...
3 x 10 = 30
```

**2.** `[M4-WI-02]` Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Per ogni parola inserita calcola quante vocali contiene. Alla fine, stampa il numero totale di vocali incontrate.

**3.** `[M4-WI-03]` Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Alla fine, stampa quante delle parole inserite finiscono per vocale.

**4.** `[M4-WI-04]` Scrivi un programma che legge parole dall'input finché l'utente non scrive `fine`. Conta quante parole iniziano con una lettera maiuscola.

**5.** `[M4-WI-05]` Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`, e al termine stampa il massimo tra quelli inseriti. (Se non viene inserito nessun numero prima dello zero, stampa un messaggio apposito.)

**6.** `[M4-WI-06]` Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`. Al termine stampa quanti erano pari e quanti dispari, e quale delle due categorie era più numerosa.

**7.** `[M4-WI-07]` Scrivi un programma che legge numeri interi finché l'utente non inserisce `0` e calcola la media dei valori inseriti. Se non viene inserito nessun valore prima dello zero, stampa `nessun dato`.

**8.** `[M4-WI-08]` Dati due numeri (es. `pagine = 3` e `righe = 5`), stampa tutte le combinazioni di pagine e righe.

**9.** `[M4-WI-09]` Chiedi all'utente `n` dall'input. Stampa un quadrato di asterischi `n x n`:

```
***
***
***
```

**10.** `[M4-WI-10]` Scrivi un programma che legge un intero positivo `n` e stampa la sequenza di Collatz: se `n` è pari calcola `n // 2`, se è dispari calcola `3 * n + 1`; ripeti finché `n` non diventa `1`. Stampa ogni valore e, alla fine, quanti passi sono stati necessari.

**11.** `[M4-WI-11]` Leggi interi uno alla volta. Continua a leggere finché ogni nuovo numero è strettamente maggiore del precedente. Quando la sequenza si interrompe (o l'utente inserisce 0), stampa quanti numeri validi hai letto.

**12.** `[M4-WI-12]` Leggi interi positivi uno alla volta, finché ogni nuovo numero è strettamente maggiore del precedente. Per ogni coppia consecutiva (a, b) con b > a+1, stampa anche tutti i numeri interi compresi tra a e b (esclusi). Es.: se l'utente inserisce 13 poi 16, stampa anche 14 e 15.

**13.** `[M4-WI-13]` Scrivi un programma che legge un intero positivo `n` e stampa i primi `n` numeri della sequenza di Fibonacci: `0, 1, 1, 2, 3, 5, 8, …`

## Esercizi - livello avanzato

**1.** `[M4-WA-01]` Scrivi un programma che legge parole dall'input e si ferma alla prima parola più lunga di 6 caratteri oppure quando trova la parola fine. Se il programma trova una parola più lunga di 6 caratteri, la stampa. Se non compare nessuna parola così lunga prima di `fine`, stampa `nessuna`.

**2.** `[M4-WA-02]` Stampa la tavola pitagorica da 1 a 10:

```
1 x 1 = 1
1 x 2 = 2
...
10 x 10 = 100
```

**3.** `[M4-WA-03]` Scrivi un programma che legge un intero positivo `n` e stampa tutte le sue cifre, una per riga, partendo da quella meno significativa. (Es.: `n = 374` → `4`, `7`, `3`.) Non usare stringhe: estrai le cifre con divisione e modulo.

**4.** `[M4-WA-04]` Scrivi un programma che legge una sequenza di numeri positivi terminata da `-1` e stampa ogni numero insieme al suo scarto rispetto al numero precedente. Per il primo numero lo scarto non esiste; per gli altri stampa `differenza: +3` o `differenza: -5` ecc.

**5.** `[M4-WA-05]` Scrivi un programma che legge numeri interi finché l'utente non inserisce `0`. Stampa `sì` se la sequenza è non-decrescente (ogni numero è ≥ al precedente), `no` altrimenti.

**6.** `[M4-WA-06]` Scrivi un programma che legge un intero positivo `n` e stabilisce se è primo. Un numero è primo se è divisibile solo per 1 e per se stesso.

**7.** `[M4-WA-07]` Scrivi un programma che chiede all'utente di inserire dei numeri interi e si ferma quando scrive `0`. Controlla se ogni `1` è seguito da un `2`. Esempi:

- `9, 1, 2, 6, 1, 2, 0` → `Sequenza corretta`
- `9, 1, 6, 1, 2, 0` → `Sequenza errata`

## Due problemi che il `while` da solo non riesce a risolvere

### Problema 1: stampa i numeri al contrario

Scrivi un programma che legge numeri interi uno alla volta (terminati da `0`) e li stampa in ordine inverso rispetto a quello in cui sono stati inseriti.

Esempio:

```
Input:  3  7  2  5  0
Output: 5  2  7  3
```

Possiamo risolverlo usando solo i costrutti che conosciamo? Cosa manca?

```python
n = int(input("Inserisci un numero:"))

while n != 0:
    # fai qualcosa, vorremmo "ricordare" numero, ma dove?
    n = int(input("Inserisci un numero:"))

# a questo punto non sappiamo più cosa è stato inserito
```

Il problema è che quando arriva lo `0`, i numeri precedenti non esistono più: ogni nuova lettura sovrascrive la variabile. Per stampare al contrario bisogna prima raccogliere tutti i valori, poi scorrere la raccolta in senso inverso.

Il `while` sa iterare, ma non sa ricordare una sequenza di valori.

### Problema 2: chi è sopra la media?

Scrivi un programma che legge numeri interi uno alla volta (terminati da `0`) e stampa quelli che superano la media di tutti i numeri inseriti.

Esempio:

```
Input:  4  8  2  6  0
Media:  5.0
Output: 8  6
```

Per sapere se `4` è sopra la media, devi già conoscere anche `8`, `2` e `6`. La media si può calcolare solo dopo aver letto l'ultimo numero.

Servono quindi due iterazioni sugli stessi dati:

1. leggi tutti i numeri, calcola la media;
2. scorri di nuovo gli stessi numeri e stampa quelli sopra la media.

Per fare la seconda iterazione i numeri devono essere ancora disponibili — e con variabili singole non lo sono.

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

print(numeri)

# ora numeri contiene tutta la sequenza
i = len(numeri) - 1
while i >= 0:
    print(numeri[i])
    i = i - 1
```

Il `while` di lettura accumula; il secondo `while` scorre la lista al contrario.

## Una nuova operazione sulle stringe

Una nuova operazione importante sulle stringhe è questa:

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

## Esercizi sulle liste

### Livello base

**1.** `[M4-LB-01]` Crea una lista con i numeri da 1 a 5 usando `append` in un ciclo `while`. Poi stampa la lista.

**2.** `[M4-LB-02]` Data la lista `voti = [24, 28, 30, 18, 27]`, stampa il primo e l'ultimo voto.

**3.** `[M4-LB-03]` Data la lista `nomi = ["Alice", "Bruno", "Carla", "Dario"]`, stampa il secondo e il penultimo nome.

**4.** `[M4-LB-04]` Leggi numeri interi dall'input fino a `0` e salvali in una lista. Stampa la lista alla fine.

**5.** `[M4-LB-05]` Leggi parole dall'input fino a `fine` e salvale in una lista. Stampa quante parole sono state inserite.

**6.** `[M4-LB-06]` Data una lista di numeri, calcola e stampa la somma di tutti gli elementi senza usare `sum()`.

**7.** `[M4-LB-07]` Data una lista di numeri, stampa solo quelli maggiori di 10.

**8.** `[M4-LB-08]` Data una lista di parole, stampa solo quelle che iniziano per vocale.

**9.** `[M4-LB-09]` Data la lista `prezzi = [3.5, 1.2, 7.8, 4.0]`, stampa il prezzo più alto senza usare `max()`: scorri la lista con un `while` e tieni traccia del massimo.

**10.** `[M4-LB-10]` Leggi parole finché l'utente non scrive `fine` e stampale in ordine inverso rispetto all'ordine di inserimento.

### Livello intermedio

**11.** `[M4-LI-01]` Leggi numeri interi dall'input fino a `0`. Costruisci una lista con i soli numeri **pari** e stampala.

```
Input:  3  8  5  4  7  2  0
Output: [8, 4, 2]
```

**12.** `[M4-LI-02]` Data la lista `voti = [18, 25, 30, 22, 28, 19]`, calcola e stampa la media. Poi stampa separatamente i voti sopra la media e quelli sotto.

```
Media: 23.67
Sopra: [25, 30, 28]
Sotto: [18, 22, 19]
```

**13.** `[M4-LI-03]` Leggi parole dall'input fino a `fine`. Costruisci due liste: una con le parole che hanno lunghezza pari, una con quelle di lunghezza dispari. Stampa entrambe.

```
Input:  sole  luna  cane  gatto  fine
Output: pari:    ['sole', 'luna', 'cane']
        dispari: ['gatto']
```

**14.** `[M4-LI-04]` Verifica se una parola letta dall'input è un **palindromo** usando una lista: converti la stringa in lista di caratteri, poi confronta il primo con l'ultimo, il secondo con il penultimo, ecc., usando un ciclo `while` con due indici.

```
Input:  radar
Output: palindromo

Input:  cane
Output: non palindromo
```

**15.** `[M4-LI-05]` Leggi numeri interi dall'input fino a `0` e costruisci una lista. Poi stampa la lista senza duplicati (ogni valore deve comparire una sola volta, nel primo ordine in cui è apparso).

```
Input:  3  1  4  1  5  3  2  0
Output: [3, 1, 4, 5, 2]
```

**16.** `[M4-LI-06]` Date due liste di numeri interi già definite nel codice, costruisci una terza lista con gli elementi **in comune** tra le due (senza duplicati).

```
a = [1, 3, 5, 7, 3]
b = [3, 5, 6, 7]
Output: [3, 5, 7]
```

### Livello avanzato

**17.** `[M4-LA-01]` Leggi numeri interi dall'input fino a `0`. Stampa il **secondo massimo** della sequenza (il più grande tra tutti i valori escluso il massimo assoluto). Se ci sono meno di due valori distinti, stampa un messaggio apposito.

```
Input:  5  3  9  7  9  0
Output: secondo massimo: 7
```

**18.** `[M4-LA-02]` Leggi parole dall'input fino a `fine`. Stampa la parola **più lunga** e quella **più corta**. In caso di parità di lunghezza prendi la prima apparsa.

```
Input:  sole  programmazione  io  cane  fine
Output: più lunga:  programmazione
        più corta:  io
```

**19.** `[M4-LA-03]` Leggi una sequenza di numeri interi dall'input fino a `0` e salvali in una lista. Poi stampa tutte le coppie `(lista[i], lista[i+1])` di elementi consecutivi tali che il secondo è strettamente maggiore del primo.

```
Input:  2  5  3  8  8  1  0
Output: (2, 5)
        (3, 8)
```

**20.** `[M4-LA-04]` Leggi parole dall'input fino a `fine` e salvale in una lista. Poi stampa, per ogni parola, quante volte quella parola è già apparsa in precedenza nella lista (inclusa la posizione corrente, la prima occorrenza vale 0 ripetizioni).

```
Input:  gatto  cane  gatto  gatto  cane  fine
Output: gatto: 0
        cane: 0
        gatto: 1
        gatto: 2
        cane: 1
```
**21.** `[M4-LA-05]` Data una frase letta dall'input, usa `split()` per ottenere la lista delle parole e stampane la lunghezza.

**22.** `[M4-LA-06]` Data una lista di interi, invertila senza crearne una nuova. Usa due indici (uno all'inizio, uno alla fine) e scambia gli elementi avvicinandoli al centro. (Es.: `[1, 2, 3, 4, 5]` → `[5, 4, 3, 2, 1]`)

**23.** `[M4-LA-07]` Data una lista di interi che contiene alcuni zeri, sposta tutti gli zeri alla fine conservando l'ordine degli altri elementi, senza creare una nuova lista. (Es.: `[0, 3, 0, 1, 5, 0, 2]` → `[3, 1, 5, 2, 0, 0, 0]`)

**24.** `[M4-LA-08]` Data una lista e un intero `k`, ruota la lista di `k` posizioni verso sinistra in place, senza creare una nuova lista. (Es.: `[1, 2, 3, 4, 5]` con `k=2` → `[3, 4, 5, 1, 2]`)

**25.** `[M4-LA-09]` Leggi interi fino a 0 e salvali in una lista. Trova il valore massimo e stampa sia il valore sia l'indice in cui si trova. In caso di parità, prendi la prima occorrenza.

**26.** `[M4-LA-10]` Date due liste già ordinate in modo crescente (es. `a=[1,3,5,7]` e `b=[2,4,6]`), costruisci una terza lista che contiene tutti gli elementi in ordine crescente, senza usare `sort()`. (Suggerimento: usa due indici, uno per lista, e avanza quello con il valore minore.)
