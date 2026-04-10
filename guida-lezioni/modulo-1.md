# Modulo 01 · Introduzione alla programmazione e Python

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- orientarti tra interprete, editor e terminale;
- usare la REPL di Python per fare prove rapide;
- riconoscere i tipi fondamentali `int`, `float`, `str` e `bool`;
- descrivere il modello input -> elaborazione -> output;
- spiegare in modo intuitivo il ruolo di CPU, memoria e file system;
- eseguire comandi base nel terminale;
- tracciare a mano piccoli programmi molto semplici.

---

## Cornice del corso

La cornice del corso e' molto precisa:

- partiamo davvero da zero;
- l'obiettivo non e' imparare "tutto Python" in poche ore;
- ci interessa soprattutto capire come codificare un problema in modo computabile;
- il fuoco del corso e' sulla ricerca umanistica e linguistica, non sulla programmazione come fine a se stessa.

Per questo il corso insiste su tre livelli diversi:

1. un minimo di sintassi di Python;
2. la semantica di base, cioe' che cosa significa davvero quello che scriviamo;
3. un metodo di lavoro fatto di prove, errori, correzioni e lettura critica dei problemi.

Nella lezione introduttiva veniva anche esplicitato che non e' un corso su:

- stile Python "avanzato" o troppo idiomatico;
- programmazione a oggetti;
- paradigma funzionale;
- ottimizzazione spinta o algoritmi specialistici.

L'idea di fondo e' piu' pragmatica:

> prima impariamo a leggere, scrivere e controllare programmi semplici; poi useremo queste basi per lavorare su dati e problemi reali.

---

## Perche' Python

Python ci interessa per tre motivi pratici:

- e' un vero linguaggio di programmazione, non un giocattolo didattico;
- ha una sintassi leggibile, quindi lascia vedere bene i concetti;
- permette di passare rapidamente da un problema a un programma eseguibile.

Ci sono anche altri motivi concreti:

- Python e' un linguaggio generale, quindi quello che impari qui si trasferisce anche ad altri linguaggi;
- e' leggibile quasi "come si dice", quindi per chi comincia il salto iniziale e' meno traumatico;
- ha molte librerie gia' pronte per il lavoro linguistico e testuale, per esempio `nltk` e `spacy`;
- permette sia scripting rapido sia programmi piu' strutturati.

In un corso introduttivo Python serve soprattutto a:

- codificare un problema in modo computabile;
- imparare sintassi e semantica di base;
- prendere dimestichezza con un metodo di lavoro fatto di prove, controlli e correzioni;
- usare strumenti reali: interprete, editor, terminale.

Non ci interessa invece inseguire subito:

- lo stile "pythonic" piu' raffinato;
- l'orientamento agli oggetti;
- la teoria avanzata degli algoritmi;
- librerie molto specialistiche.

> L'obiettivo iniziale non e' scrivere codice elegante. E' scrivere codice corretto, leggibile e controllabile.

---

## Come lavorare

Alcune abitudini utili fin dall'inizio:

- carta e penna prima del codice;
- tanti esercizi piccoli;
- lavoro per passi brevi;
- niente copia-incolla meccanico;
- confronto con un'altra persona quando possibile;
- lettura attenta dei messaggi di errore.

Conviene tenere presenti anche questi consigli pratici:

- usare carta e penna prima del computer, perche' la parte difficile spesso viene prima del codice;
- fare esercizi piccoli ma frequenti, come quando si impara una lingua;
- se possibile lavorare in coppia, perche' spiegare un problema ad alta voce spesso lo rende piu' chiaro;
- trascrivere il codice invece di copiarlo e incollarlo, sia per evitare errori nascosti sia per fare pratica vera;
- non aspettarsi fluidita' immediata: all'inizio la programmazione sembra spesso un salto misterioso, poi le cose iniziano a incastrarsi.

Se qualcosa non funziona:

1. leggi il messaggio;
2. isola un esempio piu' piccolo;
3. controlla tipi, parentesi, apici, indentazione;
4. confronta quello che volevi fare con quello che il programma fa davvero.

![How to draw an owl](../vecchio-materiale/imgs/owl.png)

