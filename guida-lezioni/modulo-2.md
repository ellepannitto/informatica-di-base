# Modulo 02 · Variabili e strutture decisionali

## A fine lezione:

- Sai distinguere espressioni e istruzioni?
- Sai usare variabili?
- Sai definire la sintassi dell'assegnamento?
- Sai definire la semantica dell'assegnamento?
- Sai leggere input con `input()` e convertire tipi con `int()` e `str()`?
- Sai definire la sintassi dei costrutti `if`, `if-else`, `elif`?
- Sai definire la semantica dei costrutti `if`, `if-else`, `elif`?
- Sai scrivere semplici decisioni con `if`, `if-else`, `elif`?
- Sai organizzare uno script in sezioni leggibili?
- Sai tracciare lo stato del programma durante l'esecuzione?
- Sai riconoscere errori frequenti e localizzarli?
- Sai usare casi di test per smascherare errori logici?
- Sai usare condizioni composte con attenzione?
- Sai applicare le leggi di De Morgan?

## Recap operativo

La scorsa lezione:

- saper usare un interprete Python 3;
- saper scrivere un file `.py` in un editor;
- conoscere tipi fondamentali e confronti.

Per ripassare:

1. dato un numero di secondi `s` convertire in ore, minuti, secondi;
2. data una stringa `s` e un intero `n`, stampare il carattere in posizione `n` insieme al precedente e al successivo.

<details>
* attenzione alle parentesi superflue: una stringa resta una stringa anche senza "impacchettarla" ulteriormente. Aggiungerle può cambiare il modo in cui un interprete o un ambiente legge l'espressione;
* conviene scrivere l'operazione nel modo più semplice che conserva il tipo giusto. -- `type()`
</details>

## Struttura di uno script

Nel modulo 1 abbiamo scritto i primi file `.py` e introdotto `print()`.
Qui vediamo come organizzare uno script un po' più articolato.

### Struttura minima di uno script

Una convenzione pratica utile per organizzare file un po' meno banali è questa.

In generale uno script tende ad avere tre blocchi:

1. intestazione e commenti generali;
2. eventuali `import` di librerie esterne;
3. definizione di funzioni e poi corpo principale del programma.

Esempio schematico:

```python
# autore, data, scopo dello script

import sys

def capitalizza(s):
    '''
    funzione che data una stringa `s` restituisce la stessa stringa con l'iniziale maiuscola e
    il resto dei caratteri minuscoli
    '''
    return s[0].upper() + s[1:].lower()

# corpo principale
nome = input("Nome: ")
print(capitalizza(nome))
```

> rendiamo il codice più leggibile per noi e per chi lo rileggerà dopo.

### Commenti

Vale anche questa osservazione:

- le righe che iniziano con `#` sono commenti;
- i commenti non vengono eseguiti dall'interprete;
- servono a spiegare struttura, scopo e scelte del codice;
- blocchi di testo descrittivo possono comparire anche come stringhe multilinea usate come documentazione.

## Espressioni e istruzioni

Tutte le operazioni che abbiamo visto fino adesso (lasciamo stare `print()` per un attimo) sono **espressioni**: l'interprete Python valuta, la CPU esegue dei calcoli e otteniamo un valore (**NB: con un suo un tipo**).

Esempi:

- `3 // 4`
- `"ciao".upper()`
- `"ciao"+" "+"mondo!"`

Un linguaggio formale è fatto anche di **istruzioni**: un comando che provoda un effetto sulla memoria gestita dal programma.

## Variabili, assegnamento e stato

Con la sola REPL possiamo calcolare un valore, ma lo perdiamo subito.

Per esempio:

```python
3 + 4
```

calcola `7`, ma cosa succede se vogliamo riutilizzare quel risultato più avanti?

Per esempio vogliamo:

- considerare la temperatura di oggi in gradi centigradi (23 gradi)
- stampare il suo equivalente in gradi Kelvin
- stampare il suo equivalente in gradi Farenheit

```python
print(23 + 273.15)           # Kelvin
print(23 * 9/5 + 32)         # Fahrenheit
```

Nei programmi reali i valori cambiano, devono essere memorizzati e riutilizzati.
Senza un modo per conservare i risultati, il programma sarebbe limitato a calcoli “usa e getta”.

Problemi del codice precedente:

- Se la temperatura cambia (es. 25 gradi), devi ricordarti di cambiare tutti i 23
- Chi legge il codice non sa subito cosa rappresenta 23
- Non puoi usare facilmente quel valore in altre parti del programma

Per risolvere questo problema, usiamo le **variabili**.

```python
temperatura = 23

print(temperatura + 273.15)
print(temperatura * 9/5 + 32)
```

Una variabile è un “contenitore” che permette di:

- salvare un valore
- dargli un nome
- riutilizzarlo in seguito

## Sintassi dell'assegnamento

Forma generale:

```python
nome_variabile = espressione
```

Parti da riconoscere:

- a sinistra c'è il **nome** che vogliamo aggiornare;
- a destra c'è un valore oppure un'**espressione** da valutare;
- il simbolo `=` in Python introduce un'assegnazione.

Regole pratiche per il nome di una variabile:

- deve iniziare con una lettera oppure con `_`;
- dal secondo carattere in poi può contenere lettere, cifre e `_`;
- non può contenere spazi;
- non può iniziare con una cifra;
- non può essere una parola riservata di Python come `if`, `for`, `while`.

Esempi di nomi validi:

```python
eta
nome_studente
_contatore
voto2
```

Esempi di nomi non validi:

```python
2voto
nome studente
if
```

> **Attenzione:** in programmazione `=` non significa "è uguale a" nel senso della matematica.
> Significa invece "assegna alla variabile di sinistra il valore calcolato a destra".

Per questo:

```python
x = 3
```

è corretto, mentre:

```python
3 = x
```

non ha senso, perchè a sinistra dell'assegnamento deve esserci un nome di variabile, non un numero.

Esempi:

```python
eta = 20
nome = "Luca"
totale = prezzo + iva
```

## Semantica dell'assegnamento

Quando Python legge:

```python
somma = 4 + 3
```

succede questo:

1. valuta l'espressione a destra;
2. ottiene un risultato;
3. associa quel risultato al nome a sinistra;
4. aggiorna lo stato del programma.

![variabili](imgs/jars.jpg)

Da questo momento quei valori non sono più "persi": sono disponibili attraverso i nomi delle variabili.
Quindi una variabile può comparire a destra dentro una nuova espressione.

Per esempio:

```python
y = 3 + 1
x = y + 2
```

Qui Python:

- valuta `3 + 1` e assegna il risultato a `y`;
- legge il valore attualmente associato a `y`;
- calcola `y + 2`;
- assegna il risultato a `x`.

### Conseguenze importanti!

```python
x = x + 1
```

non è una formula matematica, ma un aggiornamento di stato:

- leggi il valore attuale di `x`;
- aggiungi `1`;
- salva il nuovo valore nella variabile `x`.

## Tracciare dati, memoria e output

Prima di procedere, vale la pena distinguere due cose che usiamo entrambe con la parola "programma":

- il **codice sorgente** — il testo che scriviamo nel file `.py`. Non cambia mentre lo eseguiamo. Può essere eseguito zero, una o mille volte.
- l'**esecuzione** — ciò che succede quando l'interprete legge quel codice e lo esegue con dati concreti. Ogni volta che lanciamo il programma, parte una nuova esecuzione: valori diversi in ingresso producono uno svolgimento diverso.

Quando tracciamo un programma, non stiamo leggendo il file: stiamo simulando una specifica esecuzione.

Lo **stato** di un programma non riguarda il testo che scriviamo nel file, ma il programma mentre viene eseguito.
È l'insieme dei valori che, in un certo momento dell'esecuzione, sono conservati in memoria e disponibili.
In questo modulo, in pratica, lo stato coincide soprattutto con i valori associati alle variabili.

Tracciare un programma significa simulare a mano che cosa succede riga per riga,
tenendo traccia dello stato delle variabili e di quello che viene stampato.

Dobbiamo abituarci a distinguere tre cose:

- il valore che Python calcola e conserva in memoria;
- l'output che Python stampa (visibile solo se si usa `print()`);
- l'ordine in cui le istruzioni vengono eseguite.

per esempio, consideriamo questo programma:

```python
x = 4
print("ciao" + " " + "mondo")
print(x)
y = x + 3
```

Una tabella minima può contenere:

| Passo | Codice sorgente                 | Stato della memoria | Output       |
| ----- | ------------------------------- | ------------------- | ------------ |
| 1     | `x = 4`                         | `x → 4`             |              |
| 2     | `print("ciao" + " " + "mondo")` | `x → 4`             | `ciao mondo` |
| 3     | `print(x)`                      | `x → 4`             | `4`          |
| 4     | `y = x + 3`                     | `x → 4, y → 7`      |              |

### Esempio guidato

```python
x = 10
y = x // 3
print(y)
```

Traccia:

| Passo | Codice sorgente | Stato della memoria | Output |
| ----- | --------------- | ------------------- | ------ |
| 1     | `x = 10`        | `x → 10`            |        |
| 2     | `y = x // 3`    | `x → 10, y → 3`     |        |
| 3     | `print(y)`      | `x → 10, y → 3`     | `3`    |

## `input()`, e casting

Torniamo all'esempio della temperatura:

```python
temperatura = 23

print(temperatura + 273.15)
print(temperatura * 9/5 + 32)
```

Abbiamo un altro problema:
se vogliamo eseguire questo script ogni giorno, dobbiamo aprire l'**editor** e modificare manualmente il valore 23.
Vorremmo fare sì che questo valore diventi un **parametro** del nostro programma in modo da poter eseguire ogni giorno lo script e vedere la temperatura in gradi Kelvin e Farenheit sul nostro schermo.

