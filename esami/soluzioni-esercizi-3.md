# Soluzioni — Esercizi di preparazione alla seconda prova intermedia

---

## Teoria 1 — Funzione pura vs funzione void

| | Funzione pura | Funzione void |
|---|---|---|
| **Chiamata** | È un'espressione, produce un valore | È un'istruzione, non produce un valore |
| **`return`** | Obbligatorio, restituisce il risultato | Assente (o `return` senza valore) |
| **Effetti collaterali** | Non ne ha: il risultato dipende solo dagli argomenti | È il posto naturale per gli effetti collaterali |
| **Come si riconosce** | La chiamata si usa in un'espressione: `y = f(x)` | La chiamata è da sola su una riga: `f(x)` |

---

## Teoria 2 — `==` vs `is`

- `==` confronta il **contenuto**: due liste sono uguali se hanno gli stessi elementi nello stesso ordine.
- `is` confronta l'**identità**: è `True` solo se i due nomi puntano allo stesso oggetto in memoria.

```python
a = [1, 2, 3]
b = [1, 2, 3]   # oggetto diverso, stesso contenuto

print(a == b)   # True  ← stesso contenuto
print(a is b)   # False ← oggetti diversi

c = a
print(a is c)   # True  ← stesso oggetto (alias)
```

---

## Teoria 3 — Alias

Un **alias** è quando due nomi puntano allo stesso oggetto. Si crea con un semplice assegnamento:

```python
a = [1, 2, 3]
b = a           # b è un alias di a
```

Qualsiasi modifica fatta tramite `b` è visibile anche da `a`, perché non ci sono due liste — ce n'è una sola:

```python
b.append(4)
print(a)   # [1, 2, 3, 4]  ← cambiata anche a!
```

---

## Teoria 4 — Valutazione della guardia

La guardia viene valutata:

1. **Prima** di entrare nel corpo del ciclo: se è subito `False`, il corpo non viene mai eseguito.
2. **Dopo ogni esecuzione** del corpo: se è ancora `True` si ripete, altrimenti il ciclo termina.

La guardia non viene valutata durante l'esecuzione del corpo — solo all'inizio di ogni iterazione.

---

## Teoria 5 — Stato del contatore alla fine del ciclo

Quando il ciclo `while i < n` termina, `i` vale esattamente `n` (o il primo valore per cui la guardia è diventata `False`). Il contatore viene incrementato *prima* che la guardia venga rivalutata, quindi al termine ha già superato l'ultimo indice valido.

```python
i = 0
while i < 3:
    i = i + 1
print(i)   # 3  ← i vale 3, non 2
```

---

## Tracciamento 1 — Somma degli elementi di `[3, 7, 2]`

```python
numeri = [3, 7, 2]
i = 0
totale = 0
while i < len(numeri):
    totale = totale + numeri[i]
    i = i + 1
print(totale)
```

| Passo | Codice sorgente                    | Stato del programma               | Output |
| ----- | ---------------------------------- | --------------------------------- | ------ |
| 1     | `numeri = [3, 7, 2]`               | `numeri->[3,7,2]`                 |        |
| 2     | `i = 0`                            | `numeri->[3,7,2], i->0`           |        |
| 3     | `totale = 0`                       | `numeri->[3,7,2], i->0, tot->0`   |        |
| 4     | `while i < len(numeri)` (0<3 → T)  | invariato                         |        |
| 5     | `totale = totale + numeri[0]`      | `tot->3, i->0`                    |        |
| 6     | `i = i + 1`                        | `tot->3, i->1`                    |        |
| 7     | `while i < len(numeri)` (1<3 → T)  | invariato                         |        |
| 8     | `totale = totale + numeri[1]`      | `tot->10, i->1`                   |        |
| 9     | `i = i + 1`                        | `tot->10, i->2`                   |        |
| 10    | `while i < len(numeri)` (2<3 → T)  | invariato                         |        |
| 11    | `totale = totale + numeri[2]`      | `tot->12, i->2`                   |        |
| 12    | `i = i + 1`                        | `tot->12, i->3`                   |        |
| 13    | `while i < len(numeri)` (3<3 → F)  | invariato                         |        |
| 14    | `print(totale)`                    | invariato                         | `12`   |

---

## Tracciamento 2 — Funzione `quadrato(4)`

```python
def quadrato(n):
    n = n * n
    return n

x = 4
y = quadrato(x)
print(x)
print(y)
```

