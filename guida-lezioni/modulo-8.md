# Modulo 08 · Ciclo for, file e formati strutturati

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- usare il ciclo `for` su liste, stringhe e `range()`;
- capire la semantica elementare dell'iterazione;
- leggere il comportamento del `for` in termini di stato;
- applicare il `for` a conteggi, trasformazioni e scansioni;
- leggere e scrivere file di testo in modo elementare;
- costruire semplici analisi testuali a partire da un file;
- riconoscere casi tipici in cui il `for` evita codice ripetitivo.

---

<a id="mod8-for"></a>
## Il problema che porta al `for`

Nel notebook 2 si partiva da un esempio come questo:

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

Il `for` nasce proprio per esprimere una stessa azione ripetuta su una sequenza.

---

### Sintassi del `for`

```python
for identificatore in iterabile:
    # istruzioni
```

Semantica intuitiva:

1. Python prende un elemento dell'iterabile;
2. lo assegna alla variabile di iterazione;
3. esegue il blocco;
4. passa all'elemento successivo;
5. quando gli elementi finiscono, continua dopo il `for`.

Esempio:

```python
for parola in ["Ciao", "Mondo", "Python"]:
    print(parola.lower())
```

La seconda lezione lo spiegava anche in modo ancora piu' operativo:

- il `for` esegue lo stesso blocco per ogni elemento dell'iterabile;
- a ogni passo aggiorna la variabile di iterazione;
- quando non ci sono piu' elementi, il flusso prosegue dopo il ciclo.

Questo e' il motivo per cui il `for` e' cosi' utile quando:

- la stessa operazione concettuale va ripetuta molte volte;
- il codice manuale diventerebbe lungo, fragile e poco riusabile;
- non vogliamo scrivere una riga separata per ogni posizione della lista.

---

<a id="mod8-range"></a>
## `range(n)` e conteggio delle iterazioni

Il notebook 2 introduceva `range(n)` per ripetere qualcosa un numero fissato di volte.

```python
for numero in range(5):
    print("Eseguo l'istruzione print all'iterazione numero", numero)
```

`range(5)` produce i valori:

```python
0, 1, 2, 3, 4
```

Quindi il ciclo esegue il blocco 5 volte.

Usi tipici:

- contare;
- scorrere posizioni;
- costruire piccole tabelle o figure;
- iterare su intervalli di numeri.

La trascrizione aggiungeva anche due dettagli pratici:

- `range(5)` conta da `0` a `4`;
- `range(a, b)` permette di lavorare direttamente su un intervallo che parte da `a` e arriva a `b - 1`.

Quindi:

```python
for n in range(25, 35):
    print(n)
```

stampa i numeri da `25` a `34`.

---

## `for` e memoria

Il notebook mostrava anche il tracciamento di:

```python
for x in [24, -13, 8]:
    y = x + 1

print(x, y)
```

Alla fine del ciclo:

- `x` contiene l'ultimo elemento iterato;
- `y` contiene l'ultimo valore calcolato.

Questo esempio serve a ricordare che:

- il `for` aggiorna la variabile di iterazione a ogni passo;
- lo stato continua a cambiare durante il ciclo;
- il valore finale osservabile dipende dall'ultima iterazione.

La trascrizione piu' recente mostrava proprio un bug nato da qui:

- si legge un numero in `number`;
- poi si scrive `for number in range(...)`;
- dentro il ciclo `for` il nome `number` viene riutilizzato e sovrascrive il valore letto prima.

Questo e' uno dei motivi per cui conviene scegliere con attenzione i nomi delle variabili di iterazione.

Per esempio, meglio:

```python
numero = int(input())

for i in range(numero):
    ...
```

che:

```python
number = int(input())

for number in range(number):
    ...
```

Nel secondo caso il programma puo' anche "sembrare" funzionare in alcuni test, ma la logica diventa fragile e difficile da tracciare.

Se vogliamo vedere anche i valori intermedi, la lezione suggeriva semplicemente di stampare dentro il ciclo:

```python
for x in [24, -13, 8]:
    y = x + 1
    print(x, y)
```

