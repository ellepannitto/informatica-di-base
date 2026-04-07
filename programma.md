---
title: Informatica di Base
subtitle: Università degli Studi di Salerno | 30% lezione / 70% esercitazione
---

## Prima di iniziare

Prima della prima lezione è consigliato preparare l'ambiente di lavoro. In particolare:

- installare **Python**
- installare **Visual Studio Code**
- installare **Git**
- prendere un primo contatto con il **terminale**
- se si usa **Windows**, installare anche **WSL** (Windows Subsystem for Linux)

Per una guida più dettagliata vedi [guida-lezioni/modulo-0.html](guida-lezioni/modulo-0.html).

Se qualcosa non funziona non è un problema: l'installazione dell'ambiente fa parte del corso e verrà ripresa anche a lezione.

## Libro consigliato

Il testo consigliato è **Introduzione a Python** di **Tony Gaddis**, in italiano oppure in inglese.

Non è obbligatorio: **seguire le lezioni è sufficiente** per affrontare il corso. Il libro è solo un supporto aggiuntivo per chi vuole ripassare o leggere altri esempi.

## Sistema di valutazione

- Tre prove intermedie facoltative, una per ciascun blocco/modulo del corso.
- Le prove intermedie si svolgono durante le ore del corso e sono gia comprese nel monte ore totale.
- La prova finale contiene delle domande aperte, un esercizio per ciascun modulo del corso, più un esercizio extra conclusivo.
- Se uno studente ha gia sostenuto una prova intermedia su un modulo, quel risultato resta disponibile anche se consegna la prova finale.
- In sede di verbalizzazione viene considerata, per ciascun modulo, la valutazione piu favorevole per lo studente tra prova intermedia e prova finale.
- Ogni prova intermedia superata puo quindi alleggerire la prova finale e migliorare il risultato complessivo.

## Moduli

