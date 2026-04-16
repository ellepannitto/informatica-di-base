# Modulo 04 · Ciclo while, sentinelle e convalida

## Autovalutazione

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

| | `if` | `while` |
| --- | --- | --- |
| valuta la condizione | una volta | a ogni iterazione |
| esegue il blocco | al massimo una volta | finché la condizione è vera |
| va verso la terminazione | sempre | solo se lo stato cambia |

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
3. poi torna a valutare la guardia;
4. se vale `False`, esce dal ciclo.

> le istruzioni da 1 a k vengono ripetute in ordine finchè lo stato del programma continua a soddisfare l'`espressione booleana`

### Esempio 1: contatore

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

### Esempio 2: input ripetuto

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

5. Scrivi un programma che chiede all'utente di inserire una parola. Il programma continua finché l'utente non scrive `fine`.

   ```
   Inserisci una parola: storia
   Inserisci una parola: geografia
   Inserisci una parola: fine
   ```

6. Scrivi un programma che stampi i numeri dispari compresi tra 1 e 10 (inclusi).

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

## Quando l'utente decide quando fermarsi

Negli esercizi del primo blocco il numero di iterazioni dipende da un valore noto in anticipo (es. `pagine = 120`). Ma a volte il programma non sa quante volte dovrà ripetere: lo decide l'utente durante l'esecuzione.

Esempio: sommare numeri finché l'utente non inserisce `-1`.

```python
numero = int(input("Numero (-1 per terminare): "))
somma = 0

while numero != -1:
    somma = somma + numero
    numero = int(input("Numero (-1 per terminare): "))
```

Lo schema è lo stesso dei due esempi visti prima:

- si legge il primo valore **prima** del ciclo (inizializzazione dello stato);
- la guardia controlla se continuare;
- nel corpo si fa il lavoro utile e si **rilegge** il valore (aggiornamento dello stato).

La differenza rispetto al contatore è che qui lo stato non cambia in modo prevedibile: cambia perché l'utente inserisce un valore diverso. Il programma si ferma quando quel valore soddisfa una condizione speciale concordata (`-1`, `"fine"`, ecc.).

## Esercizi

8. Scrivi un programma che chiede all'utente di inserire un numero. Il programma si ferma quando l'utente inserisce `0` e conta quanti numeri interi sono stati inseriti.

9. Scrivi un programma che chiede all'utente di inserire un numero. Il programma si ferma quando l'utente inserisce `0` e, per ogni numero inserito, se il numero è pari stampa `Hai inserito un numero pari!` altrimenti stampa `Hai inserito un numero dispari!`.

10. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce la parola `fine`. Per ogni parola inserita, se la parola è più lunga di 5 caratteri stampa `parola lunga` altrimenti stampa `parola breve`.

11. Scrivi un programma che legge un numero compreso tra 1 e 10 (controlla che il numero inserito sia lecito, altrimenti stampa un messaggio di errore) e stampa la tabellina di quel numero. Ad esempio, se viene inserito `3`:

    ```
    3 x 0 = 0
    3 x 1 = 3
    3 x 2 = 6
    ...
    3 x 10 = 30
    ```

12. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Per ogni parola inserita calcola quante vocali contiene. Alla fine, stampa il numero totale di vocali incontrate.

13. Scrivi un programma che chiede all'utente di inserire una parola. Il programma si ferma quando l'utente inserisce `fine`. Alla fine, stampa quante delle parole inserite finiscono per vocale.


## Cicli nidificati

Un ciclo può contenere un altro ciclo nel suo corpo. Il ciclo interno viene eseguito per intero a ogni iterazione del ciclo esterno.

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

14. Dati due numeri (es. `pagine = 3` e `righe = 5`), stampa tutte le combinazioni di pagine e righe come nell'esempio sopra.

15. Stampa la tavola pitagorica da 1 a 10:
    ```
    1 x 1 = 1
    1 x 2 = 2
    ...
    10 x 10 = 100
    ```

16. Chiedi all'utente `n` dall'input. Stampa un quadrato di asterischi `n x n`:
    ```
    ***
    ***
    ***
    ```

## Lo stato del programma durante un `while`

Ogni ciclo `while` si legge seguendo come cambia lo stato a ogni iterazione.

### Caso 1 · contatore

```python
i = 0
while i < 5:
    print(i)
    i = i + 1
```

| Passo | Istruzione                | Stato della memoria | Output |
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

