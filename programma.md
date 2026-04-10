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
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1h     | [REPL, tipi e operazioni fondamentali: interi, float, stringhe](guida-lezioni/modulo-1.html#mod1-repl) |
| theory    | 0.5h   | [Ambiente di lavoro: Python, VS Code, terminale e differenza tra editor, shell e interprete](guida-lezioni/modulo-1.html#mod1-ambiente) |
| theory    | 0.5h   | [Tipi fondamentali e operazioni: interi, float, stringhe](guida-lezioni/modulo-1.html#mod1-repl) |
| theory    | 0.5h   | [Architettura di Von Neumann: CPU, memoria, input/output e programma come istruzioni + dati](guida-lezioni/modulo-1.html#mod1-von-neumann) |
| theory    | 1h     | [Cos'è un programma: input/elaborazione/output, file system, sistema operativo e memoria](guida-lezioni/modulo-1.html#mod1-input-output) |
| exercise  | 0.5h   | [Esercizi guidati: tracciare dati, memoria e output in piccoli esempi](guida-lezioni/modulo-1.html#mod1-tracciamento) |
| exercise  | 1h     | [Terminale: pwd, cd, ls, percorsi assoluti e relativi, apertura file da terminale](guida-lezioni/modulo-1.html#mod1-terminale) |
| exercise  | 1h     | [Progettare un programma: casi normali, casi limite, casi di errore](guida-lezioni/modulo-1.html#mod1-tdd) |


### 02 | Variabili e strutture decisionali
| Tipologia | Durata | Argomento                                                                                                                                        |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| exercise  | 1h     | [Esercizi guidati: eseguire un primo script, stampa](guida-lezioni/modulo-2.html#mod2-primo-script) |
| theory    | 0.5h   | [Espressione vs istruzione; assegnazione di variabile e stato del programma in memoria](guida-lezioni/modulo-2.html#mod2-espressioni-istruzioni) |
| theory    | 0.5h   | [Il tipo boolean, istruzioni `if`, `if-else`, `elif` e condizioni annidate](guida-lezioni/modulo-2.html#mod2-boolean-if) |
| exercise  | 1h     | [`type()`, `input()`, `print()` e casting con `int()` e `str()`](guida-lezioni/modulo-2.html#mod2-input-output) |

### 03 | Stato del programma e strutture decisionali
| Tipologia | Durata | Argomento                                                                                     |
| --------- | ------ | --------------------------------------------------------------------------------------------- |
| exercise  | 1h     | [Esercizi: calcoli, conversioni, stampa formattata e tracciamento dello stato](guida-lezioni/modulo-3.html#mod3-calcoli-conversioni) |
| theory    | 0.5h   | [Leggi di De Morgan e negazione di condizioni composte](guida-lezioni/modulo-3.html#mod3-boolean-logica) |
| exercise  | 1h     | [Primi messaggi di errore: leggerli, localizzare la riga e capire il tipo di problema](guida-lezioni/modulo-3.html#mod3-errori) |
| theory    | 1h     | [Automi a stati finiti: stati, transizioni e decisioni condizionali](guida-lezioni/modulo-3.html#mod3-automi) |
| exercise  | 1h     | [Tracciamento di condizioni, rami eseguiti e casi limite](guida-lezioni/modulo-3.html#mod3-tracciamento) |
| exercise  | 1.5h   | [Esercizi: classificazioni, validazioni, riscrittura di condizioni complesse e semplici automi](guida-lezioni/modulo-3.html#mod3-casi-limite-ai) |

### 04 | Ciclo while, sentinelle e convalida
| Tipologia | Durata | Argomento                                                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------- |
| theory    | 0.5h   | [Il ciclo `while`: condizione, stato e terminazione](guida-lezioni/modulo-4.html#mod4-while) |
| theory    | 1h     | [Sentinelle e convalida dell'input](guida-lezioni/modulo-4.html#mod4-sentinelle) |
| theory    | 0.5h   | [Errori tipici dei cicli: loop infinito, stato non aggiornato, condizione sbagliata](guida-lezioni/modulo-4.html#mod4-errori) |
| theory    | 0.5h   | [Automi a stati finiti con `while`: aggiornare lo stato in risposta all'input](guida-lezioni/modulo-4.html#mod4-automi) |
| exercise  | 1.5h   | [Esercizi: conteggi, somme, input ripetuto, sequenze terminate da sentinella e piccoli automi](guida-lezioni/modulo-4.html#mod4-sentinelle) |
| exercise  | 2h     | [Esercizi: validazione input, parità/disparità, condizioni di terminazione, tracciamento del ciclo e parser semplici](guida-lezioni/modulo-4.html#mod4-errori) |

### P1 | Prova intermedia 1 | prova=true
| Tipologia | Durata | Argomento                                                                 |
| --------- | ------ | ------------------------------------------------------------------------- |
| exercise  | 1h     | Argomenti: moduli 1-3 (basi, tipi, memoria, stato, strutture decisionali) |
| exercise  | 1h     | Correzione della prova                                                    |


### 05 | Liste e lettura dei dati
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 1h     | [Liste: creare una lista, aggiungere elementi, leggere elementi e stampare una lista](guida-lezioni/modulo-5.html#mod5-liste) |
| theory    | 0.5h   | [Leggere da standard input e accumulare dati in una lista](guida-lezioni/modulo-5.html#mod5-input-lista) |
| theory    | 0.5h   | [Redirezione dell'input: usare un file come sorgente dello standard input](guida-lezioni/modulo-5.html#mod5-redirezione) |
| exercise  | 2h     | Esercizi: leggere sequenze di numeri o parole terminate da sentinella e salvarle in lista |
| exercise  | 2h     | Esercizi: elaborare liste lette da input, inversione, conteggi e prime trasformazioni |

### 06 | Funzioni e procedure
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 1h     | [Definire funzioni: parametri, chiamata, valori di ritorno](guida-lezioni/modulo-6.html#mod6-parametri) |
| exercise  | 1h     | Esercizi: scomporre un programma in funzioni piccole |
| theory    | 1h     | [Firma di una funzione, black box e responsabilità singola](guida-lezioni/modulo-6.html#mod6-black-box) |
| theory    | 1h     | [Funzioni vs procedure: quando restituire un valore e quando produrre solo un effetto](guida-lezioni/modulo-6.html#mod6-procedure) |
| exercise  | 3h     | [Esercizi: `my_strip`, `my_join`, `is_palindroma` e semplici utility riusabili](guida-lezioni/modulo-6.html#mod6-esercizi-funzioni) |

### 07 | Memoria e passaggio degli argomenti
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 1h     | [Variabili come nomi associati a valori e oggetti; stato della memoria durante l'esecuzione](guida-lezioni/modulo-7.html#mod7-memoria-liste) |
| theory    | 1h     | Scope: variabili locali, parametri e visibilità dei nomi dentro e fuori una funzione |
| theory    | 1h     | Passaggio di argomenti: tipi immutabili e mutabili, effetti osservabili e casi tipici |
| theory    | 0.5h   | Passaggio per valore e per riferimento come modello intuitivo per leggere il comportamento dei programmi |
| exercise  | 1.5h   | Tracciamento della memoria: assegnazioni, chiamate di funzione, scope e aggiornamento dello stato |
| exercise  | 1h     | [Esercizi: modifiche in-place, copie, effetti collaterali e debugging di funzioni](guida-lezioni/modulo-7.html#mod7-copie) |

### P2 | Prova intermedia 2 | prova=true
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1h     | Argomenti: moduli 4-7 (while e convalida, liste e input, funzioni e procedure, memoria e scope) |
| exercise  | 1h     | Correzione della prova |

### 08 | Ciclo for, file e formati strutturati
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 0.5h   | [Il ciclo `for` su stringhe, liste e `range()`](guida-lezioni/modulo-8.html#mod8-for) |
| theory    | 0.5h   | [File di testo: aprire, leggere e scorrere un file riga per riga con `for`](guida-lezioni/modulo-8.html#mod8-file) |
| theory    | 0.5h   | [Differenza tra standard input e file aperto con `open()`](guida-lezioni/modulo-8.html#mod8-file) |
| theory    | 0.5h   | [Formati di input/output: testo semplice, CSV, JSON e HTML](guida-lezioni/modulo-8.html#mod8-formati) |
| theory    | 0.5h   | [Esplorazione rapida da terminale: `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc`, `uniq` e utility simili per leggere file e cartelle](guida-lezioni/modulo-8.html#mod8-terminale) |
| exercise  | 1h     | Esercizi con `for`: conteggi, scansioni, accumuli e trasformazioni su sequenze |
| exercise  | 0.5h   | [Esercizi da terminale: ispezionare file e filtrare contenuti con `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc` e `uniq`](guida-lezioni/modulo-8.html#mod8-terminale) |
| exercise  | 1h     | Esercizi su file di testo, CSV e JSON: lettura, scrittura e semplici trasformazioni |
| exercise  | 1h     | Esercizi su HTML: estrazione di informazioni e serializzazione dei risultati |

### 09 | Dizionari, set e organizzazione dell'informazione
> [ai] L'IA tende a scegliere strutture dati "a intuito". Qui vogliamo invece ragionare su quale struttura usare per rappresentare e organizzare davvero l'informazione.
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| theory    | 1h     | [Dizionari: chiavi, valori, accesso, aggiornamento e casi d'uso](guida-lezioni/modulo-9.html#mod9-dizionari) |
| theory    | 0.5h   | [Set: appartenenza, eliminazione dei duplicati e operazioni di base](guida-lezioni/modulo-9.html#mod9-set) |
| theory    | 0.5h   | [Scegliere tra lista, dizionario e set per memorizzare e strutturare informazione](guida-lezioni/modulo-9.html#mod9-uso-strutture) |
| exercise  | 2h     | [Esercizi: frequenze, raggruppamenti, conteggi e lookup con dizionari](guida-lezioni/modulo-9.html#mod9-frequenze) |
| exercise  | 1.5h   | Esercizi: uso dei set per unicità, confronti e filtraggio |
| exercise  | 0.5h   | Esercizi: modellare dati letti da JSON, CSV e HTML con liste, dizionari e set |

### P3 | Prova intermedia 3 | prova=true
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1h     | Argomenti: moduli 6-9 (funzioni e procedure, memoria e scope, ciclo for e file, dizionari e set) |

### -- | Consolidamento finale, testing e prova finale
> [ai] Riepilogo: pattern di errore ricorrenti dell'IA visti nel corso, esercizio di audit su funzioni generate dall'IA.
> [duck] Sintesi duck typing: funzione che lavora su qualsiasi iterabile.
| Tipologia | Durata | Argomento |
| --------- | ------ | --------- |
| exercise  | 1h     | Correzione della prova intermedia 3 |
| theory    | 1h     | Approfondimento TDD: test sistematici, assert avanzati, casi limite |
| theory    | 0.5h   | Virtual environment con `venv`: isolamento delle dipendenze, creazione, attivazione e ruolo di `pip` e `requirements.txt` |
| theory    | 1h     | Algoritmi fondamentali: ricerca lineare, ordinamento concettuale |
| exercise  | 0.5h   | Uso critico dell'IA: riepilogo dei pattern di errore visti nel corso |
| exercise  | 0.5h   | Esercizi: creare un virtual environment con `python -m venv`, usare `pip` e salvare le dipendenze in `requirements.txt` |
| exercise  | 3h     | Esercizi: impiccato, `ricerca_lineare` con `assert`, `conta_pari` generico, audit IA |
| exercise  | 4h     | Sessioni di problem solving su casi completi |
| exercise  | 4h     | Simulazione e prova finale |
