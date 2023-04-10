# Regressione non Lineare

## Definizione
È una generalizzazione dela [Regressione Lineare](./Regressione_Lineare.md), con i termini noti di grado superiore. Essa è impiegata per ottenere modelli capaci di **descrivere dataset più complessi**.

Per quanto aumenti il grado dei termini noti ($\textbf{x}$), la regressione polinomiale è ancora lineare rispetto ai parametri $\theta$. Perciò la funzione d'errore è definita in uno spazio a maggiori dimensioni $\theta$, ma l'**algoritmo** di regressione rimane il medesimo.

### Uso tramite `scikit-learn`
Tramite `scikit-learn` è possiible cambiare l'insieme delle feature per l'elaborazione dei dati. In partiolcare, il package di **preprocessing** offre API comuni in grado di creare l'oggetto che definisce una *trasformazione* da applicare, e poterla applicare su insieme di dati.

Per quanto riguarda la Regressione Polinomiale, la classe `PolynomialFeatures` aggiunge alle variabili di grado 1 tutte quelle fino al grado N specificato tramite:
```python
from sklearn.preprocessing import PolynomialFeatures
poly = fit_transform(degree-2) # trasformazione di secodno grado
```

Per poter "far apprendere" la struttura dei dati, possiamo ora dare in pasto all'oggetto di trasformazione `poly` un matrice del tipo:
```python
poly.fit_trasnform([[2, 10], [-3, 20]])
```
Ottenendo così un nuovo set di dati di grado due tale per cui:

| $1$ | $a$ | $b$ | $a^2$ | $a\cdot b$ | $b^2$ |
|-----|-----|----|----|----------------|-------|
| 1 | 2 | 10 | 4 | 20 | 100 |
| 1 | -3 | 20 | 9 | -60 | 400 |


Dove il termine di grado 0 risulta ridondante poiché rappresenta l'intercetta, ed è escludibile con il flag `include_bias=false` nella dichiarazione dell'oggetto di trasformazione.

```python
poly = fit_transform(degree-2, include_bias=false)
```

Possiamo ora **eseguire** la regressione polinomiale
```python
from sklearn.linear_model import LinearRegression

poly = PolynomialFeatures(degree=2, include_bias=False)

prm = LinearRegression()

# training con il modello di secondo grado
prm.fit(poly.fit_transform(X_train), Y_train)

# Per utilizzare il modello, convertiamo sempre i dati in input
# come abbiamo fatto per i dati di training
prm.predict(poly.transform(30))
# array([2.2923595])
prm.score(poly.transform(X_val), Y_val)
# 0.0000000000000000000001
```

#### Pipeline
Una pipeline incapsula una o più trasformazioni e un modello, permettendo di interagire con essi come un'entità unica, senza dover ogni volta specificare la sequenza di trasformazioni atte a introdurre/ricavare dati a/da un modello.

L'oggetto `Pipeline` offre le stesse API di un modello "semplice", quindi i metodi `fit, predict, score` sono chiamabili, dove però ad ogni chiamata di queste funzioni vengon applicate le trasformazioni che sono contenute all'interno della pipeline.
Quindi, per esempio, tramite:
```python
from sklearn.pipeline import Pipeline
prm = Pipeline ([
    ("poly", PolynomialFeatures(degree=2, include_bias=False)),
    ("linreg", LinearRegression())
])
```
Otteniamo esattamente le trasformazioni che abbiamo effettuato negli esempi precedenti. A questo punto possiamo tranquillamente fare:

```python
prm.fit(X_train, Y_train)
prm.predict(30)
prm.score(X_val, Y_val)
```
e tutte le trasformazioni sono attuate tranquillamente senza che noi dobbiamo preoccuaprci di strippare facendo conversioni.

## Overfitting
All'aumentare della complessità (grado) del modello di learning, si riduce l'errore.
Esiste però una certa soglia che, superata, l'errore sul validation set torna a crescere. Questa è la soglia di **overfitting**, che indica che la maggior complessità del modello descrive meglio il training set, ma non il validation set, ovvero che **il modello ha perso di generalità**.

