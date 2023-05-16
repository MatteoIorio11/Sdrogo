# Graph Theory

## Primal-Dual Algorithm
L'algoritmo *primale-duale* per la soluzione del problema del flusso di costo minimo è simile al *Successive Shortest Path Algorithm*, in quanto anch'esso mantien uno pseudo flusso che soddisfa le condizioni di non negatività dei costi ridotti e i vincoli di capacità mentre è mantenuta la conservazione del flusso.

L'algoritmo *primale-duale* prevede di trasformare il problema originale in modo tale da avere un solo noco con un eccesso di flusso e solo un nodo con un deficit di flusso, ovvero lo *starting node* e il *destination node*. Il nuovo grafo sarà: 
1. Aggiungiamo a **G** due nuovi nodi *s* e *t*;
2. Per ogni nodo $i \in N$ con $b_i \ge 0$, aggiungiamo un *arco sorgente (s, i)* con capacità $u_{si} = b_i$;
3. Per ogni nodo $i \in N$ con $b_i \le 0$ aggiungiamo un *arco destinazione (i, t)* con capacità $u_{it} = -b_i$;
4. Poniamo $b_s = \sum_{i \in N^+} b_i$, dove $N^+ = {i \in N : b_i \ge 0}, b_t = -b_s$ e $b_i = 0$ per ogni $i \in N$

### Grafo ammissibile
Siano dati i potenziali $\pi$. Il *grafo ammissibile* $G^{\alpha}(x)$ è un sottografo di $G(x)$ che contiene solo gli archi *(i, j)* di *G(x)* di costo ridotto nullo. La capacità residua $r_{ij}$ è la stessa del corrispondente arco in *G(x)*. In questo modo nello *shortest path* spedisco il flusso solamente dove il valore è zero, così posso spingere il flusso su questi archi.

#### Pseudo-Codice
**algorithm** primal-dual
**begin**
x=0, $\pi$=0:
$e_s=b_s$ e $e_t = b_t$
**while** $e_s \ge 0$ **do**
**begin**
    Calcola in *G(x)* le distanze minime *d* da *s* a tutti gli altri nodi rispetto ai costi ridotti $c_{ij}^\pi$
    Aggiorna $\pi = \pi - d$
    Definisci il *grafo ammissibile* $G^{\alpha}(x)$
    Calcola in $G^{\alpha}(x)$ il flusso massimo dal nodo *s* al nodo *t*
    Aggiorna $e_s$, $e_t$ e $G(x)$
**end**
**end**

