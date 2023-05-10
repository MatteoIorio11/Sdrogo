# Programmazione Lineare Intera
---
## Introduzione ai Metodi Branch and Bound
Consideriamo il seguente problema di programmazione lineare intera:
$$
\begin{align*}
z_{IP} = &\min \mathbf{cx}\\
& \text{s.t.} &\mathbf{Ax} \geq \mathbf{b}\\
&& \mathbf{x} \geq 0 &\text{ and integer}
\end{align*}
$$

Il **Rilassamento Lineare LP** del problema è dato da:
$$
\begin{align*}
z_{LP} = &\min \mathbf{cx}\\
& \text{s.t.} &\mathbf{Ax} \geq \mathbf{b}\\
&& \mathbf{x} \geq 0
\end{align*}
$$

Si deduce che se la soluzione ottima $\mathbf{x}^*$ del problema LP è intera, allora è la soluzione ottima anche per il problema intero IP.

Se invece la soluzione ottima $\mathbf{x}^*$  del problema LP è frazionaria, allora possiamo applicare il metodo **Branch and Bound**.

### Funzionamento del metodo Branch and Bound
In generale, potremmo avere diverse variabili frazionare. È necessario quindi stabilire un **criterio** per selezionare **una variabile frazionaria** per fare un branch.

Una volta selezionata la variabile $x_j$ della soluzione ottima del problema LP, si effettua un **branching** su di essa, cioè si creano due nuovi problemi dove, per esempio, uno in cui la variabile selezionata è vincolata ad essere minore o uguale ad un valore intero, e l'altro in cui la variabile è vincolata ad essere maggiore o uguale ad un valore intero, quindi:
- $P(x_j \leq \lfloor x_j \rfloor)$: ottenuto da LP aggiungendo il vincolo: $x_j \leq \lfloor x_j \rfloor$
- $P(x_j \geq \lceil x_j \rceil)$: ottenuto da LP aggiungendo il vincolo: $x_j \geq \lceil x_j \rceil$

Il processo di branching così descritto per il nodo radice, è ripetuto sui nodi figli, per cui la regola di branching è applicata ad ogni nodo k dell'albero di ricerca.

### Lower e Upper Bound
Per ogni nodo k dell'albero di ricerca, si calcola il valore della soluzione ottima $\mathbf{x}_k$ del problema LP, di costo $z_k$.
- Se $P_k$ **non ha soluzione ammissibile**, poniamo $z_k = +\infty$ e non generiamo nodi figli.
- Se la soluzione ottima $\mathbf{x}_k$ del problema LP è **intera**, allora $z_k$ è sicuramente un **upper bound** alla soluzione ottima del problema intero originario IP e non è necessario generare ulteriori figli, perché i nodi figli possono fornire solo una soluzione che sia $\leq$ a quella corrente.
- Se la soluzione ottima $\mathbf{x}_k$ del problema LP è **frazionaria**, allora $z_k$ è un **lower bound** al valore della *migliore* soluzione ottima *intera* che si può ottenere nel sottoalbero di cui il nodo k è radice..

Iterando questo processo, la miglior soluzione intera ammissibile finora traovata ha un costo $z_{UB}$.

In generale, l'inizializzazione di $z_{UB}$ può essere fatta con un valore arbitrariamente grande, ad esempio $z_{UB} = +\infty$ oppure generando un valore con un *algoritmo euristico*.

In generale il metodo dovrebbe migliorare la qualità dell'upperbound più velocemente possibile, in modo da limitare l'uso eccessivo di risorse per effettuare tutti i branching. Questo può essere effettuato con delle euristiche.

Riassumendo quindi, l'upperbound ci permette di **eliminare in anticipo** quei nodi che non possono portare ad una soluzione migliore di quella che abbiamo già trovato.

Quindi se per un nodo $k$ la soluzione $P_k$ ha costo $z_k \geq z_{UP}$ allora il nodo non deve essere **esplorato**, perché non consente di ottenre una soluzione inferiore al miglior upperbound.

### Metodi di visita dell'Albero
Ad ogni esplorazione del nodo k, i nodi figli vengono inseriti in un **heap**. A questo punto, l'ordine di visita può essere:
- **Depth First**: si estrae il nodo con il costo più basso dall'heap e si esplora il suo sottoalbero. Questo metodo è molto veloce, ma non garantisce di trovare la soluzione ottima.
- **Breadth-First**: Esplora l'albero di ricerca un livello alla volta. Questo metodo è molto lento, ma garantisce di trovare la soluzione ottima.
- **Best-First**: ad ogni iterazione estrae dalla heap il nodo con il *lower bound* più basso.

