# Modulo 00 · Prima della prima lezione

Benvenuti al corso **Informatica di Base**.

Prima di iniziare non servono conoscenze pregresse. È sufficiente arrivare alla prima lezione con l'ambiente già pronto.


## Obiettivo del modulo 0

Prima della prima lezione vi chiedo di:

- portare il **proprio laptop** a lezione
- installare **[l'interprete Python](https://www.python.org/downloads/)**
- installare **[Visual Studio Code](https://code.visualstudio.com/download)** oppure **[VSCodium](https://vscodium.com/)**
- installare **[Git](https://git-scm.com/install/)**
- fare una piccola prova con il **terminale**

Non è necessario fare tutto in autonomia in modo perfetto. È sufficiente provarci e annotare eventuali problemi.

## 1. Installare Python

Andate su [python.org/downloads](https://www.python.org/downloads/) e scaricate una versione stabile recente di Python 3.

Durante l'installazione su Windows:

- spuntate **Add Python to PATH**
- poi cliccate su Installa

Per verificare che l'installazione sia andata a buon fine, aprite il terminale e scrivete:

```bash
python --version
```

oppure, se necessario:

```bash
python3 --version
```

Dovreste vedere qualcosa come `Python 3.x.x`.

Se il comando non funziona:

- provate anche con `python3 --version`;
- su Windows controllate di aver selezionato **Add Python to PATH**;
- se compare un messaggio di errore, annotatelo e portatelo a lezione.

## 2. Installare VSCodium o Visual Studio Code

Scaricate [**Visual Studio Code**](https://code.visualstudio.com/download) oppure [**VSCodium**](https://vscodium.com/). È l'editor che useremo per scrivere e leggere il codice.

Dopo l'installazione:

- aprite l'editor
- installate l'estensione **Python** di Microsoft

Per installare un'estensione:

- aprite il pannello estensioni (`Ctrl+Shift+X` su Windows/Linux, `Cmd+Shift+X` su macOS)
- cercate il nome dell'estensione
- cliccate **Installa**

## 3. Installare Git

**Git** è uno strumento per tenere traccia delle modifiche nei file. In questo modulo ci interessa solo averlo disponibile nell'ambiente di lavoro. La parte operativa su repository, commit e GitHub è rimandata al modulo 11.

Per installarlo:

- **Windows**: scaricate Git da [git-scm.com](https://git-scm.com/downloads/win)
- **macOS**: potete installarlo da [git-scm.com](https://git-scm.com/downloads/mac) oppure tramite Xcode Command Line Tools
- **Linux**: installatelo dal gestore pacchetti della vostra distribuzione

Per verificare l'installazione:

```bash
git --version
```

Dovreste vedere qualcosa come `git version 2.x.x`.

## 4. Familiarizzare con il terminale

Il terminale è uno strumento di lavoro importante. Per chi parte da zero, la prima cosa utile è sapere dove si trova e come si apre.

### Dove si trova il terminale

Su **macOS**:

- aprite **Spotlight** con `Cmd + Spazio`
- scrivete `Terminale`
- aprite l'app **Terminale**

Su **Windows**:

- aprite il menu **Start**
- scrivete `PowerShell` oppure `Terminale`
- aprite **Windows PowerShell** o **Terminal**
- se avete installato Git, potete usare anche **Git Bash** (vedi sotto)

Su **Linux**:

- cercate `Terminale` nelle applicazioni
- in molte distribuzioni funziona anche la scorciatoia `Ctrl + Alt + T`

### Che cosa vedrete quando si apre

Quando il terminale si apre, compare una finestra con:

- un cursore lampeggiante;
- una riga in cui potete scrivere comandi;
- eventualmente un simbolo come `$`, `>` oppure `%`.

Quello è il punto in cui scrivete il comando e poi premete `Invio`.

### Come fare i controlli di installazione

Per controllare un programma installato:

1. aprite il terminale;
2. scrivete il comando esattamente come indicato;
3. premete `Invio`;
4. leggete la risposta.

Esempi:

```bash
python --version
git --version
```

Su alcuni computer Python risponde invece a:

```bash
python3 --version
```

Se il controllo va bene, vedrete una riga con il numero di versione.

Se il controllo non va bene, potete vedere:

- un messaggio del tipo "comando non trovato";
- una finestra che propone di installare il programma;
- un messaggio che indica che il comando non è riconosciuto.

Anche questi risultati sono utili: non vanno "sistemati a caso", ma annotati.

### Git Bash su Windows

Se avete installato Git, avete già a disposizione **Git Bash**: un terminale che usa gli stessi comandi Unix che useremo a lezione (`ls`, `cd`, `pwd`, ...), senza bisogno di WSL.

Per aprirlo:

- cliccate con il tasto destro su una cartella in Esplora file
- scegliete **Open Git Bash here**

oppure:

- aprite il menu **Start**
- cercate **Git Bash**
- si apre una finestra con un prompt simile a `$`

Git Bash è una buona alternativa a PowerShell per chi usa Windows e non ha ancora configurato WSL. I comandi che troverete nel corso funzionano tutti in Git Bash.

## 5. Esplorate il vostro filesystem

Prima della prima lezione provate a esplorare il vostro computer dal terminale. Non c'è nessun rischio: i comandi qui sotto leggono soltanto, non modificano nulla.

I comandi di base funzionano allo stesso modo in bash, zsh e PowerShell. Su Windows potete usare indifferentemente **PowerShell** o **Git Bash**.

### Comandi di base

Provate uno alla volta:

```bash
pwd
```

Dove siete adesso? Qual è la cartella di partenza?

```bash
ls
```

Cosa c'è in questa cartella?

Poi entrate in una cartella che conoscete. La cartella principale dei documenti si chiama:

- `Documenti` o `Documents` su macOS e Linux (dipende dalla lingua)
- `Documents` su Windows (sia in PowerShell che in Git Bash)

```bash
cd Documents
ls
```

Continuate a scendere dove tenete i file universitari, poi tornate su:

```bash
cd NomeDellaCartella
ls
pwd
cd ..
pwd
cd ../..
ls
```

### Nota per chi usa PowerShell su Windows

I comandi sopra funzionano anche in PowerShell. Alcune differenze da tenere a mente:

- i percorsi usano `\` come separatore (`C:\Users\nome\Documents`), anche se PowerShell accetta anche `/`;
- `python3` potrebbe non essere riconosciuto: provate con `python` (senza il `3`).

### Domande su cui riflettere

- Qual è la cartella in cui si apre il terminale per default?
- Quanti livelli di cartelle ci vogliono per arrivare ai vostri appunti?
- Riuscite a trovare dove il vostro computer tiene i file scaricati?

Non serve sapere le risposte: serve aver provato a cercarle. Portate a lezione quello che avete osservato.

## 6. Libro consigliato

Un testo utile per accompagnare il corso è:

- **Tony Gaddis, Introduzione a Python**

Va bene sia in **italiano** sia in **inglese**.

Non è un testo obbligatorio. **Seguire le lezioni è sufficiente** per affrontare il corso. Il libro può essere utile come supporto aggiuntivo per ripassare o vedere altri esempi.

## Se qualcosa non funziona

Non bloccatevi su un problema tecnico iniziale.

Se incontrate un errore:

- annotate il comando che avete eseguito
- annotate il messaggio di errore
- fate uno screenshot se vi è utile
- portate tutto alla prima lezione

L'ambiente di lavoro si costruisce insieme, passo dopo passo.

## Riepilogo

L'obiettivo non è arrivare con tutto perfetto, ma con una base operativa minima: Python, VSCodium o VS Code e Git installati, e una prima esperienza con il terminale. Gli eventuali problemi tecnici li sistemiamo insieme a lezione.
