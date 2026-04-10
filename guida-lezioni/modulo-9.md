# Modulo 09 · Dizionari, set e organizzazione dell'informazione

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- usare i `dict` per associare chiavi e valori;
- contare frequenze e raggruppare dati con i dizionari;
- iterare su chiavi, valori e coppie chiave-valore;
- ordinare una distribuzione di frequenza;
- usare i `set` come insiemi di elementi unici;
- distinguere bene lista, dizionario e set;
- usare unione, intersezione e differenza;
- sfruttare `in` per controlli di appartenenza;
- applicare i set a problemi di vocabolario, confronto e filtraggio.

---

<a id="mod9-dizionari"></a>
## Dizionari: associare chiavi e valori

Il quarto notebook storico introduceva i `dict` partendo da un problema concreto:
contare quante volte compare ogni parola in un testo.

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

La lezione ci arrivava anche per contrasto con una soluzione scomoda: usare due liste parallele, una per gli studenti e una per le medie, oppure una per le parole e una per le frequenze.

Per esempio:

```python
studenti = ["anna", "luca", "marta"]
medie = [28, 24, 30]
```

Questa rappresentazione e' fragile perche' l'associazione dipende dal fatto che le posizioni restino perfettamente allineate.

Con un dizionario la struttura del problema diventa esplicita:

```python
medie = {"anna": 28, "luca": 24, "marta": 30}
```

Regola pratica:

- se vuoi collegare un'etichetta a un'informazione, il `dict` e' spesso la struttura giusta;
- se vuoi solo conservare una sequenza ordinata, una `list` resta piu' naturale.

La lezione del `18 marzo 2026` formulava questa differenza in modo molto netto:

- una lista puo' contenere le stesse informazioni di un dizionario;
- ma nella lista il significato dei campi resta implicito nelle posizioni;
- nel dizionario il significato e' scritto esplicitamente nelle chiavi.

Per esempio:

```python
persona_lista = ["Ludovica", "Pannitto", 30]
```

richiede di ricordare a memoria che:

- posizione `0` -> nome
- posizione `1` -> cognome
- posizione `2` -> eta'

Con un dizionario:

```python
persona = {"nome": "Ludovica", "cognome": "Pannitto", "eta": 30}
```

la struttura diventa piu' leggibile, piu' facile da mantenere e meno fragile quando il dato cresce.

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

Il notebook 4 mostrava due forme fondamentali.

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

La seconda forma e' spesso piu' leggibile quando hai bisogno di entrambe le informazioni.

Qui `items()` produce coppie del tipo `(chiave, valore)`, e Python puo' "spacchettarle" direttamente nelle due variabili del `for`.

### Esempio: media per studente

```python
voti = {
    "anna": [30, 28, 27],
    "luca": [24, 25, 23],
    "marta": [30, 30, 29],
}

medie = {}

for studente, lista_voti in voti.items():
    medie[studente] = sum(lista_voti) / len(lista_voti)
```

Questo esempio e' utile per vedere che:

- il valore associato a una chiave non deve essere per forza un numero semplice;
- un dizionario puo' servire anche come struttura intermedia per costruirne un altro.

Un altro punto pratico emerso a lezione e' che il valore di un dizionario puo' essere anche una lista.

Per esempio:

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

<a id="mod9-frequenze"></a>
## Frequenze e distribuzioni

Il problema centrale del notebook 4 era costruire una **distribuzione di frequenza**.

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

La lezione `08.srt` rimostrava lo stesso pattern partendo da un file testuale:

```python
frequenze = {}

with open(nome_file, "r", encoding="utf-8") as file_input:
    for line in file_input:
        for parola in line.strip().split():
            if parola not in frequenze:
                frequenze[parola] = 0
            frequenze[parola] += 1
```

Questo esempio e' didatticamente forte perche' tiene insieme:

- apertura del file;
- lettura riga per riga;
- tokenizzazione elementare con `split()`;
- aggiornamento del dizionario;
- separazione tra input, elaborazione e output.

### Ordinare le frequenze

Il notebook 4 introduceva anche `sorted()` applicato a `dizionario.items()`.

Esempio:

```python
dizionario = {"a": 5, "b": 1, "c": 3, "d": 7}

lista_ordinata = sorted(dizionario.items(), key=lambda x: x[1], reverse=True)
```

Qui stiamo ordinando le coppie:

```python
[("a", 5), ("b", 1), ("c", 3), ("d", 7)]
```

