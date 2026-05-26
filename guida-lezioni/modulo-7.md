# Modulo 07 · Ciclo for e matrici

## Autovalutazione

- Sai usare il ciclo `for` su stringhe, liste e `range()`?
- Sai spiegare la differenza tra `for` e `while`?
- Sai usare cicli annidati per lavorare su matrici?

## Preparazione al compitino: Teoria

**Lista**

Una lista è una sequenza ordinata (perchè ordinata) di valori (che tipo di valori?), modificabile dopo la creazione.

```python
numeri = [1, 2, 3]
numeri[0] = 10       # modifica in-place
numeri.append(4)     # aggiunge in fondo
```

- gli elementi si accedono tramite indice (da `0`);
- `len(lista)` restituisce il numero di elementi;
- le liste sono **mutabili**: il loro contenuto può cambiare.

**`while`: sintassi e semantica**

```python
while condizione:
    # blocco
```

- la condizione viene valutata prima di ogni iterazione;
- se è vera, il blocco viene eseguito;
- se è falsa, il ciclo termina;
- se la condizione non diventa mai falsa, il ciclo non termina mai.


**Definizione vs chiamata di funzione**

La **definizione** (`def`) descrive cosa fa la funzione — non esegue nulla, crea solo un "template".
La **chiamata** (o invocazione) esegue effettivamente il corpo della funzione con gli argomenti forniti.

```python
def somma(a, b):   # definizione: niente viene eseguito qui
    return a + b

risultato = somma(3, 4)   # chiamata: il corpo viene eseguito ora
```

Una funzione può essere definita una volta e chiamata molte volte, con argomenti diversi.

**Tipi mutabili e immutabili**

| Tipo | Mutabile? | Conseguenza |
|------|-----------|-------------|
| `list` | Sì | il contenuto può cambiare dopo la creazione (`lista[0] = 99`, `lista.append(x)`) |
| `int`, `float`, `str`, `bool` | No | non si può modificare il valore — si può solo crearne uno nuovo |

La distinzione è importante nelle funzioni: riassegnare un intero dentro una funzione non cambia mai la variabile esterna; modificare una lista in-place sì (perché il parametro è un alias della lista originale).

**Funzione pura vs. funzione void**

|                            | Funzione pura                                          | Funzione void                                        |
| -------------------------- | ------------------------------------------------------ | ---------------------------------------------------- |
| Restituisce un valore?     | sì (`return`)                                          | no                                                   |
| Modifica il suo parametro? | no                                                     | spesso sì                                            |
| Come si usa il risultato?  | `risultato = f(x)` -- la chiamata è un'**espressione** | si chiama e basta -- la chiamata è un'**istruzione** |

**Scope**

Le variabili definite dentro una funzione sono **locali**: non esistono fuori.

```python
def doppio(n):
    n = n * 2      # n locale — non tocca la variabile esterna
    return n

x = 3
y = doppio(x)
print(x)  # 3  — x non è cambiato
print(y)  # 6
```

Regola pratica: riassegnare un parametro dentro la funzione non cambia mai la variabile esterna, a prescindere dal tipo.

**Aliasing**

Quando si assegna una lista a un secondo nome, i due nomi puntano alla **stessa lista** in memoria.

```python
a = [1, 2, 3]
b = a          # b non è una copia: b è un alias di a

b[0] = 99
print(a)       # [99, 2, 3] — anche a è cambiata
```

Questo spiega perchè una funzione void puè modificare una lista passata come argomento: dentro la funzione il parametro è un alias della lista originale.

## Preparazione al compitino: Cosa stampa questo codice?

```python
def doppio(n):
    n = n * 2
    return n

x = 3
y = doppio(x)
print(x, y)
```

<details>
**Come ragionare:**

La funzione riceve `x` che vale `3`. All'interno, `n = n * 2` crea una variabile locale `n` con valore `6` — non modifica `x`, che è un intero (immutabile). La funzione restituisce `6`, assegnato a `y`.

