# Come risolvere problemi di Programmazione Lineare
Dato un sistema, composto da un funzione obbietto e da un insieme di vincoli:
$$
\begin{align*}
    & \text{max} \quad z = -x_1 - 3x_2\\
    & s.t. \\
    & \quad x_1 - 2x_2 \leq 4 \\
    & \quad -x_1 +x_2 \leq 3 \\
    & \quad x_1, x_2 \geq 0
\end{align*}
$$

si vuole calcolare la migliore soluzione che risolve la nostra funzione obbiettivo.

## Portare l'insieme dei vincoli in forma canonica

La prima cosa che si deve effettuare nella risoluzione di un problema di programmazione lineare è quello di dover portare tutte le varie disequazioni in forma di equazioni. A tal proposito per effettuare tale operazione vengono aggiunte delle *variabili di slack*.
$$
\begin{align*}
    & \text{max} \quad z = -x_1 - 3x_2\\
    & s.t. \\
    & \quad x_1 - 2x_2 + x_3 = 4 \\
    & \quad -x_1 + x_2 + x_4 = 3 \\
    & \quad x_1, x_2 \geq 0
\end{align*}
$$

## Suddividere tutti i vari componenti del sistema
Vettori del nostro sistema:
* **A**: l'insieme dei valori *x* all'interno dei vincoli, ciscuna riga della matrice A, corrisponde ad un singolo vincolo. Ogni colonna della matrice A rappresenta la variabile $x_i$ (es: nella terza colonna si fa riferimento alla variabile $x_3$).
$$
\text{A=}
\begin{bmatrix}
    \textbf{1} \quad \textbf{-2} \quad \textbf{1} \quad \textbf{0}   \\
    \textbf{-1} \quad \textbf{1} \quad \textbf{0} \quad \textbf{1}
\end{bmatrix}
$$
* **b**: Il vettore colonna b, corrisponde ai valori per i quali i vincoli devono essere soddisfatti. Ogni singolo valore di b fa riferimento ad un solo valore nei vincoli(es: il vincolo i-esimo corrisponde alla riga i-esima di b).
$$
\text{b=}
\begin{bmatrix}
    \textbf{4} \\
    \textbf{3}
\end{bmatrix}
$$
* **c**: Il vettore riga c, corrisponde ai termini noti che moltiplicano le $x$ nella funzione obbiettivo. 
$$
\text{c=}
\begin{bmatrix}
    \textbf{-1} \quad \textbf{-3}
\end{bmatrix}
$$

## Trovare una Base (B) con la quale risolvere il sistema
Spesso la base da cui partire viene evidenziata dalle colonne della nostra matrice A. Bisogna sempre scegliere 2 colonne dalla matrice A (per semplicità si possono prende4e le colonne che ci permettono di avere la matrice identità, **spesso la base ci viene fornita da input**).
$$
\text{B=}
\begin{bmatrix}
    \textbf{a3} \quad \textbf{a2}
\end{bmatrix}
$$

## Fase 1: Trovare le soluzioni base
Per trovare le soluzioni *base* del nostro problema bisogna partire dalla risoluzione di tale quazione:
$$
\text{x=}
\begin{bmatrix}
    x_b \quad x_n
\end{bmatrix}=
\begin{bmatrix}
    B^{-1} \text{b} \quad 0
\end{bmatrix}=
x_B=B^{-1}b
$$
Nel nostro caso questo equivale a risolvere:
$$
x_B=\overline b=
\begin{bmatrix}
    x_3 \\
    x_2
\end{bmatrix}=
\begin{bmatrix}
1 \quad -2 \\
0 \qquad  1
\end{bmatrix}^{-1}
\begin{bmatrix}
    4 \\
    3
\end{bmatrix}=
\begin{bmatrix}
1 \qquad 2 \\
0 \qquad 1
\end{bmatrix}
\begin{bmatrix}
    4 \\
    3
\end{bmatrix}=
\begin{bmatrix}
    10 \\
    3
\end{bmatrix}
$$
Siccome i vincoli di non negatività del sistema iniziale sono rispettati la soluzione base è ammissibile($x_3=10$ e $x_2=3$) e possiamo continuare con il nostro algoritmo.

## Fase 2: Trovare il valore della Funzione Obiettivo
Una volta trovare le soluzioni base, dobbiamo calcolare la nostra funzione obiettivo. Dobbiamo prima di tutto ottenere i termini noti nei valori di base, andando a vedere i valori nella funzione obiettivo. Nel caso in cui la variabile che abbiamo in base non sia presente nella funzione obietto originale, poiché semmai è stata scelta una variabile di *slack*, il suo valore sarà *0*.

La funzione obiettivo è pari a:
$$
z=c_Bx_B=
\begin{bmatrix}
    0, -3
\end{bmatrix}
\begin{bmatrix}
    10 \\
    3
\end{bmatrix}=-9
$$

Una volta trovata la soluzione della funzione bisogna **controllare se tale soluzione è ottima**.
## Fase 3: Controllo della soluzione
Per sapere se il valore della nostra soluzione è ottima dobbiamo verificare che: 
$$ wa_j - c_j \leq 0$$ per ogni variabile non base $x_j$, dove $w=c_bB^{-1}$
Si parte con il calcolare **w**:
$$w=c_bB^{-1}=
\begin{bmatrix}
    0, -3    
\end{bmatrix}
\begin{bmatrix}
1 \qquad 2 \\
0 \qquad 1
\end{bmatrix}=
\begin{bmatrix}
    0, -3    
\end{bmatrix}
$$
Una volta ottenuto il valore del vettore *w*, si passa a controllare se il valore della disequazione esplicata in precedenza sia effettivamente negativa. Dobbiamo quindi controllare se: 
$$
wa_4 - c_4 \leq 0 \quad \\
wa_3 - c_3 \leq 0 \quad
$$ 























### Calcolo matrice inversa
Per calcolare la matrice inversa bisogna risolvere tale matrice
$$
B^{-1}=
\begin{bmatrix}
    B \quad \vert \quad I
\end{bmatrix}
$$
Dove **$I$** rappresenta la matrcie identità. Per ottenre la matrice inversa bisogna fare in modo di portare la matrice identità nel lato sinistro della matrice B, la posizione della **$I$** deve passare da destra a sinistra, in questo modo otterremo la matrice inversa. Questo lo si fa attraverso l'impiego dell'algoritmo risolutivo *Gauss* o *Gauss-Micheal Jordan*
$$
B^{-1}=
\begin{bmatrix}
    I \quad \vert \quad B^{-1}
\end{bmatrix}
$$

