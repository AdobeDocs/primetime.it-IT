---
title: Note sulla versione PTAI 19.11.1
description: Le note sulla versione di PTAI 19.11.1 descrivono le novità o le modifiche, i problemi risolti e noti in Primetime Dynamic Ad Insertion nel 2019.
translation-type: tm+mt
source-git-commit: ededb36a0b460fff4644a3716b36971ff9454c37

---


# Note sulla versione Primetime Dynamic Ad Insertion 19.11.1

Le note sulla versione Dynamic Ad Insertion 19.11.1 descrivono i problemi nuovi o modificati, risolti e noti in Primetime Dynamic Ad Insertion nel 2019.

## Novità di PTAI 19.11.1

**Quando:** Lunedì 4 novembre 2019 alle 12:01 AM alle 01:00 AM EST

Aggiornamenti di manutenzione.

## Modifiche apportate alle versioni precedenti

### Versione 19.10.2

**Quando:** Giovedì 31 ottobre 2019 dalle 01:00 alle 03:00 AM Eastern

Aggiornamenti di manutenzione.

### Versione 19.10.1

**Quando:**  Martedì 22 ottobre alle 01:00 AM alle 02:00 AM EST

Aggiornamenti di manutenzione.

### Versione 19.9.1

**Quando:** Martedì 10 settembre 2019 alle 12:30 AM alle 2:00 Ora orientale

Aggiornamenti di sicurezza

### Versione 19.8.3

**Quando:** Mercoledì 28 agosto 2019, 12:30 - 01:30 AM EST

È stato corretto un bug in seguito al quale i lettori Chromecast uscivano inaspettatamente dalla riproduzione quando i segmenti pubblicitari uscivano dalla finestra DVR.

### Versione 19.8.2

**Quando:** Mercoledì 21 agosto 2019 2:00 AM alle 3:00 Ora orientale

* Dashboard SSAI: Sezione Stato sessione. Potete esportare gli eventi di sessione tramite l’opzione Scarica CSV.
* Aggiornamenti di manutenzione

### Versione 19.8.1

**Quando:** Martedì 6 agosto 2019 2:30 Ora orientale a Martedì 6 agosto 2019 4:30 Ora orientale

* Dashboard SSAI: Aggiunta di una nuova sezione, Stati sessione, al dashboard SSAI
   * Se disponete dell&#39;ID sessione per una sessione SSAI in cui è stata attivata la modalità di debug (ptdebug=true), sarete in grado di verificare la seguente attività che si è verificata in quella sessione:
      * Richieste di annuncio/risposte
      * Annunci inseriti
      * beacon attivati (solo per il monitoraggio lato server)
   * Puoi cercare attività per un ID sessione specifico fino a 30 giorni dopo la sessione SSAI
   * Potete esportare gli eventi
* Database: Aggiornamenti di sicurezza

### Versione 19.7.1

**Quando:** Mercoledì, 10 luglio

* SSAI: Per i valori ptcueformat che supportano il segnale EXT-X-CUE-OUT e break nei flussi live, è stata aggiunta una macro generica per trasmettere i dati dagli attributi nell&#39;esempio di tag EXT-X-ASSET: Tag che accompagna il tag #EXT-X-CUE-OUT: #EXT-X-ASSET:CAID=75BCD15,GENRE=News,Program=NewsA10 Macro: # può essere utilizzato per trasmettere News (dall&#39;attributo GENRE) a un URL di chiamata annuncio # può essere utilizzato per trasmettere NewsAt10 (dall&#39;attributo Program) a un URL di chiamata annuncio Eccezione: Per compatibilità con versioni precedenti, # e # hanno la stessa funzionalità. Entrambe le macro possono essere utilizzate per trasmettere il valore dell&#39;attributo CAID, dopo la conversione del valore da esadecimale a lungo Il valore lungo è 123456789 per il valore esadecimale, 75BCD15, nell&#39;esempio precedente. Entrambe le macro vengono utilizzate per passare 123456789 a un URL di chiamata di annuncio La macro inizia sempre con #. La macro fa distinzione tra maiuscole e minuscole, ma l&#39;attributo nel tag EXT-X-ASSET non lo è. In altre parole, PROGRAMMA e Programma sono entrambi consentiti nel tag EXT-X-ASSET
* SSAI: Modifiche alla configurazione per un cliente specifico per quanto segue:
   * Durata di quattro minuti della finestra scorrevole (playlist dal vivo)
   * Se viene generata un&#39;eccezione di timeout del socket quando il server manifesto recupera il contenuto di origine, il server manifesto restituirà il codice di risposta HTTP (404) invece di 500
