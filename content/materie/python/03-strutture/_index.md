---
title: Liste, Tuple e Dizionari
summary: "Questa lezione presenta le principali strutture dati messe a disposizione nativamente dal linguaggio Python: list, tuple e dizionari."
type: "lecture"
number: 3
weight: 30
---

## Liste

Le liste sono la struttura dati più utilizzata in Python che, infatti, non
prevede una struttura simile agli *array* Java e C/C++. Normalmente, tutto
quello che si fa con gli array, in Python lo si fa con le liste che in aggiunta
offrono delle funzionalità avanzate rispetto agli array.

### Creare liste

### Indicizzazione di una lista

### List comprehension

## Tuple

## Dizionari

### Iterare su dizionari

## Conversioni utili

### Da stringa a lista
La funzione ``split`` delle stringhe permette di dividere le parti (*token*) di una stringa
mettendo ogni parte in una lista

{{<highlight python>}}
record = "Mario Rossi Roma"
lista = record.split() 
print(lista) # ["Mario", "Rossi", "Roma"]
{{</highlight>}}

L'esempio mostra la divisione in base agli spazi, ma è possibile usare qualsiasi stringa come
divisione
{{<highlight python>}}
record = "Mari,Rossi,Roma"
lista = record.split(",") 
print(lista) # ["Mario", "Rossi", "Roma"]
{{</highlight>}}
{{<highlight python>}}
record = "Mario - Rossi - Roma"
lista = record.split(" - ") 
print(lista) # ["Mario", "Rossi", "Roma"]
{{</highlight>}}

### Da lista a stringa
Sempre usando le funzioni messe a disposizione per le stringhe si può eseguire l'operazione inversa
di quanto visto sopra: unire gli elementi di una lista separandoli con una stringa arbitraria.
In questo caso si usa la funzione ``join``.
{{<highlight python>}}
lista = ["Andrea", "Fumagalli", "Milano"]
stringa = " ".join(lista)
print(stringa) # "Andrea Fumagalli Milano" 
{{</highlight>}}
{{<highlight python>}}
lista = ["Andrea", "Fumagalli", "Milano"]
stringa = ", ".join(lista)
print(stringa) # "Andrea, Fumagalli, Milano" 
{{</highlight>}}

{{<attention>}}
Per usare la funzione ``join``, è necessario che tutti gli elementi della lista data in input
siano stringhe. In caso è possibile usare la *list comprehension* per convertire tutti gli
elementi in stringa
{{<highlight python>}}
lista = ["Andrea", "Verdi", 45]
", ".join([str(item) for item in lista])
{{</highlight>}}
{{</attention>}}

## Link utili

* [Strutture dati Python (in inglese)][1]

[1]: https://docs.python.org/3/tutorial/datastructures.html