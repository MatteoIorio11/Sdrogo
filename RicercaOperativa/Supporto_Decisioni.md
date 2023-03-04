# Ricerca Operativa

## Supporto alle Decisioni : Introduzione all'Ottimizzazione

### Metodi di ottimizzazione 
I *metodi di ottimizzazione* hanno un'ampia gamma di applicazioni, tra cui il *Supporto alle Decisioni*.  I metodi utilizzati per sviluppare soluzioni software per il supporto alle decisioni spaziano *dall'Ottimizzazione* all'*Intelligenza Artificiale*.


Per sviluppare una soluzione al supporto delle decisioni è necessario seguire i seguenti passi :
1. **Modellare matematicamente il problema**
2. **Identificare la sua complessità**
3. **Progettare l'algoritmo più adatto**, usando le tecniche di soluzione in relazione al modello e alla complessità del problema.

Una **istanza** rappresenta i dati noti del problema, per risolvere un problema è necessario **costruire un modello** e definire un **algoritmo** di soluzione.

### Modelli

I *modelli* sono una rappresentazione, spesso semplificata, di concetti. I modelli possono riguardare sia aspetti puramente teorici che aspetti del mondo reale. 
I modelli possono essere di tipo : verbale, grafico, fisico, matematico ecc ecc..

Attraverso l'utilizzo dei modelli è possibile perseguire i seguenti obbiettivi: 
1. **Facilitare la comprensione**, identificando le componenti
2. **Spiegare, controllare e predire eventi**, anche sulla base di osservazioni passate
3. **Supportare i processi decisionali**

Ciò che deve essere rappresentato all'interno di un modello può essere composto da molte componenti, di conseguenza è necessario effettuare delle **semplificazioni** al modello, che non *interferiscano* con l'utilizzo che se ne vuole fare. Non bisogna adottare modelli complicatissimi. Purtroppo anche l'utilizzo di modelli estremamente semplificati portano ad avere un alto numero di errori. 

Attraverso il **Modello Matematico** è possibile rappresentare la realtà di interesse con un alto grado di astrazione. I modelli matematici prevedono l'uso di parametri.

Nel caso in cui i parametri possano essere definiti con esattenza siamo nel caso di **modelli deterministici**, nel caso in cui i parametri non siano certi siamo nel caso di **modelli stocastici** (modelli in cui i parametri non sono stati definiti a priori).

I *modelli stocastici* sono difficili da risolvere, perciò spesso ci si porta a *modelli deterministici*, enumerando degli scenari rappresentativi della realtà di interesse. 

Le approssimazioni nei parametri dei modelli possono portare ad errori nel calcolo, andando a sporcare di conseguenza la validità dell'output.

### Approssimazioni di un Modello
Prima del calcolo:
1. modello scelto
2. misure empiriche
3. precedenti calcoli.

Durante il calcolo:
1. Troncamenti
2. arrotondamenti

### Errori
**Errore di Troncamento**: L'errore di troncamento è dato dalla differenza tra il *risultato reale* e quello prodotto dall'algoritmo. 

**Errore di Arrotondamento**: L'errore di arrotondamento è dato dalla differenza tra il risultato prodotto da un dato algoritmo usando un'aritmentica esatta e il risultato prodotto dallo stesso algoritmo usando un'altra aritmetica approssimata. Errori che *vengono introdotti dalla macchina*, in quanto costituita da valori finiti (calcolatrice, registri del computer, memoria a disposizione del calcolatore ecc ecc). 

Gli errori di calcolo possono **propagarsi**, nei calcoli successivi andando a sporcare sempre di più i nostri output.

### Malcondizionamento
Piu le rette tendono ad essere parallele e più vengono amplificati gli errori, peggiora il **condizionamento** dell'istanza di un problema.

### Tipologie di Problemi
1. Problema di **Decisione**: data un'istanza si vuole determinare se esiste o meno una soluzione
2. Problema di **Ricerca**: data un'istanza si vuole determinare una possibile soluzione
3. Problema di **Enumerazione**: data un'istanza si vogliono determinare tutte le possibili soluzioni
4. Problema di **Ottimizzazione**: data un'istanza si vuole determinare la *migliore soluzione* possibile. 

### Complessità Computazionale
La complessità computazione ci permette di capire se un problema è: 
1. *facile* &rarr; la soluzione può esistere ed è polinomiale
2. *difficile* &rarr; non esiste una soluzione polinomiale, non si può garantire di conseguenza la sua soluzione

Tale distizione ci permette di capire quale algoritmo scegliere per risolvere il nostro problema. L'utilizzo di risultati approssimati spesso ci permette di ridurre la complessità della soluzione, in quanto soluzioni ottime possono essere raggiunte in maniera non polinomiale. (Esempio corriere amazon con 60 posti da cosegnare, soluzione 60!)

Un algoritmo risolve un problema se è in grado di generare una soluzione per ogni possibile istanza. 

I **problemi semplici** sono quelli polinomiali (insieme **P**), mentre i **problemi difficili** sono quelli "non polinomiali* (insieme **NP**, Nondeterministic Polynomial Time), tra cui ci sono i problemi **NP-Completi**. **NP** è l'insieme dei problemi in cui se esiste soluzione la si può verificare in tempo polinomiale ma il calcolo della soluzione richiede un tempo non polinomiale (controllare i cammini hamiltoniani si fa in tempo polinomiale, ma il calcolo della soluzione per tale problema lo si fa in tempo non polinomiale). 

