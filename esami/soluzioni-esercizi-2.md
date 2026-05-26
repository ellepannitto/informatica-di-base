# Soluzioni — Esercizi di preparazione alla prova intermedia — simulazione 2

---

## Esercizio 1 — `//` vs `/`

| Operatore | Tipo risultato | Comportamento                        |
|-----------|----------------|--------------------------------------|
| `/`       | `float`        | Divisione reale, conserva i decimali |
| `//`      | `int`          | Divisione intera, scarta il resto    |

**Esempio:**

```python
7 / 2    # → 3.5
7 // 2   # → 3
```

---

## Esercizio 2 — Divisibilità di 252

```python
252 % 4 == 0 and 252 % 7 == 0
```

Risultato: `True`  
(252 = 4 × 63 = 7 × 36)

---

## Esercizio 3 — Tabella di traccia per input `4`

```python
n = int(input("Inserisci un numero: "))
prodotto = 1
i = 1
while i <= n:
    prodotto = prodotto * 2
    i = i + 1
print(prodotto)
```

| Passo | Riga del codice sorgente         | Stato                          | Output |
|-------|----------------------------------|--------------------------------|--------|
| 1     | `n = int(input(...))`            | n=4                            |        |
| 2     | `prodotto = 1`                   | n=4, prodotto=1                |        |
| 3     | `i = 1`                          | n=4, prodotto=1, i=1           |        |
| 4     | `while i <= n` (1≤4 → True)      | n=4, prodotto=1, i=1           |        |
| 5     | `prodotto = prodotto * 2`        | n=4, prodotto=2, i=1           |        |
| 6     | `i = i + 1`                      | n=4, prodotto=2, i=2           |        |
| 7     | `while i <= n` (2≤4 → True)      | n=4, prodotto=2, i=2           |        |
| 8     | `prodotto = prodotto * 2`        | n=4, prodotto=4, i=2           |        |
| 9     | `i = i + 1`                      | n=4, prodotto=4, i=3           |        |
| 10    | `while i <= n` (3≤4 → True)      | n=4, prodotto=4, i=3           |        |
| 11    | `prodotto = prodotto * 2`        | n=4, prodotto=8, i=3           |        |
| 12    | `i = i + 1`                      | n=4, prodotto=8, i=4           |        |
| 13    | `while i <= n` (4≤4 → True)      | n=4, prodotto=8, i=4           |        |
| 14    | `prodotto = prodotto * 2`        | n=4, prodotto=16, i=4          |        |
| 15    | `i = i + 1`                      | n=4, prodotto=16, i=5          |        |
| 16    | `while i <= n` (5≤4 → False)     | n=4, prodotto=16, i=5          |        |
| 17    | `print(prodotto)`                | n=4, prodotto=16, i=5          | 16     |

---

## Esercizio 4 — Tabella di traccia per input `3` e `7`

```python
a = int(input())
b = int(input())
if a > b:
    z = a - b
elif a == b:
    z = 0
else:
    z = b - a
print(z)
```

| Passo | Riga del codice sorgente        | Stato            | Output |
|-------|---------------------------------|------------------|--------|
| 1     | `a = int(input())`              | a=3              |        |
| 2     | `b = int(input())`              | a=3, b=7         |        |
| 3     | `if a > b` (3>7 → False)        | a=3, b=7         |        |
| 4     | `elif a == b` (3==7 → False)    | a=3, b=7         |        |
| 5     | `z = b - a`                     | a=3, b=7, z=4    |        |
| 6     | `print(z)`                      | a=3, b=7, z=4    | 4      |

---

## Esercizio 5 — Errore logico

**Codice originale (con errore):**

```python
i = 1
while i <= 10:
    if i % 2 == 0:   # ← SBAGLIATO: stampa i pari, non i dispari
        print(i)
    i = i + 1
```

**Errore:** la condizione `i % 2 == 0` è vera per i numeri pari. Il programma stampa i pari invece dei dispari.

**Correzione:**

```python
i = 1
while i <= 10:
    if i % 2 != 0:
        print(i)
    i = i + 1
```

---

## Esercizio 6 — Errore di tipo

**Codice originale (con errore):**

