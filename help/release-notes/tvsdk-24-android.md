---
title: Note sulla versione di TVSDK 2.4.1 per Android
description: Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 0%

---


# TVSDK 2.4.1 per le note sulla versione Android {#tvsdk-for-android-release-notes}

Le note sulla versione di TVSDK 2.4.1 per Android descrivono le funzioni nuove e supportate e i problemi e le limitazioni noti in TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe sta rilasciando TVSDK 2.4.1 per Android.

Per utilizzare questa versione di TVSDK, assicurati che il sistema soddisfi i requisiti descritti in [Requisiti di sistema](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Qui puoi trovare la documentazione:

・ Guida in linea TVSDK 2.4 per Android

・ [Javadocs TVSDK 2.4 per API Java Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Gli Javadocs sono l’autorità suprema, in quanto vengono generati automaticamente direttamente dal codice sorgente TVSDK.

・ [C++ documentazione API TVSDK 2.4 per Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Ogni classe Java ha una classe C++ corrispondente e la documentazione C++ contiene più materiale esplicativo rispetto a Javadocs, quindi consulta la documentazione C++ per una comprensione più approfondita dell’API Java.

・ Guida alla migrazione ([Guida alla migrazione a TVSDK 2.4 per Android](../migration-guides/tvsdk-14-25-android.md))

Questa guida spiega cosa devi modificare per migrare un’applicazione basata su TVSDK 1.4 a un’applicazione basata su TVSDK 2.4.

## Nuove funzioni {#new-features}

TVSDK 2.4.1 per Android offre numerosi miglioramenti delle prestazioni rispetto alle versioni precedenti. Offre un&#39;esperienza visiva di alta qualità.

Questa versione include tutte le funzioni delle versioni 2.4 e 2.4.1 e nessuna funzione è obsoleta.

Di seguito sono elencate le nuove funzioni chiave della versione 2.4.1:

* Funzioni di HLS versione 4

   * **Riproduzione video**  (riproduzione, pausa, ricerca) con controllo del lettore per flussi in tempo reale, lineare e VOD.
   * **sottotitoli codificati.** TVSDK può visualizzare sottotitoli codificati 608/708 con una selezione di font, dimensioni dei font, colori e sfondo. Può inoltre supportare i video con didascalie di roll-up e passare tra le tracce di lingua, se disponibili.
   * **Il** modesto gioco di mattoni supporta il rapido avanzamento e il riavvolgimento per i flussi HLS che utilizzano i-frame. Tutti i controlli di riproduzione video funzionano sul contenuto. È disponibile la modalità di riproduzione video esterna con velocità comprese tra 0 e 1.
   * **Il bitrate adattivo (ABR)**  consente al lettore di selezionare dinamicamente quale delle versioni multiple dello stesso flusso di contenuto riprodurre, in base alla rete e ad altre condizioni. Puoi impostare i parametri in modo dinamico o nel file manifesto da selezionare tra criteri di selezione aggressivi, moderati e conservativi.
   * **Gli** intervalli di byte consentono a un singolo file TS di contenere più segmenti TS.
   * **Il rendering audio alternativo** consente al lettore di passare da una traccia audio all’altra.
   * **Supporto per ID3.** TVSDK può riprodurre flussi audio e video HLS che contengono metadati audio ID3, come nome dell&#39;artista, titolo e album.
   * **Failover. **TVSDK utilizza strategie per continuare la riproduzione ininterrotta, nonostante gli errori dei server host, dei file playlist e dei segmenti.
   * **Passaggio audio multicanale (DD+).** TVSDK può trasmettere i dati audio Dolby Digital Plus (E-AC3) all&#39;hardware di supporto.

* Funzioni di protezione dei contenuti

   * **DRM per HLS.** Tutte le API di riproduzione video funzionano con contenuti video crittografati protetti da Adobe Access. Sono supportate le seguenti funzioni DRM:

      * Rotazione licenza
      * Rotazione chiave
      * Memorizzazione in cache delle licenze
      * Ora dei criteri
      * IV rotazione

* **Riproduzione AES 128.** TVSDK può riprodurre contenuti HLS avanzati (AES) con dimensioni chiave di 128 bit.
* **L&#39;HLS protetto (PHLS)** fornisce un set limitato di criteri DRM predefiniti, un sottoinsieme di ciò che l&#39;accesso Adobe fornisce, per consentire un DRM leggero su HLS per flussi live e VOD.

* Funzionalità di pubblicità/contenuto alternativo e monetizzazione

   * **Tracciamento degli annunci inseriti sul lato server.** TVSDK può tenere traccia degli annunci inseriti dal servizio di inserimento annunci di Adobe Cloud. Supporta gli annunci lineari nei formati VAST2, VAST3 e VMAP per i flussi VOD e live/lineari.
   * **Tag HLS personalizzati.** TVSDK utilizza la sua  `MediaPlayerConfig` classe per abilitare la notifica all’applicazione del lettore quando nel flusso vengono visualizzati tag HLS personalizzati.
   * **Inserimento di annunci lato client.** La libreria di inserimento annunci audio funziona con i server Adobe Auditude per risolvere gli annunci da inserire in modo dinamico nei contenuti live, lineari e VOD, nelle posizioni pre-roll, mid-roll o post-roll.
   * **Risolutori di annunci personalizzati.** Le interfacce  `ContentResolver, OpportunityGenerator,` e  `MediaPlayerClientFactory` ti consentono di implementare un risolutore di contenuti alternativo/ad personalizzato e di registrare un rilevatore di opportunità personalizzato per lavorare con TVSDK. Le classi `TestAdResolver` e `AuditudeResolver` forniscono esempi C++ sull’implementazione di un risolutore di contenuti. Puoi trovare un esempio Javascript in `samples/jspsdk/testapp/psdk.js`.
   * **Comportamento pubblicitario coerente.** Utilizza l’ `AdPolicySelector` interfaccia per abilitare un comportamento coerente tra tutti i lettori per operazioni come cercare e ingannare quando gli annunci sono presenti nel contenuto. Se non implementi il tuo , TVSDK utilizza `DefaultAdPolicySelector`.
   * **Rimuovi/sostituisci gli annunci C3.** Utilizza l’API TVSDK appropriata per rimuovere intervalli di contenuto personalizzati e inserire in modo dinamico nuovi annunci senza ulteriore preparazione. Questa funzione è utile quando vengono trasmessi contenuti live/lineari, per poi renderli immediatamente disponibili su richiesta senza pulizia.

Di seguito sono elencate le nuove funzionalità principali della versione 2.4:

* **Attiva istantaneamente per VOD e** liveQuando si attiva l&#39;istante, il TVSDK inizializza e carica i contenuti multimediali prima dell&#39;avvio della riproduzione. Poiché puoi avviare più istanze `MediaPlayerItemLoader` contemporaneamente in background, puoi creare un buffer per più flussi. Quando un utente cambia il canale e il flusso è bufferizzato correttamente, la riproduzione sul nuovo canale viene avviata immediatamente. TVSDK 2.4 supporta anche l’opzione Instant On per i flussi live. I flussi live vengono ri-bufferizzati quando la finestra live si sposta.

* **Miglioramenti delle prestazioni **La nuova architettura TVSDK 2.4 offre diversi miglioramenti delle prestazioni:

   * **Sottosegmentazione** : TVSDK riduce ulteriormente le dimensioni di ciascun frammento per avviare la riproduzione il prima possibile.
   * **Download paralleli di annunci**  - TVSDK precarica gli annunci in parallelo alla riproduzione dei contenuti prima di colpire l’annuncio e interrompe così la riproduzione continua di annunci e contenuti.
   * **Lazy ad Resolution** - Con questa funzione, non aspettiamo la risoluzione degli annunci non preroll prima di avviare la riproduzione, riducendo così il tempo di avvio. Le API come ricerca e trucco non sono ancora consentite finché tutti gli annunci non vengono risolti.

* **Riproduzione di contenuti MP4**

Questa versione di TVSDK supporta la riproduzione di MP4 come contenuto principale.

* **Connessioni di rete persistenti**

TVSDK mantiene un set di connessioni di rete riutilizzabili, in modo che non si verifichi il sovraccarico della creazione e distruzione di una connessione di rete per ogni richiesta di rete.

* **Protezione dell&#39;uscita basata su risoluzione**

Questa funzione collega le restrizioni di riproduzione a risoluzioni specifiche, fornendo controlli DRM più precisi.

* **Gioco a mattoni con bit rate adattivo (ABR)**

Questa funzione consente a TVSDK di passare da un flusso di iFrame all&#39;altro in modalità di riproduzione a trucco. È possibile utilizzare profili non iFrame per eseguire la riproduzione a velocità più basse.

* **Giocare con un trucco liscio**

Questi miglioramenti migliorano l’esperienza utente:

・ Selezione del bit rate adattivo e del frame rate durante la riproduzione con trucco, in base alla larghezza di banda e al profilo del buffer

・ Utilizzare il flusso principale invece del flusso IDR per ottenere una riproduzione rapida fino a 30 fps.

* **Logica ABR migliorata**

La nuova logica ABR si basa sulla lunghezza del buffer, sulla velocità di variazione della lunghezza del buffer e sulla larghezza di banda misurata. In questo modo l&#39;ABR sceglie il bit rate corretto quando la larghezza di banda oscilla e ottimizza anche il numero di volte in cui l&#39;interruttore del bit rate si verifica effettivamente monitorando la velocità con cui cambia la lunghezza del buffer.

* **Fatturazione**

TVSDK raccoglie automaticamente le metriche, in base al contratto di vendita del cliente, per generare rapporti di utilizzo periodici richiesti a scopo di fatturazione. In ogni evento di avvio del flusso, TVSDK utilizza l’API di inserimento dati di Adobe Analytics per inviare metriche di fatturazione come il tipo di contenuto, i flag abilitati per l’inserimento di annunci e i flag abilitati per i drm, in base alla durata del flusso fatturabile, alla suite di rapporti di proprietà di Adobe Analytics Primetime. Questo non interferisce con o viene incluso nelle suite di rapporti o nelle chiamate server del cliente Adobe Analytics. Su richiesta, questo rapporto sull’utilizzo della fatturazione viene inviato periodicamente ai clienti. Questa è la prima fase della funzione di fatturazione che supporta solo la fatturazione dell’utilizzo. Può essere configurato in base al contratto di vendita utilizzando le API descritte nella documentazione.

## Funzioni supportate {#supported-features}

TVSDK per Android 2.4 supporta una serie di funzioni che è possibile implementare per aggiungere funzionalità alle applicazioni video.

>[!NOTE]
>
>Nelle tabelle a matrice di caratteristiche riportate di seguito, a Ö significa che la funzione è supportata nella versione corrente.

### Funzioni di riproduzione core {#core-playback-features}

| **Funzione** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Riproduzione generale (riproduzione, pausa, ricerca) | VOD + Live | Ö | Ö (solo VOD) |
| FER - Riproduzione generale (Play, Pause, Seek) | FER VOD | Ö | Non supportato |
| MP3 | VOD | Non supportato | Non supportato |
| Riproduzione di contenuti MP4 | VOD | Ö | Ö |
| Logica di commutazione del bit rate adattivo | VOD + Live | Ö | Non supportato |
| Riproduzione solo audio | VOD + Live | Ö | Non supportato |
| Sottotitoli codificati - 608/708 | VOD + Live | Ö | Ö (solo VOD) |
| Sottotitoli codificati - WebVTT | VOD + Live | Ö | Ö (solo VOD) |
| Failover manifesto | VOD + Live | Ö | Ö (solo VOD) |
| Failover avanzato | VOD + Live | Ö | Ö (solo VOD) |
| Notifiche di QoS e del lettore | VOD + Live | Ö | Ö (solo VOD) |
| Supporto per le intestazioni dei cookie | VOD + Live | Ö | Ö (solo VOD) |
| Supporto per intestazioni personalizzate | VOD + Live | Non supportato | Non supportato |
| Imposta parametri di controllo buffer | VOD + Live | Ö | Ö (solo VOD) |
| Imposta controlli del bit rate adattivo | VOD + Live | Ö | Ö (solo VOD) |
| Tag Manifest personalizzati (HLS) / Flussi eventi (DASH) | VOD + Live | Ö | Ö (solo VOD) |
| Audio associato in ritardo | VOD + Live | Ö | Ö (solo VOD) |
| 302 Reindirizzamento | VOD + Live | Ö | Ö (solo VOD) |

### Funzioni di riproduzione avanzate {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Funzione</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Riproduzione con offset</td> 
   <td>Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Riproduzione solo audio</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Gioco A Trick </td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Giocare liscio (con ABR)</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Analisi ID3 (HLS) / Metadati temporizzati (DASH)</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Blackout </td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Instant On</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto dei marker di discontinuità (HLS) </li> 
     <li>Multi-periodo (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>302 Atteggiamento del reindirizzamento</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Ö (solo VOD)</td> 
  </tr>
  <tr>
   <td>Scorrimento delle miniature (Iframe e JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Integrità dei flussi </td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

### Funzioni principali di Ad Insertion (CSAI) {#core-ad-insertion-features-csai}

| **Funzione** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Riproduzione generale, annunci attivati | VOD + Live | Ö | Ö (solo per i prerotoli VOD) |
| Contenuto FER con annunci abilitati | VOD | Ö | Non supportato |
| Comportamenti degli annunci predefiniti | VOD + Live | Ö | Ö (solo per i prerotoli VOD) |
| VAST 2.0/3.0 | VOD + Live | Ö | Ö (solo per i prerotoli VOD) |
| VMAP 1.0 | VOD + Live | Ö | Ö (solo per i prerotoli VOD) |
| Annunci MP4 | VOD + Live | Ö (da CRS) | Ö (da CRS, solo prerotoli) |

### Funzioni avanzate di Ad Insertion (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Funzione</strong></td> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Gioca a mattoni con annunci abilitati</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
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
   <td>Ö</td> 
   <td>Ö (solo per i prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Parametri personalizzati</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Ö (solo per i prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Comportamenti di annunci personalizzati</td> 
   <td>VOD + Live</td> 
   <td>Ö</td> 
   <td>Ö (solo per i prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Tag personalizzati degli annunci</td> 
   <td>Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Ad Resolver personalizzati</td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Ad Resolver personalizzato</td> 
   <td>VOD</td> 
   <td>Non supportato</td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Sostituzione annunci C3 </td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Caricamento annuncio pizzico</td> 
   <td>VOD</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Supporto dei marker di discontinuità - SSAI (HLS) </li> 
     <li>Multi-periodo (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Annunci Companion, Annunci Banner e Annunci Clickable</td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td>Ö (solo per i prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>Ö (JS) </td> 
   <td>Ö (solo per i prerotoli VOD)</td> 
  </tr>
  <tr>
   <td>Uscita annunci in anticipo</td> 
   <td>Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Creative VOD basato su regole + priorità in tempo reale</td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
  <tr>
   <td>Regole CRS </td> 
   <td>VOD + Live</td> 
   <td>Ö </td> 
   <td>Non supportato</td> 
  </tr>
 </tbody>
</table>

## Funzioni di protezione dei contenuti {#content-protection-features}

| **Funzione** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Crittografia AES | VOD + Live | Ö | Ö (solo VOD) |
| Crittografia AES di esempio | VOD + Live | Ö |  |
| Flussi token | VOD + Live | Ö |  |
| DRM | VOD + Live | Solo DRM di Primetime (futuro) Widevine) | Solo Widevine |
| Riproduzione esterna (RBOP) | VOD + Live | Solo DRM di Primetime | Non supportato |
| Rotazione licenza | VOD + Live | Solo DRM di Primetime | Non supportato |
| Rotazione tasti | VOD + Live | Solo DRM di Primetime | Non supportato |

### Funzionalità di integrazione {#integration-features}

| **Funzione** | **Tipo di contenuto** | **HLS** | **DASH** |
|---|---|---|---|
| Integrazione Adobe Analytics VHL | VOD + Live | Ö | Ö |
| Fatturazione | VOD + Live | Ö | Non supportato |

## Funzioni non supportate {#features-not-supported}

Questa versione di TVSDK non supporta:

* Sospensione degli annunci pubblicitari.
* Lento movimento nel gioco dei trucchi.
* Cerca e trickplay con contenuti MP4.
* Inserimento di annunci con contenuto principale MP4.
* Cerca quando un annuncio sta giocando.
* Riproduzione di annunci con supporti solo audio.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Questa versione di TVSDK presenta i seguenti problemi:

* Crash VOD DRM LBA per dispositivi specifici (Samsung Galaxy Tab 4) con audacia e clicca sugli annunci
* L’annuncio post-roll non viene riprodotto per un contenuto specifico.
* L&#39;impostazione della didascalia vicina alle lingue CJK non funziona.
* Il video può uscire dalla modalità &quot;trucco&quot; automaticamente tra VOD e live.
* VHL: vengono inviate chiamate heartbeat errate quando si avvia un contenuto da un offset.
* Quando gli annunci VPAID vengono riprodotti, le chiamate heartbeat VHL per eventi:type:play e sono mancanti.
* L&#39;annuncio pre-roll viene riprodotto anche quando viene selezionato il SKIP di adBreakPolicy.
* Dopo aver effettuato l&#39;accesso allo stato Complete, il lettore torna allo stato Playing con SKIP adBreakPolicy per gli annunci post-roll.

Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione, non è possibile visualizzare alcun elemento grafico per i sottotitoli.

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina [Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .