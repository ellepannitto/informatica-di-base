# Modulo 02 · Variabili e strutture decisionali

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- eseguire un primo script Python da file;
- distinguere espressioni e istruzioni;
- usare variabili e assegnamento;
- leggere input con `input()` e convertire tipi con `int()` e `str()`;
- usare `print()` per costruire output espliciti;
- scrivere semplici decisioni con `if`, `if-else`, `elif`;
- organizzare uno script in sezioni leggibili.

---

## Recap operativo

Prima di affrontare questo modulo, conviene richiamare questi prerequisiti:

- saper usare un interprete Python 3;
- saper scrivere un file `.py` in un editor;
- conoscere tipi fondamentali e confronti.

Tre esercizi tipici di ripasso:

1. convertire un numero di secondi in giorni, ore, minuti, secondi;
2. scambiare i valori di due variabili;
3. data una stringa `s` e un intero `n`, stampare il carattere in posizione `n` insieme al precedente e al successivo.

La seconda lezione trascritta ripartiva proprio da qui:

- controllare che interprete e IDE fossero installati correttamente;
- verificare gli esercizi assegnati;
- chiarire piccoli errori ricorrenti prima di introdurre nuovi costrutti.

Un richiamo utile emerso a voce: negli esercizi sulle stringhe molte persone tendevano ad aggiungere parentesi non necessarie. Il punto didattico era questo:

- una stringa resta una stringa anche senza "impacchettarla" ulteriormente;
- aggiungere parentesi superflue puo' cambiare il modo in cui un interprete o un ambiente legge l'espressione;
- conviene scrivere l'operazione nel modo piu' semplice che conserva il tipo giusto.

---

<a id="mod2-primo-script"></a>
## Primo script: scrivere ed eseguire un file `.py`

La REPL e' utile per prove rapide, ma i programmi veri si scrivono in file.

Esempio:

```python
print("Ciao")
print("Benvenuto nel corso")
```

Salva questo contenuto in `saluto.py` ed esegui:

```bash
python3 saluto.py
```

Differenza pratica:

- nella REPL provi una riga alla volta;
- in uno script scrivi una sequenza di istruzioni che puo' essere salvata, corretta e rieseguita.

### Struttura minima di uno script

Una convenzione pratica utile per organizzare file un po' meno banali e' questa.

In generale uno script tende ad avere tre blocchi:

1. intestazione e commenti generali;
2. eventuali `import` di librerie esterne;
3. definizione di funzioni e poi corpo principale del programma.

Esempio schematico:

```python
# autore, data, scopo dello script

import sys

def capitalizza(s):
    return s[0].upper() + s[1:].lower()

# corpo principale
nome = input("Nome: ")
print(capitalizza(nome))
```

L'idea non e' burocratica: e' rendere il codice piu' leggibile per noi e per chi lo rileggera' dopo.

### Commenti

Vale anche questa osservazione:

- le righe che iniziano con `#` sono commenti;
- i commenti non vengono eseguiti dall'interprete;
- servono a spiegare struttura, scopo e scelte del codice;
- blocchi di testo descrittivo possono comparire anche come stringhe multilinea usate come documentazione.

---

<a id="mod2-espressioni-istruzioni"></a>
## Espressioni e istruzioni

Un'**espressione** e' qualcosa che Python valuta per ottenere un valore.

Esempi:

- `3 + 4`
- `"ciao".upper()`
- `5 < 8`

Un'**istruzione** e' un comando che dice al programma di fare qualcosa.

Esempi:

- `x = 7`
- `print("ciao")`
- `if x > 0:`

Confronta:

```python
3 + 4
```

produce un valore.

```python
x = 3 + 4
```

prima valuta `3 + 4`, poi salva il risultato in una variabile.

---

<a id="mod2-assegnazione"></a>
## Variabili, assegnamento e stato

Una variabile e' un nome associato a un valore.

```python
eta = 20
nome = "Luca"
```

L'assegnamento:

1. valuta l'espressione a destra;
2. associa il risultato al nome a sinistra;
3. aggiorna lo stato del programma.

Esempio:

```python
x = 10
y = x + 5
x = x - 2
```

Traccia sintetica:

| Passo | Stato |
| --- | --- |
| `x = 10` | `x = 10` |
| `y = x + 5` | `x = 10`, `y = 15` |
| `x = x - 2` | `x = 8`, `y = 15` |

> `=` in Python non significa uguaglianza matematica permanente: significa "assegna".

---

<a id="mod2-input-output"></a>
## `input()`, `print()`, `type()` e casting

### `print()`

Serve a produrre output verso lo schermo.

```python
nome = "Anna"
print("Ciao", nome)
```

### `input()`

Legge sempre una stringa.

```python
nome = input("Come ti chiami? ")
print("Ciao", nome)
```

`input()` non e' una magia complicata, ma un modo per creare una piccola interazione col programma.

Esempio:

```python
nome = input("Inserisci il tuo nome: ")
print(nome)
```

Qui succede questo:

1. Python mostra il prompt;
2. l'utente scrive qualcosa;
3. quel testo viene salvato nella variabile;
4. il programma puo' continuare a usarlo.

Questo e' molto utile quando vogliamo riusare lo stesso script con dati diversi senza riscrivere ogni volta il codice.

### `type()`

Ti aiuta a vedere il tipo di un valore.

```python
print(type(3))
print(type("3"))
```

### Casting

Per convertire tipi:

```python
eta = int(input("Eta': "))
print(eta + 1)
```

Alcune conversioni comuni:

| Funzione | Effetto |
| --- | --- |
| `int("12")` | converte in intero |
| `str(12)` | converte in stringa |
| `float("3.5")` | converte in numero decimale |

Errore tipico:

```python
eta = input("Eta': ")
print(eta + 1)
```

Qui `eta` e' una stringa, quindi `+ 1` non funziona.

---

<a id="mod2-boolean-if"></a>
## Booleani e decisioni con `if`

Il tipo `bool` ha due soli valori:

- `True`
- `False`

Gli operatori di confronto producono booleani:

```python
x > 0
x == 10
nome != ""
```

Con i booleani possiamo decidere il flusso di esecuzione.

### `if`

```python
eta = int(input("Eta': "))

if eta >= 18:
    print("Maggiorenne")
```

La semantica operativa di `if` si puo' riassumere cosi':

- Python valuta l'espressione booleana dopo `if`;
- se vale `True`, esegue il primo blocco;
- altrimenti passa al ramo successivo (`else` oppure `elif`).

Per questo, in casi come:

```python
if nome < cognome:
    print(nome, cognome)
else:
    print(cognome, nome)
```

non serve scrivere:

```python
if nome < cognome == True:
```

perche' il comando `if` sta gia' chiedendo se quell'espressione vale vero oppure no. Scriverlo esplicitamente non e' un errore concettuale grave, ma e' ridondante.

### `if-else`

```python
if eta >= 18:
    print("Maggiorenne")
else:
    print("Minorenne")
```

### `elif`

Esempio di classificazione del voto:

```python
voto = int(input("Voto: "))

if voto < 18:
    print("L'esame non e' stato superato")
elif voto < 23:
    print("Sufficiente")
elif voto < 27:
    print("Buono")
else:
    print("Ottimo")
```

Questo e' il caso tipico in cui ci sono piu' soglie ordinate.

### Un esempio guidato: nome e cognome in ordine alfabetico

Un esercizio semplice ma utile e' questo:

- leggere nome e cognome;
- confrontarli come stringhe;
- stampare i due valori nell'ordine alfabetico giusto.

Questo esempio serviva a consolidare insieme:

- uso di variabili con nomi significativi;
- confronto tra stringhe;
- `if/else`;
- `print()`;
- eventuale uso di `input()` per rendere lo script interattivo.

---

<a id="mod2-condizioni-annidate"></a>
## Condizioni annidate

Una condizione e' detta annidata quando compare dentro un'altra condizione.

```python
x = int(input("Numero: "))

if x >= 0:
    if x == 0:
        print("Zero")
    else:
        print("Positivo")
else:
    print("Negativo")
```

Questo stile va usato solo quando il secondo controllo ha senso solo dopo il primo.

La versione annidata della classificazione dei voti si puo' anche riscrivere con `elif` per renderla piu' leggibile.

---

## Esercizi sulle condizioni

Per esempio:

1. dato nome e cognome, stampa il nome completo in ordine alfabetico;
2. scrivi una funzione che restituisce il maggiore tra due interi;
3. usa la funzione precedente per stampare una frase esplicita;
4. date due parole, stampa quella piu' lunga;
5. dati tre interi, stampali dal maggiore al minore;
6. date tre parole, mettile in ordine alfabetico;
7. dato anno e mese, stampa che anno sara' fra un mese e che anno era un mese fa;
8. scrivi una funzione che stabilisce se un anno e' bisestile;
9. data una parola, controlla se inizia con `p` e finisce con `o`, gestendo il caso di stringa troppo corta.

---

## Struttura di uno script

Una struttura standard di script e' questa:

```python
#----------------------------------
# intestazione dello script
# autore/autrice, data, contatti...
#----------------------------------

import sys

def capitalizza(stringa):
    """
    prende una stringa e la restituisce capitalizzata
    """
    nuova_stringa = stringa[0].upper() + stringa[1:].lower()
    return nuova_stringa

nome = sys.argv[1]
cognome = sys.argv[2]

nome = capitalizza(nome)
cognome = capitalizza(cognome)

print(nome + " " + cognome)
```

Struttura tipica:

1. import di librerie;
2. definizione di funzioni ausiliarie;
3. flusso principale del programma.

### Commenti e leggibilita'

- tutto cio' che segue `#` sulla riga e' un commento;
- i commenti servono a spiegare il codice;
- una funzione non banale dovrebbe avere almeno una breve descrizione.

### Indentazione e blocchi

In Python i blocchi si riconoscono dall'indentazione.

- il corpo di una funzione e' un blocco;
- il corpo di un `if` o di un `for` e' un blocco;
- se l'indentazione e' sbagliata, il programma non e' valido.

---

## Errori tipici del modulo

1. Dimenticare i due punti dopo `if`.
2. Mescolare stringhe e numeri senza conversione.
3. Usare `=` invece di `==` in una condizione.
4. Aspettarsi che `input()` restituisca un intero.
5. Perdere l'indentazione corretta.

---

## Esercizi suggeriti

1. Scrivi uno script che legge un nome e stampa un saluto.
2. Scrivi uno script che legge un numero e stampa il suo doppio.
3. Scrivi uno script che legge un numero e stampa `positivo`, `negativo` oppure `zero`.
4. Scrivi uno script che legge due numeri e stampa il maggiore.
5. Per ciascun frammento, traccia lo stato finale delle variabili:

```python
x = 3
y = x + 2
x = y * 2
```

---

## Riepilogo

In questo modulo hai introdotto il modello base del programma imperativo:

- istruzioni eseguite in ordine;
- variabili che tengono memoria;
- input e output espliciti;
- condizioni che fanno scegliere un ramo di esecuzione;
- una prima struttura leggibile dello script.