**Risposta:** `3 6`
</details>

## Preparazione al compitino: Trova l'errore

### Trova l'errore (1)

Il programma vuole stampare se in `lista` c'è almeno un elemento ripetuto oppure no.

```python
lista = [1, 2, 3, 1, 4]

trovato = False
i = 0
while i < len(lista):
    j = i + 1
    while j < len(lista):
        if lista[j] == lista[i]:
            trovato = True
    i = i + 1

if trovato:
    print("c'è almeno un elemento ripetuto")
else:
    print("nessun elemento ripetuto")
```

> **Come ragionare?** Prima di tutto, cerca di capire se il programma termina e come va avanti la sua esecuzione. Per farlo, dobbiamo controllare il valore delle variabili nello stato ad ogni passo dell'esecuzione.
> Proviamo su un input più piccolo per prendere confidenza: `lista = [1, 2, 1]`.

<details>

```python
1 trovato = False
2 i = 0

3 while i < len(lista):
4     j = i + 1

5     while j < len(lista):

6         if lista[j] == lista[i]:
7             trovato = True

8     i = i + 1
```

| Riga | `i` | `j` | `trovato` | i < len(lista) | j < len(lista) | lista[j] == lista[i]                |
| ---- | --- | --- | --------- | -------------- | -------------- | ----------------------------------- |
| 1    | -   | -   | False     |                |                |                                     |
| 2    | 0   | -   | False     |                |                |                                     |
| 3    | 0   | -   | False     | 0<3? True      |                |                                     |
| 4    | 0   | 1   | False     | -              | -              | -                                   |
| 5    | 0   | 1   | False     | -              | 1<3? True      | -                                   |
| 6    | 0   | 1   | False     | -              | -              | lista[0]==lista[1] -> 1 == 2? False |
| 5    | 0   | 1   | False     | -              | 1<3? True      | -                                   |
| 6    | 0   | 1   | False     | -              | -              | lista[0]==lista[1] -> 1 == 2? False |
| 5    | 0   | 1   | False     | -              | 1<3? True      | -                                   |
| 6    | 0   | 1   | False     | -              | -              | lista[0]==lista[1] -> 1 == 2? False |
| 5    | 0   | 1   | False     | -              | 1<3? True      | -                                   |
| 6    | 0   | 1   | False     | -              | -              | lista[0]==lista[1] -> 1 == 2? False |
| ...  | ... | ... | ...       | ...            | ...            | ...                                 |


**Trovato il problema?**: `j` non cambia mai: il ciclo interno non termina mai.

**Errore:** dentro il ciclo interno manca l'aggiornamento di `j`. La guardia `j < len(lista)` non diventa mai falsa, quindi il `while` interno gira all'infinito.

</details>

<details>

**Codice corretto:**

```python
lista = [1, 2, 3, 1, 4]

trovato = False
i = 0
while i < len(lista):
    j = i + 1
    while j < len(lista):
        if lista[j] == lista[i]:
            trovato = True
        j = j + 1
    i = i + 1

if trovato:
    print("c'è almeno un elemento ripetuto")
else:
    print("nessun elemento ripetuto")
```
</details>

### Trova l'errore (2)

Il programma vuole stampare se in `lista` c'è almeno un elemento ripetuto oppure no.

```python
lista = [1, 2, 3, 1, 4]

i = 0
while i < len(lista):
    trovato = False
    j = i + 1
    while j < len(lista):
        if lista[j] == lista[i]:
            trovato = True
        j = j + 1
    i = i + 1

if trovato:
    print("c'è almeno un elemento ripetuto")
else:
    print("nessun elemento ripetuto")
```

> **Come ragionare?** Sappiamo che il programma termina perché abbiamo controllato prima. Adesso dobbiamo capire se fa effettivamente quello che vogliamo.
>
> Per trovare un errore logico servono input "furbi": casi in cui la risposta giusta è **sì** e casi in cui è **no**, e confrontiamo quello che ci aspettiamo con quello che otteniamo.
>
> Proviamo `lista = [1, 1]` (risposta attesa: *c'è almeno un elemento ripetuto*) e `lista = [1, 2]` (risposta attesa: *nessun elemento ripetuto*).

<details>

```python
1  i = 0

2  while i < len(lista):
3      trovato = False
4      j = i + 1

5      while j < len(lista):

6          if lista[j] == lista[i]:
7              trovato = True
8          j = j + 1

9      i = i + 1
```

**Con `lista = [1, 1]`** (risposta attesa: *c'è almeno un elemento ripetuto*):

| Riga | `i` | `j` | `trovato`          | `i < len(lista)` | `j < len(lista)` | `lista[j] == lista[i]`       |
| ---- | --- | --- | ------------------ | ---------------- | ---------------- | ---------------------------- |
| 1    | 0   | —   | —                  |                  |                  |                              |
| 2    | 0   | —   | —                  | 0<2? Vero        |                  |                              |
| 3    | 0   | —   | False              |                  |                  |                              |
| 4    | 0   | 1   | False              |                  |                  |                              |
| 5    | 0   | 1   | False              |                  | 1<2? Vero        |                              |
| 6    | 0   | 1   | False              |                  |                  | lista[1]=1 == lista[0]=1? Sì |
| 7    | 0   | 1   | True               |                  |                  |                              |
| 8    | 0   | 2   | True               |                  |                  |                              |
| 5    | 0   | 2   | True               |                  | 2<2? Falso       |                              |
| 9    | 1   | 2   | True               |                  |                  |                              |
| 2    | 1   | 2   | True               | 1<2? Vero        |                  |                              |
| 3    | 1   | 2   | **False** ← reset! |                  |                  |                              |
| 4    | 1   | 2   | False              |                  |                  |                              |
| 5    | 1   | 2   | False              |                  | 2<2? Falso       |                              |
| 9    | 2   | 2   | False              |                  |                  |                              |
| 2    | 2   | 2   | False              | 2<2? Falso       |                  |                              |

Fine ciclo: `trovato = False` → stampa "nessun elemento ripetuto" ❌

L'input `[1, 2]` non rivelerebbe nulla perché la risposta corretta era già "no". È `[1, 1]` che smonta il programma.

**Errore:** `trovato = False` è dentro il ciclo esterno, quindi viene reimpostato a `False` ad ogni iterazione. Alla riga 3 della seconda iterazione, il valore `True` conquistato viene cancellato.

</details>

<details>

**Codice corretto:**

```python
lista = [1, 2, 3, 1, 4]

trovato = False
i = 0
while i < len(lista):
    j = i + 1
    while j < len(lista):
        if lista[j] == lista[i]:
            trovato = True
        j = j + 1
    i = i + 1

if trovato:
    print("c'è almeno un elemento ripetuto")
else:
    print("nessun elemento ripetuto")
```
</details>

### Trova l'errore (3)

Il programma vuole costruire la lista che, per ogni elemento di `lista`, conta quanti elementi **uguali a lui** lo **precedono**.

```python
lista = [1, 2, 1, 3, 1]

contatori = []
i = 0
while i < len(lista):
    contatore = 0
    j = 0
    while j < len(lista):
        if lista[j] == lista[i]:
            contatore = contatore + 1
        j = j + 1
    contatori.append(contatore)
    i = i + 1

print(contatori)
```

> **Come ragionare?** Il programma ha sia `i = i + 1` che `j = j + 1`: termina. Dobbiamo quindi controllare se l'output è corretto.
>
> Input furbo: `lista = [1, 1]`. Risposta attesa: `[0, 1]` (il primo `1` non ha precedenti uguali; il secondo ne ha uno).

<details>

```python
1  contatori = []
2  i = 0

3  while i < len(lista):
4      contatore = 0
5      j = 0

6      while j < len(lista):
7          if lista[j] == lista[i]:
8              contatore = contatore + 1
9          j = j + 1

10     contatori.append(contatore)
11     i = i + 1
```

**Con `lista = [1, 1]`** — tracciamo la prima iterazione esterna (`i=0`):

| Riga | `i` | `j` | `contatore` | `j < len(lista)` | `lista[j] == lista[i]`      |
|------|-----|-----|-------------|------------------|-----------------------------|
| 3    | 0   | —   | —           | 0<2? Vero        |                             |
| 4    | 0   | —   | 0           |                  |                             |
| 5    | 0   | 0   | 0           |                  |                             |
| 6    | 0   | 0   | 0           | 0<2? Vero        |                             |
| 7    | 0   | 0   | 0           |                  | lista[0]=1 == lista[0]=1? Sì |
| 8    | 0   | 0   | 1           |                  |                             |
| 9    | 0   | 1   | 1           |                  |                             |
| 6    | 0   | 1   | 1           | 1<2? Vero        |                             |
| 7    | 0   | 1   | 1           |                  | lista[1]=1 == lista[0]=1? Sì |
| 8    | 0   | 1   | 2           |                  |                             |
| 9    | 0   | 2   | 2           |                  |                             |
| 6    | 0   | 2   | 2           | 2<2? Falso       |                             |
| 10   | 0   | 2   | 2           |                  | → `contatori = [2]`          |

Il primo elemento ottiene `contatore = 2`, ma la risposta attesa era `0`. Il ciclo interno ha contato **tutti** gli `1` della lista, non solo quelli che vengono prima di `i=0`.

**Errore:** la guardia del ciclo interno è `j < len(lista)` invece di `j < i`. Così `j` scorre tutta la lista, contando anche gli elementi che vengono *dopo* la posizione `i`, e contando perfino `lista[i]` stesso.

</details>

<details>

**Codice corretto:**

```python
lista = [1, 2, 1, 3, 1]

contatori = []
i = 0
while i < len(lista):
    contatore = 0
    j = 0
    while j < i:
        if lista[j] == lista[i]:
            contatore = contatore + 1
        j = j + 1
    contatori.append(contatore)
    i = i + 1

print(contatori)
```
</details>


## Preparazione al compitino: Tracciamento dello stato

```python
def raddoppia(lista):
    i = 0
    while i < len(lista):
        lista[i] = lista[i] * 2
        i = i + 1

valori = [1, 3, 5]
raddoppia(valori)
print(valori)
```

| Passo | Codice sorgente      | Stato - globale   | Stato - funzione    | Output       |
| ----- | -------------------- | ----------------- | ------------------- | ------------ |
| 1     | `valori = [1, 3, 5]` | `valori=[1,3,5]`  | —                   |              |
| 2     | `raddoppia(valori)`  | `valori=[1,3,5]`  | `lista→valori, i=0` |              |
| 3     | `lista[0] = 1*2`     | `valori=[2,3,5]`  | `lista→valori, i=0` |              |
| 4     | `i = i + 1`          | `valori=[2,3,5]`  | `lista→valori, i=1` |              |
| 5     | `lista[1] = 3*2`     | `valori=[2,6,5]`  | `lista→valori, i=1` |              |
| 6     | `i = i + 1`          | `valori=[2,6,5]`  | `lista→valori, i=2` |              |
| 7     | `lista[2] = 5*2`     | `valori=[2,6,10]` | `lista→valori, i=2` |              |
| 8     | `i = i + 1`          | `valori=[2,6,10]` | `lista→valori, i=3` |              |
| 9     | fine `raddoppia`     | `valori=[2,6,10]` | —                   |              |
| 10    | `print(valori)`      | `valori=[2,6,10]` | —                   | `[2, 6, 10]` |

**Cosa osservare:** `lista` e `valori` puntano alla stessa lista in memoria. Le modifiche fatte dentro la funzione (in-place) sono visibili fuori.

## Preparazione al compitino: Programmazione

### Scrivi una funzione pura che riceve una lista di interi e restituisce una nuova lista con solo i numeri pari, senza modificare l'originale.

**Step 1 — firma della funzione**

La funzione riceve una lista e restituisce qualcosa, quindi è una funzione pura con `return`.

```python
def filtra_pari(lista):
    ...
    return ...
```

**Step 2 — dove metto i risultati?**

Non posso modificare `lista` (funzione pura!). Ho bisogno di una lista nuova, che all'inizio è vuota.

```python
def filtra_pari(lista):
    risultato = []
    ...
    return risultato
```

**Step 3 — quale tipo di ciclo scelgo?**

Ci sono due paradigmi principali per il `while` su una lista:

| Paradigma                         | Guardia                          | Quando usarlo                                                             |
| --------------------------------- | -------------------------------- | ------------------------------------------------------------------------- |
| **Scansione completa**            | `i < len(lista)`                 | devo esaminare *tutti* gli elementi (trasformare, filtrare, sommare...)   |
| **Ricerca con uscita anticipata** | `i < len(lista) and not trovato` | mi interessa solo scorrere la lista finchè *trovo il primo elemento* che soddisfa una condizione |

Qui voglio raccogliere **tutti** i pari, non solo il primo: devo scorrere tutta la lista. Scelgo la **scansione completa**.

```python
def filtra_pari(lista):
    risultato = []
    i = 0
    while i < len(lista):
        ...
        i = i + 1
    return risultato
```

**Step 4 — cosa faccio per ogni elemento?**

Voglio tenere solo i pari. Un numero è pari se `lista[i] % 2 == 0`. Se la condizione è vera, aggiungo l'elemento a `risultato`.

```python
def filtra_pari(lista):
    risultato = []
    i = 0
    while i < len(lista):
        if lista[i] % 2 == 0:
            risultato.append(lista[i])
        i = i + 1
    return risultato
```

**Verifica:** `filtra_pari([1, 2, 3, 4, 5])` → `risultato` cresce così:

| `i` | `lista[i]` | `lista[i] % 2 == 0`? | `risultato` dopo `append` |
|-----|------------|----------------------|---------------------------|
| 0   | 1          | No                   | `[]`                      |
| 1   | 2          | Sì                   | `[2]`                     |
| 2   | 3          | No                   | `[2]`                     |
| 3   | 4          | Sì                   | `[2, 4]`                  |
| 4   | 5          | No                   | `[2, 4]`                  |

Restituisce `[2, 4]`. La lista originale `[1, 2, 3, 4, 5]` non è stata modificata.


### Scrivi una funzione pura che riceve una lista di interi e restituisce la posizione del primo numero positivo. Se non ce n'è nessuno, restituisce `-1`.

**Step 1 — firma della funzione**

La funzione riceve una lista e restituisce un intero (un indice), quindi è una funzione pura con `return`.

```python
def primo_positivo(lista):
    ...
    return ...
```

**Step 2 — ho bisogno di una lista risultato?**

No: qui non accumulo elementi, cerco un indice.
Ho bisogno solo di tenere traccia di dove sono arrivato (`i`) e di sapere se ho trovato qualcosa (`trovato`).

```python
def primo_positivo(lista):
    trovato = False
    i = 0
    ...
    return posizione
```

**Step 3 — quale tipo di ciclo scelgo?**

| Paradigma | Guardia | Quando usarlo |
|-----------|---------|---------------|
| **Scansione completa** | `i < len(lista)` | devo esaminare *tutti* gli elementi |
| **Ricerca con uscita anticipata** | `i < len(lista) and not trovato` | mi interessa solo *trovare il primo* elemento che soddisfa una condizione |

Qui voglio solo il **primo** positivo: appena lo trovo posso fermarmi. Scelgo la **ricerca con uscita anticipata**.

```python
def primo_positivo(lista):
    trovato = False
    i = 0
    while i < len(lista) and not trovato:
        ...
        i = i + 1
    return posizione
```

**Step 4 — cosa faccio per ogni elemento?**

Se `lista[i] > 0`, ho trovato quello che cercavo: setto `trovato = True`. In questo caso **non** incremento `i`, così al termine del ciclo `i` punta esattamente all'elemento trovato.

```python
def primo_positivo(lista):
    trovato = False
    i = 0
    while i < len(lista) and not trovato:
        if lista[i] > 0:
            trovato = True
        else:
            i = i + 1
    return posizione
```

**Step 5 — cosa restituisco?**

Se `trovato` è `True`, restituisco `i`. Se invece il ciclo è finito senza trovare nulla (ho esaurito la lista), restituisco `-1`.

```python
def primo_positivo(lista):
    posizione = -1
    trovato = False
    i = 0
    while i < len(lista) and not trovato:
        if lista[i] > 0:
            trovato = True
        else:
            i = i + 1
    posizione = i
    return posizione
```

**Verifica:** `primo_positivo([-3, 0, -1, 5, 2])`:

| `i` | `lista[i]` | guardia `not trovato` | `lista[i] > 0`? | `trovato` |
|-----|------------|-----------------------|-----------------|-----------|
| 0   | -3         | Vero                  | No              | False     |
| 1   | 0          | Vero                  | No              | False     |
| 2   | -1         | Vero                  | No              | False     |
| 3   | 5          | Vero                  | Sì              | True      |
| —   | —          | Falso → esce          |                 |           |

`trovato = True`, `i = 3` → restituisce `3`.

### Scrivi una funzione pura che riceve una lista di interi e un intero `k`, e restituisce una nuova lista in cui dopo ogni numero pari viene inserito `k`, senza modificare la lista originale.

Esempio: `inserisci_dopo_pari([3, 4, 9, 2, 8, 7], 0)` → `[3, 4, 0, 9, 2, 0, 8, 0, 7]`

**Step 1 — firma della funzione**

La funzione riceve una lista e un intero `k`, e restituisce una lista nuova: funzione pura con `return`.

```python
def inserisci_dopo_pari(lista, k):
    ...
    return risultato
```

**Step 2 — dove metto i risultati?**

Non posso modificare `lista`. Ho bisogno di una lista nuova, inizialmente vuota, in cui copio ogni elemento (e inserisco `k` dove serve).

```python
def inserisci_dopo_pari(lista, k):
    risultato = []
    ...
    return risultato
```

**Step 3 — quale tipo di ciclo scelgo?**

Devo esaminare **tutti** gli elementi (per ognuno decido se inserire `k` dopo): scelgo la **scansione completa**.

```python
def inserisci_dopo_pari(lista, k):
    risultato = []
    i = 0
    while i < len(lista):
        ...
        i = i + 1
    return risultato
```

**Step 4 — cosa faccio per ogni elemento?**

Per ogni elemento ho due cose da fare:
1. aggiungerlo sempre a `risultato`;
2. se è pari (`lista[i] % 2 == 0`), aggiungere anche `k` subito dopo.

```python
def inserisci_dopo_pari(lista, k):
    risultato = []
    i = 0
    while i < len(lista):
        risultato.append(lista[i])
        if lista[i] % 2 == 0:
            risultato.append(k)
        i = i + 1
    return risultato
```

**Verifica:** `inserisci_dopo_pari([3, 4, 9, 2, 8, 7], 0)`:

| `i` | `lista[i]` | `lista[i] % 2 == 0`? | `risultato` dopo il passo     |
|-----|------------|----------------------|-------------------------------|
| 0   | 3          | No                   | `[3]`                         |
| 1   | 4          | Sì → append `0`      | `[3, 4, 0]`                   |
| 2   | 9          | No                   | `[3, 4, 0, 9]`                |
| 3   | 2          | Sì → append `0`      | `[3, 4, 0, 9, 2, 0]`          |
| 4   | 8          | Sì → append `0`      | `[3, 4, 0, 9, 2, 0, 8, 0]`   |
| 5   | 7          | No                   | `[3, 4, 0, 9, 2, 0, 8, 0, 7]`|

Restituisce `[3, 4, 0, 9, 2, 0, 8, 0, 7]`. La lista originale non è stata modificata.


## Il costrutto `for`

### Da `while` a `for`

Abbiamo scritto molti cicli di questo tipo:

```python
i = 0
while i < len(lista):
    # fai qualcosa con lista[i]
    i = i + 1
```

Questo schema ha tre parti meccaniche che dobbiamo ricordare ogni volta:
- inizializzare `i`,
- scrivere la guardia giusta,
- aggiornare `i`.

Se dimentichiamo una di queste parti, il programma non funziona (o non termina).
Concettualmente, in realtà, quello che vogliamo fare è **esaminare ogni elemento della lista** in ordine.

Il `for` ci permette di scrivere la stessa cosa in modo più compatto, delegando a Python la gestione dell'indice:

```python
for elemento in lista:
    # fai qualcosa con elemento
```

Le due versioni sono equivalenti:

```python
# con while                      # con for
i = 0                            for elemento in lista:
while i < len(lista):                print(elemento)
    print(lista[i])
    i = i + 1
```

## Sintassi del `for`

```python
for variabile in [espressione_iterabile]:
    # istruzioni
```

Parti da riconoscere:

- `for` introduce un'iterazione;
- `variabile` è il nome che prende l'elemento corrente ad ogni passo;
- `espressione_iterabile` è **qualunque valore che permette l'iterazione** — cioè che può fornire i suoi elementi uno alla volta. Le liste sono iterabili, ma lo sono anche le stringhe, i file, e altri oggetti che vedremo;
- i due punti `:` aprono il blocco;
- il blocco va indentato.

## Semantica del `for`

1. Python prende un elemento dell'iterabile.
2. Lo assegna alla variabile di iterazione.
3. Esegue il blocco.
4. Passa all'elemento successivo.
5. Quando gli elementi finiscono, continua dopo il `for`.


### `for` e stato del programma

```python
for parola in ["Ciao", "Mondo", "Python"]:
    print(parola)
```

| Passo | Codice sorgente       | Stato             | Output   |
| ----- | --------------------- | ----------------- | -------- |
| 1     | `for parola in [...]` | `parola→"Ciao"`   |          |
| 2     | `print(parola)`       | `parola→"Ciao"`   | `Ciao`   |
| 3     | `for parola in [...]` | `parola→"Mondo"`  |          |
| 4     | `print(parola)`       | `parola→"Mondo"`  | `Mondo`  |
| 5     | `for parola in [...]` | `parola→"Python"` |          |
| 6     | `print(parola)`       | `parola→"Python"` | `Python` |


> Con il `while` si itera sull'**indice** e si recupera il valore come `lista[i]`.
> Con il `for` si itera direttamente sul **valore**: `parola` è già l'elemento, non la sua posizione.

```
while:   i → lista[i] → valore
for:              parola → valore
```

## La funzione `range()`

`range` è un tipo iterabile e immutabile che produce una sequenza di interi.
Non è una lista — non occupa spazio in memoria per tutti i valori — ma si comporta come un iterabile: si può usare direttamente in un `for`.

```python
range(n)       # da 0 a n-1
range(a, b)    # da a a b-1
range(a, b, s) # da a a b-1, con passo s
```

**Ripetere un'azione n volte**

Quando non ci interessa il numero in sé ma vogliamo solo ripetere qualcosa, usiamo `range` come contatore:

```python
for i in range(5):
    print("ciao")
```

Output: `ciao` stampato 5 volte.

```python
for _ in range(5):
    print("ciao")
```

La variabile `_` è una convenzione per indicare "questo valore non mi serve".

**Generare una lista di numeri pari**

```python
pari = []
for n in range(0, 10, 2):
    pari.append(n)

print(pari)   # [0, 2, 4, 6, 8]
```

`range(0, 10, 2)` produce `0, 2, 4, 6, 8` — parte da `0`, si ferma prima di `10`, avanza di `2`.

**Generare una lista di numeri dispari**

```python
dispari = []
for n in range(1, 10, 2):
    dispari.append(n)

print(dispari)   # [1, 3, 5, 7, 9]
```

Basta cambiare il punto di partenza da `0` a `1`.

**Esempio:**

```python
for n in range(25, 35):
    print(n)
```

Stampa i numeri da `25` a `34`.


## Scansioni, trasformazioni e accumuli

Con `for` ricorrono tre schemi molto frequenti.

### Scansione

```python
for carattere in parola:
    print(carattere)
```

### Trasformazione

```python
parole = ["Giacomo", "Alessia", "Martina", "Francesco"]
parole_minuscole = []

for parola in parole:
    parole_minuscole.append(parola.lower())
```

### Accumulo

```python
numeri = [4, 9, 10, 2, -3]
somma = 0

for numero in numeri:
    somma += numero
```

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

## Esercizi

1. Stampa i numeri da 0 a 9.
2. Leggi due interi dall'input e scrivi una funzione void che li prende come parametro e stampa tutti i numeri compresi (estremi inclusi). Il programma deve passare i numeri alla funzione nell'ordine corretto (il minore come primo parametro, il maggiore come secondo)
3. Scrivi una funzione che  prende come paramtro un numero n maggiore di 0 e una stringa e stampa n volte una stessa stringa. Poi leggi un intero e una stringa dall'input e esegui la funzione.
4. Chiedi all'utente una parola e stampala lettera per lettera, una per riga.
5. Chiedi all'utente una parola e stampala lettera per lettera indicando anche la posizione (Prova sia con il for che con il while!).
6. Stampa solo i caratteri in posizione pari di una stringa.
7. Chiedi all'utente un numero `n` e stampa la tabellina di quel numero da 1 a 10.
8.  Calcola la somma e la media di una lista di numeri.
9.  Leggi due numeri (base, altezza) e stampa un rettangolo vuoto. Esempio per base=4, altezza=3:
    ```
    ****
    *  *
    ****
    ```
10. Leggi tre numeri (k, base, altezza) e stampa `k` rettangoli uno dopo l'altro. Esempio per k=3, base=4, altezza=3:
    ```
    ****
    *  *
    ****

    ****
    *  *
    ****

    ****
    *  *
    ****
    ```
11. Leggi tre numeri (k, base, altezza) e stampa `k` rettangoli affiancati. Esempio per k=3, base=4, altezza=3:
    ```
    **** **** ****
    *  * *  * *  *
    **** **** ****
    ```
12. Leggi `n` e stampa una piramide. Esempio per `n=5`:
    ```
    1
    22
    333
    4444
    55555
    ```
13. Leggi `n` e stampa una piramide diversa. Esempio per `n=5`:
    ```
    1
    12
    123
    1234
    12345
    ```
15. Data una matrice quadrata `n×n (ovvero una lista che contiene in ogni posizione un elemento di tipo lista), stampa solo i numeri sulla diagonale principale.
    ```python
    matrice = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  # output: 1  5  9
    ```
15. Crea a mano una matrice 3×3 con i numeri da 1 a 9 e stampala riga per riga.
16. Data una matrice, calcola la somma di tutti gli elementi.
17. Leggi dall'input una matrice `n×m` e stampala riga per riga (hai creato una funzione per l'esercizio 15? puoi riusarla?)
18. Data una matrice, costruisci la trasposta: una nuova matrice dove righe e colonne sono scambiate.
    ```python
    originale = [[1, 2, 3], [4, 5, 6]]  # trasposta: [[1, 4], [2, 5], [3, 6]]
    ```
19. Data una matrice di interi, trova la posizione `(riga, colonna)` del valore massimo.
20. Data una matrice quadrata `n×n`, stampa `sì` se è simmetrica (`matrice[i][j] == matrice[j][i]`), `no` altrimenti.
