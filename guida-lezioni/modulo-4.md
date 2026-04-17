# Modulo 04 · Ciclo while, sentinelle e convalida

## A fine lezione

- Sai usare `while` quando non conosci in anticipo il numero di iterazioni?
- Sai distinguere guardia del ciclo, stato e condizione di terminazione?
- Sai progettare cicli con sentinelle e input ripetuto?
- Sai riconoscere errori tipici come loop infinito e stato non aggiornato?
- Sai leggere un `while` come evoluzione dello stato del programma?
- Sai applicare `while` a conteggi, validazione e piccoli automi?

## Dal `if` al `while`

Abbiamo già visto il costrutto `if`:

```python
if condizione:
    blocco
```

Il blocco viene eseguito **al massimo una volta**: se la condizione è vera, entra; altrimenti salta.

Ma se vogliamo ripetere il blocco finché la condizione resta vera?

```python
x = 0

if x < 5:
    print(x)
    x = x + 1
```

Questo stampa `0` e basta. Per stampare `0, 1, 2, 3, 4` dovremmo copiare il blocco cinque volte — e se non sappiamo in anticipo quante volte, non possiamo farlo.

Il `while` risolve esattamente questo problema:

```python
x = 0

while x < 5:
    print(x)
    x = x + 1
```

La struttura è identica all'`if`. La differenza è una sola: dopo aver eseguito il blocco, `while` **torna a valutare la condizione**. Se è ancora vera, ripete. Se è falsa, si ferma.

|                          | `if`                 | `while`                     |
| ------------------------ | -------------------- | --------------------------- |
| valuta la condizione     | una volta            | a ogni iterazione           |
| esegue il blocco         | al massimo una volta | finché la condizione è vera |
| va verso la terminazione | sempre               | solo se lo stato cambia     |

Questa è la differenza fondamentale: con `while`, il blocco deve **modificare lo stato** in modo da portare prima o poi la condizione a diventare falsa. Se non lo fa, il ciclo non si ferma mai.

## Sintassi del `while`

Forma generale:

```python
while espressione_booleana:
    istruzione-1
    istruzione-2
    ...
    istruzione-k
```

Parti da riconoscere:

- `while` introduce una ripetizione condizionata;
- la guardia è un'espressione booleana;
- i due punti `:` aprono il blocco;
- il blocco del ciclo va indentato.

## Semantica del `while`

1. Python valuta la guardia;
2. se vale `True`, esegue il blocco;
3. poi torna a valutare la guardia (punto 1);
4. se vale `False`, esce dal ciclo.

> le istruzioni da 1 a k vengono ripetute in ordine finchè lo stato del programma continua a soddisfare l'`espressione booleana`

## Esempi

### contatore

```python
i = 0
while i < 5:
    print(i)
    i = i + 1
```

- `i = 0` è l'inizializzazione dello stato;
- `i < 5` è la guardia: il ciclo continua finché vale `True`;
- `print(i)` è l'istruzione;
- `i = i + 1` è l'aggiornamento che avvicina il programma alla terminazione.

> Cosa succede se si dimentica `i += 1`? La guardia non cambia mai e il ciclo non finisce mai: **ciclo infinito**.

### input ripetuto

```python
risposta = input("Continuo? (s/n): ")
while risposta == "s":
    print("Ancora...")
    risposta = input("Continuo? (s/n): ")
```

Qui il numero di ripetizioni non è noto in anticipo: dipende da cosa inserisce l'utente.

## Esercizi

1. Scrivi un programma che stampi i numeri da 1 a 10.
2. Scrivi un programma che legge un numero `n` dall'input e stampa i numeri da `n` a `0`.
3. Scrivi un programma che legge un numero `n` dall'input e stampa i numeri da `-n` a `n`.
4. Dato un certo numero (es. `pagine = 120`), stampa:
   ```
   Sto leggendo la pagina 1
   Sto leggendo la pagina 2
   ...
   ```
   fino all'ultima pagina.
5. Scrivi un programma che stampi i numeri dispari compresi tra 1 e 10 (inclusi).
6. Scrivi un programma che legge una parola dall'input e stampa solo le lettere in posizione pari (indice 0, 2, 4, …).
7. Scrivi un programma che chiede in input un intero e stampa le potenze di quel numero finché il valore non eccede 1000. Ad esempio, se viene inserito `2`:
   ```
   2^1 = 2
   2^2 = 4
   2^3 = 8
   2^4 = 16
   2^5 = 32
   2^6 = 64
   2^7 = 128
   2^8 = 256
   2^9 = 512
   ```
8. Scrivi un programma che chiede all'utente di inserire una parola. Il programma continua finché l'utente non scrive `fine`.
   ```
   Inserisci una parola: storia
   Inserisci una parola: geografia
   Inserisci una parola: fine
   ```

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