In questo modo osserviamo l'evoluzione passo passo, non solo lo stato finale.

---

## `for`, testo e trasformazioni in-place

Nella seconda lezione il `for` veniva motivato soprattutto con un problema concreto:

- prendere un testo;
- trasformarlo in lista con `split()`;
- rendere minuscole tutte le parole.

Il punto didattico era che fare:

```python
parole[0] = parole[0].lower()
parole[1] = parole[1].lower()
parole[2] = parole[2].lower()
```

non scala:

- il codice diventa lungo;
- non sappiamo sempre quante parole ci saranno;
- aumentano gli errori di battitura;
- il programma non e' riusabile su testi diversi.

Il `for` nasce proprio per evitare questa ripetizione manuale.

### Quando serve anche la posizione

La trascrizione mostrava anche un caso un po' piu' sottile:

- a volte non basta avere il valore corrente;
- vogliamo anche sapere in quale posizione della lista stiamo lavorando;
- per esempio se vogliamo sovrascrivere l'elemento trasformato nella lista originale.

Una prima soluzione e':

- tenere una variabile `posizione`;
- inizializzarla a `0`;
- aggiornarla a ogni iterazione.

Poi si vede una forma piu' compatta con `enumerate()`.

---

## Esercizi assegnati sul `for`

Nei materiali assegnati compaiono diversi esercizi che si appoggiano direttamente a `for` e `range()`.

### Scansione di stringhe

Esempi:

- stampare una parola lettera per lettera;
- stampare una parola lettera per lettera indicando anche la posizione;
- leggere una parola e stampare solo le lettere in posizione pari.

Questi esercizi servono a far vedere che una stringa puo' essere trattata come una sequenza da attraversare.

### Conteggi e tabelle

Esempi:

- stampare la tabellina di un numero da `1` a `10`;
- stampare la tabellina con formatted strings;
- stampare triangoli e piramidi numeriche;
- stampare rettangoli pieni o vuoti, singoli o ripetuti.

Qui il nodo didattico e' distinguere bene:

- ciclo esterno;
- ciclo interno;
- contenuto di ogni riga;
- quando andare a capo e quando no.

### Pattern con cicli annidati

Gli esercizi sui rettangoli vuoti e sulle combinazioni:

```text
Pagina 1 Riga 1
Pagina 1 Riga 2
...
```

sono particolarmente utili per far capire che i cicli annidati non sono un trucco sintattico, ma un modello per combinare due dimensioni:

- righe e colonne;
- pagina e riga;
- figura e posizione.

---

## Soluzioni commentate emerse dagli esercizi

Le soluzioni svolte mostrano alcune idee che vale la pena fissare esplicitamente.

### `enumerate()` invece di `index()`

Per stampare lettere e posizioni, nei materiali compare prima una soluzione con contatore esplicito e poi una con:

```python
for posizione, carattere in enumerate(parola):
    print(carattere, posizione)
```

Questo e' utile anche per far vedere perche' usare `index()` dentro il ciclo e' una cattiva idea:

- restituisce la prima posizione trovata;
- quindi sbaglia quando ci sono lettere ripetute;
- inoltre rende il codice meno lineare.

La seconda lezione presentava `enumerate()` proprio come scorciatoia per ottenere insieme:

- posizione;
- valore corrente.

Esempio:

```python
for posizione, parola in enumerate(parole):
    parole[posizione] = parola.lower()
```

Cosi' non dobbiamo gestire a mano `posizione = posizione + 1`.

La forma compatta equivalente e':

```python
posizione += 1
```

che la trascrizione richiamava come abbreviazione comune di:

```python
posizione = posizione + 1
```

---

## Caratteri di escape e stampa

La seconda lezione si fermava anche su alcuni dettagli pratici delle stringhe che tornano utili quando si stampa o si prepara output.

### Virgolette dentro una stringa

Per stampare virgolette come caratteri interni, senza confonderle con quelle che delimitano la stringa, si usa il backslash:

```python
print("\"print\"")
```

### A capo e tabulazioni

Alcuni caratteri speciali richiamati in lezione:

| Sequenza | Effetto |
| --- | --- |
| `\\n` | nuova riga |
| `\\r\\n` | fine riga tipica di alcuni sistemi |
| `\\t` | tabulazione |

Esempio:

```python
print("hello\nworld")
```

produce:

```text
hello
world
```

Questo torna utile quando:

- vogliamo formattare output leggibili;
- leggiamo file e ci troviamo caratteri di fine riga dentro le stringhe;
- prepariamo testo tabellare da copiare o salvare.

### Costruire figure riga per riga

Negli esercizi su triangoli e rettangoli ricorre una strategia molto chiara:

- costruire una stringa di riga;
- stamparla;
- passare alla riga successiva.

Per esempio:

```python
stringa = "*"
for i in range(1, int(numero) + 1):
    print(stringa)
    stringa = stringa + "*"
```

Questo aiuta a capire che il `for` non serve solo a "ripetere", ma anche a costruire progressivamente uno stato osservabile.

### `for` e `while` nello stesso esercizio

Nella lezione e' emersa anche una situazione tipica di debugging:

- un `for` controlla quante volte eseguire una certa parte;
- un `while` interno aggiorna un'altra variabile di stato;
- il programma gira, ma non e' subito chiaro quale variabile stia governando che cosa.

Regola pratica:

- se usi sia `for` sia `while`, chiediti sempre quale dei due controlla la struttura principale del problema;
- evita di far dipendere due cicli diversi dalla stessa variabile se non e' strettamente necessario;
- quando il comportamento e' confuso, traccia a mano i valori a ogni iterazione.

La lezione dell'`11 marzo 2026` aggiungeva un esempio molto utile sui cicli annidati:

- il ciclo esterno controlla la riga;
- il ciclo interno costruisce il contenuto della riga;
- cambiare la variabile usata nella costruzione cambia il pattern stampato.

Per esempio, se per costruire la stringa usi `i`, la riga dipende dall'indice esterno; se usi `j`, dipende dall'indice interno.

Schema:

```python
for i in range(1, n + 1):
    stringa = ""
    for j in range(1, i + 1):
        stringa += str(i)
    print(stringa)
```

Variante:

```python
for i in range(1, n + 1):
    stringa = ""
    for j in range(1, i + 1):
        stringa += str(j)
    print(stringa)
```

La struttura dei cicli e' la stessa, ma il significato del pattern cambia.

Questo e' un ottimo esercizio per capire che:

- il controllo del flusso e la costruzione dell'output sono collegati;
- gli indici dei cicli annidati hanno ruoli diversi;
- un piccolo cambio nel corpo del ciclo puo' cambiare il problema che stiamo risolvendo.

### Liste temporanee e controllo finale

Un'altra soluzione svolta legge 5 parole, le salva in lista e poi confronta primo e ultimo elemento.

Anche se l'esercizio e' semplice, e' didatticamente utile perche' mette insieme:

- input ripetuto;
- accumulo in lista;
- accesso con indice positivo e negativo.

---

<a id="mod8-file"></a>
## File di testo: aprire, leggere, scorrere

Il terzo notebook storico introduceva i file come nuovo tipo di sorgente dati.

Esempio base:

```python
nome_file = "data/le_notti_bianche.txt"
file_incipit = open(nome_file, "r")
print(file_incipit.read())
file_incipit.close()
```

Nel corso conviene usare soprattutto la forma con `with`:

```python
nome_file = "data/le_notti_bianche.txt"

with open(nome_file, "r", encoding="utf-8") as file_incipit:
    for line in file_incipit:
        print(line)
```

La terza lezione trascritta insisteva molto sul fatto che leggere file non vuol dire imparare a memoria una formula magica, ma saper leggere la documentazione di `open()` e capire che cosa stiamo chiedendo al programma.

### Parametri essenziali di `open`

| Parametro | Significato |
| --- | --- |
| `file` | percorso del file |
| `mode` | modalita', tipicamente `r` o `w` |
| `encoding` | codifica del testo, spesso `utf-8` |

La spiegazione a voce aggiungeva tre osservazioni pratiche:

- `file` e' una stringa che rappresenta un percorso;
- il percorso puo' essere assoluto oppure relativo alla cartella da cui stiamo eseguendo lo script;
- `mode` decide se stiamo aprendo il file per leggere oppure per scrivere.

La trascrizione `08.srt` chiariva anche un punto concettuale importante:

- il nome del file e' solo una stringa;
- `open(...)` non ci restituisce "gia' il testo";
- ci restituisce un oggetto che permette di fare operazioni di input/output sul file aperto.

Per esempio:

```python
nome_file = "nuovofile.txt"
file_handler = open(nome_file, "r", encoding="utf-8")
print(file_handler)
file_handler.close()
```

L'oggetto stampato puo' sembrare tecnico, ma il punto didattico e' semplice:

- identifica un file aperto in una certa modalita';
- permette di leggerne il contenuto;
- va chiuso quando non serve piu'.

Esempio di percorso relativo:

```python
with open("data/le_notti_bianche.txt", "r", encoding="utf-8") as f:
    ...
```

funziona se il file si trova davvero in una cartella `data` sotto la cartella corrente.

### Idea chiave

Quando leggiamo da un file di testo, quello che otteniamo e' comunque testo:

- una stringa intera;
- una riga;
- una lista di righe.

Se ci servono numeri o booleani, dobbiamo convertirli.

Questo vale anche quando il file contiene solo numeri:

- Python li legge come testo;
- quindi poi va fatto il casting, per esempio con `int(...)` o `float(...)`.

### Documentazione e casi di errore

Nella trascrizione veniva mostrato anche un uso molto importante della documentazione ufficiale:

- guardare quali parametri prende `open()`;
- vedere quali sono i valori di default;
- controllare quali errori aspettarsi se il file non esiste o non puo' essere aperto.

Questo punto e' importante perche' sui file i problemi piu' comuni non sono "di Python in astratto", ma di:

- percorso sbagliato;
- permessi mancanti;
- nome file errato;
- codifica non compatibile.

---

<a id="mod8-terminale"></a>
## Esplorazione rapida da terminale su file di testo

La trascrizione `03.srt` introduceva una pratica molto utile anche se poi il lavoro finale verra' spesso fatto in Python:

- usare il terminale per ispezionare rapidamente un file;
- fare piccole trasformazioni;
- capire passo passo quale pipeline logica ci serve;
- salvare risultati intermedi quando il problema inizia a complicarsi.

L'esempio di partenza era un file di testo gia' leggermente preprocessato, in cui la punteggiatura era separata dalle parole da spazi. Questo rendeva piu' facile costruire una pipeline per trovare, per esempio, le parole piu' frequenti.

### Comandi utili

| Comando | Uso tipico |
| --- | --- |
| `cat file.txt` | mostra tutto il file |
| `less file.txt` | scorre il file una schermata alla volta |
| `head file.txt` | mostra l'inizio del file |
| `tail file.txt` | mostra la fine del file |
| `grep pattern file.txt` | filtra solo le righe che contengono un pattern |
| `cut ...` | seleziona campi o colonne |
| `sort` | ordina le righe |
| `uniq` / `uniq -c` | elimina duplicati consecutivi o li conta |
| `wc` | conta righe, parole o caratteri |

### Pipe: l'output di un comando diventa l'input del successivo

Il punto chiave della lezione e' la pipe `|`:

```bash
cat alice.txt | tr ' ' '\n'
```

Qui stiamo dicendo:

1. leggi il contenuto del file;
2. passa il risultato al comando successivo;
3. sostituisci gli spazi con un carattere di nuova riga.

Il risultato non e' ancora "l'analisi finale", ma una rappresentazione del testo che puo' essere piu' comoda da elaborare con gli strumenti successivi.

### Salvare risultati intermedi

Una buona pratica emersa molto chiaramente nella lezione e' questa:

- quando una pipeline cresce, conviene spesso salvare un risultato intermedio;
- cosi' non devi ripartire ogni volta da zero;
- puoi controllare meglio dove si introduce un errore.

Per esempio:

```bash
cat alice.txt | tr ' ' '\n' > parole.txt
sort parole.txt > parole-ordinate.txt
```