e non le chiavi da sole, per non perdere l'associazione tra parola e frequenza.

La funzione `lambda x: x[1]` dice a `sorted()` di guardare il secondo elemento della coppia, cioe' il valore.

Varianti utili:

```python
sorted(dizionario.items(), key=lambda x: x[0])
sorted(dizionario.items(), key=lambda x: x[1], reverse=True)
```

La prima ordina per chiave, la seconda per valore dal piu' grande al piu' piccolo.

<a id="mod9-set"></a>
## Set: insiemi non ordinati di elementi

Il terzo notebook storico introduceva i `set` come **insiemi non ordinati**.

Proprieta' chiave:

- non mantengono l'ordine;
- non ammettono duplicati;
- sono modificabili;
- gli elementi al loro interno devono essere immutabili.

La terza lezione riprendeva i set proprio a partire da un problema concreto:

- costruire il vocabolario di un testo;
- cioe' l'insieme delle parole distinte che compaiono nel corpus.

In questo caso il set e' naturale perche':

- non ci interessa tenere duplicati;
- ci interessa sapere se una parola compare oppure no;
- non ci serve l'ordine originario del testo.

Esempi:

```python
{3, 4, 5, 6}
{"elefante", "cammello", "pentola"}

set("linguistica")
set(["elefante", "cammello", "pentola", "elefante"])
set([True, True, True, False])
set([1, 2, 0, 3, 4, 0, 5, 6, 0])
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

La trascrizione aggiungeva un'osservazione utile:

- `set(lista_di_parole)` e' spesso il modo piu' rapido per passare da una sequenza di token al vocabolario;
- `len(set(lista_di_parole))` ci da subito la dimensione del vocabolario.

---

<a id="mod9-in"></a>
## Appartenenza e operatore `in`

Il notebook 3 insisteva molto su `in`, perche' e' l'operazione naturale quando la domanda e':

> questo elemento c'e' oppure no?

Esempio:

```python
lista = [4, 2, 0, 2, 3, 5]
insieme = {0, 2, 3, 4, 5}

