# Esercizi di preparazione alla prova intermedia — simulazione 2

1. Spiega con parole tue la differenza tra la divisione intera `//` e la divisione reale `/` in Python. Scrivi un breve esempio di utilizzo per ciascuna.

2. Scrivi l'espressione Python che verifica se il numero 252 è divisibile sia per 4 che per 7.

3. Compila la tabella dello stato del seguente programma per l'input `4`:

   ```python
   n = int(input("Inserisci un numero: "))
   prodotto = 1
   i = 1
   while i <= n:
       prodotto = prodotto * 2
       i = i + 1
   print(prodotto)
   ```

   | passo | Riga del codice sorgente | Stato | Output |
   | ----- | ------------------------ | ----- | ------ |
   |       |                          |       |        |

4.  Compila la tabella dello stato del seguente programma per gli input `3` e `7`:

    ```python
    a = int(input())
    b = int(input())
    if a > b:
        z = a - b
    elif a == b:
        z = 0
    else:
        z = b - a
    print(z)
    ```

    | passo | Riga del codice sorgente | Stato | Output |
    | ----- | ------------------------ | ----- | ------ |
    |       |                          |       |        |

5.  Il seguente programma vuole stampare i numeri dispari compresi tra 1 e 10, ma contiene un errore logico. Individua l'errore e correggilo.

    ```python
    i = 1
    while i <= 10:
        if i % 2 == 0:
            print(i)
        i = i + 1
    ```

6.  Il seguente programma vuole stampare la lunghezza di una parola inserita dall'utente, ma contiene un errore. Individua l'errore, spiega perché è un errore e proponi la correzione.

    ```python
    testo = input("Inserisci una parola: ")
    lunghezza = len(testo)
    if lunghezza > 5:
        print("La parola " + testo + " è lunga " + lunghezza + " caratteri")
    else:
        print("Parola corta")
    ```

7. `[EX-SIM2-07]` Scrivi un programma che legge un numero intero positivo `n` e stampa tutti i numeri compresi tra 1 e `n` (incluso). Il programma sostituisce i multipli di 3 con `"fizz"`, i multipli di 5 con `"buzz"` e i multipli sia di 3 che di 5 con `"fizzbuzz"`.

    Esempi:

    ```
    Input:  15
    Output: 1
            2
            fizz
            4
            buzz
            fizz
            7
            8
            fizz
            buzz
            11
            fizz
            13
            14
            fizzbuzz
    ```

    ```
    Input:  7
    Output: 1
            2
            fizz
            4
            buzz
            fizz
            7
    ```

8. `[EX-SIM2-08]` Scrivi un programma che legge numeri interi dall'input, uno per riga, finché l'utente non inserisce `0`. Al termine il programma stampa quanti valori positivi e quanti valori negativi sono stati inseriti (lo zero non viene contato).

    Esempio:

    ```
    Input:  5
            -3
            8
            -1
            2
            0
    Output: Positivi: 3
            Negativi: 2
    ```

9.  Spiega la differenza tra un errore sintattico e un errore semantico (logico) in un programma Python. Fornisci un esempio di ciascuno.

10. Cosa si intende per "stato del programma"? Come cambia lo stato durante l'esecuzione delle istruzioni? Illustra con un breve esempio che usa almeno due variabili.

11. Il seguente programma produce un errore oppure stampa qualcosa? Spiega perché.

    ```python
    x = 5
    if x < 0 and y > 0:
        print("entrambi positivi")
    else:
        print("condizione falsa")
    ```

12. Considera il seguente programma:

    ```python
    parola = input("Inserisci una parola: ")
    if len(parola) == 0 or parola[0] == "A":
        print("vuota o inizia con A")
    else:
        print("non vuota e non inizia con A")
    ```

    a. Cosa stampa se l'utente inserisce la stringa vuota `""`?
    b. Cosa stampa se l'utente inserisce `"Alfa"`?
    c. Cosa succederebbe se Python valutasse sempre entrambe le condizioni, senza cortocircuito?

