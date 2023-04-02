# Regressione Lineare

## Predire Variabili Continue
La Regressione Lineare stima da un dataset una funzione lineare tale per cui:
- Associ a variabili di input (**Domini**) ad una variabile di output (**Co-Dominio**).
- Con una sola variabile indipendente (var. nel dominio) si parla di regressione *univariata*.
- Con più variabili indipendenti si parla di regresione *multivariata*.

Esistono varie forme di regressione le quali possono estrearre funzioni con andamenti diversi (polinomiali, logaritimiche, ...).

### Regressione lineare Univariata
Consideriamo un insieme di osservazioni indpendenti $x$, le quali portano ad un valore dipendente da esse $y$. Considerando il modello come un modello lineare, la generica formula di una retta che possa interpolare al meglio i punti delle osservazioni $x$ è data dalla consueta formula:
$$y = \alpha x + \beta$$

Tramite la regressione lineare, è possibile stimare una variabile dipendente $\hat{y}$ sulla base di un'unica variabile indipendente $x$. La variabile $\hat{y}$ sarà quindi il valore **predetto** della variabile dipendente, sulla base dei risultati ottenuti dalle altre $y$. $\alpha$ e $\beta$ rappresentano rispettivamente il coefficiente angolare e intercetta della retta nel piano.

Praticamente parlando:
- $\hat{y}$ è una stima sul valore effettivo di $y$.
- $\alpha$ indica quanto varia $y$ al variare di $x$.
- $\beta$ determina il valore base di $y$ quando $x$ è nullo.

Risulta quindi che il compito della regressione lineare è stimare $\alpha$ e $\beta$ in modo tale rendere la stima di $\hat{y}$ più accurata possibile.

#### Misura dell'errore Medio
Se scegliamo arbitrariamente valori di $\alpha$ e $\beta$ ammissibili, otteniamo un errore medio rispetto al valore attuale reale pari a:
$$\text{errore} = \frac{1}{m} \sum_{i=1}^m(\hat{y}_i - y_i)^2$$
Ovvero la media dei quadrati dei singoli errori.

Il nostro obiettivo è quello di trovare l'errore minimo possibile, quindi agiamo in questo modo:
- Fissato un set di dati, l'errore è calcolato come una funzione continua sui paramentri del modello di predizione.
- Denotiamo con $\Theta$ la combinazione di valori dei **parametri incogniti** e con $h_{\theta}$ il **modello** prescelto che li utilizza

Scriviamo:
$$E(\Theta) = \frac{1}{m} \sum_{i=1}^m(h_\theta(x_i) - y_i)^2$$

Nel nostro caso di regressione lineare univariata, la funzione è incognita nei sui parametri $\alpha$ e $\beta$:


$$E(\alpha, \beta) = \frac{1}{m} \sum_{i=1}^m(\alpha x_i + \beta - y_i)^2$$

#### Minimizzazione dell'errore: Discesa del Gradiente
Essendo una funzione in due variaibli, l'errore è rappresentato da un paraboloide: qusto ci fa comprendere che esiste un minimo, e inoltre è anche minimo globale (non so bene la dimostrazione esatta ma mi fido).

Perciò è semplice come bere un bicchiere di cianuro calcolare il minimo, tramite il grande gradiente. Quest'ultimo ci da una misura di dove e di quanto la funzione converge verso il minimo globale: seguendo quindi la direzione del vettore disegnato dal gradiente, raggiungeremo prima o poi il minimo globale della funzione dell'errore!

Possiamo riassumere gli step della cosidetta **discesa del gradiente** come segue:
1. Si parte da un punto $x_k = x_0$ a casio.
2. Si valuta la funzione $f$ e il suo gradiente $\nabla f$ nel punto $x_k$.
3. Ad $x_k$ si sottrae un vettore proporzionale al gradiente, per ottenere un punto $x_{k+1}$ con $f(x_{k+1}) < f(x_k)$.
4. $k\texttt{++}$ e ritornare al punto 2 fino alla **convergenza ad un minimo**.

Matematicamente parlando, la discesa del gradiente è rappresentata dalla formula:
$$\textbf{x}_{k+1} = \textbf{x}_k - \eta \cdot \nabla f(\textbf{x}_k)$$
Dove la grandissima $\eta$ ([:eta]) è la **step size**, ovvero un iperparamentro fondamentale per l'apprendimento nelle reti neurali, infatti è anche noto in queste ultime come **learning rate**. Non sempre è costante per l'intera discesa, in alcune declinazioni varia in base a dove ci si trova nell'algoritmo.

#### Discesa del Gradiente nella Regressione Univariata
Dobbiamo calcolare:
$$\nabla E(\alpha, \beta) = 
\left( 
    \frac{\partial E}{ \partial \alpha},
    \frac{\partial E}{ \partial \beta} 
\right)=
\left(
    \frac{1}{m} \sum_{i=1}^m2(\alpha x_i + \beta - y_i) x_i \quad, \quad
    \frac{1}{m} \sum_{i=1}^m2(\alpha x_i + \beta - y_i)
\right)
$$

ottenendo la formula per la discesa del gradiente:
$$
\begin{cases}
    \alpha_{k+1} \leftarrow \alpha_k - \frac{2\eta}{m}\sum_{i=1}^m (\alpha_kx_i + \beta_k + y_i)x_i \\
    \beta_{k+1} \leftarrow \beta- \frac{2\eta}{m}\sum_{i=1}^m (\alpha + \beta_k + y_i)
