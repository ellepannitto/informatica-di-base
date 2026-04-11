# Modulo 11 · Git e controllo di versione

---

## Autovalutazione

- Sai distinguere tra Git e GitHub?
- Sai inizializzare un repository locale?
- Sai leggere `git status`?
- Sai aggiungere file allo staging area e creare commit?
- Sai consultare la storia del progetto con `git log`?
- Sai riconoscere file non tracciati, modificati e già staged?
- Sai clonare un repository e sincronizzarlo con un remoto?

---

<a id="mod11-git"></a>
## Che cos'e' Git

Git e' uno strumento per tenere traccia delle modifiche nei file.

Serve soprattutto per:

- evitare di moltiplicare file come `tesi_finale_def_vera2.txt`;
- conservare la storia delle modifiche;
- tornare indietro quando serve;
- collaborare su uno stesso progetto.

### Git non e' GitHub

- **Git** e' il programma di controllo versione che usiamo sul nostro computer;
- **GitHub** e' una piattaforma web che ospita progetti Git e facilita la collaborazione.

Puoi usare Git anche senza GitHub.
GitHub diventa utile quando vuoi condividere un progetto o collaborare con altre persone.

---

## Primo flusso minimo da terminale

```bash
cd nome-cartella-progetto
git init
git status
git add nome-file
git commit -m "prima versione"
```

Significato dei comandi:

- `git init` trasforma la cartella corrente in un progetto Git;
- `git status` mostra lo stato dei file;
- `git add ...` prepara i cambiamenti per il prossimo commit;
- `git commit -m "..."` salva una nuova versione con un messaggio.

Un flusso tipico:

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

Qui `.` significa "la cartella corrente".

---

## Come leggere `git status`

`git status` e' il comando da controllare continuamente.

Ti dice:

- se ci sono file nuovi non ancora tracciati;
- se ci sono file gia' tracciati ma modificati;
- se ci sono cambiamenti gia' aggiunti e pronti per il commit;
- se non c'e' nulla da salvare.

Regola pratica:

- se non sei sicura dello stato del progetto, fai `git status`;
- se qualcosa non torna, prima leggi bene l'output e poi decidi il comando successivo.

---

## La cartella `.git`

Quando esegui `git init`, Git crea una cartella nascosta chiamata `.git`.

Quella cartella contiene:

- la storia dei commit;
- i riferimenti ai rami;
- i dati interni che permettono a Git di ricostruire gli stati del progetto.

Non va modificata a mano.

---

## File nuovi, modificati, staged

Un file puo' essere:

- **nuovo** e non ancora tracciato;
- **modificato** dopo un commit precedente;
- **staged**, cioe' gia' aggiunto per il prossimo commit.

Per questo Git lavora sempre su due piani:

- lo stato attuale della cartella;
- lo stato salvato nell'ultimo commit.

---

## Messaggi di commit e cronologia

Il commit si puo' leggere come una fotografia commentata dello stato del progetto.

Per questo il messaggio dovrebbe descrivere il cambiamento in modo breve ma concreto, per esempio:

- `Aggiungo il testo di input`
- `Aggiungo il primo script Python`
- `Correggo il conteggio delle frequenze`

Per vedere la storia dei commit:

```bash
git log
```

---

<a id="mod11-github"></a>
## GitHub e repository remoti

GitHub e' utile per:

- ospitare un repository remoto;
- condividere il codice;
- collaborare con altre persone.

Comandi base:

```bash
git clone URL_DEL_REPOSITORY
git push
git pull
```

- `clone` scarica un repository remoto in locale;
- `push` pubblica i commit locali sul remoto;
- `pull` aggiorna il repository locale con i cambiamenti remoti.

---

## Perche' farlo da terminale

L'editor puo' aiutare con colori, icone e pannelli, ma il terminale ha alcuni vantaggi didattici:

- rende espliciti i passaggi;
- funziona in modo simile su molti ambienti;
- aiuta a capire che cosa fa davvero Git;
- non nasconde troppo presto la logica dietro un'interfaccia grafica.

---

## Esercizi

1. crea una cartella e inizializza un repository Git;
2. aggiungi uno script Python e fai un primo commit;
3. modifica lo script e fai un secondo commit;
4. usa `git status` per distinguere file non tracciati, modificati e staged;
5. usa `git log` per leggere la storia dei commit;
6. clona un repository remoto e osservane la struttura.

---

## Riepilogo

Questo modulo raccoglie il materiale su:

- Git come strumento di controllo di versione;
- differenza tra Git e GitHub;
- flusso minimo `init` -> `status` -> `add` -> `commit` -> `log`;
- lettura dello stato dei file;
- primo uso di repository remoti con `clone`, `push` e `pull`.