Un problema decisionale 

$$F:I \rightarrow \{0, 1\}$$ 

è *riducibile polinomialmente* a 

$$G:I \rightarrow \{0, 1\} $$

se esiste una funzione "h" calcolabile in tempo polinomiale. **In sostanza se la soluzione si può controllare in tempo polinomiale**. 


### Problemi vs Algoritmi
Le **prestazioni di un algoritmo** possono essere misurate con:
1. Tempo di calcolo richiesto per ottenere la soluzione
2. La qualità della soluzione

Per i **problemi difficili** c'è in oltre un ulteriore opzione: 
1. _Algoritmi euristici_, che trovano soluzioni di **buona qualità**
2. _Algoritmi esatti_, che trovano le soluzioni **ottime**.

### Modelli vs Algoritmi 
Il modello scelto per un dato problema ha un impatto determinante sulla scelta dell'algoritmo più adatto. Modelli molto semplificati possono comportare errori nel futuro, modelli troppo complessi sono di difficile interpretazione e spesso calcolarne i risultati ottimi è pressocché impossibile.

### Ricerca Operativa
Per risolvere un problema bisogna **costruire un modello** che sia risolvibile da un *algoritmo adeguato alla complessità del problema* e alla tipologia di istanza che dobbiamo risolvere. 


### Esempi
#### Ottimizzazione Non-Vincolata
In generale mediante l'ottimizzazione non vincolata, stiamo ottimizzando una funzione senza la presenza generale di ulteriori vincoli sulle nostre incognite. Questo fa in modo di dare maggiore libertà nella risoluzione del modello.
##### Domanda e Ricavo
Viene prevista l'equazione della domanda $q = -2.000p  +150.000$, ovvero il *modello lineare* del problema con:
- $q$ numero di libri venduti.
- $p$ prezzo in euro.

**D**: Come ottenere il massimo ricavo?

Per ottenere il massimo ricavo si segue la formula $R=pq$, che sostituendo all'equazione della domanda, permette di ottenere una formula che lega il ricavo in funzione del prezzo, ovvero:
$$ R(p) = -2000p^2 + 150000p $$
Che risulta essere un *modello* ora *quadratico*. Risulta immediato ora calcolare il punto di massimo in modo tale da massimizzare il ricavo, ovvero algebricamente applicando la derivata prima, o geometricamente calcolando il vertice della parabola disegnata dalla funzione mediante la formula $p = -\frac{b}{2a}$. Mediante quest'ultimo si trova che $p = 37.5$, e per calcolare il corrispondete ricavo è sufficiente sostituire $p$ all'equazione sopra. 
Questo prezzo  $p$ trovato rappresenta la soluzione ottimale del problema.

#### Ottimizzazione Vincolata
I modelli di *Ottimizzazione Vincolata* presentano dei veri e propri **vincoli** sulle incognite, così facendo per risolvere il nostro sistema i vincoli dovranno essere sempre soddisfatti.
##### Miscelazione
Esistono le seguenti ricette per la miscelazione di 3 bevande:
- *PineOrange*: 2 parti di succo d'ananas e 2 parti di succo d'arancia.
- *PineKiwi*: 3 parti di succo d'ananas e 1 parte di succo di kiwi.
- *OrangeKiwi*: 3 parti di succo d'arancia e 1 parte di succo di kiwi.

Come si può notare, il modello sopra risulta consistente, ovvero i dati sono presentati in termini di quarti di litro.
**D** Quanti litri di ciascuna miscela deve produrre per utilizzare **tutte** le seguenti materie prime?
- 800 parti di succo d'ananas.
- 650 parti di succo d'arancia.
- 350 parti di succo di kiwi.

Queste misure e il fatto che il problema richieda che siano esaurite tutte le scorte, rappresentano i **vincoli** del problema.

È possibile individuare le **variabili decisionali**, dopo aver fatto attenzione alle unità di misura del problema (*parti* e *litri*):
- $x_1$: numero di **litri** di PineOrange prodotti in un giorno.
- $x_2$: numero di **litri** di PineKiwi prodotto in un giorno.
- $x_3$: numero di **litri** di OrangeKiwi prodotto in un giorno.

| | $x_1$ | $x_2$ | $x_3$ | Totale Disponibile |
|---------------------------|---|---|---|-----|
|Succo Ananas (**parti**)   | 2 | 3 | 0 | 800 |
|Succo Arancia (**parti**)  | 2 | 0 | 3 | 650 |
|Succo Kiwi (**parti**)     | 0 | 1 | 1 | 350 |

Ponendo il tutto a sistema si ottiene il sistema lineare a **rango massimo**:
$$
\begin{cases}
    2x_1 + 3x_2 = 800 \\
    2x_1 + 3x_3 = 650 \\
    1x_2 + 1x_3 = 350
\end{cases}
$$
Risolvendo la matrice associata per esempio con *Gauss-Jordan*, si arriva alla soluzoone $(x_1, x_2, x_3) = (100, 200, 150)$.

È importante notare che gli unici gradi di libertà che si hanno sono sono:
- Cambiare le ricette
- Cambiare i termini noti
- Rilassare il vincolo di consumarle tutte (introdurrebbe le disequazioni nel sistema)

