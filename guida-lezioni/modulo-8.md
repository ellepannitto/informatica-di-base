# Modulo 08 · Ciclo for e iterazione

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- usare il ciclo `for` su stringhe, liste e `range()`;
- capire la semantica elementare dell'iterazione;
- leggere il comportamento del `for` in termini di stato;
- applicare il `for` a conteggi, trasformazioni e scansioni;
- usare cicli annidati per costruire pattern e output strutturato.

---

<a id="mod8-for"></a>
## Il problema che porta al `for`

Si puo' partire da un esempio come questo:

```python
incipit = "Era una notte incantevole, una di quelle notti..."
parole = incipit.split()

parole[0] = parole[0].lower()
parole[1] = parole[1].lower()
parole[2] = parole[2].lower()
# ...
```

Problemi evidenti:

- il codice e' lungo e fragile;
- dipende dalla lunghezza della lista;
- non e' riusabile;
- ripete sempre la stessa operazione concettuale.

Il `for` nasce proprio per esprimere una stessa azione ripetuta su una sequenza, con una forma del linguaggio chiara e riusabile.

---

## Sintassi del `for`

```python
for identificatore in iterabile:
    # istruzioni
```

Parti da riconoscere:

- `for` introduce un'iterazione;
- `identificatore` e' la variabile di iterazione;
- `iterabile` e' la sequenza o struttura che stiamo attraversando;
- i due punti `:` aprono il blocco;
- il blocco del ciclo va indentato.

---

## Semantica del `for`

Semantica intuitiva:

1. Python prende un elemento dell'iterabile.
2. Lo assegna alla variabile di iterazione.
3. Esegue il blocco.
4. Passa all'elemento successivo.
5. Quando gli elementi finiscono, continua dopo il `for`.

Esempio:

```python
for parola in ["Ciao", "Mondo", "Python"]:
    print(parola.lower())
```

Il `for` e' utile quando:

- la stessa operazione concettuale va ripetuta molte volte;
- il codice manuale diventerebbe lungo e fragile;
- non vogliamo scrivere una riga separata per ogni posizione della sequenza.

---

<a id="mod8-range"></a>
## Il problema che porta a `range()`

A volte non vogliamo scorrere una lista gia' pronta, ma ripetere qualcosa un numero fissato di volte oppure lavorare su un intervallo di numeri.

Per questo serve un oggetto che rappresenti una sequenza di indici o contatori.

---

## Sintassi di `range()`

`range(n)` serve per ripetere qualcosa un numero fissato di volte.

```python
for numero in range(5):
    print(numero)
```

Forme piu' comuni:

```python
range(n)
range(a, b)
```

---

## Semantica di `range()`

`range(5)` produce:

```python
0, 1, 2, 3, 4
```

Due dettagli importanti:

- `range(5)` conta da `0` a `4`;
- `range(a, b)` parte da `a` e arriva a `b - 1`.

Esempio:

```python
for n in range(25, 35):
    print(n)
```

stampa i numeri da `25` a `34`.

---

## `for` e stato del programma

Conviene anche tracciare:

```python
for x in [24, -13, 8]:
    y = x + 1

print(x, y)
```

Alla fine del ciclo:

- `x` contiene l'ultimo elemento iterato;
- `y` contiene l'ultimo valore calcolato.

Questo aiuta a capire che:

- il `for` aggiorna la variabile di iterazione a ogni passo;
- lo stato continua a cambiare durante il ciclo;
- il valore finale osservabile dipende dall'ultima iterazione.

Un errore tipico e' riusare male i nomi:

```python
number = int(input())

for number in range(number):
    ...
```

Qui la variabile del `for` sovrascrive il valore letto prima. Meglio:

```python
numero = int(input())

for i in range(numero):
    ...
```

---

## Valore corrente e posizione

A volte non basta avere il valore corrente: serve anche sapere in quale posizione della lista stiamo lavorando.

Per esempio:

```python
for posizione, parola in enumerate(parole):
    parole[posizione] = parola.lower()
```

`enumerate()` permette di ottenere insieme:

- posizione;
- valore corrente.

Questo e' spesso piu' pulito che gestire a mano:

```python
posizione = 0
...
posizione += 1
```

