**Contenuto**
- [[#Introduzione|Introduzione]]
	- [[#Introduzione#Linguaggi|Linguaggi]]
	- [[#Introduzione#Algoritmi, Calcolabilità e Macchine di Turing|Algoritmi, Calcolabilità e Macchine di Turing]]
	- [[#Introduzione#Logiche Temporali|Logiche Temporali]]
- [[#Linguaggi Regolari|Linguaggi Regolari]]
	- [[#Linguaggi Regolari#Concetti base|Concetti base]]
	- [[#Linguaggi Regolari#Automi a Stati Finiti|Automi a Stati Finiti]]
		- [[#Automi a Stati Finiti#Automi a Stati Finiti *Deterministici*|Automi a Stati Finiti *Deterministici*]]
			- [[#Automi a Stati Finiti *Deterministici*#Riconoscimento di **Stringhe**|Riconoscimento di **Stringhe**]]
			- [[#Automi a Stati Finiti *Deterministici*#Tecnica Induttiva|Tecnica Induttiva]]
		- [[#Automi a Stati Finiti#Automi a Stati Finiti *Non Deterministici*|Automi a Stati Finiti *Non Deterministici*]]
	- [[#Linguaggi Regolari#Equivalenza tra Automi|Equivalenza tra Automi]]
		- [[#Equivalenza tra Automi#Teoremi random su DFA $\rightarrow$ NFA|Teoremi random su DFA $\rightarrow$ NFA]]
			- [[#Teoremi random su DFA $\rightarrow$ NFA#**Teorema 2.11**:|**Teorema 2.11**:]]
			- [[#Teoremi random su DFA $\rightarrow$ NFA#**Teorema 2.12**:|**Teorema 2.12**:]]
	- [[#Linguaggi Regolari#Transizioni $\epsilon$|Transizioni $\epsilon$]]

---

# Linguaggi Compilatori e Modelli Computazionali
## Introduzione
Il corso si occupa di coprire 3 branche principali:
- **Linguaggi**
- **Compilatori**
- **Modelli Computazionali**

### Linguaggi
I linguaggi di programmazione prendono spunto dai linguaggi naturali, e sono uno strumento per descrivere in modo *rigoroso* come risolvere *problemi*, in modo tale che questi possano essere poi risolti da un **esecutore automatico**.
Dietro le quinte, la componente fondamentale di un linguaggio di programmazione è il **compilatore**, il quale ha il compito di tradurre il linguaggio di programmazione in linguaggio macchina comprensibile dall'esecutore automatico (i.e. CPU).
Il compilatore si compone prima di tutto di un **parser**, le quali regole si distinguono in:
- *Regole* **Lessicali**: come viene composta una parola a partire dalle lettere.
- *Regole* **Sintattiche**: come viene composta una frase a partire dalle parole.
- *Regole* **Semantiche**: nell'ambito dei compilatori, è qui che risiedono le regole di type checking.

Successivamente il compilatore è composto da una componente *pluggable* (cioè quindi indipendente dal parser) in grado di generare codice comprensibile all'esecutore automatico (per la CPU il linguaggio macchina).

Oggi si creano parser/compilatori grazie a strumenti di **generazione automatica** del codice con un approccio dichiarativo dove si specifica
- **lessico**: **espressioni regolari** (o *automi a stati finiti*)
- **sintassi**: **grammatiche** (o *automi a pila*)

**Automa a stati finiti**: è un modello per descrivere **situazioni** di **calcolo** in cui si **consumano informazioni una alla volta**, e durante la consumazione si memorizzano **quantità finite di informazioni**. Sono utilizzati nell'ambito dei compilatori per:
- Analizzatori lessicali.
- **Model checking** (software per la verifica di un sistema).

### Algoritmi, Calcolabilità e Macchine di Turing
Secondo la **tesi Turing-Church**, ogni problema **calcolabile** da un algoritmo/procedura può essere risolto da una **macchina di Turing**: modello matematico di un semplice esecutore automatico.
È importante quindi notare come non tutti i problemi siano **calcolabili** da un algoritmo/macchina di Turing.

Con i sistemi software moderni (e.g. distribuiti, concorrenti, a microservizi, …) si supera il paradigma del modello funzionale delle macchine di Turing (ovvero non si riesce più a ricondurre il problema originario ad una funzione $f:\mathbb{N} \rightarrow \mathbb{N}$).

### Logiche Temporali
Le **logiche temporali** permettono di esprimere delle **proprietà**. Nell'ambito dei **model checker**, essi verificano se proprietà espresse tramite logiche temporali valgono oppure no.

---
## Linguaggi Regolari
### Concetti base
- **Alfabeto**: insieme **finito** e non vuoto di **simboli** (indicato con: $\Sigma$)
- **Stringa**: sequenza **finita** di simboli da un alfabeto
	- *Stringa vuota*, stringa con zero occorrenze di simboli da $\Sigma$, indicata con $\epsilon$.
	- *Lunghezza di una Stringa*: numero di posizioni per i simboli nella stringa, indicato con $|w|$ lunghezza di $w$.
- **Potenze di un alfabeto**: $\Sigma^k$ è l'insieme delle stringhe di lunghezza $k$ con simboli da $\Sigma$
	- $\Sigma^0 = \{\epsilon\}$ è detto anche **singoletto epsilon**.
 - $\Sigma^* = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \dots = \bigcup_{i \geq 0} \Sigma^i$
	 - $\Sigma^*$ è l'insieme di tutte le stringhe su $\Sigma$.
	 - $\Sigma^+ = \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cup \dots$  è detta anche Sigma con *chiusura positiva*, ovvero è l'insieme che esclude il singoletto epsilon.
	 - Quindi si ha che $\Sigma^* = \{\epsilon\} \cup \Sigma^+$
- **Concatenazione** di stringhe: Se $x$ e $y$ sono due stringhe, allora $xy$ è la stringa ottenuta collocando una copia di $y$ subito dopo una copia di $x$.
	- NB: per ogni stringa $x$ vale $x\epsilon = \epsilon x = x$ ($\epsilon$ elemento neutro).
- **Linguaggi**: Se $\Sigma$ è un alfabeto e $L \subseteq \Sigma^*$, allora $L$ è un **linguaggio**.
	- Linguaggi in po' particolari sono:
		- Linguaggio vuoto $\emptyset$
		- Il linguaggio $\{\epsilon\}$ contenente solo la stringa vuota.
		- NB: $\emptyset \neq \{\epsilon\}$

---
### Automi a Stati Finiti
#### Automi a Stati Finiti *Deterministici*
Un DFA viene definito da:
$$A = (Q, \Sigma, \delta, q_0, F)$$
Dove:
- $Q$: insieme *finito* di **stati**.
- $\Sigma$: **alfabeto** *finito*
- $\delta$: **funzione di transizione** da $Q\times\Sigma$ a $Q$, i.e. $(q,a) \rightarrow p$.
- $q_0 \in Q$: stato *iniziale*.
- $F \subseteq Q$ è un **insieme** di *stati finali*/*accettazione*.

##### Riconoscimento di Stringhe
Un automa a stati finiti *accetta una stringa* $w=a_1a_2\dots a_n$ se **esiste un cammino** nel **diagramma di transizione** che:
1. Inizia nello stato iniziale
2. Finisce in uno stato di accettazione
3. Ha una sequenza di etichette $a_1a_2\dots a_n$

##### Tecnica Induttiva
La funzione di transizione $\delta$ può essere estesa a $\hat{\delta}$ che opera su **stati** e **stringhe**.

**Base**: $$\hat{\delta}(q, \epsilon) = q$$
**Induzione**: $$\hat{\delta}(q, xa) = \delta(\hat{\delta}(q_0, x), a)$$

Quindi in parole povere, applichiamo ricorsivamente la funzione $\delta$ all'ultimo carattere della stringa in input ($a$) per passi successivi, concatenando il risultato dell'applicazione della funzione $\hat{\delta}$ al resto della stringa ($x$).

Il **linguaggio** accettato da un automa a stati finiti deterministico $A$ è: 
$$L(A) = \{w : \hat{\delta}(q_0, w) \in F\}$$

I linguaggi accettati da automi a stati finiti sono detti **linguaggi regolari**.

#### Automi a Stati Finiti *Non Deterministici*
Un NFA accetta una stringa se, **tra i tanti possibili**, esiste un **cammino** che conduce ad uno stato finale. 
A differenza dei DFA, gli stati dei NFA possono bloccarsi se per dei simboli dell'alfabeto non sono definite transizioni e stati.

Un NFA è quindi rappresentabile come:
$$A = (Q, \Sigma, \delta, q_0, F)$$
Dove:
- $Q$: insieme *finito* di **stati**.
- $\Sigma$: **alfabeto** *finito*
- $\delta$: **funzione di transizione** da $Q\times\Sigma$ all'**insieme dei sottoinsiemi** di $Q$, i.e. $(q, a) \rightarrow Q'$ con $Q' \subseteq Q$.
- $q_0 \in Q$: stato *iniziale*.
- $F \subseteq Q$ è un **insieme** di *stati finali*/*accettazione*.

Come per i DFA possiamo estendere la funzione di transizione per accettare intere stringhe attraverso il metodo induttivo:
**Base**: $$\hat{\delta}(q, \epsilon) = \{q\}$$
**Induzione**: $$\hat{\delta}(q, xa) = \bigcup_{p\in \hat{\delta}(q,x)} \delta(p,a)$$

Quindi in parole povere ad ogni passo induttivo si calcolano i valori di delta per ogni stato all'interno del sottoinsieme di stati ricavato al passo successivo, per così ricavare il nuovo sottoinsieme di stati.

Un **linguaggio accettato** da un automa a stati finiti non deterministico $A$ è 
$$L(A) = \{w: \hat{\delta}(q_0, w) \cap F \neq \emptyset\}$$

Ovvero il linguaggio è un insieme di sottoinsiemi validi per l'automa dopo aver consumato l'intera stringa $w$, nei quali è contenuto uno stato di accettazione.

### Equivalenza tra Automi
Per ogni NFA $N$ c'è un DFA $D$, tale che $L(D) = L(N)$, ovvero che entrambi gli automi riconoscono la stessa classe di linguaggi.
Possiamo quindi costruire un DFA a partire da un NFA nel seguente modo:
- Dato NDA: $N = (Q_N, \Sigma, \delta_N, q_0, F_N)$
- Costruiremo un DFA: $D = (Q_D, \Sigma, \delta_D, \{q_0\}, F_D)$
- Tali che $L(D) = L(N)$
- Impieghiamo il metodo di **costruzione a sottoinsiemi** definito come:
	- Sia $Q_D = \{S : S \subseteq Q_N\}$ cioè l'insieme dei possibili sottoinsiemi $S$ degli stati non deterministici. Di norma li prendiamo tutti, anche se molti stati non sono raggiungibili (detti anche stati *garbage*). In questo caso quindi avremmo che $|Q_D| = 2^{|Q_N|}$.
	- Sia $F_D = \{S \subseteq Q_N : S \cap F_N \neq \emptyset \}$, cioè tutti i possibili sottoinsiemi di NFA che contengono stati di accettazione.
	- Per ogni $S\subseteq Q_N$ e $a \in \Sigma$:
$$\delta_D(S, a) = \bigcup_{p \in S}\delta_N(p,a)$$

Che in italiano è che la funzione di transizione del DFA, a partire da uno dei sottoinsiemi S (contenuto in $Q_N$) e il carattere $a$, viene generata calcolando il valore della funzione di transizione dell'NFA per ogni stato $p \in S$ con il carattere $a$, e ognuno di questi risultati viene unito tra loro.

In generale possiamo evitale la crescita esponenziale degli stati del DFA, prendendo solo gli stati **$S$ accessibili** come segue:
**Base**: $S = \{q_0\}$ è accessibile in $D$
**Induzione**: Se lo stato $S$ è accessibile, lo sono anche gli stati $\delta(S, a), \forall a \in \Sigma$, ovvero tutti gli stati che sono raggiungibili attraverso una transizione che parte da $S$.

#### Teoremi random su DFA $\rightarrow$ NFA
##### **Teorema 2.11**:
> Sia $D$ Il DFA Ottenuto da un NFA $N$ con la costruzione a sottoinsiemi. Allora L(D) = L(N).

##### **Teorema 2.12**:
> Un linguaggio $L$ è accettato da un DFA se e solo se $L$ è accettato da un NFA.

### Transizioni $\epsilon$
Un $\epsilon$-NFA può consumare anche la stringa vuota '$\epsilon$'. Un $\epsilon$-NFA è una quintupla $(Q, \Sigma, \delta, q_0, F)$ dove $\delta$ è una funzione da $Q \bigtimes (\Sigma \cup \{\epsilon\})$ all'insieme dei sottoinsiemi Q. Ora uno stato può essere raggiunto anche tramite $\epsilon$ e basta. 

### Epsilon chiusura

Chiudiamo uno stato aggiungendo tutti gli stati raggiungibili da lui tramite una sequenza $\epsilon\epsilon\epsilon...\epsilon$. Sono tutti gli stati, includendo anche quello di partenza, che riesco a raggiungere consumando solamente la stringa $\epsilon$. 

Si definisce come *ECLOSE(q)*. 

**Base:**

$$q \in \text{ECLOSE}(q)$$

**Induzione:**
$$p \in \text{ECLOSE}(q) \text{ and } r \in \delta(p, \epsilon) \Rightarrow r \in \text{ECLOSE}(q)$$

* Definizione *induttiva* di $\hat \delta$ per automi $\epsilon$-NFA
**Base:**
$$\hat \delta(q, \epsilon) = \text{ECLOSE}(q)$$ **Induzione:**
$$\hat \delta(q, xa) = \bigcup_{p \in \hat \delta(q,x)} ( \bigcup_{t \in \delta(p, a)}\text{ECLOSE}(t) ) $$
## Equivalenza DFA e $\epsilon$-NFA

Dato un $\epsilon$-NFA
$$E=(Q_E, \Sigma, \delta_E, q_0, F_E)$$ costruiremo un DFA
$$D = (Q_D, \Sigma, \delta_D, q_D, F_D)$$
tale che
$$L(D)=L(E)$$
Se vuoi vedere i dettagli vai su 'Linguaggi regolari > pag 30'
##### **Teorema 2.22**:
> Un linguaggio *L* è accettato da un $\epsilon$-NFA *E* se e solo se *L* è accettato da un DFA

## Espressioni regolari

Un *FA* (*NFA* o *DFA*) è un metodo per costruire una macchina che riconosce linguaggi regolari. Una *espressione regolare* è un *modo dichiarativo* per descrivere un linguaggio regolare. Non c'è bisogno di realizzare un automa ma lo si può descrivere tramite una formula. Esempio: $01^\text{*} + 10^\text{*}$ 

### Operazioni sui linguaggi

* *Unione*
$$ L \cup M = \{w: w \in L \text{ o } w \in M \}$$
* *Concatenazione*
$$LM = \{ w: w=xy, x \in L, y \in M \}$$
* *Potenze*
$$L^0 = \{ \epsilon \}, \space L^1=L, \space L^{k+1} = LL^k $$
* *Chiusura di Kleene*
$$L^{*} = \bigcup_{i=0}^{\infty} L^i \Rightarrow L^0 \cup L^1 \cup L^2 ...$$
### Leggi algebriche per i linguaggi

* L'unione è **commutativa**: $L \cup M = M \cup L$
* L'unione è **associativa**: $(L \cup M) \cup N = L \cup (M \cup N)$
* $\emptyset$ è l'**identità** per l'unione: $\emptyset \cup L = L \cup \emptyset = L$
* {$\epsilon$} è l'**identità** sinistra e destra per la concatenazione: $\{\epsilon\}L=L\{\epsilon\} = L$
* $\emptyset$ è l'**annichilatore** sinistro e destro per la concatenazione: $\emptyset L = L\emptyset=\emptyset$
* La *concatenazione* è **distributiva** a sinistra sull'unione: $L(M \cup N) = LM \cup LN$
* La *concatenazione* è **distributiva** a destra dell'unione: $(M \cup N) L = ML \cup NL$
* L'unione è **idempotente**: $L \cup L=L$
* $\emptyset^{*} = \{\epsilon\}$
* $\{\epsilon\}^{*}=\{\epsilon\}$
* $L^{+} = LL^{*} = L^{*}L,\space L^{*}=L^{+}\cup\{\epsilon\}$
* $(L^{*})^{*}$
* La concatenazione è **associativa**: $(LM)N = L(MN)$
La concatenazione **non è commutativa**, cioè esistono *L* e *M* tali che $LM \neq ML$, dal momento in cui ottengo stringhe completamente diverse. 

## Costruire le espressioni regolari

**Base:**
$\epsilon$ e $\emptyset$ sono espressioni regolari, $L(\epsilon)=\{\epsilon\}$, e $L(\emptyset) = \emptyset$ 
Se $a \in \Sigma$ allora $a$ è una espressione regolare $L(a) = \{a\}$. 
**Induzione:**
* Se *E* è una espressione regolare, allora *(E)* è una espressione regolare $L((E)) = L(E)$
* Se *E* e *F* sono espressioni regolari, allora $E + F$  è una espressione regolare $L(E + F) = L(E) \cup L(F)$ (unione delle due espressioni)
* Se *E* e *F* sono espressioni regolari, allora $EF$ è una espressione regolare $L(EF)= L(E)L(F)$ 
* Se *E* è una espressione regolare, allora $E^{*}$ è una espressione regolare $L(E^{*}) = (L(E^{*}))$ (tutte le stringhe)

## Equivalenza di FA e espressioni regolari

Abbiamo già detto che *DFA*, *NFA*  e $\epsilon$-NFA sono tutti equivalenti, partendo da un qualsiasi automa riesco a ricavare tutti gli altri. 
1) Per ogni *DFA* *A* possiamo trovare un'espressione regolare R tale che $L(R) = L(A)$
2) Per ogni espressione regolare R esiste un $\epsilon$-NFA A, tale che $L(A) = L(R)$

### Da DFA a espressioni regolari
##### **Teorema 3.4**:
> Per ogni DFA $A=(Q, \Sigma, \delta, q_0, F)$ esiste una espressione regolare R, tale che $L(A) = L(R)$.

L'automa lo si trasforma etichettando gli archi con espressioni regolari di simboli dell'alfabeto. 

La procedura è piuttosto semplice, consiste nell'**eliminare** uno *stato* alla volta (escludendo lo stato inizia e gli stati finali). 
1) Devo individuare lo stato da rimuovere, una volta scelto individuo:
	* predecessori (frecce entranti nello stato)
	* successori (frecce uscenti dallo stato)
2) Una volta rimosso lo stato etichetto le transizioni con espressioni regolari, prendo i valori delle transizioni dei valori precedenti ed i valori delle transizioni successive e le **concateno**. 

Una volta rimossi tutti gli archi che non ci interessano saremo rimasto solamente con due forme: 
1) La prima forma che possiamo ottenere è quella in cui lo stato iniziale non è l'unico stato rimanente. In questo caso l'espressione regolare che si ottiene è: $E_q=(R + SU^{*}T)^{*}SU^{*}$. Dove $(R + SU^{*}T)^{*}$ lo si può interpretare come l'esecuzione di un avanti e indietro tra lo stato iniziale e lo stato di accettazione, mentre la parte finale $SU^{*}$ è il momento in cui ci si consuma definitivamente l'intera stringa e si rimane nello stato di accettazione. 
$$E_q=(R + SU^{*}T)^{*}SU^{*}$$
![Prima forma dopo la cancellazione degli stati "non utili"](Compilatori/images/prima_forma_er.png)

2)  La seconda forma che possiamo ottenere invece è un unico stato che rappresenta sia lo stato iniziale che lo stato finale. In questo caso l'espressione regolare è $E_q=R$
$$E_q=R$$
![Alt Text](Compilatori/images/seconda_forma_er.png)

