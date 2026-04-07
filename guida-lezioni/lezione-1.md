1. Cos'è un programma (60 min)

    Hardware vs Software: Un sistema informatico è una combinazione di hardware (componenti fisici come CPU e dischi) e software (i programmi che girano su di esso).
    Ciclo Input/Elaborazione/Output: La CPU riceve istruzioni e dati da un input o dalla memoria, li elabora e invia i risultati a un output o alla memoria di massa.
    Codice Sorgente vs Codice Macchina:
        Codice Sorgente: Scritto in linguaggi ad alto livello (come Python) facili da capire per l'uomo, usando parole come print o while.
        Codice Macchina: L'unico linguaggio compreso direttamente dalla CPU, composto da sequenze di numeri binari (0 e 1). Una singola istruzione ad alto livello viene tradotta in molte istruzioni in codice macchina.
    Sistema Operativo e RAM: Il Sistema Operativo gestisce le risorse hardware. Quando un programma viene eseguito, viene caricato nella RAM (Random Access Memory), una memoria veloce ma volatile (perde i dati allo spegnimento).
    File System: Il metodo con cui il sistema organizza i file (es. .py o .html) per l'archiviazione a lungo termine.


	2. Architettura di Von Neumann (30 min)

    Stored Program Concept: L'idea chiave è che sia i dati che le istruzioni sono memorizzati insieme nella memoria principale (RAM) sotto forma di numeri binari.
    Componenti Principali:
        CPU: Il "cervello" che processa le istruzioni.
        Memoria Principale (RAM e ROM): La ROM (Read-Only Memory) è non volatile e contiene istruzioni fisse come il BIOS, necessario per l'avvio.
        I/O: Interfacce per l'ingresso e l'uscita dei dati.
    Registri della CPU: Piccole unità di memoria ultra-veloce all'interno del processore:
        PC (Program Counter): Punta all'indirizzo della prossima istruzione da caricare.
        MAR & MBR: Gestiscono gli indirizzi e i dati in transito tra CPU e RAM.
        CIR: Contiene l'istruzione che viene attualmente decodificata ed eseguita.
        Accumulatore: Memorizza i risultati delle operazioni logico-aritmetiche.
    Ciclo Fetch-Decode-Execute: La CPU ripete continuamente tre fasi: preleva l'istruzione dalla memoria (Fetch), la interpreta (Decode) e la compie (Execute).

	3. Ambiente di lavoro (30 min)

    Linguaggi ad Alto Livello vs Basso Livello:
        Alto livello (Python, Java): Portabili, facili da scrivere, ma richiedono traduzione.
        Basso livello (Assembly, Machine Code): Molto veloci ed efficienti, ma difficili da programmare e specifici per un'architettura. L'Assembly usa "mnemonici" (codici abbreviati come ADD o MOV).
    Tipi di Traduttori:
        Interprete (Python): Traduce ed esegue un'istruzione alla volta. È utile per lo sviluppo perché segnala subito gli errori.
        Compilatore (C++, Java): Traduce tutto il codice in un file eseguibile indipendente. È più veloce e ottimizzato.
        Assembler: Traduce specificamente il linguaggio Assembly in codice macchina.
    Strumenti:
        VS Code: Un editor di testo/IDE che aiuta con numeri di riga e sintassi colorata.
        Shell/Terminale: Dove l'utente interagisce con l'interprete per eseguire lo script (es. python3 nome_file.py).


Architettura degli Elaboratori e Fondamenti di Programmazione
1. Cos'è un programma (60 min)
Un sistema informatico è composto dall'unione di hardware (componenti fisici) e software (programmi che vengono eseguiti).
Il ciclo Input/Elaborazione/Output
Un programma è essenzialmente una sequenza di istruzioni. Il suo funzionamento segue un ciclo fondamentale:

    Input: Dati inseriti nel sistema per l'elaborazione o l'archiviazione.
    Elaborazione: La CPU riceve istruzioni e dati dalla memoria o dall'input e li processa.
    Output: I risultati dell'elaborazione vengono inviati a un dispositivo di uscita o trasferiti alla memoria di massa (storage secondario).

Codice Sorgente vs Codice Macchina

    Codice Macchina: È l'unico linguaggio compreso direttamente dalla CPU, composto interamente da numeri binari (0 e 1).
    Codice Sorgente: È il codice scritto dai programmatori in un linguaggio leggibile dall'uomo (come Python). Un'istruzione ad alto livello è "one-to-many", ovvero viene tradotta in molteplici istruzioni in linguaggio macchina.

Sistema Operativo e Memoria

    Sistema Operativo (OS): Gestisce l'hardware e carica i programmi dal disco alla RAM per l'esecuzione.
    RAM (Random Access Memory): Memoria principale volatile; i dati vengono persi quando il computer viene spento.
    ROM (Read-Only Memory): Memoria non volatile che contiene istruzioni fisse, come il BIOS, necessarie per l'avvio del sistema.


--------------------------------------------------------------------------------
2. Architettura di Von Neumann (30 min)
La maggior parte dei computer moderni si basa sul design di Von Neumann, noto come stored program concept.
Elementi Chiave

    Dati e istruzioni sono entrambi memorizzati come numeri binari nella memoria principale.
    Le istruzioni vengono prelevate dalla memoria una alla volta in modo seriale.

I Registri della CPU
Per gestire il ciclo di elaborazione, la CPU utilizza cinque registri speciali:

    PC (Program Counter): Contiene l'indirizzo della prossima istruzione da prelevare.
    MAR (Memory Address Register): Contiene l'indirizzo della cella di memoria attualmente in uso per la lettura o scrittura.
    MBR (Memory Buffer Register): Contiene i dati o le istruzioni appena letti dalla memoria o in attesa di essere scritti.
    CIR (Current Instruction Register): Contiene l'istruzione che viene attualmente decodificata ed eseguita.
    ACC (Accumulatore): Memorizza i risultati temporanei delle operazioni logico-aritmetiche.

Il Ciclo Fetch-Decode-Execute
La CPU ripete continuamente queste fasi: preleva l'istruzione dalla RAM (Fetch), la interpreta (Decode) e la esegue (Execute).

--------------------------------------------------------------------------------
3. Ambiente di lavoro e Traduttori (30 min)
Linguaggi di Alto e Basso Livello

    Alto Livello (es. Python, Java): Più vicini al linguaggio umano, facili da leggere e portabili su diverse architetture.
    Basso Livello (es. Assembly): Molto vicini all'architettura fisica. L'Assembly usa mnemonici (codici brevi come ADD o MOV) per rappresentare le istruzioni macchina.

Tipi di Traduttori
Poiché il computer non capisce il codice sorgente, serve un traduttore:

    Interprete (es. Python): Traduce ed esegue il codice un'istruzione alla volta. Gli errori sono facili da individuare durante lo sviluppo, ma l'esecuzione è più lenta.
    Compilatore (es. C++): Traduce l'intero programma in un file eseguibile unico. Una volta compilato, il programma è molto veloce.
    Assembler: Traduce specificamente il linguaggio Assembly in codice macchina.

Strumenti del Corso

    VS Code: Un ambiente di sviluppo (IDE) che offre funzioni come l'evidenziazione della sintassi e i numeri di riga.
    Terminale/Shell: Interfaccia usata per lanciare l'interprete e testare gli script (es: python3 nome_script.py).


--------------------------------------------------------------------------------
Esempio di Sintassi Python (da mostrare in aula)

# Definizione di una variabile e calcolo
x = 10
y = x + 5

# Istruzione condizionale
if y > 12:
    print("Il valore è maggiore di 12") # Output
``` [30, 31]


Il ciclo Fetch-Decode-Execute (noto anche come ciclo Fetch-Execute) è il processo fondamentale che la CPU segue per elaborare ogni singola istruzione di un programma. Questo ciclo si basa sull'architettura di Von Neumann, in cui le istruzioni vengono prelevate dalla memoria principale una alla volta e in ordine sequenziale.
Il funzionamento dettagliato del ciclo può essere suddiviso nelle seguenti fasi:
1. Fase di Fetch (Prelievo)
In questa fase, la CPU recupera l'istruzione dalla memoria:

    Indirizzamento: L'indirizzo di memoria contenuto nel Program Counter (PC), che indica la prossima istruzione da eseguire, viene copiato nel Memory Address Register (MAR).
    Aggiornamento PC: Il Program Counter viene incrementato di uno, in modo da puntare già all'indirizzo dell'istruzione successiva.
    Accesso alla Memoria: Il processore invia un segnale tramite il bus degli indirizzi verso la RAM, puntando alla cella indicata nel MAR.
    Trasferimento Dati: L'istruzione contenuta in quell'indirizzo viene inviata attraverso il bus dei dati e salvata nel Memory Buffer Register (MBR) (chiamato anche MDR).
    Caricamento Istruzione: Il contenuto dell'MBR viene infine copiato nel Current Instruction Register (CIR).

2. Fase di Decode (Decodifica)
Una volta che l'istruzione è al sicuro nel CIR, deve essere interpretata:

    Interpretazione: L'unità di controllo della CPU decodifica l'istruzione presente nel CIR per capire quale operazione deve essere eseguita (ad esempio un'addizione, un caricamento di dati o uno spostamento).

3. Fase di Execute (Esecuzione)
Infine, l'azione viene effettivamente compiuta:

    Esecuzione: La CPU esegue l'istruzione. Se si tratta di un calcolo matematico o logico, viene utilizzata l'ALU (Arithmetic Logic Unit).
    Memorizzazione dei risultati: I risultati dell'elaborazione vengono solitamente memorizzati in un registro speciale chiamato Accumulatore (ACC).

4. Ripetizione
Dopo l'esecuzione, il ciclo ricomincia immediatamente dal primo passo. Questo processo continua incessantemente finché non ci sono più istruzioni disponibili o il computer viene spento.
In sintesi: I registri lavorano come una catena di montaggio: il PC tiene il segno di dove siamo, il MAR e l'MBR fanno da ponte con la memoria esterna, il CIR tiene l'istruzione "sotto i ferri" per la decodifica e l'Accumulatore raccoglie il prodotto finito dell'operazione.

L'interprete Python gestisce la memoria durante l'esecuzione agendo come un traduttore che processa il codice un'istruzione alla volta. La gestione della memoria avviene principalmente attraverso l'uso di tabelle di memoria che associano i nomi delle variabili (identificatori) ai loro valori o indirizzi fisici.
Ecco i dettagli fondamentali su come avviene questa gestione:
1. Gestione dei nomi e delle variabili
Quando l'interprete esegue un'istruzione di assegnamento (es. x = 5), segue una semantica precisa:

    Valutazione: Calcola il valore dell'espressione a destra dell'uguale.
    Creazione: Se necessario, crea una cella nella tabella di memoria dedicata a quell'identificatore.
    Associazione: Assegna il valore calcolato al nome della variabile nella tabella.

2. Memoria temporanea e Funzioni
Quando viene invocata una funzione, l'interprete non usa la tabella di memoria principale, ma crea una tabella di memoria temporanea. Questa serve a tenere traccia delle operazioni e delle variabili locali interne alla funzione. Una volta che la funzione termina e restituisce l'output, il controllo torna al flusso principale e la memoria temporanea viene gestita di conseguenza.
3. Gestione di tipi complessi (Liste e Indirizzi)
Per oggetti più complessi come le liste, l'interprete non memorizza l'intero contenuto direttamente sotto il nome della variabile, ma utilizza gli indirizzi di memoria:

    Puntatori: La variabile memorizza un riferimento (es. mem(2147478276)) alla posizione fisica dei dati.
    Condivisione della memoria: Se si assegna una lista a una nuova variabile (es. b = a), l'interprete copia l'indirizzo di memoria, non i dati. Di conseguenza, entrambe le variabili punteranno alla stessa lista e le modifiche apportate tramite una saranno visibili anche dall'altra.
    Copia profonda: Per evitare questo comportamento, è necessario istruire l'interprete a creare una copia effettiva dei dati in una nuova cella di memoria (es. tramite copy.deepcopy).

4. Gestione durante i cicli
Durante l'esecuzione di un ciclo for, l'interprete aggiorna dinamicamente la tabella di memoria. Ad ogni iterazione, prende un elemento dall'oggetto iterabile e lo assegna alla variabile del ciclo, sovrascrivendo il valore precedente nella tabella di memoria fino alla fine del ciclo.
5. Interazione con l'Hardware
Tutte queste operazioni avvengono nella RAM (Random Access Memory), la memoria principale del computer. Essendo una memoria volatile, tutte le tabelle di memoria e i dati gestiti dall'interprete vengono persi non appena il programma termina o il computer viene spento.

In Python, il ruolo dei puntatori (o più precisamente degli indirizzi di memoria) è fondamentale per la gestione dei tipi complessi, come le liste, e differisce significativamente dal modo in cui vengono gestiti i tipi di dati semplici.
Ecco come funzionano e qual è il loro ruolo principale secondo le fonti:
1. Riferimento a oggetti complessi
A differenza dei tipi fondamentali (come gli interi), dove una variabile memorizza direttamente il valore (ad esempio, a = 1), per i tipi complessi come le liste, la variabile non contiene i dati stessi, ma un indirizzo di memoria che punta alla posizione fisica in cui quei dati sono archiviati.

    Esempio: Se definiamo a =, l'identificatore a assumerà come valore un riferimento del tipo mem(2147478276).

2. Gestione dell'assegnamento e condivisione della memoria
Il ruolo dei puntatori diventa evidente durante l'operazione di assegnamento tra due variabili (b = a):

    Copia dell'indirizzo: Invece di creare una nuova copia fisica dei dati, l'interprete Python copia semplicemente l'indirizzo di memoria.
    Condivisione: Di conseguenza, sia la variabile a che la variabile b punteranno alla stessa cella di memoria.

3. Conseguenze sulle modifiche (Effetto collaterale)
Poiché entrambe le variabili fanno riferimento allo stesso indirizzo, qualsiasi modifica apportata tramite una variabile influenzerà anche l'altra.

    Se si esegue b = 1000, la modifica sarà visibile anche stampando la lista a, poiché l'oggetto fisico in memoria a cui entrambi puntano è stato alterato.

4. Soluzione: Copia profonda
Per evitare che il sistema utilizzi lo stesso indirizzo di memoria (puntatore) quando si desidera una copia indipendente, è necessario utilizzare funzioni specifiche come copy.deepcopy(). Questa operazione crea una nuova cella di memoria con un indirizzo diverso, contenente una copia effettiva dei dati originali.
In sintesi, i puntatori in Python servono a rendere più efficiente la gestione della memoria evitando di duplicare inutilmente oggetti pesanti, ma richiedono attenzione poiché portano alla condivisione involontaria dei dati tra variabili diverse.