Abbiamo già visto `print()` nel modulo 1.
Qui introduciamo il suo complemento: `input()`.

`input()` è un comando utile per leggere un valore scritto dall'utente mentre il programma è in esecuzione.
Il testo che mettiamo tra parentesi è il **parametro** della funzione: serve a mostrare un messaggio sullo schermo, per esempio una domanda o un'istruzione.

## Sintassi di assegnamento con `input()`

Forma tipica:

```python
variabile = input("Messaggio: ")
```

Qui:

- `input(...)` legge qualcosa scritto dall'utente;
- `"Messaggio: "` è il parametro passato a `input()`;
- il valore letto viene assegnato alla variabile a sinistra.

Esempi:

```python
nome = input("Come ti chiami? ")
print(nome)
eta = input("Età: ")
print(eta)
```

Possiamo usare `input()` anche senza messaggio:

```python
testo = input()
```

## Semantica di assegnamento con `input()`

`input()` mostra il messaggio, aspetta che l'utente scriva qualcosa e si ferma quando l'utente preme Invio, cioè inserisce un ritorno a capo.
Solo a quel punto restituisce il testo letto.
Il risultato di `input()` è sempre una **stringa**.

```python
nome = input("Come ti chiami? ")
print("Ciao", nome)
```

| Passo | Codice sorgente                    | Stato della memoria | Output             |
| ----- | ---------------------------------- | ------------------- | ------------------ |
| 1     | `nome = input("Come ti chiami? ")` | `nome → "Ludovica"` | `Come ti chiami? ` |
| 2     | `print("Ciao", nome)`              | `nome → "Ludovica"` | `Ciao Ludovica`    |

Succede questo:

1. Python mostra il prompt;
2. l'utente scrive qualcosa;
3. `input()` restituisce quel testo;
4. quel testo viene salvato nella variabile;
5. il programma può continuare a usarlo.

### Casting

Problema:

```python
eta = input("Età: ")
print(eta + 1)
```

<details>
<summary>Cosa succede?</summary>
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    print(eta + 1)
          ~~~~^~~
TypeError: can only concatenate str (not "int") to str
```

| Passo | Codice sorgente        | Stato della memoria | Output     |
| ----- | ---------------------- | ------------------- | ---------- |
| 1     | `eta = input("Età: ")` | `eta → "33"`        | `Età: `    |
| 2     | `print(eta + 1)`       | `eta → "33"`        | !!! ERRORE |

</details>

Versione corretta:

```python
eta = input("Eta': ")
print(int(eta) + 1)
```

Alcune conversioni comuni:

| Funzione       | Effetto                     |
| -------------- | --------------------------- |
| `int("12")`    | converte in intero          |
| `str(12)`      | converte in stringa         |
| `float("3.5")` | converte in numero decimale |

Questa operazione di conversione di chiama **casting**.

## Esercizi

1. Scrivi un programma che legge nome e cognome e stampa un saluto, per esempio `Ciao, Mario Rossi!`.
2. Scrivi un programma che legge l'età e stampa: `Tra un anno avrai X anni` e `Un anno fa avevi Y anni`.
3. Scrivi un programma che legge due numeri interi e stampa la loro somma, il loro prodotto e il resto della divisione del primo per il secondo.
4. Scrivi un programma che legge tre numeri e ne stampa la media.
5. Scrivi un programma che legge una stringa e stampa:
   - la lunghezza della stringa;
   - il primo carattere;
   - l'ultimo carattere;
   - i primi tre caratteri.
6. Scrivi un programma che legge due numeri e stampa prima i valori inseriti e poi gli stessi valori scambiati.
7. Scrivi un programma che legge un nome e un anno di nascita e stampa una frase del tipo: `Ciao Anna, potresti avere 20 o 21 anni`.
8. Scrivi un programma che legge un numero intero di secondi (es. `3723`) e stampa la conversione nel formato: `1 ore, 2 minuti, 3 secondi`.
9. Scrivi un programma che legge nome e cognome e stampa:
    - il cognome tutto in maiuscolo;
    - il nome con solo la prima lettera maiuscola e il resto minuscolo;
    - le iniziali nel formato `M.R.`
10. Scrivi un programma che legge una stringa e stampa:
    - la stringa senza il primo e l'ultimo carattere;
11. Scrivi un programma che legge un prezzo in euro (numero decimale) e una percentuale di sconto (numero intero, es. `20`), e stampa il prezzo scontato e il risparmio.

## Tipo `bool` e nuove operazioni

Fin qui abbiamo lavorato con interi, stringhe e `float`.
Ora introduciamo **nuove operazioni** che non producono un numero o una stringa, ma un valore binario.

Per esempio possiamo controllare:

- se due valori sono uguali;
- se un numero è maggiore di un altro;

Esempi:

```python
3 > 1
2.5 <= 7.0
"anna" == "anna"
"ciao" != "buongiorno"
```

Queste operazioni non restituiscono un intero, un `float` o una stringa.
Restituiscono invece un **valore booleano**, cioè un valore che rappresenta il risultato di un confronto.

Il tipo `bool` ha due soli valori possibili:

- `True`
- `False`

Operatori di confronto che restituiscono un valore booleano:

| Operazione | Significato         | Esempio  |
| ---------- | ------------------- | -------- |
| `==`       | uguale a            | `x == 3` |
| `!=`       | diverso da          | `x != 3` |
| `<`        | minore di           | `x < 3`  |
| `<=`       | minore o uguale a   | `x <= 3` |
| `>`        | maggiore di         | `x > 3`  |
| `>=`       | maggiore o uguale a | `x >= 3` |

### Altre operazioni che restituiscono booleani

Anche alcune operazioni sulle stringhe restituiscono `True` oppure `False`.

Per esempio:

| Operazione            | Significato                                                  | Esempio                   |
| --------------------- | ------------------------------------------------------------ | ------------------------- |
| `in`                  | controlla se una sottostringa compare dentro una stringa     | `"cia" in "ciao"`         |
| `not in`              | controlla se una sottostringa non compare dentro una stringa | `"x" not in "ciao"`       |
| `s.startswith("...")` | controlla se la stringa inizia con un certo prefisso         | `"ciao".startswith("ci")` |
| `s.endswith("...")`   | controlla se la stringa finisce con un certo suffisso        | `"ciao".endswith("ao")`   |
| `s.isdigit()`         | controlla se tutti i caratteri sono cifre                    | `"123".isdigit()`         |
| `s.isalpha()`         | controlla se tutti i caratteri sono lettere                  | `"ciao".isalpha()`        |

Quando tracciamo o eseguiamo il programma, anche questi valori vanno rappresentati nello stato, proprio come interi, stringhe e `float`.

## Condizionare il flusso del programma

Con i booleani possiamo decidere il flusso di esecuzione.

Fin qui tutti in tutti i programmi che abbiamo visto le istruzioni vengono eseguite tutte e nell'ordine in cui le abbiamo scritte.

Ma molti problemi chiedono una scelta:

- se il numero è positivo, fai una cosa;
- se il nome viene prima alfabeticamente, stampa in un certo ordine;
- se l'input non è valido, reagisci in modo diverso.

Per gestire queste biforcazioni serve un **costrutto condizionale**.

## Sintassi di `if`

```python
if [espressione_booleana]:
    istruzione-1
    istruzione-2
    ...
    istruzione-k