### Complessità computazionale
Nel caso peggiore l'algoritmo primale duale esegue un numero di iterazioni pari a *O(min{nU, nC})*. Nel caso sia utilizzato l'*Highest-Label Preflow-Push* la complessità del calcolo del flusso massimo è pari a $O(n^2 \sqrt m$. Quindi nel caso sia impiegato *Dijkstra* con *Fibonacci Heap* e l'*Highest-Label Preflow-Push* $O((min{nU, nC})((m + nlogn) + (n^2 + \sqrt m)))$. 

## Out-of-Kilter Algorithm
*Out-of-Kilter* mantiene soddisfatti i vincoli di **conservazione del flusso** ad ogni nodo $i \in N$. L'algoritmo iterativamente modifica il flusso x e i potenziali $\pi$, in modo da *diminuire* la **non ammissibilità** della soluzione e convergere alla soluzione ottima. Se un arco $(i, j) \in A$ soddisfa le condizioni di ottimalità diremo che è *in kilter*, mentre se non le soddisfa diremo che è *out-of-kilter*. 

### Kilter Number
Il *Kilter Number* $k_{ij} \geq 0$ indica di quanto deve essere modificato il flusso $x_{ij}$. L'algoritmo *Out-Of-Kilter* ad ogni iterazione individua un arco $(i, j) \in A$ out-of-kilter e riduce di una quantità positiva il corrispondente *kilter number*.

### Complessità computazionale
*Out-Of-Kilter* esegue un numero di iterazioni pari a *O(mU)*. Nel caso sia utilizzato *Dijkstra* con *Fibonacci Heap* la complessità del calcolo dei cammini costo minimo è pasi a *(O(m+n logn))*. Nel caso sia impiegato *Dijkstra* con *Fibonacci Heap*, la complessità è *O(mU(m+nlogn))*.

## Algoritmi Polinomiali
### Capacity Scaling Algorithm
Il *Capacity Scaling Algorithm* è una variante del *Successive Shortest Path Algorithm* in cui ad ogni iterazione viene garantino che la capacità residua del *cammino aumentante* sia *"sufficientemente grande"*. Viene definito un parametro $\Delta$:
* si selezionano i nodi *s* e *t* tali che $e_s \geq \Delta$ e $e_t \leq -\Delta$;
* si sostituisce il grafo residuo *G(x)* con il suo sottografo $G(x,\Delta)$ contente solo quegli archi di capacità residua pari almeno a $\Delta$.
Quando non è più possibile determinare una coppia di vertici *s* e *t* tali che $e_s \geq \Delta$ e $e_t \leq -\Delta$ allora si diminuisce il parametro $\Delpta$. Se $\Delta=1$ allora il flusso *x* corrente è ottimo. **Complessità computazionale:** *O((m logU)(m+ n logn))*. 

### Minimum Mean Cycle Cancelling Algorithm
Il *Minimum Mean Cycle Cacnelling Algorithm* è un altro algoritmo che riesce a migliorare la complessità computazione dell'algoritmo precedentemente detto, $O(n^2 m^3 log(n))$. 

## Flusso Massimo: Definizione e Formulazione Matematica
* Sia dato un grafo direzionato *G=(N, A)*, in cui ogni arco $(i,j) \in A$ è associata una capacità $u_{ji} \ge 0$, non ci sono costi
* Si vuole determinare il **flusso massimo** che può essere inviato dal vertice *origine* $s \in N$ al vertice *destinazione* $t \in N$.
### Algoritmo di Ford-Fulkerson
* **Step1 [Inizializza]**: Poni $x_{ij} = 0$, per ogni $(i, j) \in A$, e $v = 0$. 
* **Step2 [Determina Cammino Aumentante]**: Dichiara il vertice *s* non espanso con etichetta $[+s, \infty]$
  1. Se tutti i nodi etichettati sono già espansi, allora il flusso *v* è massimo, quindi **STOP**
  2. Se esiste un vertice *i* etichettato ma non ancora espanso, provvedi a espanderlo:
   * Per ogni vertice $j \in R_i$ non etichettato per cui $x_{ij} \le u_{ij}$ assegna l'etichetta $[+i, \delta]$, dove $\delta = min{u_{ij} - x_{ij}, \delta_i}$
   * Per ogni vertice $j \in R_{i}^{-1}$ non etichettato per cui $x_{ij} \ge 0$ assegna l'etichettà $[-i, \delta_{j}]$, dove $\delta_{j} = min(x_{ij}, \delta_{i}$
  3. Se *t* non risulta etichettato torna al passo 1
* **Step3 [Aumenta il Flusso x]**: Sia *P* il *cammino aumentante* dal vertice *s* al vertice *t*, Per ogni $(i, j) \in P$:
  1. Se l'arco (i, j) è percorso nel suo verso originario (da *i* a *j*) $x_{ij} = x_{ij} + \delta_{t}$
  2. Se l'arco (i, j) è percorso nel verso contrario (da *j* a *i*) $x_{ij} = x_{ij} - \delta_{t}$
Aggiorna il glusso $v = v + \delta_{t}$. 
Quando l'Algoritmo di Ford-Fulkerson termina, l'insieme dei vertici etichettati *S* e quello dei vertici non etichettati $S^{-}$ costituiscono un *taglio*:
$v = \sum_{i \in S} \sum_{j \in S^{-}} u_{ij}$
**Teorema**
Sia *x* un *flusso ammissibile* in *G* da *s* a *t* e sia *G(x)* il corrispondente residuo, il flusso *x* è massimo *se e solo se* non esiste in *G(x)* un cammino da *s* a *t*.
* **Step1 [Inizializza]**: Poni $x_{ij} = 0$, per ogni $(i, j) \in A$ e $v = 0$. 
* **Step2 [Determina Cammino Aumentante]**: Trova un cammino da *s* a *t* in *G(x)*, se non esiste un cammino da *s* a *t*, allora il flusso *x* è massimo, quindi **STOP**.
* **Step3 [Aumenta il Flusso x]**: Sia *P* il cammino trovato da *s* a *t* trovato e poni $\delta = min{r_{ij}:(i,j) \in P}$, per ogni $(i, j) \in P$:
  1. Se *(i,j)* corrisponde all'arco $(i, j) \in A: x_{ij} = x_{ij} + \delta$
  2. Se *(i,j)* corrisponde all'arco $(i, j) \in A: x_{ij} = x_{ij} - \delta$
Aggiorna il flusso $v = v + \delta$. L'algoritmo *Ford-Fulkerson* ha complessità *O(nmU)*, con le relative migliorie si possono **ottenere prestazioni migliori**. 

### Taglio s-t
Si definisce un *Taglio s-t* una partizione dei vertici *N*, del grafo *G* in due sottoinsiemi $S$ e $S^{-} = N \ S$ tali che $s \in S$ e $t \in S^{-}$.
**Teorema**
Dato un *flusso ammissibile x* pari a *v*, per ogni *taglio s-t* $(S, S^{-})$ si ha come valore del limite superiore, il *minimo* dell'arco che connette la parte *S* alla parte $S^{-}$.