**Contenuto**
- [[#Introduzione|Introduzione]]
	- [[#Introduzione#Linguaggi|Linguaggi]]
	- [[#Introduzione#Algoritmi, Calcolabilità e Macchine di Turing|Algoritmi, Calcolabilità e Macchine di Turing]]
	- [[#Introduzione#Logiche Temporali|Logiche Temporali]]
- [[#Linguaggi Regolari|Linguaggi Regolari]]
	- [[#Linguaggi Regolari#Concetti base|Concetti base]]
	- [[#Linguaggi Regolari#Automi a Stati Finiti|Automi a Stati Finiti]]
		- [[#Automi a Stati Finiti#Automi a Stati Finiti *Deterministici*|Automi a Stati Finiti *Deterministici*]]
			- [[#Automi a Stati Finiti *Deterministici*#Riconoscimento di Stringhe|Riconoscimento di Stringhe]]
			- [[#Automi a Stati Finiti *Deterministici*#Tecnica Induttiva|Tecnica Induttiva]]
		- [[#Automi a Stati Finiti#Automi a Stati Finiti *Non Deterministici*|Automi a Stati Finiti *Non Deterministici*]]
	- [[#Linguaggi Regolari#Equivalenza tra Automi|Equivalenza tra Automi]]
		- [[#Equivalenza tra Automi#Teoremi random su DFA $\rightarrow$ NFA|Teoremi random su DFA $\rightarrow$ NFA]]
			- [[#Teoremi random su DFA $\rightarrow$ NFA#**Teorema 2.11**:|**Teorema 2.11**:]]
			- [[#Teoremi random su DFA $\rightarrow$ NFA#**Teorema 2.12**:|**Teorema 2.12**:]]
	- [[#Linguaggi Regolari#Transizioni $\epsilon$|Transizioni $\epsilon$]]
	- [[#Linguaggi Regolari#Epsilon chiusura|Epsilon chiusura]]
- [[#Equivalenza DFA e $\epsilon$-NFA|Equivalenza DFA e $\epsilon$-NFA]]
	- [[#Equivalenza DFA e $\epsilon$-NFA#**Teorema 2.22**:|**Teorema 2.22**:]]
- [[#Espressioni regolari|Espressioni regolari]]
	- [[#Espressioni regolari#Operazioni sui linguaggi|Operazioni sui linguaggi]]
	- [[#Espressioni regolari#Leggi algebriche per i linguaggi|Leggi algebriche per i linguaggi]]
- [[#Costruire le espressioni regolari|Costruire le espressioni regolari]]
- [[#Equivalenza di FA e espressioni regolari|Equivalenza di FA e espressioni regolari]]
	- [[#Equivalenza di FA e espressioni regolari#Da DFA a espressioni regolari|Da DFA a espressioni regolari]]
		- [[#Da DFA a espressioni regolari#**Teorema 3.4**:|**Teorema 3.4**:]]
- [[#Da espressioni regolari a $\epsilon$-NFA|Da espressioni regolari a $\epsilon$-NFA]]
	- [[#Da espressioni regolari a $\epsilon$-NFA#Teorema 3.7:|Teorema 3.7:]]
- [[#Proprietà dei linguaggi regolari|Proprietà dei linguaggi regolari]]
	- [[#Proprietà dei linguaggi regolari#Pumping Lemma|Pumping Lemma]]
		- [[#Pumping Lemma#Teorema 4.1|Teorema 4.1]]
	- [[#Proprietà dei linguaggi regolari#Proprietà di Chiusura|Proprietà di Chiusura]]
		- [[#Proprietà di Chiusura#Teorema 4.4 (Unione)|Teorema 4.4 (Unione)]]
		- [[#Proprietà di Chiusura#Teorema 4.5 (Complemento)|Teorema 4.5 (Complemento)]]
		- [[#Proprietà di Chiusura#Teorema 4.8 (Intersezione)|Teorema 4.8 (Intersezione)]]
			- [[#Teorema 4.8 (Intersezione)#Prova con DeMorgan|Prova con DeMorgan]]
			- [[#Teorema 4.8 (Intersezione)#Prova con Simulazione Parallela|Prova con Simulazione Parallela]]
		- [[#Proprietà di Chiusura#Teorema 4.10 (Differenza)|Teorema 4.10 (Differenza)]]
		- [[#Proprietà di Chiusura#Teorema 4.11 (Reverse)|Teorema 4.11 (Reverse)]]
	- [[#Proprietà dei linguaggi regolari#Proprietà di Decisione|Proprietà di Decisione]]
		- [[#Proprietà di Decisione#Testare se un linguaggio è vuoto|Testare se un linguaggio è vuoto]]
		- [[#Proprietà di Decisione#Testare l'Appartenenza|Testare l'Appartenenza]]
	- [[#Proprietà dei linguaggi regolari#Equivalenza e Minimizzazione di automi|Equivalenza e Minimizzazione di automi]]
		- [[#Equivalenza e Minimizzazione di automi#Algoritmo Riempi-Tabella|Algoritmo Riempi-Tabella]]
			- [[#Algoritmo Riempi-Tabella#Spiegazione di come il prof vuole che la facciamo|Spiegazione di come il prof vuole che la facciamo]]
		- [[#Equivalenza e Minimizzazione di automi#Classi di Equivalenza|Classi di Equivalenza]]
		- [[#Equivalenza e Minimizzazione di automi#Equivalenza tra Automi|Equivalenza tra Automi]]
		- [[#Equivalenza e Minimizzazione di automi#Minimizzazione di Automi|Minimizzazione di Automi]]
- [[#Linguaggi Liberi dal Contesto|Linguaggi Liberi dal Contesto]]
	- [[#Linguaggi Liberi dal Contesto#Definizione|Definizione]]
	- [[#Linguaggi Liberi dal Contesto#Derivazione|Derivazione]]
		- [[#Derivazione#Derivazione a Sinistra e Destra|Derivazione a Sinistra e Destra]]
	- [[#Linguaggi Liberi dal Contesto#Il linguaggio di una Grammatica|Il linguaggio di una Grammatica]]
	- [[#Linguaggi Liberi dal Contesto#Alberi Sintattici|Alberi Sintattici]]
		- [[#Alberi Sintattici#Costruzione|Costruzione]]
		- [[#Alberi Sintattici#Prodotto di un albero sintattico|Prodotto di un albero sintattico]]
		- [[#Alberi Sintattici#Alberi sintattici e Derivazioni|Alberi sintattici e Derivazioni]]
		- [[#Alberi Sintattici#Ambiguità in Grammatiche e Linguaggi|Ambiguità in Grammatiche e Linguaggi]]
			- [[#Ambiguità in Grammatiche e Linguaggi#Ambiguità e Derivazioni a Sinistra|Ambiguità e Derivazioni a Sinistra]]
				- [[#Ambiguità e Derivazioni a Sinistra#Teorema 5.29|Teorema 5.29]]

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

Chiudiamo uno stato aggiungendo tutti gli stati raggiungibili da lui tramite una sequenza $\epsilon\epsilon\epsilon…\epsilon$. Sono tutti gli stati, includendo anche quello di partenza, che riesco a raggiungere consumando solamente la stringa $\epsilon$. 

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
### **Teorema 2.22**:
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
$$L^{*} = \bigcup_{i=0}^{\infty} L^i \Rightarrow L^0 \cup L^1 \cup L^2 …$$
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
#### **Teorema 3.4**:
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

## Da espressioni regolari a $\epsilon$-NFA
### Teorema 3.7:
 > Per ogni espressione regolare *R* possiamo costruire un $\epsilon$-NFA A tale che *L(A)=L(R)* 

**Prova:**
Per induzione strutturale:
**Base:**
Automa per $\epsilon$, $\emptyset$ e $a$. Si lavora sempre con uno stato iniziale ed uno finale. 

**Induzione:**
Automa per $R+S$, $RS$ e $R^*$ :
+ Automa di $R+S$
![[Pasted image 20230927174812.png]]

* Automa di $RS$
![[Pasted image 20230927174916.png]]
* Automa di $R^*$
![[Pasted image 20230927174950.png]]
--- 
## Proprietà dei linguaggi regolari
* [[#Pumping Lemma]]: Ogni linguaggio regolare soddisfa il **pumping lemma**. Dato un linguaggio, se usando il pumping lemma si ottiene una contraddizione allora esso non è un linguaggio regolare
* [[#Proprietà di Chiusura]]: Come costruire automi da componenti usando delle operazioni e per le quali operazioni è possibile farlo. 
* [[#Proprietà di Decisione]]: Analisi computazionale di automi, ad esempio quando due automi sono equivalenti
* [[#Equivalenza e Minimizzazione di automi|Tecniche di minimizzazione]]: Possiamo risparmiare costruendo automi più piccoli

### Pumping Lemma
#### Teorema 4.1
> Il *Pumping Lemma* per linguaggi regolari.

Sia *L* un linguaggio regolare, allora $\exists \space n \geq 1$  (n è il numero di stati del DFA) che soddisfa ogni $w \in L : |w| \geq n$ è **scomponibile** in tre stringhe $w =xyz$ tali che:
1) $y \neq \epsilon$ (il corpo del ciclo ha almeno un simbolo)
2) $|xy| \leq n$ (arrivo al nodo in cui ho il ciclo)
3) $\forall k \geq 0, \space xy^kz \in L$ (il ciclo può essere ripetuto k volte, la stringa che si ottiene sarà sempre accettata dal linguaggio *L*)
**Prova:** Supponiamo che *L* sia regolare
Allora *L* è riconosciuto da un *DFA A*. Chiamo **n** il **numero degli stati** di A. 
* Sia $w=a_1a_2…a_m \in L, m \geq n$ 
* Sia $p_i = \hat \delta(q_0, a_1a_2…a_m)$ dove $q_0$ è lo stato iniziale di *A*
$\Rightarrow \exists \space i < j \leq n: p_i=p_j$ (entro **n** simboli trovo il nodo che mi fa entrare nel ciclo, in questi casi lo incontro ad un momento *i* della mia stringa per poi ritornarci al carattere *j*)

Ora $w=xyz$, dove:
* $x=a_1a_2…a_i$
* $y=a_{i+1}a_{i+2}…a_j$ (caratteri che itero sul ciclo)
* $z = a_{j+1}a_{j+2}…a_m$
![[Pasted image 20230927180536.png]]
Quindi anche $xy^kz \in L$, per ogni $k \geq 0$, inoltre $y \neq \epsilon$ e $|xy| \leq n$ poiché $i < j \leq n$. 

* L'idea di base è che ogni automa dispone di una memoria limitata, proprio per questo infatti non è possibile ricordare cosa è successo negli stati precedenti.  
### Proprietà di Chiusura
Con chiusura si intende la proprietà di un insieme di supportare un insieme di operazioni fondamentali. Per esempio, se si considera l'insieme dei numeri naturali $\mathbb{N}$, possiamo dire che è chiuso rispetto la somma (cioè $a + b=c \in \mathbb{N} \iff a,b\in \mathbb{N}$), ma non possiamo dire lo stesso della *differenza*, perché se il sottraendo è maggiore, il numero sarà negativo e quindi non appartenente a $\mathbb{N}$.

Per i linguaggi regolari, siano L e M due linguaggi regolari. Allora i seguenti linguaggi sono regolari:
- [[#Teorema 4.4 (Unione)|Unione]]: $L \cup M$.
- [[#Teorema 4.8 (Intersezione)|Intersezione]]: $L \cap M$
- [[#Teorema 4.5 (Complemento)|Complemento]]: $\overline{N}$
- [[#Teorema 4.10 (Differenza)|Differenza]]: $L \setminus M$
- [[#Teorema 4.11 (Reverse)|Inversione (Reverse)]]: $L^{R} = \{w^R : w \in L\}$
- **Chiusura**: $L^*$
- **Concatenazione**: $L.M$

#### Teorema 4.4 (Unione)
> Per ogni coppia di linguaggi regolari $L$ e $M$, $L \cup M$ è regolare.

**Prova**: prendiamo le espressioni regolari dei due linguaggi, rispettivamente $L = L(E)$ e $M = L(F)$.
Per definizione delle espressioni regolari $L(E + F) = L \cup M$.

#### Teorema 4.5 (Complemento)
> Sia $L$ un linguaggio regolare su $\Sigma$, allora anche $\overline{L} = \Sigma^* \setminus L$ è regolare.

**Prova**: Sia $L$ rappresentabile da un *DFA*: $A = (Q, \Sigma, \delta, q_0, F)$ e consideriamo un altro *DFA*  $B$ tale che:
$$B = (Q, \Sigma, \delta, q_0, Q\setminus F)$$
ovvero il DFA $A$ con gli stati di accettazione invertiti con gli stati di non accettazione. Allora vale $L(B) = L$.

#### Teorema 4.8 (Intersezione)
> Se $L$ e $M$ sono regolare allora anche $L \cap M$ è regolare.

##### Prova con DeMorgan
Per la legge di **DeMorgan** si ha $L \cap M = \overline{\overline{L}\cup \overline{M}}$.
È dimostrabile per il [[#Teorema 4.4 (Unione)|teorema 4.4]] che i linguaggi regolari sono chiusi rispetto l'unione e per il [[#Teorema 4.5 (Complemento)|teorema 4.5]] rispetto il complemento.

##### Prova con Simulazione Parallela
Siano $A_L$ e $A_M$ gli automi a stati finiti deterministici rispettivamente di $L$ e $M$, costruiti in questo modo:
- $A_L = (Q_L, \Sigma, \delta_L, q_L, F_L)$
- $A_M = (Q_M, \Sigma, \delta_M, q_M, F_M)$

Costruiamo un automa che **simula in parallelo** $A_L$ e $A_M$, il quale accetta se e solo se **sia** $A_L$ sia $A_M$ accettano.

Formalmente possiamo dire che la simulazione parallela modelli l'automa così definito:
$$A_{L\cap M}(Q_L \times Q_M, \Sigma, \delta_{L \cap M}, (q_L, q_M), F_L \times F_M)$$

dove $\delta_{L \cap M}((q_L, q_M), a) = (\delta_L(p, a), \delta_M(q,a))$ e mediante la solita dimostrazione induttiva si arriva a definire $\hat{\delta}$ come:

$$\hat{\delta}_{L \cap M}((q_L, q_M), w) = (\hat{\delta}_L(q_L, w),\hat{\delta}_M(q_M, w))$$

Tutto sto casino per dire che se $A_L$ va dallo stato $p$ allo stato $s$ leggendo $a$, e $A_M$ va dallo stato $q$ allo stato $t$ leggendo $a$, allora $A_{L \cap M}$ andrà dallo stato $(p,q)$ allo stato $(s,t)$ leggendo $a$. Si ha una condizione di accettazione **solo** quando la **coppia di stati di arrivo**  è costituita da **soli stati di accettazione**.

#### Teorema 4.10 (Differenza)
> Se $L$ e $M$ sono linguaggi regolari, allora anche $L \setminus M$ è regolare.

**Prova**: si osserva che $L \setminus M = L \cap \overline{M}$. Per il [[#Teorema 4.5 (Complemento)|teorema 4.5]] e [[#Teorema 4.8 (Intersezione)|teorema 4.8]] i linguaggi regolari sono chiusi rispettivamente per complemento e intersezione.

#### Teorema 4.11 (Reverse)
> Se $L$ è un linguaggio regolare, allora anche $L^R$ (linguaggio formato dalle stringhe lette all'inverso) è regolare.

**Prova**: Sia $L$ riconosciuto da un automa a stati finiti $A$ (non per forza deterministico quindi). Modifichiamo $A$ per renderlo un altro automa a stati finiti per $L^R$, in questo modo:
1. Invertiamo il senso di tutte le transizioni (gli archi).
2. Rendiamo il vecchio stato iniziale nell'unico stato finale.
3. Creiamo un nuovo stato iniziale $p_0$ con $\delta(p_0, \epsilon) = F$, ovvero colleghiamo $p_0$ con tutti i vecchi stati finali con una transizione $\epsilon$

### Proprietà di Decisione
Vogliamo capire 3 cose:
1. Come capire che un linguaggio è vuoto (i.e. $L = \emptyset$). [[#Testare se un linguaggio è vuoto|1]]
2. Come capire se una stringa appartiene ad un linguaggio (i.e. $w\in L$). [[#Testare l'appartenenza|2]]
3. Se è possibile che due descrizioni definiscano lo stesso linguaggio.

#### Testare se un linguaggio è vuoto
Quanti passi richiede questo test?

- $L(A) \neq \emptyset$ per automi a stati finiti $A$ se e solo se uno stato finale è raggiungibile dallo stato iniziale in $A$
	- $O(n^2)$ passi.
- Consideriamo un'espressione regolare $E$ di lunghezza $s$ e controllare se $L(E) = \emptyset$ in $O(s)$ passi, usando il seguente metodo:
	- $E = F + G$:  $L(E)$ è vuoto $\iff$ sia $L(F)$ sia $L(G)$ sono vuoti.
	- $E = F.G$: $L(E)$ è vuoto $\iff$ se $L(F)$ o $L(G)$ sono vuoti.
	- $E = F^*$: $L(E)$ non è **mai** vuoto poiché $\epsilon \in L(E)$.
	- $E = \epsilon$: $L(E)$ non è vuoto.
	- $E = a$: $L(E)$ non è vuoto.
	- $E = \emptyset$: $L(E)$ è vuoto.

#### Testare l'Appartenenza
Per controllare se $w \in L(A)$
- Per un DFA $A$, simuliamo $A$ su $w$.
	- Se $|w| = n$$O(n)$ passi.
- Per un NFA a $s$ stati
	- $O(ns^2)$ passi, perché potenzialmente ogni stato dell'NFA può portarmi ad al massimo altri $s$ stati.
- Per un $\epsilon$-NFA
	- Se si calcolano preventivamente tutti gli `ECLOSE`, $O(ns^2)$ passi.
- Per un espressione regolare $E$ di lunghezza $s$, possiamo prima convertirla in un $\epsilon$-NFA con $2s$ stati.
	- $O(ns^2)$ passi.

### Equivalenza e Minimizzazione di automi
Consideriamo un DFA $A = (Q, \Sigma, \delta, q_0, F)$ e $\{p,q\} \subseteq Q$. Possiamo dire che:
$$p\equiv q \iff \forall w \in \Sigma^* : \hat{\delta}(p,w)\in F \quad\text{and}\quad \hat{\delta}(q, w)\in F$$
Ovvero che due stati si dicono equivalenti se e solo se esiste una stringa $w$ che porta sia dallo stato $q$, sia dallo stato $p$ in uno stato di accettazione $\in F$.
- Se $p \equiv q$, $p$ e $q$ sono **equivalenti**.
- Se $p \not\equiv q$, $p$ e $q$ sono **distinguibili**.
	- Possiamo dire in modo più swag che $p$ e $q$ sono distinguibili se: $\exists w : \hat{\delta}(p,w), \in F$ e $\hat{\delta}(q, w) \not\in F$

#### Algoritmo Riempi-Tabella
Riempimi sto cazzo coglione.
Possiamo calcolare coppie di stati *distinguibili* con il metodo induttivo, detto algoritmo riempi tabella:
**Base**: Se $p \in F$ e $q \not\in F$, allora $p \not \equiv q$.
**Induzione**: Se $\exists a \in \Sigma : \delta(p, a) \not\equiv \delta(q,a )$, allora $p \not\equiv q$.

##### Spiegazione di come il prof vuole che la facciamo
![[Pasted image 20231003164945.png]]
Dividere il tutto in *passate* (sì, a lezione ha fatto la battuta "passata…di pomodoro", per questo ora si spiega la faccia di chad ciuchino).
1. Inizialmente, creo la griglia come una tabella con tutti gli stati su righe e colonne, una sorta di matrice, dove però vengono tolti tutti gli elementi superiori della diagonale, e la diagonale stessa (quindi le righe partono dal secondo stato, e le colonne non contengono l'ultimo stato).
2. **Passata 1**: prendo tutte le coppie distinte $(\text{stato-finale}, \text{stato-NON-finale})$ e le si segnano nella tabella (sarebbero il passo base del metodo induttivo).
3. **Passata 2**: ci si muove riga per riga, colonna per colonna, dall'alto verso il basso, e da sinistra verso destra. KIARO???
	1. Consideriamo tutte le coppie che vengono presentate nella colonna, e facciamo il ragionamento induttivo per ogni carattere dell'alfabeto. Occhio che ho detto carattere, non stringa, quindi facciamo i test sempre con elementi base, per esempio se $\Sigma = \{0,1\}$, per ogni coppia di stati che troviamo, calcoliamo dove si arriva se in entrambi faccio 0 e poi dove si va con 1.
	2. Una volta preso il carattere da analizzare, si va a vedere in che coppia di stati si arriva con quel carattere all'interno della tabella. Questa coppia di stati verrà poi cercata nella tabella, e se risulta segnata, allora segniamo la coppia che stavamo analizzando, per via del passo induttivo.
	3. Se per un carattere si incontra una coppia segnata nella tabella, allora segno la cella corrente e vado avanti.
	4. Se per tutti i caratteri non trovo celle segnate, lascio la cella corrente non segnata e vado avanti con la prossima cella.
4. **Passata 3-$\infty$**: Una volta che terminiamo la seconda passata, avremo un certo numero di elementi segnati e altri no. Per tutti gli elementi non ancora segnati, si riprova a vedere in che coppia di stati si va con un carattere, perché magari ora la coppia che prima non era segnata poi lo è diventata! Questo procedimento va avanti, e se alla fine della passata non ho toccato nulla (non ho segnato alcun elemento in questa passata), allora l'algoritmo termina.

[Link utile per algoritmo riempi tabella](https://www.reddit.com/r/LaStalla/comments/w5k2bb/er_ciuchino_chad_ti_guarda_che_fai/)

#### Classi di Equivalenza
Una volta terminato l'algoritmo riempi tabella, tutte le coppie non segnate saranno le coppie di stati equivalenti.
Per ogni coppia di stati equivalenti, creiamo ciò che viene definita **classe di equivalenza**, in sostanza l'insieme di tutti gli stati che sono risultati equivalenti applicando l'algoritmo Riempi tabella.

Le classi di equivalenza sono molto utili per la [[#Minimizzazione di Automi]].

#### Equivalenza tra Automi
Consideriamo $L$ e $M$ due linguaggi regolari, e seguiamo il seguente processo per determinare se sono equivalenti:
1. Generiamo il DFA per entrambi i linguaggi regolari.
2. Consideriamo entrambi i DFA come uno unico.
3. Applichiamo l'algoritmo riempi tabella.
4. Se alla fine dell'applicazione dell'algoritmo, i due stati iniziali sono distinguibili, allora $L \not\equiv M$, altrimenti $L \equiv M$.

#### Minimizzazione di Automi
Applichiamo come sempre l'algoritmo riempi tabella. Una volta terminato, si saranno generati tutti gli **insiemi di tutti gli stati equivalenti**, e chiamiamo la **classe di equivalenza** di $p$, come $p\backslash_{\equiv}$.

Per minimizzare un DFA $A = (Q, \Sigma, \delta, q_0, F)$, costruiamo un DFA $B = (Q\backslash_{\equiv}, \Sigma, \gamma, p_0\backslash_{\equiv}, F\backslash_{\equiv})$ dove abbiamo:
$$\gamma(p\backslash_{\equiv},a) = \delta(p, a)$$

Dove sostanzialmente stiamo dicendo che per calcolare la transizione tra classi di equivalenza, ci basta prendere qualsiasi elemento della classe di appartenenza e controllare l'insieme dell'elemento di arrivo che porterebbe la sua transizione originaria.

Due cose per la minimizzazione:
- Il nuovo **stato iniziale**  è la classe di equivalenza che contiene il vecchio stato iniziale.
- il nuovo **stato finale** è la classi di equivalenza che contiene **solo** stati di accettazione.

---
## Linguaggi Liberi dal Contesto
Chiamiamo:
- **Linguaggi Liberi dal Contesto** (CFL = Context-Free Languages)
- **Grammatiche Libere dal Contesto** (CFG = Context-Free Grammars), sono la base della sintassi *BNF* (Backus-Naur-Form).

### Definizione
Una grammatica libera dal contesto, è una quadrupla
$$G = (V, T, P, S)$$
dove:
- $V$ &rarr; è un insieme finito di **variabili**.
- $T$ &rarr; è un insieme finito di **terminali**.
- $P$ &rarr; è un insieme finito di **produzioni** (o **regole**), della forma $A \rightarrow \alpha$, dove $A$ è una variabile e $\alpha \in (V \cup T)^*$.
- $S$ &rarr; è una variabile distinta chiamata **variabile iniziale**.

### Derivazione
Sia $G = (V, T, P, S)$ una CFG, $A \in V$, $\{\alpha, \beta\} \subset (V \cup T)^*$, e $A \rightarrow \gamma \in P$.
Possiamo scrivere:
$$\alpha A \beta \xRightarrow[G]{} \alpha\gamma\beta$$
E diciamo che da $\alpha A \beta$  si deriva $\alpha \gamma \beta$.
Nell'ambito dei linguaggi liberi da contesto, $\alpha \beta$ viene chiamato **contesto**.

Possiamo definire $\xRightarrow[]{*}$ come la chiusura *riflessiva* e *transitiva* di $\implies$:

**Base**: Sia $\alpha \in (V \cup T)^*$, allora $\alpha \xRightarrow[]{*} \alpha$.

**Induzione**: $\alpha \xRightarrow[]{*} \beta$, e $\beta \implies \gamma$, allora $\alpha \xRightarrow[]{*}\gamma$.

Cioè, se da $\alpha$ posso derivare $\beta$ e da $\beta$ posso derivare $\gamma$, allora per riflessione, esiste un numero di passi di derivazione che mi permettono $\alpha \xRightarrow[]{*}\gamma$, cioè di derivare da $\alpha$ a $\gamma$.

#### Derivazione a Sinistra e Destra
- Viene definita la **derivazione canonica a sinistra** $\xRightarrow[lm]{}$ ($lm$ = left-most): rimpiazza sempre la variabile più a sinistra con il corpo di una delle sue regole.
- Viene definita la **derivazione canonica a destra** $\xRightarrow[rm]{}$ ($rm$ = right-most): rimpiazza sempre la variabile più a destra con il corpo di una delle sue regole.

### Il linguaggio di una Grammatica
Se $G(V, T, P, S)$ è una CFG, allora il **linguaggio** di G è:
$$L(G)=\{w \in T^* : S \xRightarrow[G]{*} w\}$$
Cioè l'insieme delle stringhe su $T^*$ (paragonabile a $\Sigma^*$ per i linguaggi regolari) derivabili dal simbolo iniziale. I linguaggi definiti da una CFG, vengono definiti **linguaggi liberi dal contesto** (Context-Free Languages).
Questi linguaggi non dipendono dal contesto durante la derivazione (contesto inteso come insieme di caratteri che non cambiano durante una regola di una derivazione).

### Alberi Sintattici
Se $w \in L(G)$, per una CFG, allora $w$ ha un **albero sintattico** che ci dice la **struttura sintattica** di $w$. 
In generale, gli alberi sintattici sono una rappresentazione alternativa alle derivazioni. Per ogni stringa, in generale possono esistere più alberi sintattici, ma idealmente dovrebbe essercene solo uno, affinché la CFG sia **non ambigua**.

#### Costruzione
Sia $G=(V, T, P, S)$ una CFG; un albero sintattico per $G$ è dato da un albero che soddisfa le seguenti caratteristiche:
1. Ogni **nodo interno** è etichettato con una variabile in $V$.
2. Ogni **foglia** è etichettata con un simbolo appartenente a $V \cup T \cup \{\epsilon\}$, dove ogni foglia etichettata con $\epsilon$ è l'unico figlio di suo padre.
3. Per ogni nodo interno $A$, e i suoi figli $X_1,X_2,\dots,X_k$ vale: $A \rightarrow X_1X_2 \dots X_k \in P$, cioè i figli sono il corpo (ordinato) della produzione.

#### Prodotto di un albero sintattico
Il prodotto di un albero sintattico è la **stringa** di **foglie da sinistra a destra**. Gli alberi che interessano maggiormente sono quelli dove:
1. Il prodotto è una **stringa terminale** (composta da soli caratteri terminali).
2. La radice è etichettata dal **simbolo iniziale**.

Grazie all'insieme di questi due alberi, possiamo costruire il **linguaggio della grammatica** (per esempio usato dai compilatori).

#### Alberi sintattici e Derivazioni
Sia $G=(V, T, P, S)$ una CFG, e $A \in V$. I seguenti sono equivalenti:
1. $A \xRightarrow[]{*} w$
2. $A \xRightarrow[lm]{*} w$ e $A \xRightarrow[rm]{*} w$.
3. C'è un albero sintattico di $G$ con radice $A$ e prodotto $w$.

#### Ambiguità in Grammatiche e Linguaggi
In generale, abbiamo visto come per una grammatica possano tranquillamente esistere più derivazioni. Il problema si ha per quelle grammatiche che sono rappresentabili da più di un albero sintattico, provocando un **ambiguità** del linguaggio e della grammatica stessa.

> **Def:** Sia $G = (V, T, P, S)$ una CFG. Diciamo che $G$ è **ambigua** se esiste una stringa in $T^*$ che ha più di un albero sintattico.

##### Ambiguità e Derivazioni a Sinistra
Possiamo dire in generale che:
- Ad un albero sintattico corrispondono molte derivazioni.
- Ad ogni (diverso) albero sintattico corrisponde **un'unica (diversa) derivazione a sinistra e a destra**.

###### Teorema 5.29
> Data una CFG $G$, una **stringa terminale** $w$ ha due distinti alberi sintattici se e solo se $w$ ha **due distinte derivazioni a sinistra** dal simbolo iniziale.

### Ambiguità Inerente

In un CFL, L è *inerentemente ambiguo* se tutte le grammatiche per *L* sono ambigue (ho più di un albero).  Può essere provato che ogni grammatica per *L* si comporta come questa. Il linguaggio *L* è quindi inerentemente ambiguo. 

## Automi a Pila

Un automa a pila (PDA) è in pratica un $\epsilon$-NFA con una Pila. In una transizione un PDA:
1) Consuma un simbolo dell'input 
2) Va in un nuovo stato
3) Rimpiazza il top della pila con una stringa
Questo tipo di automa è munito di una *memoria ausiliaria* con la quale è in grado di memorizzare l'input corrente. Questo ci permette di riconoscere alcuni linguaggi che non erano in grado di essere analizzati dai DFA. E' fondamentale in *non determinismo* in modo da avere sempre due strade. 


### Definizione di un DFA

Un *PDA* è una tupla formata da 7 elementi: 
$$P=(Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$$
dove:
* Q: è un insieme di finito di stati
* $\Sigma$: è un alfabeto finito di input
* $\Gamma$: è un alfabeto finito di pila
* $\delta$: è una funzione di transizione
* $q_0$: è lo stato iniziale
* $Z_0 \in \Gamma$: è il simbolo iniziale della Pila
* $F \subseteq Q$: insieme di stati di accettazione 

### Descrizioni istantanee

Un PDA passa da una configurazione ad un'altra configurazione:
* Consuma un simbolo di input o $\epsilon$ 
* Consumando la cima dello stack sostituendolo con una stringa
Per ragionare sulle computazioni dei PDA, usiamo delle **descrizioni istantanee (ID)**  del PDA. Una ID è una tupla: $$(q, w, \gamma)$$ dove:
* q: è lo stato attuale
* w: è l'input rimanente 
* $\gamma$: è il contenuto della pila

Sia $P=(Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$ un PDA. Allora $\forall w \in \Sigma^{*}, \beta \in \Gamma^{*}$ : $$(p, \alpha)\in \delta(q, a, X) \Rightarrow (q, aw, X\beta) \vdash (p, w, \alpha \beta)$$ (Dato un simbolo dell'input e dato un valore in testa alla pila, mi muovo nel nuovo stato $p$ consumando il primo elemento della stringa e mettendolo in cima allo stack)

### Accettazione per stato finale
Il linguaggio accettato dal PDA P è:
$$L(P)=\{w:(q_0, w, Z_0) \vdash^{*} (q, \epsilon, \alpha), q \in F \}$$

### Accettazione per pila vuota

Il linguaggio accettato da P, per **pila vuota** è: $$L(P)=\{w:(q_0, w, Z_0) \vdash^{*} (q, \epsilon, \epsilon) \}$$
In questo caso il momento in cui la stringa è accettata è quando:
* si ha consumato tutta la stringa di input
* la pila è vuota
Questo tipo di grammatica ci permette di effettuare le equivalenze con le grammatiche. 


### Da pila vuota a stato finale

###### Teorema 6.9
> Se $L=N(P_N)$ per un PDA $P_N=(Q, \Sigma, \Gamma_N, \delta, q_0, Z_0, F)$ allora $\exists$ PDA $P_F$ tale che $L=L(P_F)$.

![[Pasted image 20231010125847.png]]
* Aggiungo un insieme di transizioni che riconoscono quando la pila si svuota
* Metto un simbolo nella pila esterno all'insieme di simboli della pila ($X_0$) in modo che si possa svuotare
### Da stato finale a pila vuota
###### Teorema 6.11
> Se $L=N(P_F)$ per un PDA $P_F=(Q, \Sigma, \Gamma_F, \delta, q_0, Z_0, F)$ allora $\exists$ PDA $P_N$ tale che $L=N(P_N)$.

![[Pasted image 20231010130225.png]]
Un  problema che nasce da questa trasformazione è che in questo momento il nuovo PDA potrebbe accettare gli stati in cui la stringa è vuota ma non si è in uno stato di accettazione del PDA originale. Per rimediare a questo problema si introduce un nuovo simbolo all'interno degli elementi della Pila, in modo da non risultare mai vuota negli stati in cui prima si svuotava. (Chiaro?) 

## Equivalenza di PDA e CFG

Un linguaggio è generato da una CFG se e solo se è accettato da un PDA per pila vuota se e solo se è accettato da un PDA per stato finale. 

![[Pasted image 20231010130424.png]]
L'idea è quella di vedere un PDA come un processo continuo di derivazione canonica sinistra. 

Sia $G=(V, T,Q,S)$ una CFG. Definiamo $P_G$ come:$$(\{q\}, T, V \cup T, \delta, q, S)$$ dove: 
+ S è il simbolo iniziale della pila e corrisponde alla prima variabile con la quale iniziare le derivazioni
+ Si ha un unico stato chiamato $q$ con un insieme finito di auto anelli.

Per costruire questo tipo di PDA è necessario:
1) aggiungere un insieme finito di transizioni con valore $\epsilon$ con configurazione di pila da S ad ogni sua derivazione. 
2) aggiungere un insieme di transizioni con valore dell'alfabeto in cui invece si rimuove dalla pila il simbolo che si è letto. 
![[Appunti.jpeg.png]]

## Da PDA a CFG
L'idea è quella di emulare il comportamento di un PDA per rimuovere il simbolo Y dalla pila sostituendolo con $Y$ con $Y_1 Y_2... Y_k$ 
Si definisce una grammatica con variabili della forma $[p_{i-1}Y_ip_i]$ che rappresentano il passaggio da $p_{i-1}$ a $p_i$ con l'effetto di eliminare Y. 

L'idea è che si ha una transizione all'interno del PDA che sostituisce il valore di Y con una stringa di lunghezza K. Abbiamo quindi: $$[qYp_k] \Rightarrow a[p_0Y_1p_1][p_1Y_2p_2]...[p_{k-1}Y_kp_k]$$
in cui 'a' rappresenta il simbolo della stringa che permette di eseguire la transizione, $p_0$ è lo stato che raggiungo da 'q'. ![[Pasted image 20231011180134.png]]

## PDA Deterministico 
Un PDA è deterministico se e solo se: 
1) ogni $\delta(q, a, X)$ con $a \in \Sigma \cup \{\epsilon\}$ contiene al più un elemento, ovvero esiste solo una transizione con stesso valore di transizione e stesso valore di pila
2) se $\delta(q, a, X)$ non vuoto per un $a \in \Sigma$ allora $\delta(q, \epsilon, X)$ vuoto, ovvero anche quando posso muovermi dallo stesso stato con un valore $\epsilon$ con gli stessi valori di pila

### DPDA che accettano per stato finale
###### Teorema 6.17
> Se L è regolare allora L=L(P) per qualche DPDA P

Prova: Dato che L è regolare allora esiste un DFA A tale che L=L(A) sia:$$A=(Q,\Sigma, \delta_A, q_0, F)$$
definiamo il PDA:$$P=(Q, \Sigma, \{Z_0\}, \delta_p, q_0, Z_0, F)$$ dove $$\delta_p(q,a, Z_0)=\{(\delta_A(q, a), Z_0)\}$$
In sostanza non agisco mai sulla pila, aggiungo semplicemente un solo valore di pila ovvero $Z_0$. 

## DPDA che accettano per pila vuota 

Possono riconoscere solamente linguaggi con la **proprietà del prefisso**. Un linguaggio L ha la proprietà del prefisso se **non** esistono due stringhe distinte in L tali che una è un prefisso dell'altra. 

###### Teorema 6.17
> Se L è N(P) per qualche DPDA P se e solo se L ha la proprietà del prefisso e L è L(P') per qualche DPDA P'. 

## DPDA e non ambiguità

###### Teorema 6.17
> 	Se L=N(P) per qualche DPDA P, allora L ha una CFG non ambigua
###### Teorema 6.17
> Se L=L(P) per qualche DPDA P, allora L ha una CFG non ambigua. 