```

- La parola chiave `if` introduce una condizione;
- dopo `if` c'è un'espressione booleana;
- la prima riga è conclusa da due punti `:` che aprono un blocco;
- il blocco di istruzioni da `1` a `k` va indentato.

## Semantica di `if`

```python
if [espressione_booleana]:
    istruzione-1
    istruzione-2
    ...
    istruzione-k
```

1. L'interprete valuta l'**espressione** booleana;
2. se vale `True`, esegue il blocco indentato;
3. se vale `False`, salta quel blocco e continua dopo.

## Esempi

```python
x = input("Inserisci la tua età: ")
x = int(x)

if x > 18:
    print("Sei maggiorenne")

print("Hai "+str(x)+" anni")
```

<details>
<summary>Esecuzione n.1</summary>

| Passo | Codice sorgente                       | Stato della memoria | Output                   |
| ----- | ------------------------------------- | ------------------- | ------------------------ |
| 1     | `x = input("Inserisci la tua età: ")` | `x → "33"`          | `Inserisci la tua età: ` |
| 2     | `x = int(x)`                          | `x → 33`            |                          |
| 3     | `if x > 18:`                          | `x → 33` ---> TRUE  |                          |
| 4     | `print("Sei maggiorenne")`            | `x → 33`            | `Sei maggiorenne!`       |
| 5     | `print("Hai "+str(x)+" anni")`        | `x → 33`            | `Hai 33 anni`            |

</details>

<details>
<summary>Esecuzione n.2</summary>

| Passo | Istruzione                            | Stato della memoria | Output                   |
| ----- | ------------------------------------- | ------------------- | ------------------------ |
| 1     | `x = input("Inserisci la tua età: ")` | `x → "15"`          | `Inserisci la tua età: ` |
| 2     | `x = int(x)`                          | `x → 15`            |                          |
| 3     | `if x > 18:`                          | `x → 15` ---> FALSE |                          |
| 4     | `print("Hai "+str(x)+" anni")`        | `x → 15`            | `Hai 15 anni`            |
</details>

> NB: tra la prima e la seconda esecuzione il numero di passi eseguiti è cambiato anche se il codice sorgente è rimasto invariato!

## `if-else`, `if-elif-else` e `if` annidati

Con `if` semplice possiamo eseguire un blocco solo quando una condizione è vera.
Però spesso vogliamo descrivere anche che cosa succede quando quella stessa condizione è falsa.

Per questo usiamo `if-else`, che separa esplicitamente due rami alternativi.
Quando invece una decisione deve essere presa all'interno di un altro ramo, useremo `if` annidati.

Se i casi possibili sono più di due ma restano sullo stesso livello, useremo `elif`.

## Sintassi di `if-else`

```python
if [espressione_booleana]:
    istruzione-1
    ...
    istruzione-j
