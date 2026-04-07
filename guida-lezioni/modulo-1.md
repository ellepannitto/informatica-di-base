# Modulo 01 · Introduzione alla programmazione e Python

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- Aprire e usare la REPL di Python
- Conoscere e usare i 4 tipi fondamentali: `int`, `float`, `str`, `bool`
- Assegnare variabili e usarle in espressioni
- Usare `print()` e `input()` nei tuoi script
- Navigare il file system da terminale (`pwd`, `cd`, `ls`)
- Scrivere ed eseguire un semplice script `.py`
- Descrivere il modello input → elaborazione → output
- Spiegare il ruolo di CPU, memoria e interprete
- Usare una tabella di casi per testare un programma

---

<a id="mod1-perche-python"></a>
## Perché imparare Python

In questo corso Python ci interessa perché è uno strumento pratico per imparare a programmare e per trasformare un problema in una procedura eseguibile dal computer.

Imparare Python serve a:

- **Codificare un problema** in modo preciso, così che possa essere risolto computazionalmente
- Imparare la **sintassi** di un linguaggio di programmazione, cioè le regole con cui si scrive codice corretto
- Capire la **semantica** delle istruzioni, cioè che cosa fanno davvero quando vengono eseguite
- Acquisire un primo metodo di lavoro basato su **tentativi, verifiche e correzioni**
- Familiarizzare con strumenti reali di lavoro: **interprete**, **editor** e **terminale**

Python è una buona scelta per iniziare perché è leggibile, ha una sintassi relativamente semplice e permette di ottenere risultati rapidamente.

---

<a id="mod1-come-lavorare"></a>
## Come lavorare bene

Quando impari a programmare, il metodo conta quanto la teoria. Alcune abitudini utili:

- **Carta e penna prima del codice**: prova a descrivere il problema, gli input e l'output prima di scrivere
- **Fai molti esercizi**: la programmazione si capisce soprattutto praticandola
- **Procedi per piccoli passi**: scrivi poche righe alla volta e controlla subito se funzionano
- **Trascrivi il codice** invece di fare copia-incolla: scriverlo aiuta a notare sintassi, dettagli ed errori
- **Lavora in coppia quando possibile**: spiegare a qualcun altro quello che stai facendo chiarisce anche a te le idee
- **Impara a usare REPL, editor e terminale**: sono i tre strumenti base del lavoro quotidiano

---

<a id="mod1-errori"></a>
## Se qualcosa non funziona

È normale che il codice non funzioni al primo tentativo. Non è un segnale che “non sei portato”: è parte normale del lavoro di programmazione.

Quando trovi un errore:

- fermati e **leggi bene il messaggio** restituito da Python;
- controlla prima le cause più comuni: parentesi, apici, indentazione, nomi di variabili, ordine delle istruzioni;
- prova a **isolare il problema** con un esempio più piccolo;
- consulta la documentazione o gli esempi visti a lezione;
- se serve, chiedi aiuto descrivendo con precisione cosa hai scritto, cosa ti aspettavi e cosa è successo davvero.

> **Idea chiave:** programmare significa anche fare `trial and error`, cioè provare, osservare, correggere e riprovare.

---

<a id="mod1-repl"></a>
## Parte 1 · La REPL come calcolatrice

> La REPL (Read-Eval-Print Loop) è la modalità interattiva di Python.
> Scrivi un'espressione, premi Invio, Python ti risponde.
> È il modo più diretto per iniziare a sperimentare.

Per aprirla, apri il terminale e scrivi:

```
$ python3
>>>
```

Il cursore `>>>` significa che Python è in ascolto.

---

### 1.0 · Tipi fondamentali e operazioni

Quando programmiamo, lavoriamo sempre con due idee di base:

- i **valori**, cioè gli oggetti concreti su cui vogliamo lavorare, come `7`, `"ciao"` o `True`;
- i **tipi**, cioè le categorie a cui questi valori appartengono.

Il **tipo** di un valore ci dice:

- che natura ha quel valore;
- come viene rappresentato dall'interprete;
- quali operazioni hanno senso su di esso.

In questo primo modulo useremo soprattutto quattro tipi fondamentali:

| Tipo     | Significato                    | Esempi                  |
|----------|--------------------------------|-------------------------|
| `int`    | numeri interi                  | `0`, `7`, `-12`         |
| `float`  | numeri decimali                | `3.14`, `0.5`, `-2.0`   |
| `str`    | stringhe di caratteri          | `"ciao"`, `'Python'`    |
| `bool`   | valori booleani vero/falso     | `True`, `False`         |

Un'**operazione** è un'azione applicata a uno o più valori per ottenere un nuovo risultato.

Esempi:

- `3 + 4` applica l'operazione di somma a due numeri;
- `"ciao".upper()` applica un'operazione a una stringa;
- `5 < 8` confronta due valori e restituisce un booleano.

> **Idea importante:** non tutte le operazioni sono valide per tutti i tipi. Per esempio `3 + 4` ha senso, `"ciao" + "mondo"` ha senso, ma `3 + "ciao"` produce un errore perché stiamo mescolando tipi incompatibili.

---

### 1.1 · Numeri e operazioni aritmetiche

Python riconosce due tipi numerici di base:

- **`int`** — numeri interi: `3`, `145`, `-10`, `0`
- **`float`** — numeri con la virgola: `2.05`, `-1234.897`, `13.8`

Prova nella REPL:

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

**Operatori disponibili:**

| Operazione       | Sintassi | Esempio       | Risultato |
|------------------|----------|---------------|-----------|
| Somma            | `N + N`  | `3 + 15`      | `18`      |
| Sottrazione      | `N - N`  | `10 - 4`      | `6`       |
| Moltiplicazione  | `N * N`  | `3 * 7`       | `21`      |
| Divisione        | `N / N`  | `7 / 2`       | `3.5`     |
| Divisione intera | `N // N` | `7 // 2`      | `3`       |
| Modulo (resto)   | `N % N`  | `17 % 5`      | `2`       |
| Potenza          | `N ** N` | `3 ** 2`      | `9`       |

> **Nota:** `7 / 2` restituisce `3.5` (float), mentre `7 // 2` restituisce `3` (int).
> Sono due operazioni diverse!

Le operazioni aritmetiche prendono in input valori numerici e restituiscono un nuovo valore numerico. In altre parole, non “modificano” il numero scritto nella REPL: calcolano un risultato.

Per esempio:

- `3 + 15` restituisce `18`
- `17 % 5` restituisce `2`
- `13.8 / 4` restituisce `3.45`

Questo è il primo schema fondamentale della programmazione:

`valori in input → operazione → valore in output`

---

### 1.2 · Stringhe

Le **`str`** (stringhe) sono sequenze di caratteri, racchiuse tra apici singoli o doppi.

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

**Operazioni sulle stringhe:**

| Operazione      | Sintassi         | Esempio                    | Risultato     |
|-----------------|------------------|----------------------------|---------------|
| Concatenazione  | `S + S`          | `'ab' + 'cd'`              | `'abcd'`      |
| Selezione       | `S[i]`           | `'ciao'[1]`                | `'i'`         |
| Lunghezza       | `len(S)`         | `len('ciao')`              | `4`           |
| Maiuscolo       | `S.upper()`      | `'ciao'.upper()`           | `'CIAO'`      |
| Minuscolo       | `S.lower()`      | `'CIAO'.lower()`           | `'ciao'`      |

> ⚠️ **Attenzione:** in informatica si conta a partire da **zero**.
> Il primo carattere di `'ciao'` è `'ciao'[0]`, non `'ciao'[1]`.

Anche qui il tipo conta: sulle stringhe possiamo concatenare, selezionare caratteri, misurare la lunghezza o applicare metodi come `.upper()` e `.lower()`, ma non possiamo usare operazioni pensate per i numeri come la divisione.

---

### 1.3 · Booleani e confronti

Il tipo **`bool`** ha solo due valori: `True` e `False`.

