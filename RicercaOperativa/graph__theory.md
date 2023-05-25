# Graph Theory

## Introduzione Matematica
Consideriamo un grafo *direzionato* $G = (N, A)$, in cui:
- Per ogni **arco** $(i,j) \in A$  è associato un costo $c_{ij}$ e una capacità $u_{ij}$.
- Per ogni **vertice** $i \in N$ è associata una *disponibilità* $b_i \geq 0$ oppure una *richiesta* $b_i < 0$, oppure $b_i = 0$ (ciò che entra è uguale a ciò che esce).

Il problema del **flusso a costo minimo** può essere formulato come segue:
$$
\begin{align*}
    \min z(P) &= \sum_{(i,j) \in A} c_{ij} x_{ij} \\
    &s.t. \sum_{j\in\Gamma_i} x_{ij} - \sum_{j\in \Gamma^{-1}_i} x_{ji} = b_i, \quad i \in N& \\
    &\qquad0 \leq x_{ij} \leq u_{ij},  \quad\quad\qquad (i,j) \in A&
\end{align*}
$$

dove:
- La variabile decisionale $x_{ij}$ determina quante unità di flusso passano attraverso l'arco $(i,j)$
- $\Gamma_i$ sono gli archi *uscenti* da un vertice $i$, mentre $\Gamma^{-1}_i$ sono gli archi *entranti* in $i$.
- Il primo vincolo ci assicura la **conservazione** del flusso.
- Se le capacità e le richieste/eccessi sono *interi*, allora la soluzione del flusso a costo mininimo sarà intera.

### Problema Duale
Associamo le seguenti variabili duali:
1. Per il primo vincolo (vincolo di conservazione del flusso), al nodo $i \in N$ associamo $\pi_i$.
2. Al vincolo di capacità relativo all'arco $(i,j) \in A$ associamo $\alpha_{ij}$.

In questo modo, definiamo il duale del problema $P$:
$$
\begin{align*}
    \max z(D) &= \sum_{i \in N} b_i\pi_i - \sum_{(i,j) \in A} u_{ij} \alpha_{ij}\\
    &s.t. \quad\pi_i - \pi_j - \alpha_{ij} \leq c_{ij},  &(i,j)\in A\\
    &\quad\quad\pi_i \quad \text{qualsiasi}, &i \in N \\
    &\quad\quad\alpha_{i,j}\geq 0, &i \in N
\end{align*}
$$