### Algoritmo Branch and Bound
L'algoritmo è il seguente:
1. Inizializza $z_{UB} = +\infty$ e inserisci nella heap vuota il problema $P_0: z_0 = \min\{\mathbf{cx}: \mathbf{Ax}\geq \mathbf{b}, \mathbf{x}\geq 0 \}$.
2. Estrai il problema $P_k$ dalla heap (STOP se è vuota), calcola la soluzione ottima $\mathbf{x}_k$ e il costo $z_k$.
3. Se $z_k \geq z_{UB}$, allora non generare nodi figli e torna al punto 2.
4. Se $\mathbf{x}_k$ è intera, allora $z_k$ è un upper bound alla soluzione ottima del problema IP, quindi aggiorna $z_{UB} = z_k$ e $\mathbf{x} = \mathbf{x}_k$. Elimina dalla heap tutti nodi $P_k$ per cui $z_k \geq z_{UB}$ e torna al punto 2.
5. Seleziona una variabile $x_j$ frazionaria nella soluzione ottima $\mathbf{x}_k$ e genera i due problemi $P(x_j \leq \lfloor x_j \rfloor)$ e $P(x_j \geq \lceil x_j \lceil)$. Torna allo step 2.

### Osservazioni e Varianti
Per ogni problema risolto $P_k$, risolta per esempio mediante il metodo del Simplesso, sarebbe utile memorizzare la base ottima $\mathbf{B}_k$ e il vettore dei costi ridotti $\mathbf{c}_B$ del problema precedente.

L'algoritmo può essere migliorato includendo per esempio:
- Algoritmi euristici di "repair" per generare upper bound di buona qualità.
- Aggiunta di ulteriori vincoli ("**cut**") per eliminare delle soluzioni frazionarie. (**Branch and cut**).
  - I vincoli che eliminano le soluzioni frazionarie, ma non compromettono l'ammissibilità delle soluzioni intere sono detti **valid inequalities**.

## Introduzione alle Valid Inequalities
Considerando un problema di programmazione lineare intera $P: z_P = min \{\mathbf{cx}:\mathbf{Ax}\geq\mathbf{b}, \mathbf{x} \geq 0 \text{ and integer}\}$. Ipotizziamo di risolverlo mediante il metodo del simplesso, e che la variabile in corrispondenza della riga $i$ abbia un valore $\bar{b}_i$ frazionario. È possibile costruire un vincolo da aggiungere per poter  **escludere** quella soluzione frazionaria, senza però escludere le soluzioni intere.

### Tagli di Gomory
Costruiamo delle disuguaglianza note come i **tagli di Gomory**.

Consideriamo il tableau ottimo, l'equazione corrispondente alla riga $i$ è:
$$
x_i + \sum_{j=m+1}^n y^j_ix_j = \bar{b}_i
$$
Dove indichiamo nella sommatoria tutte le variabili da $m$ a $n$ che *non* sono presenti nella base.

Ora **decomponiamo** le quantità $y^j_j$ e $\bar{b}_i$ nelle componenti intere e frazionarie:
$$
y^j_i = I^j_i + F^j_i \quad \text{e} \quad \bar{b}_i = I_i + F_i
$$
dove:
- $I^j_i = \lfloor y_i^j\rfloor\quad$ e $\quad F_i^j = y_i^j - I^j_i \quad (0 \leq F^j_i < 1)$
- $I_i = \lfloor \bar{b}_i\rfloor\quad$ e $\quad F_i = \bar{b}_i - I_i \quad (0 \leq F_i < 1)$

Perciò possiamo riscrivere l'equazione per la riga $i$ come:
$$
x_i + \sum_{j=m+1}^n (I^j_i + F^j_i)x_j = I_i + F_i
$$

$$
x_i + \sum_{j=m+1}^n I^j_ix_j - I_i = F_i - \sum_{j=m+1}^n F^j_ix_j
$$

Dove ottenimo a sinistra una quantità intera, e a destra una quantità frazionaria. Siccome il termine a sinistra è sempre intero per ogni soluzione $\mathbf{x}$, allora lo deve essere anche il termine a destra, il quale è strettamente minore di 1.

Quindi siccome:
$$F_i - \sum_{j=m+1}^n F_i^jx_j < 1$$
Ma allo stesso tempo deve essere anche intero, si ha necessariamente che:
$$
F_i - \sum_{j=m+1}^n F_i^jx_j \leq 0
$$
Che corrisponde al seguente vincolo, detto **Taglio di Gomory**:
$$
-\sum_{j=m+1}^n F_i^jx_j \leq - F_i
$$

Il quale **non** è valido per la soluzione corrente perché $x_j = 0$  per ogni $j = m+1, \dots, n$ (dato che **non sono in base**), mentre $F_i > 0$ visto che abbiamo iportizzato che $\bar{b}_i$ è frazionario.

In generale, se ipotizziamo che non abbiamo distribuito le colonne in base nelle prime $m$ colonne, ma sono sparpargliate nel tableau, il taglio di Gomory può essere espresso come:
$$
-\sum_{j\in N}^n F_i^jx_j \leq - F_i
$$
Con $N$ insieme delle colonne non in base.

Con questi risultati, possiamo capire a cosa servono.

Se risolviamo il problema con il Simplesso, quando aggiungiamo il nuovo vincolo al problema, non è necessario ripetere l'algoritmo dall'inizio, ma possiamo riaprtire dalla base corrente!

Quindi, se le variaibli attualmente in base incluse sono $n$, il **taglio di Gomory** corrisponde ad una **nuova riga** da aggiungere al tableau della forma:
$$
-\sum_{j\in N} F_i^jx_j + x_{n+1} = - F_i
$$
### Introduzione ai Metodi di Decomposizione
Quando i problemi di programmazione linaere presentano un *elevato* numero di variabili e/o vincoli, il problema potrebbe essere di difficile soluzione.

