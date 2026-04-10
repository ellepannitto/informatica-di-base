# Lezione · Leggi di De Morgan

---

## Obiettivi della lezione

Al termine di questa lezione saprai:

- leggere correttamente condizioni con `and`, `or` e `not`;
- riscrivere una negazione di condizione composta in forma equivalente;
- usare le leggi di De Morgan per semplificare test e controlli;
- verificare con casi concreti che due condizioni sono davvero equivalenti.

---

## Punto di partenza

Le condizioni composte compaiono molto presto nei programmi.

Esempio:

```python
if eta >= 18 and ha_documento:
    print("Accesso consentito")
```

Qui stiamo combinando due condizioni semplici:

- `eta >= 18`
- `ha_documento`

con l'operatore `and`.

Quando entra in gioco `not`, la lettura diventa meno immediata.

Per esempio:

```python
not (eta >= 18 and ha_documento)
```

Questa forma e' corretta, ma spesso e' piu' utile riscriverla in una forma che faccia vedere meglio i casi in cui la condizione vale.

---

## Le leggi di De Morgan

Le due leggi fondamentali sono queste:

| Forma | Equivalente |
| --- | --- |
| `not (A and B)` | `not A or not B` |
| `not (A or B)` | `not A and not B` |

Il punto importante e' che:

- la negazione "entra" dentro le due parti;
- l'operatore logico cambia:
  - da `and` a `or`
  - da `or` a `and`

---

## Primo caso: negare un `and`

Partiamo da:

```python
not (x > 0 and y > 0)
```

Applicando De Morgan otteniamo:

```python
x <= 0 or y <= 0
```

Questa seconda forma e' spesso piu' leggibile, perche' dice esplicitamente:

- oppure `x` non e' positivo;
- oppure `y` non e' positivo.

### Verifica con casi concreti

| `x` | `y` | `x > 0 and y > 0` | `not (x > 0 and y > 0)` | `x <= 0 or y <= 0` |
| --- | --- | --- | --- | --- |
| `3` | `4` | `True` | `False` | `False` |
| `3` | `0` | `False` | `True` | `True` |
| `-1` | `4` | `False` | `True` | `True` |
| `-1` | `0` | `False` | `True` | `True` |

Le ultime due colonne coincidono sempre.

---

## Secondo caso: negare un `or`

Partiamo da:

```python
not (voto < 18 or assente)
```

Applicando De Morgan otteniamo:

```python
voto >= 18 and not assente
```

Questa forma rende piu' chiaro quando il test vale:

- il voto deve essere almeno sufficiente;
- e la persona non deve essere assente.

### Verifica con casi concreti

| `voto < 18` | `assente` | `voto < 18 or assente` | `not (...)` | `voto >= 18 and not assente` |
| --- | --- | --- | --- | --- |
| `True` | `True` | `True` | `False` | `False` |
| `True` | `False` | `True` | `False` | `False` |
| `False` | `True` | `True` | `False` | `False` |
| `False` | `False` | `False` | `True` | `True` |

---

## Errore tipico

Un errore molto comune e' questo:

```python
not (A and B) == not A and not B
```

Questa riscrittura e' sbagliata.

La forma corretta e':

```python
not (A and B) == not A or not B
```

Allo stesso modo:

```python
not (A or B) == not A and not B
```

Per non sbagliare:

1. fai entrare `not` nelle due parti;
2. cambia `and` con `or`, oppure `or` con `and`.

---

## Precedenza tra `and` e `or`

Quando una condizione contiene sia `and` sia `or`, Python non legge tutto "da sinistra a destra" in modo uniforme.

La precedenza e' questa:

1. `not`
2. `and`
3. `or`

Quindi:

```python
A or B and C
```

viene interpretato come:

```python
A or (B and C)
```

non come:

```python
(A or B) and C
```

Questo punto e' importante perche' due forme che sembrano simili possono avere significati diversi.

### Esempio

```python
x > 0 or y > 0 and z > 0
```

significa:

```python
x > 0 or (y > 0 and z > 0)
```

Se invece vuoi dire:

> almeno una tra `x` e `y` deve essere positiva, e inoltre `z` deve essere positivo

devi scrivere:

