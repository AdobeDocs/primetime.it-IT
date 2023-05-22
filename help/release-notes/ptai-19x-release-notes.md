---
title: Note sulla versione di PTAI 19.11.1
description: Le note sulla versione di PTAI 19.11.1 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Ad Insertion nell’anno 2019.
exl-id: 0cc9067c-cd46-48f4-afa4-de8b15193723
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 0%

---

# Note sulla versione di Primetime Ad Insertion 19.11.1

Le note sulla versione di Primetime Ad Insertion 19.11.1 descrivono le novità o le modifiche, i problemi risolti e i problemi noti in Primetime Ad Insertion nel 2019.

## Novità di PTAI 19.11.1

**Quando:** Lunedì 4 novembre 2019 alle 01:00 CET

Aggiornamenti di manutenzione.

## Modifiche apportate alle versioni precedenti

### Versione 19.10.2

**Quando:** Giovedì 31 ottobre 2019 dalle 01:00 alle 03:00 CET

Aggiornamenti di manutenzione.

### Versione 19.10.1

**Quando:**  Martedì 22 ottobre alle 01:00 alle 02:00 CET

Aggiornamenti di manutenzione.

### Versione 19.9.1

**Quando:** Martedì 10 settembre 2019 alle 00:30 alle 02:00 fuso orientale

Aggiornamenti di sicurezza

### Versione 19.8.3

**Quando:** Mercoledì 28 agosto 2019, 12:30 - 01:30 AM ORIENTALE

È stato corretto un bug a causa del quale i lettori Chromecast terminavano in modo imprevisto la riproduzione quando i segmenti pubblicitari venivano trasferiti dalla finestra del DVR.

### Versione 19.8.2

**Quando:** Mercoledì 21 agosto 2019 dalle 02:00 alle 03:00 fuso orientale

* Dashboard SSAI: sezione Statistiche sessione. Puoi esportare gli eventi della sessione tramite l’opzione Scarica CSV.

* Aggiornamenti di manutenzione

### Versione 19.8.1

**Quando:** Martedì 6 agosto 2019 2:30 Ora orientale a Martedì 6 agosto 2019 4:30 Ora orientale

* Dashboard SSAI: aggiunta nuova sezione, Statistiche sessione, al dashboard SSAI
   * Se si dispone dell&#39;ID sessione per una sessione SSAI con la modalità di debug abilitata (ptdebug=true), sarà possibile cercare la seguente attività che si è verificata nella sessione:
      * Richieste/risposte di annunci
      * Annunci inseriti
      * Beacon attivati (solo tracciamento lato server)
   * Puoi cercare l’attività per un ID sessione specifico fino a 30 giorni dopo lo svolgimento della sessione SSAI
   * Puoi esportare gli eventi
* Database: aggiornamenti di sicurezza

### Versione 19.7.1

**Quando:** Mercoledì 10 luglio

* SSAI: per i valori ptcueformat che supportano la segnalazione di interruzione pubblicitaria EXT-X-CUE-OUT nei flussi live, è stata aggiunta una macro generica per passare i dati dagli attributi nel tag EXT-X-ASSET Esempio: Tag che accompagna il tag #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=News,Program=NewsAt10 Macro: # può essere utilizzato per passare News (dall&#39;attributo GENRE) a un URL di ad call # può essere utilizzato per passare NewsAt10 (dall&#39;attributo Program) a un URL di ad call Eccezione: per compatibilità con le versioni precedenti, # e # hanno la stessa funzionalità. Entrambe le macro possono essere utilizzate per trasmettere il valore dell&#39;attributo CAID, dopo aver convertito il valore da hex a long. Nell&#39;esempio precedente, il valore long viene 123456789 per il valore hex, 75BCD15. Entrambe le macro vengono utilizzate per passare 123456789 a un URL di ad call. La macro inizia sempre con #. La macro distingue tra maiuscole e minuscole, ma l&#39;attributo nel tag EXT-X-ASSET non lo è. In altre parole, PROGRAM e Program sono entrambi consentiti nel tag EXT-X-ASSET
* SSAI: modifiche alla configurazione per un cliente specifico per i seguenti elementi:
   * Finestra scorrevole (playlist live) di quattro minuti
   * Se viene generata un&#39;eccezione di timeout del socket quando Manifest Server recupera il contenuto sorgente, Manifest Server restituirà il codice di risposta HTTP (404) invece di 500
* Aggiornamenti di sicurezza

