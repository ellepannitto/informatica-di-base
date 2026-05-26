# Esercizi di preparazione alla seconda prova intermedia

## Teoria

1. Qual è la differenza tra una **funzione pura** e una **funzione void**? Come si riconosce quale tipo si sta usando?

2. Qual è la differenza tra l'operatore `==` e l'operatore `is` quando si confrontano due liste? In quale caso restituiscono risultati diversi?

3. Cosa si intende per **alias**? Fai un esempio in Python e spiega cosa succede se si modifica la lista attraverso uno dei due nomi.

4. Descrivi il processo di valutazione della **guardia** in un ciclo `while`: quando viene controllata la prima volta e quando le volte successive?

5. Qual è lo stato di una variabile contatore `i` nel momento esatto in cui il ciclo `while` termina?


## Tracciamento dello stato

1. Compila la tabella dello stato per il seguente programma:

   ```python
   numeri = [3, 7, 2]
   i = 0
   totale = 0
   while i < len(numeri):
       totale = totale + numeri[i]
       i = i + 1
   print(totale)
   ```

   | Passo | Codice sorgente | Stato del programma | Output |
   | ----- | --------------- | ------------------- | ------ |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |
   |       |                 |                     |        |

2. Compila la tabella dello stato per il seguente programma:

   ```python
   def quadrato(n):
       n = n * n
       return n

   x = 4
   y = quadrato(x)
   print(x)
   print(y)
   ```

   | Passo | Codice sorgente        | Stato del programma | Output |
   | ----- | ---------------------- | ------------------- | ------ |
   | 1     | `x = 4`                | `x->4`              |        |
   | 2     | chiama `quadrato(x)`   | `x->4, n->4`        |        |
   |       |                        |                     |        |
   |       |                        |                     |        |
   |       |                        |                     |        |
   |       |                        |                     |        |
   |       |                        |                     |        |


## Trovare l'errore

1.  Il seguente programma vuole stampare il doppio di ogni elemento della lista, ma l'output non è quello atteso. Individua l'errore logico e correggilo.

    ```python
    def raddoppia(lista):
        return lista

    numeri = [1, 2, 3]
    numeri = raddoppia(numeri)
    print(numeri)
    ```

2.  Il seguente programma vuole ottenere la lista ordinata senza modificare quella originale, ma non funziona come previsto. Spiega cosa stampa e perché, poi proponi la correzione.

    ```python
    originale = [5, 2, 8, 1]
    ordinata = originale.sort()
    print("originale:", originale)
    print("ordinata:", ordinata)
    ```

## Programmazione

1. `[EX-SIM3-13]` Scrivi un programma che legge numeri interi dall'input uno per riga, finché l'utente non inserisce `0`. Al termine il programma stampa la lista dei soli numeri positivi inseriti (lo zero e i negativi non vengono inclusi).

    Esempio:

    ```
    Input:  4
            -2
            7
            0
            3
            0
    Output: [4, 7]
    ```

2. `[EX-SIM3-14]` Scrivi una funzione pura `minimo(lista)` che restituisce il valore minimo di una lista di interi senza usare `min()`. Poi scrivi un programma che legge una lista di numeri dall'utente (con sentinella `0`) e stampa il minimo.

    ```python
    print(minimo([5, 2, 8, 1]))   # 1
    print(minimo([3, 3, 3]))      # 3
    ```

3. `[EX-SIM3-15]` Scrivi una funzione pura `conta_pari(lista)` che restituisce quanti numeri pari sono presenti nella lista.

    ```python
    print(conta_pari([1, 2, 3, 4, 5, 6]))   # 3
    print(conta_pari([1, 3, 5]))             # 0
    ```

4. `[EX-SIM3-16]` Scrivi una funzione void `sostituisci_negativi(lista, valore)` che sostituisce ogni elemento negativo della lista con `valore`, modificando la lista originale.

    ```python
    dati = [3, -1, 7, -4, 0]
    sostituisci_negativi(dati, 99)
    print(dati)   # [3, 99, 7, 99, 0]
    ```

5. `[EX-SIM3-17]` Scrivi una funzione pura `moltiplica(a, b)` che calcola il prodotto `a * b` **senza usare l'operatore `*`**. Puoi assumere che `b` sia un intero non negativo.

    ```python
    print(moltiplica(3, 4))   # 12
    print(moltiplica(7, 0))   # 0
    print(moltiplica(5, 1))   # 5
    ```

6. `[EX-SIM3-18]` Scrivi una funzione pura `contiene_pari(lista)` che restituisce `True` se la lista contiene almeno un numero pari, `False` altrimenti. Poi scrivi un programma che legge una lista di interi dall'utente (con sentinella `0`) e stampa un messaggio diverso a seconda del risultato.

    ```python
    print(contiene_pari([1, 3, 5]))      # False
    print(contiene_pari([1, 2, 3]))      # True
    print(contiene_pari([]))             # False
    ```

    Esempio di programma completo:

    ```
    Input:  3
            7
            4
            0
    Output: La lista contiene almeno un numero pari.
    ```

    ```
    Input:  1
            3
            5
            0
    Output: La lista non contiene numeri pari.
    ```

7. `[EX-SIM3-19]` Scrivi una funzione pura `tutti_positivi(lista)` che restituisce `True` se tutti gli elementi della lista sono strettamente positivi (maggiori di zero), `False` altrimenti. Poi scrivi un programma che legge una lista di interi con sentinella `0` e stampa il risultato.

    ```python
    print(tutti_positivi([1, 2, 3]))     # True
    print(tutti_positivi([1, -1, 3]))    # False
    print(tutti_positivi([]))            # True
    ```

8. `[EX-SIM3-20]` Scrivi una funzione pura `e_ordinata(lista)` che restituisce `True` se gli elementi della lista sono in ordine non decrescente, `False` altrimenti. Poi scrivi un programma che legge una lista con sentinella `0` e stampa un messaggio.

    ```python
    print(e_ordinata([1, 2, 2, 5]))     # True
    print(e_ordinata([1, 3, 2, 5]))     # False
    print(e_ordinata([7]))              # True
    ```

    Esempio di programma completo:

    ```
    Input:  2
            4
            4
            8
            0
    Output: La lista è ordinata.
    ```

    ```
    Input:  2
            8
            4
            0
    Output: La lista non è ordinata.
    ```