> Programmare include sempre una quota di `trial and error`. Non e' un'anomalia: e' il lavoro.

> "Don't panic" e' un buon principio didattico: le prime lezioni servono proprio a costruire familiarita' con un linguaggio che all'inizio sembra piu' difficile di quanto sia davvero.

---

<a id="mod1-ambiente"></a>
## Ambiente di lavoro

Per iniziare a programmare servono tre strumenti distinti:

| Strumento | A cosa serve | Esempi |
| --- | --- | --- |
| Interprete | esegue codice Python | `python3`, REPL |
| Editor | scrive e salva file di testo | VS Code |
| Terminale | lancia comandi e programmi | `zsh`, PowerShell, bash |

E' importante non confonderli:

- l'editor serve a scrivere il codice;
- il terminale serve a lanciare comandi;
- l'interprete Python legge il codice e lo esegue.

Due dettagli pratici importanti:

- un programma Python va scritto in un **text editor** che lavora su testo semplice;
- strumenti come Word non vanno bene, perche' aggiungono formattazione e metadati che non fanno parte del codice.

Una sessione di lavoro tipica e' questa:

1. scrivi un file `.py` nell'editor;
2. apri il terminale nella cartella giusta;
3. esegui `python3 nome_file.py`;
4. osserva l'output e correggi se necessario.

### Cosa installiamo davvero

Python e' un linguaggio formale con una sintassi e una semantica. Quello che installiamo e' un **interprete**, cioe' un programma capace di:

- leggere il codice Python;
- verificarne la sintassi;
- interpretarne il significato;
- tradurlo in operazioni eseguibili dalla macchina.

Per scrivere codice in modo comodo, usiamo anche un editor:

![Visual Studio Code](../vecchio-materiale/imgs/vscode.png)

> Il punto importante non e' il prodotto preciso, ma capire il ruolo dei tre strumenti.

### Perche' conviene usare anche il terminale

Nella lezione introduttiva veniva suggerito di non dipendere solo da interfacce grafiche.

Motivo pratico:

- molti lavori reali su dati e testi si eseguono su server;
- sui server spesso non c'e' un'interfaccia grafica completa;
- saper lanciare uno script da riga di comando rende il lavoro piu' trasferibile.

Per questo, prima o poi, conviene abituarsi anche a una forma come:

```bash
python3 nome_script.py
```

oppure:

```bash
python3 nome_script.py input.txt
```

---

## Python come linguaggio formale

Un linguaggio di programmazione e' un linguaggio formale costituito da:

| Componente | Significato |
| --- | --- |
| Vocabolario | simboli disponibili: valori, identificatori, keyword |
| Sintassi | regole con cui combiniamo i simboli |
| Semantica | significato operativo di cio' che scriviamo |

Nel vocabolario troviamo:

- valori, raggruppati in tipi;
- parole riservate come `if`, `def`, `while`, `for`.

Nella sintassi distinguiamo subito:

- **espressioni**, che producono valori;
- **istruzioni**, che modificano lo stato o il flusso del programma.

Della semantica si occupa l'interprete.

Analogia utile:

- Python e' il linguaggio;
- quello che installiamo e' l'interprete di Python;
- cioe' il programma che sa leggere quel formalismo e tradurlo in operazioni comprensibili alla macchina.

In questo senso non "installiamo il linguaggio" come idea astratta: installiamo lo strumento che lo esegue.

---

<a id="mod1-repl"></a>
## REPL, tipi e operazioni fondamentali

La **REPL** e' la modalita' interattiva di Python: scrivi un'espressione, premi Invio, Python la valuta e mostra il risultato.

Per aprirla:

```bash
python3
```

Vedrai qualcosa di simile:

```python
>>>
```

### Tipi fondamentali

I quattro tipi di base sono questi:

| Tipo | Significato | Esempi |
| --- | --- | --- |
| `int` | numeri interi | `0`, `7`, `-12` |
| `float` | numeri con la virgola | `3.14`, `0.5`, `-2.0` |
| `str` | stringhe di caratteri | `"ciao"`, `'Python'` |
| `bool` | valori booleani | `True`, `False` |