print(0 in lista)
print(0 in insieme)
```

Il significato logico e' lo stesso, ma il costo operativo non e' identico.

### Intuizione pratica

- una lista e' adatta quando l'ordine conta o quando vuoi conservare ripetizioni;
- un set e' adatto quando conta soprattutto l'appartenenza o l'unicita'.

---

<a id="mod9-uso-strutture"></a>
## Scegliere tra lista, dizionario e set

Il notebook 3 mostrava anche un confronto intuitivo:

- la `lista` conserva ordine e ripetizioni;
- il `dict` associa chiavi e valori;
- il `set` e' molto efficiente nei controlli di appartenenza;
- la scelta dipende dal problema, non dal gusto personale.

Per esempio:

- vocabolario senza ripetizioni -> `set`
- sequenza da mantenere in ordine -> `list`
- rubrica parola -> frequenza -> `dict`
- confronto tra parole presenti in due testi -> `set`
- testo tokenizzato in ordine -> `list`

Questa e' esattamente la competenza che il modulo 9 vuole consolidare.

---

## Set e vocabolario di un testo

Uno degli usi piu' naturali del `set` e' costruire il vocabolario di un testo.

Se hai gia' una lista di parole:

```python
parole = ["era", "una", "notte", "era"]
vocabolario = set(parole)
print(vocabolario)
```

ottieni solo le parole distinte.

Questo e' il ponte naturale tra:

- lettura del testo;
- tokenizzazione;
- organizzazione dell'informazione.

### Perche' non sempre basta una lista

La terza lezione mostrava anche il confronto concettuale tra due strategie:

1. costruire il vocabolario a mano con una lista e controllare ogni volta se una parola c'e' gia';
2. usare direttamente un set.

La prima strategia ha valore didattico per capire la logica del problema.
La seconda e' spesso piu' adatta quando il nostro obiettivo e' proprio tenere solo elementi unici.

### Trade-off pratico: tempo vs spazio

La trascrizione insisteva anche su un punto piu' avanzato ma utile:

- i set sono molto comodi e molto rapidi per controllare appartenenza;
- pero' possono occupare piu' spazio in memoria di una lista;
- la scelta della struttura dipende da che operazioni dobbiamo fare dopo.

Regola pratica semplificata:

- se conta soprattutto sapere in fretta se un elemento c'e' -> `set`
- se conta l'ordine oppure vogliamo conservare tutte le occorrenze -> `list`

Questa non e' una legge assoluta, ma una buona euristica iniziale.

---

## Esercizi recuperati dai notebook 3 e 4

1. data una lista di parole, controlla se contiene `"linguistica"`;
2. restituisci la posizione di `"linguistica"` oppure `-1`;
3. inserisci `"linguistica"` in posizione `p`;
4. date due liste, restituisci l'unione senza ripetizioni;
5. date due liste, restituisci l'intersezione;
6. data una lista e una parola, stampa tutte le occorrenze con contesto vicino;
7. costruisci un dizionario con la media dei voti per ogni studente;
8. conta le occorrenze dei numeri in una lista casuale;
9. costruisci la distribuzione di frequenza di un testo;
10. ordina le coppie parola-frequenza;
11. estendi il conteggio ai bigrammi.

Le ultime due richieste sono il punto in cui lista e set collaborano bene:

- la lista conserva l'ordine;
- il set aiuta a eliminare duplicati e confrontare insiemi di elementi.

Con il notebook 4 si aggiunge un altro passaggio decisivo:

- il dizionario permette di rappresentare strutture del tipo chiave -> valore;
- quindi rende naturale modellare frequenze, lookup e raggruppamenti.

---

## Esercizi assegnati su dizionari e file

Tra gli esercizi gia' assegnati c'e' un gruppo molto ben allineato a questo modulo.

### Lookup e traduzione

Esempio:

- dato un dizionario `traduzione`, leggere una parola italiana e stampare la traduzione inglese;
- se la chiave non esiste, stampare `Parola non trovata`.

Questo esercizio e' il caso base per capire il dizionario come struttura di lookup.

### Dizionari costruiti da file

Altri esercizi chiedono di:

- leggere un file con una parola per riga e costruire un dizionario parola -> lunghezza;
- contare quante volte compare ciascuna lettera in una parola;
- leggere un file e trovare la parola piu' frequente;
- contare la frequenza di ogni parola in un testo.

Qui il punto didattico centrale e' sempre lo stesso:

- leggere un elemento;
- decidere qual e' la chiave;
- aggiornare il valore associato.

### Dizionari, set e confronto tra testi

Gli esercizi finali della raccolta portano naturalmente verso la combinazione di strutture:

- copiare solo le righe che contengono `"palla"` ignorando maiuscole/minuscole;
- confrontare il vocabolario di due file;
- contare quante parole distinte compaiono in entrambi i testi oppure solo in uno dei due.

Questo e' esattamente il punto in cui lista, dizionario e set smettono di essere capitoli separati e diventano strumenti da combinare.

---

## Soluzioni commentate emerse dagli esercizi

Le soluzioni svolte sui dizionari sono utili perche' fanno vedere alcune mosse standard che tornano spesso.

### Inizializzazione e aggiornamento

Nel conteggio delle lettere compare lo schema:

```python
if lettera not in dizionario:
    dizionario[lettera] = 0

dizionario[lettera] += 1
```

Questo e' uno dei pattern fondamentali del modulo.

### Dizionario inverso

In una soluzione sulla traduzione compare anche la costruzione di un dizionario inverso:

```python
traduzione_inversa[traduzione[key]] = key
```

Questo e' un ottimo esempio per mostrare che un dizionario non serve solo a consultare dati gia' pronti, ma anche a riorganizzarli.

### Massimo per valore

Nel file sulla parola piu' frequente compaiono due idee importanti:

- scorrere tutte le coppie `parola, frequenza`;
- usare `max(dizionario, key=dizionario.get)`.

La seconda e' piu' compatta, ma la prima resta essenziale sul piano didattico, perche' rende visibile il ragionamento.

### File, argomenti da riga di comando e dizionari

Alcune soluzioni leggono il nome del file da `sys.argv`.

Questo e' utile perche' collega il modulo 9 non solo a dizionari e file, ma anche all'idea che un programma possa ricevere parametri esterni e usarli per costruire strutture dati dinamiche.

---

## Riepilogo

Tra notebook 3 e 4 questo modulo recupera e organizza il materiale su:

- dizionari, chiavi, valori e iterazione;
- frequenze, conteggi e ordinamento di distribuzioni;
- set e loro proprieta';
- operazioni principali sui set;
- appartenenza con `in`;
- confronto tra lista, dizionario e set;
- uso su vocabolari, unicita', lookup e confronto tra collezioni.
