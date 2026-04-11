# Modulo 07 · Memoria e passaggio degli argomenti

---

## Autovalutazione

- Sai distinguere tra variabili semplici e strutture mutabili?
- Sai spiegare cosa succede quando due nomi puntano alla stessa lista?
- Sai riconoscere effetti collaterali e modifiche in-place?
- Sai usare copie esplicite quando serve isolare i dati?

---

<a id="mod7-memoria-liste"></a>
## Liste e memoria: il caso speciale

Il passaggio cruciale e' da:

```python
a = 1
b = a
```

a:

```python
a = [1, 2, 3]
b = a
```

Nel primo caso i due nomi contengono semplicemente lo stesso valore intero.
Nel secondo caso i due nomi fanno riferimento alla **stessa lista** in memoria.

### Modello intuitivo

| Nome | Valore |
| --- | --- |
| `a` | lista in memoria |
| `b` | stessa lista in memoria |

Questo significa che modificare la lista tramite uno dei due nomi modifica l'oggetto condiviso.

---

## Alias e modifiche condivise

Esempio classico:

```python
a = [1, 2, 3]
b = a

print("Lista a:", a)
print("Lista b:", b)

b[0] = 1000

print("Lista a:", a)
print("Lista b:", b)
```

Output concettuale:

- prima: entrambe mostrano `[1, 2, 3]`
- dopo: entrambe mostrano `[1000, 2, 3]`

Perche'?

Perche' `a` e `b` non sono due liste diverse. Sono due nomi per la stessa lista.

La seconda lezione spiegava questo fenomeno in termini di memoria:

- nella tabella delle variabili, per una lista non viene memorizzato direttamente tutto il contenuto;
- viene memorizzato un riferimento a una zona di memoria dove quella lista vive;
- quindi con `b = a` non stiamo duplicando la lista, stiamo duplicando quel riferimento.

Una metafora ancora piu' concreta:

- per un valore semplice come un intero possiamo immaginare un cassetto che contiene direttamente il valore;
- per una lista il cassetto contiene soprattutto un indirizzo;
- il contenuto vero della lista vive altrove, in una zona di memoria dedicata che puo' crescere.

Per questo:

- copiare un intero significa copiare il valore;
- copiare una lista con `=` significa copiare il riferimento al suo indirizzo.

Questo spiega perche' una modifica fatta tramite `b` resta visibile anche tramite `a`.

---

<a id="mod7-copie"></a>
## Copie e isolamento dei dati

Quando vuoi evitare aliasing, devi costruire una copia.

Serve anche l'uso di `copy`:

```python
import copy

a = [1, 2, 3]
b = copy.deepcopy(a)
```

Nel modello introduttivo del corso, il punto importante e' questo:

- assegnare `b = a` non copia;
- copiare significa creare un nuovo oggetto indipendente.

Il punto si vede bene con:

```python
a = [1, 2, 3]
b = a
b[0] = 1000
```

e poi con la versione corretta:

```python
import copy

a = [1, 2, 3]
b = copy.deepcopy(a)
b[0] = 1000
```

Nel secondo caso:

- `a` resta `[1, 2, 3]`;
- `b` diventa `[1000, 2, 3]`.

Questo e' uno dei passaggi piu' importanti per evitare bug difficili da vedere.

### Regola pratica

Se devi modificare una lista senza toccare l'originale, chiediti sempre:

> sto usando un secondo nome per la stessa lista oppure una vera copia?

---

## Collegamento con il passaggio degli argomenti

Quando una lista viene passata a una funzione, il comportamento osservabile assomiglia a quello dell'aliasing:

- la funzione riceve un accesso allo stesso oggetto;
- una modifica in-place puo' essere visibile anche fuori;
- per questo bisogna distinguere con cura tra lettura, modifica e copia.

Questo modulo estende proprio quell'intuizione.

---

## Esercizi suggeriti

1. Scrivi un programma con:

```python
a = [1, 2, 3]
b = a
b[1] = 99
print(a)
print(b)
```

Predici l'output prima di eseguirlo.

2. Ripeti l'esercizio usando una copia esplicita.
3. Scrivi una funzione che modifica il primo elemento di una lista e osserva se il cambiamento resta visibile fuori dalla funzione.

---

## Riepilogo

Questo modulo raccoglie la parte sulle liste e la memoria:

- differenza tra valori immutabili e liste mutabili;
- aliasing;
- modifiche condivise;
- copie come strumento per evitare effetti collaterali inattesi.