### Versione 19.6.1

**Quando:** Mercoledì 12 giugno 2019 11:30 PST a giovedì 13 giugno 2019 12:30 PST

* CRS: regola di normalizzazione per i creativi di RevJet
   * Aggiunta della regola di normalizzazione URL creativo per RevJet, utilizzata da CRS e SSAI
   * TVSDK: se distribuisci o prevedi di distribuire annunci da RevJet, sarà necessario aggiungere le regole di normalizzazione al JSON delle regole CRS per poter utilizzare CRS con i loro creativi. Contatta il tuo Technical Account Manager per ricevere assistenza
* CRS: regola di normalizzazione per i creativi di Innovid
   * Aggiunta regola di normalizzazione URL creativo per Innovid, utilizzata da SSAI
   * La regola di normalizzazione utilizzata da CRS è stata aggiunta in una versione precedente
   * TVSDK: la regola di normalizzazione da aggiungere nelle regole CRS JSON è stata fornita dopo una versione precedente, ma per sicurezza, parla con il tuo Technical Account Manager per rivedere tutte le regole di normalizzazione in vigore.

      >[!NOTE]
      >
      >La maggior parte degli URL creativi di Innovid verrà transcodificata e unita correttamente senza la regola di normalizzazione. Occasionalmente, tuttavia, si verificano URL creativi Innovid con parametri dinamici. Per gestire queste istanze è necessaria la regola di normalizzazione.

### Versione 19.5.2

**Quando:** Mercoledì 22 maggio 20:30 Ora orientale mercoledì 22 maggio 20:30 Ora orientale

* È stato aggiunto il supporto per CMAF (contenuto HLS/fMP4)
   * SSAI: gestire manifesti CMAF
   * SSAI: avvia le richieste di transcodifica e recupera le risorse CRS in base al formato del contenuto (HLS/ts e HLS/fMP4)
   * CRS: è stato aggiunto un flusso di lavoro per ricompilare gli annunci in formato CMAF (HLS/fMP4)
* SSAI: è stato risolto un problema che impediva l’inserimento di annunci senza audio nel contenuto senza audio, quando sia il contenuto che l’annuncio non hanno flussi di sola audio (EXT-X-STREAM-INF)
* SSAI: aggiunto supporto per i token di autenticazione CDN Limelight (LLNW) per i segmenti di contenuto
   * Quando `pttoken=limelight` o `pttoken=llnw` viene aggiunto all’URL di avvio, verrà aggiunta un’intestazione segreta durante il recupero della playlist principale di origine, quindi verranno aggiunti ai segmenti di contenuto i parametri di query dall’intestazione X-Adobe-Sig di LLNW
* SSAI: aggiunto un altro valore pttoken (`pttoken=centurylink`) per il supporto del token di autenticazione CDN CenturyLink, rilasciato il 30 luglio 2018
   * `pttoken=centurylink` ha lo stesso comportamento di `pttoken=level3`ed entrambi i valori sono validi

### Versione 19.5.1

**Quando:** Giovedì, 9 maggio 2:30 Ora orientale a Giovedì, 9 maggio 4:30 Ora orientale

* SSAI: Aggiornamenti di sicurezza
* Dashboard CRS: la stringa &quot;FqAdId Sample&quot; è stata troncata a 255 caratteri a causa di vincoli di archiviazione dei dati (8 bit)
   * La stringa &quot;Esempio FqAdId&quot; include l’Ad System e l’ID di ogni risposta XML nella catena Wrapper dell’annuncio per gli inserimenti di tutti gli annunci CRS con SSAI (sezione Creative Stats del CRS Dashboard)
* Dashboard SSAI e CRS: aggiornamenti della versione del software

### Versione 19.4.1

**Quando:** Mercoledì 10 aprile 2:30 Ora orientale a Mercoledì 10 aprile 10 4:30 Ora orientale

* CRS: l’API di reimballaggio CRS non supporterà più i comandi HTTP POST. L’API di reindirizzamento CRS reindirizzerà automaticamente i comandi HTTP POST (301) a HTTPS
   * A partire dal 20 maggio, il reindirizzamento HTTP->HTTPS per i comandi HTTP POST verrà disattivato
   * Se utilizzi l’API di reimballaggio CRS per ricompilare gli annunci in anticipo, imposta i comandi POST su HTTPS entro il 20 maggio