```python
>>> 3 < 8
True
>>> 5 == 5
True
>>> 'aceto' < 'olio'
True
>>> True and False
False
>>> not True
False
```

**Operatori di confronto** (restituiscono sempre un `bool`):

| Operazione        | Sintassi |
|-------------------|----------|
| Maggiore          | `>`      |
| Minore            | `<`      |
| Uguale            | `==`     |
| Maggiore o uguale | `>=`     |
| Minore o uguale   | `<=`     |
| Diverso           | `!=`     |

**Operatori logici:**

| Operazione | Sintassi  | Significato                          |
|------------|-----------|--------------------------------------|
| E          | `A and B` | `True` solo se entrambi sono `True`  |
| O          | `A or B`  | `True` se almeno uno è `True`        |
| Non        | `not A`   | Inverte il valore                    |

I booleani sono fondamentali perché permettono al programma di decidere: più avanti useremo questi risultati per scrivere condizioni, controllare casi e scegliere tra comportamenti diversi.

---

### ✏️ Esercizi A — Calcoli sulla REPL

Scrivi un'espressione che calcoli ciascuno dei seguenti valori:

1. Il successore di 15
2. La metà del triplo di 12
3. Il triplo della metà di 12
4. Il doppio della differenza tra 15 e 7
5. Il doppio della differenza tra 3 e 7 *(attenzione al segno!)*
6. Il resto della divisione tra 44 e 7
7. La media di 2, 5, 9

---

### ✏️ Esercizi B — Stringhe sulla REPL

8. La lunghezza della stringa `"Happy families are all alike"`
9. La stessa stringa in TUTTO MAIUSCOLO
10. La concatenazione di `"Happy families are all alike"` e `"every unhappy family is unhappy in its own way"` con uno spazio tra le due frasi
11. Il primo carattere della stringa `"linguistica"`
12. Il sesto carattere di `"supercalifragilistichespiralidoso"` in maiuscolo

---

### ✏️ Esercizi C — Cosa calcolano queste espressioni?

Per ciascuna, scrivi il risultato **e** il tipo (`int`, `float`, `str`, `bool`):

1. `5 * (2 + 4)`
2. `152 % 9`
3. `"banana" + "fragola"`
4. `"olio".upper()`
5. `len("carote")`
6. `"cenerentola"[8]`

---

<a id="mod1-espressioni-istruzioni"></a>
## Parte 2 · Espressioni e istruzioni

> Fin qui abbiamo usato Python soprattutto come una calcolatrice evoluta.
> Ora dobbiamo distinguere due idee fondamentali: le **espressioni** e le **istruzioni**.

### 2.1 · Che cos'è un'espressione

Un'**espressione** è qualcosa che Python può **valutare** per ottenere un valore.

Esempi:

- `3 + 4` produce `7`
- `"ciao".upper()` produce `"CIAO"`
- `5 < 8` produce `True`
- `len("banana")` produce `6`

Possiamo dire quindi che un'espressione:

- prende zero o più valori in input;
- applica operazioni o funzioni;
- restituisce sempre un **valore finale**.

### 2.2 · Che cos'è un'istruzione

Un'**istruzione** è un comando che dice all'interprete di fare qualcosa.

A differenza di un'espressione, un'istruzione non serve principalmente a “produrre un valore da mostrare”, ma a **modificare lo stato del programma** oppure a controllarne l'esecuzione.

Esempi di istruzioni:

- `x = 44` assegna un valore a una variabile;
- `print("ciao")` produce un effetto di output sullo schermo;
- più avanti vedremo istruzioni come `if`, `while` e `def`.

### 2.3 · Differenza pratica

La differenza centrale è questa:

- un'**espressione** viene valutata e dà come risultato un valore;
- un'**istruzione** viene eseguita e cambia qualcosa nello stato o nel comportamento del programma.

Confronta questi esempi:

```python
>>> 3 + 4
7
```

Qui `3 + 4` è un'espressione: Python la valuta e mostra il risultato.

