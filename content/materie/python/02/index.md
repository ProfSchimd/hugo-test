---
title: Primi passi con Python
---

## Hello World!
Python può essere utilizzato anche come *linguaggio di scripting*, questo implica che
il ``main`` è implicito nella prima riga del file che viene eseguito. Per vedere
questo basta scrivere un file ``hello.py`` inserendo la seguente riga
{{<highlight python>}}
print("Hello World!")
{{</highlight>}}
ed eseguire l'interprete python su tale file

    python hello.py

il risultato dovrebbe essere proprio la stampa della famigerata stringa ``Hello World!``

### Buona pratica: il ``main``
Anche se Python non prevede esplicitamente un ``main``, è sempre buona norma (per evitare
futuri mal di testa), organizzare il codice in modo che si rispecchi la classica esecuzione
con un ``main``. Per fare questo si può usare la variabile ``__name__`` (inizio e fine con
un doppio underscore ``_``) che contiene il *nome* dell'esecuzione (``__main__`` quando si
esegue l'interprete con il comando mostrato sopra, altro valore comune è ``__test__``).

{{<highlight python "linenos=table">}}
def main():
    print("Hello World!")

if __name__ == "__main__":
    main()
{{</highlight>}}

Da notare che
* il file viene ancora eseguito come uno script cioè partendo dalla prima riga,
* essendo la prima riga un ``def`` viene quindi definita una procedura dal nome
``main``
* successivamente viene eseguito l'``if`` della riga 4 che confronta il valore
della variabile ``__name__`` con la stringa (*literal*) ``__main__``,
* se questo confronto dà esito positivo, viene invocata la funzione ``main``.

#### Dove sono i miei ``args``?!
Abbiamo visto come un vero ``main`` in Python non esista, ma allora come si
possono recuperare i parametri della riga di comando? Ad esempio il comando

    python hello_args.py Mario Rossi 34

ha tre parametri: ``Mario``, ``Rossi`` e ``34``. Per accedere a questi
parametri, bisogna utilizzare la variabile ``argv`` (*arguments vector*)
presente nel **modulo**``sys`` della libreria standard di Python che,
tuttavia, importato con l'istruzione ``import``. Copiano in un file
con il nome ``hello_args.py`` il seguente codice

{{<highlight python "linenos=table">}}
import sys

def main():
    print(sys.argv)

if __name__ == "__main__":
    main()
{{</highlight>}}

ed eseguendo l'istruzione sopra, verrà prodotto in output qualcosa simile
alla seguente riga

    ['hello_args.py', 'Mario', 'Rossi', '34']

che indica una **lista** (lo riconosciamo dalle parantesi quadre ``[ ]``)
che contiene
1. nella prima posizione (indice ``0``) il nome del programma (script) eseguito,
2. nelle rimanenti posizioni gli argomenti passati alla linea di comando.

