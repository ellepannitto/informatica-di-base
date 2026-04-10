# Modulo 06 · Funzioni e procedure

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- definire funzioni con parametri e valore di ritorno;
- distinguere bene funzione e procedura;
- scomporre un problema in sottoproblemi piu' piccoli;
- progettare interfacce semplici e responsabilita' singole;
- leggere una funzione come black box;
- costruire piccole utility testabili e riusabili.

---

<a id="mod6-funzioni"></a>
## Perche' servono le funzioni

Le funzioni servono a evitare duplicazione, isolare un compito preciso e rendere il codice piu' leggibile.

Idea chiave:

- una funzione riceve input;
- esegue una trasformazione;
- restituisce un risultato.

Esempio:

```python
def triplo_del_successore(x):
    return 3 * (x + 1)
```

Quando il problema cresce, conviene quasi sempre chiedersi:

> quale parte del programma posso trasformare in una funzione autonoma?

Una metafora molto utile:

- una funzione e' una **delega**;
- non dobbiamo saper fare tutto da soli nel codice principale;
- dobbiamo anche saper decidere quale sottoproblema affidare a un blocco specializzato.

L'analogia usata a lezione era quella della costruzione di una casa:

- non fai tutto da solo;
- chiami l'ingegnere, l'idraulico, l'elettricista;
- a ciascuno dai gli input giusti;
- da ciascuno ricevi un risultato utile per il progetto complessivo.

In programmazione vale lo stesso principio:

- una funzione e' un pezzo di lavoro ben definito;
- puo' essere scritto da noi oppure da altri;
- saper programmare vuol dire anche saper riusare soluzioni gia' disponibili.

---

<a id="mod6-parametri"></a>
## Sintassi di `def`

Una funzione si definisce con `def` e si usa tramite chiamata.

```python
def area_rettangolo(base, altezza):
    return base * altezza

print(area_rettangolo(4, 6))
```

Parti da riconoscere:

- `def` introduce la definizione della funzione;
- il nome della funzione descrive il comportamento;
- tra parentesi compaiono i parametri;
- i due punti `:` aprono il blocco;
- `return` restituisce il risultato.

### Struttura generale

```python
def nome_funzione(parametro1, parametro2):
    # istruzioni
    return risultato
```

---

## Semantica di `def`

Qui:

- `base` e `altezza` sono parametri;
- `4` e `6` sono argomenti concreti;
- `return` consegna il risultato al chiamante.

Questo modello e' fondamentale per poter comporre programmi piu' grandi a partire da blocchi affidabili.

Va distinta con forza la differenza tra:

- **definizione** della funzione;
- **invocazione** della funzione.

Definire una funzione significa salvare da qualche parte un comportamento riusabile.
Invocarla significa usarla davvero con valori concreti.

Esempio discusso a lezione:

```python
def triplo_del_successore(x):
    successore = x + 1
    triplo = 3 * successore
    return triplo
```

Quando poi scriviamo:

```python
triplo_del_successore(15)
```

non stiamo piu' parlando in astratto: stiamo chiedendo alla funzione di lavorare davvero sul valore `15`.

### Parametri ipotetici e argomenti reali

Questa distinzione e' importante:

- nella definizione usiamo nomi come `x`, `planimetria`, `budget`;
- nella chiamata passiamo valori concreti;
- i nomi dei parametri non devono per forza essere `x`, `y`, `z`;
- conviene scegliere nomi che facciano capire il ruolo di ogni input.

Ci sono anche due buone pratiche molto concrete.

---

## Sintassi di `return`

Forma tipica:

```python
return espressione
```

Esempi:

```python
return triplo
return base * altezza
return True
```

`return` compare dentro il blocco della funzione.

---

## Semantica di `return`

Quando Python esegue `return`:

1. valuta l'espressione dopo `return`;
2. produce quel valore come risultato della funzione;
3. interrompe l'esecuzione del corpo della funzione;
4. restituisce il controllo al chiamante.

Per questo tutto cio' che sta dopo un `return` nello stesso ramo non viene eseguito.

### Commentare che cosa fa una funzione

Dopo una definizione conviene lasciare almeno traccia di:

- che cosa fa la funzione;
- che cosa si aspetta in input;
- che cosa restituisce in output.

Questo e' utile perche' un nome di parametro da solo non garantisce abbastanza contesto, soprattutto quando il codice cresce.

### Evitare collisioni inutili di nomi

C'e' anche una domanda utile:

- che succede se usiamo per una nostra funzione un nome gia' occupato da una funzione importata?

Il punto didattico da trattenere e' questo:

- quando importiamo librerie, aggiungiamo al nostro ambiente molti nomi gia' esistenti;
- se riusiamo gli stessi nomi senza accorgercene, il codice diventa piu' ambiguo e fragile;
- conviene quindi scegliere nomi chiari e non in conflitto con funzioni gia' importanti del linguaggio o delle librerie usate.

Quindi:

```python
def area(base, altezza):
    return base * altezza
```

e' meglio di una versione con parametri chiamati in modo oscuro, se il problema non e' puramente astratto.

---

## Memoria locale della funzione

Una prima idea di **memoria locale** e' questa:

- quando una funzione viene chiamata, immaginiamo che riceva una tabella di memoria separata;
- dentro quella tabella vivono i parametri e le variabili locali della funzione;
- quando arriviamo a `return`, il valore torna al chiamante e quella memoria locale puo' essere considerata chiusa.

Questo modello e' didatticamente molto utile per leggere correttamente le chiamate di funzione nei casi elementari.

Per leggere correttamente una chiamata come:

```python
n = 15
risultato = triplo_del_successore(n)
```

conviene pensare cosi':

1. il programma principale ha la sua memoria;
2. la funzione riceve il valore `15` come input del parametro `x`;
3. dentro la funzione si calcolano `successore` e `triplo`;
4. `return triplo` restituisce `48`;
5. il programma principale assegna `48` a `risultato`.

Questo schema aiuta moltissimo quando iniziano i dubbi su:

- "quale `x` sto usando?"
- "dove e' stata creata questa variabile?"
- "perche' il valore restituito non coincide con il nome usato dentro la funzione?"

---

## Indentazione e blocchi

La lezione chiudeva l'introduzione alle funzioni con un punto sintattico fondamentale:

- il corpo della funzione deve essere indentato;
- in Python l'indentazione non e' estetica, ma parte della sintassi;
- di solito un editor/IDE la inserisce automaticamente, ma va comunque capita.

Esempio:

```python
def triplo_del_successore(n):
    successore = n + 1
    triplo = 3 * successore
    return triplo
```

Qui tutto cio' che appartiene alla funzione e' rientrato di un livello.

Questo serve a far capire all'interprete:

- dove inizia il blocco della funzione;
- dove finisce;
- quali istruzioni appartengono a quel sottoproblema e non al programma principale.

---

<a id="mod6-black-box"></a>
## Firma e black box

Nel programma del corso il modulo 6 insiste sulla lettura delle funzioni come **black box**.

Una funzione andrebbe capita almeno a questo livello:

- che cosa riceve;
- che cosa restituisce;
- quale problema risolve;
- che cosa non deve fare.

Per esempio:

```python
def is_palindroma(s):
    ...
```

ci interessa leggere la firma come:

- input: una stringa `s`
- output: `True` oppure `False`

senza dover ragionare subito su ogni dettaglio interno.

---

<a id="mod6-procedure"></a>
## Funzioni vs procedure

Una distinzione pratica utile:

- una **funzione** restituisce un valore;
- una **procedura** produce soprattutto un effetto, per esempio una stampa.

Esempio di funzione:

```python
def successore(x):
    return x + 1
```

Esempio di procedura:

```python
def saluta(nome):
    print("Ciao", nome)
```

La differenza conta quando vogliamo:

- riusare un risultato in altre espressioni;
- testare il comportamento;
- separare logica e presentazione.

---

<a id="mod6-esercizi-funzioni"></a>
## Esercizi assegnati: ricostruire `strip` e `join`

Tra gli esercizi gia' assegnati ce ne sono due molto adatti a questo modulo, perche' obbligano a progettare bene comportamento e responsabilita' della funzione.

### 1. Ricostruire `strip`

Leggere:

- una stringa iniziale;
- poi una sequenza di caratteri da rimuovere, uno per riga;
- la sequenza termina con riga vuota.

Obiettivo:

- rimuovere dall'inizio e dalla fine della stringa tutti i caratteri appartenenti all'insieme letto;
- senza usare `strip()`.

Questo esercizio e' utile perche' costringe a distinguere:

- bordo sinistro e bordo destro;
- condizione di arresto;
- caratteri interni che non vanno toccati.

### 2. Ricostruire `join`

Leggere:

- una stringa separatore;
- poi una sequenza di parole, una per riga;
- fermarsi quando compare `fine`.

Obiettivo:

- costruire la stringa finale senza usare `join()`.

Questo esercizio e' molto formativo perche' fa emergere subito un problema classico:

- come evitare un separatore in piu' all'inizio o alla fine.

Il contratto del problema si puo' chiarire cosi':

- la consegna va letta soprattutto come relazione tra input e output;
- la prima riga letta e' il separatore;
- le righe successive sono le parole da unire;
- `fine` serve solo a terminare la lettura e non va inserito nel risultato.