| Passo | Istruzione                                | Stato della memoria         | Output |
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

| Passo | Istruzione                       | Stato della memoria | Output |
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

In modulo 3 abbiamo usato gli automi per descrivere come un `if/elif/else` **partiziona** gli input: dato un input, l'automa sceglie un ramo e raggiunge uno stato finale e si ferma lì.

Con il `while` il modello cambia in un punto essenziale: l'automa può **tornare indietro**. Invece di scegliere un ramo e fermarsi, riesegue lo stesso blocco più volte, aggiornando lo stato a ogni passaggio.

|                    | `if`             | `while`                                   |
| ------------------ | ---------------- | ----------------------------------------- |
| legge l'input      | una volta        | a ogni iterazione                         |
| transita tra stati | una sola volta   | può ciclare                               |
| stato finale       | raggiunto subito | raggiunto quando la guardia diventa falsa |

### Struttura generale

```
                 ┌──────────────────────────────────────┐
                 │                                      │
  ──────────────►│         valuta la guardia            │◄──┐
                 └──────────────────────────────────────┘   │
                              │             │               │
                           False          True              │
                              │             │               │
                              ▼             ▼               │
                       ╔══════════╗   ┌──────────┐          │
                       ║  fine    ║   │  corpo   │──────────┘
                       ╚══════════╝   └──────────┘
```

La freccia che dal corpo torna alla guardia è la novità rispetto all'`if`: l'automa **cicla** finché la condizione rimane vera.

### Esempio: contatore

```python
i = 0
while i < 5:
    print(i)
    i = i + 1
```

Lo stato è il valore di `i`. Ad ogni iterazione aumenta di uno, finché la guardia diventa falsa.

```
         ┌──────────────────────┐
         │   i < 5, i = i+1    │
         ▼                      │
──►  ┌──────────────┐           │
     │    resta     │───────────┘
     └──────────────┘
           │  i ≥ 5
           ▼
        ╔══════╗
        ║ fine ║
        ╚══════╝
```

Lo stato `resta` rappresenta "siamo dentro il ciclo". La transizione che torna su `resta` porta con sé l'aggiornamento (`i = i + 1`). Quando `i ≥ 5` non si rientra nel ciclo: si va in `fine`.

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
         ┌──────────────────────────────────┐
         │   numero ≠ -1, leggi prossimo   │
         ▼                                  │
──►  ┌──────────────┐                       │
     │    resta     │───────────────────────┘
     └──────────────┘
           │  numero = -1
           ▼
        ╔══════╗
        ║ fine ║
        ╚══════╝
```

La differenza rispetto al contatore è che qui non sappiamo quante volte il cappio verrà percorso: dipende dall'input dell'utente.

> La domanda da farsi sempre è: **quale valore dello stato porta la guardia a diventare falsa?** Se non esiste, il ciclo non termina mai.

## Esercizi: riconoscimento di stringhe

Un automa a stati finiti legge una stringa **una lettera alla volta**. A ogni passo:

1. guarda il carattere corrente;
2. segue la transizione corrispondente allo stato in cui si trova;
3. aggiorna lo stato.

Quando la stringa è finita, l'automa si ferma. Se si trova in uno **stato finale** (doppio bordo ╔══╗), la stringa è accettata; altrimenti è rifiutata.

### Come seguire un automa su una stringa concreta

Esempio: automa "almeno una vocale", stringa `"bac"`.

| Passo | Carattere | Stato corrente | Transizione     | Stato successivo |
| ----- | --------- | -------------- | --------------- | ---------------- |
| 1     | `b`       | `non_trovata`  | b non è vocale  | `non_trovata`    |
| 2     | `a`       | `non_trovata`  | a è vocale      | `trovata`        |
| 3     | `c`       | `trovata`      | già accettata, ciclo interrotto | `trovata` |
| fine  |           | `trovata` → ╔══╗ stato finale | | **sì** |

Stessa stringa, risultato opposto: `"bcd"`.

| Passo | Carattere | Stato corrente | Transizione     | Stato successivo |
| ----- | --------- | -------------- | --------------- | ---------------- |
| 1     | `b`       | `non_trovata`  | b non è vocale  | `non_trovata`    |
| 2     | `c`       | `non_trovata`  | c non è vocale  | `non_trovata`    |
| 3     | `d`       | `non_trovata`  | d non è vocale  | `non_trovata`    |
| fine  |           | `non_trovata` → non è stato finale | | **no** |

La regola è sempre la stessa: **l'accettazione dipende dallo stato in cui ci si trova quando la stringa finisce**, non da cosa è successo durante il percorso.

---

Per ogni esercizio:

1. identifica gli **stati** necessari (cosa devo ricordare mentre scorro la stringa?);
2. disegna l'automa con stati, transizioni e **stati finali** (doppio bordo);
3. scrivi il programma con un `while`.

---

### Esempio svolto: almeno una vocale

**Problema:** data una stringa, stampare `sì` se contiene almeno una vocale, `no` altrimenti.

**Stati:** due — `non_trovata` (nessuna vocale vista finora) e `trovata`. Una volta in `trovata` non si torna indietro.

```
         ┌─── carattere non è vocale ───┐
         ▼                              │
