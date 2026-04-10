# Lezione · Testing e casi limite

---

## Obiettivi della lezione

Al termine di questa lezione saprai:

- distinguere tra programma che va in errore e programma che produce un risultato sbagliato;
- scegliere casi di test piccoli e controllabili;
- riconoscere casi normali, casi limite e casi anomali;
- usare il testing per leggere meglio il comportamento del programma.

---

## Perche' testare

Un programma non e' corretto solo perche' "parte".

Due casi diversi:

- il programma va in errore esplicito;
- il programma gira, ma il risultato non e' quello voluto.

Il secondo caso e' spesso piu' insidioso.

Per questo conviene sempre chiedersi:

- quali input voglio provare;
- quale output mi aspetto;
- che cosa succede davvero quando eseguo il programma.

---

## Tre tipi di casi

| Tipo di caso | Significato | Esempio |
| --- | --- | --- |
| Normale | input previsto e regolare | lista con alcuni numeri |
| Limite | input valido ma delicato | lista vuota, zero, stringa di lunghezza 1 |
| Anomalo | input non previsto o problematico | testo al posto di un numero |

Questa distinzione serve a non fermarsi al primo esempio che funziona.

---

## Metodo minimo di testing

1. scegli un input piccolo;
2. scrivi l'output atteso;
3. esegui il programma;
4. confronta il risultato reale con quello previsto;
5. se modifichi il codice, ripeti gli stessi test.

L'idea importante e' che il test non arriva alla fine come formalita': accompagna la scrittura del programma.

---

## Perche' iniziare da input piccoli

Se un input e' troppo grande:

- non riesci piu' a seguirlo a mano;
- diventa difficile capire in quale punto nasce l'errore;
- il programma sembra opaco.

Meglio partire da casi ridotti:

- tre numeri;
- una stringa molto corta;
- una lista di lunghezza `0`, `1` o `2`.

---

## Esempio: massimo di una lista

Se vuoi progettare una funzione che restituisce il massimo di una lista, non basta provare:

```python
[3, 8, 2]
```

Devi chiederti anche:

- che cosa succede con `[]`?
- che cosa succede con `[4]`?
- che cosa succede con `[-3, -7, -1]`?

Qui i casi limite aiutano a decidere meglio il comportamento della funzione prima ancora di scriverla.

---

## Esempio: numeri che seguono uno zero

Problema:

> data una lista di interi, restituire tutti i numeri che seguono uno `0`

Caso normale:

```python
[3, 5, 0, 7, 0, -3, 8]
```

Output atteso:

```python
[7, -3]
```

Casi importanti:

- `[]`
- `[0]`
- `[0, 4]`
- `[5, 0]`
- `[0, 0, 2]`

Questi casi mostrano subito dove un programma puo' sbagliare, soprattutto se assume che esista sempre un elemento successivo.

---

## Stampare valori intermedi

Quando il comportamento non e' chiaro, conviene osservare lo stato interno.

Per esempio:

```python
for x in numeri:
    print("sto leggendo:", x)
```

Oppure:

```python
print(lista_risultato)
```

Stampare valori intermedi aiuta a capire:

- che cosa entra davvero nelle strutture dati;
- in quale passo compare l'errore;
- se il programma sta seguendo il percorso che immaginavamo.

---

## Esercizi

1. Per un programma che stampa il doppio di un numero, scrivi due casi normali, due casi limite e un caso anomalo.
2. Per una funzione che controlla se una stringa e' vuota, elenca i casi da provare.
3. Per il problema dei numeri che seguono uno zero, costruisci una batteria minima di test.
4. Prendi un frammento di codice sbagliato e prova a prevedere dove fallira' prima di eseguirlo.

---

## Riepilogo

Testing significa:

- scegliere casi significativi;
- confrontare output atteso e output reale;
- usare casi normali, limite e anomali;
- leggere meglio il programma attraverso esempi piccoli.
