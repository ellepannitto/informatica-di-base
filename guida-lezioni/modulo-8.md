# Modulo 08 · File, Dizionari e Set

## Autovalutazione

- Sai distinguere i tre modi per far arrivare dati a un programma?
- Sai usare `sys.argv` per leggere argomenti da riga di comando?
- Sai aprire, leggere e scrivere file con `open()` e `with`?
- Sai usare i dizionari per associare chiavi e valori?
- Sai contare frequenze con un dizionario?
- Sai iterare su chiavi, valori e coppie chiave-valore?
- Sai usare i set come insiemi di elementi unici?
- Sai distinguere lista, dizionario e set e scegliere la struttura giusta?

## Tre modi per far arrivare dati a un programma

Fino a questo punto i programmi hanno ricevuto dati in due modi: scritti direttamente nel codice oppure letti con `input()`.

Normalmente però:

- i dati sono salvati in file sul disco (o su altri sistemi di archiviazione, e.g., il cloud)
- oppure potrebbero arrivare come parametri tramite riga di comando.

## `sys.argv`: argomenti da riga di comando

Fino a questo momento abbiamo usato la riga di comando per invocare l'interprete Python e passargli il file contenente codice sorgente, delegando al codice la gestione dell'input.

```bash
python3 script.py
```

Possiamo però anche sfruttare la riga di comando per passare direttamente dei valori all'interprete.

```bash
python3 script.py ciao 42
```

All'interno del programma, i valori `ciao` e `42` sono accessibili tramite `sys.argv`, una lista che Python riempie automaticamente. Per usarla bisogna importare il modulo `sys`:

```python
import sys

print(sys.argv)   # ['script.py', 'ciao', '42']
```

- `sys.argv` è una variabile di tipo **list**;
- `sys.argv[0]` è il nome dello script;
- `sys.argv[1]` e i successivi sono i valori passati dall'utente, come **stringhe**.

Esempio:

```python
import sys

nome = sys.argv[1]
print("Ciao,", nome)
```

```bash
python3 script.py Ludovica
# Ciao, Ludovica
```

### Esercizi

1. Scrivi un programma che riceve due numeri da riga di comando e stampa la loro somma.
   ```
   python3 somma.py 3 7
   10
   ```

2. Scrivi un programma che riceve una parola da riga di comando e stampa quante lettere ha.
   ```
   python3 lunghezza.py banana
   6
   ```

3. Scrivi un programma che riceve una lista di numeri da riga di comando e stampa il massimo.
   ```
   python3 massimo.py 4 7 2 9 1
   9
   ```

4. Scrivi un programma che riceve una parola da riga di comando e la stampa al contrario.
   ```
   python3 rovescia.py ciao
   oaic
   ```

5. Scrivi un programma che riceve una serie di parole da riga di comando e, per ognuna di esse, stampa se è palindroma o meno.
   ```
   python3 palindromo.py ciao radar pizza anna
   ciao - no
   radar - sì
   pizza - no
   anna - sì
   ```

## E quindi i file?

`sys.argv` e `input()` vanno bene per dati semplici, ma hanno due limiti:

- i dati sono **volatili**: spariscono quando il programma finisce;
- i dati sono **piccoli**: non è pratico passare cento numeri da riga di comando.

Immagina di voler analizzare i voti di tutti gli studenti di un corso:

```
Sandra Rossi   27
Matteo Bianchi 19
Giuseppe Verdi  30
Antonella Ferrari   18
...
```

Questi dati sono:
- **strutturati** (ogni riga ha lo stesso formato: nome e cognome nella prima colonna e voto nella seconda),
-  **persistenti** (esistono indipendentemente dal programma)
-  (potenzialmente) **grandi** (possono essere migliaia di righe).

Tipicamente, sono dati che manteniamo su dei file.

## Dove sono i file: Il filesystem e il filepath

Il **filesystem** è la struttura ad albero con cui il sistema operativo organizza i file su disco.
Ogni file e ogni cartella ha una posizione unica nell'albero, descritta dal suo **percorso** (filepath).

```
/                          ← radice (root)
├── home/
│   └── ludovica/
│       ├── script.py
│       └── dati/
│           └── voti.txt
└── usr/
    └── bin/
```

