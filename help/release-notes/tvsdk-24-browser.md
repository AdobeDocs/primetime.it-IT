---
title: Note sulla versione del browser TVSDK 2.4
seo-title: Note sulla versione del browser TVSDK 2.4
description: Le note sulla versione del browser TVSDK 2.4 descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.
seo-description: Le note sulla versione del browser TVSDK 2.4 descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.
uuid: 3a1eb1a5-0e72-4658-beeb-bca8816570e7
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: d71886cb-f34b-47b2-9df7-168686478106
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# Note sulla versione del browser TVSDK 2.4 {#browser-tvsdk-release-notes}

Le note sulla versione del browser TVSDK 2.4 descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.

## Introduzione {#introduction}

Browser TVSDK è un toolkit che consente di aggiungere funzionalità avanzate di riproduzione video, protezione dei contenuti e pubblicità alle applicazioni di lettori video basate su browser.

Il browser TVSDK 2.4 fornisce API JavaScript per creare applicazioni video basate su browser e include il supporto per la riproduzione nelle modalità seguenti:

* Solo HTML5
* HTML5 con riserva flash automatica
* Flash always

Questa versione include le informazioni seguenti:

・ [Documentazione](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)dell&#39;API TVSDK del browser.

・ [Guida alla programmazione](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf)TVSDK per browser