Dal punto di vista concettuale e' la stessa logica che poi ritroviamo in Python:

- trasformare l'input a piccoli passi;
- osservare lo stato intermedio;
- non trattare il programma come una scatola nera.

### `cat` non basta sempre

La lezione insisteva anche su un dettaglio pratico:

- `cat` va bene per file piccoli;
- su file lunghi e' spesso piu' utile `less`, `head` o `tail`.

Questo perche' il problema non e' solo "eseguire il comando", ma riuscire davvero a leggere il risultato.

### Perche' fare questo se poi useremo Python?

La risposta data a lezione era molto pragmatica:

- nella pratica reale, molte elaborazioni strutturate conviene poi farle in Python;
- ma la shell aiuta a capire il procedimento logico;
- permette di sperimentare rapidamente su file reali;
- costringe a ragionare in termini di input, output e trasformazioni successive.

Per questo le utility da terminale sono utili nel corso non come fine a se stesse, ma come ponte tra:

- file reali;
- trasformazioni testuali;
- progettazione di programmi piu' completi.

---

<a id="mod8-formati"></a>
## Dal file al testo tokenizzato

Il notebook 3 mostrava diversi esercizi sul passaggio:

1. aprire un file;
2. leggere il contenuto;
3. separare righe, frasi o parole;
4. costruire strutture dati utili.

Esempio con `split()`:

```python
parole = []

with open("data/le_notti_bianche.txt", "r", encoding="utf-8") as file_incipit:
    for line in file_incipit:
        line_split = line.strip().split()
        parole.extend(line_split)
```

Questo schema permette gia' di calcolare:

- numero di parole;
- parola piu' lunga;
- lunghezza media;
- vocabolario.

La terza lezione aggiungeva un'osservazione importante:

- `read()` e `readlines()` caricano molto contenuto in memoria;
- per file piccoli va bene;
- per corpus o testi grandi conviene spesso leggere riga per riga con `for line in file_handler`.

Questa scelta riduce il consumo di memoria e rende il codice piu' robusto su dati reali.

### `read()`, `readlines()` e iterazione

La lezione confrontava tre modi tipici di lavorare sul contenuto:

```python
contenuto = file_handler.read()
righe = file_handler.readlines()

for line in file_handler:
    ...
```

Differenza pratica:

- `read()` prende tutto il contenuto come una stringa unica;
- `readlines()` costruisce una lista di righe;
- `for line in file_handler` legge progressivamente una riga alla volta.

Per file piccoli possono andare bene tutte e tre.
Per testi piu' grandi, la lettura riga per riga e' spesso la soluzione piu' pulita.

La lezione dell'`11 marzo 2026` mostrava anche un quarto modo di ragionare sul problema:

- leggere tutto come una stringa;
- poi trasformare esplicitamente quella stringa con `split(...)`.

Per esempio:

```python
contenuto = file_handler.read()
righe = contenuto.split("\n")
```

oppure, se il file e' separato da tabulazioni:

```python
campi = contenuto.split("\t")
```

Questo e' utile per capire che:

- il file non "contiene gia' una lista";
- siamo noi a scegliere quale segmentazione applicare;
- newline e tab sono caratteri speciali che nel codice si scrivono come `\n` e `\t`.

### Esempi di esercizi del notebook 3

- stampare il file tutto su una riga;
- stampare una frase per riga;
- stampare una parola per riga;
- costruire il vocabolario del testo;
- confrontare due testi parola per parola.

### Testo non strutturato e pattern

La trascrizione `10.srt` aggiungeva un punto molto utile per chi lavora con testi reali:

- spesso il testo non e' gia' strutturato;
- non vogliamo cercare una parola sola;
- vogliamo cercare una **classe di stringhe**: date, numeri, parole con un prefisso, sequenze fatte in un certo modo.

Qui entrano in gioco le **espressioni regolari**.

In modo intuitivo, una regex e' una scrittura che descrive un pattern.
Per esempio:

- trovare tutte le parole che iniziano con `contro`;
- trovare tutte le sequenze di cifre;
- eliminare spazi ripetuti o altri caratteri indesiderati.