##### Flusso di traffico
3 strade a senso unico:
- Strada A: posizionata in alto
- Strada B: posizionata in basso
- Strada C: connette la strada A alla strada B

Un contatore di traffico (Ovest) è posizionato prima delle 3 strade e 2 sono collocati sulla strada A e B (Est).
- Il contatore Ovest regista 200 auto in entrata ogni ora.
- I contatori Est registrano 100 auto in usicta ogni ora ciascuno.

Considerando la rete come un flusso, per il *principio di conservazione del flusso*, il flusso entrante deve essere uguale al flusso uscente. 
**D**: con le informazioni a disposizione è possibile stabilire quante auto transitano ogni ora nelle strade A, B e C?
Definiamo le variabili decisionali:
- $x_1$: numero di auto che transitano ogni ora nella strada A.
- $x_2$: numero di auto che transitano ogni ora nella strada B.
- $x_3$: numero di auto che transitano ogni ora nella strada C.

E applicando il principio di conservazione del flusso, otteniamo il sistema di equazioni lineari:
$$
\begin{cases}
    x_1 + x_2 = 200 \\
    x_1 - x_3 = 100 \\
    x_2 + x_3 = 100 \\
\end{cases}$$

Dove è da subito possibile notare come una delle tre equazioni è combinazione lineare delle altre due.
Applicando Gauss-Jordan quindi riduciamo la matrice e otteniamo che la variaible $x_3$ risulta variabile indipendente del sistema, creando così la soluzione al sistema lineare pari a 
$$ \begin{cases}
    x_1 = x_3 + 100 \\
    x_2 = -x_3 + 100 \\
    x_3 \qquad \text{arbitrario}
\end{cases} $$
Dove in realtà il valore di $x_3$ deve:
- $x_3 > 0$
- Rispettare il vincono di non-negatività delle variaibli $x_1$ e $x_2$ $\rightarrow$ $0 < x_3 < 100$

Nota: per tutti i problemi di flusso, è sempre presente un vincolo ridondante.

##### Trasporti
Esistono 4 sedi di un azienda di auto noleggio:
- Sede A: 20 auto in più del necessario
- Sede B: necessita di 10 auto in più
- Sede C: 15 auto in più del necessario
- Sede D: necessita di 25 auto in più

I costi di spostamento da una sede ad un altra sono come segue:
- A &rarr; B : 10$
- C &rarr; B : 5$
- A &rarr; D : 20$
- C &rarr; D : 10$

Esiste un **vincolo di budget** di 475$. (Tale vincolo deve essere sempre rispettato affinché ci sia consistenza nel nostro modello)

**D**: con il budget previsto, è possibile spostare le auto tra le 4 sedi?

È possibile definire le variabili decisionali:
- $x_{A,B}$: numero di auto da A &rarr; B
- $x_{A,D}$: numero di auto da A &rarr; D
- $x_{C,B}$: numero di auto da C &rarr; B
- $x_{C,D}$: numero di auto da C &rarr; D

mediante le quali si può modellare modellare il problema di flusso con le rispettive equazioni:
- La sede A ha una disponibilità di 20 auto &rarr; $x_{A,B} + x_{A,D} = 20$
- La sede B richiede 10 auto &rarr; $x_{A,B} + x_{C,B} = 10$
- La sede C ha una disponibilità di 15 auto &rarr; $x_{C,B} + x_{C,D} = 15$
- La sede D richiede 25 auto &rarr; $x_{A,D} + x_{C,D} = 25$

Il vincolo di budget determina quindi infine l'equazione:
$$10x_{A,B} + 20x_{A,D} + 5x_{C,B} + 10x_{C,D} = 475$$

Si otttiene così un sistema sovradeterminato in 5 equazioni e e 4 variaibli, ma riducendo la matrice con Gauss-Jordan, fortunatamente si scopre che un'equazione è combinazione lineare delle altre, perciò può essere estratta la soluzione:
$$(x_{A,B}, x_{A,D}, x_{C,B}, x_{C,D}) = (5, 15, 5, 10)$$

Osservazioni:
- Il risultato è intero poiché la matrice associata risulta **interamente unimodulare** (?non so se si dice così), ottenendo così gratis la soluzione intera.
- Se il budget fosse stato diverso, sarebbe potuto incorrere il problema della soluzione frazionaria, dove in problemi come questo, può risultare utile il concetto di **Rounding** del risultato (non è garantita la soluzione ottima).
 
È possibile minimizzare il budget spostando tutte le auto, eliminando il vincolo e risolvendo il sistema delle 4 equazioni, ottenendo:
$$
\begin{cases}
    x_{A,B} = x_{C,D} - 5 \\
    x_{A,D} = 25 - x_{C,D} \\
    x_{C,B} = 15 - x_{C,D} \\
    x_{C,D} \qquad \text{arbitrario}
\end{cases}
$$

Anche in questo caso, esistono dei vincoli nel valore di $x_{C,D}$:
- Deve essere non-negativo $ \implies x_{C,D} > 0$
- Deve rispettare i vincoli di non-negatività delle altre variabili $ \implies 5 \leq x_{C,D} \leq 15$

Essendo il budget non più un vincolo, è possiible definire la funzione obiettivo come la funzione di costo definita come:
$$c(x) = 10x_{A,B} + 20x_{A,D} + 5x_{C,B} + 10x_{C,D}$$.
Dove, sostituendo con le soluzioni trovate nel sistema lineare sopra, si ottiene:
$$
c(x) = 10(x_{C,D}-5) + 20(25-x_{C,D}) + 5(15 - x_{C,D}) + 10x_{C,D}
$$