・ [TVSDK per la guida alla migrazione da 1.4 DHLS a browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [Conversione dal browser TVSDK 2.4.6 alla versione 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Un&#39;implementazione di riferimento, inclusa nella build.

>[!NOTE]
>
>*Per un elenco completo delle considerazioni sulla sicurezza per questa versione, consultate Considerazioni sulla sicurezza.

## Novità e funzionalità supportate {#what-s-new-and-supported-features}

Questa release di Browser TVSDK fornisce nuove funzioni che potete utilizzare per migliorare le applicazioni video.

**Novità nell’aggiornamento 2.4.12 (build 204)**

La seguente aggiunta è disponibile come parte dell’aggiornamento del browser TVSDK 2.4.12 (build 204):

* L&#39;implementazione dell&#39;API del volume di AdobePSDK.MediaPlayer viene modificata per consentire la riproduzione automatica su iOS quando la riproduzione è disattivata.

・ Viene aggiunta una nuova API `auditudeSettings.ignoreVPAIDAds`per consentire di ignorare gli annunci VPAID ricevuti dal server Auditude. L&#39;API non funziona per Flash Fallback.

**Versione 2.4.11**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.11:

・ Il failover del segmento HLS Live è supportato per le modalità di fallback MSE e Flash.

・ Il supporto per `AuditudeSettings.creativeRepackagingDomain` l&#39;API è ora disponibile anche per MSE. In precedenza era supportato solo con la modalità di fallback Flash.

・ Il rilascio contiene correzioni per problemi critici dei clienti. Vedere *Problemi risolti* un elenco.

**Versione 2.4.10**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.10:

・ TVSDK fornisce enableLogging() per abilitare o disabilitare la registrazione. Fate riferimento alla documentazione [API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)per informazioni sull&#39;utilizzo.

・ TVSDK non supporta più i capitoli predefiniti quando si utilizza Adobe Analytics. Definite e gestite i capitoli utilizzando l’applicazione.

・ Il rilascio contiene correzioni per problemi critici dei clienti. Vedere *Problemi risolti *un elenco.

**Versione 2.4.9**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.9:

・ Flussi HLS VOD e Live con discontinuità temporale ma senza marcatori di discontinuità sono supportati.

・ I fotogrammi ID3 v2.4.0 sono supportati con il tag video Safari per i flussi HLS VOD e Live.

・ L&#39;implementazione del caricamento sicuro degli annunci garantisce che le chiamate del server degli annunci vengano aggiornate a HTTP protetto in base alla configurazione dell&#39;API. Per informazioni dettagliate, consultate le classi AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration. Questa funzione non è supportata nella modalità di fallback di Flash.

・ Le informazioni sugli Ad ID e sulle informazioni sulle estensioni associate alle risposte VAST 3.0 sono ora disponibili per l&#39;applicazione da parte di TVSDK e possono essere utilizzate per implementare l&#39;integrazione Moat per le misurazioni degli Annunci. Per informazioni dettagliate, consultate API AdobePSDK.NetworkAdInfo. Questo non è supportato in modalità di fallback Flash.

・ La classe AdobePSDK.ForceHttpsConfiguration non è più disponibile. Ha avuto successo da

Classe AdobePSDK.ForceHttpsAdConfiguration.

・ È ora disponibile una nuova API, AdobePSDK.optimizeFlashCalls, per ottimizzare le chiamate per migliorare l&#39;esperienza di riproduzione HLS in modalità di fallback Flash. Per impostazione predefinita, questa opzione è disabilitata.

**Novità nell’aggiornamento 2.4.8 (build 6002)**

Questo aggiornamento contiene correzioni di problemi critici per i clienti. Consultate *Problemi* risolti, per l’elenco.

**Versione 2.4.8**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.8:

・ L&#39;SDK è ora conforme con Chrome EME e le modifiche delle best practice disponibili a partire da Chrome v58. Per ulteriori dettagli, consultate [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ Il framework dell&#39;interfaccia utente ora supporta il flusso di lavoro DRM di accesso HLS su Flash, solo annunci e informazioni di targeting.

・ L&#39;API setDRMAuthenticateData viene aggiunta al framework dell&#39;interfaccia utente. Per riprodurre i flussi protetti con Adobe Access DRM, richiamate questa API. In alternativa, l’attributo drmAuthenticateData può essere specificato nel lettore. Per informazioni, consulta [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)per i dettagli.

**Versione 2.4.7**

Le seguenti funzionalità sono nuove nella versione 2.4.7:

・ Aggiunta del configuratore dell&#39;interfaccia utente nel framework dell&#39;interfaccia utente

È possibile configurare il lettore in uno dei seguenti modi:

・ Utilizzo di un oggetto JSON

・ Utilizzo delle API

Per facilitare la generazione dell&#39;oggetto JSON, Browser TVSDK fornisce uno strumento **UI Configurator **tool.

In questo strumento, è possibile selezionare diverse impostazioni, fare clic su **Test Configuration **per verificare le impostazioni, quindi fare clic su **Download Configuration **per scaricare le impostazioni. Dopo aver scaricato il file, potete trasmettere il contenuto di questo file come oggetto JSON all&#39;API ptp.videoPlayer.

・ Aggiunta dell&#39;API MediaPlayerItemConfig al framework dell&#39;interfaccia utente

Diverse funzioni, tra cui advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscriptionTags, thumbnailScrubber, InvoiceMetricsConfiguration, possono essere configurate tramite MediaPlayerItemConfig. Per ulteriori informazioni, consulta la documentazione di AdobePSDK.MediaPlayerItemConfig nel [browser API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)TVSDK* * [documentazione](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Nel framework dell&#39;interfaccia utente, è stato modificato il modo in cui vengono trasmesse le configurazioni di rete attraverso la configurazione del lettore.

**Versione 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**Versione 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* Supporto per flussi di lavoro DRM e Analytics nel framework dell&#39;interfaccia utente

Le configurazioni DRM e il tracciamento di Analytics possono essere attivati tramite il framework dell&#39;interfaccia utente.

* Aggiunta di `AdobePSDK.embedSWFinFullScreenDiv` API

Questa nuova API offre flessibilità all&#39;app lettore per selezionare il div in cui incorporare il file FlashFallback.swf.

* È stata sostituita `getVersion`l&#39;API dalla `AdobePSDK.MediaPlayer` classe con la `AdobePSDK.Version` classe per le informazioni relative alla versione TVSDK. Per informazioni dettagliate, consultate `AdobePSDK.Version` API [qui](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versione 2.4.6**

Le seguenti funzionalità sono nuove nella versione 2.4.6:

* **Supporto per la ricerca**

Browserify consente di utilizzare i moduli di stile node.js nel browser. È possibile definire le dipendenze e Browserify racchiude tutto in un unico file JavaScript.

* **Fatturazione**

Con l&#39;aiuto della fatturazione, Browser TVSDK può raccogliere le metriche di utilizzo del lettore per fatturare ai clienti Primetime.

>[!NOTE]
>
>L’enum MediaPlayer.Events obsoleto e le costanti obsolete in Enum PSDKErrorCode sono state rimosse nella versione 2.4.6. Per ulteriori informazioni, consultate [Conversione da browser TVSDK 2.4.5 a versione 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versione 2.4.5**

Nella versione 2.4.5 sono state introdotte le seguenti funzioni:

* **Riproduci e annunci eventi completi**

   I flussi FER (Full Event Replay) HLS ora supportano la risoluzione degli annunci e i comportamenti degli annunci. Per abilitare questo supporto, impostare la modalità di segnalazione degli annunci su `MANIFEST_CUES` quando si crea l&#39; `MediaPlayerItemConfig` oggetto.

* **Supporto per MediaplayerView ScalePolicy**

   Gli sviluppatori di applicazioni ora possono specificare un diverso scalePolicy per la visualizzazione utilizzando la proprietà scalePolicy di MediaplayerView.

* **Supporto dei contenuti anamorfici**

   La riproduzione di contenuti anamorfici ora è supportata quando si utilizza la riproduzione MSE e Flash.

* **Applicazione selettiva di`withCredentials`**

Se `withCredentials` è impostato su true, l’ `Access-Control-Allow-Origin` intestazione non può essere impostata su una carattere jolly. A seconda della risposta del server, Browser TVSDK imposta l&#39; `withCredentials` attributo in modo selettivo. Per ulteriori informazioni su questo supporto, consulta Documenti API [TVSDK per browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versione 2.4.4**

Nella versione 2.4.4 sono state introdotte le seguenti funzioni:

* **Applicazione di esempio Chromecast**

Questa versione fornisce il supporto per un&#39;app mittente e ricevitore che illustra la riproduzione di flussi DASH VOD e di flussi DASH Widevine con inserimento di annunci lato client.

* **Supporto di failover avanzato**

Questa release contiene il supporto per i casi di utilizzo avanzati del failover (failover di segmenti e server) per i flussi VOD HLS.

**Versione 2.4.3**

Nella versione 2.4.3 sono state introdotte le seguenti funzioni:

* **Tag personalizzati per DASH VOD**

   I tag personalizzati in linea (Eventi) possono essere sottoscritti e ricevuti come oggetto TimedMetadata.

* **Riproduzione di flussi senza estensioni**

   Sono ora supportati i flussi HLS e DASH senza estensioni. Per il file manifesto, è necessario specificare resourceType al caricamento della risorsa. Per i segmenti e i file VTT, l&#39;intestazione di risposta Content-Type viene utilizzata per determinare il tipo di contenuto.

**Versione 2.4.2**

Nella versione 2.4.2 sono state introdotte le seguenti funzioni:

* **Parità API**

Per un elenco completo della parità API, consultate la guida alla migrazione a [TVSDK 2.4 per DPS da 1.4 a browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Supporto di Sample-AES**

   Questa versione aggiunge il supporto per la riproduzione di contenuti cifrati Sample-AES su fallback MSE e Flash. Il requisito di ospitare il contenuto AES su un&#39;origine sicura su Google Chrome è stato rimosso.

* **Supporto per contenitori AAC**

   È ora supportata la riproduzione di file con estensione .aac. Può trattarsi di flussi solo audio o audio alternativo.

   >[!NOTE]
   >
   >I codec AC3 e AC3 avanzati non sono ancora supportati.

* **Riproduzione di flussi con token**

I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare i token di autenticazione sulle richieste di verifica del manifesto e del segmento e questi token possono essere forniti come parametri URL o come intestazioni di cookie. È ora supportata la riproduzione di tali flussi.

**Versione 2.4.1**

Nella versione 2.4.1 sono state introdotte le seguenti funzioni:

* **Framework dell&#39;interfaccia utente**

Questo framework, progettato per accelerare lo sviluppo dell&#39;interfaccia utente per le applicazioni di lettori video basate su JavaScript, è costituito da API per includere controlli di base come riproduzione/pausa e volume e per aggiungere o rimuovere facilmente elementi come gli stati della barra di scorrimento e le impostazioni dei sottotitoli codificati. È possibile specificare il comportamento associato ai controlli, creare controlli personalizzati e applicare l&#39;interfaccia utente del lettore. Tutto questo avviene attraverso il framework, senza necessità di manipolare direttamente la struttura DOM.

* **Miglioramenti della riproduzione HLS per i flussi live**

Questa versione supporta le interruzioni causate dall&#39;inserimento di annunci. Utilizza il tag EXT-PROGRAM-DATE-TIME seguito dal tag EXT-MEDIA-SEQUENCE per eseguire la sincronizzazione tra i profili bitrate adattivi per una riproduzione uniforme.

* **Supporto per VPAID 2.0**

La versione 2.0 del video player ad-serving interface definition (VPAID) offre agli utenti un&#39;esperienza multimediale avanzata e consente agli editori di eseguire il targeting migliore degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video. Questa release supporta annunci JavaScript VPAID lineari per contenuti video on-demand (VOD).

* **Tag HLS personalizzati**

I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifesto. Browser TVSDK consente di specificare e sottoscrivere altri tag e ricevere notifiche quando tali tag vengono visualizzati nel manifesto.

* **Indicatori di annunci visualizzati sulla timeline del lettore**

Questa versione supporta la visualizzazione di indicatori di annunci sulla timeline del lettore per i contenuti VoD e Live. Potete visualizzare questo comportamento nel lettore di riferimento.

**Supportato in 2.4**

Nella versione 2.4 erano disponibili le seguenti funzioni:

* **Riproduzione audio MP3**

   Questa release supporta la riproduzione audio MP3 sui browser con Media Source Extensions (MSE) e con il tag video Safari.

* **Riproduzione video MP4**

   Sono supportate le seguenti funzionalità:

   * Riproduzione a flusso singolo
   * Annunci MP4 pre-roll e post-roll con comportamenti annunci e monitoraggio
   * Annunci HLS pre-roll e post-roll con comportamenti annunci e monitoraggio
   * Annunci DASH pre-roll e post-roll con comportamenti annunci e monitoraggio

## Piattaforme supportate {#supported-platforms}

Browser TVSDK ha requisiti specifici per i livelli di piattaforme e software su cui deve essere eseguito. Sono supportate le piattaforme e i livelli software seguenti:

### Configurazioni desktop {#desktop-configurations}

* Microsoft Windows 7:

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 8.1

   * Internet Explorer 11+
   * Chrome 33+
   * Firefox 38+

* Microsoft Windows 10

   * Edge+

* Apple OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### Configurazioni Web per dispositivi mobili {#mobile-web-configurations}

* Android 4.4

   * Browser nativo
   * Chrome 33+

* Android 5.0

   * Browser nativo
   * Chrome 33+

* Android 6.0

   * ・ Chrome 33+

* Apple iOS 9

   * Safari 9+
   * Chrome 33+

* Apple iOS 10

   * Safari 9+
   * Chrome 33+

**Google Chromecast (seconda generazione; solo per riproduzione DASH)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Tecnologia</strong> </p> </td> 
   <td><p><strong>Tag</strong><sup>video TVSDK browser1</sup></p> </td> 
   <td><p><strong>Browser TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Tecnologia predefinita</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Tag video</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>Tag video</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS e DASH</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, DASH</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matrice di funzioni {#feature-matrix}

Elenco delle funzioni supportate e non supportate per questa versione:

* *Caratteristiche audio MP3 — Riproduzione di base*
* *Funzioni video MP4 Riproduzione di base*
* *Funzioni video MP4 Inserimento di annunci core*

>[!NOTE]
>
>*Nelle tabelle di matrici di feature riportate di seguito, una &#39;Y&#39; indica che la funzione è supportata nella versione corrente.*

### Caratteristiche audio MP3 {#mp-audio-features}

**Tabella 1: Riproduzione di base{#table-core-playback}**

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | MP3 VOD | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

1 Il tag Video TVSDK del browser non supporta lo streaming e DRM. Il supporto di codec e contenitori non è lo stesso in tutti i browser.

2 Per impostazione predefinita, Firefox utilizza Flash Player per la versione 41 o precedente.

### Funzioni audio MP4 {#mp-audio-features-1}

**Tabella 2: Riproduzione di base**

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | MP4 VOD | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

**Tabella 3: Inserimento di annunci core**

| Categoria | Tipo di contenuto | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Inserimento annunci | MP4 VOD | Pre-roll (MP4) | Non supportato | Y | Y |
| Inserimento annunci | MP4 VOD | Post-roll (MP4) | Non supportato | Y | Y |

Per ulteriori informazioni sul supporto delle funzioni HLS o DASH, vedi di seguito.

## Matrice delle funzioni HLS {#hls-feature-matrix}

Di seguito è riportata la matrice delle funzioni per le funzionalità HLS nel browser TVSDK.

* *Riproduzione HLS Core*
* *HLS Funzioni avanzate di riproduzione*
* *Funzioni di protezione dei contenuti HLS*
* *Funzioni di inserimento di annunci chiave HLS*
* *HLS Funzioni avanzate di inserimento annunci*
* *Integrazioni HLS*

>[!NOTE]
>
>*Nelle tabelle di matrici di feature riportate di seguito, una &#39;Y&#39; indica che la funzione è supportata nella versione corrente.*

### Funzioni HLS {#hls-features}

Sono supportate le seguenti funzionalità:

**Tabella 4: Riproduzione HLS Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Riproduzione generale (riproduzione, pausa, ricerca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Riproduzione generale (riproduzione, pausa e ricerca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Bitrate adattivo</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 didascalie</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Solo VOD</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover manifesto</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover avanzato</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Notifiche QoS e del lettore</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Supporto QoS limitato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Supporto per le intestazioni dei cookie</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Impostazione dei parametri di controllo del buffer</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Imposta adattivo</p> <p>controlli bitrate</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tag personalizzati</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>Connessione audio ritardata</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reindirizzamento 302</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 5: Funzioni di riproduzione avanzate HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Riproduzione a offset</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Riproduzione solo audio</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Gioco di mattoni</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Analisi ID3</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Supporto dei marcatori di discontinuità</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Flussi token</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fatturazione</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 6: Funzioni di protezione dei contenuti HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe Access</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 7: Funzioni di inserimento di annunci chiave HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Risoluzione degli annunci e comportamenti</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annunci predefinito</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reimballaggio creativo (da MP4 a HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 8: HLS Funzioni avanzate di inserimento annunci**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo annunci</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parametri di targeting</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parametri personalizzati</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annunci personalizzato</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy e caricamento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci pubblicitari, annunci per banner, annunci cliccabili</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 9: Integrazioni HLS{#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrazioni</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrazione VHL di Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matrice delle funzioni DASH {#dash-feature-matrix}

Di seguito è riportata la matrice delle funzioni DASH nel browser TVSDK.

・ Funzioni di riproduzione *DASH Core*

・ Funzioni di riproduzione avanzate *DASH*

・ Funzioni di protezione dei contenuti *DASH*

・ Funzioni *DASH Core di inserimento annunci*

・ *DASH - Funzioni avanzate di inserimento annunci*

・ Integrazioni *DASH*

>[!NOTE]
>
>Nelle tabelle di matrici di feature riportate di seguito, una Y indica che la funzione è supportata nella versione corrente.

### Funzioni DASH {#dash-features}

Sono supportate le seguenti funzionalità:

**Tabella 10: Funzioni di riproduzione DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Riproduzione generale (riproduzione, pausa, ricerca)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Riproduzione generale (riproduzione, pausa e ricerca)</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Bitrate adattivo</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 didascalie</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Notifiche QoS e del lettore</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Supporto per le intestazioni dei cookie</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Impostazione dei parametri di controllo del buffer</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Impostare controlli bitrate adattivi</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tag personalizzati (EventStream)</p> </td> 
   <td><p>Solo VOD (in linea)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Audio ritardato</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reindirizzamento 302</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 11: Funzioni avanzate di riproduzione DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Riproduzione a offset</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Riproduzione solo audio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Gioco di mattoni</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Analisi ID3</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Supporto multiperiodo</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Flussi token</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Fatturazione</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 12: Funzioni di protezione dei contenuti DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Protezione dei contenuti</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>・ Widevine su Chrome, Firefox 47 e versioni successive, e Chromecast</p> <p>・ PlayReady su Internet Explorer su Windows 8.1 ed Edge</p> <p>・ Primetime DRM per Windows Firefox (solo video)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 13: Funzioni di inserimento annunci DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Risoluzione degli annunci e comportamenti</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annunci predefinito</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reimballaggio creativo (da MP4 a DASH)</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 14: Funzioni avanzate di inserimento annunci DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo annunci</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parametri di targeting</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parametri personalizzati</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annunci personalizzato</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy e caricamento</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci per la compagnia, annunci per banner, annunci cliccabili</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Inserimento annunci</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 15: Integrazioni DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrazioni</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrazione VHL di Adobe Analytics</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemi risolti {#issues-fixed}

**Problemi risolti nell&#39;aggiornamento 2.4.12 (build 204)**

I seguenti problemi sono stati risolti nell’aggiornamento della versione 2.4.12 dell’SDK per browser (build 204):

・ **21647**- TVSDK dovrebbe consentire la riproduzione video automatica sui dispositivi iOS quando l&#39;audio è disattivato.

・ **21465**- Accesso chiave di errore negato durante la riproduzione di un flusso DASH protetto da DRM dopo la riproduzione di un flusso DASH Live.

・ **21442**- Abilitare la riproduzione automatica dei contenuti su iOS Web, dopo che l&#39;annuncio preroll è stato riprodotto con un gesto utente.

・ **21240**- API fornita per filtrare gli annunci VPAID analizzati da Auditude/VMAP.

**Problemi risolti nella versione 2.4.11**

I seguenti problemi sono stati risolti nella versione 2.4.11 dell’SDK per browser:

**Funzioni di riproduzione principali:**

・ **19192**: TVSDK ora implementa TextFormat:bottomInset e TextFormat:safeArea. Grazie a questi miglioramenti, i sottotitoli codificati possono essere riposizionati se la barra di controllo è visualizzata sullo schermo.

・ **21009**: I sottotitoli codificati vengono visualizzati sullo schermo in caso di interruzione della ricerca fino alla visualizzazione di nuove didascalie.

・ **21141**: La ricerca di nuovo viene rifiutata a causa di una condizione di gara durante l&#39;aggiunta del segmento.

・ **21142**: Disponibilità di intervalli di riproduzione ricercabili quando il lettore è in stato INITIALIZED. A causa di queste modifiche, ora è supportato l&#39;avvio della sessione in posizione.

・ **21363**: I sottotitoli codificati 608/708 non vengono sincronizzati dopo l’inserimento di annunci per i flussi DASH.

**Funzioni di inserimento annunci:**

・ **21179**: I problemi relativi al mid-roll (pause lunghe, fotogrammi neri) con contenuto VOD ora vengono risolti impostando correttamente la proprietà ad.PrimaryAsset.adParameters.

・ **21257**: Il file MP4 con bitrate più elevato viene selezionato per la transcodifica se MP4 non è un tipo mime valido e la funzione di ricompilazione creativa è attivata.

・ **21361**: TVSDK trasmette ora un ID creativo e di sistema di annunci dalla risposta VAST come parametri di query nella richiesta di creazione del pacchetto, al fine di supportare ulteriori regole di normalizzazione.

**Problemi risolti nella versione 2.4.10**

I seguenti problemi sono stati risolti nella versione 2.4.10 dell’SDK per browser:

**Funzioni di riproduzione principali:**

・ **21060**: Errore codec non valido generato con flussi HLS che contengono discontinuità e le caselle BMFF ISO vengono eseguite alla fine del flusso.

・ **21045**: La riproduzione automatica non funziona su iOS al termine della prima riproduzione video in una playlist.

・ **200975**: La frequenza fotogrammi viene restituita come NaN dal provider QoS nel browser Chrome.

・ **20823**: Errore codec non supportato generato quando si incontrano segmenti senza dati.

・ **20769**: L’SDK ora inizia con il bitrate corrente alla ricerca invece di passare immediatamente alla ricerca in base ai criteri ABR.

・ **20031**: In modalità verticale su IE11 (Windows 8.1), la schermata video diventa piccola. Funzione di protezione dei contenuti:

・ **19316**: Saltate i segmenti che non riescono a decrittare in caso di flussi HLS AES-128.

**Problemi risolti nella versione 2.4.9**

I seguenti problemi sono stati risolti in Browser TVSDK versione 2.4.9:

**Funzioni di riproduzione principali:**

・ **13407**: I flussi DASH potrebbero arrestarsi se Firefox interrompe l&#39;invio dell&#39;evento &quot;ontimeupdate&quot; durante la riproduzione.

・ **16380**: Durante la riproduzione di contenuti video audio muxed di segmenti con tempi di inizio non corrispondenti tramite MSE, l&#39;errore di sincronizzazione audio tra le rappresentazioni si accumula sugli switch ABR, dando luogo in ultima analisi a un errore (problema di cromo #663686).

・ **17985**: Durante la riproduzione di un particolare flusso ISO-BMFF sul browser Firefox, la riproduzione si blocca (problema Firefox #1342913). Ciò è stato corretto a partire da Firefox v53.

・ **19141**: ReferenceError non rilevato (nella promessa): width non è definito.

・ **18997, 19299**: Problema di sfarfallio video al limite del segmento. Ciò si verificava in quanto l&#39;SDK non calcolava correttamente l&#39;offset del tempo di composizione dell&#39;ultimo esempio.

・ **19780**: La riproduzione non viene avviata per il contenuto HLS e per HLS Ad su Firefox v53 (problema Firefox #354653).

・ **20046**: Data programma L’ora viene ricevuta come chiave invece del valore quando viene ricevuta come oggetto metadati temporizzati.

・ **20047**: useDefaultResizeHandler genera un errore con il fallback Flash.

・ **20179**: Flash Fallback non funziona con Flash Player v25.0.0.171.

・ **20293**: Firefox interrompe il buffering dei dati per alcuni flussi HLS che provocano l&#39;arresto.

・ **20626**: Il lettore genera un errore di decodifica su Chrome a causa di una gestione non corretta dei campioni video con durata zero.

・ **20078**: La riproduzione si arresta in corrispondenza dell&#39;errore del browser &#39;QuotaExceeded&#39;.

・ **18639**: Nel flusso HLS Live 608 il testo CC a volte viene visualizzato come errato.

・ **20028**: Il parametro della dimensione ClosedCaptions non modifica la dimensione del font.

・ **2013**: Le caselle dei sottotitoli codificati si sovrappongono l’una all’altra rendendole illeggibili.

**Funzioni CSAI (Core Ad Insertion):**

・ **20043**: Chiamate ad impression annuncio mancanti e di tracciamento annunci con più annunci e reindirizzamenti di terze parti.

・ **20044**: Quando si utilizza il ricompilamento creativo, tutti gli annunci nell&#39;interruzione dell&#39;annuncio devono essere ricompilati correttamente, altrimenti l&#39;interruzione dell&#39;annuncio viene completamente eliminata.

・ **20097**: La riproduzione dell&#39;annuncio viene saltata e il contenuto principale riprende immediatamente anziché aspettare il timeout di 20 secondi se il manifesto dell&#39;annuncio non è disponibile.

**Problemi risolti nell&#39;aggiornamento della versione 2.4.8 (build 6002)**

I seguenti problemi sono stati risolti nell’aggiornamento della versione 2.4.8 dell’SDK per browser (build 6002):

・ **14126:** La riproduzione potrebbe arrestarsi su Firefox (problema #1316024) a causa di uno spazio interno nel buffer di origine MSE. Cercare per riprendere la riproduzione

・ **19608:** Correzione per rispettare il valore dell&#39;offset temporale dalla risposta Auditude VMAP.

・ **19635:** Corregge lo stallo video in Internet Explorer 11 su Windows 10.

・ **19761:** Correzioni per problemi ABR con HLS.

・ **19780:** Corregge la riproduzione degli annunci con contenuti HLS interrotti in Mozilla Firefox v53.

・ **19877 e 19744:** I problemi risolvono l&#39;incoerenza nella selezione del bitrate dopo un&#39;operazione di ricerca. Ora, la selezione del bitrate alla ricerca corrisponde al valore più basso tra il bitrate corrente e il bitrate all’avvio.

・ **1981:** La riproduzione bloccata e la sovrapposizione di buffering viene visualizzata per un periodo infinito dopo che la ricerca viene eseguita per 3-4 volte.

・ **1984:** Conferma la conformità ai requisiti di Chrome 59 Beta Verified Media Path (VMP). bTVSDK è stato in grado di riprodurre contenuto Widevine DRM con Chrome 59 Beta.

・ **19916:** Riproduzione DRM su UI-Framework interrotta. Ora, acquisisceLicense anche se non è presente alcun criterio nei metadati.

**Problemi risolti nella versione 2.4.8**

I seguenti problemi sono stati risolti nella versione del browser TVSDK 2.4.8:

・ **10075**: Quando si cerca in anticipo sulla timeline, l’evento play complete non è stato ricevuto su Firefox e Chrome e l’evento di ricerca non è stato ricevuto su Firefox.

・ **15775**: Riproduci evento completo non ricevuto in Windows 8.1 Internet Explorer.

・ **17306**: Per i flussi SSAI, la riproduzione è supportata. Il tracciamento dell&#39;annuncio con punti non è supportato.

・ **19142**: A volte il riavvolgimento fa sì che il lettore video rimanga in stato di buffering per sempre.

・ **19218**: I marcatori di annunci non sono disponibili tramite il framework dell&#39;interfaccia utente.

・ **19219**: La sola riproduzione di annunci non funziona tramite il framework dell&#39;interfaccia utente.

・ **1922**: La chiave AES-128 è richiesta una volta per una playlist e dalla cache vengono servite le richieste successive. Precedentemente veniva richiesto per ogni segmento.

・ **19597**: &quot;TipoErrore non rilevato: Impossibile leggere la proprietà &#39;log&#39; di undefined&quot; è stata visualizzata con le build canarie Chrome.

・ **19605**: adRequestDomain non era disponibile in modalità Flash Fallback.

・ **19608**: Gli annunci VMAP non venivano inseriti per i flussi HLS Live. SDK ora considera i marcatori di cue e non si basa sui valori di scostamento del tempo nelle risposte VMAP.

・ **19637**: La riproduzione degli annunci genera solo errori di script alla fine dell&#39;annuncio.

・ **19732**: Richieste playlist CRS non riuscite con errore 404. Le richieste 1401 e 1403 di Browser TVSDK ora vengono aggiornate per tenere conto di ciò.

・ **19762**: acquisitionLicense utilizzata per essere chiamata prima di setAuthenticationToken a causa del quale è stata restituita una licenza valida indipendentemente dalla validità del token. Questo problema è risolto ora e acquisitionLicense viene chiamato solo dopo la risposta setAuthenticationToken.

**Problemi risolti nella versione 2.4.7**

Nella versione 2.4.7 sono stati risolti i seguenti problemi:

・ **8397**: I flussi HLS Live generati tramite Adobe Media Server potrebbero non essere riprodotti se i segmenti non iniziano con un fotogramma chiave.

・ **13606**: Sono stati risolti diversi problemi relativi alla ricerca per il flusso HLS nel browser Chrome.

・ **14807**: Nel browser Chrome, se la ricerca o la pausa viene attivata subito dopo play(), la riproduzione potrebbe arrestarsi con errore DOMException: La richiesta play() è stata interrotta da una chiamata...(Problema di cromo n. 593273).

・ **19085**: I parametri MediaPlayer quali volume, abrControlParameters e ccStyle non sono impostati su Valori predefiniti al momento del ripristino del lettore.

**Problemi risolti nella versione 2.4.6**

Il seguente problema è stato risolto nella versione 2.4.6:

・ **18093**: TimedI metadati per il tag accanto al tag sottoscritto vengono restituiti quando si utilizza Flash Player versione 24 in modalità di fallback Flash.

**Problemi risolti nella versione 2.4.4**

Nella versione 2.4.4 sono stati risolti i seguenti problemi:

・ **8711**: Con MSE, le didascalie 608/708 vengono lasciate giustificate per impostazione predefinita.

・ **13934**: Le impostazioni ABR per gli annunci non sono applicabili durante la riproduzione con flussi HLS Live.

・ **14079**: La longevità dei flussi HLS Live con una finestra DVR bassa potrebbe non riuscire, poiché la riproduzione potrebbe essere in ritardo a causa di problemi di latenza della rete. Fare clic sul punto attivo per riprendere la riproduzione.

・ **15037**: Gli esempi forniti con il framework dell&#39;interfaccia utente del lettore non funzionano su Microsoft Internet Explorer 10 in Windows 7.

・ **15913**: Per i flussi VOD HLS, in Chrome, il flusso non verrà riprodotto se la risposta del manifesto è 304 non viene modificata. Questo è stato corretto a partire da Chrome v55 (Chromio release 633696).

・ **16103**: Su Android Chrome, in condizioni di larghezza di banda ridotta, la riproduzione potrebbe arrestare con TipoErrore non rilevato: Impossibile leggere la proprietà &#39;programDateTime&#39; di un errore non definito.

・ **16265**: Per i flussi HLS VOD e Live, la ricerca tra le discontinuità non funziona.

・ **16709**: La ripresa del flusso HLS Live con PDT e l&#39;indicatore di discontinuità potrebbe causare il blocco del lettore nel buffering.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Le limitazioni e i problemi noti nel browser TVSDK sono indicati di seguito.

**Tabella 16: Funzioni di riproduzione principali**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td><p>・ I formati multimediali diversi da HLS non sono supportati.</p> <p>8799: La funzione di fallback di Flash non si occupa di contenuti misti, pertanto è necessario garantire che Content, Ad e altri URL non portino a contenuti misti (insieme a contenuti sicuri e non sicuri).</p> <p>・ 19271: La riproduzione della visualizzazione multipla tramite framework di interfaccia utente non è supportata in modalità di fallback Flash.</p> <p>・ Il fallback Flash non funziona su Microsoft Internet Explorer 8 e 9 in Windows 7, poiché queste versioni non sono supportate dall'SDK.</p> <p>・ 20262: Flash fallback aggiunge parametri personalizzati all'elenco delle informazioni di targeting. Anche l'ordine di priorità dei parametri personalizzati è diverso nel caso di Flash e MSE.</p> <p>・ 20653:Il fallback Flash TVSDK del browser non funziona su Win10 con Creators Update.</p> <p>・ Flash Fallback funziona con Flash Player versione 23 e successive.</p> <p>・ 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (impostazione predefinita), la riproduzione HLS non funziona in modalità Flash Fallback. Sta funzionando bene su Canary.</p> </td> 
   <td><p>・ 12563: I flussi di trattini con il codec audio mp4a.40.02 non vengono riprodotti su Firefox a causa di una stringa di codec audio non supportata in MPD. È supportato il codec audio mp4a.40.2.</p> <p>15029: Quando si passa da un video all’altro in visualizzazione multipla nel framework dell’interfaccia utente, il pulsante di riproduzione/pausa non viene aggiornato di conseguenza.</p> <p>・ 16034:In Windows 8.1 IE, la chiamata di reset() porta a un errore di tipo MIME sconosciuto. Ricaricare il supporto per riprendere la riproduzione.</p> <p>・ 18235: Alcuni problemi di ricerca sono osservati con i flussi di vod DASH con Ads.</p> <p>・ 18727: API di errore non supportata per MSE</p> <p>18750: Gli eventi di modifica dello stato potrebbero non essere ordinati in alcuni casi sia per l’SDK che per il framework dell’interfaccia utente e in UI Framework, gli eventi IDLE e Initializing StatusChange potrebbero non essere presenti per i listener di eventi aggiunti dopo che la risorsa è stata caricata.</p> <p>・ 18889: Se MediaPlayer è in stato di errore, l'oggetto view non viene restituito.</p> <p>・ 19039: Se AdobePSDK. MediaPlayer. searchToLocal() viene utilizzato con un valore maggiore di EOF, quindi la riproduzione inizia dall'inizio nel caso di MSE.</p> <p>・ 19049: Nessun stato di errore segnalato per Flash Player su Chrome, IE, Firefox quando il video viene bloccato durante la riproduzione.</p> <p>・ 17205: La riproduzione video si arresta durante la riproduzione di un flusso non muxed per alcune ore mentre l'audio continua a essere riprodotto (Chromio issue# 664033).</p> <p>・ 12308: I flussi DASH con composizione_ tempo_offset specificato possono avere timeStampOffset applicato a esso sul browser Chrome che porta a tempo di decodifica negativo e quindi MEDIA_ERR_ SRC_NOT_ SUPPORTED error (problema di cromo #398141).</p> <p>・ 14126: La riproduzione potrebbe arrestarsi su Firefox (problema n. 1316024) a causa di un gap interno nel buffer di origine MSE. Cercare per riprendere la riproduzione.</p> <p>・ 1915: MS Edge e IE 11 (Win 8.1 e 10) non imposta Origin su null nel reindirizzamento CORS, ma non riesce perché l'intestazione non è null e causa un errore di riproduzione.</p> <p>・ 19861:Problema con l'aggiunta del comportamento sul buffer di origine per i supporti già riprodotti. Chrome rifiuta il frammento aggiunto, incluso moov, causando un successivo errore di decodifica. (Problema di cromo n. 735335)</p> <p>19921: La riproduzione si blocca per alcuni contenuti HLS anche se il buffer è riuscito (problema di cromo #713540)</p> <p>・ 20444:La ricerca della fine dell'intervallo di buffer su IE e Edge potrebbe causare l'arresto della riproduzione.</p> <p>・ 20511: A volte il rifiuto può essere osservato per i flussi HLS con o senza annunci.</p> <p>・ 20743: In Windows 10 Chrome, lo streaming HLS Live viene riprodotto per alcuni secondi prima della riproduzione MP4 pre-roll.</p> <p>・ 21043: La dimensione video potrebbe non essere corretta al caricamento iniziale a causa della mancanza di metadati.</p> <p>・ 21115: Il gesto dell'utente Android è necessario per avviare la riproduzione se per i video in una playlist è disponibile un annuncio pre-roll.</p> <p>・ HLS Live non supporta il rollover del timestamp.</p> <p>・ L'audio AAC-SSR non è supportato.</p> <p>I codec audio AC3 e Enhanced AC3 non sono supportati.</p> <p>・ Per i flussi con discontinuità delle marche temporali, ma senza marcatori di discontinuità</p> <p>・ La riproduzione potrebbe presentare dei problemi e una ricerca non corretta a causa di salti.</p> <p>・ La durata del contenuto e la durata della riproduzione potrebbero non corrispondere.</p> <p>・ Le discontinuità tra rappresentazioni e rappresentazioni devono corrispondere ad altri saggi possono causare problemi di sincronizzazione e arresto.</p> <p>・ Sottotitoli e WebVTT potrebbero non essere visualizzati vicino alla fine del flusso.</p> <p>・ Le modifiche del codec audio non sono supportate tra i ponti timestamp.</p> <p>・ L'inserimento di annunci non è supportato.</p> <p>・ La modalità di avanzamento rapido può condurre al loop di riproduzione su Win 8.1 IE 11 (MS issue #12446268).</p> <p>DASH:</p> <p>・ Per i flussi live - è supportato il profilo live con tipo dinamico.</p> <p>・ Per i flussi VoD - è supportato il profilo live con tipo statico.</p> <p>Per i flussi VoD - il profilo ondemand non è certificato per i flussi di lavoro di annunci.</p> </td> 
   <td><p>・ I flussi DASH Live e DASH Video on Demand non sono supportati.</p> <p>・ La riproduzione video PIP (Picture in Picture) non è supportata su iOS in modalità a schermo intero.</p> <p>In Safari (tag video) l’estensione meno manifesto senza intestazione corretta del tipo di contenuto non funziona.</p> </td> 
   <td><p>・ l'ID applicazione nell'app mittente deve essere uguale a quello generato dalla registrazione dell'URL del ricevitore come app ricevitore personalizzata.</p> <p>・ Il lettore di riferimento è certificato per i flussi di lavoro DASH. Il framework dell'interfaccia utente non è certificato.</p> <p>Per un elenco dei codec supportati, fate riferimento <a href="https://developers.google.com/cast/docs/media"><em>qui</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td> </td> 
   <td>18098: Alcuni problemi di ricerca sono osservati con il flusso FER LBA HLS.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Bitrate adattivo</td> 
   <td><p>・ 20079: Il buffer riscrive alla ricerca all'interno dell'intervallo di buffer.</p> <p>20080: Il comportamento ABR Flash è in linea con MSE.</p> </td> 
   <td><p>・ La variante di fallback solo audio in un flusso ABR viene ignorata a causa di limitazioni correlate al buffer.</p> <p>・ 12289: I parametri di controllo ABR non si applicano all'audio in caso di flussi HLS/DASH non muxed.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Sottotitoli 608/708</td> 
   <td> </td> 
   <td><p>・ 7810: In Android 4.4.4 Chrome non sembra avere supporto per famiglie di font CSS di base utilizzate dal lettore e quindi la funzione di modifica dello stile del font non funziona.</p> <p>・ I canali CC non possono essere modificati nel caso di 608 didascalie.</p> <p>・ Le funzioni di stile avanzate non sono supportate per le didascalie 608.</p> <p>Le didascalie incorporate (608/708), segnalate tramite il tag Accessibilità sono supportate.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: I tag di regione nel file WebVTT vengono ignorati dal lettore durante la visualizzazione delle didascalie.</p> <p>・ DASH: I file VTT frammentati/segmentati non sono supportati.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover manifesto</td> 
   <td>21056: Con Flash Fallback, il failover non si verifica per il flusso live se il flusso primario restituisce un errore 404 durante la riproduzione.</td> 
   <td>Il failover manifesto è applicabile solo al contenuto e non agli annunci.</td> 
   <td>Il failover della playlist mancante funziona in Safari solo per il codice di errore HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover avanzato</td> 
   <td> </td> 
   <td><p>・ Il failover dei segmenti non supporta la salta dei segmenti non disponibili e la riproduzione continua.</p> <p>20533: I segmenti mancanti in una playlist devono essere trattati come discontinuità e la riproduzione deve riprendere dal segmento successivo disponibile.</p> <p>21267: Il passaggio del flusso a causa di un failover potrebbe causare il download di segmenti meno recenti.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Notifiche QoS e Player</td> 
   <td>21129: Il frame rate non è disponibile in caso di fallback Flash.</td> 
   <td><p>• 11170:</p> <p>Timed_Event non è disponibile per l'SDK per browser TVSDK con MSE, a differenza di quanto accade per l'SDK per browser con Flash Fallback.</p> <p>21129: Il frame rate non viene calcolato per i flussi live.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto per le intestazioni dei cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>i flag withCredentials e le intestazioni dei cookie non sono supportati in Safari.</p> <p>21051: Per consentire i cookie in Safari, abilita l’impostazione "Cookie e dati del sito Web" da Preferenze &gt; Privacy.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Tag personalizzati</td> 
   <td>14763: I tag personalizzati diversi da quelli che iniziano con # non devono essere supportati. In questo momento l'oggetto TimedMetadata viene creato e segnalato per tali tag durante il fallback di Flash.</td> 
   <td>I flussi con tag personalizzati in banda non sono certificati.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Rilegatura ritardata audio</td> 
   <td> </td> 
   <td><p>・ L'inserimento di annunci non è supportato con i flussi HLS Live LBA.</p> <p>・ 17273: Il passaggio dei flussi HLS VOD LBA alla rappresentazione predefinita in caso di failover non può essere ripristinato all'ultima selezione.</p> <p>・ 20251: Il flusso LBA HLS Live potrebbe arrestare la ricerca.</p> <p>・ 20497: Il lettore rimane in stato di buffering se i flussi non muxed LBA HLS presentano fotogrammi audio o video mancanti vicino alla fine del flusso.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302 Redirect</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>l'ottimizzazione di reindirizzamento non è supportata nei browser Windows Edge e IE, in quanto non supportano la proprietà responseURL nell'oggetto XMLHttpRequest.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 17: Funzioni di riproduzione avanzate**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo di contenuto</td> 
   <td>Feature</td> 
   <td>Flash</td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Riproduzione a offset</td> 
   <td><p>L'avvio della riproduzione con un particolare valore di offset non è supportato per il contenuto MP4.</p> </td> 
   <td>20492: Gli annunci intermedi che precedono l'offset vengono riprodotti prima che il contenuto riprenda dal valore di offset.</td> 
   <td>La riproduzione con funzione di offset non è supportata su iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Gioco di mattoni</td> 
   <td>La funzione Trickplay uniforme non funziona per i flussi privi di rappresentazioni per iFrame.</td> 
   <td><p>・ Gli adattamenti di Trick Play non sono supportati su Firefox e Internet Explorer e quindi la modalità di gestione inversa non è disponibile su questi browser.</p> <p>・ Trickplay non è disponibile durante la riproduzione di contenuti con annunci.</p> <p>・ 10435: Durante la riproduzione DASH, il video si blocca durante la riproduzione con trucco in avanti su Internet Explorer (Win 8.1)</p> <p>intermittentemente. Questo accade perché stiamo utilizzando la proprietà PlayRate degli elementi video senza l'adattamento trucco del gioco.</p> <p>14182: A volte, durante il riavvolgimento sul browser Chrome, l'evento di ricerca potrebbe non essere ricevuto e quindi la modalità trucco non funzionerà.</p> <p>・ 14942: I tassi di riproduzione possono essere impostati su Chrome per Android anche in caso di flussi di riproduzione non trucco, ma l'impostazione non verrà applicata e la riproduzione continuerà a velocità normale.</p> <p>・ 17308: La ricerca non funziona in modalità Trickplay.</p> <p>・ 17309: Nel browser Chrome, la modalità di trucco inverso non può essere mantenuta per più di 2 secondi.</p> <p>19272: La riproduzione dei mattoni potrebbe non recuperare dal buffering in Windows 10 Edge browser in caso di flussi DASH.</p> </td> 
   <td>La modalità di riavvolgimento non è supportata.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Analisi ID3</td> 
   <td>20346: Anche il byte di codifica del testo dei fotogrammi ID3 deve essere restituito dall’SDK.</td> 
   <td><p>I tag ID3 disponibili nei flussi di trasporto dati audio (ADTS) vengono ignorati dall’SDK.</p> <p>・ 12378: I metadati temporizzati ID3 vengono analizzati in momenti diversi in Flash e nel browser con supporto MSE, pertanto anche il comportamento di visualizzazione nella timeline del lettore di riferimento è diverso.</p> <p>・ 19247: L'analisi ID3 non è supportata nel framework dell'interfaccia utente.</p> </td> 
   <td><p>・ 20323: Il tag PRIV ID3 usato per segnalare la marca temporale del primo campione di un segmento non viene analizzato da Safari (problema Safari #32422733)</p> <p>・ 20350: Su alcuni dispositivi (inclusi MAC OS X 10.1, iPad10) Safari non fornisce eventi di cambio cue quando è in modalità trucco e quindi i fotogrammi ID3 non vengono ricevuti. (Safari issue #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto dei marcatori di discontinuità</td> 
   <td> </td> 
   <td><p>・ L'inserimento di annunci lato client non è supportato con flussi HLS contenenti discontinuità.</p> <p>・ La modifica del codec audio non è consentita tra le discontinuità nel flusso HLS.</p> <p>・ Lo switch Audio Track non è supportato per il flusso HLS con marcatori di discontinuità</p> </td> 
   <td>Il numero di sequenza di discontinuità è un requisito per i flussi HLS con discontinuità per la riproduzione su Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 18: Funzioni di protezione dei contenuti**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>L'intervallo di byte non è supportato con il contenuto crittografato AES-128.</td> 
   <td>12324: I flussi crittografati HLS AES-128 non vengono riprodotti su Safari se non è specificato il tag IV.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>・ 12660: Il lettore HTML5 genera un errore interno del server per i contenuti di trattini crittografati PlayReady scaduti.</p> <p>・ 16720: Il contenuto crittografato DASH DRM non funziona se manca l'attributo start nel tag punto.</p> <p>・ 18589: La riproduzione non è supportata per i flussi multiperiodo VoD DRM protetti con Xlink.</p> <p>・ 18653: La riproduzione del contenuto Widevine MultiPeriod con più chiavi si arresta al primo punto e non può passare al punto successivo.</p> <p>・ 18656: Flusso multiperiodo Playready, crittografato con chiavi diverse, non esegue la riproduzione.</p> <p>Playready 2.0 per Dash non è certificato.</p> <p> </p> <p> </p> </td> 
   <td>12602: I metadati DRM di Fairplay HLS vengono continuamente aggiornati dal lettore HTML5 su Safari</td> 
   <td><p>È possibile riprodurre contenuti DASH Widevine DRM confezionati tramite Bento4. Il contenuto inserito in pacchetti offline Packager e Shaka packager non viene riprodotto. DASH PlayReady DRM non è supportato.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 19: Funzioni di inserimento annunci core (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>・ Gli annunci preroll con contenuti live HLS vengono riprodotti in modalità dual player.</p> <p>・ Gli annunci DASH con contenuti HLS e annunci HLS con contenuti DASH non sono supportati.</p> <p>・ 19002: In HTML5 Player con MSE adBreak. L'oggetto InsertType non restituisce il valore corretto per rappresentare il tipo di inserimento corretto, ad esempio client inserito e o server inserito.</p> <p>7794: Sui dispositivi mobili (iOS, Android con Chrome 33 o versione inferiore o browser nativo) dove la barra di controllo predefinita è visibile in modalità a schermo intero, la barra di ricerca e i pulsanti di avanzamento rapido sono disponibili quando Ads Play.</p> <p>・ 11048: Il passaggio da un annuncio all'altro contenuto HLS Live non è uniforme nel caso di estensioni Media Source.</p> <p>・ 16083: In Android 4.4 Chrome v52, A volte HLS ad con contenuto HLS potrebbe causare un errore di decodifica della pipeline dopo la riproduzione in stallo.</p> <p>・ 16097: Gli errori rilevati durante l'interruzione dell'annuncio non vengono gestiti. È possibile che il flusso principale interrompa la riproduzione.</p> <p>・ 18095: Gli annunci MP4 non sono supportati con il contenuto live HLS.</p> <p>19120: Più ricerche su annunci HLS con contenuti HLS potrebbero causare l'arresto della riproduzione del flusso.</p> <p>・ 19131: Quando si passa da un'interruzione annuncio pre-roll al contenuto, potrebbe comparire una sovrapposizione di buffering.</p> <p>・ 20296: In caso di flussi HLS Live, la ricerca di nuovo nella finestra DVR seguita dalla ricerca nei rulli intermedi risolti potrebbe portare allo stallo di riproduzione.</p> <p>・ 20298:I flussi live HLS con rulli intermedi si fermano al momento del primo mid roll e si sposta dalla finestra DVR.</p> <p>・ 20317: I flussi HLS Live possono arrestarsi quando si passa all'annuncio successivo o dall'annuncio al contenuto, nel caso in cui l'interruzione dell'annuncio contenga più di un annuncio.</p> 
    <ul> 
     <li>Gli annunci nella finestra DVR dei flussi HLS Live non sono stati risolti.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>L’SDK non rispetta l’attributo della sequenza nella risposta VMAP per VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: L’SDK non rispetta l’attributo della sequenza nella risposta VMAP per VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: L'attributo di ripetizione VMAP non è supportato.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Creative Repackaging</td> 
   <td> </td> 
   <td>21464: La risposta dell'annuncio viene scartata completamente se la ricompilazione creativa non riesce per uno degli annunci nell'interruzione dell'annuncio.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 20: Funzioni avanzate di inserimento annunci (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo annunci</td> 
   <td> </td> 
   <td>20056: La proprietà della tecnologia del lettore non è rilevante in quanto si basa sul contenuto principale, vuoto in caso di riproduzione Solo annunci</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Criterio annuncio personalizzato</td> 
   <td> </td> 
   <td><p>・ I comportamenti degli annunci non sono supportati con annunci MP4 e contenuti MP4.</p> <p>・ 13973: Comportamenti di annunci personalizzati - Il criterio SKIP non genera eventi completi se utilizzato con MSE.</p> <p>・ 14939: I criteri di comportamento degli annunci personalizzati saltano e saltano le interruzioni di annuncio non funzionano per il contenuto DASH.</p> <p>・ 17131: Il primo fotogramma dell'annuncio è visibile, quindi il contenuto riprende in caso di criteri di interruzione e chiusura dell'annuncio.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Annunci pubblicitari/banner pubblicitari/Annunci cliccabili</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Gli annunci banner non sono visibili quando si utilizza il lettore di riferimento.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ I comportamenti degli annunci non sono supportati per gli annunci VPAID.</p> <p>・ 15032: Gli annunci VPAID in combinazione con annunci MP4 o HLS in un'interruzione di pubblicità non sono supportati.</p> <p>・ 19001: Su Android e iOS quando VPAID annuncio viene riprodotto con MP4 come contenuto principale, le tracce audio doppie sono udibili, uno dei contenuti principali e uno degli annunci.</p> <p>・ 20762: Gli annunci VPAID non sono supportati con Picture in Picture (PIP).</p> <p>・ 21172: L'evento Play complete non viene ricevuto per il contenuto HLS VOD con annunci VPAID.</p> <p>・ 21173: onAdBreakCompleteEvent non ricevuto per il contenuto VOD HLS e gli annunci VPAID post-roll.</p> </td> 
   <td>Il lettore attiva/disattiva la modalità normale e la modalità a schermo intero quando si passa da un annuncio VPAID al contenuto principale.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 21: Integrazioni**

| **Tipo di contenuto** | **Feature** | **Flash** | **HTML5 in Firefox, IE, Chrome, Android Chrome** | **HTML5 in Safari, iOS Safari** | **Chromecast (solo riproduzione DASH)** |
|---|---|---|---|---|---|
| VOD + Live | Integrazione VHL di Adobe Analytics |  | 19004: Il tracciamento dell&#39;analisi video non è disponibile tramite lo strumento di configurazione dell&#39;interfaccia utente. |  |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida nella pagina Informazioni e supporto [di](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.