```python
>>> x = 3 + 4
```

Qui `x = 3 + 4` è un'istruzione: Python prima valuta l'espressione `3 + 4`, poi assegna il risultato alla variabile `x`.

In altre parole:

- a destra dell'uguale troviamo spesso un'**espressione**;
- l'intera riga `x = 3 + 4` è un'**istruzione di assegnamento**.

> **Idea chiave:** le espressioni producono valori; le istruzioni usano quei valori per costruire il comportamento del programma.

---

## Parte 3 · Variabili e stato del programma

> Finora Python ha risposto a ogni espressione, ma non ha ricordato nulla.
> Le **variabili** ci permettono di dare un nome ai valori e tenerli in memoria.

### 3.1 · Assegnare una variabile

Una **variabile** è un nome che usiamo per ricordare un valore.

L'assegnamento ha questa forma generale:

```python
nome_variabile = espressione
```

Questa istruzione va letta così:

1. valuta l'espressione a destra dell'uguale;
2. associa il risultato al nome scritto a sinistra;
3. memorizza questa associazione nello stato del programma.

È importante non leggere `=` come nella matematica scolastica. In Python `=` non significa “è uguale a per sempre”, ma significa **assegna a questo nome il valore che hai appena calcolato**.

```python
>>> x = 33
>>> y = 'aardvark'
>>> z = True
```

L'interprete gestisce internamente una **tabella di memoria**:

| Identificatore | Tipo   | Valore      |
|----------------|--------|-------------|
| `x`            | `int`  | `33`        |
| `y`            | `str`  | `'aardvark'`|
| `z`            | `bool` | `True`      |

L'assegnamento può prendere il risultato di qualsiasi espressione valida:

- `x = 33` assegna direttamente un valore;
- `y = x + 5` assegna il risultato di un calcolo;
- `z = True` assegna un valore booleano;
- `nome = input("Come ti chiami? ")` assegna il valore restituito da una funzione.

Una volta assegnata, la variabile si può usare nelle espressioni successive:

```python
>>> x = 44
>>> y = x + 5
>>> y
49
>>> x = x // 6
>>> x
7
```

Nota bene: una variabile può anche **cambiare valore** durante l'esecuzione.

Per esempio:

- prima `x` vale `44`;
- poi con `x = x // 6` il vecchio valore di `x` viene letto, usato nel calcolo, e il nuovo risultato `7` viene associato di nuovo allo stesso nome.

**Come scegliere il nome?**
Qualsiasi sequenza di lettere e numeri, purché non sia una parola riservata di Python (`if`, `for`, `while`, ...) e non inizi con una cifra. Scegli sempre **nomi significativi**: `eta` è meglio di `x`, `nome_utente` è meglio di `n`.

---

### ✏️ Esercizi D — Variabili e tracciamento

Per ciascun programma: **prima** scrivi a mano il valore di `y` al termine dell'esecuzione, **poi** verifica sulla REPL.

1. `x = 4` · `y = 2 * x`
2. `x = 12` · `y = x + 1`
3. `a = 1` · `b = 2` · `c = 3` · `y = a**2 + b**2 + c**2`
4. `s1 = "CIAO MONDO"` · `s2 = s1[1] + "o"` · `y = s2.lower()`
5. `s = "MONDO CIAO"` · `i = 2` · `y = s[i] + s[i+1]`

---

## Parte 3 · Come funziona il computer

> Ora che hai sperimentato la REPL, possiamo dare un nome a quello che è successo.

### 3.1 · Python come linguaggio formale

Un linguaggio di programmazione è un linguaggio **formale**, cioè ha:

- **Vocabolario** — i simboli che si possono usare: valori (raggruppati in *tipi*) e *keywords* riservate (`if`, `for`, `def`, ...)
- **Sintassi** — le regole di composizione:
  - *Espressioni* → calcolano un valore (`3 + 15`, `len('ciao')`)
  - *Istruzioni* → modificano lo stato del programma (`x = 44`)
- **Semantica** — il significato di ciò che scriviamo, interpretato dall'*interprete*

