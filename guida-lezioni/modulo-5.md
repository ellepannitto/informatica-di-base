# Modulo 05 · Liste e lettura dei dati

---

## Autovalutazione

- Sai rappresentare dati ordinati con una lista?
- Sai usare le operazioni fondamentali sulle liste?
- Sai trasformare una stringa in lista con `split()`?
- Sai leggere sequenze di dati e accumularle in una lista?
- Sai ragionare sulla differenza tra lista e stringa?

---

<a id="mod5-liste"></a>
## Liste: collezioni ordinate di elementi

Le liste sono **collezioni ordinate di elementi**.

Esempi:

```python
[3, 19, 27, 43]
["elefante", "cammello", "pentola", "ciao"]
[True, True, True, False]
[["a", "b"], ["a", "c"], ["a", "d"]]
```

![Archivio](imgs/archivio.jpg)

Una lista:

- mantiene l'ordine degli elementi;
- puo' contenere qualunque tipo di valore;
- puo' contenere anche altre liste.

Una metafora utile e' questa: se i valori semplici erano come barattoli sparsi in dispensa, la lista e' piu' simile a un **archivio ordinato**.

Questo significa che:

- gli elementi stanno insieme in una sola struttura;
- ogni elemento ha una posizione;
- possiamo distinguere il primo, il secondo, il terzo e cosi' via.

Esempio intuitivo:

- invece di avere tante variabili separate per gli studenti di una classe;
- possiamo avere una sola variabile `classe`;
- che contiene, in ordine, tutti i nomi degli studenti.

### Operazioni fondamentali

| Operazione | Sintassi |
| --- | --- |
| Concatenazione | `L1 + L2` |
| Estensione | `L1.extend(L2)` |
| Selezione | `L[i]` |
| Lunghezza | `len(L)` |
| Aggiunta in coda | `L.append(x)` |
| Conteggio occorrenze | `L.count(x)` |

> Anche qui si conta a partire da zero.

Conviene anche seguire una buona pratica importante:

- Python permette liste eterogenee;
- ma nella pratica conviene quasi sempre costruire liste omogenee.

Quindi, di norma, meglio:

- lista di interi;
- lista di stringhe;
- lista di booleani;

piuttosto che mescolare tutto senza motivo.

Il motivo e' pragmatico: e' piu' semplice applicare operazioni uniformi a tutti gli elementi se hanno lo stesso tipo.

Esempi:

```python
[1, 2, 3] + [4, 5, 6]

lista = [1, 2, 3]
lista.append(4)

["a", "b", "c"][0]
["a", "b", "c", "d", "e", "f"][1:4]

len([["a", "b"], ["a", "c"], ["a", "d"]])
len(["a", "b"])
```

---

## `split()` e prime trasformazioni

Una nuova operazione importante sulle stringhe e' questa:

```python
incipit = "Era una notte incantevole, una di quelle notti..."
parole = incipit.split()
print(parole)
```

`split()` prende una stringa e restituisce una lista di sottostringhe.

Questo passaggio e' fondamentale per molti problemi:

- tokenizzare testo;
- leggere parole una per volta;
- passare da un dato "compatto" a una struttura manipolabile.

Questo passaggio e' cosi' importante per chi lavora su testi perche':

- un file o una stringa ci arrivano inizialmente come sequenza di caratteri;
- ma per molte analisi linguistiche vogliamo lavorare parola per parola;
- quindi abbiamo bisogno di una struttura in cui `era`, `una`, `notte` siano elementi distinti.

Per questo `split()` e' uno dei primi ponti concreti tra:

- testo grezzo;
- lista di token;
- analisi successiva con cicli e conteggi.

### Esempio

```python
frase = "uno due tre quattro"
pezzi = frase.split()
print(pezzi)
```

Risultato:

```python
['uno', 'due', 'tre', 'quattro']
```

### Attenzione: `split()` taglia dove gli diciamo di tagliare

Un punto molto importante e' questo: l'unita' che otteniamo dipende dalla regola di segmentazione che stiamo usando.

Con `split()` senza argomenti:

- il taglio avviene sugli spazi;
- quindi `"La Spezia"` diventa due elementi se c'e' uno spazio in mezzo;
- mentre `"andata,"` resta un unico elemento, perche' la virgola non viene separata automaticamente.

Questo e' utile da capire subito perche':

