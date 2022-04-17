---
title: Primi passi con Python
summary: "Primissimi programmi/script Python: dal classico Hello World!, all'utilizzo delle liste Python e della list comprehension."
weight: 20
repo: "https://github.com/ProfSchimd/python/tree/main/01_python_primi_passi"
quiz_page: "quiz"
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

## Variabili
Una differenza di Python con linguaggi come Java e C++ è che le variabili
vengono dichiarate senza tipo

{{<highlight python>}}
a = 10 # intero
b = 3.14 # float
c = 'hello' # stringa
{{</highlight>}}
Questo, tuttavia, non vuol dire che Python non sia un linguaggio tipizzato.
Ad esempio, le seguenti istruzioni (successivamente a quelle sopra), falliscono
generando l'errore riportato sotto.
{{<highlight python>}}
d = a - 1 # Ok
e = c + a # Errore
{{</highlight>}}

    Traceback (most recent call last):
    File "vars.py", line 5, in <module>
        e = c + a
    TypeError: can only concatenate str (not "int") to str

Giustamente, Python si lamenta che (secondo lui) non ha senso
*concatenare* (operatore ``+`` su stringhe) una stringa e un intero.
Il modo giusto per ottenere l'effetto di creare la string ``hello10``
è convertire prima l'intero ``a`` in stringa, questo è possibile
utilizzando la funzione *built-in* ``str``
{{<highlight python>}}
e = c + str(a) # Ok
print(e)
{{</highlight>}}

Oltre a ``str`` sono disponibili altre funzioni per le conversioni "basilari":
* ``int(x)`` converte l'argomento ``x`` in intero,
* ``float(x)`` converte l'argomento ``x`` in numero decimale (*floating point*).

{{<exercise>}}
Scrivere un programma che calcola la media di 3 numero forniti dalla riga di comando
(per accedere agli elementi di una lista, si usa la notazione indice ``v[i]`` con indice
che prende i valori ``0,1,2,...``).
{{</exercise>}}

### Operatori
Python possiede tutti gli operatori aritmetici e logici che sono presenti nei linguaggi
di programmazione. Qui presentiamo solo i più importanti di questi operatori, una lista
più esauriente si può trovare a [questa pagina](https://www.w3schools.com/python/python_operators.asp).

{{<table>}}
| Operatore | Nome             | Esempio       |
|-----------|------------------|---------------|
|  ``+ ``   | Addizione        | 1 + 3 = 5     |
|  ``-``    | Sottrazione      | 3.5 - 2 = 1.5 |
|  ``*``    | Moltiplicazione  | 4 * 4 = 16    |
|  ``/``    | Divisione	       | 5 / 10 = 0.5  |	
|  ``%``    | Resto	           | 4 % 3 = 1	   |
|  ``**``   | Potenza	       | 2 ** 3 = 8	   |
|  ``//``   | Divisione intera | 5 // 2 = 1    |
{{</table>}}

{{<exercise>}}
Scrivere un programma che faccia la *divisione euclidea* di un intero ``n`` per un
intero ``m`` fornendo un intero ``q`` (*quoziente*) e un intero ``r`` (*resto*) tali
che
\\[ n = mq + r \\]
i valori di input ``n`` ed ``m`` vanno presi dalla riga di comando.
{{</exercise>}}

## Funzioni

## Liste

Le liste sono la struttura dati più utilizzata in Python che, infatti, non
prevede una struttura simile agli *array* Java e C/C++. Normalmente, tutto
quello che si fa con gli array, in Python lo si fa con le liste che in aggiunta
offrono delle funzionalità avanzate rispetto agli array. Un'intera lezione
sarà dedicata alle liste, ma è bene conoscerne le basi al più presto per poter
sfruttare al meglio le potenzialità del linguaggio Python.

### Creare liste

### Indicizzazione di una lista

### List comprehension