Nella REPL abbiamo scritto quasi solo **espressioni**. Con `x = 44` abbiamo scritto la nostra prima **istruzione**.

**Cos'è l'interprete?**

```
$ python3 mio_script.py
```

L'interprete legge il codice Python, ne capisce il significato, e lo traduce in istruzioni che il processore può eseguire.

---

### 3.2 · Che tipo di linguaggio è Python

Python è un linguaggio di programmazione con alcune caratteristiche importanti:

- **Interpretato** — il codice viene eseguito attraverso un interprete, cioè un programma che legge le istruzioni Python e le fa eseguire al computer. Per chi inizia significa che si può provare subito il codice, riga per riga, nella REPL o in uno script.
- **Ad alto livello** — permette di esprimere operazioni complesse con istruzioni relativamente vicine al linguaggio umano e lontane dai dettagli elettronici della macchina. Non dobbiamo gestire direttamente registri, indirizzi di memoria o istruzioni binarie della CPU.
- **Multiparadigma** — supporta più modi di organizzare i programmi. Per esempio possiamo scrivere codice:
  - **imperativo**, come una sequenza di istruzioni eseguite in ordine;
  - **procedurale**, raggruppando istruzioni in funzioni riutilizzabili;
  - **orientato agli oggetti**, modellando dati e comportamenti tramite oggetti e classi.
- **General purpose** — non nasce per un solo settore specifico: si usa per automazione, analisi dati, web, scripting, intelligenza artificiale, didattica e molti altri contesti.

> **In pratica:** Python è spesso scelto nei corsi introduttivi perché ha una sintassi leggibile, permette di ottenere risultati rapidamente ed espone bene i concetti fondamentali della programmazione.

---

<a id="mod1-von-neumann"></a>
### 3.3 · L'architettura di Von Neumann

Qualsiasi computer moderno è costruito secondo il modello di **Von Neumann**:

```
┌─────────────────────────────────────────┐
│               COMPUTER                  │
│                                         │
│   ┌──────────┐      ┌────────────────┐  │
│   │   CPU    │◄────►│    MEMORIA     │  │
│   │(elabora) │      │  (RAM: dati +  │  │
│   └──────────┘      │  istruzioni)   │  │
│        ▲            └────────────────┘  │
│        │                                │
│   ┌────┴────────────────────────────┐   │
│   │          INPUT / OUTPUT         │   │
│   │  (tastiera, schermo, file...)   │   │
└───┴─────────────────────────────────┴───┘
```

| Componente | Ruolo |
|------------|-------|
| **CPU**    | Esegue le istruzioni una alla volta |
| **RAM**    | Conserva dati e istruzioni durante l'esecuzione |
| **I/O**    | Riceve input dall'utente, produce output verso lo schermo o i file |

**Collegamento con la REPL:**
- `x = 44` → la CPU esegue l'istruzione, la **RAM** memorizza il valore
- `x + 5` → la CPU legge `x` dalla RAM, calcola, manda il risultato all'**output** (schermo)
- Ogni riga della REPL è un ciclo completo: **input → elaborazione → output**

> **In sintesi:** un programma è una sequenza di istruzioni e dati, tutti in memoria, eseguiti dalla CPU uno alla volta.

---

<a id="mod1-input-output"></a>
### 3.4 · Il modello Input → Elaborazione → Output

Ogni programma, dal più semplice al più complesso, segue sempre lo stesso schema:

```
  INPUT  ──►  ELABORAZIONE  ──►  OUTPUT
```

Esempi che conosci già:

| Programma      | Input                        | Elaborazione              | Output                  |
|----------------|------------------------------|---------------------------|-------------------------|
| Google Maps    | Indirizzo di partenza/arrivo | Algoritmo di percorso     | Mappa con indicazioni   |
| Shazam         | Audio dal microfono          | Riconoscimento musicale   | Nome della canzone      |
| La nostra REPL | `3 + 15`                     | Addizione                 | `18`                    |

