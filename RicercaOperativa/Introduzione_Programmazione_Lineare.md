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

## Programmazione Lineare
La programmazione lineare mira a minimizzare o minimizzare una *funzione obiettivo* lineare in presenza di *vincli* lineari.

Per esempio:
$$
\begin{align*}
& \text{min} \quad z = \sum_{j-1}^n c_jx_j \\
& \qquad s.t. \\
& \qquad\qquad \sum_{j-1}^n a_{ij}x_j \geq b)i & i=1,...,m \\
& \qquad\qquad x_j \geq 0 & j=1,...,n
\end{align*}
$$

dove:
- $x_j$ variabile decisionale
- $c_j$ coefficiente di costo della variaible $x_j$
- $b_i$ termine noto del vincolo $i$
- $a_{ij}$ coefficiente della variaible $x_j$ nel vincolo $i$
- $z$ valore della funzione obiettivo.

È possibile rappresentare il sistema lineare mediante le matrici, ottenendo così:
$$
\begin{align*}
& \text{min} \quad z = \textbf{cx} \\
& \qquad s.t. \\
& \qquad\qquad \textbf{Ax} \geq \textbf{b} \\
	& \qquad\qquad \textbf{x} \geq 0
\end{align*}
$$
Dove le matrici coinvolte sono:
$$
\textbf{c} = \begin{bmatrix}
c_1\\
c_2\\
\vdots \\
c_n
\end{bmatrix}
\qquad
\textbf{x}= \begin{bmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{bmatrix}
\qquad
\textbf{b}= \begin{bmatrix}
b_1 \\
b_2 \\
\vdots \\
b_m
\end{bmatrix}
\qquad
\textbf{A}= \begin{bmatrix}
a_{11} & a_{12} & \dots & a_{1n} \\
a_{21} & a_{22} & \dots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \dots & a_{mn} \\
\end{bmatrix}
$$

e in particolare:
- nell'equazione $\textbf{Ax} \geq \textbf{b} \\$ la soluzione del prodotto matrice vettore della disequazione ha la seguente forma lineare:
$$
\begin{cases}
a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n \geq b_1 \\
a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n \geq b_2 \\
\vdots \\
a_{m1}x_1 + a_{m2}x_2 + \dots + a_{mn}x_n \geq b_m \\
\end{cases}
$$
- Nel prodotto $z = \textbf{cx}$, è sottointeso che il vettore colonna $\textbf{c}$ venga trasposto affinche possa avvenire il prodotto scalare, quindi in realtà $z =\textbf{c}^T\textbf{x}$, ma si usa la forma semplificata quando è facilmente deducibile come in questo caso.
- La matrice $\textbf{A}$ è anche detta **matrice dei vincoli**, contenente i coefficienti delle variabili decisionali, escludendo i termini noti.

### Assunzioni implicite per LP
Nella formulazione di un problema di PL, sono implicite le assunzioni di:
- **Proporzionalità**: ogni variabile $x_j$ contribuisce con la quantità:
	- $c_jx_j$ al valore della funzione obiettivo.
	- $a_{ij}x_j$ al vincolo $i$.
- **Addittività**: ogni componente deve dare il suo contributo, in particolare:
	- Il valore della funzione obiettivo è dato dalla **somma** dei contributi $c_jx_j$ forniti da ciascuna variabile $j$.
	- Il contributo totale ad ogni vincolo $i$ è dato dalla somma dei contributi $a_{ij}x_j$ forniti da ciascuna variaible $j$.
- **Dati Deterministici**: tutti i coefficienti e parametri di un problema di PL, $c_j$, $a_{ij}$ e $b_i$ devono essere **noti**.
	- Nel caso che alcuni dati fossero non noti o di natura stocastica, essi devono essere approssimati con dati deterministici, per esempio estrapolati da numeri medi o dalla creazione di diversi scenari per varie configurazioni del problema.
	- Non ci addentreremo nella programmazione stocastica.
- **Continuità delle Variabili**: le variabili possono asumere **tutti i valori** reali che soddisfano i vincoli.
	- La programmazione lineare nel continuo, di norma, risolve problemi facili.

### Soluzione di un problema LP
Per ogni problema di programmazione lineare, la sua soluzione può essere di uno (o più) dei seguenti tipi:
- **Soluzione Ammissibile**: Una istanza particolare del vettore $\textbf{x}$ che soddisfa i vincoli $\textbf{Ax}\geq\textbf{b}$ e i vincoli di *non negatività* $\textbf{x} \geq 0$ è detta *soluzione ammissibile*.
- **Regione Ammissibile**:  è l'insieme di tutte le soluzioni ammissibili. Nella PL, assume la forma di un poliedro convesso delimitato o illimitato nella regione del problema.
- **Soluzione Ottima**: La soluzione ammissibile $\textbf{x}^*$ che minimizza/massimizza il valore della funzione obiettivo è detta *soluzione ottima*. In particolare essa può essere:
	- *Nessuna*: quando la soluzione è illimitata, e quindi nessuna è migliore di tutte le altre (vedi esempio sotto).
	- *Unica*
	- *Molteplice*: (ancora esempio sotto magari fare link) sono soluzioni che hanno caratteristiche particolari.
- **Problema senza soluzione**: Se la regione ammissibile è *vuota*, allora diremo che il problema non ha soluzione o che il problema non è ammissibile.

#### Esempio: Soluzione Ottima Unica
Sia il problema di programmazione lineare:
$$
\begin{align*}
    & \text{min} \quad z = -x_1 -3x_2 \\
    & s.t. \\
    & -x_1 -x_2 \geq-6 \\
    & \quad x_1 -2x_2 \geq -8 \\
    & \quad x_1 +x_2 \geq 2 \\
    & \quad x_1, x_2 \geq 0
\end{align*}
$$
È possibile tracciare in un grafico le aree ammissibili per ogni vincolo, in particolare è consigliato il seguente approccio:
- Trovare il valore di $x_1$ mettendo $x_2 = 0$ e risolvere l'equazione per entrambi i membri, ovvero i punti di intersezione con gli assi.
- Tracciare la retta passante per i due punti trovati.
- Individuare se l'origne è compreso nell'intervallo considerato risolvendo la disquazione del vincolo.
- Ripetere per tutti i vincoli del problema.
- Infine tracciare l'area ammissibile nell'interesezione che risulta tra le diverse aree.

Fatto questo, è possibile determinare la zona ammissibile del problema.
Ora è possibile utilizzare il valore del **gradiente** della funzione obiettivo per individuare l'insieme delle *curve di livello* che, intersecandosi col poliedro della zona ammissibile, ci permetterà di determinare l'insieme delle soluzioni e soprattutto la soluzione ottima.

Quindi:

$$\nabla z = \begin{bmatrix}
        \dfrac{\partial z}{\partial x_1} \\
        \dfrac{\partial z}{\partial x_2}
\end{bmatrix}
=\begin{bmatrix}
    -1 \\
    -3
\end{bmatrix}
$$

Il quale ci indica le coordinate della direzione del vettore gradiente di $z$.
In base alla richiesta del problema, dobbiamo decidere se seguire la direzione del gradiente, oppure procedere in direzione opposta ad esso, poiché il gradiente indica dove la funzione cresce maggiormente. Quindi:
- Se il problema PL è di **Massimo**, allora bisogna seguire la direzione del gradiente.
- Se il problema PL è di **Minimo**, bisogna seguire la direzione **opposta** del gradiente.

Nel nostro caso quindi, seguiamo l'inverso del gradiente, ovvero $\begin{bmatrix} 1 \\ 3\end{bmatrix}$. 
Ora è possibile tracciare le rette tangenti alla direzione del gradiente (ovvero le rette perpendicolari), in modo tale da poter individuare quel punto del poliedro che massimizza/minimizza la funzione obiettivo.

La soluzione ottima del problema, corrisponde ad un **vertice** (o **punto estremo**) della regione ammissibile, come mostrato nella figura sotto.

![Grafico Soluzione Ottima](./img/intro_pl/es1_sol.png)

#### Esempio: Soluzioni Ottime Equivalenti
$$
\begin{align*}
    & \text{max} \quad z = 2x_1 + 3x_2\\
    & s.t. \\
    & \quad x_1 + 3x_2 \leq9 \\
    & \quad 4x_1 +6x_2 \leq 24 \\
    & \quad x_1, x_2 \geq 0
\end{align*}
$$
Se ragioniamo come prima per la definizione delle regioni ammissibili, possiamo ottenere il poliedro che definisce l'insieme delle soluzioni del problema. A questo punto calcoliamo il gradiente della funzione $z$, ma a differenza di prima, seguiamo il suo verso poiché si tratta di un problema di masimo. Tracciando le curve di livello però, si può notare come la l'ultima curva che interseca la regione ammissibile ha la stessa inclinazione della retta passante per i punti B e C in figura più sotto. Questo accade perché uno dei vincoli è proporzionale alla funzione obietivo (il secondo dei vincoli), provocando quindi un'insieme di soluzioni ottime in corrispondenza del segmento tra B e C, ovvero dove la funzione obiettivo assume il valore $z^*=12$.
Appartengono alla soluzione ottima quindi i punti $A=(3,2)$ e $C=(6,0)$.
![Grafico Soluzione Ottima](./img/intro_pl/es2_sol.png)

#### Esempio: Soluzione Illimitata

![Grafico Soluzione Ottima](./img/intro_pl/es3_sol.png)