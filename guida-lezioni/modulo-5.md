# Modulo 05 · Funzioni

## A fine lezione

- Sai definire funzioni con parametri e valore di ritorno?
- Sai distinguere funzione e procedura?
- Sai scomporre un problema in sottoproblemi più piccoli?
- Sai progettare interfacce semplici con responsabilità singola?
- Sai leggere una funzione come black box?
- Sai costruire piccole utility testabili e riusabili?

## Codice che si ripete?

Negli esercizi sulle liste abbiamo scritto molte volte questo stesso blocco:

```python
numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())
```

Eccolo in tre esercizi diversi, fianco a fianco:

```python
# Es. 10 — stampa al contrario
numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())

i = len(numeri) - 1
while i >= 0:
    print(numeri[i])
    i = i - 1
```

```python
# Es. 9 — trova il massimo
numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())

massimo = numeri[0]
i = 1
while i < len(numeri):
    if numeri[i] > massimo:
        massimo = numeri[i]
    i = i + 1
print(massimo)
```

```python
# Es. 12 — media e valori sopra la media
numeri = []
n = int(input())
while n != 0:
    numeri.append(n)
    n = int(input())

somma = 0
i = 0
while i < len(numeri):
    somma = somma + numeri[i]
    i = i + 1
media = somma / len(numeri)
print("Media:", media)
```

Le prime cinque righe sono **identiche** in tutti e tre. Se domani vogliamo cambiare la sentinella da `0` a `-1`, o aggiungere un prompt all'`input()`, dobbiamo modificarle in ogni punto in cui compaiono — e rischiamo di dimenticarne uno.

Questo è il problema che le funzioni risolvono: isoliamo quel blocco in un posto solo, gli diamo un nome, e lo chiamiamo quando serve.

```python
def leggi_lista(sentinella):
    numeri = []
    n = int(input())
    while n != sentinella:
        numeri.append(n)
        n = int(input())
    return numeri
```

I tre programmi diventano:

```python
# Es. 10 — stampa al contrario
numeri = leggi_lista(0)

i = len(numeri) - 1
while i >= 0:
    print(numeri[i])
    i = i - 1
```

```python
# Es. 9 — trova il massimo
numeri = leggi_lista(0)

massimo = numeri[0]
i = 1
while i < len(numeri):
    if numeri[i] > massimo:
        massimo = numeri[i]
    i = i + 1
print(massimo)
```

```python
# Es. 12 — media e valori sopra la media
numeri = leggi_lista(0)

somma = 0
i = 0
while i < len(numeri):
    somma = somma + numeri[i]
    i = i + 1
media = somma / len(numeri)
print("Media:", media)
```

La logica di lettura esiste in un posto solo. Se la modifichiamo, cambia ovunque.

Lo stesso ragionamento vale per qualsiasi blocco che compare più volte: contare le vocali, trovare il minimo, verificare se una stringa è palindroma. Ogni volta che ti sorprendi a copiare e incollare le stesse righe, è il momento di scrivere una funzione.

## Funzioni in matematica

In matematica hai già incontrato le funzioni. Per esempio:

> **f(x) = 2x + 1**

Questa funzione prende un numero `x` e restituisce un numero: il doppio di `x` più uno.

| `x`  | `f(x) = 2x + 1` |
|------|-----------------|
| 0    | 1               |
| 1    | 3               |
| 3    | 7               |
| −2   | −3              |
| 10   | 21              |

Scrivere `f(3)` vuol dire applicare la regola a `3` e ottenere `7`.

Tre cose che già sai:

- una funzione ha un **nome** (`f`);
- riceve uno o più **input** (`x`) e produce un **output** (`f(x)`);
- la regola è scritta una volta sola, ma puoi applicarla a qualunque valore.

In Python si scrive esattamente la stessa cosa:

```python
def f(x):
    return 2 * x + 1

f(3)   # → 7
f(10)  # → 21
```

Il parallelismo è diretto:

| matematica       | Python               |
|------------------|----------------------|
| nome della funzione | `def nome_funzione` |
| variabile `x`    | parametro `x`        |
| `f(x) = ...`     | `return ...`         |
| `f(3)`           | `f(3)`               |

La differenza principale: in Python la funzione può fare cose più complesse di una formula — può contenere variabili, cicli, condizioni. Ma la struttura è la stessa.

## Perché servono le funzioni

Le funzioni servono a evitare duplicazione, isolare un compito preciso e rendere il codice più leggibile.

- una funzione riceve input;
- esegue una trasformazione;
- restituisce un risultato.

Esempio:

```python
def triplo_del_successore(x):
    successore = x+1
    return 3 * successore
```

- una funzione è una **delega**;
- non dobbiamo saper fare tutto da soli nel codice principale;
- dobbiamo anche saper decidere quale sottoproblema affidare a un blocco specializzato.

Pensiamo alla costruzione di una casa. Chiamiamo un elettricista e gli diciamo: "ho bisogno di un impianto per una casa da 80 mq con tre stanze". L'elettricista fa il suo lavoro e ti consegna l'impianto finito. Non ti interessa come lo fa: ti interessa che funzioni.

Se poi costruiamo una seconda casa, richiamiamo lo stesso elettricista — questa volta per 120 mq e cinque stanze. Stessa persona, stesso mestiere, parametri diversi.

In programmazione funziona esattamente così:

- la **funzione** è l'elettricista — sa fare un lavoro preciso;
- i **parametri** sono le istruzioni che gli dai ogni volta — cambiano da chiamata a chiamata;
- il **valore di ritorno** è il risultato che ti consegna.

```python
def impianto_elettrico(metri_quadri, num_stanze):
    # ... calcola il materiale necessario ...
    return costo
```

Chiamarla con valori diversi produce risultati diversi, ma la logica interna è scritta una volta sola.

Quando il programma cresce, iniziamo a ripetere pezzi di ragionamento:

- la stessa trasformazione su input diversi;
- lo stesso controllo in più punti;
- lo stesso sottoproblema dentro programmi più grandi.

Definite una funzione serve a isolare quel comportamento in un blocco riusabile.

## Sintassi della definizione di funzione

Una funzione va definita e poi chiamata. Sono due cose distinte.

**La definizione è un'istruzione.** Quando Python incontra la definizione, salva il codice della funzione in memoria — ma non lo esegue ancora. La funzione esiste, ma non ha fatto nulla.

**La chiamata o invocazione è un'espressione.** Quando scriviamo `area_rettangolo(4, 6)`, Python esegue il corpo della funzione e produce un valore. Quel valore ha un tipo — in questo caso `int`. Possiamo usarlo ovunque si può usare un'espressione: in un `print`, in un assegnamento, in una condizione (a seconda del tipo!).

```python
def area_rettangolo(base, altezza):
    return base * altezza

print(area_rettangolo(4, 6))
```

```python
risultato = area_rettangolo(4, 6)   # int
print(area_rettangolo(3, 5))        # int stampato
if area_rettangolo(2, 2) > 3:       # int confrontato
    print("grande")
```

### Sintassi generale

```python
def nome_funzione(parametro_1, parametro_2, ..., parametro_n):

    # istruzione_1
    # ...
    # istruzione_n

    return espressione
```

Parti da riconoscere:

- `def` introduce la definizione della funzione;
- il nome della funzione ha le stesse restrizioni di un nome di variabile (lettere, cifre, `_`; non può iniziare con una cifra; non può essere una parola chiave);
- i parametri sono nomi di variabile a tutti gli effetti — valgono le stesse regole; non possono essere numeri, stringhe o espressioni;
- i due punti `:` aprono il blocco;
- `return` restituisce il risultato.

## Invocare una funzione

### Sintassi dell'invocazione

```python
nome_funzione(argomento_1, argomento_2, ..., argomento_n)
```

Gli argomenti sono espressioni: possono essere valori, variabili, o qualsiasi espressione con il tipo giusto.

```python
area_rettangolo(4, 6)           # valori
area_rettangolo(base, altezza)  # variabili
area_rettangolo(b * 2, h + 1)   # espressioni
```

Il numero di argomenti deve corrispondere al numero di parametri nella definizione.

### Semantica dell'invocazione

Quando Python incontra una chiamata di funzione:

1. valuta ciascun argomento da sinistra a destra;
2. assegna ogni valore al parametro corrispondente **per posizione**:
```
chiamata:        area_rettangolo( 4  ,    6   )
                                  |       |
                                  |       |
                                  ↓       ↓
definizione:  def area_rettangolo(base, altezza):
```
All'interno del corpo, `base` varrà `4` e `altezza` varrà `6`.
3. esegue il corpo della funzione con quei valori;
4. quando incontra `return`, valuta l'espressione dopo `return`, interrompe il corpo e restituisce quel valore al chiamante;
5. la chiamata nel programma principale si "sostituisce" con quel valore.

Tutto ciò che sta dopo un `return` nello stesso ramo non viene eseguito.

### Commentare che cosa fa una funzione

Dopo una definizione conviene lasciare almeno traccia di:

- che cosa fa la funzione;
- che cosa si aspetta in input;
- che cosa restituisce in output.

Questo è utile perché un nome di parametro da solo non garantisce abbastanza contesto, soprattutto quando il codice cresce.

## Tracciare lo stato con le funzioni

Nei moduli precedenti abbiamo imparato a compilare la tabella dello stato riga per riga. Con le funzioni lo stato si divide in due parti: la memoria del **programma principale** e la memoria **locale della funzione**, che esiste solo durante la chiamata.

Consideriamo:

```python
def triplo_del_successore(x):
    successore = x + 1
    triplo = 3 * successore
    return triplo

n = 15
risultato = triplo_del_successore(n)
print(risultato)
```

| passo | riga                                  | stato principale   | stato funzione                          | output |
| ----- | ------------------------------------- | ------------------ | --------------------------------------- | ------ |
| 1     | `n = 15`                              | n=15               | —                                       |        |
| 2     | `triplo_del_successore(n)` — chiamata | n=15               | x=15                                    |        |
| 3     | `successore = x + 1`                  | n=15               | x=15, successore=16                     |        |
| 4     | `triplo = 3 * successore`             | n=15               | x=15, successore=16, triplo=48          |        |
| 5     | `return triplo`                       | n=15               | → restituisce 48, memoria locale chiusa |        |
| 6     | `risultato = 48`                      | n=15, risultato=48 | —                                       |        |
| 7     | `print(risultato)`                    | n=15, risultato=48 | —                                       | 48     |

Tre cose da notare:

- al passo 2 la memoria locale si **apre**: `x` riceve il valore di `n`;
- al passo 5 la memoria locale si **chiude**: `successore` e `triplo` spariscono, solo il valore di ritorno passa al chiamante;
- il programma principale non vede mai `successore` né `triplo`: esistono solo dentro la funzione.

## Scope (non 🧹🧹)

Lo **scope** (o ambito) di una variabile è la parte del programma in cui quella variabile esiste ed è accessibile.

In Python ogni funzione ha il proprio scope locale:
le variabili create dentro una funzione — inclusi i parametri — esistono solo per la durata di quella chiamata.
Il programma principale ha il proprio scope globale.

Le due memorie sono **separate e indipendenti**. Questo ha tre conseguenze importanti.

### 1 · Le variabili locali non sono visibili fuori dalla funzione

```python
def calcola():
    risultato = 42
    return risultato

print(risultato)   # NameError: risultato non esiste qui
```

`risultato` esiste solo dentro `calcola`. Fuori dalla funzione, quel nome non è definito.

### 2 · Le variabili esterne non sono visibili dentro la funzione

```python
x = 10

def raddoppia():
    return x * 2   # funziona, ma è una cattiva pratica: x viene "catturata" dallo scope globale
```

Usare variabili globali dentro una funzione è tecnicamente possibile ma va evitato:
rende la funzione dipendente dal contesto esterno e difficile da riusare.
La regola pratica è: **tutto ciò di cui la funzione ha bisogno deve entrare come parametro**.