## Cicli annidati

Un ciclo può contenere un altro ciclo nel suo corpo.
Il ciclo interno viene eseguito per intero a ogni iterazione del ciclo esterno.

Esempio: stampare tutte le combinazioni di pagina e riga.

```python
pagine = 3
righe = 5

p = 1
while p <= pagine:
    r = 1
    while r <= righe:
        print("Pagina", p, "Riga", r)
        r = r + 1
    p = p + 1
```

Output:
```
Pagina 1 Riga 1
Pagina 1 Riga 2
...
Pagina 3 Riga 5
```

Punti da osservare:

- il ciclo esterno controlla `p`, che va da `1` a `pagine`;
- il ciclo interno controlla `r`, che **riparte da `1` a ogni nuova pagina**;
- ogni ciclo ha la propria variabile di stato e il proprio aggiornamento.

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

## Lo stato del programma durante un `while`

Ogni ciclo `while` si legge seguendo come cambia lo stato a ogni iterazione.

### Caso 1 · contatore

```python
i = 0
while i < 5:
    print(i)
    i = i + 1
```

| Passo | Codice sorgente           | Stato della memoria | Output |
| ----- | ------------------------- | ------------------- | ------ |
| 1     | `i = 0`                   | `i → 0`             |        |
| 2     | `while i < 5` → True      | `i → 0`             |        |
| 3     | `print(i)`                | `i → 0`             | `0`    |
| 4     | `i = i + 1`               | `i → 1`             |        |
| 5     | `while i < 5` → True      | `i → 1`             |        |
| 6     | `print(i)`                | `i → 1`             | `1`    |
| 7     | `i = i + 1`               | `i → 2`             |        |
| …     | …                         | …                   | …      |
| n     | `while i < 5` → **False** | `i → 5`             |        |

### Caso 2 · valore speciale di stop

```python
numero = int(input("Numero (-1 per terminare): "))
somma = 0
while numero != -1:
    somma = somma + numero
    numero = int(input("Numero (-1 per terminare): "))
```

(ipotesi: l'utente inserisce `4`, poi `7`, poi `-1`)

| Passo | Codice sorgente                           | Stato della memoria         | Output |
| ----- | ----------------------------------------- | --------------------------- | ------ |
| 1     | `numero = int(input(...))` ← utente: `4`  | `numero → 4`                |        |
| 2     | `somma = 0`                               | `numero → 4`, `somma → 0`   |        |
| 3     | `while numero != -1` → True               | `numero → 4`, `somma → 0`   |        |
| 4     | `somma = somma + numero`                  | `numero → 4`, `somma → 4`   |        |
| 5     | `numero = int(input(...))` ← utente: `7`  | `numero → 7`, `somma → 4`   |        |
| 6     | `while numero != -1` → True               | `numero → 7`, `somma → 4`   |        |
| 7     | `somma = somma + numero`                  | `numero → 7`, `somma → 11`  |        |
| 8     | `numero = int(input(...))` ← utente: `-1` | `numero → -1`, `somma → 11` |        |
| 9     | `while numero != -1` → **False**          | `numero → -1`, `somma → 11` |        |

### Caso 3 · cicli nidificati

```python
p = 1
while p <= 2:
    r = 1
    while r <= 3:
        print(p, r)
        r = r + 1
    p = p + 1
```

| Passo | Codice sorgente                  | Stato della memoria | Output |
| ----- | -------------------------------- | ------------------- | ------ |
| 1     | `p = 1`                          | `p → 1`             |        |
| 2     | `while p <= 2` → True            | `p → 1`             |        |
| 3     | `r = 1`                          | `p → 1`, `r → 1`    |        |
| 4     | `while r <= 3` → True            | `p → 1`, `r → 1`    |        |
| 5     | `print(p, r)`                    | `p → 1`, `r → 1`    | `1 1`  |
| 6     | `r = r + 1`                      | `p → 1`, `r → 2`    |        |
| 7     | `while r <= 3` → True            | `p → 1`, `r → 2`    |        |
| 8     | `print(p, r)`                    | `p → 1`, `r → 2`    | `1 2`  |
| …     | …                                | …                   | …      |
| n     | `while r <= 3` → **False**       | `p → 1`, `r → 4`    |        |
| n+1   | `p = p + 1`                      | `p → 2`, `r → 4`    |        |
| n+2   | `while p <= 2` → True            | `p → 2`, `r → 4`    |        |
| n+3   | `r = 1` ← **reinizializzazione** | `p → 2`, `r → 1`    |        |
| …     | …                                | …                   | …      |
| m     | `while p <= 2` → **False**       | `p → 3`             |        |

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

