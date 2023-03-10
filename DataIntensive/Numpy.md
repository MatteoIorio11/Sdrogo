# Numpy

- [Numpy](#numpy)
  - [Richiami di algebra lineare](#richiami-di-algebra-lineare)
    - [Vettori](#vettori)
      - [Operazioni](#operazioni)
    - [Matrici](#matrici)
  - [Numpy](#numpy-1)
    - [Reference](#reference)
      - [`ndarray`](#ndarray)
      - [Creazione di `ndarray`](#creazione-di-ndarray)
      - [Valori Casuali](#valori-casuali)
      - [Accesso agli Elementi di un Array](#accesso-agli-elementi-di-un-array)
      - [Cambiamento di forma](#cambiamento-di-forma)
      - [Conversione da Array a Oggetti Python](#conversione-da-array-a-oggetti-python)
      - [Operazioni tra componenti di Array](#operazioni-tra-componenti-di-array)
      - [Array binari e Booleani](#array-binari-e-booleani)


## Richiami di algebra lineare
L'algebra lineare studia vettori, matrici, spazi vettoraili, sistemi di equazioni lineari e trasformazioni lineari.
### Vettori
Algebricamente, un **vettore** è una tupla di $n$ componenti reali $v = (v_1,...,v_n)$.
Geometricamente le sue componenti sono coordinate in un punto di uno spazio $n$ dimensionale.

#### Operazioni
- Somma: pari alla somma delle componenti sommate dei vettori
- Prodotto tra uno scalare: prodotto di ogni componente per lo scalare.
- **Norma 2** (detta anche Euclidea) è la lunghezza del vettore, ed equivale ad applicare il teroema di Pitagora alle compoennti, quindi:

$$\left\|a\right\| = \sqrt[2]{\sum_{i=1}^n a_i^2}$$
- **Norma 1**: calcoalta come $\frac{a}{\left\|a\right\|}$, si ottiene il vettore unitario (se si calcola la norma a 1 al vettore unitario si ottiene 1).

- **Prodotto Scalare** (**dot**): è possibile applicare il prodotto scalare tra due vettori solo se hanno la stessa dimensione $n$, ed è la somma dei prodotti delle rispettive coppie di componenti, ovvero:
$$a\cdot b = \sum_{i=1}^n{a_i\cdot b_i}$$
Geometricamente parlando, il prodotto scalare è la proiezione ortogonale del primo vettore ($a$) sul secondo ($b$).
Minore è l'angolo tra loro, maggiore sarà la lunghezza del prodotto scalare, e ciò mi fa capire quanto i due vettori sono simili.

### Matrici
Una matrice $m \times n$ è una tabella di numeri reali con $m$ righe e $n$ colonne.
Le operazioni sono le stesse dei vettori, a differenza di:
- *Somma/Sottrazione*: le matrici devono essere entrambe $m\times n$ (*element wise operation*)
- Il **prodotto** tra due matrici $A_{m\times p} \cdot B_{p \times n}$ è una matrice $m \times n$.
  - Ogni cella $A_{i,j}$ è data dal prodotto scalare tra il vettore riga $i$ di $A$ con il vettore colonna $j$ di $B$.

## Numpy
Permette di gestire array n-dimensionali e l'applicazione di concetti di algebra lineare. Moltissime operazioni usano la sintassi python standard, ma con la differenza che spesso sono 10+ volte più veloci. Funzionie e operatori agiscono su inter vettori.

### Reference
#### `ndarray`
Array n-dimensionale, tutti gli elementi al suo interno **hanno lo stesso tipo**. Per quanto i suoi valori siano mutabili, la dimensione è prefissata al momento della creazione. I tipi dei valori più comuni sono:
- numeri reali a 8 byte: `np.float64`
- numeri interi a 8 byte: `np.int64`
- booleani `np.bool` (?)

È possibile ottenere una copia del vettore ma di un tipo di dato differente mediante il metodo `astype(<nptype>)`, per esempio
```python
# x matrice di booleani
y = x.astype(np.int)
# y matrice di interi del tipo 1 = true, 0 false.
```

Anche le matrici possono essere rappresentate mediante numpy, specificando un vettore per ogni riga all'interno della dichiarazione, attraverso delle liste innestate:
```python
np.array([1, 2, 3, 4]) # vettore riga di 4 elementi
np.array([ [1, 2, 3, 4],
               [5, 6, 7, 8] ]) # matrice 2x4
```

Ogni ndarray ha una serie di attributi, di cui si ricordano:
- `ndim`: numero di dimensioni, chiamati anche assi.
- `shape`: tupla che indica la forma (nell'esempio sopra, vettore=`(4, )`, matrice=`(2, 4)`). Una tupla di interi che indica il numero di elemento lungo ciascuna dimensione.
- `size`: numero totale di valori all'interno dell'array.
- `dtype`: tipo di dato dei valori contenuti.
- `itemsize`: La dimensione in byte di ogni elemento.

#### Creazione di `ndarray`
È possibile creare e inizializzare un array in savriati modi, per esempio:
- `np.zeors((2,3))`: inizializza una matrice 2x3 con tutti zeri ( di tipo `np.float64` solitamente).
- `np.full((3, ), 7)`: inizializza un vettore di 3 valori tutti a 7.
- `np.empty((2, 3))`: crea una matrice 2x3 con valori non inizializzati.
- `arange(...)`: crea un vettore di numeri a intervalli regolari e può essere specificata una delle seguenti forme:
  - `np.arange(5)`: array da 0 a 5 *escluso*.
  - `np.arange(10, 20, 2.5)`: da 10 a 20 *escluso* con *passo* 2.5.
- `linspace`: è utilizzata come `arange` ma specifica la lunghezza desiderata come secondo parametro.
  - `geomspace`: come linspace, ma fa una progressione esponenziale.
  - `logspace`: come linespace, ma fa una progressione logaritmica.

#### Valori Casuali
Numpy espone un modulo (`np.random`) per lavorare con **valori casuali**, permettendo anche la manipolazione del seed tramite `np.random.seed(123)`.
Per ottenere un intero tra un'intervallo tra a (incluso) e b (escluso) si usa `np.random.randint(a, b, num_of_values)`. Esistono inoltre le varianti per controllare la **distribuzione di probabilità**, come `binomial`, `normal` o `geometric`, dove è possibile specificare parametri in input (e.g. per `normal`, deviazione standard e media).

#### Accesso agli Elementi di un Array
Il funzionamento è come per le liste, ma per array a più dimensioni va indicato un indice per ciascuna dimensione (e.g. `y[0, 2]`).
Gli `ndarray` contengono valori mutabili, perciò `y[0, 2] = 100`, provocherà il risultato aspettato, ovvero che l'elemento nella prima riga, terza colonna assumerà il valore di 100.

È possibile l'accesso degli elementi per intervalli (**slicing**) come segue:
```python
x = np.array([10, 20, 30, 40, 50])
blob = np.zeros((3,4,2,1,5,6))
y = [2:4] # y = array([30, 40])

x[:3]   # primi 3 elementi
x[-3:]  # ultimi 3 elementi
x[1::2] # dal secondo ogni 2 elementi
blob[...,2:2] # equivale a blob[:,:,:,:,:,2:2],
# metto tutti i valori delle precedenti dimensioni a ":"
```
È imporante notare come effettuando slicing di x, si ottiene una vista dell'array, che condivide con esso la stessa memoria.
È possibile stabilire se un array è nato da uno slice di un altro array è possibile usare il campo `base`, per esempio nell'esempio sopra `y.base is x`  restituisce `True`. Se si trattadi una copia invece, l'attributo `base` è `None`.

Nel caso in cui si volesse copiare un'intera matrice in una nuova variabile è necessario utilizzare il metodo built in di ogni ndarray `copy()` il quale permette di creare una copia esatta di tutto ndarray.

È possiible utilizzare slicing anche su matrici, dove è imporante ricodare che l'operatore `:` indica "tutti gli indici lungo quella dimensione".
```python
x[:2, 1:3]  # prime due righe e seconda e terza colonna
x[:, :2]    # tutte le righe, prime 2 colonne
x[-2:, ]    # ultime 2 righe prendendo tutte le colonne
y = x[-1]   # seleziona solo l'ultima riga ma tutte le colonne
            # y = array([7, 8, 9]), droppata la dimensione a 1
```

Per i vettori riga e colonna estratti da una matrice, è sufficiente specificare un singolo indice di una dimensione, e questa dimensione viene rimossa dall'array risultante.

Si possono specificare **liste di indici** per specificare gli indici degli elementi da prendere (e.g. `x[:, [0, 2]]` tutte le righe e prima colonna e terza). È imporante notare che al contrario dello slicing, questo metodo ritorna **sempre una copia** degli elementi.

E' inoltre possibile specificare **matrici di indici**
```python
a = (np.arange(12)**2).reshape(3,4)
# [[0, 1, 2, 3, 4]
#  [16, 25, 36, 49]
#  [64, 81, 100 ,121]]

idx_r = np.array([[0,0,0], [1,1,1]])
idx_c = np.array([[2,3,2], [0,0,0]])
a[idx_r, idx_c]
#[[4, 9, 4]
# [16, 16, 16]]

#Come è stato ottenuto il primo 4?
# a[idx_r=0, idx_c=2] = 4
#Il 9?
# a[idx_r=0, idx_c = 3] = 9
#Il 4
# a[idx_r=0, idx_c=2] = 4
```

#### Cambiamento di forma
È possibile specificare una nuova forma per l'array in una che preveda lo stesso numero complessivo di elementi tramite il metodo `reshape((a, b))` dove la tupla `(a,b)` rappresenta la nuova dimensione di vettore 1D ad una matrice 2D. 
Reshape può restituire una vista o una copia in base alla contiguità o meno nella memroia fisica.

Nella tupla passata a `reshape` è possibile specificare un `-1` in una sola delle dimensioni per fare in modo che essa venga dedotta dagli altri parametri della tupla. Per esempio
```python
x = np.array([  [1, 2, 3],
                [4, 5, 6] ])

x.reshape((-1, 2)) ----> array([[1, 2],
                                [3, 4],
                                [5, 6]])
```

Tramite il metodo `ravel()` è possibile riformare qualsiasi array in vettore 1D, in pratica `x.ravel() == x.reshape((-1, ))`.
Per forzare la creazioen di una copia si può usare `x.flatten()`.

#### Conversione da Array a Oggetti Python
Gli `ndarray` possono essere trattati come collezioni python (iterabili, indicizzabili, castabili, ...). 
- Iterando un vettore si ottengono i suoi elementi
- Iterando una matrice si ottengono le sue righe
- Iterando una matrice con il metodo `x.flat`, si ottengono i singoli valori di essa


È possibile concatenare tra loro più `ndarray` tramite `np.concatenate(a, b)` nel caso di array 1D, mentre nel caso di matrici è possibile specfificare se la concatenazione deve essere effettuata dopo l'ultima colonna (`np.concatenate(X, Y, axis=1)`), oppure il default dopo l'ultima riga della matrice (`axis=0` default).

#### Operazioni tra componenti di Array
- Valgono tutte le operazioni aritmetiche tra numeri
- Le operazioni di **array di pari forma** son sempre eseguite *element wise*
- Le operazioni base si possono applicare anche tra un `ndarray` e un numero scalare.
  - Il risultato è un array della stessa forma col risultato dell'operazione applicato a ciascun elemento (vedi Broadcasting prossima lezione).

(quando facciamo il broadcasting metterlo qui)

#### Array binari e Booleani
Possono essere rappresentati in NumPy da array di tipo bool. Se si effettua una conversione ad intero, gli 1 sono rappresentati come True e 0 False.

È possibile selezioanre elementi di un array mediante array ed espressioni booleane mediante l'uso degli operatori bit a bit
- `&` and
- `|` or
- `^` xor
- `~` not

È possibile comporre tra loro più array booleani per applicare filtri e condizioni all'indicizzazione di elementi.

Di seguito alcuni esempi illustativi si spera:
```python
x =        np.array([   -1,     2,    3,     4])
flags =    np.array([ True, False, True, False])
x[flags] # array([-1, 3])

x[x > 0] # estraggo da x i valori positivi

~flags  # array([False, True, False, True])

# IMPORTANTISSIME LE PARENTESI TONDE QUANDO 
# SI FANNO LE COSE BIT A BIT!!!!!!!!!!!!!!!

x[(x >= 10) & (x <= 20)] # elementi tra 10 e 20
```