Dove sviluppando i calcoli, si arriva alla soluzione con costo minimo pari a $c(x) = -5x_{C,D} + 525$.
Questo risultato ci dice che per ogni macchina che viene trasportata sulla strada da C &rarr; D, risparmaimo 5\$, quindi per ottenere il costo minimo, prendiamo il massimo valore di $x_{C,D}$ che è 15, arrivando ad un budget minimo pari a 450$.

##### Succhi
Esistono due ricette per il succo di mela, espresse in 32-esimi (*consistenza* del modello):
- **Tipo 1**: 1 litro composto da 30 parti d'acqua e 2 di succo di mela concentrato.
- **Tipo 2**: 1 litro composto da 20 parti d'acqua e 12 di succo di mela concentrato.

**D.1**: quanti litri di ciascun tipo devono essere prodotti per terminare tutte le scorte di acqua e succo se l'azienda ogni giorno dispone di 30.000 parti d'acqua e 3600 di succo di mela concentrato?

Come il primo probloema, identifichiamo le variabili decisionali come:
- $x_1$: litri di succo di tipo 1 prodotti ogni giorno.
- $x_2$: litri di succo di tipo 2 prodotti ogni giorno.

Ed esatamente come prima possiamo definire le equazioni lineari per le ricette con i rispettivi vincoli giornalieri:
$$
\begin{cases}
    30x_1 + 20x_2 = 30000 \\
    2x_1 + 12x_2 = 3600 \\
\end{cases}
$$

Anche se il sistema è banale da risolvere, è importante notare come una **normalizzazione** dei dati (e.g. dividere tutto per 10 sopra e 2 sotto) sia un metodo di **Precondizionamento** del problema, ovvero un metodo base che può ridurre (anche di poco, ma meglio di niente) l'indice di condizionamento del problema.

La soluzione è quidi $ \qquad \begin{cases} x_2 = 150 \\ x_1 = 900\end{cases} \qquad$

**D.2**: Il vincolo ora è di non consumare tutta l'acqua e il concentrato di mela.
Entrano in gioco le *disequazioni*, le quali prevedono una risoluzione non banale perché possono dare problemi con le operazioni elementari.
Il sistema è della forma:
$$
\begin{cases}
    30x_1 + 20x_2 \leq 30000 \\
    2x_1 + 12x_2 \leq 3600 \\
\end{cases}
$$
Il quale richiede l'ulteriore vincolo di  non negatività $x_1 \geq 0$ e $x_2 \geq 0$.
In casi come questo ci si riconduce ad un sistema di equazioni attraverso l'impiego di variaibli di scarto $s_1$ e $s_2$, anch'esse necessariamente maggiori di 0,
risultando così nel sistema "quasi equivalente":
$$
\begin{cases}
    30x_1 + 20x_2 + s_1 = 30000 \\
    2x_1 + 12x_2 + s_2 = 3600 \\
\end{cases}
$$

### Ottimizzazione in Generale
Durante la risoluzione dei nostri modelli, indipendetemente dalla tecnica risolutoria è strettamente necessario **controllare la consistenza stessa del modello**.


### Ottimizzazione Vincolata
Il sistema di disequazioni definisce l'insieme delle **soluzioni ammissibili** del nostro problema, chiamata anche come *Regione Ammissibile*. La *Regione Ammissibile* racchiude tutti i punti che soddisfano i vincoli del problema. 

Con il termine di **programmazione matematica** si intende il criterio con la quale decidere quale sia il miglior punto della regione ammissibile.


#### Esempio 
Riprendiamo il nostro esempio dei succhi. 
Se ipotizziamo che il profitto per ogni litro di succo di mela di tipo 1 è 0.25 Euro e per quello di tipo 2 0.75. Questa volta il problema di *programmazione lineare* si può scrivere in questo modo:

$$
\begin{align*}
& z = \text{Max}(0.25 x_1 + 0.75x_2)  \\
& s.t. \qquad 30x_1 + 20x_2 \leq 30000 \\
& \qquad\qquad 2x_1 + 12x_2 \leq 3600  \\
& \qquad \qquad x_1 \geq 0  \\
& \qquad \qquad x_2 \geq 0  \\ 
\end{align*}
$$

tale funzione *z* viene chiamata **Funzione Obbiettivo**, la nostra funzione obbiettivo va sempre ottimizzata, mentre le disequazioni sottostanti sono i nostri **vincoli**, i quali vanno sempre soddisfatti, definiscono la *regione dei punti da considerare*.

Tra i tanti metodi con la quale risolvere tale sistema si può utilizzare il **Metodo del Simplesso**. Il *metodo del simplesso formato tableau*, usa le operazioni elementari per risolvere dei sistemi lineari. 

La **soluzione ottima** è 
$$
(x_1, x_2) = (900, 150)\\
z = \text{Max}(0.25x_1 + 0.75x_2) = 337.5
$$

la soluzione ottima nei sistemi lineari sono sempre **gli estremi**.

Si può portare il nostro problema in una funzione a due incognite
$$
    f(x_1, x_2) = 0.25x_1 + 0.75x_2
$$

calcolandone poi la derivata, attraverso il gradiente è poi possibile trovare il nostro punto di massimo per risolvere la nostra *funzione obbiettivo*.

#### Costruzione del modello generale

E' possibile costruire per il nostro problema di *programmazione lineare* si può sirivere come:

* $p$ variabile del nostro profitto
* $b$ disponibilità, quanta materia prima ho
* $a$ quanto consumo per ogni unità

$$
\begin{align*}
    & z = \text{Max}\sum_{i=1} p_ix_i \\ 
    & s.t. \\
    &  \sum_i a_{ij}x_i \leq b_j && j = 1,...., m \\
    & x_i \geq 0 && i = 1,....n
\end{align*}
$$

Il primo passo è quello di **definire il modello matematico**. Il modello si può rappresentare come:
$$
\begin{align*}
    z = min(f(x)) \\
    s.t  \\
    & g_i(x) \leq b_i && i = 1,..., n \\
    & h_j(x) = d_j  && j = 1,..., m \\
    & x \geq 0
\end{align*}
$$

la funzione $f(x)$ è detta **funzione obbiettivo**, le espressioni $g_i(x) \leq b_i$ e $h_j(x) = d_j$ rappresentano i **vincoli** e $x = (x_1, ...., x_f)$ sono **variabili**. Se le funzioni $f(x), g_i(x) \leq b_i, h_j(x) = d_j$ sono lineari parliamo di **programmazione lineare continua**. 

### Modelli Matematici per l'Ottimizzazione
Se aggiungiamo dei vincoli per cui la nostra soluzione $x$ deve essere intera, allora parliamo di **programmazione lineare intera**. 

Se *solamente alcune* delle componenti di $x$ devono essere intere allora parliamo di **programmazione lineare mista intera**. 

#### Bound
Dato un problema di programmazione lineare di P di minimo, un valido *lower bound* $z_{LB}$ è una stima per difetto del valore della soluzione ottima. Tale procedura viene chiamata **procedura di bounding**, ci permette di stimare i limiti inferiori.

Dato un problema di programmazione lineare di P di minimo, una soluzione ammissibile corrisponde a un valido *upper bound* $z_{UB}$ e quindi un eccesso del valore per la soluzione ottima. Le procedure per lalcolare soluzioni ammissibili sono dette **euristiche**. 

Dato un problema di programmazione lineare P, un **algoritmo esatto** garantisce la determinazione della soluzione ottima di P.


#### Knapsack Problem
Il problema di knapsack può essere modellato matematicamente come segue:
$$
\begin{align*}
\text{maximize } & z_{KP} = \sum_{i=1} p_ix_i \\ 
s.t. \\ 
& \sum_{i=1} w_ix_i \leq W \\
&x_i  \{0, 1\} & i = 1, ..., n
\end{align*}
$$
Si traduce in:
$$
\begin{align*}{}
    & \text{maximize} \qquad z_{KP} = 12x_1 + 4x_2 + 15x_3 + 3x_4 &\\
    & \qquad s.t. \\
    & \qquad\qquad\qquad 6x_1 + 4x_2 + 5x_3 + 2x_4 \leq 10 & \\
    & \qquad\qquad\qquad x_1, x_2, x_3, x_3  \in \{0, 1\} & \\
\end{align*}
$$

Calcoliamo per ogni oggetto $i$ il suo profitto per unità di capacità: $r_i =  \frac{p_i}{w_i}$, l'oggetto che ha il valore $r_i$ più alto è quello che ci fa guadagnare di più per ogni unità di capacità impiegata.

Se l'oggetto 1 *fosse divisibile* posso prendere solo la frazione che ci sta, ottenendo l'occupazione di tutto il knapsack con il profitto **ottimo**. pari a: $z = 12 * 5/6 + 0 + 15 * 1 + 0 = 25$

Se però gli oggetti non sono divisibili, allora il valore $z'_{KP} = 25$ è solo una **stima per eccesso**, il nostro *upper bound*. Qualsiasi soluzione ammissibile del nostro problema è una **stima per difetto**, il nostro *lower bound*. 

Il problema in cui ammettiamo anche una sola soluzione frazionaria, è detto **rilassamento lineare**, in questo caso abbiamo *sempre* una soluzione in cui avremo **al più una soluzione frazionaria**, che chiameremo *splitting item*.

 Tale approccio è noto come **branch and bound**. Quando in un nodo dell'**albero di ricerca**, la soluzione è intera ci fermiamo e se migliora la soluzione ottima emergente la sostituisce. 

#### Knapsack Problem Dinamyc Programming
 Una delle alternative più efficienti è la **programmazione dinamica**. L'approccio della programmazione dinamica prevede $n$ **stadi**. Ad ogni stadio $j \in {1, ..., n}$ e per ogni **stato** $w \in {0, ..., W}$ si risolve il seguente sottoproblema:

$$
\begin{align*}
&(KP_j(w)) z_j(w) = max \sum_{i=1} p_ix_i \\
& \qquad s.t. \\
& \qquad\qquad \sum_{i=1} w_ix_i \leq w \\
& \qquad\qquad x_i \{0, 1\} && i = 1, ..., j
\end{align*}
$$

La programmazione dinamica di fatto è una enumaerazione parziale delle soluzioni. Risolvere per ogni stato $w$ dello stadio di $j$ i problemi $KP_j(w)$ equivale ad utilizzare la seguente recursione:
1. Inizializza $KP_0(w) = 0$, per ogni $w \in {0, .., W}$
2. Ad ogni stadio $j \in \{1, ...n\}$ e per ogni stato $w \in \{0, ..., W\}$:

$$
z_j(w) = 
\begin{cases}
        z_{j-1}(w) & \text{se} \quad w \le w_j \\
        \text{max}\{z_{j-1}(w), z_{j-1}(w - w_j) + p_j\} & \text{se}\quad w\geq w_j
\end{cases}
$$
La complessità è $O(nW)$, quindi si dice che è "*pseudopolinomiale*". 

```python
def knapsack(W, weights, prices, n):
    if(n == 0 or W == 0):
        return 0
    
    if(weights[n-1] > W):
        return knapsack(W, weights, prices, n-1)
    else:
        return max(prices[n-1] + knapsack(W-weights[n-1], weights, prices, n-1),
         knapsack(W, weights, prices, n-1))

```
### Metodi di soluzione
I problemi di programmazione lineare (LP) continua possono essere risolti con diverse tecniche:
* Simplesso Primale
* Simplesso Duale
* Simplesso per le reti
* Metodo Barrier
  
I problemi di programmazione lineare intera o mista (PLI), possono essere risolti utilizzando i seguenti algoritmi:
* Branch & Bound
* Branch & Cut &rarr; aggiungo dei vincoli in questo modo trovo soluzioni frazionarie
* Branch & Price &rarr; genero variabili
* Branch & Price & Cut
* Programmazione Dinamica

## Linguaggi di modellazione
Servono per descrivere un problma di ottmizzazione con un buon libello di astrazione e semplicità. Compito del linguaggio di modellazione è l'interfacciamento con i *solver* per caricare e risolvere il problema e per accedere ai dati e alle soluzioni.

Useremo AMPL da linea di comando, ma è possibile linkare le librerie con vari linguaggi (C/C++, Python, Java, ...)

AMPL funziona con **modelli lineari** e **quadratici**.

### Guida d'uso rapida AMPL
È possibile utilizzare AMPL da linea di comando richiamando il comando `./ampl` o `ampl` se è presente in `PATH`.
In questo modo è possibile specificare:
- `var <name>`: variabile decisionale specificata dal `<name>`.
- `maximize/minimize <f_obj_name> : <expr>`: dichiarare una funzione obiettivo, definita da un'equazione dopo i ":".
- `subject to <constraint_name>: <expr>`: dichiarazione di un vincolo.
- `solve`: risolve il problema di programmazione lineare.
- `display <var>`: mostra il valore di una variaible o parametro


#### Generalizzazione
AMPL consente di separare il modello dai dati. In particolare gli elementi fondamentali di un problema LP sono:
- **DATI**
  - *Insiemi* (`set`): liste di prodotti, risorse,...
  - *Parametri* (`param`): Sono gli input numerici del problema, e possono essere *vettori* oppure *scalari*
