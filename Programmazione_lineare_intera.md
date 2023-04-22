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
z_{IP} = &\min \mathbf{cx}\\
& \text{s.t.} &\mathbf{Ax} \geq \mathbf{b}\\
&& \mathbf{x} \geq 0
\end{align*}
$$

Si deduce che se la soluzione ottima $\mathbf{x}^*$ del problema LP è intera, allora è la soluzione ottima anche per il problema intero IP.

Se invece la soluzione ottima $\mathbf{x}^*$  del problema LP è frazionaria, allora una possiamo applicare il metodo **Branch and Bound**.

### Funzionamento del metodo Branch and Bound
In generale, potremmo avere diverse variabili frazionare. È necessario quindi stabilire un **criterio** per selezionare **una variabile frazionaria** per fare un branch.

Una volta selezionata la variabile $x_j$ della soluzione ottima del problema LP, si effettua un **branching** su di essa, cioè si creano due nuovi problemi dove, per esempio, uno in cui la variabile selezionata è vincolata ad essere minore o uguale ad un valore intero, e l'altro in cui la variabile è vincolata ad essere maggiore o uguale ad un valore intero, quindi:
- $P(x_j \leq \lfloor x_j \rfloor)$: ottenuto da LP aggiungendo il vincolo: $x_j \leq \lfloor x_j \rfloor$
- $P(x_j \geq \lceil x_j \rceil)$: ottenuto da LP aggiungendo il vincolo: $x_j \geq \lceil x_j \rceil$

Il processo di branching così ddescritto per il nodo radice, è ripetuto sui nodi figli, per cui la regola di branching è applicata ad ogni nodo k dell'albero di ricerca.

### Lower e Upper Bound
Per ogni nodo k dell'albero di ricerca, si calcola il valore della soluzione ottima $\mathbf{x}_k$ del problema LP, di costo $z_k$.
- Se $P_k$ **non ha soluzione ammissibile**, poniamo $z_k = +\infty$ e non generiamo nodi figli.
- Se la soluzione ottima $\mathbf{x}_k$ del problema LP è **intera**, allora $z_k$ è sicuramente un **upper bound** alla soluzione ottima del problema intero originario IP e non è necessario generare ulteriori figli, perché i nodi figli possono fornire solo una soluzione che sia $\leq$ a quella corrente.
- Se la soluzione ottima $\mathbf{x}_k$ del problema LP è **frazionaria**, allora $z_k$ è un **lower bound** al valore della *migliore* soluzione ottima *intera* che si può ottenere nel sottoalbero di cui il nodo k è radice..

Iterando questo processo, la miglior soluzione intera ammissibile finora traovata ha un costo $z_{UB}$.

In generale, l'inizializzazione di $z_{UB}$ può essere fatta con un valore arbitrariamente grande, ad esempio $z_{UB} = +\infty$ oppure generando un valore con un *algoritmo euristico*.

In generale il metodo dovrebbe migliorare la qualità dell'upperbound più velocemente possibile, in modo da limitare l'uso eccessivo di risorse per effettuare tutti i branching. Questo può essere effettuato con delle euristiche.

In generale quindi, l'upperbound ci permette di **eliminare in anticipo** quei nodi che non possono portare ad una soluzione migliore di quella che abbiamo già trovato.

Quindi se per un nodo $k$ la soluzione $P_k$ ha costo $z_k \geq z_{UP}$ allora il nodo non deve essere **esplorato**, perché non consente di ottenre una soluzione inferiore al miglior upperbound.

### Metodi di visita dell'Albero
Ad ogni esplorazione del nodo k, i nodi figli vengono inseriti in un **heap**. A questo punto, l'ordine di visita può essere:
- **Depth First**: si estrae il nodo con il costo più basso dall'heap e si esplora il suo sottoalbero. Questo metodo è molto veloce, ma non garantisce di trovare la soluzione ottima.
- **Breadth-First**: Esplora l'alberod i ricerca un livello alla volta. Questo metodo è molto lento, ma garantisce di trovare la soluzione ottima.
- **Best-First**: ad ogni iterazione estrae dalla heap il nodo con il *lower bound* più basso.

### Algoritmo Branch and Bound
L'algoritmo è il seguente:
1. Inizializza $z_{UB} = +\infty$ e inserisci nella heap vuota il problema $P_0: z_0 = \min\{\mathbf{cx}: \mathbf{Ax}\geq \mathbf{b}, \mathbf{x}\geq 0 \}$.
2. Estrai il problema $P_k$ dalla heap (STOP se è vuota), calcola la soluzione ottima $\mathbf{x}_k$ e il costo $z_k$.
3. Se $z_k \geq z_{UB}$, allora non generare nodi figli e torna al punto 2.
4. Se $\mathbf{x}_k$ è intera, allora $z_k$ è un upper bound alla soluzione ottima del problema IP, quindi aggiorna $z_{UB} = z_k$ e $\mathbf{x} = \mathbf{x}_k$. Elimina dalla heap tutti nodi $P_k$ per cui $z_k \geq z_{UB}$ e torna al punto 2.
5. Seleziona una variabile $x_j$ frazionaria nella soluzione ottima $\mathbf{x}_k$ e genera i due problemi $P(x_j \leq \lfloor x_j \rfloor)$ e $P(x_j \geq \lceil x_j \lceil)$. Torna allo step 2.