* CRS: riprogettazione dell’architettura e del flusso di lavoro per caricare le risorse CRS sulle origini CDN dei clienti
   * I processi di lavoro per origine CDN sono separati, pertanto i colli di bottiglia per il caricamento di un’origine CDN non influiranno sui caricamenti in altre origini CDN
   * Altri vantaggi: sono stati migliorati i tempi di elaborazione dei processi CRS e le percentuali di caricamento sulle origini CDN dei clienti
* SSAI: sono stati aggiunti URL di click-through e tracciamento dei clic per annunci video al formato JSON v2 sidecar
   * Una nuova proprietà array JSON, &quot;videoClicks&quot;, seguirà la proprietà &quot;trackingURLs&quot;
   * I nomi dei valori &quot;event&quot; saranno &quot;clickThrough&quot; e &quot;clickTracking&quot; e non avranno un valore startTime
* SSAI: per le risorse CRS, è stata aggiunta la funzionalità per estendere la scadenza dei record di ricerca di una risorsa CRS di 30 giorni a partire da quando viene inserita
   * Comportamento precedente: i record di ricerca delle risorse CRS vengono memorizzati in memcache in ogni pod. I record di ricerca delle risorse CRS vengono rimossi automaticamente 30 giorni dopo l’aggiunta a memcache. Per ripopolare il record di ricerca di risorse CRS di un creativo in un pod dopo che è stato rimosso da memcache, tale creativo deve essere rilevato 3 volte in tale pod
   * Nuovo comportamento: quando un pod accede a un record di ricerca di risorse CRS per inserire la risorsa CRS, la scadenza del record di ricerca delle risorse CRS viene estesa di 30 giorni in tale pod. Di conseguenza, le risorse CRS utilizzate di frequente non verranno rimosse dalla memcache di un pod fino a 30 giorni dopo l’ultimo utilizzo
   * Il nuovo comportamento è a livello di sistema e può essere disattivato se viene rilevato un calo delle prestazioni
* SSAI: comportamento di manipolazione del manifesto WebVTT aggiornato solo per flussi live
   * Comportamento precedente: solo nel manifesto WebVTT, rimuovi i tag EXT-X-DISCONTINUITY che verrebbero inseriti prima di ogni annuncio inserito e dopo l’ultimo segmento dell’interruzione pubblicitaria inserita
   * Nuovo comportamento: è stato aggiunto un nuovo parametro, vttdisc, con valori accettati true e false, all’URL di bootstrap di SSAI
      * vttdisc=true: i tag EXT-X-DISCONTINUITY verranno inseriti nel manifesto WebVTT prima di ogni annuncio inserito e dopo l’ultimo segmento dell’interruzione pubblicitaria inserita, in modo da corrispondere al comportamento per i manifesti audio/video e solo audio
      * vttdisc=false (come il comportamento precedente): solo nel manifesto WebVTT, rimuovi i tag EXT-X-DISCONTINUITY che verrebbero inseriti prima di ogni annuncio inserito e dopo l’ultimo segmento dell’interruzione pubblicitaria inserita
      * Se il parametro vttdisc viene omesso o ha un valore diverso da true/false, il valore predefinito di vttdisc sarà true
* SSAI: Aggiornamenti di sicurezza e aggiornamenti delle versioni del software
   * Java: è stata aggiornata la versione Java per supportare suite di cifratura aggiuntive per le chiamate pubblicitarie attivate tramite TLS 1.2 (HTTPS)

### Versione 19.2.1

**Quando:** Mercoledì 20 febbraio 2019 1:30 Ora orientale a Mercoledì 20 febbraio 2019 3:30 Ora orientale

* SSAI: sono stati aggiunti URL di click-through e tracciamento dei clic per annunci video al formato JSON v2 sidecar
   * Nella proprietà &quot;trackingURLs&quot;, i nomi dei valori &quot;event&quot; saranno &quot;clickthrough&quot; e &quot;clickTracking&quot;
   * I valori startTime rappresentano l’inizio dell’annuncio