* Aggiornamenti di sicurezza

### Versione 19.6.1

**Quando:** Mercoledì 12 giugno 2019 11:30 PM PST a giovedì 13 giugno 2019 12:30 PST

* CRS: Regola di normalizzazione per i creativi di RevJet
   * È stata aggiunta la regola di normalizzazione creativa degli URL per RevJet, utilizzata da CRS e SSAI
   * TVSDK: Se servite o pianificate di distribuire annunci da RevJet, le regole di normalizzazione dovranno essere aggiunte al JSON delle regole CRS per utilizzare CRS con i loro creativi. Per assistenza, contattate l&#39;Account Manager tecnico
* CRS: Regola di normalizzazione per i creativi di Innovid
   * È stata aggiunta la regola di normalizzazione creativa degli URL per Innovid, utilizzata da SSAI
   * La regola di normalizzazione utilizzata da CRS è stata aggiunta in una versione precedente
   * TVSDK: La regola di normalizzazione da aggiungere nel JSON delle regole del CRS è stata fornita dopo una release precedente, ma per essere sicuro, parla con il tuo Account Manager tecnico per rivedere tutte le regole di normalizzazione in vigore.
      >[!NOTE]
      >
      >La maggior parte degli URL creativi Invid verranno transcodificati e cuciti correttamente senza la regola di normalizzazione. Occasionalmente, tuttavia, vengono incontrati URL creativi Innovid con parametri dinamici. La regola di normalizzazione è necessaria per gestire queste istanze.

### Versione 19.5.2

**Quando:** Mercoledì 22 Maggio 2:30 Ora orientale a Mercoledì 22 Maggio 4:30 Ora orientale

* È stato aggiunto il supporto per CMAF (contenuto HLS/fMP4)
   * SSAI: Gestione dei manifesti CMAF
   * SSAI: Avviare richieste di transcodifica e recuperare risorse CRS in base al formato di contenuto (HLS/ts e HLS/fMP4)
   * CRS: È stato aggiunto un flusso di lavoro per ricompilare gli annunci in formato CMAF (HLS/fMP4)
* SSAI: È stato risolto un problema che impediva l&#39;inserimento di annunci non muxed in contenuto non muxed, quando sia il contenuto che l&#39;annuncio non disponevano di flussi solo audio (EXT-X-STREAM-INF)
* SSAI: È stato aggiunto il supporto per i token di autenticazione CDN Limelight (LLNW) per i segmenti di contenuto
   * Quando `pttoken=limelight` o `pttoken=llnw` viene aggiunto all’URL del programma di avvio, al momento del recupero della playlist principale di origine verrà aggiunta un’intestazione segreta, quindi verranno aggiunti i parametri di query dall’intestazione X-Adobe-Sig di LLNW ai segmenti di contenuto
* SSAI: È stato aggiunto un altro valore di token (`pttoken=centurylink`) per il supporto del token di autenticazione CDN CenturyLink, rilasciato il 30 luglio 2018
   * `pttoken=centurylink` ha lo stesso comportamento `pttoken=level3`e entrambi i valori sono validi

### Versione 19.5.1

**Quando:** Giovedì 9 Maggio 2:30 AM Ora orientale a Giovedi 9 Maggio 4:30 Ora orientale

* SSAI: Aggiornamenti di sicurezza
* Dashboard CRS: La stringa &quot;Esempio FqAdId&quot; è stata troncata a 255 caratteri a causa di vincoli di archiviazione dei dati (8 bit)
   * La stringa &quot;FqAdId Sample&quot; include Ad System e Ad ID da ogni risposta XML nella catena Wrapper dell’annuncio per gli inserimenti di tutti gli annunci CRS con SSAI (sezione Creative Stats del dashboard CRS)
* Dashboard SSAI e CRS: Aggiornamenti delle versioni software

### Versione 19.4.1

**Quando:** Mercoledì 10 Aprile 2:30 Ora orientale a Mercoledì 10 Aprile 4:30 Ora orientale

* CRS: L&#39;API CRS Repackage non supporterà più i comandi HTTP POST. L&#39;API CRS Repackaging reindirizzerà automaticamente (301) i comandi HTTP POST a HTTPS
   * A partire dal 20 maggio, il reindirizzamento HTTP->HTTPS per i comandi HTTP POST verrà disattivato
   * Se utilizzate l&#39;API CRS Repackage per rigenerare gli annunci in anticipo, passate i comandi POST su HTTPS entro il 20 maggio