Al contrario, l'**underfitting** avviene quando il modello è troppo semplice e quindi inadeguato a rappresentare i dati.

È importante notare che la **quantità dei dati** e **complessità** del modello sono **interdipendenti**. In casi quindi che i dati siano troppi pochi, è possibile generare dati casuali che seguano la distribuzione dei pochi dati a disposizione, per ribilanciare il dati di apprendimento e validazione.

### Training Set, Validation Set e Iperparametri
Nei casi più semplici, i dati vengono suddivisi casualemente, tipicamente con una distribuzione 70-30 tra training e validation set. 

- Dal **training set** si determinano i paramentri $\Theta$ del modello di learning
- Dall'**holdout (validation set)** vengono scelti tutti gli **iperparametri**.
  - e.g. tipo di funzione di regressione, grado, normalizzazione, regolarizzazione, learning rate, ...

#### K-Fold Cross Validation
- Si suddividono i dati in $k$ sottoinsiemi disgiunti
- Un sottoinsieme è usato come validation set e gli altri $k-1$ sono usati come training set.
- Si ripete il procedimento $k$ volte per ciascuno dei $k$ sottoinsiemi


Si ottengono così $k$ **modelli** di learning, e l'**accuratezza** è calcolata come la media delle accuratezze dei $k$ modelli.

È possibile piccola variante chiamata **k-Fold cross validation stratificata** dove per ogni fold, i dati hanno stessa distribuzione e stesse caratteristiche.

### Regolarizzazione
Come detto prima, all'aumento del grado, aumenta l'errore nell'holdout, ma parallelamente cresce rapidamente il valore assoluto dei coefficienti $\Theta$!

### Ridge Regression
Aumentando infinitamente il grado della regressione polinomiale, possiamo modellare qualsiasi dataset, ma i coefficienti $\Theta$ diventano molto grandi, provocando forti oscillazioni nella regressione, **peggiorandone** l'accuratezza.

È possibile **regolarizzare** i coefficienti, ovvero ridurre il loro valore, aggiungendo alla funzione d'errore da minimizzare anche un paramentro $\lambda$, tale per cui:
- $\lambda \geq 0$ con $\lambda = 0$ nessuna regolarizzazione.

La funzione da minimazzare diventa quindi una cosa del tipo:

$$
\min_\theta \sum_{i=1}^m(\theta^Tx^{(i)} - y^{(i)})^2 + \lambda \lVert \theta\rVert^2_2
$$

Dove:
- $$\lVert \theta_2^2\rVert = \sum_{i=0}^{n-1}\theta^2_i$$
con $n =$ numero di parametri $\theta$.


Si capisce quindi che più $\lambda$ è alto, più i $\theta$ diventeranno piccoli in valore assoluto.

Per poter minimizzare, come sempre calcoliamo il gradiente di questa nuova funzione:
$$
\nabla_\theta(\sum_{i=1}^m(\theta^Tx^{(i)} - y^{(i)})^2 + \lambda \lVert \theta\rVert^2_2) = 2X^T(X\theta - y) + 2\lambda\theta $$

E troviamo il minimo ponendo il gradiente uguale a zero:
$$
2X^TX\theta+2\lambda\theta = 2X^Ty \implies \theta = (X^TX + \lambda I)^{-1}X^Ty
$$

Dove il termine $(X^TX + \lambda I)^{-1}$ richiede una marea di risorse.

Tramite un analisi geometrica, è possibile notare come esista un valore $\theta_{\text{opt}}$ il quale **minimizza** la funzione di errore. In paricolare, per semplicità, se considerassimo il caso in cui una regressione con parametri $\theta$ sia della forma $\hat{y} = \theta_0 + \theta_1 x_1 + \theta_2 x_2$, geometricamente l'errore può essere raffigurato come un'ellisse la quale aumenta di raggio all'aumento di $\theta_1$ e $\theta_2$. Minimizzando la funzione aggiundo $\lambda \lVert \theta\rVert^2_2$, significa che il punto $\theta_{\text{opt}}$ viene "shiftato" in nuova nuova posizione dello spazio 2D. Questa nuova posizione posiamo marcarla con $\theta^*$, la quale rappresenta il **minimo vincolato**.

