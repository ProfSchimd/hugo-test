---
title: Installazione Python
summary: "Alcuni tra i modi più semplici e diretti per installare Python sulla propria macchina di sviluppo."
type: "lecture"
number: 1
weight: 10
---

Ci sono diverse possibilità per installare Python nella propria macchina
(Windows, Mac OS o Linux). Qui mostriamo solo i modi più comuni e quelli
tra i più facili.


## Installer "standard"
Visitando il sito [Python.org][1] si può scaricare l'installer ufficiale di Python scegliendo il
sistema operativo di interesse. Una volta installato il pacchetto scaricato, è disponibile
l'interprete ``python`` che rappresenta il "punto di ingresso" verso il linguaggio. Infatti si
usa l'interprete sia per eseguire uno script

    python main.py

si per avviare la console dell'interprete

    $python
    Python 3.8.9 (default, Feb 18 2022, 07:45:33) 
    [Clang 13.1.6 (clang-1316.0.21.2)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> 

È importante sottolineare che l'interprete **non è un editor**, di conseguenza una volta installato
deve essere corredato da un editor di file testo.

## Thonny IDE
Un'ottima IDE (*Integrated Development Environment*) è [Thonny][2] che permette di iniziare a programmare
in Python in pochissimi passi. I principali vantaggi di Thonny sono:
* semplicità e immediatezza: si inizia subito in un ambiente familiare;
* *stand-alone*: [Thonny][2] installa tutto il necessario cioè sia interprete che IDE, inoltre è possibile
installare [Thonny][2] anche senza i privilegi di amministratore;
* *orientato alla didattica* [Thonny][2] contiene diverse caratteristiche pensate per la didattica

Qui sotto si vede uno screenshot dell'IDE [Thonny][2], come si può vedere sono presenti diversi elementi.
* Una parte riservata al codice (nell'esempio si vede un file ``main.py`` aperto).
* Una parte con la *shell* nella quale si possono dare istruzioni Python.
* Altre parti (*outline*, *heap*, ...) utili allo sviluppo e all'apprendimento del linguaggio.

{{<figure src="thonny-screenshot.png" width="800" title="Screenshot dell'IDE 'Thonny'">}}


## Gestore dei pacchetti
Uno dei punti di forza di Python è la disponibilità di un numero importante di librerie, tuttavia, la
necessità di *gestire* l'enorme quantità di librerie richiede una **packet manager** flessibile ed
efficace. 

### ``pip`` e ``venv``

I [Virtual Environments (``venv``)][3] rappresentano un ottimo modo per gestire in maniera intelligente
i pacchetti e i vari progetti.

* Creazione di un *virtual environment* chiamato ``primo-env``

        python3 -m venv primo-env

    questo crea una directory ``primo-env/`` all'interno della quale viene messo il minimo
    indispensabile per eseguire l'interprete ``python``.

* Prima di poter utilizzare il *virtual environment* appena creato, è necessario "attivarlo" con il comando

        source primo-env/bin/activate 

* Normalmente, l'*environment* contiene il **packet manager** ``pip``

        pip --version

    è sempre opportuno eseguire l'aggiornamento del packet manager ``pip`` prima di procedere all'installazione
    di eventuali pacchetti.

* Per installare un pacchetto con ``pip`` si usa il sotto-comando ``install``

        pip install numpy

{{<attention title="Python e Windows" >}}
In certe situazioni, alcuni comandi descritti (ad esempio i vari comandi ``pip``) potrebbero generare *errori* o
*warning* e potrebbero non andare a buon fine. In questo caso si può provare la "variante" ``python -m`` prima
del comando. Ad esempio 

        pip install numpy

diventa

        python -m pip install numpy
{{</attention>}}


### Conda e Anaconda
L'installazione dell'interprete

[1]: https://www.python.org/
[2]: https://thonny.org/
[3]: https://docs.python.org/3/tutorial/venv.html