### Percorso assoluto

Parte dalla radice `/` e descrive il percorso completo:

```
/home/ludovica/dati/voti.txt
```

Funziona indipendentemente da dove ci si trova nel filesystem.

### Percorso relativo

Parte dalla **cartella corrente** (la cartella da cui si lancia lo script):

```
dati/voti.txt       ← entra nella sottocartella dati/
../altro/file.txt   ← risale di un livello con ..
voti.txt            ← nella stessa cartella dello script
```

La posizione del percorso relativo dipende da dove si trova lo script nel filesystem. Ecco un esempio:

```
/home/ludovica/
├── progetto/
│   ├── script.py          ← lo script è qui
│   └── dati/
│       └── voti.txt
└── altro/
    └── note.txt
```

Se si lancia lo script con:

```bash
cd /home/ludovica/progetto
python3 script.py
```

allora la **cartella corrente** è `/home/ludovica/progetto/` e i percorsi relativi si interpretano così:

```python
open("dati/voti.txt")       # → /home/ludovica/progetto/dati/voti.txt  ✓
open("voti.txt")            # → /home/ludovica/progetto/voti.txt        ✗ non esiste
open("../altro/note.txt")   # → /home/ludovica/altro/note.txt           ✓
```

Se invece si lancia da una cartella diversa:

```bash
cd /home/ludovica
python3 progetto/script.py
```

la cartella corrente diventa `/home/ludovica/` e gli stessi percorsi puntano a posti diversi:

```python
open("dati/voti.txt")       # → /home/ludovica/dati/voti.txt           ✗ non esiste!
```

Per questo motivo è importante **lanciare lo script dalla cartella giusta**.

### Recap dei comandi bash utili

| Comando                   | Significato                                           |
| ------------------------- | ----------------------------------------------------- |
| `pwd`                     | stampa la cartella corrente (print working directory) |
| `ls`                      | elenca i file nella cartella corrente                 |
| `ls dati/`                | elenca i file nella sottocartella `dati/`             |
| `cd dati/`                | entra nella cartella `dati/`                          |
| `cd ..`                   | risale di un livello                                  |
| `cd ~`                    | torna alla cartella home                              |
| `mkdir nome`              | crea una nuova cartella                               |
| `cp origine destinazione` | copia un file                                         |
| `mv origine destinazione` | sposta o rinomina un file                             |
| `rm file`                 | elimina un file (irreversibile)                       |
| `cat file`                | stampa il contenuto di un file                        |
| `python3 script.py`       | esegue uno script Python                              |

La cartella corrente è importante: quando si usa un percorso relativo in Python (es. `open("dati/voti.txt")`), Python lo interpreta rispetto alla cartella da cui è stato lanciato lo script, non rispetto alla cartella dove si trova il file `.py`.

### Esercitazione: navigare il filesystem

Apri un terminale e segui questi passi uno alla volta.

**1. Dove sono?**

```bash
pwd
```

Leggi il percorso assoluto che viene stampato. È la tua cartella home.

**2. Cosa c'è qui?**

```bash
ls
```

Osserva i file e le cartelle presenti.

**3. Crea una struttura di cartelle**

```bash
mkdir esercizi
mkdir esercizi/modulo8
mkdir esercizi/modulo8/dati
```

**4. Verifica la struttura**

```bash
ls esercizi/
ls esercizi/modulo8/
```

**5. Entra nella cartella di lavoro**

```bash
cd esercizi/modulo8
pwd
```

Il percorso stampato ora finisce con `esercizi/modulo8`. Questa è la tua nuova cartella corrente.

**6. Crea un file di testo**

```bash
echo "Sandra,Rossi,27" > dati/studenti.txt
echo "Matteo,Bianchi,19" >> dati/studenti.txt
echo "Giuseppe,Verdi,30" >> dati/studenti.txt
```

(`>` sovrascrive, `>>` aggiunge in coda.)

**7. Controlla il contenuto**

```bash
cat dati/studenti.txt
```

**8. Torna alla home**

```bash
cd ~
pwd
```

Nella prossima sezione scaricheremo dalla repository git uno script già pronto che legge i file di dati — e vedremo cosa succede se lo si lancia dalla cartella sbagliata.