* CRS: Architettura e flusso di lavoro riprogettati per caricare le risorse CRS nelle origini CDN dei clienti
   * I processi di processo per origine CDN sono separati, quindi i colli di bottiglia di caricamento per un’origine CDN non influiranno sui caricamenti in altre origini CDN
   * Altri vantaggi: Sono stati migliorati i tempi di elaborazione dei processi CRS e le frequenze di caricamento per le origini CDN dei clienti
* SSAI: Sono stati aggiunti gli URL ClickThrough e ClickTracking per i video pubblicitari nel formato JSON v2 collaterale
   * Una nuova proprietà array JSON, &quot;videoClicks&quot;, seguirà la proprietà &quot;trackingURLs&quot;
   * I nomi dei valori &quot;event&quot; saranno &quot;clickThrough&quot; e &quot;clickTracking&quot; e non avranno un valore startTime
* SSAI: Per le risorse CRS, è stata aggiunta una funzionalità per estendere la scadenza del record di ricerca di una risorsa CRS di 30 giorni ogni volta che viene inserita
   * Comportamento precedente: I record di ricerca delle risorse CRS vengono memorizzati in memcache in ciascun contenitore. I record di ricerca delle risorse CRS vengono automaticamente rimossi 30 giorni dopo essere stati aggiunti a memcache. Per popolare nuovamente il record di ricerca delle risorse CRS di un creativo in un contenitore dopo che questo è stato rimosso da memcache, è necessario che la creatività si trovi 3 volte in tale contenitore
   * Nuovo comportamento: Quando un contenitore accede a un record di ricerca delle risorse CRS per inserire la risorsa CRS, la scadenza del record di ricerca delle risorse CRS verrà prorogata di 30 giorni in tale contenitore. Di conseguenza, le risorse CRS usate di frequente non verranno rimosse dalla cache delle memcache di un contenitore fino a 30 giorni dopo l’ultimo utilizzo
   * Il nuovo comportamento è ampio e può essere disattivato se viene rilevato un calo di prestazioni
* SSAI: Comportamento di manipolazione del manifesto WebVTT aggiornato solo per i flussi live
   * Comportamento precedente: Solo nel manifesto WebVTT, rimuovere i tag EXT-X-DISCONTINUITY che sarebbero inseriti prima di ogni annuncio inserito e dopo l&#39;ultimo segmento dell&#39;annuncio inserito
   * Nuovo comportamento: Aggiunto un nuovo parametro, vttdisk, con valori accettati di true e false, all&#39;URL SSAI per il bootstrap
      * vttdisc=true: I tag EXT-X-DISCONTINUITY verranno inseriti nel manifesto WebVTT prima di ogni annuncio inserito e dopo l&#39;ultimo segmento dell&#39;interruzione annuncio inserita, in modo da corrispondere al comportamento per i manifesti solo audio/video e audio
      * vttdisc=false (come nel comportamento precedente): Solo nel manifesto WebVTT, rimuovere i tag EXT-X-DISCONTINUITY che sarebbero inseriti prima di ogni annuncio inserito e dopo l&#39;ultimo segmento dell&#39;annuncio inserito
      * Se il parametro vttdisc viene omesso o ha un valore diverso da true/false, per impostazione predefinita vttdisc corrisponde a true
* SSAI: Aggiornamenti di sicurezza e versioni software
   * Java: È stata aggiornata la versione Java per supportare altre suite cifrate per le chiamate ad annunci effettuate tramite TLS 1.2 (HTTPS)

### Versione 19.2.1

**Quando:** Mercoledì 20 febbraio 2019 1:30 Ora orientale a Mercoledì 20 febbraio 2019 3:30 Ora orientale

* SSAI: Sono stati aggiunti gli URL ClickThrough e ClickTracking per i video pubblicitari nel formato JSON v2 collaterale
   * Nella proprietà &quot;trackingURLs&quot;, i nomi dei valori &quot;event&quot; saranno &quot;clickthrough&quot; e &quot;clickTracking&quot;
   * I loro valori startTime saranno l&#39;inizio dell&#39;annuncio