- **MODELLO**
  - *Variabili* (`var`): var. decisionali definite dal risolutore.
  - *Funzione Obiettivo*: funzione delle var. decsionali da *massimizzare*/*minimizzare*.
  - *Vincoli* (`subject to`): funzioni delle var. decisionali che devono rimanere entro certi limiti.

#### Esempi d'uso
#### Esempio 1
Consideriamo il seguente problema LP:
$$
\begin{align*}
    & z = \text{Max}3x_1 + 4x_2 & \text{Rendimento} \\
    & \qquad s.t.  \\
    & \qquad\qquad x_1 + x_2      \leq 100 & \text{Capitale} \\
    & \qquad\qquad 2x_1 + x_2     \leq 150 & \text{Rating Medio} \\
    & \qquad\qquad 3x_1 + 4x_2    \leq 360 & \text{Scadenza Media} \\
    & \qquad\qquad x_1,x_2 \geq 0 \\
\end{align*}
$$

Seguendo l'approccio generalizzato, è possibile creare i seguenti file, rispettivamente per il modello e per i dati:
```bash
# bonds.mod

set bonds; # insieme di bonds
param yield {bonds};    # rendimenti
param rating {bonds};   # ratings
param maturity {bonds}; # scadenze
param max_rating;       # massimo rating medio ammesso
param max_maturity;     # Massima scadenza media ammessa
param max_cash;         # capitale massimo disponibile

var buy {bonds} >= 0    # Quantità da investire per il prodotto i: var. decisionale

maximize total_yield : sum {i in bonds} yield[i] * buy[i];

# Vincoli delle variaibli e f. obiettivo
subject to cash_limit : sum {i in bonds} buy[i] <= max_cash
subject to rating_limit : sum {i in bonds} rating[i] * buy[i] <= max_rating
subject to maturity_limit : sum {i in bonds} maturity[i] * buy[i] <= max_maturity
```

```bash
# bonds.dat

set bonds := A B; # da notare lo spazio come delimitatore 🤮

param : yield rating maturity :=
    A       4       2       3
    B       3       1       4;

param max_cash := 100;
param max_rating := 150;
param max_maturity := 360;
```

Per risolvere il problema, basterà ora lanciare:
```bash
$ ampl: model bonds.mod
$ ampl: data bonds.dat
$ ampl: solve;
...
$ ampl: display buy;
buy[*] :=
A 50
B 50
```

In questo modo se si vogliono cambiare i dati (anche aggiungere un ulteriore bond), sarà sufficiente modificare il file `*.dat`.

Osservazioni interessanti:
- Un parametro definito con `param` può essere un vettore o uno scalare: quando viene specificata la dimensione tra parentesi graffe, si sta definiendo la sua dimensione (e.g. `param yield {bonds}` dichiara un parametro `yield` per ogni elemento contenuto in `bond`).
- Per ogni parametro, essi sono i **termini noti** delle equazioni del problema.
  - È possiible visualizzarli dopo il `solve;` per visualizzare le **variabili duali** ottime (? non ho capito bene cosa siano ma le vedremo più avanti).
- I delimitatori sono degli spazi.
- Si possono modificare i dati direttamente da console con l'istruzione `data`.
- È fortemente consigliato ad ogni risoluzioned i resettare le variaibli, mediante `reset data` (con `reset` si resetta anche il modello), mentre con `reset data <nomevar>` si droppa un solo dato.

#### Esempio 2
- Un'azienda deve produrre $n$ prodotti con a disposizione $m$ materie prime (simile all'eserizio di miscelazione).
- Ogni prodotto $i$ ha una ricetta che indica per ogni materia prima $j$ la quantità $a_{ij}$ per produrre una unità.
- Ogni unità di prodotto genera un profitto $p_i$ e la disponibilità di ogni materia prima $j$ è pari a $b_j$.

**D**: Trovare le quantità di prodotto per **Massimizzare** il profitto dati i seguenti dati:
- Materie prime $m=2$ con $b_1=30000$ e $b_2=3600$
- Prodotto $n=2$:
  - $p_1 = 0.25$, $a_{11} = 30$ e $a_{12}=2$
  - $p_2 = 0.75$, $a_{21} = 20$ e $a_{22}=12$

Il testo corrisponde al problema di **programmazione lineare**, e sarebbe esprimibile come segue:
$$
\begin{align*}
    &z = \text{Max}\sum_{i=1}^{n}{p_ix_i} \\
    & \qquad s.t. \\
    & \qquad\qquad \sum_{i=1}^{n}{a_{ij}x_i} \leq b_j & j=1..m \\
    & \qquad\qquad x_i \geq 0 & i=1..n
\end{align*}
$$

Che trasposto su AMPL diventa:
```bash
# es1.mod

set prod;   # prodotti
set raw;    # materie prime

param profit {prod};        # profitti
param qnt {raw};            # quantità materie prime disponibili
param recipe {prod, raw};   # ricetta

var x {prod} >= 0;      # v. decisionale, quanto produrre di prodotto i

maximaze tot_prof : sum {i in prod} profit[i] * x[i];

# abbiamo un limite per ogni materia prima
subject to raw_limit {j in raw} : sum {i in prod} recipe[i,j] * x[i] <= qnt[j]
```

```bash
# es1.dat
set prod := T1 T2;
set raw := water apple;

param : profit :=
    T1  0.25
    T2  0.75;

param : qnt :=
    water   30000
    apple    3600;

param recipe : water apple :=
    T1      30       2 
    T2      20      12;
```

EASY!

#### Esercizio 3/4
In questo eserizio viene mostrata la differenza sostanziale che esiste tra un problema di programmazione lineare che ha a che fare con variaibli continue (caso facile), e uno stesso problema che ha a che fare con *variaibli intere* (?).

##### Parte 1
- Un'azienda ha $n$ depositi e $m$ punti vendita.
- Da ogni deposito $i=1..n$ deve trasferire $a_i$ quantità di merce.
- A ogni punto vendita $j=1..m$ devono arrivare $b_j$ unità di merce.
- Trasportare *una unità di merce* dal depositio $i$ al punto vendita $j$ costa $c_{ij}$ (**costo variaible**).

**D**: Determinare come rifornire i punti vendita dai depositi **minimizzando** il costo di trasporto, dati i seguenti parametri:
- Depositi $n=2$: $a_1=10$ e $a_2 = 15$.
- Punti vendita $m=3$: $b_1=5$, $b_2 = 12$ e $b_3 = 8$.
- Costi per i trasporti:
  - Deposito 1: $c_{11} = 100$, $c_{12} = 300$ e $c_{13}=500$.
  - Deposito 2: $c_{21} = 200$, $c_{22} = 400$ e $c_{23}=600$.

Si determina subito il modello di programmazione lineare:
$$
\begin{align*}
    & z = \text{Min}\sum_{i=1}^{n}{\sum_{j=1}^{m}{c_{ij}x_{ij}}} \\
    & \qquad s.t. \\
    & \qquad \qquad \sum_{j=1}^{m}{x_{ij}} = a_j & i=1..n \\
    & \qquad \qquad \sum_{i=1}^{n}{x_{ij}} = b_j & j=1..m \\
    & \qquad \qquad x_{ij} \geq 0 & i=1..n,\quad j=1..m
\end{align*}
$$

- Da notare che è necessario che $\sum_{i=1}^{n}a_i = \sum_{j=1}^{m}b_j$ affinché non si abbiano sbilanciamenti. In caso contrario una possibile soluzione sarebbe quella di generare dalla parte sbilanciata un oggetto **dummy** per poter mantenere il vincolo soddisfatto, dove per non interferire con gli *archi* (collegamento da magazzino $i$ a punto vendita $j$) vengono settati con costo $c_{ij}$ pari a 0. Penso che lo rivedremo più avanti.
- Basta che solo $b_j$ e $a_i$ siano interi per ottenere una **soluzione intera** (lo vedremo più avanti il perché).

Traducendo il modello per AMPL si ottiene:
```bash
# es3.mod

set depot;      # depositi
set pdv;        # punti vendita

param disp {depot};         # disponibilità dei depositi
param req {pdv};            # richieste dei punti vendita
param cost {depot, pdv};    # costi da deposito i a pdv j

var x {depot, pdv} >= 0; # quantità trasportata dal deposito i al pdv j

minimize tot_cost : sum {i in depot} sum {j in pdv} cost[i,j] * x[i,j];

subject to depot_limit {i in depot} : sum {j in pdv} x[i,j] = disp[i];
subject to req_limit {j in pdv} : sum {i in depot} x[i,j] = req[j];
```
Mentre il file dati può essere scritto come:
```bash
# es3.dat

set depot := depBO depMI;
set pdv := pdvFI pdvRM pdvNA;

param : disp :=
    depBO 10
    depMI 15;

param : req :=
    pdvFI  5
    pdvRM 12
    pdvNA  8;

param cost : pdvFI pdvRM pdvNA :=
    depBO     100   300   500
    depMI     200   400   600
```

##### Parte 2
Come cambia il problema dell'esercizio precedente se per essere abilitato a trasportare una qualunque quantità di merce dal deposito $i$ al punto vendita $j$ bisogna pagare un costo fisso $f_{ij}$?

Per quanto possa sembrare una cazzata, con questo vincolo il problema che prima era facile ora diventa difficilissmo ($\in \text{NP}$).

Questo succede poiché durante la risoluzione del problema, vengono rilassati i vincoli di interezza, che portano il problema ad un cattivo *bounding* che può essere addirittura molto lontano dalla soluzione ottima, le soluzioni trovate potrebbero discostarsi tanto dalla soluzione migliore. 

Viene quindi aggiunta una nuova variabile decisionale al modello di prima, $y_{ij}$ che sta ad indicare quanti mezzi vengono impiegati per effettuare il viaggio dal deposito $i$ al punto vendita $j$. Questa variaible necessità del vincolo di non negatività e di **interezza**. È inoltre necessario definire un limite ad ogni mezzo impiegato di quante unità può trasportare, modellato da $u_{ij}$.

Il modello ora assume questa forma:
$$
\begin{align*}
    & z = \text{Min}\sum_{i=1}^{n}{\sum_{j=1}^{m}{c_{ij}x_{ij}} + f_{ij}y_{ij}} \\
    & \qquad s.t. \\
    & \qquad\qquad \sum_{j=1}^{m}{x_{ij} = a_i}      & i=1..n \\
    & \qquad\qquad \sum_{i=1}^{n}{x_{ij} = b_j}      & j=1..m \\
    & \qquad\qquad 0 \leq x_{ij} \leq u_{ij}y_{ij}   & i=1..n, \quad j=1..m \\
    & \qquad\qquad y_{ij} \geq 0 \quad \text{intero}          & i=1..n, \quad j=1..m
\end{align*}
$$

La soluzione in AMPL viene modificata come segue:
```bash
# es3-2.mod

set depot;
set pdv;

param disp {depot};
param req {pdv};
param cost {depot, pdv};
param fixcost {depot, pdv}
param cap {depot, pdv}

var x {depot, pdv} >= 0;
var y {depot, pdv} integer >= 0;

minimize tot_cost : sum {i in depot} sum {j in pdv} (cost[i,j] * x[i,j]) + (fixcost[i,j] * y[i,j])

subject to depot_limit {i in depot} : sum {j in pdv} x[i,j] = disp[i];
subject to pdv_limit {j in pdv} : sum {i in depot} x[i,j] = req[j];
subject to cap_limit {i in depot, j in pdv} : x[i,j] <= cap[i,j] * y[i,j]
```
che prevede di caricare i seguenti dati:
```bash
set depot := depBO depMI
set pdv := pdvFI pdvRM pdvNA

param : disp :=
    depBO   10
    depMI   15;

param : req 
    pdvFI   5
    pdvRM   12
    pdvNA   8;

param cost : pdvFI pdvRM pdvNA :=
    depBO     100   300   500
    depMI     200   400   600

param fixcost : pdvFI pdvRM pdvNA :=
    depBO       1000  1000  1000
    depMI       1000  1000  1000

param cap : pdvFI pdvRM pdvNA :=
    depBO     8     8     8
    depMI     8     8     8
```

Nota: avendo in posto il vincolo di interezza nella variabile $y$, i tempi d'esecuzione possono prolonguarsi notevolemnte, ed essendo il problema $\in \text{NP}$, non è detto che venga fornita dal solver la soluzione ottima. In caso, viene fornita, oltre alla soluzione calcolata, la distanza dalla soluzione ottima.

### Intelligenza Artificiale

Molti plrobemi relativi al supporto delle decisioni possono essere risolti con **la programmazione matematica** e **l'ottimizzazione combinatoria**.

L'intelligenza artificiale copre l'area degli *algoritmi euristici*.

Il *machine learning* può utilizzare due approcci:
* supervisionato
* non-supervisionato

### Regressione
Una *regressione* ci permette di costruire quelle funzioni che dovrebbero approssimare il comportamento del fenomeno di nostro interesse. 
