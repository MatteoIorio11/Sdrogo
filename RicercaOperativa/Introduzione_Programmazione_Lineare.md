# Introduzione alla Programmazione Lineare

## Algoritmi di Ottimizzazione
### Modelli
Per poter definire un algoritmo di ottimizzazione, è necessario definire il modello matematico, rappresentato come:

$$
\begin{align*}
& z_p = \text{min}\quad f(\textbf{x}) \\
& \qquad s.t. \\
& \qquad\qquad g_i(\textbf{x}) \leq b_i  & i=1..n \\
& \qquad\qquad g_j(\textbf{x}) = d_j    & j=1..m \\
& \qquad\qquad x \geq 0
\end{align*}
$$

dove:
- La funzione $f(\textbf{x})$ è la **funzione obiettivo**.
- La variabile $\textbf{x}$ è la **variaibile decisionale**.
- Le epsressioni $g_i(\textbf{x}) \leq b_i$ e $h_j(\textbf{x}) = d_j$ rappresentano i **vincoli**.
- L'espressione $\textbf{x} \geq 0$ è il **vincolo di non negatività**.

Inoltre:
- Se le funzioni $f(\textbf{x})$, $g_i(\textbf{x})$ e $h_j(\textbf{x})$ sono *lineari*, si parla di programmazione lineare **continua**.
- Se vi sia il vincolo aggiuntivo che la soluzione deve avere *tutte* le componenti interi, si parla di programmazione lineare **intera**.
- Se solo alcune componenti di $\textbf{x}$ devono essere intere, programmazione lineare **mista intera**.

### Lower e Upper Bound
Dato un problema di programmazione lineare di *minimo*, un valido **lower bound** è una stima per difetto del valore della soluzione ottima: $ z_{LB} \leq z_P $. Il suo calcolo è reso posssibile da **procedure di Bounding**.

È possibile invece individuare un **upper bound**, ovvero una soluzione ammissibile calcolata come stima per eccesso del valore della soluzione ottima: $ z_P \leq z_{UB} $. È calcolabile tramite **procedure euristici** (euristiche?).

Nel caso il problema di PL sia di *massimo*, i ruoli si invertono, ovvero le procedure di bounding forniscono l'upper bound, mentre i metodi euristici un lower bound.

---
Un **algoritmo esatto** invece, è un algoritmo che *garantisce* la determinazione della soluzione ottima di P (compatibilmente con le risorse di memoria e tempo di calcolo disponibili).

### Knapsack Problem
Obiettivo: determinare quale degli $n$ oggetti di peso $w_i$ e profitto $p_i$ devono essere inseriti nel knapsack di capacità $W$ per **massimizzare il profitto** complessivo.

Il modello matematico per il problema del knapsack (0-1) è il seguente:
$$
\begin{align*}
    (KP) & \qquad z_{KP} = \text{max} \sum_{i=1}^n{p_ix_i} \\
    & \qquad\qquad s.t. \\
    & \qquad\qquad\qquad \sum_{i-1}^n{w_ix_i} \leq W \\
    & \qquad\qquad\qquad x_i \in \{0,1\}, & i=1..n
\end{align*}
$$

#### KP: Upper Bound
Possiamo calcoalre un buon **Upper Bound** risolvendo il **rilassamento continuo** della formulazione matematica:
$$
\begin{align*}
    (LKP) & \qquad z_{LKP} = \text{max} \sum_{i=1}^n{p_ix_i} \\
    & \qquad\qquad s.t. \\
    & \qquad\qquad\qquad \sum_{i-1}^n{w_ix_i} \leq W \\
    & \qquad\qquad\qquad 0 \leq x_i \leq 1, & i=1..n
\end{align*}
$$
In questo caso all'interno delle condizioni di esistenza *diamo la possibilità di prendere frazioni di elementi* nel caso in cui non si potesse prendere l'elemento interamente.
È possiible così ricavare un valido upper bound mediante il seguente algoritmo:
```python
def upper_bound_KP(W, w, p, x):
    # Ordina tutti gli oggetti per ordine non crescente (decrescente) di r[i] = p[i]/w[i]
    # Inizializza W1 = W e x[i] = 0 for i..n
    for i in range(n):
        if W1 >= r[i].weight:
            x[i] = 1;
            W1 -= r[i].weight
        else:
            x[i] = W1/r[i].weight # Elemento Critico, prendo la 
            \ #parte frazionaria che riesco a mettere dentro
            return
```
È importante notare come in questo approccio se arrivassimo al punto in cui riempiamo completamente il knapsack senza solzuzioni frazionare (*Elemento Critico*), allora si arriverebbe direttamente alla soluzione ottima!