In alcuni casi la struttura della matrice dei vincoli permette di **decomporre** il problema originale in sottoproblemi di più facile risoluzione.

Esistono vari metodi che permettono di effettuare la decomposizione, tra cui la classe di metodi  di *Column Generation* (generazione dinamica delle colonne), e metodi più sofisticati come il **Rilassamento Lagrangiano**.

Tutti questa classe di metodi di decomposizione possono essere applicati a problemi di programmazione lineare continua, intera e mista intera.

Partiamo da un problema P della forma:
$$
\begin{align}
    z_p = &\min &\mathbf{c}_1\mathbf{x} + &\mathbf{c}_2\mathbf{y}\\
    &\text{s.t.}&\mathbf{Ax} + &\mathbf{By} \geq \mathbf{b}\\
    &&&(\mathbf{x}, \mathbf{y}) \in D
\end{align}
$$

Dove l'insieme dei punti ammissibili $D$ può essere definito per esempio come:
$$
D = \{(\mathbf{x}, \mathbf{y}): \mathbf{D}_1\mathbf{x} \geq \mathbf{d}_1, \mathbf{D}_2\mathbf{y}\geq \mathbf{d}_2, \mathbf{x} \geq 0,\mathbf{y} \geq 0 \quad \text{and integer}\}
$$

Oppure:

$$
D = \{(\mathbf{x}, \mathbf{y}): \mathbf{D}_1\mathbf{x} + \mathbf{D}_2\mathbf{y}\geq \mathbf{d}, \mathbf{x} \geq 0,\mathbf{y} \geq 0 \quad \text{and integer}\}
$$

Se consideriamo il primo esempio, il problema P diventa:
$$
\begin{align}
    z_p = &\min &\mathbf{c}_1\mathbf{x} + &\mathbf{c}_2\mathbf{y}\\
    &\text{s.t.}&\mathbf{Ax} + &\mathbf{By} &\geq \mathbf{b}\\
    && \mathbf{D}_1 \mathbf{x} &&\geq \mathbf{d}_1 \\ 
    &&& \mathbf{D}_2 \mathbf{y} &\geq \mathbf{d}_2 \\ 
    && \mathbf{x} &\geq 0 \\
    && \mathbf{c} &\geq 0 \quad \text{and integer}
\end{align}
$$

Se si rilassano i vincoli $(5)$ allora il problema P is decomopone in due **problemi indipendenti**, uno rispetto le variabili $\mathbf{x}$ e l'altro rispetto le variabili $\mathbf{y}$:

Però è facile notare come la soluzione $(\mathbf{x}, \mathbf{y})$ calcolata risolvendo i due problemi separatamente potrebbe **non soddifare** i vincoli $(5)$ rilassati.


Se invece consideriamo il secondo esempio, il problema P diventa:
$$
\begin{align}
    z_p = &\min &\mathbf{c}_1\mathbf{x} + &\mathbf{c}_2\mathbf{y}\\
    &\text{s.t.}&\mathbf{Ax} + &\mathbf{By} &\geq \mathbf{b}\\
    && \mathbf{D}_1 \mathbf{x} + &\mathbf{D}_2 \mathbf{y} &\geq \mathbf{d} \\ 
    && \mathbf{x} &\geq 0 \\
    && \mathbf{c} &\geq 0 \quad \text{and integer}
\end{align}
$$

Rilassando il vincolo $(11)$, il problema P **non** si decompone in due problemi indipendenti.

Nonostante ciò, potrebbe convenire perché quei vincoli rendono il problema particolarmente difficile da risolvere.

In ogni caso, la soluzione $(\mathbf{x}, \mathbf{y})$ calcolata risolvendo i due problemi separatamente potrebbe **non soddifare** i vincoli $(11)$ rilassati.

Consideriamo adesso il seguente problema P:
$$
\begin{align}
    z_p = &\min &\mathbf{cx} \\
    &\text{s.t.}&\mathbf{Ax} &\geq \mathbf{b}\\
    &&\mathbf{Bx} &\geq \mathbf{d}\\
    && \mathbf{x} &\geq 0 \quad \text{and integer}\\
\end{align}
$$
Dove consideriamo i vincoli $(16)$ come complicati.

Denotiamo con **$LP$** il rilassamento lineare del problema P, ottenuto rilassando i vincoi di integrità $(18)$, e con $z_{LP}$ il valore della sua soluzione ottima.

### Rilassamento Langrangiano
Il rilassamento Lagrangiano permette di ottenere un *lower bound* per il problema P nel seguente modo:
- alcuni vincoli considerati *difficili* sono rimosi dal problema P;
- i vincoli rimossi sono inserti nella funzione obiettivo per mezzo delle **penalità Lagrangane**.

Per esempio, se nel problema P si rilassano i vincoli $(16)$ usando il vettore non negativo di pensalità Lagrangiane $\mathbf{\lambda
}$, si ottiene la seguente formulazione LR:
$$
\begin{align}
    z_{LR}(\lambda) = &\min &\mathbf{cx} + &\lambda(\mathbf{b} - \mathbf{Ax})\\
    &\text{s.t.}&\mathbf{Bx} &\geq \mathbf{d}\\
    &&\mathbf{x} &\geq 0 \quad \text{and integer}\\