### 01 | Introduzione alla programmazione e Python
- [exercise] [REPL, tipi e operazioni fondamentali: interi, float, stringhe, bool, input() e print()](guida-lezioni/modulo-1.html#mod1-repl) | ex 1h
- [theory] [Valori e tipi fondamentali: interi, float, stringhe e bool](guida-lezioni/modulo-1.html#mod1-repl) | lez 0.5h
- [theory] [Cos'è un programma: input/elaborazione/output, file system, sistema operativo e memoria](guida-lezioni/modulo-1.html#mod1-input-output) | lez 1h
- [theory] [Architettura di Von Neumann: CPU, memoria, input/output e programma come istruzioni + dati](guida-lezioni/modulo-1.html#mod1-von-neumann) | lez 0.5h
- [theory] [Ambiente di lavoro: Python, VS Code, terminale e differenza tra editor, shell e interprete](guida-lezioni/modulo-1.html#mod1-ambiente) | lez 0.5h
- [exercise] [Esercizi guidati: tracciare dati, memoria e output in piccoli esempi](guida-lezioni/modulo-1.html#mod1-tracciamento) | ex 0.5h
- [exercise] [Terminale: pwd, cd, ls, percorsi assoluti e relativi, apertura file da terminale](guida-lezioni/modulo-1.html#mod1-terminale) | ex 1h
- [exercise] [Introduzione al TDD: casi normali, casi limite, casi di errore](guida-lezioni/modulo-1.html#mod1-tdd) | ex 1h
- [theory] [Espressione vs istruzione; assegnazione di variabile e stato del programma in memoria](guida-lezioni/modulo-1.html#mod1-espressioni-istruzioni) | lez 0.5h
- [exercise] [Esercizi guidati: eseguire un primo script, stampa](guida-lezioni/modulo-1.html#mod1-primo-script) | ex 1.5h

### 02 | Variabili, tipi di dato e memoria
- [theory] Operazioni sui tipi fondamentali: calcoli, concatenazione, len() e accesso ai caratteri | lez 0.5h
- [exercise] type(), input(), print() e casting con int() e str() | 1h
- [exercise] Primi messaggi di errore: leggerli, localizzare la riga e capire il tipo di problema | 1.5h
- [exercise] Esercizi: calcoli, conversioni, stampa formattata e tracciamento dello stato | 2h

### 03 | Stato del programma e strutture decisionali
> [ai] Verifica del codice generato dall'IA: tracciare lo stato a mano per controllare i casi limite.
- [theory] Il tipo boolean, operatori di confronto e operatori logici | lez 0.5h
- [theory] Istruzioni if, if-else, elif e condizioni annidate | lez 0.5h
- [theory] Leggi di De Morgan e negazione di condizioni composte | lez 0.5h
- [theory] Automi a stati finiti: stati, transizioni e decisioni condizionali | lez 0.5h
- [exercise] Tracciamento di condizioni, rami eseguiti e casi limite | 1.5h
- [exercise] Esercizi: classificazioni, validazioni, riscrittura di condizioni complesse e semplici automi | 2.5h

### P1 | Prova intermedia 1 | prova=true
- Argomenti: moduli 1-3 (basi, tipi, memoria, stato, strutture decisionali) | 1h
- Correzione della prova | 1h

### 04 | Ciclo while, sentinelle e convalida
- [theory] Il ciclo while: condizione, stato e terminazione | lez 0.5h
- [theory] Sentinelle e convalida dell'input | lez 1.5h
- [theory] Errori tipici dei cicli: loop infinito, stato non aggiornato, condizione sbagliata | lez 0.5h
- [theory] Automi a stati finiti con while: aggiornare lo stato in risposta all'input | lez 0.5h
- [exercise] Esercizi: conteggi, somme, input ripetuto, sequenze terminate da sentinella e piccoli automi | 2.5h
- [exercise] Esercizi: validazione input, parità/disparità, condizioni di terminazione, tracciamento del ciclo e parser semplici | 2.5h

### 05 | Liste e lettura dei dati
- [theory] Liste: creare una lista, aggiungere elementi, leggere elementi e stampare una lista | lez 1h
- [theory] Leggere da standard input e accumulare dati in una lista | lez 0.5h
- [theory] Redirezione dell'input: usare un file come sorgente dello standard input | lez 0.5h
- [exercise] Esercizi: leggere sequenze di numeri o parole terminate da sentinella e salvarle in lista | 2h
- [exercise] Esercizi: elaborare liste lette da input, inversione, conteggi e prime trasformazioni | 2h

### 06 | Funzioni e procedure
- [theory] Definire funzioni: parametri, chiamata, valori di ritorno | lez 1h
- [exercise] Esercizi: scomporre un programma in funzioni piccole | 1h
- [theory] Firma di una funzione, black box e responsabilità singola | lez 1h
- [theory] Funzioni vs procedure: quando restituire un valore e quando produrre solo un effetto | lez 1h
- [exercise] Esercizi: my_strip, my_join, is_palindroma e semplici utility riusabili | 3h

### 07 | Memoria e passaggio degli argomenti
- [theory] Variabili come nomi associati a valori e oggetti; stato della memoria durante l'esecuzione | lez 1h
- [theory] Scope: variabili locali, parametri e visibilità dei nomi dentro e fuori una funzione | lez 1h
- [theory] Passaggio di argomenti: tipi immutabili e mutabili, effetti osservabili e casi tipici | lez 1h
- [theory] Passaggio per valore e per riferimento come modello intuitivo per leggere il comportamento dei programmi | lez 0.5h
- [exercise] Tracciamento della memoria: assegnazioni, chiamate di funzione, scope e aggiornamento dello stato | 1.5h
- [exercise] Esercizi: modifiche in-place, copie, effetti collaterali e debugging di funzioni | 1h

### P2 | Prova intermedia 2 | prova=true
- Argomenti: moduli 4-7 (while e convalida, liste e input, funzioni e procedure, memoria e scope) | 1h
- Correzione della prova | 1h

### 08 | Ciclo for, file e formati strutturati
- [theory] Il ciclo for su stringhe, liste e range() | lez 0.5h
- [theory] File di testo: aprire, leggere e scorrere un file riga per riga con for | lez 0.5h
- [theory] Differenza tra standard input e file aperto con open() | lez 0.5h
- [theory] Formati di input/output: testo semplice, CSV, JSON e HTML | lez 0.5h
- [theory] Esplorazione rapida da terminale: cat, head, tail, grep, cut, sort, wc, uniq e utility simili per leggere file e cartelle | lez 0.5h
- [exercise] Esercizi con for: conteggi, scansioni, accumuli e trasformazioni su sequenze | 1h
- [exercise] Esercizi da terminale: ispezionare file e filtrare contenuti con cat, head, tail, grep, cut, sort, wc e uniq | 0.5h
- [exercise] Esercizi su file di testo, CSV e JSON: lettura, scrittura e semplici trasformazioni | 1h
- [exercise] Esercizi su HTML: estrazione di informazioni e serializzazione dei risultati | 1h

### 09 | Dizionari, set e organizzazione dell'informazione
> [ai] L'IA tende a scegliere strutture dati "a intuito". Qui vogliamo invece ragionare su quale struttura usare per rappresentare e organizzare davvero l'informazione.
- [theory] Dizionari: chiavi, valori, accesso, aggiornamento e casi d'uso | lez 1h
- [theory] Set: appartenenza, eliminazione dei duplicati e operazioni di base | lez 0.5h
- [theory] Scegliere tra lista, dizionario e set per memorizzare e strutturare informazione | lez 0.5h
- [exercise] Esercizi: frequenze, raggruppamenti, conteggi e lookup con dizionari | 2h
- [exercise] Esercizi: uso dei set per unicità, confronti e filtraggio | 1.5h
- [exercise] Esercizi: modellare dati letti da JSON, CSV e HTML con liste, dizionari e set | 0.5h

### P3 | Prova intermedia 3 | prova=true
- Argomenti: moduli 6-9 (funzioni e procedure, memoria e scope, ciclo for e file, dizionari e set) | 1h

### -- | Consolidamento finale, testing e prova finale
> [ai] Riepilogo: pattern di errore ricorrenti dell'IA visti nel corso, esercizio di audit su funzioni generate dall'IA.
- Correzione della prova intermedia 3 | ex 1h
- Approfondimento TDD: test sistematici, assert avanzati, casi limite | lez 1h
- [theory] Virtual environment con venv: isolamento delle dipendenze, creazione, attivazione e ruolo di pip e requirements.txt | lez 0.5h
- Algoritmi fondamentali: ricerca lineare, ordinamento concettuale | lez 1h
- [duck] Sintesi duck typing: funzione che lavora su qualsiasi iterabile | lez 0.5h
- [ai] Uso critico dell'IA: riepilogo dei pattern di errore visti nel corso | ex 0.5h
- [exercise] Esercizi: creare un virtual environment con python -m venv, usare pip e salvare le dipendenze in requirements.txt | ex 0.5h
- Esercizi: impiccato, ricerca_lineare con assert, conta_pari generico, audit IA | ex 3h
- Sessioni di problem solving su casi completi | ex 4h
- Simulazione e prova finale | 4h
