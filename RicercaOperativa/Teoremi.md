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
1. Definire una soluzione basee ammissibile $\mathbf{x = [x_B, X_N] = [B^{-1}b, 0] = [\bar{b}, 0]}$ di costo $z = \mathbf{c_Bx_B = c_BB^{-1}b}$.
2. Calcolare $\mathbf{w=c_BB^{-1}}$ e calcolare i **costi ridotti** $\mathbf{wa_j} - c_j$ per le variabile non-base $j\in N$ e determina: $$\mathbf{wa_k} - c_k = \max_{j\in N}\{\mathbf{wa_j} - c_j\}$$
3. Se $\mathbf{wa_k} - c_j < 0$ allora STOP, la **soluzione è ottima**.
4. Calcola $\mathbf{y^k = B^{-1}a_k}$; se $\mathbf{y^k} < 0$, allora STOP la soluzione è **illimitata**.
5. Calcola il valore da assegnare a $x_k$: $$x_k = \frac{\bar{b}_r}{y^k_r} = \min \left\{ \frac{\bar{b}_i}{y^k_i}: y^k_i > 0, i=1,\dots,m\right\}$$ La variabile $x_r$ esce dalla base e $x_k$ entra al posto suo. Aggiorna $\mathbf{B, N}$ e la soluzione base $\mathbf{x = [x_B, x_N] = [\bar{b}, 0]}$. Ritorna allo step 2.

## Dualità Debole (*Lemma*)
Se $\mathbf{\tilde{x}} \in X = \mathbf{\{x: Ax \geq b, x \geq 0\}}$ e $\mathbf{\tilde{w}} \in W = \{\mathbf{w: wA \leq c, w \geq 0}\}$ allora $\mathbf{\tilde{w}b \leq c\tilde{x}}$.

### Dimostrazione
Siccome $\mathbf{\tilde{x}} \in X$ allora $\mathbf{A\tilde{x} \geq b}$. Poichè $\mathbf{\tilde{w}} \leq 0$, si ha (cioè possiamo premoltiplicare per w easy senza cambiare il segno della disequazione):
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
$$\mathbf{c_BB^{-1}a_j} - c_j \leq 0, \quad j=1,\dots,n+m$$
Dove ponendo $\mathbf{w^* = c_BB^{-1}}$, equivale a:
$$\begin{align*}
    \mathbf{w^*A}&\leq \mathbf{c} \\
    \mathbf{w^*} &\leq 0
\end{align*}$$

Per cui la soluzione $\mathbf{w^*=c_BB^{-1}}$ è duale ammissibile, cioè $\mathbf{w^*}\in W$.
Infine, siccome $\mathbf{w^* = c_BB^{-1}}$ e $\mathbf{x^*=(B^{-1}b, 0)}$, si ha:
$$\mathbf{w^* b = c_BB^{-1}b = cx^*}$$
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