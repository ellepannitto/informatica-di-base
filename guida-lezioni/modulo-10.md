# Modulo 10 · Dizionari, set e organizzazione dell'informazione

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- usare i `dict` per associare chiavi e valori;
- contare frequenze e raggruppare dati con i dizionari;
- iterare su chiavi, valori e coppie chiave-valore;
- usare i `set` come insiemi di elementi unici;
- distinguere bene lista, dizionario e set;
- applicare dizionari e set a problemi di lookup, frequenza, confronto e filtraggio.

---

<a id="mod10-dizionari"></a>
## Dizionari: associare chiavi e valori

Un dizionario permette di associare:

- una **chiave**;
- un **valore**.

Nel caso delle frequenze:

- chiave -> parola
- valore -> numero di occorrenze

Esempi:

```python
{}
{"the": 156, "cat": 20, "is": 80}
{"lazio": "roma", "campania": "napoli"}
{"molise": ["campobasso", "isernia"]}
```

Idea chiave:

- la chiave deve essere immutabile;
- il valore puo' essere di qualunque tipo;
- il dizionario e' utile quando vuoi recuperare rapidamente un'informazione associata a una chiave.

### Lista o dizionario?

Una lista puo' contenere le stesse informazioni di un dizionario, ma nella lista il significato dei campi resta implicito nelle posizioni.

Per esempio:

```python
persona_lista = ["Ludovica", "Pannitto", 30]
```

Con un dizionario:

```python
persona = {"nome": "Ludovica", "cognome": "Pannitto", "eta": 30}
```

la struttura diventa piu' leggibile e meno fragile.

### Operazioni fondamentali

| Operazione | Sintassi |
| --- | --- |
| chiavi | `D.keys()` |
| valori | `D.values()` |
| coppie | `D.items()` |
| appartenenza di una chiave | `k in D` |
| accesso | `D[k]` |
| aggiornamento | `D[k] = v` |
| cancellazione | `del D[k]` |
| numero di chiavi | `len(D)` |

---

## Iterazione sui dizionari

Iterare sulle chiavi:

```python
for chiave in dizionario:
    print(chiave, dizionario[chiave])
```

Iterare direttamente su coppie chiave-valore:

```python
for chiave, valore in dizionario.items():
    print(chiave, valore)
```

`items()` produce coppie del tipo `(chiave, valore)` che Python puo' spacchettare direttamente.

### Valori complessi

Il valore di un dizionario puo' essere anche una lista.

```python
persona = {
    "nome": "Ludovica",
    "cibi_preferiti": ["pane", "fiori di zucca"],
}
```

In quel caso:

- `persona["cibi_preferiti"]` restituisce una lista;
- quindi possiamo usare su quel valore i metodi delle liste, per esempio `append(...)`.

---

<a id="mod10-frequenze"></a>
## Frequenze e distribuzioni

Schema base:

```python
frequenze = {}

for parola in testo_tokenizzato:
    if parola in frequenze:
        frequenze[parola] = frequenze[parola] + 1
    else:
        frequenze[parola] = 1
```

Questo schema compare continuamente quando vogliamo:

- contare parole;
- contare caratteri;
- contare valori numerici;
- costruire raggruppamenti e statistiche discrete.

Versione che parte da un file:

```python
frequenze = {}

with open(nome_file, "r", encoding="utf-8") as file_input:
    for line in file_input:
        for parola in line.strip().split():
            if parola not in frequenze:
                frequenze[parola] = 0
            frequenze[parola] += 1
```

### Ordinare le frequenze

```python
dizionario = {"a": 5, "b": 1, "c": 3, "d": 7}

lista_ordinata = sorted(dizionario.items(), key=lambda x: x[1], reverse=True)
```

Varianti utili:

```python
sorted(dizionario.items(), key=lambda x: x[0])
sorted(dizionario.items(), key=lambda x: x[1], reverse=True)
```

---

<a id="mod10-set"></a>
## Set: insiemi non ordinati di elementi

