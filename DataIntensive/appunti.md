# Data Intensive

## Introduzione al Machine learning 

Attraverso **ambienti virtuali** è possibile addestrare gli algoritmi, fornendo tantissima conoscenza. L'intelligenza viene ricavata dai dati utilizzati durante l'addestramento, qualsiasi informazione viene rappresentata come un vettore. Il training permette di minimizzare le funzioni errore andando ad individuare punti di minimo. La **Regressione** ci permette di predire una variabile continua, andando ad effettuare oltre classificazioni delle previsioni (prezzi, eta di morte, ecc).

Il _deep learning_ è una rete neurale con un numero elevatissimo di **layer**, assieme al _deep reinforcement learning_ sono due tecniche molto precise ma che purtroppo richiedono dispositivi molto performanti. L'intelligenza artificiale **non è cablata nel codice** ma è **appresa da un insieme di dati**. 

## Machine Learning

Bisogna sempre definire l'obbiettivo e che cosa si vuole misurare, si vogliono spesso cercare **variazioni inusuali**. Tutte le decisioni che vengono prese dall'algoritmo sono guidate dai dati. I dati sono **pre etichettati**, oltre a tutti gli attributi da valutare devo aggiungere al più un valore che viene ricavato dalla conoscenza acquisita, ovver il nostro risultato. Il concetto fondamentale è che _l'algoritmo apprende dai dati_, se i dati sono errati l'algoritmo risulterà errato. Una fase fondamentale è il controllo dei dati.

La **knowledge discovery** è l'estrazione implicita della conoscenza utile dentro ai dati su cui viene addestrato il nostro algoritmo. Il discovery viene fatto tramite tecniche statistiche, visualizzazione e machine learning. Deve essere estremamente scalabile siccome si vanno a manipolare grandi quantità di dati, andando semmai andando a **paralelizzare l'addestramento**, avendo più istanze dello stesso algoritmo che viene addestrato in parallelo.

Il **machine learning** viene adottato dopo aver effettuato *collezione dei dati*, *controllo qualità*, *classificazione*, tutto ciò che va dalla *data integration*, il *data cleaning* (pulendo i dati dal rumore). Il **condizionamento** può sporcare i nostri risultati andando a fornire output errati solamente a causa del mal condizionamento dei dati forniti, gli algoritmi potrebbero imparare a fare cose solamente sbagliate. Tutto ciò è dato dall'univocità di alcune informazioni nei dati che potrebbero condizionare i nostri risultati, bisogna controllare la conoscenza che è stata acquisita.

Il **data mining** è l'estrazione di conoscenza dai dati.

### Learning & Training
**Learning** saper modificare il proprio comportamento in modo da migliorare le proprie prestazioni su problemi noti. Imparare a fare meglio su problemi già affrontati in precedenza.  
**Train** Apprendimento passivo, saper risolvere nuovi problemi che prima non sapevo risolvere.

### Dati ed Informazioni

**Buisness Intelligence** è un insieme di processi aziendali per raccogliere ed analizzare informazioni strategiche, la differenza con il machine learning è che l'analisi la fa un umano. Si parte  da una sorgente dei dati, successiamente si eseguono analisi descrittive dei miei dati, andando ad identificare anche eventuali errori (potrebbero alterare di molto i dati). La **preparazione dei dati**, individuare le *features* ovvero le variabili che mi permettono di identificare in maniera esatta l'output del mio problema (colore vino, numero di fori in una cellula per capire se è tumorale o meno). La scelta delle variabili è fondamentale, esistono anche classi di algoritmi che permettono di individuare le variabili migliori da individuare (esistono algoritmi stessi di ML : random forest). **Patterns & Model**, una volta individuati i dati da utilizzare si provano diversi algoritmi, che dipendono dal problema che si deve risolvere. Infine si ha la **valutazione** dei risultati, andandoli a confrontare in maniera *oggettiva*, si utilizzano metodi statistici trovando modelli *equivalenti* o *non equivalenti*, potendo confrontare i diversi output ottenuti. 

### Tipi di analisi

* _analisi descrittiva_ &rarr; descrivere che cosa è successo, in allegato si possno aggiungere anche informazioni di tipo statistico
* _diagnostica_ &rarr; perché tutto ciò è successo, capire accuratamente i motivi per cui certi eventi accadono
* _predittiva_ &rarr; predire ciò che succederà
* _prescrittiva_ &rarr; che cosa possiamo fare affinche una cosa accada/non accada

