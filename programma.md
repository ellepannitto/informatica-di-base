---
title: Informatica di Base
subtitle: Università degli Studi di Salerno | 30% lezione / 70% esercitazione
---

## Prima di iniziare

Prima della prima lezione è consigliato preparare l'ambiente di lavoro. In particolare:

- installare **Python**
- installare **Visual Studio Code** oppure **VSCodium**
- installare **Git**
- prendere un primo contatto con il **terminale**

Per una guida più dettagliata vedi [guida-lezioni/modulo-0.slides.html](guida-lezioni/modulo-0.slides.html).

Se qualcosa non funziona non è un problema: l'installazione dell'ambiente fa parte del corso e verrà ripresa anche a lezione.

## Libro consigliato

Il testo consigliato è **Introduzione a Python** di **Tony Gaddis**, in italiano oppure in inglese.

Non è obbligatorio: **seguire le lezioni è sufficiente** per affrontare il corso.
Il libro è solo un supporto aggiuntivo per chi vuole ripassare o leggere altri esempi.

I moduli su **Git**, **terminale** e parte del materiale sugli **automi** seguono soprattutto le lezioni e le esercitazioni, piu che il libro.

## Sistema di valutazione

- Ci sono **3 prove intermedie facoltative**, una per blocco (moduli 1–3, 4–6, 7–8). Si svolgono durante le ore di corso e sono già comprese nel monte ore totale.
- Lo **scritto finale** copre i tre blocchi (moduli 1–9). Per ogni blocco viene considerata la valutazione più favorevole tra prova intermedia e scritto finale: le prove già superate alleggeriscono lo scritto e possono migliorare il voto complessivo.
- L'esame si conclude con un **orale** che include live coding e domande di teoria. I moduli 10 e 11 sono testati solo in questa sede.

## Moduli

### 01 | Introduzione alla programmazione e Python | slides=guida-lezioni/modulo-1.slides.html

| Tipologia | Durata | Libro            | Argomento                                                                                                                    |
| --------- | ------ | ---------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| theory    | 0.5h   | app. A           | Introduzione al corso: obiettivi, metodo di lavoro e perché Python — prima lezione con tempo dedicato al setup dell'ambiente |
| exercise  | 1h     | cap. 1.5/2.7     | REPL, tipi e operazioni fondamentali: interi, float, stringhe                                                                |
| theory    | 0.5h   | cap. 1.4         | Python come linguaggio formale: vocabolario, sintassi, semantica, interprete e compilatore                                   |
| theory    | 0.5h   | cap. 1.1/1.2/1.3 | Architettura di Von Neumann: CPU (ALU, registri, Control Unit), RAM, disco e dispositivi I/O                                 |
| theory    | 0.5h   | cap. 2.1/2.2     | Cos'è un programma: input/elaborazione/output, file system e sistema operativo                                               |
| theory    | 0.5h   | cap. 2.3/2.4     | Ambiente di lavoro: interprete, editor e terminale                                                                           |
| exercise  | 1.5h   | -                | Terminale: pwd, cd, ls, percorsi assoluti e relativi, lancio di script Python                                                |
| exercise  | 1h     | -                | Cosa stampa questo programma? Script da leggere, prevedere ed eseguire                                                       |

### 02 | Variabili e strutture decisionali | slides=guida-lezioni/modulo-2.slides.html

| Tipologia | Durata | Libro            | Argomento                                                                                 |
| --------- | ------ | ---------------- | ----------------------------------------------------------------------------------------- |
| theory    | 0.5h   | cap. 2.5         | Espressioni e istruzioni                                                                  |
| theory    | 0.5h   | cap. 2.5         | Variabili, assegnamento e stato: sintassi, semantica e tracciamento                       |
| theory    | 0.5h   | cap. 2.6         | `input()` e casting con `int()`, `float()`, `str()`                                       |
| exercise  | 0.5h   | -                | Esercizi: variabili, input/output, operazioni su stringhe e numeri                        |
| theory    | 0.5h   | cap. 3.3/3.6     | Tipo `bool`, operatori di confronto e operazioni su stringhe che restituiscono booleani   |
| theory    | 0.5h   | cap. 3.1/3.2/3.4 | Sintassi e semantica di `if`, `if-else`, `elif` e condizioni annidate                     |
| theory    | 1h     | cap. 3.5         | Condizioni composte: `and`, `or`, `not`, tabelle di verità e precedenza degli operatori   |

### 03 | Dall'if al while | slides=guida-lezioni/modulo-3.slides.html