──►  ┌──────────────────┐               │
     │   non_trovata    │───────────────┘
     └──────────────────┘
           │  carattere è vocale
           ▼
        ╔══════════╗
        ║  trovata ║
        ╚══════════╝
```

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

---

### Esempio svolto: ogni `a` seguita da `b`

**Problema:** data una stringa, stampare `sì` se ogni `a` è immediatamente seguita da `b`, `no` altrimenti (es. `"abxab"` → sì, `"axb"` → no, `"a"` → no).

**Stati:** tre — `ok` (finora tutto corretto), `dopo_a` (l'ultimo carattere letto era `a`, aspettiamo `b`), `errore` (trovata una `a` non seguita da `b`). Da `errore` non si esce.

```
         ┌─── car ≠ 'a' ───┐          ┌─── qualsiasi ───┐
         ▼                 │          ▼                  │
──►  ╔═══════╗             │      ┌─────────┐            │
     ║  ok   ║─────────────┘      │ errore  │────────────┘
     ╚═══════╝
         │  car = 'a'
         ▼
     ┌─────────┐
     │ dopo_a  │── car = 'b' ──► ok
     └─────────┘── car ≠ 'b' ──► errore
```

Il diagramma diventa denso: è normale per automi con tre stati e transizioni incrociate. La tabella delle transizioni è spesso più chiara:

| Stato corrente | Carattere letto | Stato successivo |
| -------------- | --------------- | ---------------- |
| `ok`           | `a`             | `dopo_a`         |
| `ok`           | altro           | `ok`             |
| `dopo_a`       | `b`             | `ok`             |
| `dopo_a`       | `a`             | `errore`         |
| `dopo_a`       | altro           | `errore`         |
| `errore`       | qualsiasi       | `errore`         |

**Traccia su `"abxab"`:**

| Passo | Carattere | Stato corrente | Transizione         | Stato successivo |
| ----- | --------- | -------------- | ------------------- | ---------------- |
| 1     | `a`       | `ok`           | car = 'a'           | `dopo_a`         |
| 2     | `b`       | `dopo_a`       | car = 'b'           | `ok`             |
| 3     | `x`       | `ok`           | car ≠ 'a'           | `ok`             |
| 4     | `a`       | `ok`           | car = 'a'           | `dopo_a`         |
| 5     | `b`       | `dopo_a`       | car = 'b'           | `ok`             |
| fine  |           | `ok` → ╔══╗ stato finale | | **sì** |

**Traccia su `"axb"`:**

| Passo | Carattere | Stato corrente | Transizione         | Stato successivo |
| ----- | --------- | -------------- | ------------------- | ---------------- |
| 1     | `a`       | `ok`           | car = 'a'           | `dopo_a`         |
| 2     | `x`       | `dopo_a`       | car ≠ 'b'           | `errore`         |
| 3     | `b`       | `errore`       | ciclo interrotto    | `errore`         |
| fine  |           | `errore` → non è stato finale | | **no** |

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

Il controllo dopo il ciclo è necessario: una stringa come `"xxa"` non fa scattare `errore` durante il ciclo, ma finisce in `dopo_a` senza aver mai trovato la `b`.

---

### Livello base — due stati

13. **Almeno una vocale.** *(vedi esempio svolto sopra)*

14. **Tutte maiuscole.** Data una stringa, stampa `sì` se tutti i caratteri sono lettere maiuscole, `no` appena trovi un carattere che non lo è.

15. **Contiene cifra.** Data una stringa, stampa `sì` se contiene almeno un carattere numerico (`"0"` … `"9"`).

---

### Livello medio — tre stati o più

16. **Due vocali consecutive.** Data una stringa, stampa `sì` se contiene almeno due vocali consecutive (es. `"piaue"` → sì, `"cane"` → no).

    Suggerimento: gli stati sono `nessuna`, `una_vocale` (ultima letta era vocale), `trovata`.

17. **Ogni `a` seguita da `b`.** *(vedi esempio svolto sopra)*

18. **Numero pari di vocali.** Data una stringa, stampa `sì` se il numero totale di vocali è pari.

    Suggerimento: bastano due stati — `pari` e `dispari`. Si passa da uno all'altro a ogni vocale incontrata.

---

### Livello avanzato

19. **Parentesi bilanciate (solo tonde).** Data una stringa, stampa `sì` se ogni `(` è chiusa da una `)` e non compaiono `)` senza una `(` precedente.

    Suggerimento: lo stato è un contatore intero (non solo due valori); il ciclo termina prima se il contatore scende sotto zero.

<!-- <a id="mod4-errori"></a>
## Errori tipici dei cicli `while`

I problemi tipici sono quasi sempre tre.

| Errore | Che cosa succede |
| --- | --- |
| guardia sbagliata | il ciclo termina troppo presto o non termina |
| stato non aggiornato | la guardia non cambia mai |
| aggiornamento nel punto sbagliato | salti casi, duplichi passi o perdi il controllo del flusso |

Esempio di loop infinito:

```python
x = 0

while x < 5:
    print(x)
```

Qui `x` non cambia mai, quindi la guardia resta sempre vera.

Versione corretta:

```python
x = 0

while x < 5:
    print(x)
    x = x + 1
```

Domanda da farsi sempre:

> quale variabile sta portando il ciclo verso la terminazione?

Due errori tipici nei `while` di stampa sono questi:

- dimenticare l'aggiornamento della variabile interna, per esempio `j += 1`;
- scrivere una guardia troppo debole, come `while 1 < n`, che non dipende davvero dallo stato del ciclo.

In entrambi i casi il sintomo è lo stesso:

- il programma non si ferma;
- oppure continua a stampare righe sbagliate;
- oppure produce un pattern quasi giusto ma con uno shift di una unita'.

Regola pratica:

- la guardia deve dipendere da una variabile che cambia davvero;
- e quella variabile deve essere aggiornata nel punto giusto del ciclo. -->

## Esercizi utili

Conviene lavorare soprattutto su questi esercizi:

1. leggere parole da un file e fermarsi alla prima parola piu' lunga di 6 caratteri;
2. leggere frasi e fermarsi dopo 100 parole;
3. leggere 10 numeri e decidere se sono di piu' i pari o i dispari;
4. leggere numeri finché non compare una sentinella;
5. dire se un numero positivo è primo;
6. contare quante cifre ha un numero;
7. fermarsi quando la media di un gruppo di numeri diventa zero.

Sono esercizi utili perche' costringono a progettare con attenzione:

- la guardia;
- le variabili di stato;
- l'aggiornamento a ogni iterazione;
- la condizione di uscita.

---

## Esercizi assegnati su `while`

Nei testi degli esercizi assegnati ricorrono alcuni pattern molto coerenti con questo modulo.

### Sequenze terminate da sentinella

Esempi assegnati:

- leggere parole finché non compare `fine` e controllare se compare `"lingua"`;
- leggere numeri finché non compare `0` e stampare il massimo;
- leggere parole finché non compare `fine` e classificare ogni parola come lunga o breve;
- leggere numeri finché non compare `0` e dire per ciascuno se è pari o dispari.

Questi esercizi servono a consolidare tre idee:

- la sentinella non va trattata come dato normale;
- il controllo di terminazione va ripetuto a ogni passo;
- bisogna mantenere uno stato cumulativo corretto.

### Stato del ciclo e proprieta' della sequenza

Un secondo gruppo di esercizi chiede di riconoscere proprieta' piu' strutturate:

- verificare che ogni `1` sia seguito da `2`;
- contare quante parole finiscono per vocale;
- accumulare il numero totale di vocali lette;
- leggere un intero e stampare le sue potenze finché non si supera `1000`.

Qui il punto non è solo iterare, ma scegliere con precisione:

- quali variabili aggiornare;
- quando aggiornare;
- quale informazione deve sopravvivere da un'iterazione alla successiva.

### Convalida e vincoli

Tra gli esercizi assegnati compare anche la validazione esplicita:

```python
# leggere un numero tra 1 e 10, altrimenti segnalare errore
```

Questo è un caso tipico di `while` usato non per accumulare una sequenza, ma per imporre un vincolo sull'input.

### Mini-progetto: impiccato

L'esercizio sull'impiccato è particolarmente adatto a questo modulo perche' combina:

- stato corrente del gioco;
- ripetizione finché la parola non è completata;
- aggiornamento dopo ogni lettera proposta;
- possibilita' di introdurre tentativi massimi.

E' un buon ponte tra:

- `while`;
- stringhe;
- funzioni di aggiornamento dello stato;
- debugging di programmi un po' piu' lunghi.

---

## Soluzioni commentate emerse in lezione

Le soluzioni svolte mostrano bene che spesso conviene arrivare al programma finale per raffinamenti successivi.

### Verificare la regola "ogni 1 è seguito da 2"

Nei file svolti compaiono piu' versioni della stessa idea:

1. una soluzione che salva tutta la sequenza in lista;
2. una soluzione che controlla posizioni adiacenti;
3. una soluzione piu' pulita che tiene memoria del numero precedente.

Questa progressione è didatticamente molto utile perche' mostra che:

- una prima soluzione puo' funzionare ma essere fragile;
- rileggere il problema puo' suggerire uno stato piu' semplice;
- spesso basta una variabile `numero_pred` per evitare strutture superflue.

### Trovare il massimo con sentinella

Una delle soluzioni svolte usa lo schema:

```python
numero = int(input("Inserisci un numero: "))
massimo = -1

while numero != 0:
    if numero > massimo:
        massimo = numero
    numero = int(input("Inserisci un numero: "))

print(massimo)
```

Questo è un ottimo esempio di `while` con:

- sentinella;
- variabile accumulatrice;
- aggiornamento dello stato a ogni iterazione.

### Impiccato come automa

La soluzione svolta dell'impiccato introduce una funzione:

```python
def update(guess, parola_segreta, lettera):
    ...
```

e poi usa un ciclo:

```python
while GUESS != PAROLA_SEGRETA:
    ...
```

Questo rende esplicita una struttura molto importante:

- stato corrente del gioco -> `GUESS`
- input del giocatore -> nuova lettera
- funzione di transizione -> `update`
- condizione di arresto -> parola completata

In pratica, è un automa a stati finiti travestito da gioco.

---

## Esercizi di stampa con `while`

Ci sono anche esercizi molto utili per capire davvero come evolve lo stato in un ciclo:

- stampare `1`, poi `22`, poi `333`, fino a `n`;
- stampare triangoli o pattern numerici usando due cicli annidati;
- riscrivere la stessa soluzione passando da `while` a `for`.

Il valore di questi esercizi non è estetico, ma strutturale:

- costringono a distinguere il ciclo che controlla le righe dal ciclo che controlla i simboli dentro ogni riga;
- fanno vedere subito gli errori di guardia, di inizializzazione e di incremento;
- mostrano che un piccolo cambio di indice puo' produrre un pattern diverso.

Per esempio, in una soluzione con due cicli:

- l'indice esterno `i` puo' dire quale riga stiamo costruendo;
- l'indice interno `j` puo' dire quante volte ripetere un simbolo o quale simbolo mettere.

Se usi `i` per costruire la stringa ottieni un risultato; se usi `j`, ne ottieni un altro. Questo è uno dei modi piu' chiari per vedere che gli indici non sono "nomi intercambiabili", ma rappresentano ruoli diversi nello stato del programma.

---

## Esercizi

### Sequenze e contatori

1. Scrivi un programma che stampa i numeri da 1 a 10.
2. Scrivi un programma che legge un numero `n` dall'input e stampa i numeri da `n` a `0`.
3. Scrivi un programma che legge un numero `n` dall'input e stampa i numeri da `-n` a `n`.
4. Dato `pagine = 120`, stampa: `Sto leggendo la pagina 1`, `Sto leggendo la pagina 2`, ... fino all'ultima pagina.

### Input con sentinella

5. Scrivi un programma che chiede all'utente di inserire una parola e si ferma quando scrive `fine`.
6. Scrivi un programma che chiede all'utente di inserire un numero, si ferma quando inserisce `0` e conta quanti numeri interi sono stati inseriti.
7. Scrivi un programma che chiede all'utente di inserire un numero, si ferma quando inserisce `0` e, per ogni numero inserito, stampa `pari` oppure `dispari`.
8. Scrivi un programma che chiede all'utente di inserire una parola, si ferma quando scrive `fine` e, per ogni parola inserita, stampa `parola lunga` se ha più di 5 caratteri, altrimenti `parola breve`.

### Accumuli su sequenze

9. Chiedi all'utente di inserire una stringa e calcola quante vocali ci sono.
10. Dati `pagine = 3` e `righe = 5`, stampa tutte le combinazioni (Pagina 1 Riga 1, Pagina 1 Riga 2, ... Pagina 3 Riga 5).
11. Scrivi un programma che stampa i numeri dispari compresi tra 1 e 10 (inclusi).
12. Scrivi un programma che legge una parola dall'input e stampa solo le lettere in posizione pari.

### Convalida dell'input

13. Scrivi un programma che legge un numero compreso tra 1 e 10, stampa un messaggio di errore se il numero non è lecito, e stampa la tabellina di quel numero. Esempio per `3`:
    ```
    3 x 0 = 0
    3 x 1 = 3
    ...
    3 x 10 = 30
    ```

### Stato del ciclo e proprietà della sequenza

14. Scrivi un programma che chiede all'utente di inserire una parola e continua finché non scrive `fine`. Per ogni parola inserita calcola quante vocali ci sono. Alla fine stampa il numero totale di vocali.
15. Scrivi un programma che chiede all'utente di inserire una parola e continua finché non scrive `fine`. Alla fine stampa quante delle parole inserite finiscono per vocale.
16. Scrivi un programma che chiede all'utente di inserire dei numeri interi e si ferma quando scrive `0`. Stampa il maggiore dei numeri inseriti.
17. Scrivi un programma che chiede all'utente di inserire dei numeri interi e si ferma quando scrive `0`. Controlla se ogni `1` è seguito da un `2`. Esempi:
    - `9, 1, 2, 6, 1, 2, 0` → `Sequenza corretta`
    - `9, 1, 6, 1, 2, 0` → `Sequenza errata`
18. Scrivi un programma che chiede all'utente di inserire una parola e continua finché non scrive `fine`. Controlla se tra le parole inserite compare la parola `lingua`. Stampa `Sequenza corretta` o `Sequenza errata`.

### Potenze e cicli numerici

19. Scrivi un programma che chiede in input un intero e stampa le sue potenze finché il valore non supera 1000. Esempio per `2`:
    ```
    2^1 = 2
    2^2 = 4
    ...
    2^9 = 512
    ```

### Mini-progetto: impiccato

20. Scarica i file `parola_segreta.py` e `impiccato.py` dalla cartella `impiccato/`. Leggi il codice, eseguilo e poi cerca di aggiungere un numero massimo di tentativi.

---

## Riepilogo

Questo modulo organizza il materiale su:

- significato del ciclo `while`;
- iterazione a terminazione non nota in anticipo;
- sentinelle e input ripetuto;
- convalida dell'input;
- errori tipici dei cicli;
- uso del `while` per piccoli automi e problemi di scansione.



<!-- Per questo ogni `while` va letto sempre in termini di:

- stato iniziale;
- guardia;
- aggiornamento dello stato;
- condizione di uscita.

Un punto pratico importante:

- con `for` di solito sappiamo gia' quante volte iterare oppure quale sequenza stiamo scorrendo;
- con `while` la domanda tipica è invece: "continuo finché non succede qualcosa che mi fa fermare".

Per questo il `while` compare spesso in problemi del tipo:

- continua a leggere input finché non arriva una sentinella;
- continua a scorrere dati finché non trovi il primo caso interessante;
- continua a chiedere un valore finché non rispetta il vincolo richiesto.

Python non ha una forma `do ... while`: se il corpo del ciclo deve essere eseguito almeno una volta, bisogna progettare con attenzione stato iniziale e prima lettura dei dati.


## Il problema che porta al `while`

Il modulo parte da una domanda semplice:

> come si itera quando non sappiamo prima quante volte dovremo ripetere il blocco?


Esempio:

```python
lista_nomi = []
i = 0

while len(lista_nomi) < 10:
    if nome(testo[i]):
        lista_nomi.append(testo[i])
    i = i + 1
```

Qui non sappiamo in anticipo dove comparira' il decimo nome nel testo, quindi non possiamo fissare subito il numero corretto di passi.  -->