In particolare, il punto $\theta^*$ giace sulla circonferenza con centro all'origine degli assi e raggio $r$, tale per cui $\theta_1^2 + \theta_2^2 \leq r^2$ e con $r$ inversamente proprozionale a $\lambda$, ovvero all'aumentare di $\lambda$, si riduce $r$ e la soluzione tende ad avvicinarsi all'origine con $\theta$ minori.

*Speculation Moment*: questa dimostrazione geometrica ci evita di effettuare il calcolo $(X^TX + \lambda I)^{-1}$, il quale richiederebbe un sacco di risorse. Tramite i metodi geometrici e di ricerca Operativa (da quel che ho capito, centra Lagrange), è possibile individuare il valore della funzione errore regolarizzata senza far esplodere il computer.

La regolarizzazione è un altro **iperparametro** da ottimizzare rispetto al validation set, e lo si trova con cross validation.

#### Individuazione del miglior $\lambda$
Il metodo più semplice per determinarlo è tramite la cross validation:
(in python $\lambda$ è chiamato $\alpha$):
```python
from sklearn.linear_model import RidgeCV
...
# Creiamo 25 lambda che spaziano da 10E-15 a 10E9
alphas = 10**np.linspace(-15, 9, 25)

reg_cv = RigeCV(alphas, cv=5) # 5 cross validation
reg_cv.fit(poly.fit_transform(X_train), Y_train)
reg_cv.score(ploy.transform(X_val), Y_val)
>>> 0.01102

reg_cv.alpha_ # miglior alpha trovato
>>> 0.1
```

Nota: determinare gli iperparametri ($\alpha$) migliori con gli stessi dati usati per estrarre il modello migliore, genera score ottmisti.

Se si usa **Nested Cross Validation**, è possibile stimare correttamente lo score anche su dati ignoti.

### Nested Cross Validation
Vengono effettuate due cross validation, una interna ed una esterna.
Vengono creati $k$ fold per la cross validation esterna, ed ogni fold, viene suddiviso in ulteriori $m$ fold per effettuare la cross validation interna. 

Lo scopo è quello di trovare gli **iperparametri** migliori nella cross validation interna, per poi usarli per addestrare e testare il modello nella relativa parte della validation esterna.

Perciò, non viene estratto un modello migliore di altri, ma vengono stimati gli iperparamentri per estrarre il modello migliore.

Per passi quindi viene seguito il seguente algoritmo:
- Per $i$ in ogni $k$ split esterno:
  - Dividi il dataset in train e test set per lo split $i$-esimo
  - Per $j$ in ogni $m$ split interno:
    - Dividi il dataset di train in train e test set per lo split $j$ esimo
    - Scegli casualmente un set di iperperametri
    - Addestra il modello sul dataset di train per lo split $j$-esimo
    - Calcola l'errore con il test set per lo split $j$-esimo
  - Seleziona il set $p^*$ di iperparametri ottimali, dove l'errore calcolato al passo precedente è minore.
  - Addestra il modello sui dati di train per lo split $i$-esimo
  - Calcola l'errore con il test set per lo split $i$-esimo.

Al termine, il modello migliore si ottiene addestrando su tutti i dati, utilizzando per ogni iperparametro il valore che ha dato il risultato medio migliore.

## Colinearità
Nella regresione lineare, si assume che le variabili in input siano **indipendenti tra loro**.

Con dipendezne, la regressione risulta instabile: in generale esiste un accuratezza imprevedibile sui dati ignoti, in tutti quei casi in cui esiste una dipendenza tra uno o più $\theta$.

La **regolarizzazione** risolve il problema, poiché vincola/riduce le possiibili soluzioni.