| Tipologia | Durata | Libro        | Argomento                                                                              |
| --------- | ------ | ------------ | -------------------------------------------------------------------------------------- |
| theory    | 1h     | -                | Errori nel codice: leggerli e correggerli                                                 |
| exercise  | 0.5h   | -                | Testing e casi limite: confrontare output atteso e reale, programmi che sembrano corretti |
| theory    | 0.5h   | -                | Valutazione lazy e leggi di De Morgan                                                     |
| theory    | 0.5h   | cap. 4.1/4.2 | Dal `if` al `while`: motivazione, struttura e tabella comparativa                      |
| exercise  | 0.5h   | -            | Esercizi: contatori, dispari, potenze, sequenze e stop-word                            |
| theory    | 0.5h   | cap. 4.7     | Cicli annidati                                                                         |
| exercise  | 1h     | -            | Esercizi                                                                               |
| theory    | 0.5h   | -            | Lo stato del programma durante un `while`: tracce di esecuzione                        |

### P1 | Prova intermedia 1 | prova=true
| Tipologia | Durata | Libro | Argomento                                                                                 |
| --------- | ------ | ----- | ----------------------------------------------------------------------------------------- |
| exercise  | 1.5h     | —     | Argomenti: moduli 1-3 (basi, tipi, memoria, stato, strutture decisionali, semplici while) |


### 04 | Iterazione con sentinelle, e liste | slides=guida-lezioni/modulo-4.slides.html
| Tipologia | Durata | Libro                | Argomento                                                                                        |
| --------- | ------ | -------------------- | ------------------------------------------------------------------------------------------------ |
| theory    | 0.5h   | cap. 4.5/4.6         | Sentinelle                                                                                       |
| exercise  | 1h     | -                    | Esercizi: input ripetuto, conteggi, classificazione, tabellina con validazione, vocali           |
| theory    | 0.5h   | -                    | Automi a stati finiti e il `while`: stato `resta`, stato `fine`, self-loop                       |
| exercise  | 1h     | -                    | Esercizi: riconoscimento di stringhe con automi                                                  |
| theory    | 1h     | cap. 7.1/7.2/7.3/7.4 | Liste                                                                                            |
| exercise  | 1h     | -                    | Esercizi: costruire liste, accedere agli elementi, scorrere con `while`                          |
| exercise  | 1h     | -                    | Esercizi: verifica di proprietà anche su liste annidate, serie multiple, conteggio per categoria |

