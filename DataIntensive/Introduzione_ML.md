# Data Intensive

## Introduzione al Machine learning 

Attraverso **ambienti virtuali** è possibile addestrare gli algoritmi, fornendo una elevata quantità di conoscenza. *L'intelligenza viene ricavata dai dati utilizzati* durante l'addestramento, qualsiasi informazione viene rappresentata come un vettore. Il training permette di minimizzare le funzioni errore andando ad individuare punti di minimo. La **Regressione** ci permette di predire una variabile continua, andando ad effettuare oltre alla classificazioni delle previsioni (prezzi, eta di morte, ecc).

Il _deep learning_ è una rete neurale con un numero elevatissimo di **layer**, assieme al _deep reinforcement learning_ sono due tecniche molto precise ed accurate ma purtroppo richiedono grandi capacità computazionali. L'intelligenza artificiale **non è cablata nel codice** ma è **appresa da un insieme di dati**. 

## Machine Learning

Bisogna sempre definire l'obbiettivo e che cosa si vuole misurare, si vogliono spesso cercare **variazioni inusuali**. Tutte le decisioni che vengono prese dall'algoritmo sono guidate dai dati. I dati sono **pre etichettati**, oltre a tutti gli attributi da valutare devo aggiungere al più un valore che viene ricavato dalla conoscenza acquisita, il nostro risultato. Il concetto fondamentale è che _l'algoritmo apprende dai dati_, se i dati sono errati l'algoritmo risulterà errato. Una fase fondamentale è il **controllo dei dati**.

La **knowledge discovery** è l'estrazione implicita della conoscenza utile dentro ai dati su cui viene addestrato il nostro algoritmo. Il discovery viene fatto tramite tecniche statistiche, visualizzazione e machine learning. Deve essere estremamente scalabile siccome si vanno a manipolare grandi quantità di dati. Inoltre è possibile anche **paralelizzare l'addestramento**, ovvero avere la possibilità di più istanze dello stesso algoritmo che viene addestrato nello stesso momento.

Il **machine learning** viene adottato dopo aver effettuato *collezione dei dati*, *controllo qualità*, *classificazione*, tutto ciò che va dalla *data integration*, il *data cleaning* (pulendo i dati dal rumore). 

Il **condizionamento** può sporcare i nostri risultati andando a fornire output non corretti solamente a causa del mal condizionamento dei dati forniti, gli algoritmi potrebbero imparare a fare cose solamente sbagliate. Tutto ciò può essere causato dall'univocità di alcune informazioni nei dati che potrebbero condizionare i nostri risultati, bisogna quindi controllare la conoscenza che è stata acquisita.

Il **data mining** è l'estrazione di conoscenza dai dati.

### Learning & Training
**Learning** saper modificare il proprio comportamento in modo da migliorare le proprie prestazioni su problemi noti. Imparare a fare meglio su problemi già affrontati in precedenza.  
**Training** Apprendimento passivo, saper risolvere nuovi problemi che prima non sapevo risolvere.

### Dati ed Informazioni

**Buisness Intelligence** è un insieme di processi aziendali per raccogliere ed analizzare informazioni strategiche, la differenza con il machine learning è che l'analisi la fa un umano. Si parte  da una sorgente dei dati, successivamente si eseguono analisi descrittive dei miei dati, andando ad identificare anche eventuali errori (potrebbero alterare di molto i dati). La **preparazione dei dati**, individuare le *features* ovvero le variabili che mi permettono di identificare in maniera esatta l'output del mio problema (colore vino, numero di fori in una cellula per capire se è tumorale o meno). La scelta delle variabili è fondamentale, esistono anche classi di algoritmi che permettono di individuare le variabili migliori da individuare (esistono algoritmi stessi di ML : random forest). **Patterns & Model**, una volta individuati i dati da utilizzare si provano diversi algoritmi, che dipendono dal problema che si deve risolvere. Infine si ha la **valutazione** dei risultati, andandoli a confrontare in maniera *oggettiva*, si utilizzano metodi statistici trovando modelli *equivalenti* o *non equivalenti*, potendo confrontare i diversi output ottenuti. 

E' un modello a spirale in quanto nel caso in cui l'accuratezza non sia all'altezza si vanno a modificare iperparametri, gli algoritmi o gli stessi dati. 

### Tipi di analisi

* _analisi descrittiva_ &rarr; descrivere che cosa è successo, in allegato si possno aggiungere anche informazioni di tipo statistico
* _diagnostica_ &rarr; perché tutto ciò è successo, capire accuratamente i motivi per cui certi eventi accadono (*Explainability*)
* _predittiva_ &rarr; predire ciò che succederà
* _prescrittiva_ &rarr; che cosa possiamo fare affinché un evento accada/non accada

### Macchine Learning

Gli algoritmi di Machine learning si dividono in:

* **Supervised Learning** si dividono in *classification* e *regression*: 
    * **Algoritmi di Classificazione**, tendono a classificare anche casi corretti in casi incorretti, nonostante la sua accuratezza possa essere molto elevata, le misure di valutazione devono essere utilizzate con attenzione:
        * Diagnostic
        * Identity Fraud
    * **Algoritmi di regressione**:
        * Market Forecasting
        * Population Growth Prediction
        * Estimating Life Expectancy
        * Weather Forecasting 

* **Unsupervised Learning**, si cercano dei **pattern**,non si ha la possibilità di misurare il nostro algoritmo ma solamente quanto gli elementi del cluster sono coesi, vicini tra loro e quanto ciascun gruppo è dissimile dagli altri (*Frequent Item Set*, bisogna spostare questi prodotti in modo che mi minimizza il tempo di ricerca di tali prodotti, trovare delle regole associative ed anche le regole di dipendenze birra &rarr; noccioline, chiamate regole di confidenza). Gli algoritmi di **Unsupervised Learning** si dividono in *clustering* e *dimensionality reduction*:
    * **Clustering**, non si sono etichette nei dati, viene usato per la *Customer Segmentation*(capire i gruppi più omgenei, questo dipende dalle variabili che vengono utilizzate), capisco quanto dei gruppi siano distanti tra loro, la distanza tra cluster diversi deve essere tanta.  Se i Cluster non sono *ipersferici*, ma hanno forme particolari questo fa si che alcuni elementi possono mischiarsi oppure elementi dello stesso cluster possono essere molto distanti tra loro, il vero problema è che non esistono etichette, non si hanno i gruppi di appartenenza i quali vanno individuati dal nostro algoritmo.
    * **Dimensionality Reduction**, 

* **Reinforcement Learning**, si fanno tante prove si misurano gli errori e mano mano nel tempo la rete neurale apprende quali sono i pattern migliori e li ripete, vengono utilizzate per addestramenti, i *problemi non sono differenziabili*, sono problemi di ottimizzazione combinatoria. Permette di risolvere problemi **NP-Hard**.  

* **Self Supervised Learning**, tipo di apprendimento in cui c'è una supervisione in algoritmi *unsupervised*, questo apprendimento ha del trading, è possibile misurare un gradiente, c'è un errore. In questo modo è possibile, attraverso la *back propagation* permette di aggiornare i pesi della rete neurale, apprendendo il significato dei dati, in maniera autonoma. Viene utilizzato **in problemi in cui non ci sono etichette**, trovando relazione nei dati, trovando attraverso gli algoritmi di Machine Learning le relazione stesse dei dati.  

*Transoformer*, sono evoluzioni degli auto encoder, vi è un encoder, trova rappresentazioni e segue un *decoder* ovvero quello che ritrasforma, tali vettori in parole.  

