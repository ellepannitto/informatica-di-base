# Modulo 03 · Dall'if al while

## A fine lezione

- Sai modellare piccoli problemi con automi a stati finiti?
- Sai ragionare sui casi limite anche quando il codice sembra plausibile a prima vista?
- Sai definire sintassi e semantica del `while`?
- Sai distinguere guardia del ciclo, stato e condizione di terminazione?
- Sai usare il `while` conoscendo il numero di iterazioni da effettuare?
- Sai riconoscere errori frequenti e localizzarli?
- Sai usare casi di test per smascherare errori logici?
- Sai applicare le leggi di De Morgan?

## Errori nel codice

Abbiamo scritto dei programmi!
Ma saranno corretti?

**Caso 1:** il programma genera un errore

**Caso 2:** il programma termina l'esecuzione senza generale alcun errore

## Primi messaggi di errore

Un messaggio di errore contiene almeno tre informazioni utili:

| Informazione   | Domanda                                 |
| -------------- | --------------------------------------- |
| tipo di errore | che genere di problema e`?              |
| riga segnalata | dove si manifesta?                      |
| contesto       | quale operazione stava tentando Python? |

Esempi frequenti:

| Errore        | Causa tipica                      |
| ------------- | --------------------------------- |
| `SyntaxError` | sintassi non valida               |
| `NameError`   | nome di variabile non definito    |
| `TypeError`   | operazione tra tipi incompatibili |
| `ValueError`  | conversione non possibile         |

### Esercizi

Per ciascun programma: esegui il codice, individua il tipo di errore che produce e la riga in cui compare, poi spiega perché si verifica e correggi il codice di conseguenza.

**E1.**

Il codice chiede all'utente di inserire nome, cognome ed età e poi stampa la stringa
```
Ciao [NOME] [COGNOME]!
Tra dieci anni avrai X anni.
```

```python
nome = input("Nome: ")
cognome = input("Cognome: ")
eta = input("Età: ")
print("Ciao " + nome + " " + cognome + "!")
print("Tra dieci anni avrai " + eta + 10 + " anni.")
```

**E2.**

Il codice chiede all'utente di inserire l'anno di nascita e calcola l'età attuale.

```python
anno_nascita = input("Anno di nascita: ")
anno_corrente = 2026
eta = anno_corrente - anno_nascita
print("Hai circa " + str(eta) + " anni.")
```

**E3.**

Il codice chiede all'utente di inserire una parola e poi ne stampa la lunghezza

```python
parola = input("Parola: ")
lunghezza = len(parola)
print("La parola ha " + lunghezza + " lettere.")
```

**E4.**

Il codice chiede all'utente di inserire un numero intero e poi ne stampa il segno (positivo se compreso tra 0 e +inf, negativo altrimenti)

```python
x = int(input("Numero: "))
if x > 0:
    segno = "positivo"
elif x < 0:
    segno = "negativo"
print("Il numero è " + segno)
```

## Testing e casi limite

Anche se il programma non genera un errore, potrebbe comunque fare la cosa sbagliata: non basta che l'esecuzione si concluda per dire che "funziona".
Bisogna confrontare input e output attesi su casi scelti apposta.

Consideriamo questo programma, scritto per stampare un numero con il suo segno esplicito (`+7`, `-3`, `0`):

```python
n = int(input("Numero: "))
if n > 0:
    segno = "+"
else:
    segno = "-"
print(segno + str(n))
```

Proviamolo su diversi input:

| Input  | Output atteso | Output reale |
| ------ | ------------- | ------------ |
| `7`    | `+7`          | ?            |
| `-3`   | `-3`          | ?            |
| `0`    | `0`           | ?            |

Sembra ragionevole: il ramo `if` (se maggiore di 0) aggiunge `+`, il ramo `else` aggiunge `-`.

Ma `str(-3)` restituisce già `"-3"`: concatenarci davanti un altro `"-"` produce `"--3"`.
E per `0`, il ramo `else` produce `"-0"` invece di `"0"`.

Il programma non genera nessun errore, ma l'output è sbagliato per tutti i numeri non positivi.

**Perché succede:** `str(n)` su un numero negativo include già il segno meno.
Aggiungere `"-"` davanti raddoppia il segno.

**Correzione:**

```python
n = int(input("Numero: "))
if n > 0:
    print("+" + str(n))