### 05 | Funzioni e procedure | slides=
| Tipologia | Durata | Libro | Argomento                                                                                                                           |
| --------- | ------ | ----- | ----------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | cap. ___ | [Definire funzioni: parametri, chiamata, valori di ritorno](guida-lezioni/modulo-6.slides.html#mod6-parametri)                             |
| exercise  | 1h     | cap. ___ | Esercizi: scomporre un programma in funzioni piccole                                                                                |
| theory    | 0.5h   | cap. ___ | [Firma di una funzione, black box e responsabilità singola](guida-lezioni/modulo-6.slides.html#mod6-black-box)                             |
| theory    | 0.5h   | cap. ___ | Scope: variabili locali, parametri e visibilità dei nomi dentro e fuori una funzione                                                |
| exercise  | 3h     | cap. ___ | [Esercizi: `my_strip`, `my_join`, `is_palindroma` e semplici utility riusabili](guida-lezioni/modulo-6.slides.html#mod6-esercizi-funzioni) |


### 06 | Memoria e passaggio degli argomenti | slides=
| Tipologia | Durata | Libro | Argomento                                                                                                                                    |
| --------- | ------ | ----- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | cap. ___ | [Funzioni vs procedure: quando restituire un valore e quando produrre solo un effetto](guida-lezioni/modulo-6.slides.html#mod6-procedure)           |
| theory    | 1h     | cap. ___ | [Variabili come nomi associati a valori e oggetti; stato della memoria durante l'esecuzione](guida-lezioni/modulo-7.slides.html#mod7-memoria-liste) |
| exercise  | 2h     | cap. ___ | Esercizi: elaborare liste lette da input, inversione, conteggi e prime trasformazioni                                                        |
| theory    | 1h     | cap. ___ | Passaggio per valore e per riferimento e side effects                                                                                        |
| exercise  | 1h     | cap. ___ | [Esercizi: modifiche in-place, copie, effetti collaterali e debugging di funzioni](guida-lezioni/modulo-7.slides.html#mod7-copie)                   |

### P2 | Prova intermedia 2 | prova=true
| Tipologia | Durata | Libro | Argomento |
| --------- | ------ | ----- | --------- |
| exercise  | 1.5h     | — | Argomenti: moduli 4-7 (while e convalida, liste e input, funzioni)|
| exercise  | 1.5h     | — | Correzione della prova |

### 07 | Ciclo for e iterazione | slides=
| Tipologia | Durata | Libro | Argomento                                                                                                                  |
| --------- | ------ | ----- | -------------------------------------------------------------------------------------------------------------------------- |
| theory    | 0.5h   | cap. ___ | [Il ciclo `for` su stringhe, liste e `range()`](guida-lezioni/modulo-8.slides.html#mod8-for)                               |
| theory    | 0.5h   | cap. ___ | [Cicli annidati con `for`: righe, colonne, pattern e costruzione di stringhe](guida-lezioni/modulo-8.slides.html#mod8-for) |
| exercise  | 1h     | cap. ___ | Esercizi con `for`: conteggi, scansioni, accumuli e trasformazioni su sequenze                                             |
| exercise  | 1h     | cap. ___ | Esercizi: pattern di stampa, triangoli, rettangoli e uso degli indici nei cicli annidati                                   |

### 08 | File e formati strutturati | slides=
| Tipologia | Durata | Libro | Argomento                                                                                                                                                                               |
| --------- | ------ | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | cap. ___ | [File di testo: aprire, leggere e scorrere un file riga per riga con `for`](guida-lezioni/modulo-9.slides.html#mod9-file)                                                                      |
| theory    | 0.5h   | cap. ___ | [Formati di input/output: testo semplice, CSV, JSON e HTML](guida-lezioni/modulo-9.slides.html#mod9-formati)                                                                                   |
| theory    | 0.5h   | cap. ___ | [Differenza tra standard input, file aperto con `open()` e parametri da riga di comando](guida-lezioni/modulo-9.slides.html#mod9-file) |
| exercise  | 0.5h   | cap. ___ | [Esplorazione rapida da terminale: `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc`, `uniq` e utility simili per leggere file e cartelle](guida-lezioni/modulo-9.slides.html#mod9-terminale) |
| exercise  | 0.5h   | cap. ___ | [Esercizi da terminale: ispezionare file e filtrare contenuti con `cat`, `head`, `tail`, `grep`, `cut`, `sort`, `wc` e `uniq`](guida-lezioni/modulo-9.slides.html#mod9-terminale)              |
| exercise  | 2h     | cap. ___ | Esercizi su file di testo, CSV e JSON: lettura, scrittura e semplici trasformazioni |
| exercise  | 1h     | cap. ___ | Esercizi: parametri da riga di comando, output su file e piccole pipeline di elaborazione |


### P3 | Prova intermedia 3 | prova=true
| Tipologia | Durata | Libro | Argomento                                                                  |
| --------- | ------ | ----- | -------------------------------------------------------------------------- |
| exercise  | 1h     | — | Argomenti: moduli 8-9 (`for`, file, input/output, terminale, formati) |
| exercise  | 1h     | — | Correzione della prova                                                     |

### 09 | Dizionari, set e organizzazione dell'informazione | slides=
| Tipologia | Durata | Libro | Argomento                                                                                                                          |
| --------- | ------ | ----- | ---------------------------------------------------------------------------------------------------------------------------------- |
| theory    | 1h     | cap. ___ | [Dizionari: chiavi, valori, accesso, aggiornamento e casi d'uso](guida-lezioni/modulo-10.slides.html#mod10-dizionari)                       |
| theory    | 1h     | cap. ___ | [Set: appartenenza, eliminazione dei duplicati e operazioni di base](guida-lezioni/modulo-10.slides.html#mod10-set)                 |
| exercise  | 2h     | cap. ___ | [Esercizi: frequenze, raggruppamenti, conteggi e lookup con dizionari](guida-lezioni/modulo-10.slides.html#mod10-frequenze)                 |


### 10 | Git e controllo di versione | slides=
| Tipologia | Durata | Libro | Argomento                                                                                             |
| --------- | ------ | ----- | ----------------------------------------------------------------------------------------------------- |
| theory    | 1h     | — | [Git: repository, working tree, staging area, commit e storia del progetto](guida-lezioni/modulo-11.slides.html#mod11-git)                             |
| theory    | 1h     | — | [Git da terminale: `git init`, `git status`, `git add`, `git commit`, `git log`](guida-lezioni/modulo-11.slides.html#mod11-git)                        |
| exercise  | 1h   | — | Esercizi: creare un repository locale, tracciare file, salvare versioni e leggere `git status`        |
| theory    | 0.5h   | — | [GitHub: repository remoto, `clone`, `push`, `pull` e collaborazione di base](guida-lezioni/modulo-11.slides.html#mod11-github)                           |
| exercise  | 0.5h   | — | Esercizi: clonare un repository, aggiungere modifiche e pubblicarle sul remoto                        |
| exercise  | 1h     | — | Esercizi: leggere differenze tra file non tracciati, modificati e già staged                          |
| exercise  | 1h     | — | Mini-laboratorio finale: usare Git per tenere traccia di uno script Python e dei file di input/output |