\end{align}
$$

Dove:
- La funzione obiettivbo ha i costi penalizzati in base ai pesi dei coefficienti della matrice $\mathbf{A}$ (coefficienti del vincolo rilassato);
- $\lambda$ è un parametro il quale fa scoraggiare le soluzioni del problema che violano il vincolo $\mathbf{b} - \mathbf{Ax} \leq 0$ (poichè il vincolo originario era $\mathbf{Ax} \geq \mathbf{b}$).

#### Teorema Dualità Lagrangiana Debole
$z_{LR}(\lambda)$ è un *valido lower bound* al valore della soluzione ottima di $P$.

**Dimostrazione**:

- Sia $\mathbf{x}^*$ una soluzione ottima di $P$;
- Siccome $\mathbf{x}^*$ è una soluzione ammissibile anche per $LR(\lambda), \forall \lambda \geq 0$, si ha che:

$$
z_{LR}(\lambda, \mathbf{x}^*) = \mathbf{cx}^* + \lambda(\mathbf{b} - \mathbf{Ax}^*) \geq z_P(\lambda)
$$
- Però $\lambda(\mathbf{b} - \mathbf{Ax}^*) \leq 0$, perché $\lambda > 0$ e $\mathbf{Ax}^* \geq \mathbf{b}$, quindi:

$$
z_{LR}(\lambda) \leq z_{LR}(\lambda, \mathbf{x}^*) \leq z_P, \qquad \forall \lambda \geq 0.
$$
Dove con $\lambda > 0$ penalizziamo tutte le soluzioni $\mathbf{Ax} \leq b$, ovvero non ammissibili.

---
Il sottoproblema LR è detto **problema Lagrangiano**.
Per identificare il vettore di penalità $\mathbf{\lambda}$ che massimizza il lower bound $z_{LR}(\lambda)$, si deve risolvere il cosiddetto **Lagrangiano Duale**, che può essere scritto come:
$$
z_{LR} = \max \{z_{LR}(\lambda): \lambda \geq 0\}
$$

Dove per ogni vettore di penalità fissato deve essere risolto il problema Lagrangiano LR:
$$
\begin{align}
    z_{LR}(\lambda) = &\min &(\mathbf{c} - &\lambda\mathbf{A})\mathbf{x} + \lambda \mathbf{b}\\
    &\text{s.t.}&\mathbf{Bx} &\geq \mathbf{d}\\
    &&\mathbf{x} &\geq 0 \quad \text{and integer}\\
\end{align}
$$

> Il lower bound $z_{LR}$ fornito dal Lagrangiano duale è maggiore o ugale a quello fornito dalla soluzione ottima $z_{LP}$ del rilassamento lineare del problema P, i.e. $z_{LR} \geq z_{LP}$.

Se il lower bound $z_{LR}$ è **strettamente minore della soluzione ottima** del problema P, $z_{LR} < z_P$, allora si dice che c'è **_Duality Gap_** (se è molto alto potrebbe suggerirmi di non seguire questo approccio).

Per risolvere il problema LR il metodo più swag e il **subgradiente**.

### Rilassamento Lagrangiano: Esempio
**Set covering Problem**: è il problema di *coprire* le righe di una matrice $A$ con coefficienti $a_{ij} \in \{0,1\}$ e di dimensione $m \times n$, con un sottoinsieme $S$ di colonne di *costo minimo*.

Sia $x_j$ una variabile binaria 0-1 uguale a 1 se la colonna $j$ di costo $c_j$ è in soluzione, 0 altrimenti. Un modello del problema SC è:

$$
\begin{align}
    z_{SC} = &\min &\sum_{j=1}^n c_j x_j \\
    &\text{s.t.}&\sum_{j=1}^n a_{ij} x_j &\geq 1, &\quad i = 1, \dots, m\\
    &&x_j &\in \{0,1\}, &\quad j = 1, \dots, n\\
\end{align}
$$

Il Rilassamento Lagrangiano del problema SC, rispetto ai vincoli $(26)$ è:
$$
\begin{align*}
    z_{LR}(\lambda) = &\min &\sum_{j=1}^n c_j x_j + &\sum_{i=1}^m \lambda_i (1 - \sum_{j=1}^n a_{ij} x_j)\\
    &\text{s.t.}&x_j &\in \{0,1\}, \quad j = 1, \dots, n\\
\end{align*}
$$

Dove $\lambda_i \geq 0, i = 1, \dots, m$.

Possiamo riordinare i membri della funzione obiettivo, riottenendo il problema $LR(\lambda)$ come segue:
$$
\begin{align*}
    z_{LR}(\lambda) = &\min \sum_{j=1}^n(c_j - \sum_{i=1}^m \lambda_i a_{ij})x_j +  \sum_{i=1}^m\lambda_i \\
    &\text{s.t.}\quad x_j \in \{0,1\}, \qquad j = 1, \dots, n\\
\end{align*}
$$

