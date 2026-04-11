# Modulo 03 · Stato del programma e strutture decisionali

---

## Autovalutazione

- Sai tracciare lo stato del programma durante l'esecuzione?
- Sai riconoscere errori frequenti e localizzarli?
- Sai usare casi di test per smascherare errori logici?
- Sai usare condizioni composte con attenzione?
- Sai applicare le leggi di De Morgan?
- Sai modellare piccoli problemi con automi a stati finiti?
- Sai ragionare sui casi limite anche quando il codice sembra plausibile a prima vista?

---

<a id="mod3-testing"></a>
## Testing e casi limite

Il modulo si apre con un richiamo esplicito all'importanza del **testing**.

L'idea chiave e' semplice:

- non basta che un programma funzioni su un caso "normale";
- bisogna controllare casi piccoli, casi strani e casi limite;
- proprio i casi limite fanno emergere gli errori che altrimenti restano nascosti.

Domande tipiche:

- che cosa succede se la lista e' vuota?
- che cosa succede se la stringa ha lunghezza 1?
- che cosa succede se il valore e' zero?
- che cosa succede se due casi diversi finiscono sullo stesso ramo?

### Esempio

Se scrivi una funzione che restituisce l'elemento massimo di una lista, il caso:

```python
[]
```

non e' un dettaglio secondario. E' un caso che il programma deve decidere come trattare.

### Esercizi: trova l'errore

Ci sono anche esercizi specifici di debugging:

- leggere il codice;
- prevedere dove fallisce;
- costruire input che mostrino il problema;
- correggere il comportamento.

Questo approccio e' perfettamente coerente con il lavoro del modulo: tracciamento, condizioni e controllo dei casi limite.

La terza lezione trascritta rendeva questo punto ancora piu' operativo.

### Che cosa vuol dire testare davvero

L'idea proposta a lezione era molto concreta:

- anche se il programma non va in errore, potrebbe comunque fare la cosa sbagliata;
- quindi non basta "farlo partire";
- bisogna confrontare input e output attesi su casi scelti apposta.

Metodo minimo suggerito:

1. scegli input piccoli e controllabili a mano;
2. scrivi quale output ti aspetti;
3. esegui il programma;
4. confronta il risultato reale con quello previsto;
5. se modifichi il codice, rifai gli stessi test.

Questa pratica vale soprattutto quando iniziamo a lavorare su:

- liste;
- file;
- corpus o dataset lunghi;
- funzioni che sembrano plausibili ma nascondono errori logici.

### Perche' iniziare da input piccoli

Conviene insistere anche su un principio molto pragmatico:

- non si testa subito su un corpus enorme;
- si parte da una versione ridotta che possiamo seguire a mano;
- solo dopo si scala a input piu' grandi.

Questo serve perche' su migliaia di righe non possiamo piu' controllare facilmente se l'output e' corretto, mentre su tre o quattro casi scelti bene possiamo ancora capire davvero che cosa sta succedendo.

### Stampare variabili intermedie

Un altro consiglio esplicito emerso in lezione:

- se stiamo costruendo una lista o una struttura dati;
- conviene stampare valori intermedi per vedere se ci stanno finendo dentro proprio gli elementi giusti.

Questo e' un modo semplice ma molto efficace per diagnosticare errori prima che diventino invisibili.

---

<a id="mod3-tracciamento"></a>
## Tracciamento dello stato

Quando un programma usa variabili e condizioni, la domanda chiave diventa:

> qual e` lo stato del programma in questo punto?

Lo stato e` l'insieme dei valori che le variabili hanno in un certo momento.

Esempio:

```python
x = 8
y = x - 3
if y > 4:
    z = y * 2
else:
    z = 0
print(z)
```

Traccia:

| Passo | Stato | Nota |
| --- | --- | --- |
| `x = 8` | `x = 8` | |
| `y = x - 3` | `x = 8`, `y = 5` | |
| `y > 4` | `x = 8`, `y = 5` | condizione vera |
| `z = y * 2` | `x = 8`, `y = 5`, `z = 10` | ramo `if` |
| `print(z)` | `x = 8`, `y = 5`, `z = 10` | output `10` |

---

<a id="mod3-calcoli-conversioni"></a>
## Calcoli, conversioni e stato

Molti errori iniziali non sono di sintassi ma di stato: il programma gira, ma usa valori diversi da quelli immaginati.

Esempio:

```python
prezzo = input("Prezzo: ")
sconto = 5
totale = prezzo - sconto
```

Questo non funziona perche` `prezzo` e` una stringa. La versione corretta e`:

```python
prezzo = int(input("Prezzo: "))
sconto = 5
totale = prezzo - sconto
```

La sequenza giusta da controllare e`:

1. che tipo ha ogni input;
2. come cambia lo stato dopo ogni assegnamento;
3. che tipo richiede ogni operazione.

---

<a id="mod3-errori"></a>
## Primi messaggi di errore

Un messaggio di errore contiene almeno tre informazioni utili:

| Informazione | Domanda |
| --- | --- |
| tipo di errore | che genere di problema e`? |
| riga segnalata | dove si manifesta? |
| contesto | quale operazione stava tentando Python? |

Esempi frequenti:

| Errore | Causa tipica |
| --- | --- |
| `SyntaxError` | sintassi non valida |
| `NameError` | nome di variabile non definito |
| `TypeError` | operazione tra tipi incompatibili |
| `ValueError` | conversione non possibile |

Metodo minimo:

1. leggi il tipo di errore;
2. trova la riga;
3. controlla i tipi e i valori coinvolti;
4. riduci il caso a un esempio piu` piccolo.

Una distinzione importante e' questa:

- un errore esplicito dell'interprete e' spesso il caso piu' semplice da affrontare;
- il caso piu' insidioso e' quando il programma gira ma il comportamento non coincide con cio' che volevamo.

Per questo leggere un messaggio di errore resta necessario, ma non esaurisce il lavoro di verifica del programma.

---

<a id="mod3-boolean-logica"></a>
## Condizioni composte e leggi di De Morgan

Le condizioni possono essere combinate con:

- `and`
- `or`
- `not`

Esempio:

```python
eta = 20
ha_documento = True

if eta >= 18 and ha_documento:
    print("Accesso consentito")
```

Le **leggi di De Morgan** servono a riscrivere negazioni di condizioni composte:

| Forma | Equivalente |
| --- | --- |
| `not (A and B)` | `not A or not B` |
| `not (A or B)` | `not A and not B` |

Esempio:

```python
not (x > 0 and y > 0)
```

equivale a:

```python
x <= 0 or y <= 0
```

Questa riscrittura e` utile per controllare meglio casi limite e semplificare il ragionamento.

---

## Casi e tabelle di verita'

Tra i materiali svolti compare anche un modo molto utile di preparare un esercizio prima ancora di scrivere il codice: costruire i **casi**.

Esempio:

| Eta' attuale | Eta' da raggiungere | Comportamento |
| --- | --- | --- |
| `< 0` | `<= 0` | impossibile |
| `< 0` | `> 0` | eta' negativa non valida |
| `>= 0` | `<= 0` | caso assurdo nel modello |
| `>= 0` | `> 0` | procedi con il messaggio corretto |

Questo approccio e' prezioso perche' costringe a separare:

- casi impossibili;
- casi di errore;
- casi normali;
- casi limite.

Nei materiali di supporto ricompaiono anche le tavole di verita' di:

- `and`
- `or`
- `not`

Non come teoria astratta, ma come strumento per capire davvero quando una condizione composta vale `True` oppure `False`.

---

<a id="mod3-automi"></a>
## Automi a stati finiti

Un automa a stati finiti e` un modello semplice per descrivere un programma che cambia comportamento in base allo stato corrente e a un input.

Componenti:

- un insieme di stati;
- un input osservato;
- regole di transizione;
- eventualmente un output.

Esempio intuitivo: validare una risposta `s` o `n`.

| Stato corrente | Input | Stato successivo |
| --- | --- | --- |
| attesa | `s` | confermato |
| attesa | `n` | annullato |
| attesa | altro | attesa |

Anche un semplice `if` puo` essere letto come un minuscolo automa:

- osserva una condizione;
- sceglie un ramo;
- aggiorna lo stato del programma.

---

<a id="mod3-casi-limite"></a>
## Verifica del codice e casi limite

Un frammento di codice puo` sembrare plausibile e restare comunque sbagliato.

Per questo va controllato con:

- tracciamento a mano;
- casi normali;
- casi limite;
- casi anomali.

Esempio molto utile:

> data una lista di interi, restituire tutti i numeri che seguono uno `0`

Su un caso normale come:

```python
[3, 5, 0, 7, 0, -3, 8]
```

potremmo aspettarci:

```python
[7, -3]
```

Ma i casi davvero interessanti sono altri:

- che cosa succede se la lista e' vuota?
- che cosa succede se `0` e' l'ultimo elemento?
- che cosa succede se ci sono due zeri consecutivi?
- che cosa succede se la lista ha un solo elemento?

Questo esempio e' ottimo perche' mostra che:

- il caso vuoto puo' anche andare bene senza errore;
- un accesso alla posizione successiva puo' invece fallire se `0` e' in ultima posizione;
- alcuni casi non sono "errori" ma scelte progettuali da esplicitare.

### Leggere il codice prima ancora di eseguirlo

Nella lezione veniva proposto anche un esercizio molto utile:

- prendere codice intenzionalmente sbagliato;
- leggerlo a occhio;
- provare a prevedere dove fallira';
- solo dopo copiarlo nell'editor per verificare.

Questo allena due competenze che tornano continuamente:

- debugging;
- previsione del comportamento del programma.

### Anche un solo elemento puo' essere un caso limite

Vale esplicitamente anche questo:

- una lista con un solo elemento puo' essere un caso limite;
- se il programma assume implicitamente che esista sempre un "successivo", puo' rompersi proprio li'.

Questa e' una buona regola generale:

> quando un programma usa posizioni vicine, chiediti sempre che cosa accade su liste vuote, liste di lunghezza 1 e ultimo elemento.

Esempio:

```python
if voto > 18:
    print("superato")
else:
    print("non superato")
```

Domanda giusta: che cosa succede con `18`?

Qui il bug non e` sintattico. E` un errore di specifica o di condizione.

---

## Esercizi suggeriti

1. Traccia a mano questo codice:

```python
x = 4
y = 9
if x * 2 < y:
    y = y - 1
else:
    y = y + 1
print(y)
```

2. Riscrivi usando De Morgan:

- `not (a > 0 and b > 0)`
- `not (nome == "" or eta < 18)`

3. Spiega che cosa non va in ciascun frammento:

```python
numero = input("Numero: ")
print(numero + 1)
```

```python
if x = 3:
    print("ok")
```

4. Modella come piccolo automa un programma che legge un voto e lo classifica in `insufficiente`, `sufficiente`, `buono`.

---

## Riepilogo

In questo modulo hai consolidato il ragionamento sullo stato del programma:

- valori e tipi devono restare coerenti;
- le condizioni vanno tracciate e verificate;
- gli errori si leggono, non si ignorano;
- le condizioni composte si possono trasformare;
- un problema decisionale puo` essere descritto come automa.