elif n < 0:
    print(str(n))  # str(n) contiene già il segno
else:
    print("0")
```

## Metodo

1. scegli un input piccolo;
2. scrivi l'output atteso;
3. esegui il programma;
4. confronta il risultato reale con quello previsto;
5. se modifichi il codice, ripeti gli stessi test.

## Esercizi: if/elif/else e testing

Per ognuno degli esercizi seguenti il metodo è sempre lo stesso:

1. **scrivi i desiderata** — prima di eseguire il codice, compila la tabella con l'output che ti aspetti per ogni input;
2. **esegui e controlla** — lancia il programma con quegli input e annota l'output reale;
3. **confronta** — dove differiscono, spiega perché.

### Esercizio 1

Il programma riceve un numero intero e stampa `"pari"` se è pari, `"dispari"` se è dispari.

| Input | Output atteso | Output reale |
| ----- | ------------- | ------------ |
| `0`   |               |              |
| `3`   |               |              |
| `-4`  |               |              |
| `7`   |               |              |

<details>
```python
n = int(input("Numero: "))
if n > 0 and n % 2 == 0:
    print("pari")
else:
    print("dispari")
```
</details>

### Esercizio 2

Il programma riceve un voto e stampa `"promosso"` se è almeno 18, `"non promosso"` altrimenti.

| Input | Output atteso | Output reale |
| ----- | ------------- | ------------ |
| `15`  |               |              |
| `30`  |               |              |
| `18`  |               |              |

<details>

```python
voto = int(input("Voto: "))
if voto >= 18:
    print("promosso")

if voto <= 18:
    print("non promosso")
```

</details>


### Esercizio 3

Il programma riceve un numero intero e stampa `"positivo"` se è maggiore di zero, `"grande"` se è maggiore di 10, `"non positivo"` negli altri casi.

| Input | Output atteso | Output reale |
| ----- | ------------- | ------------ |
| `5`   |               |              |
| `15`  |               |              |
| `-2`  |               |              |


<details>

```python
x = int(input("x: "))
if x > 0:
    print("positivo")
elif x > 10:
    print("grande")
else:
    print("non positivo")
```

</details>

### Esercizio 4

Il programma riceve un intero e stampa `"fizz"` se è divisibile per 3, `"buzz"` se è divisibile per 5, `"fizzbuzz"` se è divisibile per entrambi, il numero stesso negli altri casi.

| Input | Output atteso | Output reale |
| ----- | ------------- | ------------ |
| `1`   |               |              |
| `3`   |               |              |
| `5`   |               |              |
| `15`  |               |              |
| `9`   |               |              |

Scrivi il programma e testane il funzionamento.

## Valutazione lazy

Gli operatori `and` e `or` non valutano sempre entrambe le parti dell'espressione.
Python si ferma appena il risultato finale è già determinato.

Questo comportamento si chiama **valutazione lazy** oppure **short-circuit**.

Partiamo da questo esempio:

```python
x = 5

if x > 0 and y > 0:
    print("Entrambi i numeri positivi!")
```

<details>
Questo codice genera errore, perché `y` non è definita.
</details>

Ora consideriamo questo caso:

```python
x = 5

if x > 0 or y > 0:
    print("Almeno un numero positivo!")
```

Perchè non genera errore?

| `x > 0` | `y > 0` | `x > 0 or y > 0` |
| ------- | ------- | ---------------- |
| `True`  | `False` | `True`           |
| `True`  | `True`  | `True`           |

`x > 0` vale già `True`, e questo basta a rendere vera tutta l'espressione con `or`.
Di conseguenza Python non valuta `y > 0`.

In generale:

- in `A or B`, se `A` vale `True`, Python non valuta `B`;
- in `A and B`, se `A` vale `False`, Python non valuta `B`.




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