I `set` sono insiemi non ordinati:

- non mantengono l'ordine;
- non ammettono duplicati;
- sono modificabili;
- gli elementi al loro interno devono essere immutabili.

Esempi:

```python
{3, 4, 5, 6}
{"elefante", "cammello", "pentola"}

set("linguistica")
set(["elefante", "cammello", "pentola", "elefante"])
```

### Operazioni fondamentali

| Operazione | Sintassi |
| --- | --- |
| Lunghezza | `len(S)` |
| Aggiunta | `S.add(x)` |
| Rimozione | `S.remove(x)` |
| Unione | `S1 | S2` |
| Intersezione | `S1 & S2` |
| Differenza | `S1 - S2` |

`set(lista_di_parole)` e' spesso il modo piu' rapido per passare da una sequenza di token al vocabolario.

---

## Appartenenza e operatore `in`

`in` e' l'operazione naturale quando la domanda e':

> questo elemento c'e' oppure no?

Esempio:

```python
lista = [4, 2, 0, 2, 3, 5]
insieme = {0, 2, 3, 4, 5}

print(0 in lista)
print(0 in insieme)
```

Il significato logico e' lo stesso, ma il costo operativo non e' identico.

---

<a id="mod10-uso-strutture"></a>
## Scegliere tra lista, dizionario e set

- la `lista` conserva ordine e ripetizioni;
- il `dict` associa chiavi e valori;
- il `set` e' molto efficiente nei controlli di appartenenza.

Per esempio:

- vocabolario senza ripetizioni -> `set`
- sequenza da mantenere in ordine -> `list`
- rubrica parola -> frequenza -> `dict`
- confronto tra parole presenti in due testi -> `set`

La scelta dipende dal problema, non dal gusto personale.

---

## Esercizi

### Dizionari: costruzione e accesso

1. costruisci un dizionario con la media dei voti per ogni studente;
2. conta le occorrenze dei numeri in una lista casuale;

3. Dato il seguente dizionario:
   ```python
   traduzione = {"gatto": "cat", "cane": "dog", "topo": "mouse", "uccello": "bird"}
   ```
   Scrivi un programma che chiede all'utente di inserire una parola italiana e stampa la traduzione in inglese. Se la parola non è nel dizionario, stampa `Parola non trovata`.

4. Scrivi un programma `conta_lettere.py` che prende come parametro una parola e conta quante volte compare ciascuna lettera usando un dizionario. Esempio:
   ```
   python3 conta_lettere.py banana
   {'b': 1, 'a': 3, 'n': 2}
   ```

### Frequenze e distribuzioni

5. costruisci la distribuzione di frequenza di un testo;
6. ordina le coppie parola-frequenza;
7. data una lista di parole, costruisci il vocabolario;

8. Scrivi un programma che legge un file di testo e conta la frequenza di ogni parola usando un dizionario. Stampa le parole e il loro conteggio, una per riga.

9. Scrivi un programma che legge un file di testo e stampa la parola che compare più volte. Se ci sono pareggi, basta stamparne una.

10. Scrivi un programma che legge una stringa letta dall'input (es. `adoro programmare in Python!`) e stampa la frequenza di ogni lettera.

### Dizionari e file

11. Scrivi un programma che legge un file di testo contenente una parola per riga e costruisce un dizionario dove la chiave è la parola e il valore è la sua lunghezza. Stampa il dizionario alla fine.

### Set e confronto tra collezioni

12. date due liste, restituisci unione e intersezione;

13. Scrivi un programma che legge due file di testo e confronta il loro vocabolario: stampa quante parole distinte compaiono in entrambi i file, quante solo nel primo e quante solo nel secondo.

---

## Riepilogo

Questo modulo organizza il materiale su:

- dizionari, chiavi, valori e iterazione;
- frequenze, conteggi e ordinamento di distribuzioni;
- set e loro proprieta';
- appartenenza con `in`;
- confronto tra lista, dizionario e set;
- uso su vocabolari, lookup e confronto tra collezioni.