Un programma è essenzialmente una sequenza di istruzioni. Il suo funzionamento segue un ciclo fondamentale:

- Input: Dati inseriti nel sistema per l'elaborazione o l'archiviazione.
- Elaborazione: La CPU riceve istruzioni e dati dalla memoria o dall'input e li processa.
- Output: I risultati dell'elaborazione vengono inviati a un dispositivo di uscita o trasferiti alla memoria di massa (storage secondario).

* Codice Sorgente vs Codice Macchina
  * Codice Macchina: È l'unico linguaggio compreso direttamente dalla CPU, composto interamente da numeri binari (0 e 1).
  * Codice Sorgente: È il codice scritto dai programmatori in un linguaggio leggibile dall'uomo (come Python). Un'istruzione ad alto livello è "one-to-many", ovvero viene tradotta in molteplici istruzioni in linguaggio macchina.

Poiché il computer non capisce il codice sorgente, serve un traduttore:

* Interprete (es. Python): Traduce ed esegue il codice un'istruzione alla volta. Gli errori sono facili da individuare durante lo sviluppo, ma l'esecuzione è più lenta.
* Compilatore (es. C++): Traduce l'intero programma in un file eseguibile unico. Una volta compilato, il programma è molto veloce.
* Assembler: Traduce specificamente il linguaggio Assembly in codice macchina.

Dati e istruzioni sono entrambi memorizzati come numeri binari nella memoria principale.
Le istruzioni vengono prelevate dalla memoria una alla volta in modo seriale.

Per gestire il ciclo di elaborazione, la CPU utilizza cinque registri speciali:

* PC (Program Counter): Contiene l'indirizzo della prossima istruzione da prelevare.
* MAR (Memory Address Register): Contiene l'indirizzo della cella di memoria attualmente in uso per la lettura o scrittura.
* MBR (Memory Buffer Register): Contiene i dati o le istruzioni appena letti dalla memoria o in attesa di essere scritti.
* CIR (Current Instruction Register): Contiene l'istruzione che viene attualmente decodificata ed eseguita.
* ACC (Accumulatore): Memorizza i risultati temporanei delle operazioni logico-aritmetiche.

La CPU ripete continuamente queste fasi: preleva l'istruzione dalla RAM (Fetch), la interpreta (Decode) e la esegue (Execute).

Il ciclo **Fetch-Decode-Execute** è il processo fondamentale con cui la CPU elabora ogni singola istruzione di un programma. Poiché le istruzioni sono in memoria, la CPU le legge una alla volta e ripete sempre lo stesso schema:

1. **Fetch (Prelievo)**: la CPU recupera l'istruzione dalla memoria.
   - **Indirizzamento**: l'indirizzo contenuto nel `PC` (Program Counter), che indica la prossima istruzione da eseguire, viene copiato nel `MAR` (Memory Address Register).
   - **Aggiornamento del PC**: il `PC` viene incrementato, così punta già all'istruzione successiva.
   - **Accesso alla memoria**: il processore usa l'indirizzo contenuto nel `MAR` per leggere la cella di memoria corretta.
   - **Trasferimento dati**: l'istruzione letta viene copiata nel `MBR` (Memory Buffer Register, detto anche `MDR`).
   - **Caricamento istruzione**: il contenuto del `MBR` viene trasferito nel `CIR` (Current Instruction Register).

2. **Decode (Decodifica)**: la CPU interpreta l'istruzione appena caricata.
   - L'unità di controllo legge il contenuto del `CIR` e determina quale operazione deve essere eseguita.
   - Per esempio può trattarsi di un'addizione, di una lettura dalla memoria o di uno spostamento di dati.

3. **Execute (Esecuzione)**: la CPU esegue davvero l'operazione richiesta.
   - Se l'istruzione richiede un calcolo matematico o logico, entra in gioco l'`ALU` (Arithmetic Logic Unit).
   - Il risultato dell'operazione può essere conservato temporaneamente nell'`ACC` (Accumulatore).