else:
    istruzione-1
    ...
    istruzione-k
```

Qui ci sono due blocchi alternativi:

- il blocco dopo `if`;
- il blocco dopo `else`.

`else` non ha una condizione propria: raccoglie tutti i casi in cui la condizione dell'`if` vale `False`.

## Semantica di `if-else`

```python
if [espressione_booleana]:
    istruzione-1
    ...
    istruzione-j
else:
    istruzione-1
    ...
    istruzione-k
```

Con `if-else` Python:

1. valuta la condizione dell'`if`;
2. se vale `True`, esegue il primo blocco;
3. se vale `False`, esegue il blocco `else`.

Quindi tra i due rami se ne esegue sempre uno solo.

## Esempi:

```python
x = input("Inserisci la tua età: ")
x = int(x)

if x > 18:
    print("Sei maggiorenne")
else:
    print("Sei minorenne")

print("Hai "+str(x)+" anni")
```

<details>
<summary>Esecuzione n.1</summary>

| Passo | Istruzione                            | Stato della memoria | Output                   |
| ----- | ------------------------------------- | ------------------- | ------------------------ |
| 1     | `x = input("Inserisci la tua età: ")` | `x → "33"`          | `Inserisci la tua età: ` |
| 2     | `x = int(x)`                          | `x → 33`            |                          |
| 3     | `if x > 18:`                          | `x → 33` ---> TRUE  |                          |
| 4     | `print("Sei maggiorenne")`            | `x → 33`            | `Sei maggiorenne!`       |
| 5     | `print("Hai "+str(x)+" anni")`        | `x → 33`            | `Hai 33 anni`            |

</details>

<details>
<summary>Esecuzione n.2</summary>

| Passo | Istruzione                            | Stato della memoria | Output                   |
| ----- | ------------------------------------- | ------------------- | ------------------------ |
| 1     | `x = input("Inserisci la tua età: ")` | `x → "15"`          | `Inserisci la tua età: ` |
| 2     | `x = int(x)`                          | `x → 15`            |                          |
| 3     | `if x > 18:`                          | `x → 15` ---> FALSE |                          |
| 4     | `print("Sei minorenne")`              | `x → 15`            | `Sei minorenne`          |
| 5     | `print("Hai "+str(x)+" anni")`        | `x → 15`            | `Hai 15 anni`            |

</details>

## A volte due rami non bastano

Non si diventa maggiorenni in tutto il mondo alla stessa età!

- se hai più di 21 anni, sei maggiorenne in USA
- se hai meno di 21 anni, ma più di 18, sei maggiorenne in Italia
- se hai meno di 18 anni, non sei maggiorenne nè in Italia nè in USA.

In questi casi vorremmo una catena di controlli ordinati.

```python
x = input("Inserisci la tua età: ")
x = int(x)

if x > 21:
    print("Sei maggiorenne in USA")
else:
    if x > 18:
        print("Sei maggiorenne in Italia ma non in USA")
    else:
        print("Sei minorenne")
```

Questa cascata di `if` inclusi negli `else` può diventare poco leggibile...

## `if-elif-else`

```python
if [espressione_booleana]:
    istruzione
elif [espressione_booleana]:
    istruzione
elif [espressione_booleana]:
    istruzione
else:
    istruzione