```python
def raddoppia(x):   # corretto: x è un parametro
    return x * 2
```

### 3 · Stesso nome, variabili diverse

Se una variabile nel programma principale e una variabile dentro la funzione hanno lo stesso nome,
sono due variabili distinte e non si influenzano a vicenda.

```python
def incrementa(x):
    x = x + 1       # questa x è locale alla funzione
    return x

x = 5               # questa x è nel programma principale
y = incrementa(x)
print(x)            # 5  — x nel programma principale non è cambiata
print(y)            # 6
```

Traccia dello stato:

| passo | riga | stato principale | stato funzione |
|-------|------|-----------------|----------------|
| 1 | `x = 5` | x=5 | — |
| 2 | `incrementa(x)` — chiamata | x=5 | x=5 (copia) |
| 3 | `x = x + 1` | x=5 | x=6 |
| 4 | `return x` | x=5 | → restituisce 6, memoria locale chiusa |
| 5 | `y = 6` | x=5, y=6 | — |

La `x` della funzione è una copia del valore passato, non la stessa variabile.
Modificarla dentro la funzione non tocca la `x` di fuori.

---

## Esercizi

### Tracciare lo stato

**1.** `[M5-TRACE-01]` Compila la tabella dello stato per il seguente programma:

```python
def somma(a, b):
    risultato = a + b
    return risultato

x = 3
y = 7
z = somma(x, y)
print(z)
```

| passo | riga | stato principale | stato funzione | output |
|-------|------|-----------------|----------------|--------|
| | | | | |

**2.** `[M5-TRACE-02]` Compila la tabella dello stato per il seguente programma:

```python
def is_pari(n):
    return n % 2 == 0

x = 4
if is_pari(x):
    print("pari")
else:
    print("dispari")
```

| passo | riga | stato principale | stato funzione | output |
|-------|------|-----------------|----------------|--------|
| | | | | |

### Trovare l'errore

**3.** `[M5-ERR-01]` Il seguente programma vuole stampare il doppio di un numero, ma non funziona. Individua l'errore e correggilo.

```python
def doppio(n):
    n = n * 2

x = 5
print(doppio(x))
```

**4.** `[M5-ERR-02]` Il seguente programma vuole calcolare la somma di tre numeri usando una funzione, ma produce un risultato sbagliato. Individua l'errore.

```python
def somma(a, b):
    return a + b

print(somma(1, 2, 3))
```

**5.** `[M5-ERR-03]` Il seguente programma vuole usare il risultato della funzione in una condizione, ma produce un errore. Spiega perché e correggilo.

```python
def messaggio(nome):
    print("Ciao, " + nome)

if messaggio("Alice") == "Ciao, Alice":
    print("ok")
```

### Scope

**6.** `[M5-SCOPE-01]` Il seguente programma produce un errore oppure stampa qualcosa? Spiega cosa succede e perché.

```python
def calcola():
    x = 100
    return x

calcola()
print(x)
```

**7.** `[M5-SCOPE-02]` Considera il seguente programma. Cosa stampa? Spiega perché `n` nel programma principale non cambia.

```python
def azzera(n):
    n = 0
    return n

n = 42
azzera(n)
print(n)
```

**8.** `[M5-SCOPE-03]` Il seguente programma vuole raddoppiare una variabile globale dall'interno di una funzione. Funziona come ci si aspetta? Riscrivilo nel modo corretto.

```python
valore = 10

def raddoppia():
    return valore * 2

print(raddoppia())
```

**9.** `[M5-SCOPE-04]` Cosa stampa il seguente programma? Compila la tabella dello stato.

```python
def f(x):
    y = x * 2
    return y

x = 3
y = 10
risultato = f(5)
print(x, y, risultato)
```

| passo | riga | stato principale | stato funzione | output |
|-------|------|-----------------|----------------|--------|
| | | | | |

**10.** `[M5-SCOPE-05]` Il seguente programma contiene un errore di scope. Individualo e correggilo senza usare variabili globali.