In questa configurazione, è possibile risolvere i problemi per ogni $j=1,\dots, n$ in modo indipendente e separato, senza violazione di alcun vincolo.

Possiamo definire quindi il costo penalizzato $c_j'$ come:
$$
c_j' = c_j - \sum_{i=1}^m \lambda_i a_{ij}, \quad j=1,\dots,n
$$
E **infine** il problema $LR(\lambda)$ diventa:
$$
\begin{align*}
    z_{LR}(\lambda) = &\min \sum_{j=1}^n c_j' x_j +  \sum_{i=1}^m\lambda_i \\
    &\text{s.t.}\quad x_j \in \{0,1\}, \qquad j = 1, \dots, n\\
\end{align*}
$$

La cui soluzione ottima $\mathbf{x}^*$ può essere ottenuta ponendo, per ogni $j=1,\dots,n$:
$$
x_j^* = \begin{cases}
1 & \text{se } c_j' \leq 0\\
0 & \text{altrimenti}
\end{cases}
$$

#### Esempio numerico
Si consideri il seguente problema di set covering:
$$
\begin{align*}
    z_{SC} = &\min          &2x_1 + &3x_2 + 4x_3 + 5x_4 \\
             &\text{s.t.}   &x_1 + &x_2 + x_3 \geq 1\\
                            &&x_1 + &x_4 \geq 1 \\
                            &&x_2 + &x_3 + x_4 \geq 1 \\
                            &&x_1,&x_2,x_3,x_4 \in \{0,1\}\\
\end{align*}
$$

La soluzione ottima di costo $5$ è $x_1 = x_2 = 1$ e $x_3 = x_4 = 0$.

Si rilassano mediante le penalità Lagrangiane $\lambda_1, \lambda_2, \lambda_3$ i vincoli di set covering.

Otteniamo il seguente problema di rilassamento Lagrangiano LR, mediante i costi penalizzati:
$$
\begin{align*}
    z_{LR}(\lambda)  = &\min&c'_1x_1 + &c'_2x_2 + c'_3x_3 + c'_4x_4 + \lambda_1 + \lambda_2 + \lambda_3\\
    &\text{s.t.}&x_1,&x_2,x_3,x_4 \in \{0,1\}\\
\end{align*}
$$

dove:
$$
\begin{align*}
    c'_1 &= 2 - \lambda_1 - \lambda_2\\
    c'_2 &= 3 - \lambda_3\\
    c'_3 &= 4 - \lambda_1 - \lambda_3\\
    c'_4 &= 5 - \lambda_2 - \lambda_3\\
\end{align*}
$$

Ora possiamo sostituire ai $\lambda_i$ valori arbitrari per calcolare al solzione ottima $\mathbf{x}^*$ del problema corrispondente $LR(\lambda)$.


## Dualità Lagrangiana Forte
**Teorema**:
Dato il problema P, sia $x'$ la soluzione ottima di $z_{LR}(\lambda')$ per un dato $\lambda' \geq 0$. Se $x'$ e $\lambda'$ soddisfano le seguenti condizioni:
* $x'$ è ammissibile per P ($Ax'\geq b)$
* $\lambda'(b-Ax')=0$

allora $x'$ è la soluzione ottima di P e $z_{LR} = z_{LR}(\lambda')$.

**Dimostrazione**:
La dimostrazione è suddivisa in:
1. Si dimostra che la soluzione $x'$ è una soluzione ottima di P;
2. Si dimostra che $z_{LR} = z_{LR}(\lambda')$.

**Dimostrazione punto 1**
Essendo $x'$ una soluzione ammisssibile di P si ha:
$$
    cx'\geq z_p
$$
Per il teorema della dualità Lagrangiana debole si ha:
$$
    z_p \geq z_{LR}(\lambda') = cx' + \lambda'(b-Ax'). \\
    \text{Rircordo che: } \lambda'(b-Ax').
