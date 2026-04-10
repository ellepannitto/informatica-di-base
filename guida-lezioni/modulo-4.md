# Modulo 04 · Ciclo while, sentinelle e convalida

---

## Obiettivi del modulo

Al termine di questo modulo saprai:

- usare `while` quando non conosci in anticipo il numero di iterazioni;
- distinguere bene guardia del ciclo, stato e condizione di terminazione;
- progettare cicli con sentinelle e input ripetuto;
- riconoscere errori tipici come loop infinito e stato non aggiornato;
- leggere un `while` come evoluzione dello stato del programma;
- applicare `while` a conteggi, validazione e piccoli automi.

---

<a id="mod4-while"></a>
## Il problema che porta al `while`

Il quarto notebook storico partiva da una domanda semplice:

> come si itera quando non sappiamo prima quante volte dovremo ripetere il blocco?

Con `for` sappiamo gia' quante iterazioni vogliamo o quale sequenza stiamo scorrendo.

Con `while`, invece, la ripetizione continua finche' una condizione resta vera.

Esempio del notebook:

```python
lista_nomi = []
i = 0

while len(lista_nomi) < 10:
    if nome(testo[i]):
        lista_nomi.append(testo[i])
    i = i + 1
```

Qui non sappiamo in anticipo dove comparira' il decimo nome nel testo, quindi non possiamo fissare subito il numero corretto di passi.

---

## Sintassi e semantica del `while`

Forma generale:

```python
while espressione_booleana:
    # istruzioni
```

Semantica:

1. Python valuta la guardia;
2. se vale `True`, esegue il blocco;
3. poi torna a valutare la guardia;
4. se vale `False`, esce dal ciclo.

Idea chiave:

- il `while` non ripete "per sempre";
- ripete finche' lo stato del programma continua a soddisfare la guardia.

Per questo ogni `while` va letto sempre in termini di:

- stato iniziale;
- guardia;
- aggiornamento dello stato;
- condizione di uscita.

La quarta lezione insisteva su un punto pratico:

- con `for` di solito sappiamo gia' quante volte iterare oppure quale sequenza stiamo scorrendo;
- con `while` la domanda tipica e' invece: "continuo finche' non succede qualcosa che mi fa fermare".

Per questo il `while` compare spesso in problemi del tipo:

- continua a leggere input finche' non arriva una sentinella;
- continua a scorrere dati finche' non trovi il primo caso interessante;
- continua a chiedere un valore finche' non rispetta il vincolo richiesto.

Python non ha una forma `do ... while`: se il corpo del ciclo deve essere eseguito almeno una volta, bisogna progettare con attenzione stato iniziale e prima lettura dei dati.

### Esempio: fermarsi alla prima parola lunga

Una situazione discussa a lezione e' questa:

> leggere parole da un file e fermarsi alla prima parola con piu' di 6 caratteri.

Schema possibile:

```python
file_in = open("parole.txt", "r", encoding="utf-8")
parola = file_in.readline().strip()

while parola != "" and len(parola) <= 6:
    parola = file_in.readline().strip()

file_in.close()
```

Qui:

- `parola` e' lo stato che guida il ciclo;
- la guardia dice di continuare solo se non siamo a fine file e la parola letta e' ancora "corta";
- l'aggiornamento consiste nel leggere la parola successiva.

Questo esempio fa emergere due dettagli facili da sbagliare:

- senza `strip()` la riga letta contiene spesso anche `\n`, quindi la lunghezza risulta falsata;
- se non controlli anche `parola != ""`, a fine file rischi di continuare a ragionare su una pseudo-parola vuota.

### Contare mentre si cerca

Se oltre a fermarti vuoi sapere quante parole hai letto prima di trovare quella giusta, devi mantenere anche un contatore:

```python
file_in = open("parole.txt", "r", encoding="utf-8")
parola = file_in.readline().strip()
conteggio = 0

while parola != "" and len(parola) <= 6:
    conteggio += 1
    parola = file_in.readline().strip()

file_in.close()
```

Qui l'ordine delle istruzioni conta: cambiare il punto in cui incrementi `conteggio` produce facilmente errori di una unita'.

---

<a id="mod4-sentinelle"></a>
## Sentinelle e input ripetuto

Una **sentinella** e' un valore speciale che segnala al programma quando fermarsi.

Esempio classico:

```python
numero = int(input("Numero (-1 per terminare): "))
somma = 0

while numero != -1:
    somma = somma + numero
    numero = int(input("Numero (-1 per terminare): "))
```

