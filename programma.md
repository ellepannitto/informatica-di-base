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

Per una guida più dettagliata vedi [guida-lezioni/modulo-0.slides.html](guida-lezioni/modulo-0.slides.html).

Se qualcosa non funziona non è un problema: l'installazione dell'ambiente fa parte del corso e verrà ripresa anche a lezione.

## Libro consigliato

Il testo consigliato è **Introduzione a Python** di **Tony Gaddis**, in italiano oppure in inglese.

Non è obbligatorio: **seguire le lezioni è sufficiente** per affrontare il corso. Il libro è solo un supporto aggiuntivo per chi vuole ripassare o leggere altri esempi.

## Sistema di valutazione

- il corso è organizzato in 4 macroblocchi. Ai primi 3 blocchi corrisponde una prova intermedia
- tutte le prove intermedie sono facoltative, si svolgono durante le ore del corso e sono gia comprese nel monte ore totale.
- Le prove intermedie sono allineate ai blocchi `1-3`, `4-7` e `8-9`.
- La prova finale sarà strutturata seguendo la stessa logica: sarà presente almeno un esercizio per blocco e una sezione sui moduli `10` e `11`, non coperti dalle prove intermedie.
- Se uno studente ha gia sostenuto una prova intermedia su un blocco, quel risultato resta disponibile anche se consegna la prova finale.
- In sede di verbalizzazione viene considerata, per ciascun blocco, la valutazione piu favorevole per lo studente tra prova intermedia e prova finale.
- Ogni prova intermedia superata puo quindi alleggerire la prova finale e migliorare il risultato complessivo.

## Moduli