### Osservazioni e Varianti
Per ogni problema risolto $P_k$, risolta per esempio mediante il metodo del Simplesso, sarebbe utile memorizzare la base ottima $\mathbf{B}_k$ e il vettore dei costi ridotti $\mathbf{c}_B$ del problema prcedente.

L'algoritmo può essere migliorato includendo per esempio:
- Algoritmi euristici di "repair" per generare upper bound di buona qualità.
- Aggiunta di ulteriori vincoli ("**cut**") per eliminare delle soluzioni frazionarie. (**Branch and cut**).
  - I vincoli che eliminano le soluzioni frazionarie, ma non compromettono l'ammissibilità delle soluzioni intere sono detti **valid inequalities**.

## Introduzione alle Valid Inequalities
Considerando un problema di programmazione lineare intera P: $z_P = min \{\mathbf{cx}:\mathbf{Ax}\geq\mathbf{b}, \mathbf{x} \geq 0 \text{ and integer}\}$. Ipotizziamo di risolverlo mediante il metodo del simplesso, e che la variabile in corrispondenza della riga $i$ abbia un valore $\bar{b}_i$ frazionario. È possibile costruire un vincolo da aggiungere per poter  **escludere** quella soluzione frazionaria, senza però escludere le soluzioni intere.

### Tagli di Gomory
Costuiamo delle disuguaglianza note come i **tagli di Gomory**.

Consideriamo il tableau ottimo, l'equazione corrispondente alla riga $i$ è:
$$
x_i + \sum_{j=m_1}^n y^j_ix_j = \bar{b}_i
$$

Ora **decomponiamo** le quantità $y^j_j$ e $\bar{b}_i$ nelle componenti intere e frazionarie:
$$
y^j_i = I^j_i + F^j_i \quad \text{e} \quad \bar{b}_i = I_i + F_i
$$
dove:
- $I^j_i = \lfloor y_i^j\rfloor\quad$ e $\quad F_i^j = y_i^j - I^j_i \quad (0 \leq F^j_i < i)$
- $I_i = \lfloor \bar{b}_i\rfloor\quad$ e $\quad F_i = \bar{b}_i - I_i \quad (0 \leq F_i < i)$

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

Quindi, se le variaibli attualmente in base include sono $n$, il taglio di Gomory corrisponde ad una $nuova riga$ da aggiungere al tableau della forma:
$$
-\sum_{j\in N} F_i^jx_j + x_{n+1} = - F_i
$$

#### Esempio
??? non so se farlo

### Introduzione ai Metodi di Decomposizione
Quando i problemi di programmazione linaere presentano un *elevato* numero di variabili e/o vincoli, il problema potrebbe essere di difficile soluzione.

In alcuni casi la struttura della matrice dei vincoli permette di **decomporre** il problema originale in sottoproblemi di più facile risolzuione.

Esistono vari metodi che permettono di effettuare la decomposizione, tra cui la classe di metodi  di *Column Generation* (generazione dinamica delle colonne), e metodi più sofisticati come il **Rilassamento Lagrangiano**.

Tutti questa classe di metodi di decomposizione pososno essere applicati a problemi di programmazione lineare continua, intera e mista intera.

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

Per esempio, se nel problema P i vincoli si rilassano i vincoli $(16)$ usando il vettore non negativo di pensalità Lagrangiane $\mathbf{\lambda
}$, si ottiene la seguente formulazione LR:
$$
\begin{align}
    z_{LR}(\lambda) = &\min &\mathbf{cx} + &\lambda(\mathbf{b} - \mathbf{Ax})\\
    &\text{s.t.}&\mathbf{Bx} &\geq \mathbf{d}\\
    &&\mathbf{x} &\geq 0 \quad \text{and integer}\\
\end{align}
$$

Dove:
- La funzione obiettivbo ha i costi penalizzati in base ai pesi dei coefficienti della matrice $\mathbf{A}$;
- $\lambda$ è un parametro il quale fa scoraggiare le soluzioni del problema che violano il vincolo $\mathbf{b} - \mathbf{Ax} \leq 0$

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
z_P(\lambda) \leq z_{LR}(\lambda, \mathbf{x}^*) \leq z_P, \qquad \forall \lambda \geq 0.
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

Per risolvere il problema LR il metodo più e il **subgradiente**.

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

La cui soluzione ottima $\mathbf{x}^*$ pu`o essere ottenuta ponendo, per ogni $j=1,\dots,n$:
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