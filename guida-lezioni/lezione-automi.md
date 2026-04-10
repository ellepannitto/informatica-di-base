# Lezione · Automi a stati finiti

---

## Obiettivi della lezione

Al termine di questa lezione saprai:

- descrivere un piccolo problema decisionale in termini di stati;
- distinguere tra stato corrente, input e stato successivo;
- leggere un `if` o un ciclo come aggiornamento dello stato;
- usare tabelle di transizione molto semplici.

---

## Idea di base

Un automa a stati finiti e' un modello molto semplice per descrivere un programma che:

- si trova in uno stato;
- riceve un input;
- decide come cambiare stato.

Gli ingredienti minimi sono:

- un insieme di stati possibili;
- un input osservato;
- una regola di transizione;
- eventualmente un output.

---

## Esempio intuitivo

Immagina un programma che deve validare una risposta `s` oppure `n`.

Possiamo descriverlo cosi':

| Stato corrente | Input | Stato successivo |
| --- | --- | --- |
| `attesa` | `s` | `confermato` |
| `attesa` | `n` | `annullato` |
| `attesa` | altro | `attesa` |

Questa tabella dice:

- se arriva un input valido, il programma cambia stato;
- se arriva un input non valido, resta nello stato di attesa.

---

## Collegamento con `if`

Anche un semplice `if` puo' essere letto come un piccolo automa.

```python
if risposta == "s":
    stato = "confermato"
else:
    stato = "attesa"
```

Qui:

- `stato` rappresenta la situazione corrente del programma;
- la condizione controlla l'input;
- l'assegnamento aggiorna lo stato.

---

## Collegamento con `while`

Il modello degli automi diventa ancora piu' naturale con `while`.

```python
stato = "attesa"

while stato == "attesa":
    risposta = input("s/n: ")
    if risposta == "s":
        stato = "confermato"
    elif risposta == "n":
        stato = "annullato"
```

Qui il programma:

- continua finche' resta nello stato `attesa`;
- esce quando lo stato cambia.

---

## Perche' sono utili

Gli automi aiutano a:

- separare i casi possibili;
- capire quando il programma deve restare nello stesso stato;
- progettare meglio programmi interattivi e controlli di validazione;
- leggere con piu' chiarezza il rapporto tra condizione e aggiornamento.

---

## Esempio: controllo di una parola

Supponi di voler controllare se un input appartiene all'insieme:

- `si`
- `no`

Una descrizione possibile e':

| Stato corrente | Input | Stato successivo | Output |
| --- | --- | --- | --- |
| `attesa` | `si` | `valido` | accetta |
| `attesa` | `no` | `valido` | accetta |
| `attesa` | altro | `attesa` | ripeti la richiesta |

Questo rende esplicita una cosa importante:

- non tutti gli input fanno avanzare il programma;
- alcuni fanno semplicemente ripetere lo stesso controllo.

---

## Errori tipici

Quando si usa questo modello, gli errori frequenti sono:

- dimenticare di aggiornare lo stato;
- aggiornare lo stato sbagliato;
- avere transizioni mancanti;
- uscire dal ciclo troppo presto o troppo tardi.

Per questo conviene sempre chiedersi:

- qual e' lo stato iniziale?
- quali input sono ammessi?
- quando il programma deve restare fermo?
- quando il programma deve cambiare stato?

---

## Esercizi

1. Descrivi come automa il controllo di un input `y/n`.
2. Costruisci una tabella di transizione per un programma che continua a chiedere un numero finche' non riceve un valore positivo.
3. Scrivi un piccolo `while` che implementa uno degli automi descritti.
4. Individua un caso in cui il programma resta bloccato perche' lo stato non viene aggiornato.

---

## Riepilogo

Un automa a stati finiti descrive un programma come:

- stato corrente;
- input osservato;
- regola di transizione;
- stato successivo.

Serve soprattutto a leggere e progettare meglio condizioni, validazioni e piccoli cicli interattivi.