## Cos'è un file per Python

Un file è una sequenza di dati salvata su disco.
Per Python, un file è identificato univocamente dal suo **percorso** (path): una stringa che descrive dove si trova nel filesystem.

```python
"dati.txt"                # nella stessa cartella dello script
"data/testo.txt"          # nella sottocartella data/
"../esercizi/testo.txt"   # risale di un livello, poi entra in esercizi/
"/home/utente/note.txt"   # percorso assoluto
```

Per lavorare con un file, Python crea un oggetto speciale chiamato **file handler** (o file object): una variabile che rappresenta il canale aperto tra il programma e il file su disco. Attraverso questo handler si legge e si scrive; il file fisico non viene mai manipolato direttamente.

```python
handler = open("dati.txt", "r", encoding="utf-8")
# handler è ora il canale verso il file
```

## La funzione `open()`

`open()` è una funzione che riceve il percorso di un file e restituisce un **file handler**: l'oggetto attraverso cui leggere o scrivere il file.

```python
open(percorso, mode, encoding)
```

### Parametro `percorso`

Una **stringa** con il path del file.
Può essere relativo (rispetto alla cartella da cui si lancia lo script) o assoluto.

### Parametro `mode`

Controlla cosa si può fare con il file una volta aperto:

| Valore | Significato                                                                          |
| ------ | ------------------------------------------------------------------------------------ |
| `"r"`  | lettura (default); il file deve esistere                                             |
| `"w"`  | scrittura; crea il file se non esiste, **sovrascrive** se esiste                     |
| `"a"`  | scrittura in coda (append); crea il file se non esiste, aggiunge alla fine se esiste |

### Parametro `encoding`

Su disco un file è una sequenza di **byte**.
Un byte è formato da 8 **bit**, ciascuno dei quali può valere 0 o 1:

```
  bit:   1  0  1  1  0  1  0  0
         ^                     ^
       (più significativo)   (meno significativo)

  valore decimale: 128 + 0 + 32 + 16 + 0 + 4 + 0 + 0 = 180
  range possibile: 0 … 255  (2⁸ = 256 valori)
```

L'encoding è la tavola di corrispondenza che dice come trasformare quei byte in caratteri leggibili.

### ASCII

Il primo encoding standardizzato è **ASCII** (1963). Usa 7 bit per carattere, quindi può rappresentare solo 128 simboli: le lettere inglesi maiuscole e minuscole, le cifre, la punteggiatura e alcuni caratteri di controllo.

```
Dec  Char       Dec  Char       Dec  Char
 65   A          97   a          48   0
 66   B          98   b          49   1
 67   C          99   c          50   2
 32   (spazio)   46   .          10   \n (newline)
```

ASCII è sufficiente per l'inglese, ma non ha lettere accentate, caratteri greci, arabi, cinesi, emoji, ecc.

### Il problema: 256 valori non bastano

Con un byte si possono rappresentare 256 valori (0–255). Nel corso degli anni ogni paese ha definito il proprio modo di usare i valori 128–255 per le proprie lettere speciali: Latin-1 per l'Europa occidentale, cp1251 per il cirillico, ecc. Il risultato è che lo stesso byte  `11100000` (224 in decimale) significa `à` in Latin-1 e `а` (a cirillica) in cp1251.

### UTF-8

**UTF-8** risolve il problema: è un encoding a **lunghezza variabile** che può rappresentare tutti i circa 150000 caratteri dello standard Unicode.

- I caratteri ASCII (0–127) occupano **1 byte**, identico a ASCII — retrocompatibile.
- I caratteri latini estesi (lettere accentate) occupano **2 byte**.
- I caratteri di altri alfabeti occupano **3 byte**.
- Gli emoji e i simboli rari occupano **4 byte**.

Esempi:

```
Carattere   byte (un gruppo per byte, in binario)
'A'         01000001
'à'         11000011  10100000
'è'         11000011  10101000
'ù'         11000011  10111001
'€'         11100010  10000010  10101100
'😀'        11110000  10011111  10011000  10000000
```

