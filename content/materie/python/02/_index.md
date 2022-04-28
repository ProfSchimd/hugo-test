---
title: Primi passi con Python
summary: "Primissimi programmi/script Python: dal classico Hello World!, all'utilizzo delle liste Python e della list comprehension."
type: "lecture"
number: 2
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

{{<observe>}}
Come tutti i linguaggi di programmazione, anche Python ha i **commenti**. Un commento
inizia con il carattere *sharp* ``#`` (cancelletto) e termina con la fine della riga.
Non è prevista una sintassi apposita per i *blocchi di commento*, bisogna quindi
utilizzare un ``#`` ad ogni inizio di riga di commento.
{{</observe>}}

## Variabili
Una differenza di Python con linguaggi come Java e C++ è che le variabili
vengono dichiarate senza tipo

{{<highlight python>}}
a = 10 # intero
b = 3.14 # float
c = "hello" # stringa
cc = 'world!' # stringa
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
i valori di input ``n`` ed ``m`` vanno presi dalla riga di comando mentre i valori
di output ``q`` ed ``r`` vanno stampati sulla console.
{{</exercise>}}

## Funzioni
È sempre buona norma dividere il codice in *blocchi* ognuno dei quali si occupa di risolvere un
problema ben specifico. Il modo più semplice di dividere in blocchi è utilizzando le **funzioni**
o *subroutine* (un altro modo è utilizzando la programmazione ad oggetti che tratteremo in una
lezione futura).

In Python una funzione si dichiara utilizzando la parola chiave ``def``, seguita dalla **firma**
della funzione:
* nome della funzione e
* lista dei parametri.

{{<highlight python>}}
def nomeFunzione(parametro1, parametro2, ...):
    istruzione1
    istruzione2
    # ...
    return valoreDaRestituire
{{</highlight>}}

In Python il tipo ritornato da una funzione ed il tipo dei parametri non sono
obbligatori (nelle prime versioni di Python non erano previste, ma più di recente è stata
introdotta la possibilità di indicare i tipo). Ad esempio la funzione ``somma`` del codice
sotto, avrà risultati diverso in base ai parametri forniti

{{<highlight python "linenos=table">}}
def somma(a, b):
    return a + b

def main():
    print(somma(1,2))
    print(somma("1", "2"))

if __name__ == "__main__":
    main()
{{</highlight>}}

### Valori di ritorno
Per ritornare un valore da una funzione in Python si usa l'istruzione ``return``. Nell'esempio
visto sopra, la funziona ``somma`` restituisce il risultato dell'operazione ``a + b``. L'istruzione
``return`` fa anche terminare l'esecuzione della funzione ovunque questa si trovi

Le funzioni Python ritornano sempre un valore, quando questo non è esplicitato dal
programmatore, questo valore è ``None``.

{{<highlight python "linenos=table">}}
def noneReturn():
    pass

a = noneReturn()
print(a)
{{</highlight>}}

In questo esempio si vede anche come creare un blocco che non ha alcuna istruzione (in questo caso
si tratta di un blocco funzione, ma lo stesso si può fare con blocchi cicli e classi).

#### Ritornare più valori
Altra caratteristica interessante di Python, è la possibilità che una funziona restituisca più di un
valore
{{<highlight python "linenos=table">}}
def minmax(a, b):
    return min(a,b), max(a,b)

def main():
    print(minmax(3,1))
    
if __name__ == "__main__":
    main()
{{</highlight>}}

Nell'esempio sopra, la funzione ``minmax`` restituisce due valori: il minimo ed il massimo dei due
parametri passati in ingresso.

{{<observe>}}
Nell'esempio di codice ``minmax`` si può vedere l'utilizzo di due altre funzioni standard di Python:
``min`` restituisce il minimo tra **2 o più valori** e ``max`` restituisce il massimo tra **2 o più
valori**.  
{{</observe>}}

{{<exercise>}}
Ri-scrivere il codice per la *divisione euclidea* (vedi sopra) utilizzando una funzione che
prende in input ``n`` ed ``m`` e che restituisce i valori ``q`` e ``r``.
{{</exercise>}}

{{<exercise title="Equazione di secondo grado">}}
Scrivere una funzione Python ``secondoGrado`` che calcola le soluzioni dell'equazione

$$ ax^2 + bx + c = 0 $$

quando \\(a\\), \\(b\\) e \\(c\\) sono input della funzione e le due soluzioni \\(x_1\\) e \\(x_2\\)
sono output. Per calcolare \\(\sqrt{x}\\) si può usare la funzione ``sqrt(x)`` attraverso il pacchetto
``math`` che va importato
{{<highlight python>}}
import math
...
def secondoGrado(a, b, c):
    ...
    # mette in 'r' la radice quadrata di 'discriminante'
    r = math.sqrt(discriminate) 
    ...
{{</highlight>}}
{{</exercise>}}

In Python è possibile catturare valori di ritorno multipli sia utilizzando le *tuple*, sia utilizzando
le variabili. Ad esempio per mettere minimo e massimo in due variabile usando la nostra funzione ``minmax``
possiamo usare il seguente codice
{{<highlight python "linenos=table">}}
minimo, massimo = minmax(3, 1)
print(minimo) # stampa 1
print(massimo) # stampa 3
{{</highlight>}}

{{<attention>}}
Quando si usano funzioni con più valori ritornati bisogna fare attenzione a cosa viene *catturato*.
{{<highlight python>}}
v = minmax(2, -1)
print(v) # stampa (-1, 2) -> tupla
v, w = minmax(2, -1)
print(v) # stampa -1 -> intero
{{</highlight>}}
A sinistra dell'uguale ci può essere 

* una sola variabile questa variabile sarà una tupla se la funzione restituisce più di un valore
* un numero variabili **uguale** al numero di variabili restituite dalla funzione

In tutti gli altri casi l'interprete Python darà un messaggio d'errore simile al seguente

    Traceback (most recent call last):
    File "<pyshell>", line 1, in <module>
    ValueError: too many values to unpack (expected 2)

{{</attention>}}

## Input
Chiedere l'input da tastiera in Python è molto semplice, basta usare la funzione ``input`` la quale
si metterà in attesa di un input dalla tastiera
{{<highlight python "linenos=table">}}
nome = input()
  Mario
print(nome) # stampa 'Mario'
{{</highlight>}}
È possibile indicare una stringa come parametri di ``input`` per aiutare a comprendere l'input richiesto
{{<highlight python "linenos=table">}}
nome = input("Nome: ")
  Nome: Fabio
print(nome) # stampa 'Fabio'
{{</highlight>}}

{{<exercise>}}
Scrivere una funzione Python senza parametri che richieda di inserire in input nome e cognome
e che restituisca le due stringhe (prima cognome e poi nome).
{{</exercise>}}

