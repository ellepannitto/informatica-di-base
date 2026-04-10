# Modulo 00 · Prima della prima lezione

Benvenuti al corso **Informatica di Base**.

Prima di iniziare non servono conoscenze pregresse, ma è utile arrivare alla prima lezione con l'ambiente già pronto. Se qualcosa non funziona non bloccatevi: l'installazione fa parte del corso e la sistemeremo insieme.

---

## Obiettivo del modulo 0

Prima della prima lezione vi chiedo di:

- installare [**l'interprete Python**](https://www.python.org/downloads/)
- installare [**Visual Studio Code**](https://code.visualstudio.com/download)
- installare [**Git**](https://git-scm.com/install/)
- fare una piccola prova con il **terminale**
- se usate Windows, installare anche [**WSL**](https://learn.microsoft.com/en-us/windows/wsl/install)

Non è necessario fare tutto in autonomia in modo perfetto. È sufficiente provarci e annotare eventuali problemi.

---

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

---

## 2. Installare Visual Studio Code

Scaricate **VS Code** da [code.visualstudio.com](https://code.visualstudio.com/download). È l'editor che useremo per scrivere e leggere il codice.

Dopo l'installazione:

- aprite VS Code
- installate l'estensione **Python** di Microsoft

Per installare un'estensione:

- aprite il pannello estensioni (`Ctrl+Shift+X` su Windows/Linux, `Cmd+Shift+X` su macOS)
- cercate il nome dell'estensione
- cliccate **Installa**

---

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

---

## 4. Se usate Windows: installare WSL

Se lavorate su Windows, consiglio di installare anche **WSL** (**Windows Subsystem for Linux**), o quantomeno di provarci!

WSL permette di usare un ambiente Linux direttamente dentro Windows. È utile perché molti strumenti di programmazione, comandi di terminale ed esempi del corso funzionano in modo più lineare in un ambiente Unix-like.

Per installarlo:

1. aprite **PowerShell come amministratore**
2. eseguite:

```powershell
wsl --install
```

3. riavviate il computer se richiesto
4. al primo avvio scegliete una distribuzione Linux (di solito Ubuntu va benissimo)

Per verificare che WSL sia disponibile:

```powershell
wsl --status
```

Se l'installazione non funziona subito, non è un problema: ne parliamo a lezione.

---

## 5. Familiarizzare con il terminale

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
- se usate WSL, potete anche cercare **Ubuntu**

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

Su Windows, per WSL:

```powershell
wsl --status
```

Se il controllo va bene, vedrete una riga con il numero di versione.

Se il controllo non va bene, potete vedere:

- un messaggio del tipo "comando non trovato";
- una finestra che propone di installare il programma;
- un messaggio che indica che il comando non è riconosciuto.

Anche questi risultati sono utili: non vanno "sistemati a caso", ma annotati.

### Prime operazioni di orientamento

Non serve diventare esperti subito: basta imparare alcune operazioni di base.

Provate ad eseguire varie volte questi comandi e prendete nota del risultato che ottenete:

```bash
pwd
ls
cd Documenti
cd ..
```

Su Windows fuori da WSL, al posto di `ls` potete trovare anche:

```powershell
dir
```
---

## 6. Libro consigliato

Un testo utile per accompagnare il corso è:

- **Tony Gaddis, Introduzione a Python**

Va bene sia in **italiano** sia in **inglese**.

Non è un testo obbligatorio. **Seguire le lezioni è sufficiente** per affrontare il corso. Il libro può essere utile come supporto aggiuntivo per ripassare o vedere altri esempi.

---

## Se qualcosa non funziona

Non bloccatevi su un problema tecnico iniziale.

Se incontrate un errore:

- annotate il comando che avete eseguito
- annotate il messaggio di errore
- fate uno screenshot se vi è utile
- portate tutto alla prima lezione

L'ambiente di lavoro si costruisce insieme, passo dopo passo.

---

## Riepilogo

Prima della prima lezione l'obiettivo non è "sapere già programmare", ma arrivare con una base operativa minima:

- Python installato e verificato;
- VS Code pronto;
- Git disponibile;
- primo orientamento nel terminale;
- eventuali problemi tecnici annotati in modo chiaro.

Se qualcosa non è ancora a posto, va bene: la prima parte del corso serve anche a costruire insieme questo ambiente di lavoro.
