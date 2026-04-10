# Modulo 09 · File e formati strutturati

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- aprire file di testo in lettura e in scrittura;
- leggere un file come stringa, come lista di righe o riga per riga;
- distinguere tra standard input, file aperto con `open()` e parametri da riga di comando;
- usare `split()`, `strip()` e conversioni di tipo sui dati letti da file;
- scrivere output su file;
- riconoscere i formati di base: testo semplice, CSV, JSON e HTML;
- usare alcune utility da terminale per ispezionare file e cartelle.

---

<a id="mod9-file"></a>
## Il problema che porta a `open()`

Finche' i dati sono scritti direttamente nel codice o arrivano da `input()`, i programmi restano piccoli.

Ma presto vogliamo lavorare su:

- testi salvati su disco;
- file di dati;
- input riutilizzabili.

Per farlo il programma deve poter aprire un file.

---

## Sintassi di `open()`

I file sono un nuovo tipo di sorgente dati.

Esempio base:

```python
nome_file = "data/testo.txt"
file_in = open(nome_file, "r", encoding="utf-8")
print(file_in.read())
file_in.close()
```

Forma generale:

```python
open(percorso, mode, encoding="utf-8")
```

---

## Semantica di `open()`

Nel corso conviene usare soprattutto la forma con `with`:

```python
with open("data/testo.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        print(line)
```

### Parametri essenziali di `open`

| Parametro | Significato |
| --- | --- |
| `file` | percorso del file |
| `mode` | modalita', tipicamente `r` o `w` |
| `encoding` | codifica del testo, spesso `utf-8` |

Punti chiave:

- il nome del file e' una stringa;
- il percorso puo' essere assoluto oppure relativo;
- `open(...)` restituisce un oggetto che permette di fare operazioni di input/output sul file aperto.

---

## Il problema che porta a `with`

Aprire un file non basta: bisogna anche ricordarsi di chiuderlo correttamente.

Se il programma cresce, scrivere sempre:

- apri;
- usa;
- chiudi

puo' diventare fragile. `with` serve a rendere questa gestione piu' sicura e leggibile.

---

## Sintassi di `with`

Forma tipica:

```python
with open("data/testo.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        print(line)
```

Parti da riconoscere:

- `with` introduce un contesto di lavoro;
- `open(...)` crea la risorsa da usare;
- `as file_in` assegna un nome a quella risorsa;
- il blocco indentato contiene le operazioni da fare.

---

## Semantica di `with`

Quando Python esegue un blocco `with`:

1. apre la risorsa;
2. la rende disponibile tramite il nome dopo `as`;
3. esegue il blocco indentato;
4. alla fine chiude correttamente la risorsa.

Per questo `with` e' spesso preferibile a:

```python
file_in = open(...)
...
file_in.close()
```

perche' rende piu' sicura la gestione del file.

---

## Il problema che porta a `read()` e `readlines()`

Una volta aperto un file, dobbiamo decidere come leggerlo.

Possibili bisogni:

- leggere tutto il contenuto in una volta;
- ottenere una lista di righe;
- scorrere il file riga per riga.

`read()` e `readlines()` servono proprio a esprimere queste strategie.

---

## Sintassi di `read()` e `readlines()`

```python
contenuto = file_handler.read()
righe = file_handler.readlines()

for line in file_handler:
    ...
```

`read()` e `readlines()` sono metodi dell'oggetto file.

---

## Semantica di `read()` e `readlines()`

Differenza pratica:

- `read()` prende tutto il contenuto come una stringa unica;
- `readlines()` costruisce una lista di righe;
- `for line in file_handler` legge una riga alla volta.

Per file piccoli possono andare bene tutte e tre.
Per file piu' grandi, la lettura riga per riga e' spesso la soluzione piu' pulita.

---

## Il problema che porta a `split()`

Quando leggiamo da file, otteniamo testo grezzo.

Molto spesso pero' ci servono unita' piu' piccole:

- righe;
- campi;
- parole.

`split()` serve a segmentare una stringa usando un separatore.

---

## Sintassi di `split()`

Possiamo anche leggere tutto e poi segmentare esplicitamente:

```python
contenuto = file_handler.read()
righe = contenuto.split("\n")
campi = contenuto.split("\t")
```

Forma generale:

```python
stringa.split(separatore)
```

---

## Semantica di `split()`

Questo aiuta a capire che:

- il file non contiene gia' una lista;
- siamo noi a scegliere come segmentare;
- newline e tab si scrivono come `\n` e `\t`.

---

## Il problema che porta a `strip()`

Le righe lette da file contengono spesso caratteri indesiderati ai bordi:

- spazi;
- tab;
- fine riga.

Prima di convertire o confrontare i dati conviene ripulirli.

---

## Sintassi di `strip()`

Forma tipica:

```python
line.strip()
```

Possiamo usarlo anche con argomenti:

```python
line.strip(".,;")
```

---

## Semantica di `strip()`

Quando leggiamo da file:

- ogni riga letta e' una stringa;
- puo' contenere il carattere di fine riga;
- se ci servono numeri dobbiamo convertire.

Schema tipico:

```python
somma = 0.0

with open("dati.txt", "r", encoding="utf-8") as file_in:
    for line in file_in:
        somma = somma + float(line.strip())
```

`strip()` senza argomenti toglie i caratteri bianchi ai bordi:

- spazi;
- tab;
- ritorni a capo.

Se serve, possiamo anche specificare quali caratteri togliere.

---

## Scrivere su un file

Forma base:

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

Attenzione:

- `w` sovrascrive il contenuto precedente;
- il nome del file e' sempre una stringa che rappresenta un percorso.

### Standard output e file

`print(...)` di default scrive sullo standard output, cioe' sul canale che il terminale mostra a schermo.

Con `file=...` possiamo mandare lo stesso output in un file aperto.

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

### Redirezione della shell vs scrittura in Python

1. Redirezione della shell:

```bash
python3 script.py > output.txt
```

2. Scrittura esplicita in Python:

```python
with open("output.txt", "w", encoding="utf-8") as file_output:
    print("ciao", file=file_output)
```

Nel primo caso e' la shell che intercetta lo standard output.
Nel secondo caso e' il programma Python che decide dove scrivere.

---

## Il problema che porta a `sys.argv`

Se il nome del file di input e di output e' scritto nel codice, ogni volta che cambia dobbiamo modificare lo script.

Molto meglio passare questi dati dall'esterno, da riga di comando.

Per farlo il programma deve poter leggere gli argomenti con cui e' stato lanciato.

---

## Sintassi di `sys.argv`

Forma tipica:

```python
import sys

nome_input = sys.argv[1]
nome_output = sys.argv[2]
files = sys.argv[1:]
```

---

## Semantica di `sys.argv`

`sys.argv` e' una lista che contiene gli argomenti passati al programma da riga di comando.

In particolare:

- `sys.argv[0]` e' il nome dello script;
- `sys.argv[1]` e i successivi sono gli argomenti forniti dall'utente.

Per questo:

```python
files = sys.argv[1:]
```

significa:

- ignora il nome dello script;
- prendi tutti i file o parametri passati dopo.

---

## Standard input, `open()` e `sys.argv`

Ci sono tre modi diversi per far arrivare dati a un programma.

### 1. Standard input

```python
numero = int(input())
```

### 2. File aperto con `open()`

```python
with open("input.txt", "r", encoding="utf-8") as file_in:
    ...
```

### 3. Parametri da riga di comando

```python
import sys

nome_input = sys.argv[1]
nome_output = sys.argv[2]
```

---

<a id="mod9-terminale"></a>
## Esplorazione rapida da terminale su file di testo

Le utility da terminale sono utili per:

- ispezionare rapidamente un file;
- fare piccole trasformazioni;
- capire il procedimento logico prima di scrivere uno script piu' completo.

| Comando | Uso tipico |
| --- | --- |
| `cat file.txt` | mostra tutto il file |
| `less file.txt` | scorre il file una schermata alla volta |
| `head file.txt` | mostra l'inizio del file |
| `tail file.txt` | mostra la fine del file |
| `grep pattern file.txt` | filtra le righe che contengono un pattern |
| `cut ...` | seleziona campi o colonne |
| `sort` | ordina le righe |
| `uniq` / `uniq -c` | elimina duplicati consecutivi o li conta |
| `wc` | conta righe, parole o caratteri |