```python
def calcola_sconto():
    return prezzo * sconto / 100

prezzo = 80
sconto = 20
print(calcola_sconto())
```

### Scrivere funzioni

**11.** `[M5-WRITE-01]` Scrivi una funzione `perimetro_rettangolo(base, altezza)` che restituisce il perimetro di un rettangolo.

```
perimetro_rettangolo(3, 5)  →  16
```

**12.** `[M5-WRITE-02]` Scrivi una funzione `divisibile(n, d)` che restituisce `True` se `n` è divisibile per `d`, `False` altrimenti.

```
divisibile(12, 4)  →  True
divisibile(7, 3)   →  False
```

**13.** `[M5-WRITE-03]` Scrivi una funzione `massimo(a, b)` che restituisce il maggiore tra due numeri senza usare `max()`.

```
massimo(3, 7)  →  7
massimo(5, 5)  →  5
```

**14.** `[M5-WRITE-04]` Scrivi una funzione `conta_vocali(s)` che riceve una stringa e restituisce il numero di vocali che contiene.

```
conta_vocali("informatica")  →  5
conta_vocali("ritmo")        →  2
```

**15.** `[M5-WRITE-05]` Scrivi una funzione `ripeti(s, n)` che restituisce la stringa `s` ripetuta `n` volte, separata da spazi, senza usare l'operatore `*`.

```
ripeti("ciao", 3)  →  "ciao ciao ciao"
ripeti("ok", 1)    →  "ok"
```

**16.** `[M5-WRITE-06]` Scrivi una funzione `valore_assoluto(n)` che restituisce il valore assoluto di un numero senza usare `abs()`.

```
valore_assoluto(-3)  →  3
valore_assoluto(5)   →  5
```

**17.** `[M5-WRITE-07]` Scrivi una funzione `è_vocale(c)` che riceve un carattere e restituisce `True` se è una vocale (maiuscola o minuscola), `False` altrimenti.

```
è_vocale("a")  →  True
è_vocale("b")  →  False
```

**18.** `[M5-WRITE-08]` Scrivi una funzione `fahrenheit_in_celsius(f)` che converte gradi Fahrenheit in Celsius con la formula `(f - 32) × 5 / 9`.

```
fahrenheit_in_celsius(32)   →  0.0
fahrenheit_in_celsius(212)  →  100.0
```

**19.** `[M5-WRITE-09]` Scrivi una funzione `minimo(a, b)` che restituisce il minore tra due numeri senza usare `min()`.

```
minimo(3, 7)  →  3
minimo(5, 5)  →  5
```

**20.** `[M5-WRITE-10]` Scrivi una funzione `media(a, b, c)` che restituisce la media aritmetica di tre numeri.

```
media(4, 8, 6)  →  6.0
```

### Scrivere funzioni — livello avanzato

**21.** `[M5-WRITE-11]` Scrivi una funzione `somma_cifre(n)` che riceve un intero positivo e restituisce la somma delle sue cifre, senza convertirlo in stringa (usa `%` e `//`).

```
somma_cifre(123)  →  6
somma_cifre(9)    →  9
```

**22.** `[M5-WRITE-12]` Scrivi una funzione `è_primo(n)` che restituisce `True` se `n` è un numero primo, `False` altrimenti.

```
è_primo(7)   →  True
è_primo(12)  →  False
```

**23.** `[M5-WRITE-14]` Scrivi una funzione `inverti_stringa(s)` che restituisce la stringa invertita senza usare lo slicing `[::-1]`. Costruisci il risultato carattere per carattere partendo dalla fine.

```
inverti_stringa("ciao")   →  "oaic"
inverti_stringa("radar")  →  "radar"
```

**24.** `[M5-WRITE-15]` Scrivi una funzione `conta_occorrenze(lista, valore)` che restituisce quante volte `valore` compare nella lista, senza usare `.count()`.

```
conta_occorrenze([3, 1, 4, 1, 5, 1], 1)  →  3
```