Il punto didattico della lezione non era memorizzare subito tutta la sintassi, ma capire l'idea:

> una regex non descrive una singola stringa, ma un insieme di stringhe con una certa forma.

### Quantificatori e classi di caratteri

Le prime due famiglie di strumenti introdotte a lezione erano:

- i **quantificatori**, che dicono quante volte puo' comparire qualcosa;
- le **classi di caratteri**, che dicono quali caratteri sono ammessi in uno slot.

Esempi tipici:

| Pattern | Intuizione |
| --- | --- |
| `a+` | una o piu' `a` consecutive |
| `a*` | zero o piu' `a` |
| `\\d+` | una o piu' cifre |
| `\\s+` | uno o piu' spazi bianchi |
| `contro.*` | una stringa che comincia con `contro` |

La lezione insisteva anche su un dettaglio pratico importante:

- molti strumenti ragionano riga per riga;
- il ritorno a capo e' spesso una barriera forte;
- su file diversi possono comparire fine-riga diversi, come `\\n` oppure `\\r\\n`.

Questo spiega perche' a volte una regex "giusta in teoria" non trova quello che ci aspettiamo su un file reale.

### Regex e Python

Nel corso basta arrivare a una lettura elementare di questo tipo:

```python
import re

testo = "Angela e' nata nel 1961 e vive a Bologna."
anni = re.findall(r"\\d+", testo)
print(anni)
```

Qui `findall` restituisce tutte le sottostringhe che rispettano il pattern.

Altri esempi vicini agli usi discussi a lezione:

```python
re.findall(r"contro\\w*", testo)
re.findall(r"\\d+", testo)
re.sub(r"\\s+", " ", testo)
```

Questi esempi bastano per fissare tre usi di base:

- estrarre;
- contare;
- sostituire.

### Quando conviene usare una regex

Regola pratica:

- se ti basta dividere sulle spaziature, `split()` resta spesso piu' semplice;
- se devi riconoscere forme piu' flessibili, la regex diventa utile;
- se il pattern richiede memoria strutturale piu' complessa, una regex potrebbe non bastare o diventare poco leggibile.

Questo si collega bene a un'idea gia' vista nel corso:

- scegliere lo strumento giusto dipende dalla forma del dato e dalla domanda che stiamo facendo;
- non ogni problema testuale va risolto con la stessa tecnica.

---

<a id="mod8-vocabolario"></a>
## Dal testo al vocabolario

Il notebook 3 conteneva una piccola sequenza di analisi testuale sul file delle *Notti bianche*:

1. lunghezza del testo;
2. parola piu' lunga;
3. lunghezza media delle parole;
4. vocabolario e sua dimensione.

Esempio di conteggio:

```python
numero_parole = 0

with open(nome_file, "r", encoding="utf-8") as file_incipit:
    for line in file_incipit:
        parole = line.strip().split()
        numero_parole += len(parole)
```

Esempio di parola piu' lunga:

```python
parola_lunga = ""

with open(nome_file, "r", encoding="utf-8") as file_incipit:
    for line in file_incipit:
        for parola in line.strip().split():
            if len(parola) > len(parola_lunga):
                parola_lunga = parola
```

Questi esempi sono importanti perche' mostrano come combinare:

- file;
- stringhe;
- liste;
- `for`;
- confronti e accumuli.

---

## Scrivere su un file

Il notebook 3 mostrava anche la forma base di scrittura:

```python
nome_file = "data/file_in_output.txt"

with open(nome_file, "w", encoding="utf-8") as file_output:
    print("hello world", file=file_output)
```

Attenzione pratica:

- se apri in modalita' `w`, il contenuto precedente viene sovrascritto;
- il nome del file e' sempre una stringa che rappresenta un percorso.

La terza lezione metteva un avviso molto netto su questo punto:

> se il file esiste gia', aprirlo in `w` lo sostituisce senza chiedere conferma

Quindi scrivere su file richiede attenzione doppia rispetto alla lettura.

La trascrizione mostrava anche un'idea molto utile:

- `print(...)` di default scrive sullo **standard output**;
- cioe' sul canale che il terminale ci mostra a schermo;
- ma con `file=...` possiamo mandare lo stesso output in un file aperto.

Esempio:

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

Questo e' interessante perche' unifica due casi che sembrano diversi:

- stampare nel terminale;
- scrivere su file.

In entrambi i casi stiamo producendo output testuale; cambia solo la destinazione.

La lezione metteva anche a confronto due strategie diverse:

1. usare il sistema operativo per ridirigere l'output:

```bash
python3 script.py > output.txt
```

2. aprire esplicitamente un file di output in Python:

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

Le due strade servono a scopi simili, ma non sono la stessa cosa:

- nel primo caso e' la shell che intercetta lo standard output;
- nel secondo caso e' il programma Python che decide dove scrivere.

Quando il programma cresce, la seconda soluzione e' spesso piu' controllabile.

### Perche' usare `with`

Un altro punto esplicitato nella trascrizione:

- senza `with` dobbiamo ricordarci di chiudere il file a mano;
- se ci dimentichiamo, soprattutto in scrittura, possiamo creare comportamenti confusi o perdere controllo sul flusso;
- `with` automatizza apertura e chiusura del file nel blocco giusto.

Per questo nel corso conviene trattare:

```python
with open(...):
    ...
```

come forma standard.

### Un file letto una volta non si "riavvolge" da solo

La trascrizione mostrava anche che, se scorriamo un file fino in fondo, poi non basta rieseguire lo stesso ciclo sullo stesso oggetto aperto per leggerlo di nuovo dall'inizio.

In pratica:

- il puntatore di lettura avanza;
- quando arriva in fondo, il file risulta esaurito;
- per rileggere da capo conviene riaprirlo.

Anche questo e' un buon motivo per preferire blocchi `with` separati per operazioni distinte.

---

## File, `strip()` e conversione dei valori

La terza lezione lavorava anche su un esercizio semplice ma molto istruttivo:

- leggere un file con un numero per riga;
- sommare tutti i numeri presenti.

Il punto didattico non era la somma in se', ma gli ostacoli reali:

- ogni riga letta e' una stringa;
- puo' contenere il carattere di fine riga;
- il numero puo' essere intero o decimale.

Per questo diventano utili insieme:

- `line.strip()` per togliere spazi e fine riga ai bordi;
- `int(...)` oppure `float(...)` per convertire il testo nel tipo numerico giusto.

Schema tipico:

```python
somma = 0.0

with open("dati.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        somma = somma + float(line.strip())
```

Questo esercizio e' importante perche' mette insieme:

- file;
- stringhe;
- caratteri invisibili come il ritorno a capo;
- casting;
- accumulo in una variabile.

### Formatted strings per output leggibile

Nella stessa lezione comparivano anche le formatted strings come strumento pratico per rendere leggibili risultati e colonne.

Esempio semplice:

```python
parola = "alice"
frequenza = 145

print(f"{parola}\t{frequenza}")
```

oppure, se vogliamo colonne piu' regolari:

```python
print(f"{parola:20}{frequenza}")
```

Il dettaglio sintattico non e' la cosa piu' importante all'inizio. Il punto didattico e' questo:

- quando produciamo output strutturato, la leggibilita' conta;
- formattare bene l'output rende piu' facile controllare se il programma sta facendo la cosa giusta.

### Input e output da riga di comando

La trascrizione chiudeva con un altro passaggio molto utile: non fissare dentro il codice un solo file di input e un solo file di output.

Invece di scrivere sempre:

```python
nome_file = "alice.txt"
```

si puo' far arrivare il nome del file dall'esterno, per esempio tramite `sys.argv`.

Schema minimo:

```python
import sys

nome_input = sys.argv[1]
nome_output = sys.argv[2]
```

Questo permette di riusare lo stesso programma su file diversi senza modificarne il sorgente ogni volta.

Dal terminale:

```bash
python3 frequenze.py alice.txt output.txt
```

La lezione insisteva giustamente sul fatto che:

- `input()` legge una stringa interattiva;
- `sys.argv` legge i parametri con cui il programma e' stato lanciato;
- sono due meccanismi diversi e vanno scelti in base al tipo di interazione che vogliamo.

La stessa trascrizione aggiungeva un passaggio importante:

- `sys.argv` e' una lista;
- in posizione `0` c'e' il nome dello script Python;
- da `1` in poi ci sono i parametri passati da terminale.

Quindi, se vogliamo lavorare su molti file, possiamo prendere una sottolista:

```python
files = sys.argv[1:]

for nome_file in files:
    ...
```

Questo permette di scrivere programmi che funzionano su uno o piu' file senza modificare il sorgente.

### Nota sulla codifica

Qui teniamo solo il punto generale che emergeva dalla lezione:

- se un file mostra caratteri strani o illeggibili, uno dei possibili colpevoli e' l'encoding;
- oggi `utf-8` e' spesso la scelta giusta;
- ma quando qualcosa non torna, la codifica e' una delle prime cose da controllare.

---

## Esercizi assegnati su file e trasformazioni

Dagli esercizi assegnati emergono anche alcune trasformazioni molto utili per questo modulo:

1. leggere un file e produrre un secondo file con tutte le righe in minuscolo e senza righe vuote;
2. leggere un file riga per riga e copiare solo le righe che contengono una certa parola;
3. contare righe, parole e caratteri di un file;
4. confrontare il vocabolario di due file.

Questi esercizi mostrano bene come combinare:

- lettura sequenziale;
- stringhe;
- liste e set;
- scrittura di file in output.

---

## Escape nelle stringhe stampate

Nel notebook 2 compariva anche un piccolo approfondimento pratico sulle stringhe usate nel `print`:

| Sequenza | Significato |
| --- | --- |
| `\"` o `\'` | virgolette dentro una stringa |
| `\n` | nuova riga |
| `\t` | tabulazione |

Esempi:

```python
print("\"")
print("hello\nworld")
print("hello\tworld")
```

Questo non e' il cuore del modulo, ma e' molto utile quando i cicli producono output strutturato.

---

## Esercizi recuperati dal notebook

### Base

1. stampa i numeri da 0 a 9;
2. stampa i numeri da 25 a 34;
3. stampa 10 volte la stringa `"Adoro programmare in Python!"`.

### Filtri e condizioni

4. stampa da 1 a 100 saltando i multipli di 5;
5. stampa da 1 a 100 saltando i multipli di 3 e 5;
6. stampa da 1 a 100 saltando i multipli di 3 e 5, ma includendo quelli multipli di entrambi.

### Stringhe e liste

7. stampa i caratteri in posizione dispari di una stringa;
8. scrivi una funzione che restituisce la lista dei numeri da `n` a `m - 1`;
9. scrivi una funzione che restituisce i numeri pari da `N` a `0`;
10. data una stringa, restituisci solo le consonanti.

### Output strutturato

11. stampa un quadrato di `+` di lato `n`;
12. stampa triangoli e triangoli invertiti;
13. generalizza a rettangoli e trapezi con base `n` e altezza `m`.

### Liste

14. controlla se una lista contiene la parola `"linguistica"`;
15. restituisci la posizione di `"linguistica"` oppure `-1`;
16. inserisci `"linguistica"` in posizione `p`;
17. unione senza ripetizioni di due liste;
18. intersezione di due liste;
19. date una lista e una parola, stampa tutte le occorrenze insieme al contesto vicino.

### File e testi

20. leggi un file di numeri e calcolane la somma;
21. leggi un file testuale e stampalo su una sola riga;
22. stampa le parole di un testo una per riga;
23. costruisci il vocabolario di un testo;
24. confronta le parole presenti in due testi diversi.

---

## Riepilogo

Dal notebook 2 questo modulo recupera il nucleo dell'iterazione con `for`:

- motivazione del costrutto;
- sintassi e semantica;
- uso di `range()`;
- tracciamento della variabile di iterazione;
- lettura e scrittura di file di testo;
- prime analisi sul vocabolario di un testo;
- esercizi graduali su numeri, stringhe, pattern testuali, liste e file.