4. **Ripetizione**: dopo l'esecuzione, il ciclo ricomincia dal primo passo.
   - La CPU passa alla prossima istruzione indicata dal `PC`.
   - Questo processo continua finché il programma è in esecuzione.

In sintesi: I registri lavorano come una catena di montaggio: il PC tiene il segno di dove siamo, il MAR e l'MBR fanno da ponte con la memoria esterna, il CIR tiene l'istruzione "sotto i ferri" per la decodifica e l'Accumulatore raccoglie il prodotto finito dell'operazione.

L'interprete Python gestisce la memoria durante l'esecuzione agendo come un traduttore che processa il codice un'istruzione alla volta. La gestione della memoria avviene principalmente attraverso l'uso di tabelle di memoria che associano i nomi delle variabili (identificatori) ai loro valori o indirizzi fisici.

**RAM vs. file system:**
- La **RAM** è veloce ma volatile: le variabili spariscono quando chiudi Python
- Il **file system** (disco) è permanente: i file `.py` che scriveremo restano salvati

---

<a id="mod1-ambiente"></a>
### 3.5 · I tre strumenti dell'ambiente di lavoro

| Strumento             | Ruolo                          | Esempio d'uso              |
|-----------------------|--------------------------------|----------------------------|
| **Editor** (VS Code)  | Scrivere il codice             | Creare e salvare `script.py` |
| **Terminale / Shell** | Parlare con il sistema operativo | `cd`, `ls`, eseguire script |
| **Interprete Python** | Eseguire il codice             | `python3 script.py`        |

> **La REPL** combina terminale e interprete: scrivi → esegui → vedi il risultato, senza creare file.

---

<a id="mod1-terminale"></a>
## Parte 4 · Il terminale

> Per eseguire i tuoi script devi saper navigare il file system dal terminale.

### 4.1 · Comandi fondamentali

```bash
pwd            # dove sono? (stampa il percorso della cartella corrente)
ls             # cosa c'è qui? (elenca file e cartelle)
cd cartella    # entra nella cartella
cd ..          # torna alla cartella superiore
```

**Percorsi assoluti vs. relativi:**

```bash
# Assoluto: parte sempre dalla radice del disco
/home/studente/corso/script.py

# Relativo: parte da dove sei adesso
corso/script.py
```

---

<a id="mod1-primo-script"></a>
### 4.2 · Il primo script

Crea un file `saluto.py` in VS Code con questo contenuto:

```python
nome = input("Come ti chiami? ")
print("Ciao,", nome)
```

Poi eseguilo dal terminale:

```bash
cd /percorso/della/cartella
python3 saluto.py
```

**Prova anche queste varianti:**

```python
# Versione 2: calcolo
eta = input("Quanti anni hai? ")
eta = int(eta)
print("Fra 10 anni avrai", eta + 10, "anni.")
```

```python
# Versione 3: più input
nome = input("Come ti chiami? ")
cognome = input("Qual è il tuo cognome? ")
print("Benvenuto/a,", nome, cognome + "!")
```

> **Domanda:** perché serve `int(eta)` nella versione 2? Cosa succede se lo togli?
> *(Lo approfondiremo nel Modulo 02)*

---

## Parte 5 Assegnamento di variabili

Quando l'interprete esegue un'istruzione di assegnamento (es. x = 5), segue una semantica precisa:

    Valutazione: Calcola il valore dell'espressione a destra dell'uguale.
    Creazione: Se necessario, crea una cella nella tabella di memoria dedicata a quell'identificatore.
    Associazione: Assegna il valore calcolato al nome della variabile nella tabella.



---

<a id="mod1-tdd"></a>
## Parte 6 · Testare il codice: introduzione al TDD

> Scrivere codice che funziona **in tutti i casi** è più difficile che farlo funzionare nel caso ovvio.
> Il **Test-Driven Development** ci insegna a ragionare sui casi *prima* di scrivere una riga.

### 6.1 · I tre tipi di caso

Prima di scrivere qualsiasi script, poniti queste domande:

| Tipo di caso  | Domanda                                   |
|---------------|-------------------------------------------|
| **Normale**   | Cosa mi aspetto con un input tipico?      |
| **Limite**    | Cosa succede ai bordi? (zero, negativo, stringa vuota) |
| **Errore**    | Cosa può andare storto?                   |

**Esempio guidato:** script che calcola il doppio di un numero

Compila la tabella *prima* di scrivere il codice:

| Tipo    | Input  | Output atteso |
|---------|--------|---------------|
| Normale | `5`    | `10`          |
| Normale | `3.5`  | `7.0`         |
| Limite  | `0`    | `0`           |
| Limite  | `-4`   | `-8`          |

Solo dopo si scrive:

```python
n = input("Inserisci un numero: ")
n = int(n)
print("Il doppio è", n * 2)
```

E si verifica su ciascun caso della tabella.

---

### ✏️ Esercizi E — TDD: prima la tabella, poi il codice

Per ciascun esercizio: **prima** compila la tabella dei casi, **poi** scrivi lo script e verifica ogni caso.

**Esercizio 1 — Secondi in ore, minuti e secondi**

```
Input:  un numero intero di secondi (es. 3661)
Output: "1 ore, 1 minuti, 1 secondi"
```

**Esercizio 2 — Saluto con cognome in maiuscolo**

```
Input:  nome e cognome (due input() separati)
Output: "Ciao COGNOME, nome!"
```

**Esercizio 3 — Doppio e triplo**

```
Input:  un numero intero
Output: due righe — una con il doppio, una con il triplo
```

---

<a id="mod1-tracciamento"></a>
## Parte 7 · Tracciare l'esecuzione a mano

> La macchina non può sbagliare. Se il programma fa qualcosa di inatteso,
> il problema è nel nostro modello mentale. Tracciare l'esecuzione su carta
> è lo strumento più potente per capire cosa sta succedendo davvero.

### 7.1 · Come si tracccia

Per ogni istruzione, aggiorna la tabella delle variabili e annota l'eventuale output.

**Esempio:** dato il programma

```python
x = 10
y = x * 2
x = y - 3
z = x + y
print(z)
```

La traccia è:

| Istruzione    | `x`  | `y`  | `z`  | Output |
|---------------|------|------|------|--------|
| `x = 10`      | `10` | —    | —    |        |
| `y = x * 2`   | `10` | `20` | —    |        |
| `x = y - 3`   | `17` | `20` | —    |        |
| `z = x + y`   | `17` | `20` | `37` |        |
| `print(z)`    | `17` | `20` | `37` | `37`   |

---

### ✏️ Esercizi F — Tracciamento

Per ciascun programma: **prima** compila la tabella a mano, **poi** esegui sulla REPL e confronta.

**Programma 1**
```python
a = 5
b = a + 3
a = b * 2
print(a)
print(b)
```

**Programma 2**
```python
s = "ciao"
t = s.upper()
s = t + "!"
print(s)
print(len(s))
```

**Programma 3**
```python
x = 10
y = 3
x = x % y
z = x + y
print(z)
print(x == y)
```

---

## Riepilogo

| Concetto               | In breve                                                   |
|------------------------|------------------------------------------------------------|
| **REPL**               | Modalità interattiva: scrivi → esegui → vedi il risultato  |
| **Tipi fondamentali**  | `int`, `float`, `str`, `bool`                              |
| **Espressione**        | Calcola un valore: `3 + 15`, `len("ciao")`                 |
| **Istruzione**         | Modifica lo stato: `x = 44`                                |
| **Variabile**          | Un nome associato a un valore in memoria (RAM)             |
| **Interprete**         | Legge Python, lo traduce in istruzioni per la CPU          |
| **Von Neumann**        | CPU + RAM + I/O — il modello di ogni computer moderno      |
| **I/E/O**              | Ogni programma: input → elaborazione → output              |
| **TDD (base)**         | Prima i casi attesi, poi il codice                         |
| **Tracciamento**       | Seguire l'esecuzione riga per riga su carta                |

---