### 01 | Introduzione alla programmazione e Python
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1h     | [REPL, tipi e operazioni fondamentali: interi, float, stringhe](guida-lezioni/modulo-1.slides.html#mod1-repl) |
| theory    | 0.5h   | [Ambiente di lavoro: Python, VS Code, terminale e differenza tra editor, shell e interprete](guida-lezioni/modulo-1.slides.html#mod1-ambiente) |
| theory    | 0.5h   | [Tipi fondamentali e operazioni: interi, float, stringhe](guida-lezioni/modulo-1.slides.html#mod1-repl) |
| theory    | 0.5h   | [Architettura di Von Neumann: CPU, memoria, input/output e programma come istruzioni + dati](guida-lezioni/modulo-1.slides.html#mod1-von-neumann) |
| theory    | 1h     | [Cos'è un programma: input/elaborazione/output, file system, sistema operativo e memoria](guida-lezioni/modulo-1.slides.html#mod1-input-output) |
| exercise  | 0.5h   | [Esercizi guidati: tracciare dati, memoria e output in piccoli esempi](guida-lezioni/modulo-1.slides.html#mod1-tracciamento) |
| exercise  | 1h     | [Terminale: pwd, cd, ls, percorsi assoluti e relativi, apertura file da terminale](guida-lezioni/modulo-1.slides.html#mod1-terminale) |
| exercise  | 1h     | [Esercizi guidati: distinguere risultato calcolato, memoria e output](guida-lezioni/modulo-1.slides.html#mod1-tracciamento) |


### 02 | Variabili e strutture decisionali
| Tipologia | Durata | Argomento                                                                                                                                        |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| theory    | 0.5h   | [Espressione vs istruzione; assegnazione di variabile e stato del programma in memoria](guida-lezioni/modulo-2.slides.html#mod2-espressioni-istruzioni) |
| theory    | 0.5h   | [Il tipo boolean, istruzioni `if`, `if-else`, `elif` e condizioni annidate](guida-lezioni/modulo-2.slides.html#mod2-boolean-if) |
| exercise  | 1h     | [Primo script, `input()`, `print()` e casting con `int()` e `str()`](guida-lezioni/modulo-2.slides.html#mod2-primo-script) |
| exercise  | 1h     | [Variabili, stato del programma e primi esercizi con input/output](guida-lezioni/modulo-2.slides.html#mod2-input-output) |


### 03 | Stato del programma e strutture decisionali
| Tipologia | Durata | Argomento                                                                                     |
| --------- | ------ | --------------------------------------------------------------------------------------------- |
| exercise  | 1h     | [Lezione-laboratorio: testing, casi di test e casi limite](guida-lezioni/lezione-testing-casi-limite.slides.html) |
| theory    | 0.5h   | [Lezione: leggi di De Morgan, precedenza tra `and`/`or` e effetti sugli errori](guida-lezioni/lezione-leggi-de-morgan.slides.html) |
| exercise  | 1h     | [Primi messaggi di errore: leggerli, localizzare la riga e capire il tipo di problema](guida-lezioni/modulo-3.slides.html#mod3-errori) |
| theory    | 1h     | [Lezione: automi a stati finiti](guida-lezioni/lezione-automi.slides.html) |
| exercise  | 1h     | [Tracciamento di condizioni, rami eseguiti e casi limite](guida-lezioni/modulo-3.slides.html#mod3-tracciamento) |
| exercise  | 1.5h   | [Esercizi: classificazioni, validazioni, riscrittura di condizioni complesse e semplici automi](guida-lezioni/modulo-3.slides.html#mod3-casi-limite) |

### 04 | Ciclo while, sentinelle e convalida
| Tipologia | Durata | Argomento                                                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------- |
| theory    | 0.5h   | [Il ciclo `while`: condizione, stato e terminazione](guida-lezioni/modulo-4.slides.html#mod4-while) |
| theory    | 1h     | [Sentinelle e convalida dell'input](guida-lezioni/modulo-4.slides.html#mod4-sentinelle) |
| theory    | 0.5h   | [Errori tipici dei cicli: loop infinito, stato non aggiornato, condizione sbagliata](guida-lezioni/modulo-4.slides.html#mod4-errori) |
| theory    | 0.5h   | [Automi a stati finiti con `while`: aggiornare lo stato in risposta all'input](guida-lezioni/modulo-4.slides.html#mod4-automi) |
| exercise  | 1.5h   | [Esercizi: conteggi, somme, input ripetuto, sequenze terminate da sentinella](guida-lezioni/modulo-4.slides.html#mod4-sentinelle) |
| exercise  | 2h     | [Esercizi: validazione input, parità/disparità, condizioni di terminazione, tracciamento del ciclo e parser semplici](guida-lezioni/modulo-4.slides.html#mod4-errori) |

### P1 | Prova intermedia 1 | prova=true
| Tipologia | Durata | Argomento                                                                 |
| --------- | ------ | ------------------------------------------------------------------------- |
| exercise  | 1h     | Argomenti: moduli 1-3 (basi, tipi, memoria, stato, strutture decisionali) |
| exercise  | 1h     | Correzione della prova                                                    |

### 05 | Strutture dati: liste
| Tipologia | Durata | Argomento                                                                                                                     |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [Liste: creare una lista, aggiungere elementi, leggere elementi e stampare una lista](guida-lezioni/modulo-5.slides.html#mod5-liste) |
| exercise  | 0.5h   | [Leggere da standard input e accumulare dati in una lista](guida-lezioni/modulo-5.slides.html#mod5-input-lista)                      |
| theory    | 0.5h   | [Redirezione dell'input: usare un file come sorgente dello standard input](guida-lezioni/modulo-5.slides.html#mod5-redirezione)      |
| exercise  | 2h     | Esercizi: leggere sequenze di numeri o parole terminate da sentinella e salvarle in lista                                     |

### 06 | Funzioni e procedure
| Tipologia | Durata | Argomento                                                                                                                           |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [Definire funzioni: parametri, chiamata, valori di ritorno](guida-lezioni/modulo-6.slides.html#mod6-parametri)                             |
| exercise  | 1h     | Esercizi: scomporre un programma in funzioni piccole                                                                                |
| theory    | 0.5h   | [Firma di una funzione, black box e responsabilità singola](guida-lezioni/modulo-6.slides.html#mod6-black-box)                             |
| theory    | 0.5h   | Scope: variabili locali, parametri e visibilità dei nomi dentro e fuori una funzione                                                |
| exercise  | 3h     | [Esercizi: `my_strip`, `my_join`, `is_palindroma` e semplici utility riusabili](guida-lezioni/modulo-6.slides.html#mod6-esercizi-funzioni) |


### 07 | Memoria e passaggio degli argomenti
| Tipologia | Durata | Argomento                                                                                                                                    |
| --------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [Funzioni vs procedure: quando restituire un valore e quando produrre solo un effetto](guida-lezioni/modulo-6.slides.html#mod6-procedure)           |
| theory    | 1h     | [Variabili come nomi associati a valori e oggetti; stato della memoria durante l'esecuzione](guida-lezioni/modulo-7.slides.html#mod7-memoria-liste) |
| exercise  | 2h     | Esercizi: elaborare liste lette da input, inversione, conteggi e prime trasformazioni                                                        |
| theory    | 1h     | Passaggio per valore e per riferimento e side effects                                                                                        |
| exercise  | 1h     | [Esercizi: modifiche in-place, copie, effetti collaterali e debugging di funzioni](guida-lezioni/modulo-7.slides.html#mod7-copie)                   |

### P2 | Prova intermedia 2 | prova=true
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1.5h     | Argomenti: moduli 4-7 (while e convalida, liste e input, funzioni e procedure)|
| exercise  | 1.5h     | Correzione della prova |

### 08 | Ciclo for e iterazione
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 0.5h   | [Il ciclo `for` su stringhe, liste e `range()`](guida-lezioni/modulo-8.slides.html#mod8-for) |
| theory    | 0.5h   | [Cicli annidati con `for`: righe, colonne, pattern e costruzione di stringhe](guida-lezioni/modulo-8.slides.html#mod8-for) |
| exercise  | 1h   | Esercizi con `for`: conteggi, scansioni, accumuli e trasformazioni su sequenze |
| exercise  | 1h     | Esercizi: pattern di stampa, triangoli, rettangoli e uso degli indici nei cicli annidati |

### 09 | File e formati strutturati
| Tipologia | Durata | Argomento                                                                                                                                                                               |
| --------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [File di testo: aprire, leggere e scorrere un file riga per riga con `for`](guida-lezioni/modulo-9.slides.html#mod9-file)                                                                      |
| theory    | 0.5h   | [Formati di input/output: testo semplice, CSV, JSON e HTML](guida-lezioni/modulo-9.slides.html#mod9-formati)                                                                                   |
| theory    | 0.5h   | [Differenza tra standard input, file aperto con `open()` e parametri da riga di comando](guida-lezioni/modulo-9.slides.html#mod9-file) |
| exercise  | 0.5h   | [Esplorazione rapida da terminale: `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc`, `uniq` e utility simili per leggere file e cartelle](guida-lezioni/modulo-9.slides.html#mod9-terminale) |
| exercise  | 0.5h   | [Esercizi da terminale: ispezionare file e filtrare contenuti con `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc` e `uniq`](guida-lezioni/modulo-9.slides.html#mod9-terminale)              |
| exercise  | 2h     | Esercizi su file di testo, CSV e JSON: lettura, scrittura e semplici trasformazioni |
| exercise  | 1h     | Esercizi: parametri da riga di comando, output su file e piccole pipeline di elaborazione |


### P3 | Prova intermedia 3 | prova=true
| Tipologia | Durata | Argomento                                                                  |
| --------- | ------ | -------------------------------------------------------------------------- |
| exercise  | 1h     | Argomenti: moduli 8-10 (`for`, file, input/output, terminale, formati) |
| exercise  | 1h     | Correzione della prova                                                     |

### 10 | Dizionari, set e organizzazione dell'informazione
| Tipologia | Durata | Argomento                                                                                                                          |
| --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [Dizionari: chiavi, valori, accesso, aggiornamento e casi d'uso](guida-lezioni/modulo-10.slides.html#mod10-dizionari)                       |
| theory    | 1h     | [Set: appartenenza, eliminazione dei duplicati e operazioni di base](guida-lezioni/modulo-10.slides.html#mod10-set)                 |
| exercise  | 2h     | [Esercizi: frequenze, raggruppamenti, conteggi e lookup con dizionari](guida-lezioni/modulo-10.slides.html#mod10-frequenze)                 |


### 11 | Git e controllo di versione
| Tipologia | Durata | Argomento                                                                                             |
| --------- | ------ | ----------------------------------------------------------------------------------------------------- |
| theory    | 1h     | [Git: repository, working tree, staging area, commit e storia del progetto](guida-lezioni/modulo-11.slides.html#mod11-git)                             |
| theory    | 1h     | [Git da terminale: `git init`, `git status`, `git add`, `git commit`, `git log`](guida-lezioni/modulo-11.slides.html#mod11-git)                        |
| exercise  | 1.5h   | Esercizi: creare un repository locale, tracciare file, salvare versioni e leggere `git status`        |
| theory    | 0.5h   | [GitHub: repository remoto, `clone`, `push`, `pull` e collaborazione di base](guida-lezioni/modulo-11.slides.html#mod11-github)                           |
| exercise  | 0.5h   | Esercizi: clonare un repository, aggiungere modifiche e pubblicarle sul remoto                        |
| exercise  | 1h     | Esercizi: leggere differenze tra file non tracciati, modificati e già staged                          |
| exercise  | 1h     | Mini-laboratorio finale: usare Git per tenere traccia di uno script Python e dei file di input/output |