#### KP: Euristico
In caso invece sia stata generata una soluzione con un elemento frazionario, è possibile procedere con l'individuazione di un **lower bound** che possa generare una soluzione valida e ammissibile attraverso un algoritmo *greedy* derivato dall'upper bound:
```python
def greedy_KP(W, w, p, x):
    # Ordina tutti gli oggetti per ordine non crescente di r[i] = p[i]/w[i]
    # Inizializza W1 = W e x[i] = 0 for i..n
    for i in range(n):
        if W1 >= r[i].weight: #ci sta? posso usarlo?
        \ #Poiché vogliamo solo soluzioni intere
            x[i] = 1
            W1 -= r[i].weight
```
In questo codice si va rilevare il *lower bound* migliore, si può notare infatti che i nostri elementi vengono presi interamente oppure non vengono presi affatto. 

Questo algoritmo può essere migliorato se si considerano le diverse permutazioni all'ordinamento originario, dando luogo anche alla permutazione per cui si ottiene la soluzione ottima.

### KP: Algoritmi Esatti
La soluzione ottima può essere ricavata mediante due approcci:
- Metodi **Branch \& Bound**
- **Programmazione Dinamica**

#### KP: Branch \& Bound
È un algoritmo di **enumerazione** che utilizza procedure di bounding per ridurre le dimensioni dell'albero di ricerca. Ad **ogni nodo** dell'albero viene calcolato il bounding e possono verificarsi le seguenti condizioni
1. Il bound indica che **non può essere** ottenuta una soluzione migliore della migliore soluzione ammisibile &rarr; il nodo viene eliminato.
2. Il bound fornisce una **soluzione ammissibile** (intera) &rarr; si aggiorna la migliore soluzione ammissibile disponibile e il nodo viene elminato.
3. Non si verifica ne (1) ne (2) (e.g. viene calcolata una soluzione frazionaria) &rarr; **branching**: il problema viene ulteriormente decomposto in $k$ sottoproblemi.

Possiamo così definire i seguenti insiemi per ogni nodo dell'albero:
- $F_0 \subseteq \{1,...,n\}$: variabili fissate a 0, gli elementi che non vengono presi
- $F_1 \subseteq \{1,...,n\}$: variabili fissate a 1, gli elementi che vengono utilizzati
  - ovviamente vale $F_0 \cap F_1 = \empty$
- $L = \{1,...,n\}\setminus(F_0 \cup F_1)$: insieme delle variabili *libere*.

Ora è possibile calcoalre un upper bound ad ogni nodo mediante il seguente **rilassamento lineare** del knapsack:
$$
\begin{align*}
    & (LKP) \qquad z_{LKP}(L,F_0,F_1) = \text{max} \sum_{i \in L} p_i x_i + \sum_{i \in F_1}p_i \\
    & \qquad\qquad s.t. \\
    & \qquad\qquad\qquad \sum_{i \in L}w_i x_i \leq W - \sum_{i \in F_1} w_i \\
    & \qquad\qquad\qquad 0 \leq x_i \leq 1 \qquad i \in L
\end{align*}
$$

La nostra funzione obbiettivo è quindi la sommatoria di tutti gli elementi gia presi $p_i$ sommata alla sommatoria di tutti gli altri elementi che ancora devono essere aggiunti $p_ix_i$.
Nei vincoli invece troviamo $W-\sum_{i \in F_1} w_i$, che si traduce in: rimuovo dallo spazio disponibile $W$ i volumi degli elementi presi $w_i$.  

Un algoritmo Branch \& Bound per il knapsack (0-1) è il seguente:
```python
def BBKP(f0, f1, W, w, p, x, z):
    # L = {1..n} - (f0 | f1) dove | è l'unione dei set
    # Calcolare Z_LKP (L, f0, f1) e sia x1 la sua soluzione
    if Z_LKP(L, f0, f1) < z or Z_LKP(L, f0, f1) is None:
        # Elimina il nodo
        return;
    elif # la variabile dell'elemento critico j è intera:
        if Z_LKP(L, f0, f1) > z: # se la nuova soluzione è maggiore della migliore soluzione ammissibile
            z = Z_LKP(L, f0, f1)
            x = x1
        return;
    else: # la soluzione trovata (j) è frazionaria
        f0 = f0 | (j); BBKP(f0, f1, W, w, p, x, z); f0 = f0 - (j)
        f1 = f1 | (j); BBKP(f0, f1, W, w, p, x, z); f1 = f1 - (j)
```