### Assunzioni
- Tutti i dati sono valori interi.
- Il grafo è **direzionato**.
- Le richieste e le disponibilità dei diversi nodi soddisfano la condizione $\sum_{i\in N} b_i = 0$ (non ci sono perdite di flusso).
- Il problema di flusso a costo minimo **ha una soluzione ammissibile**.
- Il grafo contiene un cammino diretto di capacità infinita per ogni coppia di nodi (utile per garantire di ottenere una soluzione ammissibile durante l'esecuzione degli algoritmi).
- Tutti i **costi** sono **non negativi**, e le **capacità** sono **positive**.


### Definizioni
Useremo le seguenti notazioni per i **parametri** all'interno di questo documento:
- $n = |N|$ è il numero di **nodi** del grafo $G$.
- $m = |A|$ è il numero di **archi** del grafo $G$.
- $U = \max\{u_{ij}: (i,j) \in A\}$, *capacità massima*.
- $C = \max\{c_{ij}: (i,j) \in A\}$, *costo massimo*.

#### Grafo residuo
Il grafo residuo $G(x)$ corrispondente al flusso $x$ è ottenuto sostituendo ogni arco $(i,j)\in A$ con due archi:
- $(i,j)$ con **costo** pari a $c_{ij} = c_{ij}$ e **capacità residua** $r_{ij} = u_{ij} - x_{ij}$
- $(j,i)$ con **costo** pari a $c_{ji} = -c_{ij}$ e **capacità residua** $r_{ji} = x_{ij}$

#### Potenziale
Denotiamo con $\pi_i \in \mathbb{R}$ il **potenziale** associato ad ogni *nodo* $i \in N$.
Il suo corrispondente **costo ridotto** $c_{ij}^\pi$ verrà calcolato come:
$$c_{ij}^\pi = c_{ij} - \pi_i + \pi_j$$
Il quale corrisponde tra l'altro anche alla variabile duale associata al vincolo di conservazione del flusso relativo al nodo $i \in N$.
##### Proprietà dei Potenziali
Per ogni **cammino diretto** $P$ dal nodo $k$ al nodo $l$ si ha:
$$
\sum_{(i,j)\in P} c_{ij}^\pi = \sum_{(i,j) \in P} c_{ij} - \pi_k + pi_l
$$
Ovvero che costo del flusso all'interno del cammino $P$ è pari al costo di tutti i nodi intermedi e i costi ridotti di sorgente e destinazione.

Inoltre, per ogni **ciclo diretto** $W$ si ha:
$$
\sum_{(i,j) \in W} c_{ij}^\pi = \sum_{(i,j) \in W} c_{ij}
$$
E questo invece non so che cazzo signifihi, l'unica cosa che so è che all'interno di un ciclo, posso capire il suo costo sia usando i costi normali, che i costi ridotti.

### Condizioni di Ottimalità
Consideriamo una soluzione ammisibile $x^*$ del problema del *flusso di costo minimo*.
- **Assenza di Cicli di Costo Negativo**: la soluzione $x^*$ è ottima se e solo se il **grafo residuo** $G(x)$ *non* contiene cicli di costo negativo.
- **Costi Ridotti Positivi**: La soluzione $x^*$ è ottima se e solo se è possibile trovare dei potenziali $\pi$ tali che per ogni arco $(i,j)$ di $G(x^*)$ soddisfano la condizione: $c_{ij}^\pi = c_{ij} - \pi_i + \pi_j \geq 0$.
- **Relazione degli Scarti Complementari**: La soluzione $x^*$ è ottima se e solo se è possibile trovare dei potenziali $\pi$ tali che per ogni arco $(i,j) \in A$ il *costo ridotto* $c_{ij}^\pi$ soddisfa le seguenti condizioni degli scarti complementari:
$$
\begin{align*}
    \text{If} \quad &c_{ij}^\pi > 0, &\text{then} \quad &x_{ij}^* = 0 \\
    \text{If} \quad &c_{ij}^\pi = 0, &\text{then} \quad &0 \leq x_{ij}^* \leq u_{ij}\\
    \text{If} \quad &c_{ij}^\pi < 0, &\text{then} \quad &x_{ij}^* = u_{ij} 
\end{align*}
$$
Dove il loro significato in ordine:
1. Sarebbero le variabili non in base con valore 0, non le prendo.
2. Variabili inbase, devono rispettare i vincoli (nel nostro caso la soglia minima è zero).
3. Le variabili posso essere non in base e diverse da 0, in particolare il loro valore è pari all'upperbound (variante del simplesso con upperbound).

---
# Algoritmi
## Cycle Cancelling Algorithm
Permette di cancellare cicli di costo negativo all'interno del grafo, e si basa sulla seguente osservazione: Se nel grafo $G(x)$ identifico un ciclo $W$ di **costo negativo**, allora posso *aumentare* il flusso in $W$ diminuendo il costo complessivo della soluzione.

### Pseudocodice
$$
\begin{align*}
    & \textbf{algorithm } \text{cycle cancelling} \\
    & \textbf{begin} \\
    & \quad\text{Stabilisci un flusso ammissibile }x\text{ nel grafo }G& ;\\
    & \quad\textbf{while }G(x)\text{ contiene un ciclo di costo negativo }\textbf{do}& \\
    & \quad\textbf{begin} \\
    & \quad\quad\text{Applica un algoritmo per identificare un ciclo di costo negativo }W \\
    & \quad\quad\text{Calcola } \delta = \min\{r_{ij}: (i,j)\in W\}; \\
    & \quad\quad\text{Aumenta di }\delta \text{ unità il flusso nel ciclo } W\\
    & \quad\quad\text{Aggiorna }G(x); \\
    & \quad\textbf{end} \\
    & \textbf{end} \\
\end{align*}
$$

### Osservazioni
- Se esiste un ciclo di costo negativo all'interno del grafo mediante la soluzioen $x$, allora la soluzione **non** è ottima.
- L'algoritmo mantiene ad ogni passo **l'ammissibilità della solzione** e cerca di ottenere un soddisfacimento delle condizioni di ottimalità.
- **Calcolo di un Flusso ammissibile**: può essere calcolato risolvendo un problema di *flusso massimo* di un grafo $G'$ costruito come segue:
  - Aggiungiamo due nodi $s$ e $t$.
  - Per ogni nodo $i \in N$ con $b_i > 0$ aggiungiamo un arco $(s,i)$ con **capacità** $u_{si} = b_i$.
  - Per ogni nodo $i \in N$ con $b_i < 0$ aggiungiamo un arco $(i,t)$ con **capacità** $u_{si} = -b_i$.
  - A questo punto, se il flusso massimo da $s$ a $t$ calcolato, **satura tutti gli archi sorgente e destinazione**, allora il flusso trovato è ammissbile per $G$.
- **Identificazione di un Ciclo di Costo Negativo**: si può usare un algoritmo di tipo "label-correcting" per il calcolo del cammino di costo minimo (**Bellman-Ford**).

### Complessità Computazionale
1. Vengono eseguite nel caso peggiore $O(mCU)$ iterazioni.
2. Per ogni iterazione l'algoritmo risolve il problema del cammino di costo minimo per identificare il ciclo di costo negativo. Con Bellman-Ford, la complessità è pari a $O(nm)$.
3. In totale, Cycle Cancelling Algorithm ha complessita computazionale pari a $O(nm^2CU)$.

## Successive Shortest Path
- Ad ogni passo **mantiene** soddisfatte le **condizioni** di non negatività dei **costi ridotti** e i **vincoli di capacità**.
- Rilassa (cerca di soddisfare ma ammette violazioni) i vincoli di conservazione di flusso
$$
\sum_{j\in \Gamma_i}x_{ij} - \sum_{\Gamma_i^{-1}}x_{ji} = b_ij
$$
Il flusso sarà ammissibile **solo al termine** dell'algoritmo. Nelle fasi intermedie il flusso $x$ viene anche chiamato *pseudoflusso*.
- Per ogni nodo $i$ definiamo:
$$
e_i = b_i - \sum_{j\in\Gamma_i}x_{ij} + \sum_{\Gamma_i^{-1}}x_{ji}
$$

Il primo lemma mi sembra un po' inutile. Il secondo invece dice:
> Sia $x$ uno *pseudoflusso* che soddisfa le condizioni di non negatività dei costi ridotti per un qualche potenziale $\pi$.
> Se $x'$ è il pseudoflusso ottenuto da $x$ aumentando il flusso lungo il cammino di costo minimo da $s$ ad un altro nodo $k$, allora anche $x'$ soddisfa le condizioni di non negatività dei costi ridotti per un qualche $\pi'$, e.g. $\pi' = \pi - d$.

Qualsiasi cosa voglia dire, io so che la seguente strategia viene applicata:

Ad ogni iterazione, l'algoritmo deve selezionare un nodo $s$ con un *eccesso* di flusso ($e_s > 0$), e un nodo $t$ con un *deficit* di flusso ($e_t < 0$), e aumentare il flusso lungo il cammino di costo minimo da $s$ a $t$ nel grafo residuo $G(x)$.

È figo perché si può usare Dijkstra perché nel calcolo del cammino a costo minimo si utilizzano i costi ridotti $c_{ij}^\pi$ che sono positivi.

### Pseudocodice
$$
\begin{align*}
    & \textbf{algorithm } \text{successive shortest path} \\
    & \textbf{begin} \\
    & \quad x=0, \pi=0 \text{ e }e_i=b_i \text{ per ogni }i \in N& ;\\
    & \quad E = \{i\in N: e_i > 0\} \text{ e }D=\{i\in N: e_i < 0\}; \\
    & \quad\textbf{while }E \neq \empty \textbf{ do} \\
    & \quad\textbf{begin} \\
    & \quad\quad\text{Seleziona un nodo }k \in E \text{ e un nodo }l\in D\\
    & \quad\quad\text{Calcola in }G(x) \text{ le distanze minime }d \text{ da } k \\
    & \quad\quad\quad\text{ a tutti gli altri nodi rispetto ai costi ridotti }c_{ij}^\pi ;\\
    & \quad\quad\text{Sia }P\text{ il cammino di costo minimo da } k \text{ a }l;\\
    & \quad\quad\text{Aggiorna }\pi = \pi - d; \\
    & \quad\quad\text{Calcola }\delta = \min\{e_k, -e_l, \min\{r_{ij}: (i,j) \in P\}\};\\
    & \quad\quad\text{Aumenta di }\delta \text{ untià il flusso nel cammino }P;\\
    & \quad\quad\text{Aggiorna }G(x);\\
    & \quad\textbf{end} \\
    & \textbf{end} \\
\end{align*}
$$

Dove ricordiamo a i gentili telespettattori che $d$ sono le etichette prodotte applicando Dijkstra.

### Complessità Computazionale
1. Nel caso peggiore, $O(nU)$ iterazioni.
2. Per ogni iterazione, si risolve un costo minimo con costi positivi: usando Dijkstra e Heap di Fibonacci, la complessità è pari a $O(m+n\log n)$.
3. In totale, Successive Shortest Path ha una complessita computazionale pari a $O(nU(m+n\log n))$.

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
Quando non è più possibile determinare una coppia di vertici *s* e *t* tali che $e_s \geq \Delta$ e $e_t \leq -\Delta$ allora si diminuisce il parametro $\Delta$. Se $\Delta=1$ allora il flusso *x* corrente è ottimo. **Complessità computazionale:** *O((m logU)(m+ n logn))*. 

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
   * Per ogni vertice $j \in R_i$ non etichettato per cui $x_{ij} \le u_{ij}$ assegna l'etichetta $[+i, \delta]$, dove $\delta = \min\{u_{ij} - x_{ij}, \delta_i\}$
   * Per ogni vertice $j \in R_{i}^{-1}$ non etichettato per cui $x_{ij} \ge 0$ assegna l'etichettà $[-i, \delta_{j}]$, dove $\delta_{j} = \min\{x_{ij}, \delta_{i}\}$
  3. Se *t* non risulta etichettato torna al passo 1
* **Step3 [Aumenta il Flusso x]**: Sia *P* il *cammino aumentante* dal vertice *s* al vertice *t*, Per ogni $(i, j) \in P$:
  1. Se l'arco (i, j) è percorso nel suo verso originario (da *i* a *j*) $x_{ij} = x_{ij} + \delta_{t}$
  2. Se l'arco (i, j) è percorso nel verso contrario (da *j* a *i*) $x_{ij} = x_{ij} - \delta_{t}$
Aggiorna il flusso $v = v + \delta_{t}$. 
Quando l'Algoritmo di Ford-Fulkerson termina, l'insieme dei vertici etichettati *S* e quello dei vertici non etichettati $\bar{S}$ costituiscono un *taglio*:
$v = \sum_{i \in S} \sum_{j \in \bar{S}} u_{ij}$

**Teorema**
Sia *x* un *flusso ammissibile* in *G* da *s* a *t* e sia *G(x)* il corrispondente residuo, il flusso *x* è massimo *se e solo se* non esiste in *G(x)* un cammino da *s* a *t*.
* **Step1 [Inizializza]**: Poni $x_{ij} = 0$, per ogni $(i, j) \in A$ e $v = 0$. 
* **Step2 [Determina Cammino Aumentante]**: Trova un cammino da *s* a *t* in *G(x)*, se non esiste un cammino da *s* a *t*, allora il flusso *x* è massimo, quindi **STOP**.
* **Step3 [Aumenta il Flusso x]**: Sia *P* il cammino trovato da *s* a *t* trovato e poni $\delta = \min\{r_{ij}:(i,j) \in P\}$, per ogni $(i, j) \in P$:
  1. Se *(i,j)* corrisponde all'arco $(i, j) \in A: x_{ij} = x_{ij} + \delta$
  2. Se *(i,j)* corrisponde all'arco $(i, j) \in A: x_{ij} = x_{ij} - \delta$
Aggiorna il flusso $v = v + \delta$.

L'algoritmo *Ford-Fulkerson* ha complessità *O(nmU)*, con le relative migliorie si possono **ottenere prestazioni migliori**. 

### Taglio s-t
Si definisce un *Taglio s-t* una partizione dei vertici *N*, del grafo *G* in due sottoinsiemi $S$ e $S^{-} = N \ S$ tali che $s \in S$ e $t \in S^{-}$.
**Teorema**
Dato un *flusso ammissibile x* pari a *v*, per ogni *taglio s-t* $(S, S^{-})$ si ha come valore del limite superiore, il *minimo* dell'arco che connette la parte *S* alla parte $S^{-}$.