```python
(x > 0 or y > 0) and z > 0
```

Le parentesi non sono un abbellimento: fissano la struttura logica della condizione.

---

## Precedenza ed errori di valutazione

L'ordine di valutazione non cambia solo il significato logico. Puo' cambiare anche il fatto che il programma vada oppure no in errore.

Python usa una valutazione "corta":

- con `or`, se la parte sinistra e' gia' `True`, la parte destra non serve;
- con `and`, se la parte sinistra e' gia' `False`, la parte destra non serve.

Questo si chiama spesso **short-circuit**.

### Caso 1: l'errore viene evitato

```python
x = 0

if x != 0 and 10 / x > 2:
    print("ok")
```

Qui Python valuta prima:

```python
x != 0
```

che vale `False`.

Siccome c'e' un `and`, la seconda parte non viene valutata e quindi:

```python
10 / x
```

non viene eseguito.

Risultato: nessun `ZeroDivisionError`.

### Caso 2: l'errore compare

```python
x = 0

if 10 / x > 2 and x != 0:
    print("ok")
```

Qui la prima parte viene valutata subito:

```python
10 / x > 2
```

e il programma va in errore prima ancora di arrivare a `x != 0`.

La differenza non e' nel contenuto generale della condizione, ma nell'ordine in cui le parti vengono valutate.

---

## `or` e accessi pericolosi

Lo stesso vale quando una parte della condizione fa un accesso che potrebbe essere non valido.

Per esempio:

```python
indice = 5
lista = [10, 20, 30]

if indice < len(lista) and lista[indice] > 0:
    print("ok")
```

Questa forma e' sicura:

- prima controlla se l'indice esiste;
- solo dopo prova ad accedere a `lista[indice]`.

Se scrivi invece:

```python
if lista[indice] > 0 and indice < len(lista):
    print("ok")
```

puoi ottenere un `IndexError` immediatamente.

---

## Regola pratica

Quando una condizione contiene:

- controlli di validita';
- divisioni;
- accessi a posizioni;
- conversioni;

conviene mettere prima il controllo che rende sicura la parte successiva.

Per esempio:

- prima `x != 0`, poi la divisione;
- prima `indice < len(lista)`, poi l'accesso alla lista;
- prima `s != ""`, poi l'accesso a `s[0]`.

Questo vale sia per evitare errori sia per rendere la condizione piu' leggibile.

---

## Quando conviene usarle

Le leggi di De Morgan sono utili quando:

- una condizione con `not (...)` e' difficile da leggere;
- vuoi controllare meglio i casi limite;
- vuoi scrivere un `if` in forma piu' esplicita;
- stai facendo debugging di condizioni composte.

Per esempio, questa forma:

```python
if not (x > 0 and y > 0):
    ...
```

puo' essere piu' chiara cosi':

```python
if x <= 0 or y <= 0:
    ...
```

---

## Esercizi

1. Riscrivi usando De Morgan:

```python
not (a == 0 and b == 0)
```

2. Riscrivi usando De Morgan:

```python
not (nome == "" or cognome == "")
```

3. Verifica con una tabella di verita' che le due forme sono equivalenti:

```python
not (x < 10 or y < 10)
```

e

```python
x >= 10 and y >= 10
```

4. Riscrivi in forma piu' leggibile:

```python
if not (eta < 18 or senza_documento):
    print("ok")
```

5. Metti le parentesi in modo da rendere esplicita la precedenza:

```python
a or b and c
```

6. Spiega perche' questa forma evita un errore:

```python
x != 0 and 10 / x > 2
```

7. Correggi questa condizione in modo che non produca `IndexError`:

```python
lista[indice] > 0 and indice < len(lista)
```

---

## Riepilogo

Le leggi di De Morgan permettono di trasformare:

- `not (A and B)` in `not A or not B`
- `not (A or B)` in `not A and not B`

Inoltre:

- `not` ha precedenza su `and`;
- `and` ha precedenza su `or`;
- l'ordine delle sotto-condizioni puo' cambiare non solo il significato logico, ma anche la comparsa di errori a runtime.

Questi strumenti servono a leggere meglio condizioni composte, controllare casi concreti e ridurre errori logici nei test.
