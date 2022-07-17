---
title: Glossario di Account IQ
description: 'Glossario delle terminologie dei prodotti.  '
source-git-commit: 8d8aa00d693b1ca7f960a71b40053e47249c63e4
workflow-type: tm+mt
source-wordcount: '1455'
ht-degree: 0%

---

# Concetti di prodotto e glossario {#glossary}

Fai riferimento alle seguenti terminologie di prodotto e relative definizioni.

## Probabilità di condivisione account {#account-sharing-probability-def}

Un pannello del dashboard con grafici che divide i segmenti correnti condividendo punteggi in categorie di range di Molto basso, Basso, Moderato, Alto e Molto alto.

## Azione {#action-def}

Un evento diretto o indiretto associato a un [Funzionamento](#operation-def) che influisce sulle caratteristiche (ad esempio, Condivisione di un punteggio o numero di dispositivi in uso) di un segmento di operazione correlato (o coorte).

## Punteggio di condivisione aggregato {#sharing-probability-level-def}

Un pannello del dashboard con grafici che divide i punteggi dei segmenti correnti in categorie di intervalli di condivisione molto bassi, bassi, moderati, alti e molto alti, insieme a ciascuna categoria percentuale della quantità totale di streaming per il segmento.

## AuthN {#authn-def}

Autenticazione o il numero di tentativi di autenticazione. Un tentativo di autenticazione è il processo tramite il quale un utente senza uno stato di autenticazione attualmente valido viene reindirizzato al proprio MVPD scelto, dove si identificano al MVPD - in genere con un nome utente e una password.

## AuthN OK {#authn-ok-def}

Numero di autenticazioni riuscite. Un&#39;autenticazione di successo si verifica quando un utente si identifica è confermato da un MVPD e fa sì che l&#39;utente venga reindirizzato nuovamente all&#39;app o al sito del programmatore.

## AuthZ {#authz-def}

Autorizzazione o numero della richiesta di autorizzazione. Una richiesta di autorizzazione è il processo con cui un programmatore richiede l&#39;autorizzazione da un MVPD attraverso l&#39;Adobe per iniziare a trasmettere il contenuto richiesto da un utente. L’MVPD in genere concede la richiesta in base ai diritti di contenuto associati all’abbonamento MVPD dell’utente (ad esempio, se il canale associato al contenuto si trova nell’abbonamento dell’utente). Alcune risposte alle richieste di autorizzazione sono memorizzate nella cache per Adobe, il che consente all&#39;Adobe di rispondere immediatamente senza passare la richiesta all&#39;MVPD.

## AuthZ OK {#authz-ok-def}

Numero di autorizzazioni riuscite.

## Canale {#channel-def}

Il canale, noto anche come Proprietà, è una fonte di contenuto video correlata al tema. Tradizionalmente rappresenta un feed video continuo distinto e indirizzabile numericamente da un MVPD. Il canale viene mappato direttamente su un canale accessibile di contenuto disponibile agli abbonati attraverso il loro Set Top Box (STB).

## Cluster {#cluster-def}

Un cluster è una raccolta di posizioni e dispositivi. I cluster vengono creati trovando posizioni comuni tra i dispositivi. I dispositivi visualizzati in una posizione comune saranno considerati appartenenti allo stesso cluster. Due dispositivi possono trovarsi nello stesso cluster anche se non hanno posizioni comuni ma possono essere collegati attraverso le posizioni di altri dispositivi.

### Cluster mobile {#mobile-cluster-def}

Un cluster privo di dispositivi statici.

### Cluster statico {#static-cluster-def}

Un cluster con almeno una periferica statica.

## Concorrenza {#consurrency-def}

Il concomitante è definito da due (o più) flussi riprodotti contemporaneamente o molto vicini nel tempo in modo che l&#39;intervallo tra di essi non possa essere giustificato viaggiando a una velocità normale.
L’utilizzo simultaneo viene calcolato utilizzando la velocità massima (miglia/ora) tra 2 diversi cluster. Si considera che un utente utilizzi contemporaneamente se ha una velocità superiore a 124 m/h su una distanza inferiore a 124 miglia o se ha una velocità superiore a 400 m/h su una distanza superiore a 124 miglia. La distanza viene calcolata tra posizioni di cluster diversi. L&#39;utilizzo simultaneo è consentito nello stesso cluster.

## Dispositivo {#device-def}

Prodotto hardware video digitale in grado di riprodurre contenuti TV Everywhere e supportato da Adobe Pass. Ad esempio, smartphone, computer portatili e desktop, console giochi e televisori intelligenti.

## Area geografica {#geographical-span-def}

La distanza tra i punti più lontani in un insieme di posizioni.

## Granularità {#granularity-def}

In riferimento al periodo di tempo, la dimensione del periodo; ad esempio una settimana o un mese.

## Indice medio dell&#39;industria {#industry-avg-index-def}

Valore calcolato per ciascuno degli indici di rischio (Account, Utilizzo, Complessivo) per tutti i programmatori e gli MVPD durante l&#39;intervallo di tempo selezionato.

## IP {#ip-def}

Indirizzo del protocollo Internet assegnato a un dispositivo da un provider di servizi Internet. Ad esempio, provider di servizi via cavo e provider di servizi di telefonia cellulare.

## Modalità di isolamento {#isolation-mode-def}

Un tipo di analisi di condivisione in cui la valutazione di un account è limitata agli eventi che si sono verificati direttamente sui programmatori nel segmento selezionato.  Normalmente, vengono valutati tutti gli eventi del conto, il che fornisce una stima molto più accurata della condivisione.  Alcuni dati MVPD sono strutturati in modo da consentire solo l’analisi della modalità di isolamento.

## Posizione {#location-def}

Un punto unico sulla terra. Viene anche definita geolocalizzazione per una specifica richiesta di gioco, rilevata utilizzando i dati Pass, con una precisione di 1000mx1000m (un km quadrato).

<!-- ### Home location {#home-location-def}

the precision is 0.01 ~ 2000mx2000m (4 square km) - at this moment the home location is detected using an ML algo, based on data provided by two mvpds. The probability is ~ 80%. We are not using the zip code for the majority of the users. Currently, this information is not used in assessing the sharing probability. -->

## Media Company {#media-company-def}

Media Company è un&#39;azienda proprietaria di un gruppo di reti di media.

## Metrica {#metric}

La metrica è un attributo dell&#39;account utente (ad esempio, il MVPD, i programmatori e i canali del contenuto che trasmettono, il numero di dispositivi che utilizzano).

## Dispositivo mobile {#mobile-device-def}

Dispositivo ad alta mobilità. Ad esempio, telefono cellulare e tablet.

## MVPD {#mvpd-def}

MVPD, noto anche come Distributore, è aggregatore, rivenditore e distributore di contenuti video Media Company.

## Funzionamento {#operation-def}

L&#39;operazione è un record creato per tenere traccia dell&#39;effetto di una particolare [action](#action-def) su un segmento associato. Un esempio di azione può essere un limite posto al numero di flussi simultanei consentiti per account identificati dal segmento.

## Punteggio di condivisione complessivo {#overall-sharing-score}

Un valore che aiuta gli utenti a comprendere l&#39;ampiezza della condivisione delle password sulle proprietà del programmatore o dagli abbonati MVPD e fornisce loro un senso di urgenza per agire su di esso.

<!--**Aggregated Risk Index**
Also known as Risk Index and Sharing Risk Index, it is a value that helps users understand the magnitude of password sharing on Programmer properties or by MVPD subscribers and provides them a sense of urgency to act upon it.-->

<!--**Risk Index - Overall**
A value computed as an average of "Risk Index - Accounts" and the "Risk Index - Usage". Overall Sharing Risk Index-->

## Richiesta Play {#play-requests-def}

Richiesta di Adobe di un&#39;app client o di un sito per richiedere un token multimediale per registrare e proteggere un avvio del flusso.

## Programmatore {#programmer-def}

Il programmatore, noto anche come Network, è una società controllata da una società di maggiori dimensioni (corporation) che possiede e gestisce uno o più canali.

## requestorID {#requestorid-def}

L&#39;ID utilizzato da una Media Company per identificare se stessa o una controllata di un MVPD.  A seconda dell&#39;implementazione del programmatore, questo potrebbe essere mappato a una Media Company, un programmatore o un canale.  L&#39;ID più comune utilizzato da una Media Company per identificare se stessa o una controllata di un MVPD.  A seconda dell&#39;implementazione del programmatore, questo potrebbe essere mappato a una Media Company, un programmatore o un canale.  Tradizionalmente, mappato su un canale.  Con la creazione di pseudo-canali come MML (March Madness Live) e mosse tecnicamente per risolvere i limiti dei dati basati su MVPD, requestorID sta iniziando a diventare più associato con Media Company.

## resourceID {#resource-id-def}

Contenuto richiesto dall’utente finale.  Tradizionalmente, questo ha identificato il canale associato al contenuto richiesto dall’utente.  I miglioramenti del sistema consentono a tale ID di rappresentare programmi specifici (ad esempio con valutazioni specifiche), l&#39;ID continua a identificare il Canale associato.

## Indice dei rischi - Utilizzo {#risk-index-usage}

Noto anche come Utilizzo da account condivisi, è un valore calcolato in base al numero di richieste di riproduzione effettuate da ciascun account ponderato dalla probabilità di condivisione di ciascun account. È anche noto come Utilizzo per Indice di rischio dei conti condivisi.

## Segmento {#segmet-def}

Il segmento è un insieme di account che soddisfano le condizioni definite dall’utente specificate dalle metriche selezionate (ad esempio &quot;utenti di MVPD A, B, C, D o E che hanno guardato i canali X, Y o Z&quot;).

## Livello di condivisione {#sharing-level-def}

Noto anche come Indice dei rischi - Indice dei conti o Indice dei rischi dei conti condivisi, è un valore calcolato in base alla media della probabilità di condivisione calcolata per ogni conto nell&#39;insieme di MVPD selezionati che è stato trasmesso da uno dei canali programmatori selezionati durante l&#39;intervallo di tempo selezionato.

## Dispositivo statico {#static-device-def}

Un dispositivo a mobilità molto bassa. Ad esempio, console giochi, set top box e televisore.

## Intervallo temporale {#time-frame-def}

Noto anche come slot per periodo o per ora, è la finestra di tempo che contiene l&#39;attività di richiesta di riproduzione rappresentata nell&#39;interfaccia utente e le tabelle dall&#39;inizio alla fine.

## MVPD principali nel segmento {#top-mvpds-def}

Gli MVPD principali (al massimo 10) nel segmento selezionato come misura per il livello di condivisione, l&#39;utilizzo dagli account condivisi o il punteggio di condivisione complessivo.

## Tendenza {#trend-def}

La differenza percentuale nella metrica associata (ad esempio, percentuale delle richieste di riproduzione totali) tra il periodo corrente e quello precedente.

## Sottoscrittori univoci {#unique-subscriber-def}

Il numero di account MVPD univoci per un determinato periodo di tempo che hanno interagito con programmi TV Everywhere app o siti che coinvolgono Adobe Pass per un determinato periodo di tempo.  Tale interazione include qualsiasi attività sull&#39;app o sul sito programmatore che si traduce in una chiamata a un servizio Adobe Pass. Ad esempio, controllare lo stato authN o authZ, l&#39;autenticazione e l&#39;autorizzazione. Il numero totale di abbonati univoci includerà anche il numero di dispositivi univoci se l&#39;uso di un programmatore di Adobe TempPass (che è anteprima gratuita) fa parte del segmento.

## Utilizzo {#usage-defs}

### Utente Avid {#avid-user-def}

Più di 37 richieste di riproduzione al mese.

### Utente frequente {#infrequent-users-def}

Meno di 9 richieste di riproduzione al mese.

### Utente regolare {#regular-user-def}

Da 9 a 37 richieste di riproduzione al mese.

## Pattern di utilizzo {#usage-patern-def}

Una delle etichette di categoria finite applicate a un account che meglio caratterizza gli utenti dell&#39;account in termini di gruppi o comportamenti sociali (ad esempio, una piccola famiglia, un viaggiatore o pendolare, condivisione social sharing, ecc.).

## Codice postale {#zip-code-def}

Il codice postale degli Stati Uniti associato alle posizioni all&#39;interno degli Stati Uniti