### Pipe e risultati intermedi

```bash
cat alice.txt | tr ' ' '\n'
```

La pipe `|` passa l'output del comando precedente come input del successivo.

Possiamo anche salvare risultati intermedi:

```bash
cat alice.txt | tr ' ' '\n' > parole.txt
sort parole.txt > parole-ordinate.txt
```

---

<a id="mod9-formati"></a>
## Formati di input/output

### Testo semplice

- una riga dopo l'altra;
- nessuna struttura esplicita oltre ai caratteri e ai separatori.

### CSV

- valori separati da virgole o altro separatore;
- ogni riga rappresenta spesso un record.

### JSON

- struttura annidata;
- tipicamente oggetti, liste, chiavi e valori.

### HTML

- testo con marcatura;
- utile quando vogliamo estrarre informazioni da pagine o frammenti strutturati.

Nel corso, per questi formati, il punto non e' entrare subito in librerie avanzate, ma capire:

- che tipo di struttura ha il dato;
- quale metodo di lettura e segmentazione conviene usare;
- quando basta il testo semplice e quando serve una rappresentazione piu' ricca.

---

## Esercizi

### Lettura e scrittura di base

1. leggi un file di numeri e calcolane la somma;
2. leggi un file testuale e stampalo su una sola riga;
3. stampa le parole di un testo una per riga;
4. leggi un file e produci un secondo file in minuscolo;
5. conta righe, parole e caratteri di un file;
6. usa `sys.argv` per scegliere il file di input;
7. salva l'output di uno script in un file;
8. ispeziona un file da terminale con `cat`, `head`, `tail`, `grep`, `sort`, `wc`.

### Input da file come stdin

I seguenti esercizi usano la redirezione dell'input (`python3 script.py < input.txt`). Prepara un file di input per ogni esercizio e prova a eseguirlo in entrambi i modi: con `input()` interattivo e con il file.

9. Scrivi un programma che legge una serie di numeri finché non incontra `0`. Per ogni numero `n` letto, stampa tutti i numeri pari compresi tra `0` (incluso) e `n` (escluso).

   Input:
   ```
   6
   10
   0
   ```
   Output:
   ```
   0 2 4
   0 2 4 6 8
   ```

10. Scrivi un programma che legge una stringa e controlla se è palindroma (ignora maiuscole e spazi). Esempio: `I topi non avevano nipoti` è palindroma.

11. Scrivi un programma che legge una sequenza di stringhe finché non incontra `fine` e conta il numero di parole che iniziano per ogni vocale (`a`, `e`, `i`, `o`, `u`).

12. Scrivi un programma che legge 5 lettere, poi una sequenza di stringhe finché non incontra `fine`, e conta il numero di parole che iniziano per ciascuna delle lettere lette.

13. Scrivi un programma che legge tre serie di numeri separate da `0`. Per ogni serie stampa i numeri letti al contrario.

    Input:
    ```
    4
    12
    0
    9
    7
    6
    0
    4
    1
    -3
    8
    0
    ```
    Output:
    ```
    [12, 4]
    [6, 7, 9]
    [8, -3, 1, 4]
    ```

### File di testo: trasformazioni

14. Scrivi un programma che legge un file di testo e scrive su un nuovo file lo stesso testo con tutte le lettere in minuscolo e le righe vuote rimosse.
15. Scrivi un programma che legge un file di testo riga per riga e produce un secondo file contenente solo le righe che contengono la parola `palla` (senza distinzione maiuscole/minuscole).
16. Scrivi un programma che legge un file di testo riga per riga e conta quante righe ci sono, quante parole e quanti caratteri. Stampa i tre conteggi.

---

## Riepilogo

Questo modulo raccoglie il materiale su:

- apertura e lettura di file;
- segmentazione del testo con `split()` e `strip()`;
- scrittura su file;
- differenza tra standard input, file aperto e parametri da riga di comando;
- utility da terminale per file di testo;
- primi formati strutturati: testo semplice, CSV, JSON e HTML.