Il tipo di un valore determina quali operazioni hanno senso su di esso.

### Interi e float

| Operazione | Sintassi | Esempio |
| --- | --- | --- |
| Somma | `N + N` | `3 + 15` |
| Sottrazione | `N - N` | `10 - 4` |
| Moltiplicazione | `N * N` | `3 * 7` |
| Divisione | `N / N` | `7 / 2` |
| Potenza | `N ** N` | `3 ** 2` |
| Divisione intera | `N // N` | `17 // 5` |
| Modulo | `N % N` | `17 % 5` |

```python
>>> 3 + 15
18
>>> 3 ** 2
9
>>> 17 // 5
3
>>> 17 % 5
2
>>> 13.8 / 4
3.45
```

Conviene insistere molto su due operazioni che a scuola tendiamo a trattare meno:

- `//` per il **quoziente** della divisione intera;
- `%` per il **resto** della divisione intera.

Esempio discusso a voce:

```python
>>> 44 // 6
7
>>> 44 % 6
2
```

L'idea e' la stessa della divisione in colonna:

- `6 * 7 = 42`
- da `44` avanzano `2`

![Divisione intera e resto](../vecchio-materiale/imgs/divisione.png)

### Stringhe

Le stringhe sono sequenze di caratteri.

| Operazione | Sintassi | Esempio | Risultato |
| --- | --- | --- | --- |
| Concatenazione | `S1 + S2` | `'ab' + 'cd'` | `'abcd'` |
| Selezione | `S[i]` | `'ciao'[1]` | `'i'` |
| Maiuscolo | `S.upper()` | `'ciao'.upper()` | `'CIAO'` |
| Minuscolo | `S.lower()` | `'CIAO'.lower()` | `'ciao'` |
| Conteggio | `S1.count(S2)` | `'aaa'.count('a')` | `3` |
| Lunghezza | `len(S)` | `len('ciao')` | `4` |

```python
>>> 'Hello' + ' ' + 'world'
'Hello world'
>>> 'linguistica'[0]
'l'
>>> 'linguistica'[3]
'g'
>>> len('Hello world')
11
>>> 'ciao'.upper()
'CIAO'
```

Vale anche un punto che per chi comincia non e' ovvio:

- `+` tra numeri significa somma;
- `+` tra stringhe significa concatenazione.

Esempio:

```python
>>> "3" + "15"
'315'
```

Qui Python non sta facendo un calcolo aritmetico: sta mettendo insieme due sequenze di caratteri.

Un altro dettaglio importante emerso a voce:

- gli spazi non vengono "indovinati";
- se vuoi uno spazio in mezzo tra `"ciao"` e `"mondo"`, devi scriverlo tu.

Quindi:

```python
>>> "ciao" + "mondo"
'ciaomondo'
>>> "ciao" + " " + "mondo"
'ciao mondo'
```

> In informatica si conta a partire da zero.

Le sottostringhe si leggono anche per intervalli:

```python
>>> "linguistica"[0:3]
'lin'
```

Qui il carattere iniziale e' incluso, quello finale no.

### Booleani

I booleani servono a rappresentare vero e falso.

```python
>>> True and False
False
>>> True or False
True
>>> not True
False
```

Tabelle di verita' essenziali:

| `and` | `True` | `False` |
| --- | --- | --- |
| `True` | `True` | `False` |
| `False` | `False` | `False` |

| `or` | `True` | `False` |
| --- | --- | --- |
| `True` | `True` | `True` |
| `False` | `True` | `False` |

| `not` | Risultato |
| --- | --- |
| `not True` | `False` |
| `not False` | `True` |

Dettaglio pratico richiamato in lezione:

- in Python i valori booleani si scrivono `True` e `False`;
- con iniziale maiuscola;
- non esistono abbreviazioni come `T` e `F`.

### Operazioni di confronto

| Operazione | Sintassi |
| --- | --- |
| Maggiore | `T > T` |
| Minore | `T < T` |
| Uguale | `T == T` |
| Maggiore o uguale | `T >= T` |
| Minore o uguale | `T <= T` |

Restituiscono sempre un booleano.