```

Ogni `elif` aggiunge una nuova condizione.

L'interprete controlla i rami in ordine:

1. prova la condizione dell'`if`;
2. se è falsa, prova il primo `elif`;
3. continua finché trova la prima condizione vera;
4. se nessuna è vera, esegue `else`.

Quindi:

- conta l'ordine dei rami;
- viene eseguito solo il primo ramo che risulta vero;
- `else` copre il caso residuo.

## Esercizi

1. Leggi un numero intero e stampa `Positivo` solo se è maggiore di zero.
2. Leggi una parola e stampa `La parola è lunga` solo se ha più di 5 caratteri.
3. Leggi un numero intero e stampa `Pari` solo se è divisibile per 2.
4. Leggi un numero intero e stampa `Pari` oppure `Dispari` a seconda se è divisibile per due o meno.
5. Leggi due numeri interi e stampa il maggiore o un messaggio se sono uguali.
6. Leggi due nomi e stampali nell'ordine alfabetico corretto.
7. Leggi una parola e controlla se inizia con una vocale; stampa un messaggio diverso nei due casi.
8. Leggi un numero intero e stampa `Negativo`, `Zero` o `Positivo`.
9. Leggi un voto da 0 a 30 e stampa:
   - `Insufficiente` se il voto è minore di 18;
   - `Sufficiente` se è tra 18 e 23;
   - `Buono` se è tra 24 e 27;
   - `Ottimo` se è 28 o più.
10. Leggi una parola e stampa se è corta (meno di 4 lettere), media (da 4 a 7 lettere) o lunga (più di 7 lettere).
11. Leggi una coppia di numeri che rappresentano un mese (1–12) e un anno e stampa il mese successivo con l'anno corretto.
    Per esempio: mese 12, anno 2024 → `Gennaio 2025`.
12. Leggi nome, cognome e anno di nascita. Stampa sempre il nome completo e l'anno di nascita. Se l'anno di nascita è precedente al 2000, stampa anche `Nato/a nel secolo scorso`.
13. Leggi due numeri interi. Stampa sempre entrambi i numeri.
    Se il primo è maggiore del secondo, stampa anche `Il primo è maggiore`.
    Stampa sempre anche la loro somma.
14. Leggi una parola. Se ha più di 3 caratteri, stampa il secondo carattere; altrimenti stampa `Parola troppo corta`. In entrambi i casi stampa alla fine la lunghezza della parola.
15. Leggi una parola. Costruisci una variabile `risultato`:
    - se la parola inizia con una lettera maiuscola, `risultato` vale `"maiuscola"`;
    - altrimenti vale `"minuscola"`.
    Stampa `La parola è: ` seguito da `risultato`.
16. Leggi un numero intero. Costruisci una variabile `messaggio`:
    - se il numero è pari, `messaggio` vale `"pari"`;
    - altrimenti vale `"dispari"`.
    Stampa `Il numero X è` seguito da `messaggio`.
17. Leggi due numeri interi `a` e `b`. Se `a` è maggiore di `b`, scambia i valori delle due variabili.
Stampa sempre `a` e `b` alla fine: i valori usciti devono essere in ordine crescente.


Per ciascun programma e input indicato, cerca di predire l'output del programma con gli input proposti e compila la tabella con lo stato della memoria.

**T1.**

```python
x = int(input("x: "))
y = int(input("y: "))
z = x + y
if z > 10:
    x = x * 2
    etichetta = "grande"
elif z > 0:
    x = x + 1
    etichetta = "medio"
else:
    etichetta = "piccolo"
print(etichetta + ": " + str(x))
```

- Traccia con input `3`, `4`
- Traccia con input `6`, `7`

**T2.**

```python
s = input("Parola: ")
n = len(s)
if n > 4:
    s = s[0].upper() + s[1:]
    risultato = s + " (" + str(n) + ")"
else:
    risultato = s.upper()
print(risultato)
```

- Traccia con input `"python"`
- Traccia con input `"ciao"`

**T3.**

```python
a = int(input("a: "))
b = int(input("b: "))
if a > b:
    tmp = a
    a = b
    b = tmp
diff = b - a
if diff > 5:
    messaggio = "distanti"
else:
    messaggio = "vicini"
print(str(a) + " " + str(b) + " - " + messaggio)
```

- Traccia con input `9`, `2`

**T4.**

```python
n = int(input("n: "))
print("Inizio")
if n < 0:
    print("Negativo")
    n = -n
    print("Valore assoluto: " + str(n))
elif n == 0:
    print("Zero")
else:
    print("Positivo")
    n = n * n
print("Fine: " + str(n))
```

- Traccia con input `-3`
- Traccia con input `4`

**T5.**

```python
a = int(input("a: "))
b = int(input("b: "))
print("a=" + str(a) + " b=" + str(b))
if a > b:
    print("a è maggiore")
    diff = a - b
    print("Differenza: " + str(diff))
else:
    print("b è maggiore o uguale")
    diff = b - a