$$
Per cui si ottiene: 
$$
cx' \geq z_p \geq cx' \rightarrow z_p = cx' (=z_{LR}(\lambda'))
$$
**Dimostrazione punto 2**
Dalla definizione di Lagrangiano Duale $z_{LR}$ si ha:
$$
z_{LR} \geq z_{LR}(\lambda')
$$
Mentre, dalla dualità Lagrangiana debole si ha:
$$
z_{p} \geq z_{LR}
$$
Si ottiene:
$$
z_p=z_{LR}(\lambda')
$$
## Rilassamento Lineare vs Rilassamento Lagrangiano
Per comodita il problema: 
$$
\begin{align}
    z_p = &\min &\mathbf{cx} \\
    &\text{s.t.}&\mathbf{Ax} &\geq \mathbf{b}\\
    &&\mathbf{Bx} &\geq \mathbf{d}\\
    && \mathbf{x} &\geq 0 \quad \text{and integer}\\
\end{align}
$$
Questo può essere riscritto come: 
$$
\begin{align}
    z_p = &\min &\mathbf{cx} \\
    &\text{s.t.}&\mathbf{Ax} \geq \mathbf{b}\\
    && \mathbf{x} \in X\\
    &&X = &\{x:Bx \geq d, x \geq 0 \text{ and integer}\}\\
\end{align}
$$
Il rilassamento del problema è ottenuto rilassando il vincolo di interezza in $X$. Si ricorda che il valore ottimo del problema $z_{LP}$ del rilassamento lineare di P è un valido *lower bound* al valore $z_p$ della soluzione ottima di P, $z_{LP} \leq z_p$. Si denota con **conv(X)** l'inviluppo convesso di *X*, che è dato dall'intersezione di tutti gli insieme convessi che contengono *X*. L'insieme convesso è un poligono al cui interno e lungo i suoi bordi vi sono un insieme di valori interi.
### Teorema Caratterizzazione del Lagrangiano Duale
**Teorema (Caratterizzazione del Lagrangiano Duale)**
$z_p = min{cx: Ax \geq b, x \in conv(X)}$, se si rilassano in modo *Lagrangiano* i vincoli $Ax \geq b$, il costo della soluzione ottima $z_{LR}$ del *Lagrangiano Duale* è uguale al costo della soluzione ottima del seguente problema di programmazione lineare:
$$
\begin{align}
    z_p = &\min &\mathbf{cx} \\
    &\text{s.t.}&\mathbf{Ax} &\geq \mathbf{b}\\
    && \mathbf{x} \in conv(X)\\
\end{align}
$$
*Ricordo* che **conv(X)** è l'insieme in cui contenuti tutti i valori interi. 
**Dimostrazione**
$$z_{LR}=\max\{z_{LR}(\lambda:\lambda \geq 0\} = \max_{\lambda \geq 0}\{\min_{x \in X}\{cx + \lambda(b-Ax)\}\}$$
Se **T** è l'insieme dei punti estremi del poliedro $X$ allora:
$z_{LR}=max_{\lambda \geq 0}\{min_{t \in T}\{cx^t + \lambda(b - Ax^t)\}\}$, si traduce nell'attraversare tutti i punti estremi del poliedro convesso in modo da trovare il valore migliore per la nostra *funzione obiettivo*, che equivale al seguente problema:
$$
\begin{align}
    z_{LR} = &\max &\mathbf{z} \\
    &\text{s.t.}&\mathbf{z} &\leq \mathbf{cx^t} + \lambda(b - Ax^t), t \in T\\
    && \mathbf{\lambda} \geq 0\\
\end{align}
$$
Ne ricavo il problema duale *(39)-(41)*:
$$
\begin{align}
    z_{LR} = &\max \sum_{t \in T}  &\mathbf{cx^t}\alpha_{t} \\
    &\text{s.t.}& \sum_{t \in T}  &\mathbf{b-Ax^t}\alpha_{t} \leq 0\\
    &&  \sum_{t \in T}  &\mathbf{\lambda_{t}} = 1 \\
    & \lambda_{t} \geq 0, && t \in T
\end{align}
$$
**Dimostrazione**
Definendo $x=\sum_{t \in T} x^t \alpha_{t}$ dal problema *(42)-(45)* si ottiene:
$$
\begin{align}
    z_{LR} = &\max &\mathbf{cx} \\
    &\text{s.t.}& &\mathbf{Ax} \geq 0\\
    & x \in conv(X)
\end{align}
$$
### Teorema Relazione tra Rilassamento Lagrangiano e LP
**Teorema (Relazione tra Rilassamento Lagrangiano e LP)**
Il *lower bound* ottenuto dal rilassamento Lagrangiano del problema P è **sempre maggiore o uguale** del *lower bound* ottenuto dal Rilassamento lineare di P, $z_{LP} \leq z_{LR}$.

**Dimostrazione**
Siccome $conv(X) \subseteq \{x: Bx \geq d, x \geq 0 \}$, l'insieme delle soluzioni *Lagrangiano Duale* dato da $\{x:Ax \geq b, x \in conv(X) \}$ è contenuto nell'insieme delle soluzioni di *LP* dato a $\{x:Ax \geq b, Bx \geq d, x \geq 0 \}$:

$$\{x:Ax \geq b, x \in conv(X)\} \subseteq \{x: Ax \geq b, Bx \geq d, x \geq 0 \}$$

da cui segue che $z_{LP} \leq z_{LR}$.
### Teorema
**Teorema**
Si hanno le seguenti proprietà:
* $z_p = z_{LR}$ se e solo se:
$$
\begin{align}
    conv(X \cap \{x:Ax \geq b, x \geq 0 \}) \\
    & = 
    &conv(X) \cap conv(\{x: Ax \geq b, x \geq 0 \});  \\
\end{align}
$$
* $z_{LP} = z_{LR}$ se (*Proprietà di Integralità*):
$$
\begin{align}
    & conv(X) \cap conv(\{x: Bx \geq d, x \geq 0 \});  \\
\end{align}
$$
Equivalente all'inviluppo convesso in cui ho rilassato il vincolo di interezza.

## Metodo del Subgradiente
Il *Lagrangiano Duale* può essere risolto come problema di programmazione lineare. Per risolvere il lagrangiano duale si possono usare dei *metodi euristici*, come il **metodo del Subgradiente**. 
### Definizione Subgradiente
**Teorema**:
La funzione *lagrangiana* $z_{LR}(\lambda') = cx' + \lambda'(b-Ax')$ è concava, di conseguenza derivabile potendo trovare un *massimo*.
**Dimostrazione**:
Siano $\lambda_1, \lambda_1 \geq 0$ e $\lambda'$ *una combinazione convessa* di $\lambda_1$ e $\lambda_2$, ovvero $\lambda' = \alpha \lambda_1 + (1 - \alpha)\lambda_2$ con $\alpha \in [0, 1]$. Sia $x'$ la soluzione ottima di $LR(\lambda')$:
$$
\begin{align}
    z_{LR}(\lambda') = &\mathbf{cx' + \lambda'(b - Ax')} \\
\end{align}
$$
$x'$ *è una soluzione ammissibile di* $LR(\lambda_1)$ e $LR(\lambda_2)$, quindi:
$$
\begin{align}
    z_{LR}(\lambda_1) \leq &\mathbf{cx' + \lambda_1(b - Ax')} \\
    z_{LR}(\lambda_2) \leq &\mathbf{cx' + \lambda_2(b - Ax')} \\