Questo aiuta a distinguere due sottoproblemi:

1. leggere correttamente i dati;
2. costruire la stringa finale senza separatore in eccesso.

Una buona osservazione di metodo:

- `split`, `strip` e `join` non si imparano solo "a memoria";
- conviene leggere la documentazione e capire su quale oggetto vivono;
- per esempio `"-".join(lista)` e non `lista.join("-")`, semplicemente perche' in Python quel metodo e' definito sulla stringa separatore.

Questo non va preso come un fatto metafisico, ma come una convenzione concreta del linguaggio:

- alcune operazioni sono metodi delle stringhe;
- altre sono funzioni globali;
- parte del lavoro del programmatore e' capire quale interfaccia espone l'oggetto che sta usando.

Questi esercizi servono anche a ricordare che:

- ricostruire `strip` o `join` non serve solo a copiare un metodo gia' esistente;
- serve a capire che comportamento preciso ci aspettiamo;
- e quindi a progettare meglio la funzione prima ancora di scriverla.

---

## Import e file di libreria

Qui conviene introdurre anche un passaggio utile:

- un file Python puo' contenere codice da eseguire subito;
- ma puo' anche contenere funzioni, costanti o strutture dati da riusare altrove;
- in questo secondo caso lo trattiamo come una piccola libreria locale.

Schema minimo:

```python
# mialib.py

def somma1(x):
    return x + 1
```

```python
# main.py

import mialib

print(mialib.somma1(4))
```

---

## Sintassi di `import`

Forma base:

```python
import nome_modulo
```

Esempi:

```python
import sys
import mialib
```

---

## Semantica di `import`

Quando Python esegue `import nome_modulo`:

1. cerca il modulo richiesto;
2. lo carica;
3. rende disponibile quel nome nell'ambiente corrente.

Dopo:

```python
import mialib
```

possiamo accedere agli oggetti del modulo con il prefisso:

```python
mialib.somma1(4)
```

Punti chiave:

- il nome della libreria coincide con il nome del file senza `.py`;
- `import mialib` rende disponibili gli oggetti definiti in quel file;
- il prefisso `mialib.` evita collisioni tra nomi uguali provenienti da file diversi.

Questo si collega bene a una buona pratica gia' vista:

- non dare per scontato che nomi come `len`, `print` o altri identificatori importanti siano sempre liberi;
- quando usiamo librerie, il namespace conta.

### Perche' stanno bene nel modulo 6

Questi esercizi sono ideali come funzioni del tipo:

```python
def my_strip(s, chars):
    ...

def my_join(separatore, parole):
    ...
```

perche' permettono di:

- definire un contratto chiaro;
- testare casi normali e casi limite;
- riusare la soluzione in programmi diversi.

---

## Soluzioni commentate: palindromi e normalizzazione

Tra le soluzioni svolte compaiono due idee molto utili per questo modulo.

### `is_palindroma` come funzione di confronto simmetrico

Una soluzione efficace controlla la stringa solo fino a meta':

```python
condizione = True

for i in range(len(parola) // 2):
    if parola[i] != parola[-1 - i]:
        condizione = False
```

Il punto didattico importante non e' solo il risultato, ma il ragionamento:

- confrontiamo posizioni speculari;
- non serve scorrere tutta la stringa;
- possiamo fermarci concettualmente a meta'.

Questa e' una base molto buona per una funzione:

```python
def is_palindroma(s):
    ...
```

### Separare normalizzazione e controllo

In un'altra soluzione, prima di controllare il palindromo si normalizza la stringa:

- conversione in minuscolo;
- rimozione di spazi;
- rimozione di punteggiatura e apostrofi.

Questo insegna una distinzione cruciale:

- una funzione puo' preparare il dato;
- un'altra puo' verificare la proprieta' richiesta.

E' un ottimo esempio di scomposizione in sottoproblemi:

1. `normalizza_testo(s)`
2. `is_palindroma(s)`

---

## Esercizi suggeriti per la scomposizione in funzioni

1. scrivi una funzione che restituisce il massimo di una lista di interi positivi;
2. scrivi `is_palindroma(s)` che ignora maiuscole e spazi;
3. scrivi `conta_vocali(s)`;
4. scrivi `stampa_rettangolo(base, altezza)` come procedura;
5. riscrivi un programma lungo dividendolo in funzioni piccole con un solo compito.

---

## Riepilogo

Questo modulo raccoglie il materiale necessario per:

- definire funzioni con parametri e `return`;
- distinguere funzione e procedura;
- ragionare in termini di firma e black box;
- progettare utility riusabili;
- usare esercizi come `my_strip` e `my_join` per consolidare astrazione e testing.
