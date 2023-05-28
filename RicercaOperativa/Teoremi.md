- [Programmazione Lineare](#programmazione-lineare)
  - [Teorema della Rappresentazione](#teorema-della-rappresentazione)
  - [Step Simplesso Primale](#step-simplesso-primale)
  - [Dualità Debole (*Lemma*)](#dualità-debole-lemma)
    - [Dimostrazione](#dimostrazione)
    - [Corollario 1.](#corollario-1)
      - [Dimostrazione](#dimostrazione-1)
  - [Dualità Forte](#dualità-forte)
    - [Teorema 1](#teorema-1)
      - [Dimostrazione](#dimostrazione-2)
  - [Condizioni di Complementarietà](#condizioni-di-complementarietà)
    - [Corollario 2.](#corollario-2)
      - [Dimostrazione](#dimostrazione-3)
        - [Parte 1](#parte-1)
        - [Parte 2](#parte-2)
  - [Metodo 2 Fasi fun facts](#metodo-2-fasi-fun-facts)
    - [Degenerazione e Convergenza: Regola di Bland](#degenerazione-e-convergenza-regola-di-bland)
  - [Simplessi e garanzie](#simplessi-e-garanzie)
    - [Base ammissibile Simplesso Duale](#base-ammissibile-simplesso-duale)
- [Programmazione Lineare Intera](#programmazione-lineare-intera)
  - [Regole di Branching](#regole-di-branching)
    - [Algoritmo Branch and Bound](#algoritmo-branch-and-bound)
  - [Valid Inequalities: Tagli di Gomory](#valid-inequalities-tagli-di-gomory)
  - [Rilassamento Lagrangiano](#rilassamento-lagrangiano)
    - [Dualità Lagrangiana Debole](#dualità-lagrangiana-debole)
      - [Dimostrazione](#dimostrazione-4)
    - [Dualità Lagrangiana Forte](#dualità-lagrangiana-forte)
      - [Dimostrazione](#dimostrazione-5)
        - [Parte 1](#parte-1-1)
        - [Parte 2](#parte-2-1)
  - [Teorema: Metodo del Subgradiente](#teorema-metodo-del-subgradiente)
    - [Dimostrazione](#dimostrazione-6)
    - [Calcolo del $\\theta$](#calcolo-del-theta)
    - [Considerazioni](#considerazioni)
  - [Algoritmo: Metodo del Subgradiente](#algoritmo-metodo-del-subgradiente)
  - [Column Generation](#column-generation)
    - [Algoritmo: Column Generation](#algoritmo-column-generation)
  - [TSP](#tsp)
- [Graph Theory](#graph-theory)
  - [Flusso a costo Minimo](#flusso-a-costo-minimo)
    - [Duale](#duale)
    - [Definizioni varie](#definizioni-varie)
      - [Grafo residuo](#grafo-residuo)
      - [Potenziali](#potenziali)
        - [Proprietà dei potenziali](#proprietà-dei-potenziali)
      - [Condizioni di Ottimalità](#condizioni-di-ottimalità)
    - [Cycle Canceling: Costi](#cycle-canceling-costi)
    - [Successive Shortest Path](#successive-shortest-path)
      - [Lemma](#lemma)
      - [Costi](#costi)
    - [Primal Dual](#primal-dual)
    - [Out-of-Kilter](#out-of-kilter)
    - [Algoritmi Polinomiali e Pseudopolinomiali](#algoritmi-polinomiali-e-pseudopolinomiali)
  - [Flusso massimo](#flusso-massimo)
    - [Proprietà di Ford Fulkerson](#proprietà-di-ford-fulkerson)
      - [Teorema (Grafo Residuo)](#teorema-grafo-residuo)
      - [Costi](#costi-1)
      - [Taglio $s$-$t$](#taglio-s-t)
      - [Teoremi sui Tagli](#teoremi-sui-tagli)
        - [Max-Flow/Min-Cut](#max-flowmin-cut)

# Programmazione Lineare
## Teorema della Rappresentazione
Sia dato un insieme Poliedrico convesso $X = \{\textbf{x} : \textbf{Ax}\ = \textbf{b}, \textbf{x} \geq 0\}$.
Sia $P = \{\mathbf{x}_j: i=1,\dots , np\}$ l'insieme di tutti i **punti estremi** di $X$ e sia $D = \{\mathbf{d}_j: j=1,\dots,nd\}$ l'insieme di tutte le **direzioni estreme** di $X$.
Ogni Punto di $X$ può essere rappresentato come:
$$
\begin{align*}
    \mathbf{x} = &\sum_{i=1}^{np}\lambda_i \mathbf{x}_i + \sum_{j=1}^{nd}\mu_j \mathbf{d}_j \\
    s.t. &\sum_{i=1}^{np}\lambda_i = 1 \\
    & \lambda_i \geq 0, & i =1,\dots,np \\
    & \mu_j \geq 0, & j =1,\dots,nd \\
\end{align*}
$$

## Step Simplesso Primale
1. Definire una soluzione basee ammissibile $\mathbf{x = [x_B, X_N] = [B^{-1}b, 0] = [\bar{b}, 0]}$ di costo $z = \mathbf{c_B x_B = c_B B^{-1}b}$.
2. Calcolare $\mathbf{w=c_B B^{-1}}$ e calcolare i **costi ridotti** $\mathbf{wa_j} - c_j$ per le variabile non-base $j\in N$ e determina: $$\mathbf{wa_k} - c_k = \max_{j\in N}\{\mathbf{wa_j} - c_j\}$$
3. Se $\mathbf{wa_k} - c_j < 0$ allora STOP, la **soluzione è ottima**.
4. Calcola $\mathbf{y^k = B^{-1}a_k}$; se $\mathbf{y^k} < 0$, allora STOP la soluzione è **illimitata**.
5. Calcola il valore da assegnare a $x_k$: $$x_k = \frac{\bar{b}_r}{y^k_r} = \min \left\{ \frac{\bar{b}_i}{y^k_i}: y^k_i > 0, i=1,\dots,m\right\}$$ La variabile $x_r$ esce dalla base e $x_k$ entra al posto suo. Aggiorna $\mathbf{B, N}$ e la soluzione base $\mathbf{x = [x_B, x_N] = [\bar{b}, 0]}$. Ritorna allo step 2.

## Dualità Debole (*Lemma*)
Se $\mathbf{\tilde{x}} \in X = \mathbf{\{x: Ax \geq b, x \geq 0\}}$ e $\mathbf{\tilde{w}} \in W = \{\mathbf{w: wA \leq c, w \geq 0}\}$ allora $\mathbf{\tilde{w}b \leq c\tilde{x}}$.

### Dimostrazione
Siccome $\mathbf{\tilde{x}} \in X$ allora $\mathbf{A\tilde{x} \geq b}$. Poichè $\mathbf{\tilde{w}} \geq 0$, si ha (cioè possiamo premoltiplicare per w easy senza cambiare il segno della disequazione):
$$\mathbf{\tilde{w}A\tilde{x} \geq \tilde{w}b}$$
Similmente, siccome $\mathbf{\tilde{w}} \in W$, allora $\mathbf{\tilde{w}A \leq c}$. Poiché $\mathbf{\tilde{x}} \geq 0$, allora:
$$\mathbf{\tilde{w}A\tilde{x} \leq c\tilde{x}}$$
Si ottiene quindi: $\mathbf{\tilde{w}b \leq c\tilde{x}}$, ovvero il valore di una soluzione duale è un lower bound allo soluzione ottima del primale. 

**Picola Digressione sul Duale**: Perciò per trovare il miglior lower bound, si può imporre che la funzione obiettivo del duale massimizzi il valore di questa soglia $\mathbf{wb}$, quindi la risoluzione del seguente PL:
$$
\begin{align*}
    z = \max    \quad&\mathbf{wb} \\
    s.t.        \quad&\mathbf{wA} \leq c \\
                \quad&\mathbf{w} \geq 0
\end{align*}
$$

### Corollario 1.
Se $\mathbf{x^*} \in X$ e $\mathbf{w^*} \in W$ soddisfano $\mathbf{w^*b = cx^*}$, allora $\mathbf{x^*}$ è soluzione ottima del primale e $w^*$ è soluzione ottima del duale.
#### Dimostrazione
Per dualità debole si ha $\mathbf{wb \leq cx}$, $\forall\mathbf{w} \in W$ e $\forall\mathbf{x} \in X$.
Quindi, $\mathbf{cx \geq w^*b}$, $\forall\mathbf{x} \in X$, ma poiché per ipotesi $\mathbf{w^*b = cx^*}$ si ha:
$$\mathbf{cx \geq w ^*b=cx^*}, \forall \mathbf{x} \in X$$ Per cui $\mathbf{x^*} \in X$ è **soluzione ottima** del primale.
Analogamente, $\mathbf{cx^* \geq wb}, \forall \mathbf{w} \in W$, ma poichè per ipotesi $\mathbf{w^*b = cx^*}$ si ha: $$\mathbf{w^*b = cx^* \geq wb}, \forall \mathbf{w}\in W$$.
Per cui anche $\mathbf{w^*}\in W $ è **soluzione ottima** del duale.

## Dualità Forte
Stabilisce che se *esistono soluzioni ammissibili* sia per il primale, che per il duale, allora esistono due soluzioni ottime i cui valori coincidono.
### Teorema 1
Se $X\neq \empty$ e $W \neq \empty$, allora esiste una soluzione $\mathbf{x^*}$ ottima per il primale e una soluzione $\mathbf{w^*}$ per il duale. Inoltre $\mathbf{w^*b = cx^*}$.
#### Dimostrazione
Per il [corollario 1](#corollario-1) è sufficiente dimostrare che esistono $\mathbf{x^*} \in X$ e $\mathbf{w^*} \in W$ tali che $\mathbf{w^*b = cx^*}$.

Siccome $W \neq \empty$ per ipotesi, per la [dualità debole](#dualità-debole-lemma) il valore di $\mathbf{cx}$ è limitato inferiormente, poiché $\mathbb{wb}$ fornisce un lower bound alla soluzione ottima del problema primale. Di conseguenza, $X\neq \empty$ e $\mathbf{cx}$ limitata: ciò implica che il primale ha soluzione ottima *limitata*.

Se riscriviamo il primale in forma standard:
$$\begin{align*}
    z = \min    \quad&\mathbf{cx} \\
    s.t.        \quad&\mathbf{Ax - Ix_S} = b \\
                \quad& \mathbf{x,x_S} \geq 0
\end{align*}$$
Possiamo indicare con $\mathbf{(x^*, x^*_S)}$ la soluzione ottima del primale e con $\mathbf{B}$ la corrispondente base ottima.

Per le condizioni di ottimalità si ha che
$$\mathbf{c_B B^{-1}a_j} - c_j \leq 0, \quad j=1,\dots,n+m$$
Dove ponendo $\mathbf{w^* = c_B B^{-1}}$, equivale a:
$$\begin{align*}
    \mathbf{w^*A}&\leq \mathbf{c} \\
    \mathbf{w^*} &\geq 0
\end{align*}$$

Per cui la soluzione $\mathbf{w^*=c_B B^{-1}}$ è duale ammissibile, cioè $\mathbf{w^*}\in W$.
Infine, siccome $\mathbf{w^* = c_B B^{-1}}$ e $\mathbf{x^*=(B^{-1}b, 0)}$, si ha:
$$\mathbf{w^* b = c_B B^{-1}b = cx^*}$$
Per cui il teorema è dimostrato.

## Condizioni di Complementarietà
### Corollario 2.
Le soluzioni $\mathbf{\tilde{x}} \in X$ del primale e $\mathbf{\tilde{w}} \in W$ del duale sono ottime *se e solo se*:
$$
\begin{align}
    \mathbf{\tilde{w}(A\tilde{x} - b) = 0} \\
    \mathbf{(c - \tilde{w}A)\tilde{x} = 0} \\
\end{align}$$

#### Dimostrazione
Si vuole dimostrare che:
- Se $(1)$ e $(2)$ sono soddisfatte, allora le soluzioni $\mathbf{\tilde{x}}$ e $\mathbf{\tilde{w}}$ sono ottime.
- Se le soluzioni $\mathbf{\tilde{x}}$ e $\mathbf{\tilde{w}}$ sono ottime, allora le condizioni $(1)$ e $(2)$ *devono* essere soddisfatte.

##### Parte 1
Dal [lemma della dualità debole](#dualità-debole-lemma) si ha che per ogni $\mathbf{\tilde{x}}$ e $\mathbf{\tilde{w}}$: $$\mathbf{\tilde{w}b \leq \tilde{w}A\tilde{X} \leq c\tilde{x}}$$

Ma se $(1)$ e $(2)$ sono soddisfatte, si ha anche:
$$
\begin{align*}
    \mathbf{\tilde{w}A\tilde{x}} &= \mathbf{\tilde{w}b} \\
    \mathbf{c\tilde{x}} &= \mathbf{\tilde{w}A\tilde{x}}
\end{align*}
$$
Allora necessariamente $\mathbf{\tilde{w}b = c\tilde{x}}$, e per il [corollario 1](#corollario-1), $\mathbf{\tilde{x}}$ e $\mathbf{\tilde{w}}$ sono ottime.

##### Parte 2
Se una delle due condizioni di complementarietà non è soddisfatta, allora almeno una delle due soluzioni non è ottima, perché se per esempio $\mathbf{\tilde{w}(A\tilde{x} - b) > 0}$, allora ne consegue che $\mathbf{\tilde{w}b < c\tilde{x}}$, che violerebbe il corollario 1.

--- 
Questo corollario ci insegna che data una soluzione primale, per dimostrarne l'ottimalità è sufficiente trovare una soluzione duale che soddisfi le condizioni di complementarietà.

## Metodo 2 Fasi fun facts
Mediante il metodo due fasi si risolve il problema $P'$ associato al problema primale originario $P$.
Risolvere il problema $P'$ serve solo a determianre una soluzione base ammissibile per il problema $P$.

Sia $\mathbf{(x^*, x^*_A)}$ la soluzione ottima del problema $P'$ di valore $z_{P'}$. Si possono presentare 3 casi:
- $z_{P'} > 0$
  - $\implies$ il problema $P$ **non** ha una base ammissibile;
- $z_{P'} = 0$ e nessuna variabile artificiale è in base
  - $\implies$ il problema $P$ ha una base ammissibile;
- $z_{P'} = 0$ e almeno una variabile artificiale è in base
  - $\implies$ il problema $P$ ha una base ammissibile, ma bisogna estrarla. (**Soluzione Degenere**: una variabile in base ha valore nullo).

### Degenerazione e Convergenza: Regola di Bland
La *Regola di Bland* stabilisce che per evitare la degenerazione ciclante (un coefficiente $b_i = 0$, e si cicla su basi già considerate) è sufficiente scegliere tra le variabili candidate a entrare in base e quelle candidate a uscire dalla base quelle di **indice minimo**.

## Simplessi e garanzie
Il **simplesso primale** ad ogni iterazione soddisfa:
- *Ammissibilità primale* della soluzione $\bar{b}_i \geq 0$ per ogni $i$.
- Le Condizioni di Complementarietà

Il **simplesso duale** ad ogni iterazione soddisfa:
- L'ammissibilità duale della soluzione: $\mathbf{wa_j} - c_j \leq 0$ per ogni $j$.
- Le Condizioni di Complementarietà.

Per entrambi i casi le Condizioni di Complementarietà sono soddisfatte perché le variabili $x_j$ che sono in base hanno $\mathbf{wa_j} - c_j = 0$, mentre quelle con in base hanno valore nullo.


### Base ammissibile Simplesso Duale
Se alcuni $\mathbf{wa_j} - c_j$ sono $ > 0$, allora la base non è duale ammissibile. Per ovviare a questo problema aggiungiamo un vincolo artificiale della forma:
$$\sum_{j\in N}x_j \leq M \implies \sum_{j\in N}x_j + x_{n+1} = M$$
Dove $N$ è l'insieme delle variabili *non base* ed $M$ è un numero positivo sufficientemente grande.
Dopodiché pivotiamo sulla colonna $k$ tale che:
$$\mathbf{wa_k} - c_k = \max\{\mathbf{wa_j} - c_j: j \in N\}$$
Due outcome sono possibili:
- $x_{n+1} > 0$ &rarr; la soluzione **è ottima**.
- $x_{n+1} = 0$ &rarr; la soluzione **è illimitata**.

# Programmazione Lineare Intera
## Regole di Branching
Noi consideriamo la regola di branching per cui, selezionata la variabile frazionaria $x_j$, possiamo creare due sottoproblemi del tipo:
- $P(x_j \leq \lfloor x_j\rfloor)$: ottenuto da LP aggiungendo il vincolo $x_j \leq \lfloor x_j \rfloor$.
- $P(x_j \geq \lceil x_j\rceil)$: ottenuto da LP aggiungendo il vincolo $x_j \geq \lceil x_j \rceil$.

Per ogni nodo $k$ dobbiamo risolvere il sottproblema $P_k$ ottenendo la soluzione $\mathbf{x_k}$ di costo $z_k$, presentando i seguenti outcome:
- Se $P_k$ **non ha soluzione ammissibile**, poniamo $z_k = +\infty$ e *non generiamo nodi figli*.
- Se la soluzione $\mathbf{x_k}$ di $P_k$ è **intera**, allora è sicuramente un **upper bound** alla soluzione ottima del problema intero originario, e non è necessario generare ulteriori figli poiché questi possono solo portare a lower bound della soluzione corrente.
- Se la soluzione $\mathbf{x_k}$ di $P_k$ è **frazionaria**, allora $z_k$ rappresenta un **lower bound** al valore della migliore soluzione intera che si può ottenere nel sottoalbero di cui il nodo k è radice.

### Algoritmo Branch and Bound
1. Poni $z_{UB} = +\infty$ e inserisci nella heap vuota il problema $P_0: z_0\min\{\mathbf{cx: Ax \geq b, x \geq 0}\}$.
2. Estrai il problema $P_k$ dalla heap (se è vuota STOP), e ottieni la soluzione $\mathbf{x_k}$ di costo $z_k$.
   1. Se $z_k \geq z_{UB}$ torna allo step due e non espandere il nodo $k$.
   2. Se la soluzione $\mathbf{x_k}$  è intera, aggiorna l'upper bound: $z_{UB} = z_k$ e $\mathbf{x = x_k}$.
3. Seleziona una variabile $x_j$ frazionaria nella solzione $\mathbf{x_k}$ e inserisci nella heap due nodi figli $P(x_j \leq \lfloor x_j\rfloor)$ e $P(x_j \geq \lceil x_j\rceil)$; torna allo step 2.

## Valid Inequalities: Tagli di Gomory
Prendendo il tableau ottimo con soluzioni frazionarie, possiamo decomporre la riga $i-$esima in parte intera e frazionaria. Possiamo quindi aggiungere un nuovo vicolo al tableau, detto *taglio di Gomory*, dove se le variabili attualemnte include sono $n$, la nuova riga nel tableau ottimo è pari a:
$$-\sum_{j \in N}F^j_ix_j + x_{n+1} = -F_i$$

## Rilassamento Lagrangiano
Consideriamo il problema $P$:
$$
\begin{align*}
  z_P = \min  \quad&\mathbf{cx} \\
  s.t.        \quad&\mathbf{Ax \geq b} \\
              \quad&\mathbf{Bx \geq d} \\
              \quad&\mathbf{x \geq 0} \text{ and integer}
\end{align*}$$

Il rilassamento lagrangiano permette di:
- Rimuovere vincoli considerti rimossi
- I vincoli rimossi sono **inserti** nella funzione obiettivo per mezzo delle **penalità lagrangiane**.

$P$ quindi ora diventa:
$$
\begin{align*}
  z_{LR}(\lambda) = \min  \quad&\mathbf{cx} + \lambda(\mathbf{b - Ax}) \\
  s.t.                    \quad&\mathbf{Bx \geq d} \\
                          \quad&\mathbf{x \geq 0} \text{ and integer} 
\end{align*}
$$

### Dualità Lagrangiana Debole
$z_{LR}(\lambda)$ è un *valido lower bound* al valore della soluzione ottima di $P$, per ogni $\lambda \geq 0$.

#### Dimostrazione
Sia $\mathbf{x^*}$ la soluzione ottima di $P$. Siccome $\mathbf{x^*}$ è una soluzione ammissibile per $LR(\lambda)$, per ogni $\lambda \geq 0$ si ha che:
$$z_{LR}(\lambda, \mathbf{x^*}) = \mathbf{cx^* + \lambda(b-Ax^*)} \geq z_{LR}(\lambda)$$
Dove $z_{LR}(\lambda)$ è la soluzione ottima per quel certo $\lambda$ scelto.

Però $\mathbf{\lambda(b - Ax^*)} \leq 0$, perché $\lambda \geq 0$ e $\mathbf{Ax^* \geq b}$, quindi:
$$z_{LR}(\lambda) \leq z_{LR}(\lambda, \mathbf{x^*})\leq z_P, \quad \forall \mathbf{\lambda \geq 0}$$

### Dualità Lagrangiana Forte
Dato il problema $P$, sia $\mathbf{\bar{x}}$ la soluzione ottima di $z_{LR}(\bar{\lambda})$ per un  dato $\bar{\lambda} \geq 0$. Se $\mathbf{\bar{x}}$ e $\bar{\lambda}$ soddisfano le seguenti condizioni:
- $\mathbf{\bar{x}}$ è ammissibile per $P$ (cioè $\mathbf{A\bar{x} \geq b}$)
- $\mathbf{\bar{\lambda}(b - A\bar{x}) = 0}$

Allora  $\bar{\mathbf{x}}$ è la **soluzione ottima** di $P$ e $z_{LR} = z_{LR}(\bar{\lambda})$.

#### Dimostrazione
##### Parte 1
Si vuole dimostrare che la soluzione $\mathbf{\bar{x}}$ è **ottima**.
Essendo $\mathbf{\bar{x}}$ *soluzione ammissibile* di $P$, si ha:
$$\mathbf{c\bar{x}} \geq z_P$$
Per il teorema della dualità lagrangiana debole, si ha che:
$$z_P \geq z_{LR}(\bar{\lambda}) = \mathbf{c\bar{x} + \bar{\lambda}(b - A\bar{x})}$$
Ma per ipotesi, $\mathbf{\bar{\lambda}(b-A\bar{x}) = 0}$, quindi otteniamo:
$$\mathbf{c\bar{x}} \geq z_P \geq \mathbf{c\bar{x}} \implies z_p = \mathbf{c\bar{x}}(=z_{LR}(\bar{\lambda}))$$

##### Parte 2
Si vuole dimostrare che $z_{LR} = z_{LR}(\bar{\lambda})$.
Dalla definizione di lagrangiano duale, si ha che:
$$z_{LR} \geq z_{LR}(\bar{\lambda})$$
Mentre, dalla *dualità lagrangiana debole*, si ha che:
$$z_P \geq z_{LR}$$
Quindi, insieme all'ultimo passaggio della parte 1 ($z_p = z_{LR}(\bar{\lambda})$), otteniamo:
$$z_{LR} = z_{LR}(\bar{\lambda})$$

--- 
NB: tutte le dimostrazioni e teoremi della differenza tra Rilassamento Lineare e Lagrangiano verranno brutalmente paccate perché non ho idea di cosa sia una combinazione convessa, e non ho voglia di perdere la vita per massimo 3/4 punti su 33 ;). (che dio ce la mandi buona)
## Teorema: Metodo del Subgradiente
La funzione Lagrangiana $z_{LR}(\bar{\lambda}) = \mathbf{c\bar{x} + \bar{\lambda}(b - A\bar{x})}$ è **concava** (quindi esiste un massimo :)).

### Dimostrazione
No grazie.

L'unica cosa interessante è che un vettore $s$ è detto **subgradiente** della funzione $f(\lambda)$ nel punto $\bar{\lambda}$ se soddisfa la seguente condizione:
$$f(\lambda) \leq f(\bar{\lambda}) + s(\lambda - \bar{\lambda})$$

--- 
Il subgradiente della funzione lagrangiana è trovabile come:
$$z_{LR}(\bar{\lambda}) = \mathbf{c\bar{x} + \bar{\lambda} (b - A\bar{x})}$$
Dove per ogni $\lambda \geq 0$, le soluzioni del lagrangiano sono più piccole o pari alla soluzione ottima, ovvero:
$$z_{LR}(\lambda) \leq \mathbf{c\bar{x} + \bar{\lambda} (b - A\bar{x})}$$
Se sottraiamo queste due, otteniamo:
$$z_{LR}(\lambda) - z_{LR}(\bar{\lambda}) \leq (\lambda - \bar{\lambda})\mathbf{(b - A\bar{x})}$$
Che riscrivendo come:
$$z_{LR}(\lambda) \leq z_{LR}(\bar{\lambda}) + (\lambda - \bar{\lambda})\mathbf{(b - A\bar{x})}$$
Risulta proprie l'equazione del subgradiente sopra; in particolare, $\mathbf{s = (b - A\bar{x})}$ è un subgradiente della funzione Lagrangiana $z_{LR}(\lambda)$ calcolata nel punto $\bar{\lambda}$.

### Calcolo del $\theta$
$\theta$ è lo spostamento lungo il subgradiente, e compare nella formual di aggiornamento delle penalità lagrangiane come: $\lambda = \bar{\theta}+ \theta \mathbf{s}$.

- **Modo Esatto**: $\theta^* = \argmax\{z_{LR}(\bar{\lambda} + \theta \mathbf{s}): \theta > 0\}$, ma può essere molto costoso.
- Ad ogni iterazione $k$ del subgradiente lo spostamento $\theta^k$ può essere calcolato con i seguenti approcci euristici:
  - ***Polyak-type step size***: $$\theta^k = \beta^k \frac{\bar{z} - z_{LR}(\mathbf{\lambda^k})}{||\mathbf{s^k}||^2_2}$$ con $0 < \beta^k \leq 2$, garantisce convergenza di $z_{LR}(\lambda^k)$.
  - Tramite una *sovrastima* di $z_{LR}(\lambda^k)$: $$\theta^k = \beta^k \frac{0.01 \times z_{LR}(\lambda^k)}{||\mathbf{s^k}||^2_2}$$

### Considerazioni
Quando si aggiornano le penalità lagrangiane, si deve tenere conto di eventuali vincoli di segno:
- $\mathbf{a_ix} = b_i$: la penalità $\lambda_i$ può essere qualsiasi &rarr; $\lambda^{k+1}_i = \lambda_i^k + \theta^ks_i$


- $\mathbf{a_ix} \geq b_i$: la penalità $\lambda_i$ deve essere non negativa &rarr; $\lambda^{k+1}_i = \max\{0, \lambda_i^k + \theta^ks_i\}$


- $\mathbf{a_ix} \leq b_i$: la penalità $\lambda_i$ deve essere non positiva &rarr; $\lambda^{k+1}_i = \min\{0, \lambda_i^k + \theta^ks_i\}$

## Algoritmo: Metodo del Subgradiente
1. Sia $z_P = \min \{\mathbf{cx: Ax\geq b, x}\in X\}$, dove $\mathbf{A}\in\mathbb{R}^{m\times n}$, $\mathbf{c} \in \mathbb{R}^n$ e $\mathbf{b} \in \mathbb{R}^m$. <br> Poni $z_{LB} = -\infty$, $z_{UB} = + \infty$ e $\mathbf{\lambda} = 0$.
2. Risolvi il problema Lagrangiano $$z_{LR}(\lambda) = \mathbf{(c - \lambda A)\bar{x} +\lambda b} = \min\{\mathbf{(c - \lambda A)x + \lambda b: x \in} X\}$$ e aggiorna il *lower bound* $z_{LB} = \min\{z_{UB}, \mathbf{c\bar{x}}\}$.
3. Se $\mathbf{\bar{x}}$ è ammissibile $z_{UB} = \min \{z_{UB}, \mathbf{c\bar{x}}\}$, e se ottima, STOP! (per ottimalità vedi la [dualità lagrangiana forte](#dualità-lagrangiana-forte)).
4. Aggiorna le penalità lagrangiane (occhio al segno del vincolo rilassato nel problema specifico) $$\lambda_i = \max\{0, \lambda_i + \theta s_i\}, \quad i=1,\dots,m$$ dove $s_i=b_i -\mathbf{a_i\bar{x}}$ e torna allo step 2.

## Column Generation
Il problema di programmazione lineare:
$$
\begin{align*}
z(P) = \min   &\sum_{j=1}^n c_jx_j \\
s.t.          &\sum_{j=1}^n a_{ij}x_j = b_i, &i=1,\dots,m \\
              &x_j \geq 0, &j=1,\dots,n \\
\end{align*}
$$

Data una base $B$ di $A$, la corrispondente soluzione base può esse migliorata se esiste una colonna $h$ tale che $\bar{c}_h > 0$ dove:
$$\bar{c}_h = \max\{\bar{c}_j = wa_j - c_j: j=1,\dots,n\} > 0$$
Che viene definito *problema di **pricing***, dove in alcuni casi, dove applicare il simplesso può risultare proibitivo, la sua struttura è tale da consentire di calcolare la soluzione ottima senza considerare esplicitamente tutte le varibaili del problema originario.
### Algoritmo: Column Generation
1. Definisci una base ammissibile iniziale $B$.
2. Calcola la solzuione base corrispondente a $B$: $$x = (x_b, 0) = (B^{-1}b, 0)$$ e la corrispondente soluzione duale $$w = c_BB^{-1}$$
3. Risolvi il problema di pricing, generando la variabile $h$ di costo ridotto $\bar{c}_h = wa_h - c_h$ massimo.
4. Se il costo ridotto $\bar{c}_h \leq 0$ allora STOP: la solzuione $x$ è ottima e non è necesario generare altre colonne; altrimenti calcola la nuova base $B$ e vai allo step 2.


## TSP
Consideriamo un grafo direzionato $G=(V,A)$, dove $V$ è l'insieme dei vertici e $A$ è l'insieme degli archi. Ad ogni arco è associato un costo $c_{ij} : (i,j) \in A$. In questo caso $c_{ij} \neq c_{ji}$, per cui si parla di ***Asymmetric Traveling Salesman Problem***.

Siano $x_{ij}$ variabili decisionali binarie uguali a 1 se l'arco $(i,j)$ è nella soluzione ottima, 0 altrimenti.

Modellimao il TSP come:
$$
\begin{align*}
  z_{TSP} = \min &\sum_{i\in V}\sum_{j\in V}c_{ij}x_{ij} \\
  s.t.          &\sum_{j\in V}x_{ij} = 1 &i \in V \\
                &\sum_{j\in V}x_{ji} = 1 &i \in V \\
                &\sum_{i\in S}\sum_{j\in \bar{S}} x_{ij} \geq 1, &\forall S \subset V, \bar{S} = V \setminus S \\
                &x_{ij} \in \{0, 1\}, &(i,j) \in A
\end{align*}
$$

# Graph Theory
Sia dato un grafo direzionato $G=(N, A)$ in cui:
- Ad ogni arco $(i,j) \in A$ è associato:
  - Un **costo** $c_{ij}$
  - Una **capacità** $u_{ij}$
- Ad ogni *vertice* $i \in N$ è associata:
  - Una *disponibilità* $b_i > 0$
  - Una *richiesta* $b_i < 0$
  - Un *cazzo* se $b_i = 0$

## Flusso a costo Minimo
Può essere formulato come segue:
$$
\begin{align*}
  \min z(P) =   &\sum_{(i,j)\in A} c_{ij} x_{ij} \\
  s.t.          &\sum_{j\in \Gamma_i}x_{ij} - \sum_{j \in \Gamma_i^{-1}} x_{ji} = b_i & i \in N \\
                &0\leq x_{ij} \leq u_{ij} &(i,j) \in A \\
\end{align*}
$$
Dove:
- $\Gamma_i = \{j:(i,j) \in A\}$, archi uscenti dal vertice $i$.
- $\Gamma_i^{-1} = \{j:(j,i) \in A\}$, archi entranti nel vertice $i$.

### Duale
$$
\begin{align*}
  \max z(D) = \quad&\sum_{i\in N} b_i \pi_i - \sum_{(i,j) \in A} u_{ij}\alpha_{ij} \\
  s.t.        \quad& \pi_i - \pi_j - \alpha_{ij} \leq c_{ij} & (i,j)\in A \\
              \quad& \pi \text{ qualsiasi}, & i\in N \\
              \quad& \alpha_{ij} \geq 0, &(i,j) \in A \\
\end{align*}
$$

Dove:
- $\pi_i$ è la variabile duale associata al vincolo di conservazione del flusso corrispondente al nodo $i \in N$.
- $\alpha_{ij}$ variabile duale associata al vincolo di capacità relativo all'arco $(i,j) \in A$.

### Definizioni varie
#### Grafo residuo
Il grafo residuo $G(x)$ corrispondente al flusso $x$ è ottenuto sostituendo ogni arco $(i,j) \in A$  con due archi $(i,j)$ e $(j,i)$ tali che:
- $(i,j)$: con costo $c_{ij} = c_{ij}$ e *capactià residua* $r_{ij} = u_{ij} - x_{ij}$
- $(j,i)$: con costo $c_{ji} = -c_{ij}$ e *capacità residua* $r_{ji} = x_{ij}$.

#### Potenziali
Denotando il potenziale $\pi_i \in \mathbb{R}$ associato al nodo $i \in N$, possiamo definire il **costo ridotto** $c_{ij}^\pi$ come: $$c_{ij}^\pi =  c_{ij} - \pi_i + \pi_j$$

##### Proprietà dei potenziali
Per ogni cammino *diretto* $P$ dal nodo $k$ al nodo $l$ si ha:
$$\sum_{(i,j) \in P} c_{ij}^\pi = \sum_{(i,j) \in P} c_{ij} - \pi_k + \pi_l$$
E per ogni **ciclo diretto** $W$ si ha che:
$$\sum_{(i,j) \in W} c_{ij}^\pi = \sum_{(i,j) \in W} c_{ij}$$ poiché sorgente e destinazione sono uguali in un ciclo.

#### Condizioni di Ottimalità
Una soluzione $x^*$ ammissibile è ottima se e solo se:
- Il grafo residuo $G(x^*)$ non contiene **cicli di costo negativo**.
- È possibile trovare dei potenziali $\pi$ tali che, $\forall (i,j)$ di $G(x^*)$ soddisfano $c_{ij}^\pi = c_{ij} - \pi_i + \pi_j \geq 0$
- È possibile trovare dei potenziali $\pi$ tali che, $\forall (i,j) \in A$, il *costo ridotto* $c_{ij}^\pi$ soddisfa le seguenti condizioni degli **scarti complementari**:
$$
\begin{align*}
  &\text{If } c_{ij}^\pi > 0, \quad \text{then }x_{ij}^* =0 \\
  &\text{If } c_{ij}^\pi = 0, \quad \text{then } 0\leq x_{ij}^* \leq u_{ij}\\
  &\text{If } c_{ij}^\pi < 0, \quad \text{then }x_{ij}^* = u_{ij}\\
\end{align*}
$$

### Cycle Canceling: Costi
- Nel caso peggiore esegue $O(mCU)$ iterazioni.
- Ad ogni iterazione c'è un calcolo del cammino di costo minimo per scovare cicli di costo negativo: Bellman Ford con complessità $O(nm)$
- **Totale**: $O(nm^2CU)$

### Successive Shortest Path
#### Lemma
Sia $x$ un *pseudoflusso* che soddisfa le condizioni di non negatività dei costi ridotti per un qualche $\pi$ in $G(x)$.
Sia $d=(d_1, \dots, d_n)$ la *distanza minima* in $G(x)$ da un nodo $s$ a tutti gli altri nodi rispetto ai costi ridotti $c_{ij}^\pi$. Le seguenti proprietà sono valide:
- Il pseudoflusso $x$ soddisfa le condizioni di non negatività dei costi ridotti anche per i potenziali $\pi' = \pi - d$.
- I costi ridotti $c_{ij}^{\pi'}$ sono nulli per tutti gli archi $(i,j)$ nel cammino minimo da $s$ a ogni altro nodo.
---
Questo serve a dire che ad ogni iterazione, l'algoritmo deve selezionare un nodo $s$ con un eccesso di flusso, e un nodo $t$ con un deficit di flusso, e aumentare il flusso lungo il cammino di costo minimo da $s$ a $t$ nel grafo residuo $G(x)$.

#### Costi
- Nel caso peggiore sono effettuate $O(nU)$ iterazioni.
- Ad ogni iterazione viene calcolato uno shortest path: Applicando Dijkstra ($c_{ij}^\pi \geq 0$), la complessità è $O(m + n\log n)$ implementandolo con Heap di Fibonacci.
- **Totale**: $O(nU(m+n\log n))$

### Primal Dual 
Zero voglia
### Out-of-Kilter
Tanto meno
### Algoritmi Polinomiali e Pseudopolinomiali
Se lo mette scrivo meno di zero

## Flusso massimo
Sia dato un grafo *direzionato* $G=(N,A)$, in cui ad ogni arco $(i,j) \in A$ è associata una capacità $c_{ij} > 0$.

Si vuole determinare il *flusso massimo* che può essere inviato dal vertice **origine** $s \in N$ al vertice **destinazione** $t \in N$.

$$
\begin{align*}
  \max z(P) = \quad&v \\
  s.t.        \quad&\sum_{j \in \Gamma_i} x_{ij} - \sum_{j \in \Gamma^{-1}_i} x_{ji} = \begin{cases}
      v, &i=s \\
      -v, &i=t \\
      0, &i \neq s, t
  \end{cases} & i\in N \\
            \quad&0\leq x_{ij} \leq u_{ij}, &(i,j) \in A
\end{align*}
$$

### Proprietà di Ford Fulkerson
Quando termina, l'insieme dei vertici etichettati $S$ e quello dei vertici non etichettati $\bar{S}$ costituiscono un **taglio**, tale che il flusso ottimo $v^*$ è pari alla capacità degli archi del taglio:
$$v^* = \sum_{i\in S} \sum_{j \in \bar{S}}u_{ij}$$

#### Teorema (Grafo Residuo)
Sia $x$ un flusso ammissibile in $G$ da $s$ a $t$ e sia $G(x)$ il corrisponente grafo residuo. 
Il flusso $x$ è *massimo* se e solo se non esiste in $G(x)$ un cammino da $s$ a $t$.

#### Costi
Ha complesità $O(nmU)$ poiché:
- Ad ogni iterazione il flusso aumenta di $\delta \geq 1$ e il valore del flusso è limitato superiormente da $nU$.
- Il calcolo di un cammino aumentante ha complessità $O(m)$.

#### Taglio $s$-$t$
È una partizione dei vertici $N$ del grafo $G$ in due sottoinsiemi $S$ e $\bar{S} = N \setminus S$ tali che $s \in S$ e $t \in \bar{S}$.

La capacità di un taglio $s$-$t$ è data da:
$$
u(S, \bar{S}) = \sum_{(i,j)\in \Gamma(S, \bar{S})} u_{ij}
$$
dove $\Gamma(S, \bar{S}) = \{(i,j) \in A: i \in S, j\in \bar{S}\}$ ovvero la somma delle capacità degli archi che partono dalla partizione contenente la sorgente $s$, e arrivano nella partizione contenente la destinazione $t$.

#### Teoremi sui Tagli

**Teorema**: dato un flusso ammissibile $x$ pari a $v$, per ogni taglio $s$-$t$ $(S, \bar{S})$ si ha:
$$v = \sum_{(i,j) \in \Gamma(S, \bar{S})} x_{ij} - \sum_{(i,j) \in \Gamma(S, \bar{S})}x_{ij}$$

**Teorema**: il valore $v$ di ogni flusso ammissibile $x$ in $G$ è minore o uguale alla capacità $u(S, \bar{S})$ di un qualunque taglio $s$-$t$.

##### Max-Flow/Min-Cut
Il flusso massimo da $s$ a $t$ in $G$ è uguale alla capacità del taglio $s$-$t$ di capactià minima.