```python
>>> 3 < 8
True
>>> len('ciao') <= len('hello')
True
>>> 'hello world' == 'Hello World'
False
>>> 'Hello World'.lower() == 'hello world'
True
```

Per i numeri vale l'ordinamento usuale. Per le stringhe vale un ordinamento alfanumerico.

C'e' anche un punto utile per orientarsi:

- tutte le operazioni di confronto restituiscono un booleano;
- quindi possono essere composte con `and`, `or` e `not`;
- per controllare uguaglianza si usa `==`, non `=`.

Esempio:

```python
>>> len("ciao") <= len("hello")
True
>>> 3 == 3
True
>>> 3 == 5
False
```

---

## Esercizi sulla REPL

### Esercizi 1 · Espressioni numeriche

Scrivi un'espressione che calcoli:

1. il successore di `15`;
2. la meta' del triplo di `12`;
3. il triplo della meta' di `12`;
4. il doppio della differenza tra `15` e `7`;
5. il doppio della differenza tra `3` e `7`;
6. la somma dei primi tre numeri pari;
7. la media di `2`, `5`, `9`;
8. il resto della divisione tra `44` e `7`;
9. la somma dei quadrati dei primi tre numeri naturali.

### Esercizi 2 · Stringhe

Scrivi un'espressione che calcoli:

1. la lunghezza della stringa `"Happy families are all alike"`;
2. la sua versione tutta maiuscola;
3. la concatenazione di `"Happy families are all alike"` e `"every unhappy family is unhappy in its own way"`;
4. la stessa concatenazione ma con uno spazio in mezzo;
5. il primo carattere di `"linguistica"`;
6. il sesto carattere di `"supercalifragilistichespiralidoso"` in maiuscolo;
7. la concatenazione del sesto, nono, decimo, ventiseiesimo e ventisettesimo carattere della stessa stringa.

### Esercizi 3 · Che cosa produce?

Per ciascuna espressione, scrivi il valore prodotto e il tipo del risultato:

1. `5 * (2 + 4)`
2. `152 % 9`
3. `"banana" + "fragola"`
4. `"olio".upper()`
5. `len("carote")`
6. `"cenerentola"[8]`

### Esercizi 4 · Confronti

Controlla se e' vero che:

1. la seconda lettera del tuo nome e' uguale alla quarta del tuo cognome;
2. `3 * 5 < 7 + 2`;
3. `"aceto" < "olio"`;
4. `"aceto".upper() == "aceto"`;
5. `len("carote" + "cipolla" + "sedano") == len("carote") + len("cipolla") + len("sedano")`;
6. `"barba" < "Barba"`;
7. `"barba" < "barbabietola"`.

---

<a id="mod1-von-neumann"></a>
## Architettura di Von Neumann

Un computer puo' essere descritto in modo intuitivo con tre blocchi principali:

| Componente | Ruolo |
| --- | --- |
| CPU | esegue le istruzioni |
| Memoria | conserva dati e istruzioni durante l'esecuzione |
| Input/Output | riceve dati dall'esterno e produce risultati |

Schema essenziale:

```text
input -> CPU + memoria -> output
```

Quando esegui un programma Python:

- il codice viene letto come sequenza di istruzioni;
- i valori intermedi vengono tenuti in memoria;
- la CPU esegue un passo alla volta;
- il risultato puo' essere mostrato a schermo o scritto su file.

Questo modello e' utile perche' ci costringe a ragionare in termini di stato, dati e trasformazioni.

---

<a id="mod1-input-output"></a>
## Cos'e' un programma

Un programma e' una procedura che prende dati in ingresso, li elabora e produce un risultato.

| Fase | Domanda tipica |
| --- | --- |
| Input | quali dati ricevo? |
| Elaborazione | quali regole applico? |
| Output | che risultato restituisco? |

Esempi:

| Programma | Input | Output |
| --- | --- | --- |
| somma di due numeri | `a`, `b` | `a + b` |
| conteggio caratteri | una stringa | un numero |
| scelta del file giusto | nome e percorso | file aperto o errore |

Qui entra anche il **file system**:

- i file sono contenitori persistenti di dati;
- le cartelle organizzano i file;
- il sistema operativo gestisce accesso a file, memoria, processi e periferiche.