- `split()` e' semplice e spesso basta per iniziare;
- ma non coincide ancora con una tokenizzazione linguistica raffinata.

---

<a id="mod5-input-lista"></a>
## Leggere dati e accumularli in lista

Una volta che sappiamo costruire liste, possiamo usarle per raccogliere dati in ingresso.

Schema tipico:

```python
numeri = []

for token in ["3", "5", "8"]:
    numeri.append(int(token))
```

Più avanti questo schema si combinera' con:

- lettura da standard input;
- lettura da file;
- cicli `while` con sentinella.

Per ora il punto chiave e' questo:

> una lista e' il contenitore naturale quando non sappiamo in anticipo quanti dati dovremo raccogliere.

---

<a id="mod5-redirezione"></a>
## Redirezione dell'input e sorgenti dei dati

Nel programma del corso il modulo 5 include anche la redirezione dell'input. Qui la prepariamo trattando dati testuali gia' disponibili come sequenze.

Concettualmente:

- la sorgente puo' essere la tastiera;
- puo' essere una stringa gia' caricata;
- puo' essere un file;
- il programma spesso trasforma comunque tutto in una lista di elementi da elaborare.

---

## Esercizi assegnati: input da file e sequenze

Nei testi degli esercizi assegnati compare un passaggio importante: usare un file come sorgente dello standard input invece dell'interazione diretta da tastiera.

Schema di riferimento:

```python
lista_numeri = []

number = int(input())
while number != 0:
    lista_numeri.append(number)
    number = int(input())

print("Numeri letti:", lista_numeri)
```

eseguito anche come:

```bash
python3 script.py < input.txt
```

Questo punto e' molto utile didatticamente perche' chiarisce che:

- `input()` non "sa" se i dati arrivano da tastiera o da file;
- il programma legge uno stream di righe;
- possiamo testare meglio i programmi preparando input ripetibili.

Due osservazioni pratiche molto utili:

- `input()` legge sempre testo, quindi se ci servono numeri dobbiamo convertire con `int(...)` o `float(...)`;
- il file passato con `<` non viene "capito" da Python come file speciale: per il programma e' semplicemente una sorgente di input riga per riga.

### Anche l'output si puo' ridirigere

Allo stesso modo possiamo salvare su file quello che normalmente vedremmo nel terminale:

```bash
python3 script.py < input.txt > output.txt
```

Qui:

- `< input.txt` fornisce l'input al programma;
- `> output.txt` salva in un file tutto cio' che il programma stampa su standard output.

Questo e' molto utile per:

- testare programmi senza dover digitare ogni volta gli input;
- confrontare facilmente l'output prodotto con quello atteso;
- conservare esempi di esecuzione ripetibili.

Queste redirezioni si possono anche combinare:

- il programma legge da uno stream di input;
- produce uno stream di output;
- il terminale decide se questi stream passano da tastiera/schermo oppure da file.

### Esercizi coerenti con il modulo 5

1. leggere una serie di numeri fino a `0` e memorizzarli per poi stamparli al contrario;
2. leggere parole fino a `fine` e contare quante iniziano per ciascuna vocale;
3. leggere 5 lettere iniziali e poi contare quante parole iniziano con ciascuna di esse;
4. leggere una serie di numeri dispari e per ciascuno stampare un rombo di asterischi.

Questi esercizi stanno bene qui perche' combinano:

- lettura sequenziale;
- sentinelle;
- accumulo in lista;
- trasformazione dell'input in una struttura dati.

---

## Esercizi suggeriti

1. Crea una lista di 5 parole e stampa il primo e l'ultimo elemento.
2. Data una lista di numeri, stampa la sua lunghezza.
3. Aggiungi un elemento in coda con `append`.
4. Data una frase, usa `split()` per ottenere la lista delle parole.
5. Scrivi un programma che costruisce una lista di numeri e ne stampa gli elementi in ordine inverso usando gli indici.
6. Leggi una sequenza di numeri da standard input o da file e salvala in una lista fino alla sentinella.
7. Leggi tre serie di numeri separate da `0` e stampa ogni serie al contrario.

---

## Riepilogo

Questo modulo raccoglie il nucleo sulle liste:

- definizione di lista come collezione ordinata;
- operazioni elementari;
- relazione tra stringhe e liste tramite `split()`;
- accumulo di dati in una struttura ordinata.
