**Contenuto**
- [[#Introduzione|Introduzione]]
	- [[#Introduzione#Linguaggi|Linguaggi]]
	- [[#Introduzione#Algoritmi, Calcolabilità e Macchine di Turing|Algoritmi, Calcolabilità e Macchine di Turing]]
	- [[#Introduzione#Logiche Temporali|Logiche Temporali]]
- [[#Linguaggi Regolari|Linguaggi Regolari]]
	- [[#Linguaggi Regolari#Concetti base|Concetti base]]
	- [[#Linguaggi Regolari#Automi a Stati Finiti *Deterministici*|Automi a Stati Finiti *Deterministici*]]

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

### Automi a Stati Finiti *Deterministici*