\end{cases}
$$

Iterando questo procedimento, arrivamo ad avere due parametri $\alpha$ e $\beta$  in grado di poter costruire una retta che possa stimare i nuovi valori $\hat{y}$ dati nuovi valori $x$.

### Regresione Lineare Multivariata
In questo caso, si stima la variabile dipendente $y$ sulla base di più variabili indipendenti $x_1, \dots, x_n$.
Il nostro modello quindi assumerà la forma:
$$h_\theta(x_1,\dots, x_n) = \theta_0 + \theta_1x_1, \dots \theta_n x_n$$
(occhio alla notazione, qui sopra le $\theta$ sono miniuscole, la theta maiuscola è $\Theta$ e denota il **vettore** dei parametri incogniti).

Dove 
- Ogni coefficiente angolare $\theta_i$ denota il "peso" della variabile $x_i$ nella previsione.
- L'intercetta è rapprensetata dal valore di $\theta_0$, ovvero quando $x=0$.

N.B. Le variabili categoriche in questo tipo di modelli vengono "Binarizzate" (**One Hot Encoding**) ovvero vengono mappate nell'insieme $\{0,1\}$.

Se per esempio stiamo considerando la vendita di appartamenti in base ai parametri:
- $s$: metri quadri
- $n_b$: stanze da letto
- $q$: quartiere $\in \{0,1\}$

Otteniamo la funzione di prezzo $P$ pari a:
$$P(n_b, s, q) = \theta_0 + \theta_1 n_b + \theta_2 s + \sum_{i\in q} \theta_i \delta(q)$$
Dove la funzione $\delta(q)$ rappresenta il one hot encoding della categoria q per l'instanza i-esima considerata.

Considerando il **modello generale** per la regressione lineare multivariata  $h_\theta(x_1,\dots, x_n) = \theta_0 + \theta_1x_1, \dots \theta_n x_n$, possiamo riscriverlo in forma matriciale, considerando che poniamo $x_0 = 0$ per compattezza di notazione:
$$h_\theta(\textbf{x}) = \Theta\textbf{x}$$

#### Stima dell'errore
Se prendiamo la formula citata per la regressione univariata per l'errore:
$$E(\Theta) = \frac{1}{m} \sum_{i=1}^m(h_\theta(x_i) - y_i)^2$$

Dove si ricorda che:
- $m$ è il numero di dati.
- $x$ è la variabile indipendente.
- $y$ è la variabile dipendente.

Nel modello multivariato a $n$ dimensioni otteniamo:
$$E(\theta_0, \theta_1, \dots, \theta_n) = \frac{1}{m}\sum_{i=1}^m
\left(
    \theta_0 + \sum_{j=1}^n (\theta_j \cdot x_{ij}) - y_i
\right)^2$$

Dove nella sommatoria più interna, $x_{ij}$ indica la **feature** j-esima, nell'**istanza** i-esima.
Come sempre, il tutto può essere semplificato con la notazione matriciale:
$$E(\Theta) = \frac{1}{m}\sum_{i=1}^m(\Theta \textbf{x}_i - y_i)^2$$

#### Discesa del gradiente Multivariata
Non cambia molto, bisogna come sempre calcoalre il gradiente, ma in questo caso è un pelo più complesso avendo $n$ features. (piccola nota, $p=1,\dots, n$)
$$\nabla E(\Theta) = \frac{\partial E(\Theta)}{\partial \theta_p} 
= \frac{2}{m}\left(
    \sum_{i=1}^m \theta_0 + \sum_{j=1}^n(\theta_0 \cdot x_{ij} - y_i)x_{ip}
\right)$$

Potendo così facilemte ricavare la formula iterativa per la discesa del gradiente per ciascuna feature $\theta_p$:
$$\theta_{p,k+1} \leftarrow \theta_{p, k} - \frac{2\eta}{m}
\left(
    \sum_{i=1}^m \theta_{0, k} + \sum_{j=1}^n(\theta_{j, k} \cdot x_{ij}) - y_i
\right)x_{ip}$$

##### Momento speculazione matematica di cui non ne conosco il significato
Finora abbiamo rappresentato ciascuna delle $m$ osservazioni su cui calcolare l'errore con un vettore $\textbf{x}_i$ e un valore atteso $y_i$.

L'intero insieme delle osservazione può essere raccolto in una matrice $\textbf{X}$ degli input e un vettore $\textbf{y}$ degli output. In particolare;
- $\textbf{X}$ ha una riga per ogni osservazione (o istanza) e un acolonna per ogni variabile (o feature), più una colonna relativa all'intercetta con tutti valori a uno.
- $\textbf{y}$ ha un elemento per ogni osservazione (corrispondenti alle righe).

In questo modo possiamo scrivere il gradiente non più in termini di singole derivate parziali, ma in forma vettoriale:
$$\nabla E(\Theta) = \frac{2}{m} \textbf{X}^T(\textbf{X}\Theta - \textbf{y})$$

Non so come sia cicciata fuori la trasposta.

Perciò si può scrivere la discesa del gradiente come:
$$
\Theta_{k+1} =
\Theta_k - 
\frac{2\eta}{m}
\textbf{X}^T(\textbf{X}\Theta_k - \textbf{y})$$

Ed eccoci qua, senza aver capito nulla. Buonanotte.