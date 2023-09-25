# Machine Learning

**Contenuto**
- [[#Introduzione|Introduzione]]
- [[#Intelligenza Artificiale e "Forza Bruta"|Intelligenza Artificiale e "Forza Bruta"]]
	- [[#Intelligenza Artificiale e "Forza Bruta"#Brute Force|Brute Force]]
	- [[#Intelligenza Artificiale e "Forza Bruta"#Weak AI|Weak AI]]
	- [[#Intelligenza Artificiale e "Forza Bruta"#Evolutionary Computing|Evolutionary Computing]]
- [[#Le stagioni dell'Intelligenza Artificiale|Le stagioni dell'Intelligenza Artificiale]]
- [[#Deep Learning|Deep Learning]]
- [[#Fondamenti|Fondamenti]]
	- [[#Fondamenti#Dati  e Pattern|Dati  e Pattern]]
		- [[#Dati  e Pattern#Tipi di Pattern|Tipi di Pattern]]
	- [[#Fondamenti#Classificazione|Classificazione]]
	- [[#Fondamenti#Regressione|Regressione]]
	- [[#Fondamenti#Clustering|Clustering]]
	- [[#Fondamenti#Riduzione delle Dimensionalità|Riduzione delle Dimensionalità]]
	- [[#Fondamenti#Representation Learning|Representation Learning]]
	- [[#Fondamenti#Problemi nel dominio Visione|Problemi nel dominio Visione]]
	- [[#Fondamenti#Apprendimento|Apprendimento]]
---
## Introduzione

Un *modello* di **Machine Learning** durante la fase di *training* apprende a partire da esempi. Successivamente è in grado di **generalizzare** e gestire nuovi dati nello stesso dominio applicativo. Questo tipo di modello è in grado di **imparare dagli esempi a migliorare le proprie prestazioni per la gestione dei nuovi dati**. 

All'interno del machine learning vi sono alcuni concetti chiave, tra cui:
* L'apprendimento è una componente chiave
* Apprendere il comportamento desiderato dai dati forniti
* Rende possibile esplorare i dati
* Addestramento *end-to-end*
* **Deep Learning**
## Intelligenza Artificiale e "Forza Bruta"

### Brute Force

Il **brute-force** è utilizzato in alcuni domini applicativi ed è in grado di risolvere problemi in modo ottimo semplicemente **enumerando e valutando tutte le possibili alternative**. Nella maggior parte dei caso però la valutazione esaustiva di tutte le possibili soluzioni non è computazionalmente gestibile, si utilizzano tecniche di *trial and error* e tecniche 
*euristiche* per ridurre il numero totale di casi da valutare. 

### Weak AI
In questi casi si tratta di **Weak AI**, sistemi capaci di risolvere problemi complessi senza però capacità di ragionamento e comprensione.

### Evolutionary Computing

Una famiglia particolare di **Evolutionary Computing**, tra cui gli algoritmi *genetici*, sono in grado di creare delle specie/generazioni in cui vengono mantenute solamente le caratteristiche migliori. Questi algoritmi si ispirano al principio di evoluzione degli esseri viventi.

## Le stagioni dell'Intelligenza Artificiale

1) 1940 - 1974 **LA NASCITA E GLI ANNI D'ORO**: 
	* Primi calcolatori elettronici
	* Teoria della computazione Turing
	* Neuroni Artificiali
	* Primi risultati del **symbolic reasoning**
2) 1974 - 1980 **IL PRIMO INVERNO**: 
	* Drastica riduzione dei finanziamenti
	* Scarsa capacità computazionale
	* Esplosione combinatoria e non trattabilità
3) 1980 - 1987 **NUOVA PRIMAVERA**: 
	* Nascita dei sistemi esperti (conoscenza + regole logiche)
	* Algoritmo di **Backpropagation** (algoritmi con la quale addestrare i modelli/reti neurali)
4) 1987 - 1993 **IL SECONDO INVERNO**: 
	* Stop ai finanziamenti
	* Hardware specializzato non più competitivo con PC
	* Le reti neurali non scalano a problemi complessi
5) 1993 - 2011 **TEMPI MODERNI**:
	* Classificatori robusti (*SVM*)
	* Multi-classificatori (*Random Forest, Adaboost*)
	* Tecniche di *feature extraction*
6) 2011 - oggi (scudetto napoli) **DEEP LEARNING**:
	* CNN (Convolutional Neural Network) grazie ai "big data & potenza di calcolo"
	* *Speech Recognition*
	* *Language Translation*
	* *Large Language Models*
## Deep Learning

Le tecniche di *Deep Learning* **raggiungono e superano** lo stato dell'arte in molteplici applicazioni. Questa nuova tecnologia è composta da **reti neurali profonde**. 

---
## Fondamenti
### Dati  e Pattern
Essendo il comportamento modelli di machine learning appreso dai dati stessi, è necessario quindi lo studio del dato stesso (branche come il Data Analysis, Data Mining e Big Data).
Un singolo record viene generalmente chiamato **Data Point**,  o il suo sinonimo **Pattern**.
> *Pattern*: opposto del caos e entità vagamente definita cui può essere dato un nome.

#### Tipi di Pattern
- **Numerici**: valore associato a caratteristiche *misurabili* o *conteggi*.
	- Producono **feature vectors**, ovvero descrizione numerica delle caratteristiche di un singolo data point.
- **Categorici**: valori associati a caratteristiche **qualitative** o **booleane** (presenza/assenza).
	- Grazie all'*encoding* o *embedding* si possono utilizzare anche con questi pattern modelli che operano solo su dati numerici.
		- *One-hot*: una colonna booleana aggiunta per attributo possibile. Se gli attributi sono molti, le colonne esplodono.
		- *Ordinal-encoding*: campo numerico associato agli attributi in ordine crescente. Attenzione al modello utilizzato, perché non deve cercare similarità tra le categorie in base alla vicinanza dei numeri (problema: in base a cosa si sceglie l'ordine delle categorie?).
- **Sequenze**: pattern sequenziali con **relazioni** *spaziali* o *temporali* (e.g. stream audio o video).
	- Richiede allineamento spaziale/temporale e "memoria" per tener conto di quanto visto in precedenza.
	- Approcci  moderni: Deep-Learning, Long Short-Term Memory (LSTM), Transformer.
- Altri **dati strutturati**: output organizzati in strutture complesse quali alberi o grafi.
- **Dati Tabulari** (*eterogenei*): dati organizzati in tabelle (e.g. RDBMS) le cui colonne contengono le *features* eterogenee, e nelle righe i *data-point*.
	- Per via del fatto che esistono valori a *null* e molto spesso alcuni valori sono fortemente sbilanciati, risulta difficile  stabilire una similarità tra i record.
	- Oggi, per quanto le reti neurali profonde siano dominanti in molti ambiti dell'AI, non sono molto competitive nell'ambito dei dati tabulari, dove per esempio una gradient boosting machine o un random forest sono molto più performanti.

### Classificazione
Obiettivo: assegnare una **classe** a un pattern.
Una **classe** in generale, è un insieme di pattern aventi proprietà comuni. Non è definibile a priori per ogni problema, poiché la classe dipende strettamente dalla semantica e obiettivi dell'applicazione.

Per il problema della classificazione, il modello deve apprendere una *funzione* capace di eseguire il mapping dallo spazio dei pattern allo spazio delle classi.
- Si parla di *binary classification* con due classi sole, mentre *multi-class* con più di due classi.

### Regressione
Obiettivo: assegnare un **valore continuo** a un pattern.
I modelli di regressione lavorano generalmente con valori continui (perché l'output è continuo). La risoluzione di un problema di regressione significa far apprendere al modello una funzione che approssima le coppie `(input, output)` date (ovvero creare una funzione approssimante l'andamento del fenomeno delle features).

Strano ma vero, l'*object detection* è un problema di regressione (cioè il problema della creazione della bounding box).

### Clustering
![[img/Pasted image 20230925101622.png|right|300]]
obiettivo: individuare dei gruppi, regioni di spazio di data point con proprietà comuni, senza conoscere a priori la loro classe.
Possiamo definirlo come un problema **non supervisionato**, perché anche in fase di addestramento non abbiamo le label della classe.
I cluster individuati nell'apprendimento possono poi essere usati come classi.
Lo spazio può essere ovviamente multidimensionale.

Utile per il *knowledge discovery*, per comprendere elementi non noti del dominio.

### Riduzione delle Dimensionalità
Molto spesso per rendere **trattabili** i problemi ad elevata dimensionalità, si effettua l'apprendimento su un mapping da $\mathbb{R}^d$ a $\mathbb{R}^k$ con $k < d$. Questo comporta una perdita di informazioni (quindi è necessario massimizzare le informazioni e scartare quelle meno).

### Representation Learning
L'efficacia dei modelli di machine learning dipende da quanto bene rappresentano i pattern in termini di features. Questo può essere raggiunto tramite un approccio *hand-crafted* detto *feature engineering*, dove vengono definite features ad hoc.
È però anche possibile apprendere automaticamente feature efficaci a partire dai dati grezzi (approccio detto **Representation Learning** o **Feature Learning**).  Gran part delle tecniche di deep leaning operano in questo modo, prendendo in input dati grezzi ed estraendo automaticamente le feature necessarie per risolvere il problema di interesse. 

### Problemi nel dominio Visione
- [[#Classificazione|Classification]].
- **Localization**: determina classe dell'oggetto e sua posizione nell'immagine (bound box).
- **Detection**: per ogni oggetto presente nell'immagine, stabilire classe e bound box.
- **Segmentation**: al posto della bound box, etichetta i singoli pixel dell'immagine a classi con indici delle classi.

### Apprendimento
- **Suopervised**: sono note le classi dei pattern a priori durante l'addestramento.
	- Etichettamento del training set.
	- Tipico in classificazione e regressione.
- **Non-Supervised**: non sono note le classi dei pattern utilizzati per l'addestramento.
	- Nessun etichettamento del training set.
	- tipico nel clustering e nella maggior parte delle tecniche di riduzione della dimensionalità.
- **Semi-Supervised**: il training set è *etichettato parzialmente*.
	- la distribuzione dei pattern non etichettati può aiutare a ottimizzare la regola di classificazione.

L'addestramento poi può essere gestito nei seguenti modi:
- **Batch**: l'addestramento è effettuato una sola volta su un  training set dato. Una volta terminato il training, il sistema viene deployato e non è in grado di apprendere ulteriormente.
- **Incrementale**: a seguito dell'addestramento iniziale, è possibile effettuare ulteriori sessioni di addestramento:
	- Viene utilizzato in sequenze di Batch e Unsupervised Tuning.
	- Il rischio è che il sistema dimentichi quello che ha appreso in precedenza (*catastrophic forgetting*).
- **Naturale**: addestramento continuo, attivo in *working mode* (quando è già deployato).
	- Necessaria una coesistenza tra approccio supervisionato e non supervisionato (pensa a un bambino piccolo, la mamma quando è piccolo lo corregge (supervised), poi col tempo e con l'esperienza(self-interaction) impara da solo senza supervisione parentale).

![[Pasted image 20230925111356.png|left|300]]
 - **Reinforcement Learning**: **apprendere un comportamento** ottimale a partire da esperienze passate.
	 - Un agente esegue azioni che modificano un ambiente provocando passaggi di stato. Se il risultato è positivo viene premiato (reward) il comportamento, vincolando quindi la scelta della prossima azione in un certo modo (massimizzare l'operazione ottimale). Viceversa per azioni errate, non viene generato un reward e quindi il modello passa ad un approccio diverso per la massimizzazione della funzione che modella il comportamento da apprendere. 

Vista di overview su **Parametri e Funzione Obiettivo** (la si vedrà più avanti).

In generale, un modello $M$ di ML è regolato da un set di parametri $\Theta$. Quindi l'apprendimento per il modello $M(\Theta)$ consiste nel determinare il valore ottimo $\Theta^*$ di questi parametri.
Dato un training set $\text{Train}$ e un insieme di parametri $\Theta$, la **funzione obiettivo** $f(\text{Train}, M(\Theta))$ può indicare:
- l'ottimalità della soluzione (da massimizzare):
$$\Theta^* = \text{argmax}_\Theta\quad f(\text{Train}, M(\Theta))$$
- oppure può rappresentare l'errore o perdita da *minimizzare* (**loss-function**):
$$\Theta^* = \text{argmin}_\Theta\quad f(\text{Train}, M(\Theta))$$
	- Questa è una metrica più usata.

- $f(\text{Train}, M(\Theta))$ può essere ottimizzata:
	- *esplicitamente* con metodi che operano a partire dalla sua definizione matematica: calcoliamo il minimo della funzione analiticamente, tramite derivate/gradiente.
	- *implicitamente* utilizzando euristiche che modificano i parametri in modo coerente con $f$. Passi euristici che minimizzano la loss, roba di buon senso non analitica.

Stabilito il modello da utilizzare, prima dell'apprendimento viene definito il valore degli **iperparametri**. Gli iperparametri $H$ definiscono i *dettagli architetturali* del modello e della corrispondente procedura di training. Esplicitiamo questa dipendenza scrivendo il modello come: $M(H, \Theta)$.
- e.g. numero di neuroni nella rete neurali, tipo di loss function, grado del polinomio usato in regressione, …

Per trovare gli iperparametri migliori si può operare in due livelli:
- Si fissano gli iperparametri $H$ nel livello esterno
- Per ogni configurazione di $H$ si valutano le prestazioni sul validation set nel livello interno.
- Al termine della procedura si scelgono gli iperparametri $H^*$ che hanno fornito prestazioni migliori.

e.g. grid-search di scikit-learn.

Per poter effettaure un apprendimento efficiente, usiamo tre set disgiunti  tra loro, ognuno con uno scopo diverso:
- **Training set**: è l'insieme di pattern su cui addestrare il modello, su cui trovare il valore ottimo $\Theta^*$.
- **Training set**: è l'insieme di pattern su cui tarare gli iperparametri $H$.
- **Training set**: è l'insieme di pattern su cui valutare le prestazioni finali.

Capire la cardinalità di questi insiemi non è predefinito, è necessaria un po' di esperienza, poiché ogni set deve avere il giusto numero di elementi (no set troppo sbilanciati in numero), per evitare di non creare overfitting e non permettere al modello di generalizzare il fenomeno sui cui è allenato. In generale per come sono disposti i dati (magari anche relazioni temporali) bisogna sempre vedere caso per caso (per esempio usare random ogni volta non è sempre corretto, specialmente per relazioni intricate tipo temporali sui parametri).

Si può usare la k-fold cross validation per una scelta robusta degli iperparametri.
![[Pasted image 20230925113933.png|center]]
Dividiamo il training set in k-fold o gruppi. Per ogni combinazione di iperparametri $H_i$ che si vuole valutare:
- si esegue k volte il training scegliendo uno dei fond come validation set e i 4 rimanenti come training set.
- si calcola l'accuratezza come media/mediana delle k accuratezze sui rispettivi validation set.
- Scegli l'iperparametri ottimali si riaddestra il modello su tutto il training set (tutti i k fold) e solo a questo punto si verifica sul test set lasciato da parte prima della k-fold cross validation.

Il problema sta nel fatto che scegliamo il miglior modello che meglio si adatta al *test-set*. Questo viene chiamato **cherry picking**, e agendo in questo modo si ha overfitting sul test set. Questo ha forti implicazioni negative nell'ambito business, o in generale in ogni ambito dove i dataset sono molto piccoli o variabili molto nel tempo.