| Passo | Codice sorgente      | Stato del programma | Output |
| ----- | -------------------- | ------------------- | ------ |
| 1     | `x = 4`              | `x->4`              |        |
| 2     | chiama `quadrato(x)` | `x->4, n->4`        |        |
| 3     | `n = n * n`          | `x->4, n->16`       |        |
| 4     | `return n`           | `x->4` (n scompare) |        |
| 5     | `y = quadrato(x)`    | `x->4, y->16`       |        |
| 6     | `print(x)`           | invariato           | `4`    |
| 7     | `print(y)`           | invariato           | `16`   |

`x` non è cambiata perché `int` è immutabile: `n = n * n` dentro la funzione crea un nuovo oggetto e sposta il riferimento locale `n`, senza toccare `x`.

---

## Trovare l'errore 1 — `raddoppia` che non raddoppia

**Errore:** la funzione restituisce la lista originale senza modificarla. `return lista` non raddoppia nessun elemento.

**Correzione:**

```python
def raddoppia(lista):
    nuova = []
    i = 0
    while i < len(lista):
        nuova.append(lista[i] * 2)
        i = i + 1
    return nuova

numeri = [1, 2, 3]
numeri = raddoppia(numeri)
print(numeri)   # [2, 4, 6]
```

---

## Trovare l'errore 2 — `.sort()` restituisce `None`

**Cosa stampa:**

```
originale: [1, 2, 5, 8]
ordinata: None
```

**Perché:** `.sort()` è una funzione void — ordina la lista originale in-place e restituisce `None`. Quindi `ordinata` vale `None` e `originale` è già ordinata (effetto collaterale inatteso).

**Correzione** (senza modificare l'originale):

```python
originale = [5, 2, 8, 1]
ordinata = []
i = 0
while i < len(originale):
    ordinata.append(originale[i])
    i = i + 1
ordinata.sort()
print("originale:", originale)   # [5, 2, 8, 1]
print("ordinata:", ordinata)     # [1, 2, 5, 8]
```

---

## Programmazione 1 — Sentinella con lista di positivi

```python
numeri = []
n = int(input())
while n != 0:
    if n > 0:
        numeri.append(n)
    n = int(input())
print(numeri)
```

---

## Programmazione 2 — `minimo`

```python
def minimo(lista):
    m = lista[0]
    i = 1
    while i < len(lista):
        if lista[i] < m:
            m = lista[i]
        i = i + 1
    return m

numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())
print(minimo(numeri))
```

---

## Programmazione 3 — `conta_pari`

```python
def conta_pari(lista):
    conta = 0
    i = 0
    while i < len(lista):
        if lista[i] % 2 == 0:
            conta = conta + 1
        i = i + 1
    return conta
```

---

## Programmazione 4 — `sostituisci_negativi`

```python
def sostituisci_negativi(lista, valore):
    i = 0
    while i < len(lista):
        if lista[i] < 0:
            lista[i] = valore
        i = i + 1
```

`lista[i] = valore` modifica la lista originale direttamente — non serve `return`.

---

## Programmazione 5 — `moltiplica` senza `*`

```python
def moltiplica(a, b):
    risultato = 0
    i = 0
    while i < b:
        risultato = risultato + a
        i = i + 1
    return risultato
```

Somma `a` per `b` volte. Se `b == 0` il ciclo non esegue mai e restituisce `0`.

---

## Programmazione 6 — `contiene_pari`

```python
def contiene_pari(lista):
    i = 0
    while i < len(lista):
        if lista[i] % 2 == 0:
            return True
        i = i + 1
    return False

numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())

if contiene_pari(numeri):
    print("La lista contiene almeno un numero pari.")
else:
    print("La lista non contiene numeri pari.")
```

Il `return True` interrompe subito la funzione non appena trova il primo pari — non è necessario scorrere tutta la lista.

---

## Programmazione 7 — `tutti_positivi`

```python
def tutti_positivi(lista):
    i = 0
    while i < len(lista):
        if lista[i] <= 0:
            return False
        i = i + 1
    return True
```

Basta trovare un elemento non positivo per restituire `False`. Se la lista è vuota il ciclo non esegue mai e restituisce `True` (vacuamente vero: nessun elemento viola la condizione).

---

## Programmazione 8 — `e_ordinata`

```python
def e_ordinata(lista):
    i = 1
    while i < len(lista):
        if lista[i] < lista[i - 1]:
            return False
        i = i + 1
    return True

numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())

if e_ordinata(numeri):
    print("La lista è ordinata.")
else:
    print("La lista non è ordinata.")
```

L'indice parte da `1` perché ogni elemento viene confrontato con il precedente (`lista[i - 1]`). Con una lista di un solo elemento il ciclo non esegue mai e restituisce `True`.