print("Distanza: " + str(diff))
```

- Traccia con input `a = 7`, `b = 2`
- Traccia con input `a = 3`, `b = 3`

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

```python
nome = input("Nome: ")
cognome = input("Cognome: ")
eta = input("Età: ")
print("Ciao " + nome + " " + cognome + "!")
print("Tra dieci anni avrai " + eta + 10 + " anni.")
```

**E2.**

```python
anno_nascita = input("Anno di nascita: ")
anno_corrente = 2025
eta = anno_corrente - anno_nascita
print("Hai circa " + str(eta) + " anni.")
```

**E3.**

```python
parola = input("Parola: ")
lunghezza = len(parola)
print("La parola ha " + lunghezza + " lettere.")
```

**E4.**

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

## Comporre condizioni

Fino adesso abbiamo visto operazioni che confrontano ad esempio numeri interi e restituiscono un valore booleano. Ma esistono anche operazioni che agiscono direttamente su valori booleani.

In particolare consideriamo tre operazioni:

- `and`
- `or`
- `not`

## Sintassi di `and`, `or`, `not`

Forme generali:

```python
espressione_booleana and espressione_booleana
```

```python
espressione_booleana or espressione_booleana
```

```python
not espressione_booleana
```

Queste operazioni si usano per costruire condizioni più complesse a partire da condizioni più semplici.

Esempi:

```python
x > 0 and x < 10
eta >= 18 or ha_permesso
not nome == "Ludovica"
```

## Semantica di `and`, `or`, `not`

Queste operazioni prendono in ingresso valori booleani e restituiscono a loro volta un valore booleano.

### Semantica di `and`

```python
A and B
```

vale `True` solo quando **entrambe** le condizioni sono vere.
Se almeno una delle due è falsa, il risultato è `False`.

Per esempio:

```python
x > 0 and x < 10
```

significa: "x è maggiore di 0 e contemporaneamente minore di 10".

### Tavola di verità di `and`

| x | y | x and y |
| --- | --- | --- |
| `False` | `False` | `False` |
| `False` | `True` | `False` |
| `True` | `False` | `False` |
| `True` | `True` | `True` |

### Semantica di `or`

```python
A or B
```

vale `True` quando **almeno una** delle due condizioni è vera.
Vale `False` solo quando sono false entrambe.

Per esempio:

```python
voto < 18 or voto > 30
```

significa: "il voto è fuori dall'intervallo valido", potrebbe esserlo perché minore di 18 o perché maggiore di 30.

### Tavola di verità di `or`

| x | y | x or y |
| --- | --- | --- |
| `False` | `False` | `False` |
| `False` | `True` | `True` |
| `True` | `False` | `True` |
| `True` | `True` | `True` |

### Semantica di `not`

```python
not A
```

inverte il valore booleano della condizione:

- se `A` vale `True`, allora `not A` vale `False`;
- se `A` vale `False`, allora `not A` vale `True`.

Per esempio:

```python
not x > 0
```

significa: "non è vero che x è maggiore di 0", equivale a `x<=0`.

### Tavola di verità di `not`

| x | not x |
| --- | --- |
| `False` | `True` |
| `True` | `False` |

## Esercizi

### Valutare espressioni booleane

Per ciascuna espressione e valori di variabili indicati, calcola il risultato (`True` o `False`) senza eseguire il codice.

1. `x = 5`, `y = 3` → `x > 0 and y > 0`
2. `x = -2`, `y = 4` → `x > 0 and y > 0`
3. `x = -2`, `y = 4` → `x > 0 or y > 0`
4. `x = -2`, `y = -1` → `x > 0 or y > 0`
5. `n = 7` → `not n > 10`
6. `n = 15` → `not n > 10`
7. `eta = 20`, `ha_documento = False` → `eta >= 18 and ha_documento`
8. `eta = 16`, `ha_documento = True` → `eta >= 18 or ha_documento`

### Condizioni composte nei programmi

1. Scrivi un programma che legge un numero intero e stampa `Nel range` se è compreso tra 1 e 100 (estremi inclusi), `Fuori range` altrimenti.
2. Un anno è bisestile se è divisibile per 4 ma non per 100, oppure se è divisibile per 400. Scrivi un programma che verifica questa condizione
3. Scrivi un programma che legge due stringhe e stampa `Almeno una è vuota` se almeno una delle due ha lunghezza zero, altrimenti stampa `Entrambe non vuote`.
4. Scrivi un programma che legge un numero intero e stampa `Fuori range` se è minore di 0 oppure maggiore di 10. Poi riscrivi la stessa condizione usando `not` e `and`.
5. Scrivi un programma che legge nome, età attuale ed età da raggiungere. Il programma stampa un saluto, la tua età attuale e tra quanti anni raggiungerai l'età desiderata.
    - Ad esempio Maria ha 10 anni e vuole averne 18, il programma stamperà:
      `Ciao Maria, oggi hai 10 anni, tra 8 anni ne avrai 18 come desideri`

## Ordine di precedenza degli operatori

Quando una condizione contiene più operatori, Python non legge tutto "da sinistra a destra" in modo piatto.
Usa invece un **ordine di precedenza**, cioè alcune operazioni vengono valutate prima di altre.

Nelle espressioni che useremo più spesso vale questa regola pratica:

1. parentesi;
2. confronti come `<`, `<=`, `==`, `!=`, `>`, `>=`;
3. `not`;
4. `and`;
5. `or`.

Quindi `not` ha precedenza su `and`, e `and` ha precedenza su `or`.

Esempio:

```python
True or False and False
```

non si legge come:

```python
(True or False) and False
```

ma come:

```python
True or (False and False)
```

perché `and` viene valutato prima di `or`.

Un altro esempio:

```python
not x > 0 and y > 0
```

si legge come:

```python
(not (x > 0)) and (y > 0)
```

Come in matematica, con le parentesi possiamo influenzare l'ordine delle operazioni.

Confronta:

```python
A or B and C
```

con:

```python
(A or B) and C
```

Non sono in generale equivalenti.

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

## Leggi di De Morgan

Le condizioni composte compaiono molto presto nei programmi.

Per esempio, se automatizzassimo il controllo degli accessi in discoteca il programma potrebbe somigliare a qualcosa come:

```python
if eta >= 18 and ha_documento:
    print("Accesso consentito")