* SSAI: Per le risorse CRS, è stata aggiunta una funzionalità per estendere la scadenza del record di ricerca di una risorsa CRS di 30 giorni ogni volta che viene inserita
   * Comportamento precedente: I record di ricerca delle risorse CRS vengono memorizzati in memcache in ciascun contenitore. I record di ricerca delle risorse CRS vengono automaticamente rimossi 30 giorni dopo essere stati aggiunti a memcache. Per popolare nuovamente il record di ricerca delle risorse CRS di un creativo in un contenitore dopo che questo è stato rimosso da memcache, è necessario che la creatività si trovi 3 volte in tale contenitore
   * Nuovo comportamento: Quando un contenitore accede a un record di ricerca delle risorse CRS per inserire la risorsa CRS, la scadenza del record di ricerca delle risorse CRS verrà prorogata di 30 giorni in tale contenitore. Di conseguenza, le risorse CRS usate di frequente non verranno rimosse dalla cache delle memcache di un contenitore fino a 30 giorni dopo l’ultimo utilizzo
   * Il nuovo comportamento è ampio e può essere disattivato se viene rilevato un calo di prestazioni

* SSAI: Aggiornamenti delle versioni software per NGINX e Kafka
   * NGINX e Kafka sono utilizzati per attivare URL di tracciamento annunci lato server e inviare dati ai dashboard SSAI e CRS
* CRS: Miglioramenti delle prestazioni del dashboard CRS

### Versione dell&#39;interfaccia Web

**Quando:** Mercoledì 13 febbraio, 4:00 AM - 4:30 AM Pacifico

**Cosa:** Componente Primetime e Decisioni dell’interfaccia utente Web

* È stato corretto il problema relativo all&#39;interfaccia utente del calendario a causa del quale l&#39;utente non poteva selezionare una data oltre il 31 dicembre 2018 dal componente del calendario durante il traffico di una campagna o il pulling di un rapporto.

### Versione 19.1.2

**Quando:** Mercoledì 30 gennaio 2019 1:30 Ora orientale a Mercoledì 30 Gennaio 3:30 Ora orientale

* SSAI: È stata aggiornata la struttura chiave di ricerca utilizzata da SSAI per memorizzare e recuperare risorse CRS, in modo da gestire gli scenari in cui i fornitori di annunci pubblicitari dispongono di un ID Annuncio dinamico o Creative ID per lo stesso annuncio
   * Nuova struttura chiave di ricerca: Parametri relativi a area, URL creativo e formato (durata target, formato di output, CDN di destinazione)
   * Vecchia struttura chiave di ricerca: Zone, Ad System, Ad ID, Creative ID, Creative URL e parametri di formato (durata target, formato di output, CDN di destinazione)
   * Le chiavi di ricerca per le risorse CRS esistenti verranno aggiornate in modo da corrispondere alla nuova struttura prima della release di produzione, ma si noti che le nuove risorse transcodificate tra l&#39;aggiornamento delle chiavi di ricerca e la release di produzione potrebbero non essere disponibili. In tal caso, avvierebbero una nuova richiesta CRS al successivo rilevamento dopo il rilascio

* CRS: Aggiunta la possibilità di richieste CRS blacklist/whitelist da sistemi di annunci pubblicitari, ID di annunci, ID creativi, URL creativi e/o formato creativo specifici

   >Nota
   >
   >Adobe aggiungerà delle regole per la blacklist quando verranno trovati fornitori di annunci con valori dinamici (ad esempio, parametri dinamici in URL) per lo stesso annuncio. Tali regole della blacklist verranno disattivate dopo che il componente dinamico è stato risolto, dal provider o tramite una regola di normalizzazione.

   * Se desiderate aggiungere una regola di blacklist o whitelist per la vostra zona, rivolgetevi al vostro responsabile dell&#39;account tecnico per assistenza.

### Versione 19.1.1

**Quando:** Mercoledì 9 gennaio 2019 1:30 Ora orientale a Mercoledì 9:30 Ora orientale

* È stato risolto un problema che causava un errore durante la convalida delle risorse creative in entrata ospitate su total-stream.net a causa di una errata interpretazione delle intestazioni di conservazione HTTP.
* È stato risolto un problema a causa del quale le virgolette singole (&#39;) e doppie (&quot;) in ID annuncio, ID creativo e altri campi per una richiesta di ricompilazione causavano il fallimento della richiesta di reimballaggio.
* Passato a Java long (tipo di dati) per risolvere un problema per il quale il raggiungimento del limite Java int di 2.147.483.647 nei valori ID processo di transcodifica causerebbe il fallimento di tutte le richieste di ricompilamento.
* Ottimizzazioni del database.

## Problemi risolti

Se la risoluzione è associata a un problema segnalato, viene visualizzato un riferimento Zendesk. Ad esempio, ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - Le risposte Json per le regole CRS vengono memorizzate nella cache per evitare richieste duplicate.

## Problemi noti e limitazioni

**PTAI 19.7.1**

Nessuna nuova limitazione aggiunta.
