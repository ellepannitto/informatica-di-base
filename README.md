# Fondamenti di Programmazione Python

Università degli Studi di Salerno

## Contenuti

- [programma.md](programma.md) — sorgente Markdown del programma del corso
- [calendario.md](calendario.md) — calendario delle lezioni usato per distribuire automaticamente le date sui singoli argomenti
- [programma.html](programma.html) — programma interattivo generato (apri nel browser)
- [guida-lezioni](guida-lezioni) — materiali Markdown dei moduli, compilabili sia come pagina sia come slide

## Generazione

Per rigenerare [programma.html](programma.html) a partire da [programma.md](programma.md) e [calendario.md](calendario.md):

```bash
python3 scripts/genera_programma.py
```

Per generare la pagina HTML di una guida:

```bash
python3 scripts/genera_guida_html.py guida-lezioni/modulo-1.md
```

Per generare la versione slide standalone dello stesso file:

```bash
python3 scripts/genera_guida_html.py guida-lezioni/modulo-1.md --slides
```

Per generare entrambe le versioni di tutti i moduli:

```bash
python3 scripts/genera_guida_html.py --all --both
```

## Licenza

Questo materiale è distribuito con licenza [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).

Puoi condividere e adattare il materiale per scopi non commerciali, a condizione di citare l'autore e di distribuire le versioni derivate con la stessa licenza.

**Autore:** Ludovica Pannitto — Università degli Studi di Salerno

### Attribuzioni

- L'attività "Simulare Von Neumann" nel Modulo 1 è adattata da [cse4k12.org — How Computers Work](https://cse4k12.org/how_computers_work/index.html), usata con licenza CC BY-NC-SA.
