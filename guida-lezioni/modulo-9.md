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
## File di testo: aprire, leggere, scorrere

I file sono un nuovo tipo di sorgente dati.

Esempio base:

```python
nome_file = "data/testo.txt"
file_in = open(nome_file, "r", encoding="utf-8")
print(file_in.read())
file_in.close()
```

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

### `read()`, `readlines()` e iterazione

```python
contenuto = file_handler.read()
righe = file_handler.readlines()

for line in file_handler:
    ...
```

Differenza pratica:

- `read()` prende tutto il contenuto come una stringa unica;
- `readlines()` costruisce una lista di righe;
- `for line in file_handler` legge una riga alla volta.

Per file piccoli possono andare bene tutte e tre.
Per file piu' grandi, la lettura riga per riga e' spesso la soluzione piu' pulita.

### Segmentare il contenuto

Possiamo anche leggere tutto e poi segmentare esplicitamente:

```python
contenuto = file_handler.read()
righe = contenuto.split("\n")
campi = contenuto.split("\t")
```

Questo aiuta a capire che:

- il file non contiene gia' una lista;
- siamo noi a scegliere come segmentare;
- newline e tab si scrivono come `\n` e `\t`.

---

## `strip()` e conversione dei valori

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

`sys.argv` e' una lista:

- in posizione `0` c'e' il nome dello script;
- da `1` in poi ci sono i parametri passati da terminale.

Quindi possiamo anche lavorare su molti file:

```python
files = sys.argv[1:]

for nome_file in files:
    ...
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

1. leggi un file di numeri e calcolane la somma;
2. leggi un file testuale e stampalo su una sola riga;
3. stampa le parole di un testo una per riga;
4. leggi un file e produci un secondo file in minuscolo;
5. conta righe, parole e caratteri di un file;
6. usa `sys.argv` per scegliere il file di input;
7. salva l'output di uno script in un file;
8. ispeziona un file da terminale con `cat`, `head`, `tail`, `grep`, `sort`, `wc`.

---

## Riepilogo

Questo modulo raccoglie il materiale su:

- apertura e lettura di file;
- segmentazione del testo con `split()` e `strip()`;
- scrittura su file;
- differenza tra standard input, file aperto e parametri da riga di comando;
- utility da terminale per file di testo;
- primi formati strutturati: testo semplice, CSV, JSON e HTML.
