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

## Il problema che porta all'assegnamento

Con la sola REPL possiamo calcolare un valore, ma lo perdiamo subito.

Per esempio:

```python
3 + 4
```

calcola `7`, ma se vogliamo riusare quel risultato in un secondo passo abbiamo bisogno di un nome.

L'assegnamento serve proprio a questo:

- conservare un risultato;
- dargli un nome;
- riusarlo in istruzioni successive.

---

## Sintassi dell'assegnamento

Forma generale:

```python
nome_variabile = espressione
```

Esempi:

```python
eta = 20
nome = "Luca"
totale = prezzo + iva
```

Parti da riconoscere:

- a sinistra c'e' il nome che vogliamo aggiornare;
- a destra c'e' un valore oppure un'espressione da valutare;
- il simbolo `=` in Python introduce un'assegnazione.

---

## Semantica dell'assegnamento

Quando Python legge:

```python
x = y + 3
```

succede questo:

1. valuta l'espressione a destra;
2. ottiene un risultato;
3. associa quel risultato al nome a sinistra;
4. aggiorna lo stato del programma.

Quindi:

```python
x = x + 1
```

non e' una formula matematica, ma un aggiornamento di stato:

- leggi il vecchio valore di `x`;
- aggiungi `1`;
- salva il nuovo valore in `x`.

---

<a id="mod2-tracciamento"></a>
## Tracciare dati, memoria e output

Tracciare un programma significa simulare a mano che cosa succede riga per riga, tenendo traccia dello stato delle variabili e di quello che viene stampato.

Conviene abituarsi a distinguere tre cose:

- il valore che Python calcola e conserva in memoria;
- l'output che Python stampa (visibile solo se si usa `print()`);
- l'ordine in cui le istruzioni vengono eseguite.

Una tabella minima puo' contenere:

| Passo | Istruzione | Stato della memoria | Output |
| ----- | ---------- | ------------------- | ------ |
| 1 | `x = 4` | `x = 4` | |
| 2 | `y = x + 3` | `x = 4`, `y = 7` | |
| 3 | `print(y)` | `x = 4`, `y = 7` | `7` |

Questo esercizio serve a:

- distinguere valore in memoria e testo stampato;
- capire l'ordine di esecuzione;
- trovare errori di logica prima ancora di eseguire il programma.

### Esempio guidato

```python
x = 10
y = x // 3
print(y)
```

Traccia:

| Passo | Stato della memoria | Output |
| --- | --- | --- |
| dopo `x = 10` | `x = 10` | |
| dopo `y = x // 3` | `x = 10`, `y = 3` | |
| dopo `print(y)` | `x = 10`, `y = 3` | `3` |

### Esercizio

Traccia a mano:

```python
a = 5
b = a + 2
print(a)
print(b)
```

---

<a id="mod2-input-output"></a>
## `input()`, `print()`, `type()` e casting

## Il problema che porta a `print()` e `input()`

Un programma non deve solo calcolare: deve anche comunicare con l'esterno.

Due bisogni diversi:

- mostrare un risultato all'utente;
- ricevere un dato dall'utente.

Qui entrano in gioco:

- `print()` per l'output;
- `input()` per l'input.

---

## Sintassi di `print()`

Forma base:

```python
print(valore1, valore2)
```

Esempi:

```python
print("Ciao")
print("Ciao", nome)
print(eta + 1)
```

`print(...)` e' una chiamata di funzione:

- il nome della funzione e' `print`;
- tra parentesi passiamo gli argomenti;
- gli argomenti vengono stampati in output.

---

## Semantica di `print()`

Serve a produrre output verso lo schermo.

```python
nome = "Anna"
print("Ciao", nome)
```

Quando Python esegue `print(...)`:

1. valuta gli argomenti;
2. li converte in una forma stampabile;
3. li manda sullo standard output.

`print(...)` non salva valori in memoria: rende visibile all'esterno un risultato.

---

## Sintassi di `input()`

Forma tipica:

```python
variabile = input("Messaggio: ")
```

Esempi:

```python
nome = input("Come ti chiami? ")
eta = input("Eta': ")
```

Possiamo usare `input()` anche senza messaggio:

```python
testo = input()
```

---

## Semantica di `input()`

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

## Il problema che porta a `if`

Fin qui il programma esegue istruzioni in ordine.

Ma molti problemi chiedono una scelta:

- se il numero e' positivo, fai una cosa;
- se il nome viene prima alfabeticamente, stampa in un certo ordine;
- se l'input non e' valido, reagisci in modo diverso.

Per gestire queste biforcazioni serve un costrutto condizionale.

---

## Sintassi di `if`

```python
if eta >= 18:
    print("Maggiorenne")
```

Parti da riconoscere:

- `if` introduce una condizione;
- dopo `if` c'e' un'espressione booleana;
- i due punti `:` aprono il blocco;
- il blocco va indentato.

---

## Semantica di `if`

La semantica operativa di `if` si puo' riassumere cosi':

1. Python valuta la condizione;
2. se vale `True`, esegue il blocco indentato;
3. se vale `False`, salta quel blocco e continua dopo.

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

---

## Sintassi di `if-else`

```python
if eta >= 18:
    print("Maggiorenne")
else:
    print("Minorenne")
```

Qui ci sono due blocchi alternativi:

- il blocco dopo `if`;
- il blocco dopo `else`.

`else` non ha una condizione propria: raccoglie tutti i casi in cui la condizione dell'`if` vale `False`.

---

## Semantica di `if-else`

Con `if-else` Python:

1. valuta la condizione dell'`if`;
2. se vale `True`, esegue il primo blocco;
3. se vale `False`, esegue il blocco `else`.

Quindi tra i due rami se ne esegue sempre uno solo.

---

## Il problema che porta a `if-elif-else`

A volte due rami non bastano.

Per esempio:

- classificare un voto;
- distinguere piu' fasce numeriche;
- descrivere piu' casi mutuamente esclusivi.

In questi casi serve una catena di controlli ordinati.

---

## Sintassi di `if-elif-else`

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

Questa forma si usa quando:

- i casi sono piu' di due;
- vogliamo provarli in ordine;
- ogni `elif` aggiunge una nuova condizione.

---

## Semantica di `if-elif-else`

Python controlla i rami in ordine:

1. prova la condizione dell'`if`;
2. se e' falsa, prova il primo `elif`;
3. continua finche' trova la prima condizione vera;
4. se nessuna e' vera, esegue `else`.

Quindi:

- conta l'ordine dei rami;
- viene eseguito solo il primo ramo che risulta vero;
- `else` copre il caso residuo.

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