* SSAI: per le risorse CRS, è stata aggiunta la funzionalità per estendere la scadenza dei record di ricerca di una risorsa CRS di 30 giorni a partire da quando viene inserita
   * Comportamento precedente: i record di ricerca delle risorse CRS vengono memorizzati in memcache in ogni pod. I record di ricerca delle risorse CRS vengono rimossi automaticamente 30 giorni dopo l’aggiunta a memcache. Per ripopolare il record di ricerca di risorse CRS di un creativo in un pod dopo che è stato rimosso da memcache, tale creativo deve essere rilevato 3 volte in tale pod
   * Nuovo comportamento: quando un pod accede a un record di ricerca di risorse CRS per inserire la risorsa CRS, la scadenza del record di ricerca delle risorse CRS viene estesa di 30 giorni in tale pod. Di conseguenza, le risorse CRS utilizzate di frequente non verranno rimosse dalla memcache di un pod fino a 30 giorni dopo l’ultimo utilizzo
   * Il nuovo comportamento è a livello di sistema e può essere disattivato se viene rilevato un calo delle prestazioni

* SSAI: Aggiornamenti delle versioni software per NGINX e Kafka
   * NGINX e Kafka vengono utilizzati per attivare gli URL di tracciamento degli annunci lato server e inviare dati alle dashboard SSAI e CRS
* CRS: miglioramenti delle prestazioni del dashboard CRS

### Versione interfaccia web

**Quando:** Mercoledì 13 febbraio, 04:00 - 04:30 Pacifico

**Cosa:** Componente interfaccia utente Web di Primetime ad Decisioning

* È stato risolto il problema relativo all’interfaccia utente del calendario a causa del quale l’utente non poteva selezionare una data successiva al 31 dicembre 2018 dal componente calendario durante il traffico di una campagna o l’estrazione di un rapporto.

### Versione 19.1.2

**Quando:** Mercoledì 30 gennaio 2019 1:30 Ora orientale a Mercoledì 30 gennaio 30:30 Ora orientale

* SSAI: è stata aggiornata la struttura della chiave di ricerca utilizzata da SSAI per memorizzare e recuperare le risorse CRS al fine di gestire scenari in cui i provider di annunci hanno un ID annuncio o un ID creativo dinamico per lo stesso annuncio
   * Nuova struttura della chiave di ricerca: zona, URL creativo e parametri di formato (durata di destinazione, formato di output, CDN di destinazione)
   * Vecchia struttura della chiave di ricerca: zona, sistema di annunci, ID annuncio, ID creativo, URL creativo e parametri di formato (durata target, formato di output, CDN di destinazione)
   * Le chiavi di ricerca per le risorse CRS esistenti verranno aggiornate per corrispondere alla nuova struttura prima del rilascio della versione di produzione, ma tieni presente che le nuove risorse trascodificate tra l’aggiornamento delle chiavi di ricerca e il rilascio della versione di produzione potrebbero non essere utilizzate. In tal caso, avvierebbe una nuova richiesta CRS la volta successiva che si verifica dopo il rilascio

* CRS: è stata aggiunta la possibilità di elenco Bloccati/elenco consentiti di richieste CRS da sistemi di annunci specifici, ID di annunci, ID creativi, URL creativi e/o formato creativo

   >Nota
   >
   >Adobe aggiungerà regole di elenco Bloccati quando vengono trovati provider di annunci con valori dinamici (ad esempio, parametro dinamico nell’URL) per lo stesso annuncio. Tali regole di elenco Bloccati verranno disattivate dopo la risoluzione del componente dinamico, da parte del provider o tramite una regola di normalizzazione.

   * Se desideri aggiungere un elenco Bloccati o una regola di elenco consentiti per la tua zona, contatta il tuo Technical Account Manager per assistenza.

### Versione 19.1.1

**Quando:** Mercoledì 9 gennaio 2019 1:30 Ora orientale a Mercoledì 9 gennaio 3:30 Ora orientale

* È stato risolto un problema a causa del quale l’interpretazione errata delle intestazioni keep-alive HTTP poteva causare un errore durante la convalida delle risorse creative in entrata ospitate su total-stream.net.
* È stato risolto un problema a causa del quale le virgolette singole (&#39;) e le virgolette doppie (&quot;) in Ad ID, Creative ID e altri campi per una richiesta di riconfezionamento non riuscivano.
* È stato eseguito il passaggio a Java long (tipo di dati) per risolvere un problema per cui il raggiungimento del limite int Java di 2.147.483.647 nei valori ID del processo di transcodifica causerebbe il mancato funzionamento di tutte le richieste di repackaging.
* Ottimizzazioni del database.

## Problemi risolti

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento a Zendesk. Ad esempio, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - Le risposte JSON per le regole CRS vengono memorizzate nella cache per evitare le richieste duplicate.

## Problemi noti e limitazioni

**PTAI 19.7.1**

Non è stata aggiunta alcuna nuova limitazione.