Lo stesso file letto con encoding sbagliato produce caratteri incomprensibili. Per esempio, la stringa `"città"` salvata in UTF-8 e letta come Latin-1 diventa `"cittÃ "` perché i due byte `C3 A0` di `à` vengono interpretati come due caratteri Latin-1 separati.

Usare sempre `encoding="utf-8"` sui file che si creano. Quando si legge un file prodotto da altri e si vedono caratteri strani, è probabile che l'encoding sia sbagliato.

## Valore restituito

`open()` restituisce un oggetto di tipo **file handler**.
Non è una stringa né una lista: è un canale verso il file, e i suoi metodi (`read()`, `readlines()`, `write()`, …) permettono di trasferire dati.

Il file handler è un **iterabile**: supporta il `for`, che consegna una riga alla volta.

```python
for line in file_in:      # OK: itera riga per riga
    print(line)
```

Non supporta però l'accesso diretto per posizione:

```python
file_in[0]    # ERRORE: i file handler non sono indicizzabili
```

Per accedere a una riga specifica bisogna prima caricare tutto il contenuto in una lista con `readlines()`, e poi indicizzare quella.

```python
nome_file = "data/testo.txt"
file_in = open(nome_file, "r", encoding="utf-8")
print(file_in.readlines())
file_in.close()
```

## `with` e la gestione sicura dei file

Aprire un file non basta: bisogna anche ricordarsi di chiuderlo.

Perché?

- Il sistema operativo tiene un limite al numero di file che un processo può tenere aperti contemporaneamente. Se un programma apre molti file senza mai chiuderli, a un certo punto ottiene un errore.
- Quando si **scrive** su un file, Python non invia i dati subito al disco: li accumula in un **buffer** in memoria per efficienza. La chiusura del file svuota il buffer e garantisce che tutti i dati vengano effettivamente salvati. Un programma che termina senza chiudere i file di output può perdere le ultime righe scritte.

`with` rende questa gestione automatica: il file viene chiuso al termine del blocco indentato, anche se si verifica un errore nel mezzo.

```python
with open("data/testo.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        print(line)
```

Quando Python esegue un blocco `with`:

1. apre la risorsa;
2. la rende disponibile tramite il nome (nome di variabile) dopo `as`;
3. esegue il blocco indentato;
4. alla fine chiude correttamente la risorsa.

## Leggere un file

Tre strategie principali:

```python
# tutto il contenuto in una stringa
contenuto = file_in.read()

# lista di righe
righe = file_in.readlines()

# riga per riga (il più comune)
for line in file_in:
    ...
```

### `strip()` e `split()` sui dati letti

Le righe lette da file contengono spesso caratteri indesiderati ai bordi (spazi, fine riga). Prima di usare i dati conviene ripulirli:

```python
somma = 0.0

with open("dati.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        somma = somma + float(line.strip())
```

Per segmentare una riga in campi:

```python
with open("dati.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        campi = line.strip().split(",")
```

## Ottenere i file di dati: git e GitHub

I file di esempio per questi esercizi si trovano in una **repository git** su GitHub. Git è un sistema di **controllo versione**: tiene traccia di tutte le modifiche ai file nel tempo e permette a più persone di lavorare sullo stesso progetto.

GitHub è una piattaforma web che ospita repository git e le rende accessibili a chiunque.

### Clonare una repository

Per scaricare una repository sul proprio computer si usa il comando `clone`:

```bash
git clone https://github.com/ellepannitto/informatica-di-base-dati.git
```

Questo crea una cartella locale `informatica-di-base-dati/` con i file di esempio e uno script di prova:

```
informatica-di-base-dati/
├── dati/
│   ├── voti.txt
│   ├── voti_materie.txt
│   ├── numeri.txt
│   └── testo.txt
└── leggi.py
```

### Eseguire lo script dalla cartella giusta

Entra nella cartella clonata e lancia lo script:

```bash
cd informatica-di-base-dati
python3 leggi.py
```

Lo script legge `dati/voti.txt` (percorso relativo rispetto alla cartella corrente) e stampa nome, cognome e voto di ogni studente.

### Cosa succede se lanci lo script dalla cartella sbagliata?

```bash
cd ..
python3 informatica-di-base-dati/leggi.py
```

