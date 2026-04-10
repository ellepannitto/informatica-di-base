# Modulo 00 · Prima della prima lezione

Benvenuti al corso **Informatica di Base**.

Prima di iniziare non servono conoscenze pregresse, ma è utile arrivare alla prima lezione con l'ambiente già pronto. Se qualcosa non funziona non bloccatevi: l'installazione fa parte del corso e la sistemeremo insieme.

---

## Obiettivo del modulo 0

Prima della prima lezione vi chiedo di:

- installare **Python**
- installare **Visual Studio Code**
- installare **Git**
- usare il **terminale**
- se usate Windows, installare anche **WSL**

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

---

## 2. Installare Visual Studio Code

Scaricate **VS Code** da [code.visualstudio.com](https://code.visualstudio.com/download). È l'editor che useremo per scrivere e leggere il codice.

Dopo l'installazione:

- aprite VS Code
- installate l'estensione **Python** di Microsoft
- facoltativo ma consigliato: installate anche l'estensione **GitLens** o familiarizzate con il pannello Source Control di VS Code

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

Se lavorate su Windows, consiglio di installare anche **WSL** (**Windows Subsystem for Linux**).

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

Il terminale è uno strumento di lavoro importante. Non serve diventare esperti subito: basta imparare alcune operazioni di base.

Provate questi comandi:

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

L'idea minima è questa:

- `pwd` mostra dove vi trovate
- `ls` o `dir` mostra cosa c'è nella cartella
- `cd nome_cartella` entra in una cartella
- `cd ..` torna alla cartella superiore

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

Prima della prima lezione l'obiettivo non e' "sapere gia' programmare", ma arrivare con una base operativa minima:

- Python installato e verificato;
- VS Code pronto;
- Git disponibile;
- primo orientamento nel terminale;
- eventuali problemi tecnici annotati in modo chiaro.

Se qualcosa non e' ancora a posto, va bene: la prima parte del corso serve anche a costruire insieme questo ambiente di lavoro.
