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

Un problema decisionale F:I &rarr; {0,1} è *riducibile polinomialmente* a g:I &rarr; {0,1} se esiste una funzione "h" calcolabile in tempo polinomiale. **In sostanza se la soluzione si può controllare in tempo polinomiale**. 


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
In generale mediante l'ottimizzazione non vincolata, stiamo ottimizzando una funzione senza la presenza generale di ulteriori vincoli sulle nostre incognite (il prezzo deve essere maggiore di una determinata soglia, ecc ecc).
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

Esiste un **vincolo di budget** di 475$

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
$$10x_{A,B} + 20x_{A,D} + 5x_{C,B} + 10x_{C,D} = 475$$.

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