### Regressione LASSO
La [regressione Ridge](#ridge-regression) all'aumentare di $\lambda$ **riduce**, ma non azzera il valore dei parametri $\theta$. Perciò la soluzione utilizza sempre tutte le variaibili, anche quelle irrilevanti per la predizione (*soluzione densa*).

Se **penalizziamo** i $\theta$ nella minimizzazione dell'errore con norma L1 invece che L2, otteniamo:

$$
\min_{\theta}\sum_{i=1}^m(\theta^Tx^{(i)} - y^{(i)})^2 + \lambda \lVert\theta\rVert_1 \quad : \quad \lVert \theta\rVert_1 = \sum_{j=1}^n |\theta_j|
$$

In questo modo, la soluzione vincolata $\theta^*$, non è più sulla circonferenza di un cerchio centrato nell'origine (o ipersfera in casi $\mathbb{R}^n$ con $n > 2$), ma su un **ipercubo** centrato sull'origine con le diagonali parallele agli assi, dove:
- Al crescere di $\lambda$, è più probabile che $\theta^*$ cada sugli spigoli, azzerando in questo modo diversi $\theta$ $\implies$ più variabili irrelevanti si azzerano (*soluzione sparsa*).

Diventa quindi un modello predittivo più interpetabile, dove attraverso questa tecnica di regressione, vengono selezionate le variabili/features più importanti.

## Regressione Elastic Net
Generalizza [Rige](#ridge-regression) e [Lasso](#regressione-lasso), con entrambe le penalizzazioni dei $\theta$ con norma L1 e L2:

$$
\min_{\theta}\sum_{i=1}^m(\theta^Tx^{(i)} - y^{(i)})^2 + \lambda
(\alpha \lVert \theta\rVert_1 + (1-\alpha) \lVert\theta\rVert_2^2)
$$

Introducendo un nuovo iperparametro $\alpha$ per pesare le penalizzazioni L1 e L2, per poter effettuare combinazioni tra le due, sfruttandone i relativi pro e contro in base al modello e dataset da modellare.

In Python:
- $\alpha$ è `l1_ratio`
- $\lambda$ è `alpha`

## Gestione della dimensionalità
In generale, la regressione polinomiale di grado $g$ in $n$ variaibli genera $\binom{n+g}{g}$ termini.
Una rule of thumb potrebbe essere quella di diminuire $g$ all'aumentare di $n$ e viceversa, ma questo può portare a effetti indesiderati o mancanza di accuratezza del modello.

Esiste un metodo in grado di mappare i dati originali in nuovo spazio ad elevata dimensionalità **senza** però creare le relative nuove variabili.
Queste funzioni prendono il nome di **funzioni kernel**.

### Funzioni Kernel
Se prendiamo un polinomio del tipo $(1+x_1z_1 + x_2z_2)^2$, con $x=(x_1, x_2)$ e $z=(z_1, z_2)$ e sviluppando il quadrato, otteniamo il seguente mapping:
$$
\begin{align*}
    (1 + x_1z_1 + x_2z_2)^2&= x_1^2z_1^2 + 2x_1x_2z_1z_2+x_2^2z_2^2+2x_1z_1 + 2x_2z_2 + 1\\
    &=(x_1z_1+x_2z_2)^2 + 2(x_1z_1 + x_2z_2) + 1 \\
    &=(x^Tz)^2 + 2(x^Tz) + 1 \\
    &=(x^Tz + 1)^2
\end{align*}
$$

Dove di interessante c'è che il quadrato del prodotto scalare dei vettori iniziali $x$ e $z$ in 2 dimensioni + 1, è uguale al prodotto scalare dei vettori trasormati in 6 dimensioni, ovvero:
$$((x_1, x_2) \cdot (z_1, z_2) + 1)^2 = (x_1^2, x_1x_2 \sqrt{2}, x_2^2, x_1\sqrt{2}, x_2 \sqrt{2}, 1) \cdot (z_1^2, z_1z_2\sqrt{2}, z_2^2, z_1\sqrt{2}, z_2\sqrt{2}, 1)$$

Quindi capiamo che, il quadrato della somma di 2 moltiplicazioni $x_1z_1, x_2z_2$, produce lo stesso effetto della somma di 6 moltiplicazioni.

**Kernel Trick** (polinomiale): vale per ogni grado $g$ e numero di dimensioni $n$:
$$\textbf{x}(x_1,\dots,x_n) \quad \textbf{z}=(z_1,\dots,z_n)
\quad \text{Kernel}(\textbf{x}, \textbf{z}) = (\textbf{x} \cdot \textbf{z} + 1)^g$$

Computazionalmente parlando:
- Senza Kernel: $O(\frac{r^2n^g}{2g!})$
- Con Kernel, il costo è costante all'aumentare di $g$ $\implies O(\frac{r^2n^2}{2})$

#### Utilizzo del Kernel nella Regressione
Consideriamo una regressione quadratica in una variabile:
$$h_\theta(x) = \theta_0 + \theta_1x + \theta_2x_2 = (\theta_0, \theta_1, \theta_2) \cdot (1, x, x^2) = \Theta^T\phi(x)$$
Dove $\phi(x)$ è una trasformazione di $x$.
In tutto questo delirio, i coefficienti ottimali $\Theta$ sono combinazioni lineari dei dati stessi, perciò: $\Theta^T = \sum_{i=1}^m\alpha_i\phi(x^{(i)})$. Sostiuendo, otteniamo:
$$h_\theta(x) = \sum_{i=1}^m\alpha_i\phi(x)\phi(x^{(i)})$$
Dove:
- $x$ sono parametri in input.
- $\phi(x)$ trasformazione della singola istanza in input
- $\phi(x^{(i)})$ è l'applicazione della trasformazione all'**istanza** $i$-esima diversa da $x$.

Siccome è quindi presente un proddotto scalare tra due vettori in $\mathbb{R}^2$, possiamo scrivere sostituirlo con la funzione kernel polinomiale:
$$h_\theta(x) = \sum_{i=1}^m \alpha_i K(x, x^{(i)})$$

In tutto questo ci si chiede perché la sommatoria. La sommatoria è presente perché introduce il prodotto tra il dato di input $x$ da predire, e tutti gli altri $m$ dati $x^{(i)}, i=1,\dots,m$ del dataset e per ciascuno c'è un proprio parametero $\alpha_i$ da apprendere.

$\implies$ la complessità di training è circa quadratica rispetto al numero di istanze.

##### Minimizzazione della Funzione di Errore con Kernel
Ricordiamo la funzione di errore da minimizzare:
$$\min_\theta \sum_{i=1}^m(\Theta^Tx^{(i)} - y^{(i)})^2 + \lambda\lVert\Theta\rVert^2_2$$

Per introdurre il kernel, aggiungiamo i pezzi incrementalmente, cominciando con la Norma 2:
Il vettore dei parametri ottimali $\theta^*$, possiamo ricavarlo come combinazione lineare dei dati in input, ovvero $\theta^*=\sum_{i=1}^m\alpha_i\phi(x^{(i)})$. La sua norma al quadrato quindi è esprmibile come
$$\lVert\Theta\rVert^2_2 = \Theta^T\Theta 
= \sum_{i=1}^m(\alpha_i\phi(x^{(i)})^T)
\cdot
\sum_{j=1}^m(\alpha_j\phi(x^{(j)}))
= \sum_{i=1}^m\sum_{j=1}^m\alpha_i\alpha_jK(x^{(i)}, x^{(j)})
$$

Riscrivibile in forma vettoriale come:
$$\Alpha^TK\Alpha$$
Dove $K \in \mathbb{R}^{m\times m}$ è la matrice quadrata $K_{i,j} = K(x^{(i)}, x^{(j)})$ con i valori kernel di tutte le coppie dei dati.

Ora possiamo tranquillamente proseguire con il riscrivere l'errore quadratico medio con i nuovi valori e la funzione kernel:
$$\min_\alpha \frac{1}{m} \sum_{i=1}^m
\left(
\sum_{j=1}^m \alpha_jK(x^{(j)}, x^{(i)}) - y^{(i)}
\right)^2 + \lambda\Alpha^TK\Alpha$$

È possibile riscrivere la sommatoria interna, e di conseguenza ridurre la sommatoria esterna e il quadrtato con una norma a due, creando così:
$$
\min_\theta \frac{1}{m} \lVert K \Alpha - \textbf{y} \rVert^2_2 + \lambda \Alpha^TK\Alpha
$$

Dove considerando che l'$i$-esmio elemento del vettore $K\Alpha - \textbf{y}$ è il quadrato della vecchia sommatoria interna.