\end{align}
$$
da cui si ottiene: 
$\alpha z_{LR}(\lambda_1) + (1-\alpha)z_{LR}(\lambda_2) \leq cx' + (\alpha \lambda_1 + (1 - \alpha)\lambda_2)(b - Ax') = z_{LR}(\lambda')$
$(\alpha \lambda_1 + (1 - \alpha)\lambda_2) = \lambda'$
## Subgradiente
Un vettore *s* è dettp *subgradiente* della funzione $f(\lambda)$ nel punto $\lambda'$ se soddisfa la seguente condizione:
$$
\begin{align}
    f(\lambda) \leq &\mathbf{f(\lambda') + s(\lambda - \lambda')} \\
\end{align}
$$
In modo da trovare una retta che rimane sempre sotto.
Si vuole definire il subgradiente della funzione Lagrangiana:
$$
\begin{align}
    z_{LR}(\lambda') = &\mathbf{cx' + \lambda'(b - Ax')} \\
\end{align}
$$
Per ogni $\lambda \geq 0$ si ha che: 
$$
\begin{align}
    z_{LR}(\lambda) \leq &\mathbf{cx' + \lambda(b - Ax')} \\
\end{align}
$$
Sottraendo l'equazione e la disequazione precedente si ottiene:
$$
\begin{align}
    z_{LR}(\lambda) - z_{LR}(\lambda') \leq &\mathbf{(\lambda - \lambda')(b - Ax')} \\
\end{align}
$$
oppure
$$
\begin{align}
    z_{LR}(\lambda) \leq  &\mathbf{z_{LR}(\lambda') + (\lambda - \lambda')(b - Ax')} \\
\end{align}
$$
Per cui $s = (b - Ax')$ è un subgradiente della funzione Lagrangiana $z_{LR}(\lambda)$ calcolata nel punto $\lambda'$. 
Affinché $z_{LR}(\lambda)$ sia maggiore di $z_{LR}(\lambda')$ è necessario muoversi nella direzione del sub gradiente:
$$
\begin{align}
    \lambda = &\mathbf{\lambda' + \theta \textbf{s}} \\
\end{align}
$$
dove $\theta$ è lo spostamento lungo il subgradiente, come si traduce questa cosa? 
1. Prima di tutto bisogna scegliere il $\lambda$ iniziale, semplicemente si può partire con 0
2. Una volta che si è calcolato il $z_{LR}(\lambda')$ si controlla se la soluzione sia ottima, in che modo lo so? Se $\lambda(b-Ax')=0$, ricordo che in questo modo si ottiene sempre un upper bound del nostro problema
3. Se vogliamo continuare ad iterare con questo algoritmo troverò il nuovo lambda semplicemente calcolando la formula precedente
4. Torno al punto 2.
### Calcolare lo spostamento
* Modo esatto
$$
\begin{align}
    \theta = \text{argmax} &\mathbf{ \{z_{LR}(\lambda' + \theta s): \theta \ge 0 \} } \\
\end{align}
$$
* Ad ogni iterazione *k* del subgradiente dello spostamento $\theta^{k}$ può essere calcolato con uno dei seguenti approcci euristici:
$$
\begin{align}
    \theta^{k} = \beta^{k} &\mathbf{\frac{z - z_{LR}(\lambda^{k})}{||s^{k}||_2^2}} \\
\end{align}
$$
Il valore nel denominatore mi permette di capire quanto veloce mi muovo verso l'ottimo, mentre $z$ è una semplice stima per difetto del lagrangiano duale. Ricordo che $s$ è il subgradiente. Se $0 \ge \beta^{k} \leq 2$ la convergenza di $z_{LR}(\lambda^k)$ a $z_{LR}$ è garantita, in alternativa si può usare: 
$$
\begin{align}
    \theta^{k} = \beta^{k} &\mathbf{\frac{0.01 \times z_{LR}(\lambda^{k})}{||s^{k}||_2^2}} \\
\end{align}
$$
Il parametro $\beta^{k}$ può essere diminuito se dopo in certo numero di iterazioni $z_{LR}(\lambda^k)$ a $z_{LR}$ non è migliorato.
Quando la penalità Lagrangiana $\lambda_i$ è aggiornata si deve tenere conto di eventuali vincoli sul segno siccome calcolo dal duale la nostra lambda:
* $a_i x = b_i$: La penalità $\lambda_i$ può essere qualsiasi,
$$
\begin{align}
    \lambda_i^{k+1} = &\mathbf{\lambda_i^{k} + \theta^{k}s_i} \\
\end{align}
$$
* $a_i x \geq b_i$: la penalità $\lambda_i$ deve essere non negativa, prendo una penalità se il valore è positivo,
$$
\begin{align}
    \lambda_i^{k+1} = &\mathbf{max{0, \lambda_i^{k} + \theta^{k}s_i}} \\
\end{align}
$$
* $a_i x \leq b_i$: la penalità $\lambda_i$ deve essere non positiva, prendo una penalità se il valore è negativo,
$$
\begin{align}
    \lambda_i^{k+1} = &\mathbf{min{0, \lambda_i^{k} + \theta^{k}s_i}} \\
\end{align}
$$
## Algoritmo del Subgradiente
- **Step 1**. Sia $z_p = \min\{cx:Ax \geq b, x \in X\}$, dove $A \in \R^{mn}$, $c \in \R^{n}$ e $b \in \R^{m}$. Poniamo $z_{LB}=-\infty$, $z_{UB}=+\infty$ e $\lambda=0$.
- **Step 2**. Risolvi il problema Lagrangiano:
$$z_{LR}(\lambda) = (c - \lambda A)x' + \lambda b = \min\{(c - \lambda A)x + \lambda b : x \in X \}$$
e aggiorna il lower bound $z_{LB} = \max\{z_{LB}, z_{LR}(\lambda)\}$. 
- **Step 3**. Se $x'$ è ammissibile $z_{UB} = \min\{z_{LB}, z_{LR}(\lambda)\}$ e se ottima STOP, ottima quando $\lambda (b - Ax) = 0$
- **Step 4.** Aggiorna le penalità Lagrangiane: 
$$ \lambda_i = max\{0, \lambda + \theta s_i\}, \quad i = 1, ..., m, $$
dove $s_i = b_i - a_i x'$ e vai allo step 2.
## Euristica Lagrangiana
* **Step 1**. Calcola una soluzione euristica del problema P e inizializza il subgradiente;
* **Step 2**. Calcola $z_{LR}(\lambda)$ ottenendo la soluzione **x**;
* **Step 3**. Verifica l'ammissibilitò della soluzione **x**;
* **Step 4**. Costruisci una soluzione ammissibile per il problema P utilizzando **x** e/o $\lambda$;
* **Step 5**. Se si verificano le condizioni di arresto allosta STOP;
* **Step 6**. Aggiorna le penalità Lagrangiane $\lambda$ e vai allo Step 2.
## Generazione di Colonne
### Introduzione
I metodi di generazione di colonne risolvono il problema senza considerare esplicitamejte tutte le variabili. Si definine un *core* iniziale dopodiché si aggiungono dinamicamente le variabili mancanti "necessarie" durante il processo di soluzione. Dato il seguente problema: 
$$
\begin{align}
    z_p = \min cx \\
    s.t & Ax = b \\
    & x \geq 0
\end{align}
$$
Il problema duale è il seguente: 
$$
\begin{align}
    z_D = \max wb \\
    s.t & wA \leq c \\
\end{align}
$$
Il simplesso primale esegue iterativamente le seguente operazioni:
* Selezione di una colonna *s* di A
* Selezione di una riga *r* di A
* Esecuzione di un'operazione di pivoting sull'elemento pivot $a_{rs}$
Data una base *B* di *A*, la corrispondente soluzione base può essere migliorata se esiste una colonna *h* tale che $c_{h}' \ge 0$ dove: 
$
\mathbf{c_{h}' = \max\{c_{j}' = wa_j - c_j : j=1,....n\} \le 0}
$
detto anche **problema di pricing**.
Ad ogni iterazione è necessario determinare se esiste una colonna $a_h$ di costo $c_h$ tale che $c_{h}' = \max\{c_{j}' = wa_{j} - c_j : j=1,...,n\} \le 0 $. 
In alcuni casi la struttura del problema di pricing, (quello precedente) è tale da consentire la soluzione senza considerare tutte le variabili. Il metodo della *generazione di colonne* perché nella soluzione del problema di pricing, le variabili (colonne) del problema vengono generate solo quando servono, individuo la colonna migliore che massimizza il mio problema.
### Algoritmo Column Generation
* Step 1. Definisci una base ammissibile iniziale *B*; 
* Step 2. Calcola la soluzione base corrispondente a *B*,
$ x = (x_B, 0) = (B^{-1}b, 0)$ corrisponde all'ultima colonna del tableau dove ho tutte le *b*
* Step 3. Risolvi il *problema di pricing*, generando le variabili *h* di costo ridotto $c_{h}' = wa_h - c_h$ massimo;
* Step 4. Se il costo ridotto $c_h' \leq 0$ allora STOP: la soluzione *x* è ottima e non è necessario generare altre colonne; altrimenti calcola la nuova base *B* e vai allo *Step 2*. 