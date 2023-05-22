---
title: Note sulla versione di TVSDK 2.4.1 per Android
description: Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# Note sulla versione di TVSDK 2.4.1 per Android {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Un Adobe di è il rilascio di TVSDK 2.4.1 per Android.

Per utilizzare questa versione di TVSDK, assicurati che il sistema soddisfi i requisiti descritti in [Requisiti di sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

La documentazione è disponibile qui:

· Guida in linea di TVSDK 2.4 per Android

· [Javadocs TVSDK 2.4 per API Java Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

I JavaScript sono l’autorità finale, perché vengono generati automaticamente direttamente dal codice sorgente TVSDK.

· [Documentazione API C++ TVSDK 2.4 per API C++ Android](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Ogni classe Java ha una classe C++ corrispondente e la documentazione C++ contiene più materiale esplicativo rispetto ai Java, quindi consulta la documentazione C++ per una comprensione più approfondita dell’API Java.

· Guida alla migrazione ([Guida alla migrazione di TVSDK 2.4 per Android](../migration-guides/tvsdk-14-25-android.md))

Questa guida spiega cosa è necessario modificare per migrare un’applicazione basata su TVSDK 1.4 a un’applicazione basata su TVSDK 2.4.

## Nuove funzioni {#new-features}

TVSDK 2.4.1 per Android offre molti miglioramenti delle prestazioni rispetto alle versioni precedenti. Offre un’esperienza visiva di alta qualità.

Questa versione include tutte le funzionalità delle versioni 2.4 e 2.4.1 e nessuna funzionalità è obsoleta.

Di seguito sono elencate le nuove funzioni chiave della versione 2.4.1:

* Funzioni di HLS versione 4

   * **Riproduzione video** (riproduzione, pausa, ricerca) con controllo del lettore per flussi live, lineari e VOD.
   * **Sottotitoli.** TVSDK è in grado di visualizzare sottotitoli codificati 608/708 con una selezione di font, dimensioni dei font, colori e sfondo. Può anche supportare video con sottotitoli roll-up e passare da una traccia all’altra della lingua, se disponibili.
   * **Modalità di riproduzione dei brani** supporta l&#39;avanzamento rapido e il riavvolgimento per i flussi HLS che utilizzano i-frame. Tutti i controlli di riproduzione video funzionano sul contenuto. Lo slow motion (in avanti) è disponibile per la modalità di riproduzione video esterna con frequenze comprese tra 0 e 1.
   * **Bitrate adattivo (ABR)** consente al lettore di selezionare in modo dinamico quale tra più versioni dello stesso flusso di contenuto riprodurre, in base alla rete e ad altre condizioni. Puoi impostare i parametri in modo dinamico o nel file manifesto per selezionare tra criteri di selezione aggressivi, moderati e conservativi.
   * **Intervalli di byte** abilitare un singolo file TS per contenere più segmenti TS.
   * **Rappresentazioni audio alternative** consente al lettore di passare da una traccia audio disponibile all&#39;altra.
   * **Supporto ID3.** TVSDK può riprodurre flussi audio e video HLS che contengono metadati audio ID3, come il nome dell’artista, il titolo e l’album.
   * **Failover. **TVSDK utilizza strategie per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file delle playlist e dei segmenti.
   * **Pass-through audio multicanale (DD+).** TVSDK può trasmettere i dati audio Dolby Digital Plus (E-AC3) all&#39;hardware di supporto.

* Funzioni di protezione dei contenuti

   * **DRM per HLS.** Tutte le API di riproduzione video funzionano con contenuti video crittografati protetti da Accesso Adobe. Sono supportate le seguenti funzionalità DRM:

      * Rotazione delle licenze
      * Rotazione chiave
      * Memorizzazione delle licenze nella cache
      * Ora criterio
      * Rotazione IV

* **Riproduzione AES 128.** TVSDK è in grado di riprodurre contenuti HLS AES (Advanced Encryption Standard) con una dimensione di chiave di 128 bit.
* **HLS protetto (PHLS)** fornisce un set limitato di regole DRM predefinite, un sottoinsieme di ciò che Adobe Access fornisce, per consentire una DRM leggera su HLS per i flussi live e VOD.

* Contenuti pubblicitari/alternativi e funzioni di monetizzazione

   * **Tracciamento per annunci inseriti lato server.** TVSDK può tenere traccia degli annunci inseriti dal servizio di inserimento di annunci Adobe Cloud. Supporta gli annunci lineari nei formati VAST2, VAST3 e VMAP per i flussi VOD e live/lineari.
   * **Tag HLS personalizzati.** TVSDK utilizza `MediaPlayerConfig` per abilitare la notifica all’applicazione lettore quando nel flusso vengono visualizzati tag HLS personalizzati.
   * **Inserimento di annunci lato client.** La libreria di inserimento di annunci Auditude funziona con i server Adobe Auditude per risolvere dinamicamente gli annunci da inserire nei contenuti live, lineari e VOD, nelle posizioni pre-roll, mid-roll o post-roll.
   * **Ad resolver personalizzati.** Il `ContentResolver, OpportunityGenerator,` e `MediaPlayerClientFactory` Le interfacce consentono di implementare un agente di risoluzione dei contenuti personalizzato/alternativo e di registrare un rilevatore di opportunità personalizzato per l’utilizzo con TVSDK. Il `TestAdResolver` e `AuditudeResolver` Le classi forniscono esempi C++ di implementazione di un resolver di contenuti. Un esempio JavaScript è disponibile all’indirizzo `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento coerente degli annunci.** Utilizza il `AdPolicySelector` per abilitare un comportamento coerente in tutti i lettori per operazioni come la ricerca e la riproduzione con trucco quando gli annunci sono presenti nel contenuto. Se non implementi il tuo, TVSDK utilizza `DefaultAdPolicySelector`.
   * **Rimuovere/sostituire gli annunci C3.** Utilizza l’API TVSDK appropriata per rimuovere intervalli di contenuti personalizzati e inserire dinamicamente nuovi annunci senza ulteriore lavoro di preparazione. Questa funzione è particolarmente utile per la trasmissione di contenuti live o lineari, che vengono immediatamente resi disponibili on-demand senza bisogno di interventi di pulizia.

Di seguito sono elencate le nuove funzioni chiave versione 2.4:

* **Attivazione immediata per VOD e live** Quando attivate l&#39;opzione di attivazione immediata, TVSDK inizializza e memorizza in buffer i contenuti multimediali prima dell&#39;avvio della riproduzione. Perché è possibile avviare più `MediaPlayerItemLoader` istanze simultaneamente in background, puoi bufferizzare più flussi. Quando un utente cambia il canale e il flusso viene memorizzato correttamente nel buffer, la riproduzione sul nuovo canale inizia immediatamente. TVSDK 2.4 supporta anche l&#39;Instant On per i flussi live. I flussi live vengono riinseriti nel buffer quando la finestra live si sposta.

* **Miglioramenti delle prestazioni **La nuova architettura TVSDK 2.4 offre diversi miglioramenti delle prestazioni:

   * **Sottosegmentazione** - TVSDK riduce ulteriormente le dimensioni di ciascun frammento per iniziare la riproduzione il prima possibile.
   * **Download paralleli di annunci** - TVSDK preacquisisce gli annunci in parallelo alla riproduzione del contenuto prima che l’annuncio venga interrotto, consentendo in tal modo una riproduzione fluida di annunci e contenuti.
   * **Risoluzione annuncio lazy** - Grazie a questa funzione, prima di avviare la riproduzione non attendiamo la risoluzione degli annunci non preroll, riducendo così il tempo di avvio. API come seek e trick-play non sono ancora consentite fino a quando tutti gli annunci non sono risolti.

* **Riproduzione di contenuti MP4**

Questa versione di TVSDK supporta la riproduzione di MP4 come contenuto principale.

* **Connessioni di rete persistenti**

TVSDK mantiene un set di connessioni di rete riutilizzabili, in modo da non sostenere il sovraccarico di creare ed eliminare una connessione di rete per ogni richiesta di rete.

* **Protezione dell&#39;output basata sulla risoluzione**

Questa funzione associa le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più dettagliati.

* **Trick play con velocità bit adattiva (ABR)**

Questa funzione consente a TVSDK di passare da un flusso iFrame a un altro in modalità &quot;trick play&quot;. È possibile utilizzare profili non iFrame per eseguire la riproduzione a velocità inferiori.

* **Riproduzione più fluida dei trucchi**

Questi miglioramenti migliorano l’esperienza utente:

· Selezione adattiva del bit rate e del frame rate durante la riproduzione dei &quot;trick&quot;, in base alla larghezza di banda e al profilo del buffer

· Utilizzare lo streaming principale invece dello streaming IDR per ottenere una riproduzione rapida fino a 30 fps.

* **Logica ABR migliorata**

La nuova logica ABR si basa sulla lunghezza del buffer, sul tasso di variazione della lunghezza del buffer e sulla larghezza di banda misurata. Questo assicura che l&#39;ABR scelga il bit rate corretto quando la larghezza di banda fluttua e ottimizza anche il numero di volte che l&#39;interruttore di bitrate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.

* **Fatturazione**

TVSDK raccoglie automaticamente le metriche, rispettando il contratto di vendita del cliente per generare rapporti periodici sull&#39;utilizzo richiesti a scopo di fatturazione. In ogni evento di avvio del flusso, TVSDK utilizza l’API di inserimento dati di Adobe Analytics per inviare alla suite di rapporti di proprietà di Adobe Analytics Primetime metriche di fatturazione quali il tipo di contenuto, i flag con inserimento di annunci e i flag con drm abilitato, in base alla durata del flusso fatturabile. Questo non interferisce con le suite di rapporti Adobe Analytics del cliente o non viene incluso nelle sue chiamate al server. Su richiesta, questo rapporto sull’utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell’utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione.

## Funzioni supportate {#supported-features}

TVSDK per Android 2.4 supporta una serie di funzioni che è possibile implementare per aggiungere funzionalità alle applicazioni video.

>[!NOTE]
>
>Nelle tabelle delle matrici di funzioni riportate di seguito, un √ indica che la funzione è supportata nella versione corrente.

### Funzioni di riproduzione core {#core-playback-features}

| **Funzionalità** | **Tipo di contenuto** | **HLS** | **TRATTINO** |
|---|---|---|---|
| Riproduzione generale (riproduzione, pausa, ricerca) | VOD + Live | √ | √ (solo VOD) |
| FER - Riproduzione generale (riproduzione, pausa, ricerca) | VOD FER | √ | Non supportato |
| MP3 | VOD | Non supportato | Non supportato |
| Riproduzione di contenuti MP4 | VOD | √ | √ |
| Logica di commutazione del bit rate adattivo | VOD + Live | √ | Non supportato |
| Riproduzione solo audio | VOD + Live | √ | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | √ | √ (solo VOD) |
| Sottotitoli codificati - WebVTT | VOD + Live | √ | √ (solo VOD) |
| Failover del manifesto | VOD + Live | √ | √ (solo VOD) |
| Failover avanzato | VOD + Live | √ | √ (solo VOD) |
| Notifiche QoS e lettore | VOD + Live | √ | √ (solo VOD) |
| Supporto per le intestazioni dei cookie | VOD + Live | √ | √ (solo VOD) |
| Supporto per intestazioni personalizzate | VOD + Live | Non supportato | Non supportato |
| Impostare i parametri di controllo del buffer | VOD + Live | √ | √ (solo VOD) |
| Impostazione dei controlli del bit rate adattivo | VOD + Live | √ | √ (solo VOD) |
| Tag manifesto personalizzati (HLS) / Flussi evento (DASH) | VOD + Live | √ | √ (solo VOD) |
| Late Bound Audio | VOD + Live | √ | √ (solo VOD) |
| Reindirizzamento 302 | VOD + Live | √ | √ (solo VOD) |

### Funzioni di riproduzione avanzate {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>TRATTINO</strong></td> 
  </tr>
  <tr>
   <td>Riproduzione con offset</td> 
   <td>Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Riproduzione solo audio</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Smooth Trick Play (con ABR)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Analisi ID3 (HLS) / Metadati temporizzati (DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Sospensioni attività </td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Istantanea attiva</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto marker di discontinuità (HLS) </li> 
     <li>Più periodi (TRATTINO)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Adesività reindirizzamento 302</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (solo VOD)</td> 
  </tr>
  <tr>
   <td>Scrubbing delle miniature (Iframe e JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Integrità del flusso </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

### Funzioni principali di Ad Insertion (CSAI) {#core-ad-insertion-features-csai}

| **Funzionalità** | **Tipo di contenuto** | **HLS** | **TRATTINO** |
|---|---|---|---|
| Riproduzione generale, annunci abilitati | VOD + Live | √ | √ (solo pre-roll VOD) |
| Contenuto FER con annunci abilitati | VOD | √ | Non supportato |
| Comportamenti predefiniti degli annunci | VOD + Live | √ | √ (solo pre-roll VOD) |
| VAST 2.0/3.0 | VOD + Live | √ | √ (solo pre-roll VOD) |
| VMAP 1.0 | VOD + Live | √ | √ (solo pre-roll VOD) |
| Annunci MP4 | VOD + Live | √ (da CRS) | √ (da CRS, solo pre-roll) |

### Funzioni Ad Insertion avanzate (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>TRATTINO</strong></td> 
  </tr>
  <tr>
   <td>Riproduzione nei trucchi con annunci abilitata</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Solo annuncio </td> 
   <td>VOD</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Parametri di targeting</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (solo pre-roll VOD)</td> 
  </tr>
  <tr>
   <td>Parametri personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (solo pre-roll VOD)</td> 
  </tr>
  <tr>
   <td>Comportamenti annuncio personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (solo pre-roll VOD)</td> 
  </tr>
  <tr>
   <td>Tag annuncio personalizzati</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Ad Resolver personalizzati</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Ad Resolver personalizzato ruota libera</td> 
   <td>VOD</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Sostituzione annuncio C3 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Caricamento annuncio lazy</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto per marker di discontinuità - SSAI (HLS) </li> 
     <li>Più periodi (TRATTINO)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Annunci aziendali, annunci banner e annunci cliccabili</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√ (solo pre-roll VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√ (JS) </td> 
   <td>√ (solo pre-roll VOD)</td> 
  </tr>
  <tr>
   <td>Uscita anticipata dall’annuncio</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>VOD creativo basato su regole + Priorità live</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Regole CRS </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

## Funzioni di protezione dei contenuti {#content-protection-features}

| **Funzionalità** | **Tipo di contenuto** | **HLS** | **TRATTINO** |
|---|---|---|---|
| Crittografia AES | VOD + Live | √ | √ (solo VOD) |
| Esempio di crittografia AES | VOD + Live | √ |  |
| Flussi con token | VOD + Live | √ |  |
| DRM | VOD + Live | Solo DRM di Primetime (in futuro: Widevine) | Solo widevine |
| Riproduzione esterna (RBOP) | VOD + Live | Solo DRM di Primetime | Non supportato |
| Rotazione licenza | VOD + Live | Solo DRM di Primetime | Non supportato |
| Rotazione tasti | VOD + Live | Solo DRM di Primetime | Non supportato |

### Funzioni di integrazione {#integration-features}

| **Funzionalità** | **Tipo di contenuto** | **HLS** | **TRATTINO** |
|---|---|---|---|
| Integrazione Adobe Analytics VHL | VOD + Live | √ | √ |
| Fatturazione | VOD + Live | √ | Non supportato |

## Funzioni non supportate {#features-not-supported}

Questa versione di TVSDK non supporta:

* Sospensione attività degli annunci.
* Rallentatore nella riproduzione con trucco.
* Ricerca e riproduzione con contenuti MP4.
* Inserimento di annunci con contenuto principale MP4.
* Ricerca durante la riproduzione di un annuncio.
* Riproduzione di annunci con contenuti multimediali solo audio.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Questa versione di TVSDK presenta i seguenti problemi:

* crash VOD DRM LBA specifico per dispositivo (Samsung Galaxy Tab 4) con audio e clic sugli annunci
* L’annuncio post-roll non viene riprodotto per un contenuto specifico.
* L&#39;impostazione della didascalia di chiusura sulle lingue CJK non funziona.
* Il video può uscire automaticamente dalla modalità trick sia tra VOD che live.
* VHL - le chiamate heartbeat errate vengono inviate quando si avvia un contenuto da un offset.
* Quando gli annunci VPAID vengono riprodotti, le chiamate VHL heartbeat per l’evento:type:annuncio di riproduzione mancante.
* L’annuncio pre-roll viene riprodotto anche quando si seleziona adBreakPolicy SKIP.
* Dopo essere passato a Stato completo, il lettore torna allo Stato di riproduzione con SKIP adBreakPolicy per gli annunci post-roll.

Senza video, non esiste alcuna dimensione del riquadro di visualizzazione e senza una dimensione del riquadro di visualizzazione non è possibile visualizzare elementi grafici per i sottotitoli.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
