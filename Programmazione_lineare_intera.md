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
