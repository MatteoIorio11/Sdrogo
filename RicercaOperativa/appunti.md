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

I *modelli* sono una rappresentazione, spesso semplificata, di concetti. I modelli possono riguardare sia aspetti puramente teorici che del mondo reale. 
I modelli possono essere di tipo : verbale, grafico, fisico, matematico ecc ecc..

Attraverso l'utilizzo dei modelli è possibile perseguire i seguenti obbiettivi: 
1. **Facilitare la comprensione**, identificando le componenti
2. **Spiegare, controllare e predire eventi**, anche sulla base di osservazioni passate
3. **Supportare i processi decisionali**

Ciò che deve essere rappresentato all'interno di un modello può essere composto da molte componenti, di conseguenza è necessario effettuare delle **semplificazioni** al modello, che non *interferiscano* con l'utilizzo che se ne vuole fare. Non bisogna adottare modelli complicatissimi. 

Attraverso il **Modello Matematico** è possibile rappresentare la realtà di interesse con un alto grado di astrazione. I modelli matematici prevedono l'uso di parametri.

Nel caso in cui i parametri possano essere definiti con esattenza siamo nel caso di **modelli deterministici**, nel caso in cui i parametri non siano certi siamo nel caso di **modelli stocastici** (modelli in cui i parametri non sono stati definiti a priori).

I *modelli stocastici* sono difficili da risolvere, perciò spesso ci si porta a *modelli deterministici*, enumerando degli scenari rappresentativi della realtà di interesse. 

Le approssimazioni nei parametri dei modelli possono portare ad errori nel calcolo, andando a sporcare di conseguenza la validità dell'output.

### Approssimazioni di un Modello
Prima del calcolo:
1. modello 
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
3. Problema di **Enumerazione**: data un'istanza si vuole determinare tutte le possibili soluzioni
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