Ottieni un `FileNotFoundError` perché il percorso relativo `dati/voti.txt` è ora interpretato rispetto alla cartella genitore, dove quella sottocartella non esiste. Per farlo funzionare bisogna rientrare nella cartella giusta:

```bash
cd informatica-di-base-dati
python3 leggi.py
```

### Aggiornare i file

Se i file del repository vengono aggiornati in seguito, per scaricare le ultime versioni basta eseguire dalla cartella del progetto:

```bash
git pull
```

## Esercizi

1. Apri un file di testo e stampa ogni riga così com'è.
2. Apri un file di testo e stampa solo le righe non vuote.
3. Apri un file di testo e stampa ogni riga in maiuscolo.
4. Apri un file di testo e stampa il numero di righe che contiene.
5. Apri un file che contiene un numero per riga e stampa ogni numero moltiplicato per 2.

Considera un file `voti.txt` con il formato seguente (nome, cognome, voto separati da virgola):

```
Sandra,Rossi,27
Matteo,Bianchi,19
Giuseppe,Verdi,30
Antonella,Ferrari,18
Luigi,Esposito,24
```

1. Leggi il file e stampa il nome e cognome di ogni studente (ignora il voto).
2. Leggi il file e stampa il nome e cognome degli studenti che hanno superato l'esame (voto >= 18).
3. Leggi il file e stampa la media dei voti.
4. Leggi il file e stampa il nome e cognome dello studente con il voto più alto.
5.  Leggi il file e stampa quanti studenti hanno preso 30.
6.  Leggi un file testuale e stampalo su una sola riga.
7.  Stampa le parole di un testo una per riga.
8.  Conta righe, parole e caratteri di un file.

## Scrivere su un file

### Redirezione della shell

Il modo più semplice per salvare l'output di un programma su file è usare la redirezione della shell, senza modificare il codice Python:

```bash
python3 script.py > output.txt
```

Il simbolo `>` dice alla shell di intercettare tutto ciò che il programma stampa su schermo e di scriverlo nel file indicato. Il programma Python non sa che l'output va su file: continua a usare `print()` normalmente.

### Apertura in modalità scrittura

Quando è il programma a dover decidere dove o cosa scrivere, si usa `open()` con mode `"w"`:

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

- `print(..., file=file_output)` scrive nel file invece che sullo schermo;
- `"w"` crea il file se non esiste e **sovrascrive** il contenuto se esiste già.

## Esercizi

1. Scrivi un programma che legge il nome di un file di output da `sys.argv` e scrive al suo interno i numeri da 1 a 10, uno per riga.

2. Scrivi un programma che legge da `sys.argv` il nome di un file di input e il nome di un file di output, e copia il contenuto del primo nel secondo tutto in maiuscolo.

3. Scrivi un programma che chiede all'utente un nome di file tramite `input()` e scrive in quel file le prime 5 righe di testo digitate dall'utente.
   ```
   Nome del file di output: appunti.txt
   Riga 1: ciao
   Riga 2: questo è un test
   Riga 3: terza riga
   Riga 4: quarta
   Riga 5: fine
   ```

4. Scrivi un programma che legge dall'utente una sequenza di parole (una per riga, fino a riga vuota) e le scrive su un file il cui nome è passato da `sys.argv`.

5. Leggi `dati/voti.txt` e scrivi due file separati: `sufficienti.txt` con le righe degli studenti che hanno superato l'esame (voto >= 18) e `insufficienti.txt` con gli altri.
   ```
   python3 filtra.py dati/voti.txt sufficienti.txt insufficienti.txt
   ```

6. Leggi `dati/voti.txt` e distribuisci casualmente ogni riga in uno di due file usando `random.random()`: se il valore estratto è minore di 0.5 la riga va in `parte1.txt`, altrimenti in `parte2.txt`. Stampa quante righe sono finite in ciascun file.
   ```python
   import random
   # random.random() restituisce un float tra 0.0 e 1.0
   ```

7. Leggi `dati/testo.txt` e scrivi in `brevi.txt` solo le righe con meno di 50 caratteri e in `lunghe.txt` solo quelle con 50 o più caratteri.

8. Leggi `dati/numeri.txt` e scrivi in `positivi.txt` i numeri positivi e in `negativi.txt` quelli negativi (ignora gli zeri).