```

Qui stiamo combinando due condizioni semplici:

- `eta >= 18`
- `ha_documento`

con l'operatore `and`.

Quando entra in gioco `not`, la lettura diventa meno immediata.

Supponiamo che il programma, invece che lasciare entrare, voglia stampare "Accesso non consentito" se:

- l'età è minore di 18, oppure
- non si ha il documento

```python
if eta < 18 or not ha_documento:
    print("Accesso non consentito")
```

Ma questo deve essere equivalente anche alla negazione della condizione precedente!

```python
if not (eta >= 18 and ha_documento):
    print("Accesso non consentito")
```

Le **leggi di De Morgan** servono a riscrivere negazioni di condizioni composte:

| Forma           | Equivalente       |
| --------------- | ----------------- |
| `not (A and B)` | `not A or not B`  |
| `not (A or B)`  | `not A and not B` |

Esempio:

```python
not (x > 0 and y > 0)
```

equivale a:

```python
not x > 0 or not y > 0
```

ovvero:

```python
x <= 0 or y <= 0
```

## Esercizi

Riscrivi ciascuna condizione in forma equivalente usando le leggi di De Morgan, poi verifica con un esempio numerico.

1. `not (x > 0 and y > 0)`
2. `not (a == b or c == d)`
3. `not (eta >= 18 and ha_documento)`

## Casi e tabelle di verità

Prima di scrivere il codice conviene costruire una tabella dei casi:
elencare esplicitamente tutte le combinazioni di input rilevanti e il comportamento atteso per ciascuna.

Questo serve a non dimenticare casi limite e a capire di quanti rami ha bisogno il programma.

**Esempio:** esercizio 13 — nome, età attuale, età da raggiungere.

Quali combinazioni di input esistono?

Prima versione della tabella — solo i casi "normali":

| Confronto                       | Esempio               | Output atteso                                                        |
| ------------------------------- | --------------------- | -------------------------------------------------------------------- |
| `eta_desiderata > eta_attuale`  | attuale=10, target=18 | `Ciao Maria, oggi hai 10 anni, tra 8 anni ne avrai 18 come desideri` |
| `eta_desiderata == eta_attuale` | attuale=18, target=18 | `Ciao Maria, hai già 18 anni come desideri`                          |
| `eta_desiderata < eta_attuale`  | attuale=25, target=18 | `Ciao Maria, hai già superato i 18 anni`                             |

La tabella mostra che servono tre rami: `if`, `elif`, `else`.
Costruirla prima evita di accorgersi del caso `==` solo dopo aver scritto il codice.

Ma cosa succede se l'utente inserisce un'età negativa?

| Input                          | Esempio               | Comportamento del programma    | Corretto? |
| ------------------------------ | --------------------- | ------------------------------ | --------- |
| `eta_attuale < 0`              | attuale=-5, target=18 | entra nel ramo `>`             | no        |
| `eta_desiderata < 0`           | attuale=10, target=-3 | entra nel ramo `<`             | no        |
| entrambe negative, uguali      | attuale=-5, target=-5 | entra nel ramo `==`            | no        |

Il programma non genera errori ma produce output privi di senso.
Per gestirlo correttamente bisogna aggiungere una validazione degli input **prima** di tutto il resto:

```python
nome = input("Nome: ")
eta_attuale = int(input("Età attuale: "))
eta_desiderata = int(input("Età desiderata: "))

if eta_attuale < 0 or eta_desiderata < 0:
    print("Errore: le età non possono essere negative.")
elif eta_desiderata > eta_attuale:
    anni_mancanti = eta_desiderata - eta_attuale
    print("Ciao " + nome + ", oggi hai " + str(eta_attuale) + " anni, tra " + str(anni_mancanti) + " anni ne avrai " + str(eta_desiderata) + " come desideri")
elif eta_desiderata == eta_attuale:
    print("Ciao " + nome + ", hai già " + str(eta_desiderata) + " anni come desideri")
else:
    print("Ciao " + nome + ", hai già superato i " + str(eta_desiderata) + " anni")
```

> La validazione dell'input è sempre il primo controllo da fare.
> Gli altri rami assumono che i dati siano validi — ma solo perché lo abbiamo già verificato.

| Età attuale        | Età desiderata                  | Output atteso                                                        |
| ------------------ | ------------------------------- | -------------------------------------------------------------------- |
| `eta_attuale <= 0` | `eta_desiderata <= 0`           | `INPUT NON VALIDO`                                                   |
|                    | `eta_desiderata > 0`            | `INPUT NON VALIDO`                                                   |
| `eta_attuale > 0`  | `eta_desiderata <= 0`           | `INPUT NON VALIDO`                                                   |
|                    | `eta_desiderata < eta_attuale`  | `Ciao Maria, hai già superato i 18 anni`                             |
|                    | `eta_desiderata == eta_attuale` | `Ciao Maria, hai già 18 anni come desideri`                          |
|                    | `eta_desiderata > eta_attuale`  | `Ciao Maria, oggi hai 10 anni, tra 8 anni ne avrai 18 come desideri` |