```python
testo = input("Inserisci una parola: ")
lunghezza = len(testo)
if lunghezza > 5:
    print("La parola " + testo + " è lunga " + lunghezza + " caratteri")
```

**Errore:** `lunghezza` è di tipo `int`, ma l'operatore `+` tra stringhe richiede che tutti gli operandi siano `str`. Causa `TypeError: can only concatenate str (not "int") to str`.

**Correzione:**

```python
testo = input("Inserisci una parola: ")
lunghezza = len(testo)
if lunghezza > 5:
    print("La parola " + testo + " è lunga " + str(lunghezza) + " caratteri")
else:
    print("Parola corta")
```

---

## Esercizio 7 — FizzBuzz

```python
n = int(input("Inserisci un numero: "))
i = 1
while i <= n:
    if i % 3 == 0 and i % 5 == 0:
        print("fizzbuzz")
    elif i % 3 == 0:
        print("fizz")
    elif i % 5 == 0:
        print("buzz")
    else:
        print(i)
    i = i + 1
```

**Nota:** il caso `fizzbuzz` va testato per primo, altrimenti verrebbe intercettato dalle condizioni `fizz` o `buzz`.

---

## Esercizio 8 — Conteggio positivi e negativi

```python
positivi = 0
negativi = 0

n = int(input("Inserisci un numero: "))
while n != 0:
    if n > 0:
        positivi = positivi + 1
    else:
        negativi = negativi + 1
    n = int(input("Inserisci un numero: "))

print("Positivi:", positivi)
print("Negativi:", negativi)
```

---

## Esercizio 9 — Errore sintattico vs errore semantico

| Tipo              | Definizione                                                       | Quando viene rilevato         |
|-------------------|-------------------------------------------------------------------|-------------------------------|
| **Sintattico**    | Viola le regole grammaticali del linguaggio                       | Prima dell'esecuzione         |
| **Semantico**     | Il codice è grammaticalmente corretto ma produce risultati errati | Durante o dopo l'esecuzione   |

**Esempio sintattico:**

```python
if x = 5:   # SyntaxError: usa = invece di ==
    print(x)
```

**Esempio semantico:**

```python
i = 1
while i <= 10:
    if i % 2 == 0:   # logicamente sbagliato: stampa pari invece di dispari
        print(i)
    i = i + 1
```

---

## Esercizio 10 — Stato del programma

Lo **stato del programma** è l'insieme dei valori correnti di tutte le variabili in un dato momento dell'esecuzione. Cambia a ogni istruzione di assegnamento.

**Esempio:**

```python
x = 5        # stato: {x: 5}
y = x + 3   # stato: {x: 5, y: 8}
x = x * 2   # stato: {x: 10, y: 8}
```

Ogni riga modifica lo stato: la prima crea `x`, la seconda crea `y` usando il valore corrente di `x`, la terza aggiorna `x` senza toccare `y`.

---

## Esercizio 11 — Valutazione lazy con `and`

Il programma **non produce un errore** e stampa:

```
condizione falsa
```

**Perché:** Python valuta le condizioni di un `and` da sinistra a destra e si ferma appena trova un valore `False` (cortocircuito). Poiché `x < 0` è `False` (dato che `x = 5`), Python non arriva mai a valutare `y > 0`, quindi non rileva che `y` non è definita. Il ramo `else` viene eseguito.

Se invece `x` fosse negativo (ad esempio `x = -3`), Python valuterebbe `y > 0` e solleverebbe un `NameError`.

---

## Esercizio 12 — Valutazione lazy con `or`

**a. Input `""`:**

```
vuota o inizia con A
```

`len("") == 0` è `True` → Python non valuta `parola[0]` (cortocircuito su `or`). Bene, perché `""[0]` solleverebbe un `IndexError`.

**b. Input `"Alfa"`:**

```
vuota o inizia con A
```

`len("Alfa") == 0` è `False` → Python valuta `"Alfa"[0] == "A"` → `True` → stampa il primo messaggio.

**c. Senza cortocircuito:**

Con input `""`, Python valuterebbe sempre entrambe le condizioni: `""[0]` causerebbe un `IndexError: string index out of range`, mandando in crash il programma anche se la prima condizione è già `True`.