---

<a id="mod1-terminale"></a>
## Terminale: comandi di base

Il terminale serve a spostarsi nelle cartelle e lanciare programmi.

Comandi essenziali:

| Comando | Significato |
| --- | --- |
| `pwd` | mostra la cartella corrente |
| `ls` | elenca file e cartelle |
| `cd nome-cartella` | entra in una cartella |
| `cd ..` | torna alla cartella padre |
| `python3 file.py` | esegue uno script Python |

### Percorsi assoluti e relativi

- un **percorso assoluto** parte dalla radice del sistema;
- un **percorso relativo** parte dalla cartella in cui ti trovi adesso.

Tre scorciatoie molto utili:

- `.` significa "la cartella corrente";
- `..` significa "la cartella superiore";
- possiamo concatenare piu' salite con percorsi del tipo `../../`.

Quindi, per esempio:

```bash
ls .
ls ..
cd ..
ls ../../
```

In pratica:

- `ls` e `ls .` sono equivalenti;
- `./file.txt` indica un file nella cartella corrente;
- `../file.txt` indica un file nella cartella sopra;
- ogni `..` ci fa salire di un livello nell'albero delle cartelle.

Punto pratico importante:

- uno stesso file puo' essere indicato in molti modi diversi;
- con il nome assoluto completo;
- con un percorso relativo breve;
- oppure con forme come `./pippo.txt`.

L'importante non e' usare sempre la forma piu' lunga, ma capire che il percorso deve descrivere correttamente come arrivare al file partendo dalla cartella corrente.

Esempio:

```bash
pwd
ls
cd guida-lezioni
ls
cd ..
python3 scripts/genera_programma.py
```

> Se un comando "non trova il file", il primo controllo da fare e' quasi sempre la cartella corrente.

---

<a id="mod1-tracciamento"></a>
## Tracciare dati, memoria e output

Nel primo modulo conviene gia' abituarsi a distinguere tre cose:

- il valore che Python calcola;
- l'output che Python stampa;
- l'ordine in cui le istruzioni vengono eseguite.

Tracciare un programma significa simulare a mano che cosa succede riga per riga.

Una tabella minima puo' contenere:

| Passo | Istruzione o espressione | Stato / risultato |
| --- | --- | --- |
| 1 | `x = 4` | `x` vale `4` |
| 2 | `y = x + 3` | `y` vale `7` |
| 3 | `print(y)` | output: `7` |

Questo esercizio serve a:

- distinguere valore in memoria e testo stampato;
- capire l'ordine di esecuzione;
- trovare errori di logica prima di eseguire il programma.

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

Questa tecnica basta gia' per controllare piccoli esempi, senza introdurre altro lessico tecnico.

Il lavoro piu' sistematico su:

- espressioni e istruzioni;
- variabili e assegnamento;
- primo script;
- input/output;
- casi normali, limite ed errore

comincia nel modulo 2 e viene consolidato nel modulo 3.

---

## Esercizi suggeriti

### REPL

1. Calcola il resto della divisione tra `44` e `7`.
2. Scrivi un'espressione che produca il triplo della meta' di `12`.
3. Ottieni il primo carattere di `"linguistica"`.

### Terminale

1. Entra nella cartella del progetto e mostra il contenuto.
2. Spostati in `guida-lezioni` e poi torna indietro.
3. Esegui uno script Python dal terminale.

### Tracciamento

Traccia a mano:

```python
a = 5
b = a + 2
print(a)
print(b)
```

### Progettazione

Per un programma che legge un numero e stampa `"pari"` oppure `"dispari"`, scrivi almeno:

- due casi normali;
- due casi limite;
- un caso di errore.

---

## Riepilogo

Hai quindi in un solo posto:

- motivazioni e metodo di lavoro;
- ambiente di sviluppo;
- Python come linguaggio formale;
- REPL e tipi fondamentali;
- operazioni aritmetiche, stringhe, booleani e confronti;
- modello input/elaborazione/output;
- architettura di Von Neumann;
- terminale e percorsi;
- tracciamento di esempi molto semplici.