## Dati strutturati: Dizionari

Immaginiamo di avere un file con tutti i voti di tutti gli studenti per tutte le materie:

```
Sandra,Rossi,matematica,28
Matteo,Bianchi,matematica,22
Sandra,Rossi,informatica,30
Sandra,Rossi,linguistica,27
Matteo,Bianchi,informatica,19
Matteo,Bianchi,linguistica,25
...
```

Vogliamo calcolare la media dei voti per ogni studente. Il problema è che ogni studente compare su più righe: dobbiamo raccogliere tutti i suoi voti mentre leggiamo il file, e poi calcolare la media alla fine.

Con una lista non possiamo farlo facilmente: la lista non ha un modo diretto per rispondere alla domanda "dammi tutti i voti di Sandra Rossi". Dovremmo scorrere tutta la lista ogni volta.

Ci serve una struttura che associ un **nome** (la chiave) a una **lista di voti** (il valore). Questa struttura è il **dizionario**.

```python
voti = {
    "Sandra Rossi":  [28, 30, 27],
    "Matteo Bianchi": [22, 19, 25],
}
```

Con questa struttura, aggiungere un voto è immediato:

```python
studente = "Sandra Rossi"
if studente not in voti:
    voti[studente] = []
voti[studente].append(28)
```

E calcolare la media di ogni studente diventa un semplice ciclo:

```python
for studente, lista_voti in voti.items():
    media = sum(lista_voti) / len(lista_voti)
    print(studente, media)
```

## Dizionari

Un dizionario si scrive tra `{` e `}`. Ogni elemento è una coppia `chiave: valore` separata da virgola:

```python
{}                                       # dizionario vuoto
{"the": 156, "cat": 20, "is": 80}       # chiavi stringa, valori interi
{"lazio": "roma", "campania": "napoli"} # chiavi e valori stringa
{"molise": ["campobasso", "isernia"]}   # valore che è una lista
```

Per creare un dizionario vuoto e popolarlo un elemento alla volta si usa l'assegnazione con `[]`:

```python
d = {}                 # dizionario vuoto
d["chiave"] = valore   # aggiunge (o aggiorna) la coppia chiave → valore
```

La chiave tra `[]` deve essere un valore **immutabile** (stringa, intero, …). Il valore a destra può essere qualunque espressione Python. Se la chiave esiste già, il valore viene **sovrascritto**:

```python
d = {}
d["gatto"] = 1
d["gatto"] = 5   # ora d["gatto"] vale 5, non 1
```

### Semantica

Un dizionario associa una **chiave** a un **valore**:

- la chiave deve essere **immutabile** (stringa, intero, tupla) — non si possono usare liste o altri dizionari come chiavi;
- il valore può essere di **qualunque tipo**, incluse liste o altri dizionari;
- l'accesso avviene tramite la chiave, non tramite la posizione.

Se si accede a una chiave che non esiste si ottiene un `KeyError`:

```python
d = {"gatto": 1}
d["cane"]   # KeyError: 'cane'
```

Per evitarlo si usa prima `in`:

```python
if "cane" in d:
    print(d["cane"])
```

### Lista o dizionario?

Una lista può contenere le stesse informazioni, ma il significato dei campi resta implicito nelle posizioni:

```python
persona_lista = ["Ludovica", "Pannitto", 30]
```

Con un dizionario la struttura diventa più leggibile e meno fragile:

```python
persona = {"nome": "Ludovica", "cognome": "Pannitto", "eta": 30}
```

## Operazioni fondamentali

| Operazione       | Sintassi     |
| ---------------- | ------------ |
| Accesso          | `D[k]`       |
| Aggiornamento    | `D[k] = v`   |
| Appartenenza     | `k in D`     |
| Numero di chiavi | `len(D)`     |
| Chiavi           | `D.keys()`   |
| Valori           | `D.values()` |
| Coppie           | `D.items()`  |

## Iterazione sui dizionari

Iterare sulle chiavi (default):

```python
for chiave in dizionario:
    print(chiave, dizionario[chiave])
```

Iterare su coppie chiave-valore con `items()`:

```python
for chiave, valore in dizionario.items():
    print(chiave, valore)
```

`items()` restituisce coppie `(chiave, valore)` che Python spacchetta direttamente nelle due variabili del `for`.

## Esercizi

1. Dato il seguente dizionario:
   ```python
   traduzione = {"gatto": "cat", "cane": "dog", "topo": "mouse", "uccello": "bird"}
   ```
   Scrivi un programma che chiede all'utente una parola italiana e stampa la traduzione in inglese. Se la parola non è nel dizionario, stampa `Parola non trovata`.

2. Scrivi un programma `conta_lettere.py` che prende come parametro una parola e conta quante volte compare ciascuna lettera usando un dizionario. Esempio:
   ```
   python3 conta_lettere.py banana
   b: 1
   a: 3
   n: 2
   ```

3. Scrivi un programma che legge una stringa dall'input e stampa la frequenza di ogni lettera, ordinata dalla più frequente alla meno frequente.

4. Scrivi un programma che legge dall'input una serie di parole (una per riga, fino a riga vuota) e stampa quante volte è stata inserita ciascuna parola distinta.

5. Leggi `testo.txt` e conta la frequenza di ogni parola. Stampa le 10 parole più frequenti con il loro conteggio.

6. Leggi `testo.txt` e stampa la parola più lunga e la parola più corta (escludi le parole di un solo carattere).

7. Leggi `voti.txt` (formato `nome,cognome,voto`) e costruisci un dizionario `cognome → lista di voti`. Stampa per ogni cognome la media dei voti.

8. Leggi `voti_materie.txt` (formato `nome,cognome,materia,voto`) e stampa, per ogni studente, la materia in cui ha preso il voto più alto.

9. Leggi `voti_materie.txt` e costruisci un dizionario `materia → voto medio`. Stampa le materie ordinate dal voto medio più alto al più basso.

10. Scrivi un programma che simula 1000 lanci di un dado a sei facce usando `random.randint(1, 6)` e usa un dizionario per contare quante volte è uscita ciascuna faccia. Stampa i risultati.

11. Scrivi un programma che genera una lista di 500 numeri casuali tra 1 e 10 con `random.randint`, li raggruppa in un dizionario `numero → quante volte è comparso`, e stampa il numero più frequente.

## Set

Un **set** è una collezione di elementi **unici** e **non ordinati**.

```python
s = {1, 2, 3, 2, 1}   # {1, 2, 3} — i duplicati vengono rimossi
s = set()              # set vuoto (non {} che è un dizionario vuoto)
```

### Operazioni fondamentali

| Operazione          | Sintassi           |
| ------------------- | ------------------ |
| Aggiunta            | `s.add(x)`         |
| Rimozione           | `s.remove(x)`      |
| Appartenenza        | `x in s`           |
| Numero di elementi  | `len(s)`           |

### Quando usare un set

Un set è utile quando:
- si vuole sapere **se un elemento è già stato visto** (senza contarlo);
- si vuole eliminare i duplicati da una sequenza;
- si vogliono confrontare due insiemi (chi è in entrambi, chi manca).

```python
# eliminare duplicati da una lista
parole = ["gatto", "cane", "gatto", "topo", "cane"]
uniche = set(parole)   # {"gatto", "cane", "topo"}
```

## Scegliere tra lista, dizionario e set

| Struttura    | Usa quando…                                                      |
| ------------ | ---------------------------------------------------------------- |
| **Lista**    | l'ordine conta, ci possono essere duplicati, accedi per posizione |
| **Dizionario** | hai coppie chiave → valore, cerchi per nome non per posizione  |
| **Set**      | ti interessano solo gli elementi distinti, vuoi verificare appartenenza velocemente |

### Esercizi

1. Scrivi un programma che legge una serie di parole dall'input (una per riga, fino a riga vuota) e stampa quante sono le parole **distinte** inserite.

2. Scrivi un programma che legge due file di testo e stampa le parole che compaiono in entrambi i file.

3. Scrivi un programma che legge `voti.txt` e stampa i cognomi degli studenti senza ripetizioni.

4. Scrivi un programma che legge `testo.txt` e stampa quante parole distinte contiene il file (il **vocabolario** del testo).