In questo schema:

- `-1` non e' un dato da elaborare;
- serve solo a interrompere il ciclo;
- il programma continua a leggere input finche' non incontra la sentinella.

Questo modello e' utile per:

- leggere una sequenza di numeri;
- leggere parole fino a una parola speciale;
- validare un dato finche' non diventa accettabile.

### Convalida dell'input

Il modulo 4 del programma insiste anche sulla convalida:

```python
eta = int(input("Eta': "))

while eta < 0:
    eta = int(input("Inserisci un'eta' valida: "))
```

Qui il ciclo non accumula dati: controlla che lo stato rientri nei vincoli del problema.

---

<a id="mod4-errori"></a>
## Errori tipici dei cicli `while`

Il notebook 4 rendeva molto chiaro che i problemi tipici sono quasi sempre tre.

| Errore | Che cosa succede |
| --- | --- |
| guardia sbagliata | il ciclo termina troppo presto o non termina |
| stato non aggiornato | la guardia non cambia mai |
| aggiornamento nel punto sbagliato | salti casi, duplichi passi o perdi il controllo del flusso |

Esempio di loop infinito:

```python
x = 0

while x < 5:
    print(x)
```

Qui `x` non cambia mai, quindi la guardia resta sempre vera.

Versione corretta:

```python
x = 0

while x < 5:
    print(x)
    x = x + 1
```

Domanda da farsi sempre:

> quale variabile sta portando il ciclo verso la terminazione?

La trascrizione dell'`11 marzo 2026` mostrava bene due errori tipici nei `while` di stampa:

- dimenticare l'aggiornamento della variabile interna, per esempio `j += 1`;
- scrivere una guardia troppo debole, come `while 1 < n`, che non dipende davvero dallo stato del ciclo.

In entrambi i casi il sintomo e' lo stesso:

- il programma non si ferma;
- oppure continua a stampare righe sbagliate;
- oppure produce un pattern quasi giusto ma con uno shift di una unita'.

Regola pratica:

- la guardia deve dipendere da una variabile che cambia davvero;
- e quella variabile deve essere aggiornata nel punto giusto del ciclo.

---

<a id="mod4-automi"></a>
## `while` e automi a stati finiti

Il `while` e' una forma naturale per rappresentare un programma che:

- resta in attesa di input;
- aggiorna il proprio stato;
- decide se continuare o fermarsi.

Esempio intuitivo:

```python
stato = "attesa"

while stato == "attesa":
    risposta = input("Confermi? [s/n] ")
    if risposta == "s":
        stato = "confermato"
    elif risposta == "n":
        stato = "annullato"
```

Questa lettura collega bene:

- condizioni;
- memoria;
- aggiornamento dello stato;
- terminazione del ciclo.

---

## Esercizi recuperati dal notebook 4

Dal notebook 4 conviene recuperare soprattutto questi esercizi:

1. leggere parole da un file e fermarsi alla prima parola piu' lunga di 6 caratteri;
2. leggere frasi e fermarsi dopo 100 parole;
3. leggere 10 numeri e decidere se sono di piu' i pari o i dispari;
4. leggere numeri finche' non compare una sentinella;
5. dire se un numero positivo e' primo;
6. contare quante cifre ha un numero;
7. fermarsi quando la media di un gruppo di numeri diventa zero.

Sono esercizi utili perche' costringono a progettare con attenzione:

- la guardia;
- le variabili di stato;
- l'aggiornamento a ogni iterazione;
- la condizione di uscita.

---

## Esercizi assegnati su `while`

Nei testi degli esercizi assegnati ricorrono alcuni pattern molto coerenti con questo modulo.

### Sequenze terminate da sentinella

Esempi assegnati:

- leggere parole finche' non compare `fine` e controllare se compare `"lingua"`;
- leggere numeri finche' non compare `0` e stampare il massimo;
- leggere parole finche' non compare `fine` e classificare ogni parola come lunga o breve;
- leggere numeri finche' non compare `0` e dire per ciascuno se e' pari o dispari.

Questi esercizi servono a consolidare tre idee:

- la sentinella non va trattata come dato normale;
- il controllo di terminazione va ripetuto a ogni passo;
- bisogna mantenere uno stato cumulativo corretto.

### Stato del ciclo e proprieta' della sequenza

Un secondo gruppo di esercizi chiede di riconoscere proprieta' piu' strutturate:

- verificare che ogni `1` sia seguito da `2`;
- contare quante parole finiscono per vocale;
- accumulare il numero totale di vocali lette;
- leggere un intero e stampare le sue potenze finche' non si supera `1000`.

Qui il punto non e' solo iterare, ma scegliere con precisione:

- quali variabili aggiornare;
- quando aggiornare;
- quale informazione deve sopravvivere da un'iterazione alla successiva.

### Convalida e vincoli

Tra gli esercizi assegnati compare anche la validazione esplicita:

```python
# leggere un numero tra 1 e 10, altrimenti segnalare errore
```

Questo e' un caso tipico di `while` usato non per accumulare una sequenza, ma per imporre un vincolo sull'input.

### Mini-progetto: impiccato

L'esercizio sull'impiccato e' particolarmente adatto a questo modulo perche' combina:

- stato corrente del gioco;
- ripetizione finche' la parola non e' completata;
- aggiornamento dopo ogni lettera proposta;
- possibilita' di introdurre tentativi massimi.

E' un buon ponte tra:

- `while`;
- stringhe;
- funzioni di aggiornamento dello stato;
- debugging di programmi un po' piu' lunghi.

---

## Soluzioni commentate emerse in lezione

Le soluzioni svolte mostrano bene che spesso conviene arrivare al programma finale per raffinamenti successivi.

### Verificare la regola "ogni 1 e' seguito da 2"

Nei file svolti compaiono piu' versioni della stessa idea:

1. una soluzione che salva tutta la sequenza in lista;
2. una soluzione che controlla posizioni adiacenti;
3. una soluzione piu' pulita che tiene memoria del numero precedente.

Questa progressione e' didatticamente molto utile perche' mostra che:

- una prima soluzione puo' funzionare ma essere fragile;
- rileggere il problema puo' suggerire uno stato piu' semplice;
- spesso basta una variabile `numero_pred` per evitare strutture superflue.

### Trovare il massimo con sentinella

Una delle soluzioni svolte usa lo schema:

```python
numero = int(input("Inserisci un numero: "))
massimo = -1

while numero != 0:
    if numero > massimo:
        massimo = numero
    numero = int(input("Inserisci un numero: "))

print(massimo)
```

Questo e' un ottimo esempio di `while` con:

- sentinella;
- variabile accumulatrice;
- aggiornamento dello stato a ogni iterazione.

### Impiccato come automa

La soluzione svolta dell'impiccato introduce una funzione:

```python
def update(guess, parola_segreta, lettera):
    ...
```

e poi usa un ciclo:

```python
while GUESS != PAROLA_SEGRETA:
    ...
```

Questo rende esplicita una struttura molto importante:

- stato corrente del gioco -> `GUESS`
- input del giocatore -> nuova lettera
- funzione di transizione -> `update`
- condizione di arresto -> parola completata

In pratica, e' un automa a stati finiti travestito da gioco.

---

## Esercizi di stampa con `while`

Nella lezione dell'`11 marzo 2026` sono comparsi anche esercizi molto utili per capire davvero come evolve lo stato in un ciclo:

- stampare `1`, poi `22`, poi `333`, fino a `n`;
- stampare triangoli o pattern numerici usando due cicli annidati;
- riscrivere la stessa soluzione passando da `while` a `for`.

Il valore di questi esercizi non e' estetico, ma strutturale:

- costringono a distinguere il ciclo che controlla le righe dal ciclo che controlla i simboli dentro ogni riga;
- fanno vedere subito gli errori di guardia, di inizializzazione e di incremento;
- mostrano che un piccolo cambio di indice puo' produrre un pattern diverso.

Per esempio, in una soluzione con due cicli:

- l'indice esterno `i` puo' dire quale riga stiamo costruendo;
- l'indice interno `j` puo' dire quante volte ripetere un simbolo o quale simbolo mettere.

Se usi `i` per costruire la stringa ottieni un risultato; se usi `j`, ne ottieni un altro. Questo e' uno dei modi piu' chiari per vedere che gli indici non sono "nomi intercambiabili", ma rappresentano ruoli diversi nello stato del programma.

---

## Riepilogo

Dal notebook 4 questo modulo recupera e organizza il materiale su:

- significato del ciclo `while`;
- iterazione a terminazione non nota in anticipo;
- sentinelle e input ripetuto;
- convalida dell'input;
- errori tipici dei cicli;
- uso del `while` per piccoli automi e problemi di scansione.
