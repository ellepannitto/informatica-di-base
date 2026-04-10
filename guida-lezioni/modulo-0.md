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

**Git** è uno strumento per tenere traccia delle modifiche nei file. Lo useremo come supporto pratico al lavoro sul codice.

Per installarlo:

- **Windows**: scaricate Git da [git-scm.com](https://git-scm.com/downloads/win)
- **macOS**: potete installarlo da [git-scm.com](https://git-scm.com/downloads/mac) oppure tramite Xcode Command Line Tools
- **Linux**: installatelo dal gestore pacchetti della vostra distribuzione

Per verificare l'installazione:

```bash
git --version
```

Dovreste vedere qualcosa come `git version 2.x.x`.

### Git non e' GitHub

La trascrizione della lezione insisteva su questa distinzione:

- **Git** e' il programma di controllo versione che usiamo sul nostro computer;
- **GitHub** e' una piattaforma web che ospita progetti Git e facilita la collaborazione.

In pratica:

- puoi usare Git anche senza GitHub;
- GitHub diventa utile quando vuoi condividere il progetto, scaricare materiali o collaborare con altre persone.

Il motivo didattico per cui ci interessa Git e' semplice:

- evita di moltiplicare file come `tesi_finale_def_vera2.txt`;
- conserva la storia delle modifiche;
- rende piu' facile tornare indietro e capire che cosa e' cambiato.

### Primo flusso minimo da terminale

La trascrizione `07.srt` rendeva questa parte molto concreta: Git serve soprattutto quando stai lavorando dentro una cartella e vuoi salvare stati successivi del progetto senza duplicare i file a mano.

Una sequenza minima e' questa:

```bash
cd nome-cartella-progetto
git init
git status
git add nome-file
git commit -m "prima versione"
```

Significato dei comandi:

- `git init` trasforma la cartella corrente in un progetto Git;
- `git status` mostra che cosa Git vede come nuovo, modificato o gia' pronto per il commit;
- `git add ...` dice a Git quali cambiamenti vuoi includere nella prossima versione salvata;
- `git commit -m "..."` salva una nuova versione con un messaggio.

Un flusso tipico, molto vicino a quello mostrato a lezione, e' questo:

```bash
cd git-esempio
ls
git init
git add alice.txt
git commit -m "Aggiungo il testo di input"
```

Poi, se aggiungi o modifichi altri file:

```bash
git status
git add .
git commit -m "Aggiungo il primo script Python"
```

Qui `.` significa "la cartella corrente", quindi `git add .` aggiunge tutti i cambiamenti rilevati in quella cartella e nelle sottocartelle.

### Come leggere `git status`

La lezione insisteva sul fatto che `git status` e' il comando da controllare continuamente.

In pratica ti dice:

- se ci sono file nuovi non ancora tracciati;
- se ci sono file gia' tracciati ma modificati;
- se ci sono cambiamenti gia' aggiunti e pronti per il commit;
- se non c'e' nulla da salvare.

Regola pratica:

- se non sei sicura dello stato del progetto, fai `git status`;
- se qualcosa non torna, prima leggi bene l'output e poi decidi il comando successivo.

### La cartella nascosta `.git`

Quando esegui `git init`, Git crea una cartella nascosta chiamata `.git`.

Quella cartella contiene:

- la storia dei commit;
- i riferimenti ai rami;
- i dati interni che permettono a Git di ricostruire gli stati del progetto.

Non va modificata a mano.

Il punto importante e' capire che la storia del progetto non e' "magica": e' salvata in quella cartella nascosta.

### File nuovi, file modificati, file eliminati

La sessione mostrava anche una distinzione molto utile:

- un file puo' essere **nuovo** e non ancora tracciato;
- puo' essere **modificato** dopo un commit precedente;
- puo' essere **eliminato** dal file system, ma la rimozione non entra nella storia finche' non fai un nuovo commit.

Per questo Git lavora sempre su due piani:

- lo stato attuale della cartella;
- lo stato salvato nell'ultimo commit.

### Perche' farlo da terminale

L'editor puo' aiutare con colori, icone e pannelli, ma nella lezione il terminale veniva preferito per un motivo didattico preciso:

- rende espliciti i passaggi;
- funziona in modo simile su molti ambienti;
- aiuta a capire che cosa fa davvero Git;
- evita di nascondere troppo presto la logica dietro un'interfaccia grafica.

Una volta capito il flusso da terminale, usare anche l'editor diventa molto piu' semplice.

### Messaggi di commit

Il commit puo' essere letto come una fotografia commentata dello stato del progetto.

Per questo il messaggio dovrebbe descrivere il cambiamento in modo breve ma concreto, per esempio:

- `Aggiungo il testo di input`
- `Aggiungo il primo script Python`
- `Correggo il conteggio delle frequenze`

### Un comando utile in piu'

Per vedere la storia dei commit:

```bash
git log
```

Non serve usarlo subito in modo avanzato. Per ora basta sapere che esiste e che permette di rileggere la sequenza delle versioni salvate.

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