Dove nello pseudocodice:
- `Z_LKP(L, f0, f1)` = $z_{LKP}$, ovvero l'[upper bound](#kp-upper-bound) calcolato nel nodo corrente dell'albero.
- L'`elif` sta ad indicare che nella soluzione trovata tramite il calcolo dell'upper bound fino a quel punto, l'ultimo elemento trovato $j$ nella soluzione prende il nome di elemento critico poiché può essere intero o frazionario.
  - In caso sia intero e maggiore della soluzione massima corrente, allora la soluzione trovata sostituisce la soluzione corrente.
  - In caso sia frazionario, allora si esplora il suo sottoalbero come indicato dalle chiamate ricorsive nelle ultime due righe.

Il costo computazione dell'algoritmo è pari a $O(2^n)$.

#### KP: Programmazione Dinamica
La DP risolve il problema componendo la soluzione a **stadi** partendo dalle soluzioni parziali dei sottoproblemi seguendo un approccio *bottom-up*.

Essa si applica a **problemi di ottimizzazione** che hanno le seguenti **caratterstiche**:
- Il problema può essere decomposto in **stadi**: ad ogni stadio è associata una **decisione**.
- Ad ogni stadio $k$ il problema può trovarsi in un **numero finito di stati** possibili: $\{s_1^k,...,s_{q_k}^k\}$.
- Può essere definita una **funzione di costo** $f_k(s_i^k)$ dello stato $s_i^k$ dello stadio $k$ che **dipende solo dagli stadi precedenti**.
- Da ogni stato $s_i^k$ dello stadio $k$ può essere calcolato ogni possiible stato dello stadio $k+1$.

Nel caso del knapsack, per risolvere il problema possiamo individuare:
- $n+1$ stadi (numero degli oggetti + 1).
- $W + 1$ stati, dove per ogni stato $w \in \{0,...,W\}$ si risolve il seguente sottoproblma:

$$
\begin{align*}
    & (KP_j(W)) \qquad z_j(w) = \text{max} \sum_{i=1}^j p_ix_i \\
    & \qquad\qquad s.t. \\
    & \qquad\qquad\qquad \sum_{i=1}^j{w_ix_i} \leq w \\
    & \qquad\qquad\qquad x_i \in \{0,1\}, \qquad i=1,...,j
\end{align*}
$$

In questo caso $w$ è lo spazio totale che possiamo ancora occupare all'interno dello zaino in uno specifico stadio. **Per ogni stadio ho tanti stati**. 

Risolvere per ogni stato $w$ dello stadio $j$ i problemi $KP_j(w)$ equivale ad utilizzare la seguente recurcsione:
1. Inizializza $KP_0(w)= 0$, $\forall w \in \{0,...,W\}$
2. Ad ogni stadio $j \in \{1,...,n\}$ e per ogni $w \in \{0,...,W\}$, calcola la recursione:
$$
z_j(w)=\begin{cases}
    z_{j-1}(w)                                  & \text{if} \quad w<w_j\\
    \text{max}\{z_{j-1}(w), z_{j-1}(w-w_j)\}    & \text{if} \quad w\geq w_j
\end{cases}
$$

Nel caso $w\geq w_j$, la funzione di massimo è da interpretare come segue:
- Se scegliessimo l'elemento dello stadio j-esimo ma la soluzione ottenuta è minore della soluzione al passo precedente, allora manteniamo la soluzione come sta.
- Se scegliamo l'elemento dello stadio j-esimo, aggiungiamo al suo profitto ($p_j$) il profitto ottenuto dal caso dello stadio precedente ($j-1$) dello *stato* relativo alla capacità dello zaino meno il peso dell'oggetto j-esimo ($w-w_j$).
  - In questo modo implicitamente vengono non considerate tutte le soluzioni precedenti che risultano peggiori della nuova scelta, riducendo drasticamente i tempi d'esecuzione.


L'algoritmo così implementato ha complessità $O(nW)$, la quale ci suggerisce come sia possibile preferire questo approccio ad un approccio [Branch \& Bound](#kp-branch--bound):
- La complessità della programmazione dinamica dipende fortemente dall'aumento della capacità dello zaino $W$.
- La complessità di B&B esplode all'aumento di $n$ esponenzialmente.