---

## Il problema che porta a `enumerate()`

In molti esercizi il solo valore corrente non basta.

Serve anche la posizione:

- per riscrivere un elemento nella lista;
- per stampare indice e contenuto;
- per distinguere posizione e valore senza un contatore separato.

`enumerate()` nasce proprio per evitare quella gestione manuale.

---

## Sintassi di `enumerate()`

Forma tipica:

```python
for posizione, valore in enumerate(sequenza):
    ...
```

Esempio:

```python
for posizione, parola in enumerate(parole):
    parole[posizione] = parola.lower()
```

---

## Semantica di `enumerate()`

`enumerate(sequenza)` permette di iterare ottenendo insieme:

- la posizione corrente;
- il valore corrente.

Quindi, a ogni iterazione:

1. Python prende il prossimo elemento della sequenza;
2. gli associa anche il suo indice;
3. assegna entrambi alle variabili del `for`.

---

## Scansioni, trasformazioni e accumuli

Con `for` ricorrono tre schemi molto frequenti:

### Scansione

```python
for carattere in parola:
    print(carattere)
```

### Trasformazione

```python
parole_minuscole = []

for parola in parole:
    parole_minuscole.append(parola.lower())
```

### Accumulo

```python
somma = 0

for numero in numeri:
    somma += numero
```

Questi tre schemi ricorrono continuamente negli esercizi del modulo.

---

## Cicli annidati

Quando il problema ha due dimensioni, servono spesso due cicli:

- riga e colonna;
- pagina e riga;
- riga e contenuto della riga.

Schema:

```python
for i in range(1, n + 1):
    stringa = ""
    for j in range(1, i + 1):
        stringa += str(i)
    print(stringa)
```

Se dentro usi `i`, il pattern dipende dall'indice esterno.
Se usi `j`, il pattern cambia:

```python
for i in range(1, n + 1):
    stringa = ""
    for j in range(1, i + 1):
        stringa += str(j)
    print(stringa)
```

Questo e' un ottimo esercizio per capire che gli indici dei cicli annidati hanno ruoli diversi.

---

## Pattern di stampa

Gli esercizi su triangoli, piramidi e rettangoli servono a consolidare:

- uso di `range()`;
- distinzione tra ciclo esterno e ciclo interno;
- costruzione progressiva di una stringa;
- controllo di quando andare a capo.

Per esempio:

```python
stringa = "*"

for i in range(1, n + 1):
    print(stringa)
    stringa = stringa + "*"
```

---

## `for` e `while` nello stesso esercizio

Se usi sia `for` sia `while`, chiediti sempre:

- quale dei due controlla la struttura principale del problema;
- quale variabile governa davvero la terminazione;
- se stai riusando male la stessa variabile in due ruoli diversi.

Quando il comportamento e' confuso, conviene tracciare a mano i valori a ogni iterazione.

---

## Caratteri di escape e stampa

Alcuni caratteri speciali utili quando si prepara output:

| Sequenza | Effetto |
| --- | --- |
| `\\n` | nuova riga |
| `\\t` | tabulazione |
| `\"` o `\'` | virgolette dentro una stringa |

Esempi:

```python
print("hello\nworld")
print("a\tb")
print("\"print\"")
```

---

## Esercizi

### Base

1. stampa i numeri da 0 a 9;
2. stampa i numeri da 25 a 34;
3. stampa 10 volte una stessa stringa.

### Stringhe e liste

4. stampa una parola lettera per lettera;
5. stampa una parola lettera per lettera indicando anche la posizione;
6. stampa solo i caratteri in posizione pari;
7. trasforma una lista di parole in minuscolo.

### Cicli annidati

8. stampa un triangolo di numeri;
9. stampa un quadrato di `+` di lato `n`;
10. stampa un rettangolo di base `n` e altezza `m`;
11. costruisci pattern diversi cambiando l'indice usato nel ciclo interno.

---

## Riepilogo

Questo modulo raccoglie il nucleo dell'iterazione con `for`:

- sintassi e semantica;
- uso di `range()`;
- tracciamento della variabile di iterazione;
- scansioni, trasformazioni e accumuli;
- cicli annidati e pattern di stampa.
