---
title: Note sulla versione di TVSDK 2.4 per il browser
description: Le note sulla versione del browser TVSDK 2.4 descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Note sulla versione di TVSDK 2.4 per il browser {#browser-tvsdk-release-notes}

Le note sulla versione del browser TVSDK 2.4 descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.

## Introduzione {#introduction}

Browser TVSDK è un toolkit che consente di aggiungere funzionalità avanzate di riproduzione video, protezione dei contenuti e annunci pubblicitari alle applicazioni di riproduzione video basate su browser.

Il browser TVSDK 2.4 fornisce API JavaScript per creare applicazioni video basate su browser e include il supporto per la riproduzione nelle seguenti modalità:

* Solo HTML5
* HTML5 con fallback flash automatico
* Flash sempre

Questa versione include le seguenti informazioni:

· [Documentazione API TVSDK per il browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

· [Guida alla programmazione di TVSDK per browser](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

· [Guida alla migrazione da TVSDK per 1.4 DHLS a Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

· [Conversione dal browser TVSDK 2.4.6 alla versione 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

· Un’implementazione di riferimento, inclusa nella build.

>[!NOTE]
>
>*Per un elenco completo delle considerazioni di sicurezza per questa versione, vedere Considerazioni sulla sicurezza.

## Novità e funzionalità supportate {#what-s-new-and-supported-features}

Questa versione di Browser TVSDK offre nuove funzioni che è possibile utilizzare per migliorare le applicazioni video.

**Novità dell’aggiornamento del 2.4.12 (build 204)**

La seguente aggiunta è disponibile come parte dell’aggiornamento del browser TVSDK 2.4.12 (Build 204):

* L’implementazione dell’API del volume di AdobePSDK.MediaPlayer viene modificata per consentire la riproduzione automatica su iOS quando la riproduzione viene disattivata.

· Una nuova API, `auditudeSettings.ignoreVPAIDAds`, viene aggiunto per consentire di ignorare gli annunci VPAID ricevuti dal server di Auditude. L’API non funziona per il fallback del Flash.

**Versione 2.4.11**

I seguenti miglioramenti e aggiunte sono disponibili come parte della versione del browser TVSDK 2.4.11:

· Il failover dei segmenti HLS Live è supportato per le modalità di fallback di MSE e Flash.

· Supporto per `AuditudeSettings.creativeRepackagingDomain` L’API è ora disponibile anche per MSE. In precedenza era supportato solo con la modalità di fallback del Flash.

· La versione include correzioni per problemi critici del cliente. Consulta *Problemi risolti* un elenco.

**Versione 2.4.10**

I seguenti miglioramenti e aggiunte sono disponibili come parte della versione del browser TVSDK 2.4.10:

· TVSDK fornisce enableLogging() per abilitare o disabilitare la registrazione. Consulta la sezione [Documentazione API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)per l&#39;utilizzo.

· TVSDK non supporta più i capitoli predefiniti quando si utilizza Adobe Analytics. Definisci e gestisci i capitoli utilizzando l’applicazione.

· La versione include correzioni per problemi critici del cliente. Consulta *Problemi risolti *un elenco.

**Versione 2.4.9**

I seguenti miglioramenti e aggiunte sono disponibili come parte della versione Browser TVSDK 2.4.9:

· Sono supportati i flussi HLS VOD e Live con discontinuità temporale, ma senza marcatori di discontinuità.

· I frame ID3 v2.4.0 sono supportati con il tag video Safari per i flussi HLS VOD e Live.

· L’implementazione del caricamento sicuro degli annunci garantisce che le chiamate al server di annunci siano aggiornate a HTTP sicuro in base alla configurazione API. Per informazioni dettagliate, consulta Classi AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration. Questa funzione non è supportata in modalità di fallback del Flash.

· Le informazioni sull’ID annuncio e sull’estensione associate alle risposte VAST 3.0 sono ora rese disponibili all’applicazione da TVSDK e possono essere utilizzate per implementare l’integrazione Moat per le misurazioni degli annunci. Per informazioni dettagliate, consulta API AdobePSDK.NetworkAdInfo. Questa funzione non è supportata in modalità di fallback del Flash.

· AdobePSDK.ForceHttpsConfiguration non è più disponibile. Viene succeduto da

Classe AdobePSDK.ForceHttpsAdConfiguration.

· È ora disponibile una nuova API, AdobePSDK.optimizeFlashCalls, che consente di ottimizzare le chiamate per migliorare l’esperienza di riproduzione HLS in modalità di fallback del Flash. Questa funzione è disabilitata per impostazione predefinita.

**Novità dell’aggiornamento 2.4.8 (build 6002)**

Questo aggiornamento contiene correzioni per problemi critici del cliente. Consulta *Problemi risolti*, per l&#39;elenco.

**Versione 2.4.8**

I seguenti miglioramenti e aggiunte sono disponibili come parte della versione Browser TVSDK 2.4.8:

· L’SDK è ora conforme all’EME di Chrome e le modifiche alle best practice sono disponibili a partire da Chrome v58. Per ulteriori dettagli vedi [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

· Il framework dell’interfaccia utente ora supporta l’accesso HLS DRM nel flusso di lavoro Flash, Solo annuncio e Informazioni di targeting.

· L&#39;API setDRMAuthenticateData viene aggiunta al Framework dell&#39;interfaccia utente. Per riprodurre i flussi protetti con Adobe Access DRM, richiama questa API. In alternativa, è possibile specificare l’attributo drmAuthenticateData nel lettore. Consulta [AdobePSDK.videoBehavior](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)per i dettagli.

**Versione 2.4.7**

Le seguenti funzioni sono nuove nella versione 2.4.7 di:

· Aggiunta del Configuratore dell’interfaccia utente nel Framework dell’interfaccia utente

Puoi configurare il lettore in uno dei seguenti modi:

· Utilizzo di un oggetto JSON

· Utilizzo delle API

Per facilitare la generazione dell’oggetto JSON, il browser TVSDK fornisce uno strumento **UI Configurator **strumento.

Con questo strumento, puoi selezionare varie impostazioni, fare clic su **Prova configurazione **per verificare le impostazioni, quindi fare clic su **Scarica configurazione **per scaricare le impostazioni. Dopo aver scaricato il file, puoi passare il contenuto del file come oggetto JSON all’API ptp.videoPlayer.

· Aggiunta dell’API MediaPlayerItemConfig al framework dell’interfaccia utente

È possibile configurare tramite MediaPlayerItemConfig varie funzioni, tra cui advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration. Per ulteriori informazioni, consulta la documentazione AdobePSDK.MediaPlayerItemConfig in [API TVSDK del browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)** [documentazione](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Nel framework dell’interfaccia utente è stata modificata la modalità di passaggio delle configurazioni di rete tramite la configurazione del lettore.

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

* Supporto per i flussi di lavoro DRM e Analytics nel framework dell’interfaccia utente

Le configurazioni DRM e il tracciamento di Analytics possono essere abilitati tramite il Framework dell’interfaccia utente.

* Aggiunta di `AdobePSDK.embedSWFinFullScreenDiv` API

Questa nuova API offre flessibilità all’app del lettore per selezionare il div in cui può incorporare il file FlashFallback.swf.

* Sostituito `getVersion`API da `AdobePSDK.MediaPlayer` classe con `AdobePSDK.Version` classe per informazioni relative alla versione TVSDK. Per ulteriori informazioni, consulta `AdobePSDK.Version` API [qui](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versione 2.4.6**

Nella versione 2.4.6 sono state introdotte le seguenti funzioni:

* **Supporto Browserify**

Browserify consente di utilizzare i moduli di stile node.js nel browser. Puoi definire le dipendenze e Browserify raggruppa tutto in un unico file JavaScript.

* **Fatturazione**

Con l’aiuto della fatturazione, il browser TVSDK può raccogliere le metriche di utilizzo del lettore per fatturare ai clienti Primetime.

>[!NOTE]
>
>L’enum obsoleta MediaPlayer.Events e le costanti obsolete in Enum PSDKErrorCode sono state rimosse nella versione 2.4.6. Per ulteriori informazioni, consulta [Conversione dal browser TVSDK 2.4.5 alla versione 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versione 2.4.5**

Nella versione 2.4.5 sono state introdotte le seguenti funzioni:

* **Riproduzioni e annunci di eventi completi**

  I flussi FER (Full Event Replay) HLS ora supportano la risoluzione degli annunci e i comportamenti degli annunci. Per abilitare questo supporto, imposta la modalità di segnalazione dell’annuncio su `MANIFEST_CUES` durante la creazione di `MediaPlayerItemConfig` oggetto.

* **Supporto di MediaplayerView ScalePolicy**

  Gli sviluppatori di applicazioni possono ora specificare un ScalePolicy diverso per la visualizzazione utilizzando la proprietà scalePolicy di MediaplayerView.

* **Supporto di contenuti anamorfici**

  La riproduzione di contenuti anamorfici è ora supportata quando si utilizza MSE e la riproduzione di Flash.

* **Applicazione selettiva di`withCredentials`**

Quando `withCredentials` è impostato su true, il `Access-Control-Allow-Origin` l’intestazione non può essere impostata su un carattere jolly. A seconda della risposta del server, Browser TVSDK imposterà selettivamente il `withCredentials` attributo. Per ulteriori informazioni su questo supporto, consulta [Documentazione API TVSDK per browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versione 2.4.4**

Le seguenti funzioni erano nuove nella versione 2.4.4:

* **App di esempio Chromecast**

Questa versione fornisce il supporto per un’app di invio e ricezione che illustra la riproduzione di flussi DASH VOD e flussi DASH Widevine con inserimento di annunci lato client.

* **Supporto di failover avanzato**

Questa versione contiene il supporto per casi di utilizzo di failover avanzato (failover di segmenti e server) per flussi VOD HLS.

**Versione 2.4.3**

Nella versione 2.4.3 erano state introdotte le seguenti funzioni:

* **Tag personalizzati per DASH VOD**

  I tag personalizzati in linea (Eventi) possono essere sottoscritti e ricevuti come oggetto TimedMetadata.

* **Riproduzione di flussi senza estensioni**

  Sono ora supportati i flussi HLS e DASH senza estensioni. Per il file manifesto, è necessario specificare resourceType durante il caricamento della risorsa. Per i segmenti e i file VTT, l’intestazione di risposta Content-Type viene utilizzata per determinare il tipo di contenuto.

**Versione 2.4.2**

Nella versione 2.4.2 erano state introdotte le seguenti funzioni:

* **Parità API**

Per un elenco completo della parità API, vedi [Guida alla migrazione da TVSDK per 1.4 DHLS a Browser TVSDK 2.4](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Esempio di supporto AES**

  Questa versione aggiunge il supporto per la riproduzione di contenuti crittografati Sample-AES su MSE e fallback di Flash. È stato rimosso il requisito per l’hosting di contenuti AES su un’origine sicura in Google Chrome.

* **Supporto per contenitori AAC**

  È ora supportata la riproduzione di file con estensione .aac. Può trattarsi di flussi solo audio o di audio alternativo.

  >[!NOTE]
  >
  >I codec AC3 e AC3 avanzati non sono ancora supportati.

* **Riproduzione di flussi con token**

I flussi HLS consegnati tramite una rete CDN (Content Delivery Network) possono a volte utilizzare token di autenticazione nelle richieste di manifesti e segmenti per la verifica e possono essere forniti come parametri URL o come intestazioni cookie. La riproduzione di tali flussi è ora supportata.

**Versione 2.4.1**

Nella versione 2.4.1 erano state introdotte le seguenti funzioni:

* **Framework interfaccia utente**

Questo framework, progettato per accelerare lo sviluppo dell’interfaccia utente per le applicazioni di riproduzione video basate su JavaScript, è costituito da API per l’inclusione di controlli di base come riproduzione/pausa e volume e per l’aggiunta o la rimozione semplice di elementi come gli stati delle barre di scorrimento e le impostazioni dei sottotitoli. Puoi specificare il comportamento associato ai controlli, creare controlli personalizzati ed eseguire l’interfaccia dell’interfaccia utente del lettore. Tutto questo avviene attraverso il framework, senza alcuna necessità di manipolare direttamente la struttura DOM.

* **Miglioramenti alla riproduzione HLS per i flussi live**

Questa versione supporta le discontinuità causate dall’inserimento di annunci. Utilizza il tag EXT-PROGRAM-DATE-TIME seguito dal tag EXT-MEDIA-SEQUENCE per eseguire la sincronizzazione tra i profili bitrate adattivi al fine di garantire una riproduzione fluida.

* **Supporto VPAID 2.0**

La definizione VPAID (ad-serving interface definition, interfaccia per il lettore video), versione 2.0, offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video. Questa versione supporta annunci VPAID JavaScript lineari per contenuti video on-demand (VOD).

* **Tag HLS personalizzati**

I flussi multimediali possono contenere metadati aggiuntivi sotto forma di tag nel file di playlist/manifesto. Browser TVSDK consente di specificare e sottoscrivere tag aggiuntivi e di ricevere una notifica quando tali tag vengono visualizzati nel manifesto.

* **Marcatori annuncio visualizzati sulla timeline del lettore**

Questa versione supporta la visualizzazione di marcatori di annunci sulla timeline del lettore sia per contenuti VOD che Live. Puoi vedere questo comportamento nel lettore di riferimento.

**Supportato in 2.4**

Nella versione 2.4 erano disponibili le seguenti funzioni:

* **Riproduzione audio MP3**

  Questa versione supporta la riproduzione audio MP3 sui browser con Media Source Extensions (MSE) e con il tag video Safari.

* **Riproduzione video MP4**

  Sono supportate le seguenti funzionalità:

   * Riproduzione a flusso singolo
   * Annunci MP4 pre-roll e post-roll con comportamenti e tracciamento degli annunci
   * Annunci HLS pre-roll e post-roll con comportamenti e tracciamento degli annunci
   * Annunci DASH pre-roll e post-roll con comportamenti e tracciamento degli annunci

## Piattaforme supportate {#supported-platforms}

Browser TVSDK ha requisiti specifici per i livelli di piattaforme e software su cui deve essere eseguito. Sono supportati i seguenti livelli software e piattaforme:

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

* APPLE OS X

   * Safari 9+
   * Chrome 33+
   * Firefox 38+

### Configurazioni web per dispositivi mobili {#mobile-web-configurations}

* Android 4.4

   * Browser nativo
   * Chrome 33+

* Android 5.0

   * Browser nativo
   * Chrome 33+

* Android 6.0

   * · Chrome 33+

* APPLE IOS 9

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
   <td><p><strong>Tag video TVSDK per browser</strong><sup>1</sup></p> </td> 
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
   <td><p>Internet Explorer 11</p> <p>(Windows 7</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, TRATTINO</p> </td> 
   <td><p>MP4 e HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matrice di funzioni {#feature-matrix}

Elenco delle funzioni supportate e non supportate per questa versione:

* *Caratteristiche audio MP3 — Riproduzione Core*
* *Funzioni video MP4 — Riproduzione core*
* *Funzioni video MP4 — Core Ad Insertion*

>[!NOTE]
>
>*Nelle tabelle delle matrici di funzioni riportate di seguito, il valore &quot;Y&quot; indica che la funzione è supportata nella versione corrente.*

### Caratteristiche audio MP3 {#mp-audio-features}

**Tabella 1: Riproduzione Core{#table-core-playback}**

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD MP3 | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

1 Il tag video TVSDK del browser non supporta streaming e DRM. Il supporto per codec e contenitori non è lo stesso in tutti i browser.

2 Firefox utilizza come impostazione predefinita il Flash Player per la versione 41 o precedente.

### Caratteristiche audio MP4 {#mp-audio-features-1}

**Tabella 2: Riproduzione Core**

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | VOD MP4 | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

**Tabella 3: Ad Insertion principali**

| Categoria | Tipo di contenuto | Funzionalità | Flash | HTML 5: FF, IE, Chrome, Android Chrome | HTML 5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD MP4 | Pre-roll (MP4) | Non supportato | Y | Y |
| Ad Insertion | VOD MP4 | Post-roll (MP4) | Non supportato | Y | Y |

Per ulteriori informazioni sul supporto delle funzioni HLS o DASH, vedere di seguito.

## Matrice di funzioni HLS {#hls-feature-matrix}

Di seguito è riportata la matrice delle funzioni per HLS in Browser TVSDK.

* *Riproduzione core HLS*
* *Funzioni di riproduzione avanzate HLS*
* *Funzioni di protezione del contenuto HLS*
* *Funzioni di inserimento e core HLS*
* *Funzioni avanzate di inserimento annunci HLS*
* *Integrazioni HLS*

>[!NOTE]
>
>*Nelle tabelle delle matrici di funzioni riportate di seguito, il valore &quot;Y&quot; indica che la funzione è supportata nella versione corrente.*

### Funzioni HLS {#hls-features}

Sono supportate le seguenti funzionalità:

**Tabella 4: Riproduzione core HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>VOD FER</p> </td> 
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
   <td><p>Sottotitoli 608/708</p> </td> 
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
   <td><p>Failover del manifesto</p> </td> 
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
   <td><p>Notifiche QoS e lettore</p> </td> 
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
   <td><p>Imposta adattivo</p> <p>controlli della velocità di trasmissione</p> </td> 
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
   <td>Audio di associazione tardiva</td> 
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
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>Trick Play</p> </td> 
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
   <td><p>Supporto per marcatori di discontinuità</p> </td> 
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

**Tabella 6: funzioni di protezione del contenuto HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>Accesso Adobe</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 7: Funzioni di inserimento e core HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD FER</p> </td> 
   <td><p>Risoluzione e comportamenti degli annunci</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annuncio predefinito</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reimballaggio creativo (da MP4 a HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 8: Funzioni avanzate di inserimento degli annunci HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo annuncio</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parametri di targeting</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Parametri personalizzati</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annuncio personalizzato</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Caricamento annuncio lazy</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>Limitazione piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci di accompagnamento, banner pubblicitari, annunci cliccabili</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
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
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML 5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrazioni</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrazione Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Matrice di funzioni TRATTEGGIO {#dash-feature-matrix}

Ecco la matrice delle funzioni per le funzioni DASH in Browser TVSDK.

· *Funzioni di riproduzione core DASH*

· *DASH Funzioni di riproduzione avanzate*

· *DASH Funzioni di protezione del contenuto*

· *Funzionalità di inserimento e core DASH*

· *DASH Funzioni avanzate di inserimento annunci*

· *Integrazioni DASH*

>[!NOTE]
>
>Nelle tabelle delle matrici di funzioni riportate di seguito, il simbolo Y indica che la funzione è supportata nella versione corrente.

### Feature TRATTEGGIO {#dash-features}

Sono supportate le seguenti funzionalità:

**Tabella 10: funzioni di riproduzione core DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
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
   <td><p>VOD FER</p> </td> 
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
   <td><p>Sottotitoli 608/708</p> </td> 
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
   <td><p>Notifiche QoS e lettore</p> </td> 
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
   <td><p>Impostazione dei controlli del bit rate adattivo</p> </td> 
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
   <td><p>Audio con associazione in ritardo</p> </td> 
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

**Tabella 11: funzioni di riproduzione avanzate DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
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
   <td><p>Trick play</p> </td> 
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
   <td><p>Supporto di più periodi</p> </td> 
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

**Tabella 12: funzioni di protezione del contenuto DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
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
   <td><p>· Widevine su Chrome, Firefox 47 e versioni successive e Chromecast</p> <p>· PlayReady in Internet Explorer su Windows 8.1 ed Edge</p> <p>· DRM Primetime per Windows Firefox (solo video)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 13: feature di inserimento e core DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/TRATTINO)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (TRATTINO)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD FER</p> </td> 
   <td><p>Risoluzione e comportamenti degli annunci</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annuncio predefinito</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reimballaggio creativo (da MP4 a DASH)</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 14: feature di inserimento pubblicitario avanzate DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Solo annuncio</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parametri di targeting</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Parametri personalizzati</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annuncio personalizzato</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Caricamento annuncio lazy</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci per compagni di viaggio, banner pubblicitari, annunci cliccabili</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
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
   <td><p><strong>Funzionalità</strong></p> </td> 
   <td><p><strong>HTML 5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrazioni</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Integrazione Adobe Analytics VHL</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Problemi risolti {#issues-fixed}

**Problemi risolti nell’aggiornamento 2.4.12 (Build 204)**

Sono stati risolti i seguenti problemi nella versione 2.4.12 del browser TVSDK Update (Build 204):

· **21647**- TVSDK deve consentire la riproduzione video automatica sui dispositivi iOS quando l’audio è disattivato.

· **21465**- Viene ricevuto un messaggio di errore di tipo Accesso negato al sistema quando si riproduce un flusso DASH protetto da DRM dopo la riproduzione di un flusso DASH Live.

· **21442**: abilita la riproduzione automatica del contenuto su iOS Web, dopo la riproduzione dell’annuncio preroll con un gesto dell’utente.

· **21240**: API fornita per filtrare gli annunci VPAID analizzati dall’Auditude/VMAP.

**Problemi risolti nella versione 2.4.11**

I seguenti problemi sono stati risolti nella versione 2.4.11 di TVSDK per il browser:

**Funzioni di riproduzione di base:**

· **19192**: TVSDK ora implementa TextFormat:bottomInset e TextFormat:safeArea. Grazie a questi miglioramenti, i sottotitoli codificati possono essere riposizionati se la barra di controllo viene visualizzata sullo schermo.

· **21009**: i sottotitoli codificati persistono sullo schermo in caso di ricerca attraverso la discontinuità fino alla visualizzazione di nuovi sottotitoli.

· **21141**: la ricerca viene rifiutata a causa di una situazione di tipo &quot;race condition&quot; durante l’aggiunta del segmento.

· **21142**: rendendo disponibili intervalli di riproduzione ricercabili quando il lettore è in stato INIZIALIZZATO. A causa di queste modifiche, ora è supportato avviare la sessione dalla posizione.

· **21363**: i sottotitoli codificati 608/708 non saranno più sincronizzati dopo l’inserimento degli annunci per i flussi DASH.

**Funzioni di inserimento annunci:**

· **21179**: i problemi relativi al mid-roll (pause lunghe, fotogrammi neri) con contenuti VOD ora vengono risolti impostando correttamente la proprietà ad.primaryAsset.adParameters.

· **21257**: il file MP4 con la velocità in bit più elevata viene selezionato per la transcodifica se MP4 non è un tipo mime valido e la funzione di riconfezionamento creativo è abilitata.

· **21361**: TVSDK ora trasmette l’ID del sistema di annunci e l’ID creativo dalla risposta VAST come parametri di query nella richiesta di creazione pacchetti al fine di supportare regole di normalizzazione aggiuntive.

**Problemi risolti nella versione 2.4.10**

I seguenti problemi sono stati risolti nella versione 2.4.10 di TVSDK per il browser:

**Funzioni di riproduzione di base:**

· **21060**: errore codec non valido generato con flussi HLS che contengono discontinuità e le caselle BMFF ISO vengono eseguite fino alla fine del flusso.

· **21045**: la riproduzione automatica non funziona su iOS dopo il completamento della prima riproduzione video in una playlist.

· **20975**: la frequenza fotogrammi viene restituita come NaN dal provider QoS sul browser Chrome.

· **20823**: errore codec non supportato generato quando si incontrano segmenti senza dati.

· **20769**: l’SDK inizia ora con la velocità in bit corrente al momento della ricerca, invece di passare immediatamente in base ai criteri ABR.

· **20031**: in modalità verticale su IE11 (Windows 8.1), lo schermo video diventa piccolo. Funzione di protezione dei contenuti:

· **19316**: salta i segmenti che non riescono a decrittografare in caso di flussi HLS AES-128.

**Problemi risolti nella versione 2.4.9 di**

Sono stati risolti i seguenti problemi nella versione 2.4.9 di TVSDK per il browser:

**Funzioni di riproduzione di base:**

· **13407**: i flussi DASH possono bloccarsi se Firefox smette di inviare l’evento &quot;ontimeupdate&quot; durante la riproduzione.

· **16380**: durante la riproduzione di contenuti audio video misti di segmenti con orari di inizio non corrispondenti tramite MSE, l’errore di sincronizzazione audio tra rappresentazioni si accumula sugli switch ABR, generando in ultima analisi un errore (#663686 del problema cromo).

· **17985**: durante la riproduzione di un particolare flusso ISO-BMFF sul browser Firefox, la riproduzione si blocca (problema di Firefox #1342913). Questo problema è stato risolto dopo Firefox v53.

· **19141**: ReferenceError non rilevato (in promise): la larghezza non è definita.

· **18997, 19299**: problema di visualizzazione momentanea di altri video al limite del segmento. Ciò si verificava perché l’SDK non calcolava correttamente l’offset temporale della composizione dell’ultimo campione.

· **19780**: la riproduzione non viene avviata per il contenuto HLS e l’annuncio HLS su Firefox v53 (Firefox issue #354653).

· **20046**: la data e l’ora del programma vengono ricevute come chiave invece del valore quando vengono ricevute come oggetto metadati temporizzati.

· **20047**: useDefaultResizeHandler genera un errore con il fallback del Flash.

· **20179**: il fallback del Flash non funziona con il Flash Player v25.0.0.171.

· **20293**: Firefox interrompe il buffering dei dati per alcuni flussi HLS, causando lo stallo.

· **20626**: il lettore genera un errore di decodifica dei contenuti multimediali su Chrome a causa di una gestione errata dei campioni video con durata pari a zero.

· **20078**: la riproduzione si interrompe in seguito all’errore del browser &quot;QuotaExceeded&quot; (Limite superato).

· **18639**: nel flusso HLS Live 608 il testo CC a volte viene visualizzato come errato.

· **20028**: il parametro di dimensione ClosedCaptions non modifica la dimensione del carattere.

· **20613**: le caselle con sottotitoli codificati si sovrappongono rendendo tali sottotitoli illeggibili.

**Caratteristiche principali di Ad Insertion (CSAI):**

· **20043**: chiamate di impression e tracciamento degli annunci mancanti con più annunci e reindirizzamenti di terze parti.

· **20044**: quando si utilizza il repackaging creativo, tutti gli annunci nell’interruzione pubblicitaria devono essere ricompilati correttamente; in caso contrario, l’interruzione pubblicitaria viene completamente eliminata.

· **20097**: la riproduzione dell’annuncio viene saltata e il contenuto principale riprende immediatamente, anziché attendere 20 secondi per il timeout se il manifesto dell’annuncio non è disponibile.

**Problemi risolti nell’aggiornamento versione 2.4.8 (Build 6002)**

Sono stati risolti i seguenti problemi nell’aggiornamento TVSDK versione 2.4.8 del browser (Build 6002):

· **14126:** La riproduzione potrebbe bloccarsi su Firefox (problema #1316024) a causa di un gap interno nel buffer sorgente MSE. Prova a cercare per riprendere la riproduzione

· **19608:** Correzione per rispettare il valore di scostamento temporale dall’Auditude della risposta VMAP.

· **19635:** Corregge il blocco video in Internet Explorer 11 su Windows 10.

· **19761:** Correzioni relative ai problemi ABR con HLS.

· **19780:** È stata corretta la riproduzione dell’annuncio con contenuti HLS interrotti in Mozilla Firefox v53.

· **19877 e 19744:** Questo problema risolve l’incoerenza nella selezione del bitrate dopo un’operazione di ricerca. Ora la selezione del bitrate alla ricerca è il valore più basso del bitrate corrente e del bitrate all&#39;avvio.

· **19881:** La riproduzione bloccata e la sovrapposizione del buffering vengono visualizzate per un tempo infinito dopo che la ricerca viene eseguita per 3-4 volte.

· **19884:** Conferma la conformità ai requisiti del percorso multimediale verificato beta di Chrome 59 (VMP). bTVSDK è stato in grado di riprodurre contenuti Widevine DRM con Chrome 59 Beta.

· **19916:** La riproduzione DRM nell’interfaccia utente Framework è stata interrotta. Ora, richiama acquisitionLicense anche se non sono presenti criteri nei metadati.

**Problemi risolti nella versione 2.4.8**

Sono stati risolti i seguenti problemi nella versione Browser TVSDK 2.4.8:

· **10075**: quando si esegue la ricerca prima della timeline, l’evento di riproduzione completa non è stato ricevuto su Firefox e Chrome e l’evento di ricerca non è stato ricevuto su Firefox.

· **15775**: evento Riproduci completo non ricevuto in Windows 8.1 Internet Explorer.

· **17306**: per i flussi SSAI, la riproduzione è supportata. Il tracciamento degli annunci uniti non è supportato.

· **19142**: a volte il riavvolgimento fa sì che il lettore video rimanga per sempre nello stato di buffering.

· **19218**: i marcatori annuncio non sono disponibili tramite il framework dell’interfaccia utente.

· **19219**: la sola riproduzione degli annunci non funziona tramite il framework dell’interfaccia utente.

· **19222**: la chiave AES-128 viene richiesta una volta per una playlist e le richieste successive vengono servite dalla cache. In precedenza veniva richiesto per ogni segmento.

· **19597**: &quot;TypeError non rilevato: impossibile leggere la proprietà &quot;log&quot; di undefined&quot; visualizzata con le build Chrome canary.

· **19605**: adRequestDomain non era disponibile in modalità di fallback del Flash.

· **19608**: gli annunci VMAP non venivano inseriti per i flussi HLS Live. L’SDK ora considera i marcatori di cue e non si basa sui valori di scostamento temporale nelle risposte VMAP.

· **19637**: la riproduzione degli annunci solo porta a un errore di script alla fine dell’annuncio.

· **19732**: le richieste della playlist CRS non riuscivano con errore 404. Le richieste 1401 e 1403 del browser TVSDK sono ora aggiornate per occuparsene.

· **19762**: acquisitionLicense veniva chiamata prima di setAuthenticationToken a causa della quale veniva restituita una licenza valida indipendentemente dalla validità del token. Questo problema è risolto ora e acquisitionLicense viene chiamato solo dopo la risposta setAuthenticationToken.

**Problemi risolti nella versione 2.4.7 di**

Nella versione 2.4.7 sono stati risolti i seguenti problemi:

· **8397**: i flussi HLS Live generati tramite Adobe Media Server potrebbero non essere riprodotti se i segmenti non iniziano con un fotogramma chiave.

· **13606**: sono stati risolti diversi problemi relativi alla ricerca per il flusso HLS sul browser Chrome.

· **14807**: nel browser Chrome, se la ricerca o la pausa viene attivata immediatamente dopo la riproduzione(), la riproduzione potrebbe interrompersi con l’errore DOMException: La richiesta play() è stata interrotta da una chiamata... (Chromium issue# 593273).

· **19085**: i parametri MediaPlayer come volume, abrControlParameters e ccStyle non sono impostati sui valori predefiniti al momento del ripristino del lettore.

**Problemi risolti nella versione 2.4.6 di**

Nella versione 2.4.6 è stato risolto il seguente problema:

· **18093**: TimedMetadata per il tag accanto al tag sottoscritto viene restituito quando si utilizza la versione 24 del Flash Player in modalità Fallback del Flash.

**Problemi risolti nella versione 2.4.4**

Nella versione 2.4.4 sono stati risolti i seguenti problemi:

· **8711**: in MSE, i sottotitoli 608/708 rimangono giustificati per impostazione predefinita.

· **13934**: le impostazioni ABR per gli annunci non sono applicabili quando si riproducono con flussi HLS Live.

· **14079**: la durata dei flussi HLS Live con finestra DVR bassa potrebbe non riuscire poiché la riproduzione potrebbe rimanere indietro a causa di problemi di latenza della rete. Fate clic sul punto attivo per riprendere la riproduzione.

· **15037**: gli esempi forniti con il framework dell’interfaccia utente del lettore non funzionano in Microsoft Internet Explorer 10 su Windows 7.

· **15913**: per i flussi VOD HLS, in Chrome il flusso non viene riprodotto se la risposta del manifesto è 304 non modificata. Questo problema è stato risolto a partire da Chrome v55 (Chromium issue 633696).

· **16103**: su Android Chrome, in condizioni di larghezza di banda ridotta, la riproduzione potrebbe interrompersi con TypeError non rilevato: impossibile leggere la proprietà &#39;programDateTime&#39; di errore non definito.

· **16265**: per i flussi VOD HLS e Live, la ricerca tra discontinuità non funziona.

· **16709**: la ripresa dello streaming HLS Live con PDT e marcatore di discontinuità può causare il blocco del lettore nel buffering.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Le limitazioni e i problemi noti in Browser TVSDK sono menzionati di seguito.

**Tabella 16: Caratteristiche principali di riproduzione**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td><p>· I formati multimediali diversi da HLS non sono supportati.</p> <p>8799: il fallback del Flash non si occupa dei contenuti misti e pertanto è necessario garantire che Contenuto, Annuncio e altri URL non conducano a contenuti misti (contenuti sicuri e non sicuri insieme).</p> <p>· 19271: la riproduzione di più viste tramite il framework dell’interfaccia utente non è supportata nella modalità di fallback del Flash.</p> <p>· Il fallback di Flash non funziona in Microsoft Internet Explorer 8 e 9 su Windows 7 in quanto queste versioni non sono supportate dall'SDK.</p> <p>· 20262: il fallback del Flash aggiunge parametri personalizzati all’elenco di informazioni di targeting. Anche l’ordine di priorità dei parametri personalizzati è diverso in caso di Flash e MSE.</p> <p>· 20653:Il fallback del Flash TVSDK del browser non funziona su Win10 con Creators Update.</p> <p>· Flash Fallback funziona con il Flash Player versione 23 e successive.</p> <p>· 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (impostazione predefinita), la riproduzione HLS non funziona in modalità Fallback del Flash. Sta funzionando bene su Canary.</p> </td> 
   <td><p>· 12563: i flussi trattino con codec audio mp4a.40.02 non vengono riprodotti su Firefox a causa di una stringa di codec audio non supportata in MPD. È supportato il codec audio mp4a.40.2.</p> <p>15029: quando si passa da un video all’altro in multiView nell’interfaccia utente-Framework, il pulsante di riproduzione/pausa non viene aggiornato di conseguenza.</p> <p>· 16034:In Windows 8.1 IE, la chiamata di reset() causa un errore di tipo MIME sconosciuto. Ricarica il supporto per riprendere la riproduzione.</p> <p>· 18235: alcuni problemi di ricerca vengono osservati con i flussi di vod DASH con Ads.</p> <p>· 18727: API di errore non supportata per MSE</p> <p>18750: in alcuni casi, gli eventi di modifica dello stato potrebbero non essere ordinati per l’SDK e il framework dell’interfaccia utente e, dopo il caricamento della risorsa, gli eventi IDLE e Initializing StatusChange potrebbero non essere presenti per i listener di eventi aggiunti.</p> <p>· 18889: se MediaPlayer è in stato ERROR, l'oggetto di visualizzazione non viene restituito.</p> <p>· 19039: se AdobePSDK. MediaPlayer. seekToLocal() viene utilizzato con un valore maggiore di EOF, quindi la riproduzione inizia dall’inizio in caso di MSE.</p> <p>· 19049: non è stato segnalato alcuno stato di errore per il Flash Player su Chrome, IE, Firefox quando il video è bloccato durante la riproduzione.</p> <p>· 17205: la riproduzione video si interrompe durante la riproduzione di uno streaming non muxed per alcune ore mentre l’audio continua a essere riprodotto (problema Chromium n. 664033).</p> <p>· 12308: ai flussi DASH con_time_offset_component specificati può essere applicato timeStampOffset sul browser Chrome, causando un tempo di decodifica negativo e quindi un errore MEDIA_ERR_ SRC_NOT_ SUPPORTED (problema di cromo #398141).</p> <p>· 14126: la riproduzione potrebbe bloccarsi su Firefox (problema n. 1316024) a causa di un gap interno nel buffer sorgente MSE. Prova a cercare per riprendere la riproduzione.</p> <p>· 19115: MS Edge e IE 11 (Win 8.1 e 10) non impostano Origin su null nel reindirizzamento CORS e tuttavia non riescono perché l’intestazione non è null e causa un errore di riproduzione.</p> <p>· 19861: problema con il comportamento di aggiunta sul buffer di origine per i file multimediali già riprodotti. Chrome rifiuta il frammento aggiunto, incluso lo spostamento, causando un errore di decodifica successivo. (Problema di cromo #735335)</p> <p>19921: la riproduzione di determinati contenuti HLS si interrompe anche se vengono memorizzati correttamente nel buffer (problema Chromium #713540)</p> <p>· 20444: la ricerca della fine dell’intervallo nel buffer su IE ed Edge può causare l’arresto della riproduzione.</p> <p>· 20511: a volte può essere osservato il rifiuto della ricerca per i flussi HLS con o senza annunci.</p> <p>· 20743: su Windows 10 Chrome, lo streaming HLS Live viene riprodotto per alcuni secondi prima della riproduzione MP4 pre-roll.</p> <p>· 21043: la dimensione video potrebbe non essere corretta al caricamento iniziale a causa della mancanza di metadati.</p> <p>· 21115: per avviare la riproduzione è necessario un gesto utente Android se l’annuncio pre-roll è disponibile per i video in una playlist.</p> <p>· HLS Live non supporta il rollover della marca temporale.</p> <p>· Audio AAC-SSR non supportato.</p> <p>I codec audio AC3 e Enhanced AC3 non sono supportati.</p> <p>· Per i flussi con discontinuità della marca temporale ma senza marcatori di discontinuità</p> <p>· La riproduzione potrebbe presentare problemi e la ricerca non corretta a causa di salti.</p> <p>· La durata del contenuto e la durata della riproduzione potrebbero non corrispondere.</p> <p>· Le discontinuità tra rappresentazioni e rappresentazioni dovrebbero corrispondere ad altre potrebbero causare problemi di sincronizzazione e arresto.</p> <p>· I sottotitoli e WebVTT potrebbero non essere visualizzati vicino alla fine del flusso.</p> <p>· Le modifiche al codec audio non sono supportate nei salti con marca temporale.</p> <p>· Inserimento di annunci non supportato.</p> <p>· La modalità di avanzamento rapido può causare un loop di riproduzione su Win 8.1 IE 11 (#12446268 problemi MS).</p> <p>TRATTINO:</p> <p>· Per flussi live: è supportato il profilo live con tipo dinamico.</p> <p>· Per flussi VoD: è supportato il profilo live con tipo statico.</p> <p>Per i flussi VoD: il profilo ondemand non è certificato per i flussi di lavoro degli annunci.</p> </td> 
   <td><p>· I flussi DASH Live e DASH Video on Demand non sono supportati.</p> <p>· La riproduzione video PIP (Picture in Picture) non è supportata su iOS in modalità a schermo intero.</p> <p>In Safari (tag video), un manifesto meno evidente senza l’intestazione del tipo di contenuto corretta non funziona.</p> </td> 
   <td><p>· applicationID nell'app del mittente deve essere lo stesso generato alla registrazione dell'URL di Receiver come app di ricezione personalizzata.</p> <p>· Il lettore di riferimento è certificato per i flussi di lavoro DASH. Il framework dell’interfaccia utente non è certificato.</p> <p>Per un elenco dei codec multimediali supportati, consulta <a href="https://developers.google.com/cast/docs/media"><em>qui</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>VOD FER</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td> </td> 
   <td>18098: con il flusso FER LBA HLS si osservano alcuni problemi di ricerca.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Bitrate adattivo</td> 
   <td><p>· 20079: riscrittura del buffer in caso di ricerca entro l'intervallo del buffer.</p> <p>20080: il comportamento dell’ABR di Flash è in linea con quello del MSE.</p> </td> 
   <td><p>· La variante di fallback solo audio in un flusso ABR viene ignorata a causa di limitazioni relative al buffer.</p> <p>· 12289: i parametri di controllo ABR non si applicano all'audio in caso di flussi HLS/DASH non misti.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Sottotitoli 608/708</td> 
   <td> </td> 
   <td><p>· 7810: su Android 4.4.4 Chrome non sembra avere il supporto per le famiglie di font CSS di base utilizzate dal lettore e quindi la funzione di modifica dello stile del font non funziona.</p> <p>· I canali CC non possono essere modificati nel caso di sottotitoli 608.</p> <p>· Le funzioni di stile avanzate non sono supportate per i sottotitoli 608.</p> <p>Sono supportati i sottotitoli incorporati (608/708) segnalati tramite il tag Accessibilità.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>· 5206: i tag di regione nel file WebVTT vengono ignorati dal lettore durante la visualizzazione dei sottotitoli.</p> <p>· DASH: i file VTT frammentati /segmentati non sono supportati.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover del manifesto</td> 
   <td>21056: con Fallback Flash, il failover non si verifica per lo streaming live se il flusso primario restituisce un errore 404 durante la riproduzione.</td> 
   <td>Il failover del manifesto è applicabile solo ai contenuti e non agli annunci.</td> 
   <td>Il failover della playlist mancante funziona su Safari solo per il codice di errore HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover avanzato</td> 
   <td> </td> 
   <td><p>· Il failover dei segmenti non supporta il salto dei segmenti non disponibili e la prosecuzione della riproduzione.</p> <p>20533: i segmenti mancanti in una playlist devono essere trattati come una Discontinuità e la riproduzione deve riprendere dal successivo segmento disponibile.</p> <p>21267: la commutazione di flusso dovuta al failover può causare il download di segmenti precedenti.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Notifiche QoS e lettore</td> 
   <td>21129: il frame rate non è disponibile in caso di fallback del Flash.</td> 
   <td><p>• 11170:</p> <p>Timed_Event non è disponibile per TVSDK per browser con MSE, a differenza di TVSDK per browser con fallback di Flash.</p> <p>21129: la frequenza fotogrammi non viene calcolata per i flussi live.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto per le intestazioni dei cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Il flag withCredentials e le intestazioni dei cookie non sono supportati in Safari.</p> <p>21051: per consentire i cookie in Safari, abilita l’impostazione "Cookie e dati del sito web" da Preferenze &gt; Privacy.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Tag personalizzati</td> 
   <td>14763: i tag personalizzati diversi da quelli che iniziano con # non devono essere supportati. Al momento viene creato e segnalato l’oggetto TimedMetadata per tali tag durante il fallback del Flash.</td> 
   <td>I flussi con tag personalizzati in banda non sono certificati.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Late Binding Audio</td> 
   <td> </td> 
   <td><p>· L’inserimento di annunci non è supportato con i flussi LBA HLS Live.</p> <p>· 17273: i flussi LBA VOD HLS passano alla rappresentazione predefinita in caso di failover e non possono essere ripristinati all’ultima selezione.</p> <p>· 20251: il flusso LBA HLS Live potrebbe bloccarsi durante la ricerca.</p> <p>· 20497: il lettore rimane in stato di buffering se i flussi HLS LBA non misti hanno fotogrammi audio o video mancanti vicino alla fine del flusso.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Reindirizzamento 302</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>l'ottimizzazione del reindirizzamento non è supportata nei browser Windows Edge e IE in quanto non supportano la proprietà responseURL nell'oggetto XMLHttpRequest.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 17: Funzioni avanzate di riproduzione**

<table> 
 <tbody> 
  <tr> 
   <td>Tipo di contenuto</td> 
   <td>Funzionalità</td> 
   <td>Flash</td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Riproduzione a offset</td> 
   <td><p>L'avvio della riproduzione con un particolare valore di offset non è supportato per i contenuti MP4.</p> </td> 
   <td>20492: gli annunci mid-roll che precedono l'offset vengono riprodotti prima che il contenuto riprenda dal valore di offset.</td> 
   <td>La riproduzione con funzione di offset non è supportata in iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>Smooth Trickplay non funziona per i flussi privi di rappresentazioni iFrame.</td> 
   <td><p>· Gli adattamenti Trick Play non sono supportati su Firefox e Internet Explorer, pertanto la modalità reverse trick non è disponibile in questi browser.</p> <p>· La funzione Trickplay non è disponibile quando si riproducono contenuti con annunci.</p> <p>· 10435: durante la riproduzione DASH, il video si blocca durante la riproduzione con i trucchi in avanti su Internet Explorer (Win 8.1)</p> <p>a intermittenza. Ciò si verifica in quanto viene utilizzata la proprietà playbackRate degli elementi video senza l’adattamento alla riproduzione mediante trucco.</p> <p>14182: a volte, durante il riavvolgimento sul browser Chrome, l’evento di ricerca potrebbe non essere ricevuto e quindi la modalità trucco non funziona.</p> <p>· 14942: le velocità di riproduzione possono essere impostate su Chrome per Android anche in caso di flussi di riproduzione non trick ma l’impostazione non viene applicata e la riproduzione continua a velocità normale.</p> <p>· 17308: la ricerca non funziona in modalità Trickplay.</p> <p>· 17309: nel browser Chrome, la modalità reverse trick non può essere mantenuta per più di 2 secondi.</p> <p>19272: la riproduzione dei trucchetti potrebbe non essere ripristinata dal buffering nel browser Windows 10 Edge in caso di flussi DASH.</p> </td> 
   <td>La modalità di trucco del riavvolgimento non è supportata.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Analisi ID3</td> 
   <td>20346: anche il byte di codifica del testo dei fotogrammi ID3 deve essere restituito dall'SDK.</td> 
   <td><p>I tag ID3 disponibili nei flussi di trasporto dati audio (ADTS) vengono ignorati dall’SDK.</p> <p>· 12378: i metadati temporizzati dell'ID3 vengono analizzati in momenti diversi sul Flash e sul browser con supporto MSE e quindi anche il comportamento di visualizzazione sulla timeline del lettore di riferimento è diverso.</p> <p>· 19247: l’analisi ID3 non è supportata nel framework dell’interfaccia utente.</p> </td> 
   <td><p>· 20323: il tag PRIV ID3 utilizzato per segnalare la marca temporale del primo campione di un segmento AAC non viene analizzato da Safari (#32422733 problema Safari)</p> <p>· 20350: su alcuni dispositivi (tra cui MAC OS X 10.1, iPad10) Safari non fornisce l’evento di cambio del segnale quando è in modalità "trick" e di conseguenza i fotogrammi ID3 non vengono ricevuti. (#32450526 problema Safari)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto per marcatori di discontinuità</td> 
   <td> </td> 
   <td><p>· L’inserimento di annunci lato client non è supportato con flussi HLS contenenti discontinuità.</p> <p>· La modifica del codec audio non è consentita tra le discontinuità nel flusso HLS.</p> <p>· Lo switch di traccia audio non è supportato per il flusso HLS con marcatori di discontinuità</p> </td> 
   <td>Il numero di sequenza della discontinuità è un requisito per i flussi HLS con discontinuità per poter essere riprodotti su Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 18: caratteristiche di protezione dei contenuti**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>L'intervallo di byte non è supportato con contenuto crittografato AES-128.</td> 
   <td>12324: se non è specificato alcun tag IV, i flussi crittografati HLS AES-128 non vengono riprodotti su Safari.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>· 12660: il lettore HTML5 genera un errore interno del server per i contenuti scaduti del trattino crittografato PlayReady.</p> <p>· 16720: il contenuto crittografato DASH DRM non funziona se manca l’attributo start nel tag punto.</p> <p>· 18589: la riproduzione non è supportata per i flussi multi-periodo Dash VoD protetti da DRM con Xlink.</p> <p>· 18653: Riproduzione di contenuti Widevine MultiPeriod con più chiavi, si arresta al primo punto e non può passare al periodo successivo.</p> <p>· 18656: Playready MultiPeriod Stream, crittografato con chiavi diverse, non viene riprodotto.</p> <p>Playready 2.0 per Dash non è certificato.</p> <p> </p> <p> </p> </td> 
   <td>12602: i metadati DRM di HLS Fairplay vengono ripetutamente aggiornati dal lettore HTML5 su Safari</td> 
   <td><p>È possibile riprodurre il contenuto DRM widevine DASH fornito tramite Bento4. I contenuti inseriti tramite Offline Packager e Shaka Packager non vengono riprodotti. DASH DRM PlayReady non supportato.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 19: Caratteristiche principali di Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>· Gli annunci preroll con contenuti live HLS vengono riprodotti in modalità Dual player.</p> <p>· Gli annunci DASH con contenuti HLS e gli annunci HLS con contenuti DASH non sono supportati.</p> <p>· 19002: In HTML5 Player con MSE adBreak. insertionType non restituisce un valore corretto per rappresentare il tipo di inserimento corretto, ovvero client inserito e/o server inserito.</p> <p>7794: sui dispositivi mobili (iOS, Android con Chrome 33 o inferiore o Browser nativo) dove la barra di controllo predefinita è visibile in modalità a schermo intero, la barra di ricerca e i pulsanti di avanzamento rapido sono disponibili quando Ads Play.</p> <p>· 11048: il passaggio dai contenuti live dell’annuncio a quelli HLS non è ottimale in caso di estensioni di sorgenti multimediali.</p> <p>· 16083: su Android 4.4 Chrome v52, a volte gli annunci HLS con contenuto HLS possono causare un errore di decodifica della pipeline dopo la riproduzione bloccata.</p> <p>· 16097: gli errori rilevati durante l’interruzione dell’annuncio non vengono gestiti, potrebbero causare l’arresto della riproduzione del flusso principale.</p> <p>· 18095: gli annunci MP4 non sono supportati con i contenuti live HLS.</p> <p>19120: le ricerche multiple su annunci HLS con contenuti HLS possono causare l’arresto della riproduzione del flusso.</p> <p>· 19131: la sovrapposizione del buffering può apparire durante il passaggio dall’interruzione pubblicitaria pre-roll al contenuto.</p> <p>· 20296: nel caso di flussi HLS Live, il ripristino nella finestra DVR seguito da un superamento del numero di rotoli medi risolti può causare lo stallo della riproduzione.</p> <p>· 20298:I flussi HLS Live con rotoli medi si arrestano nel momento in cui il primo rotolo medio esce dalla finestra del DVR.</p> <p>· 20317: i flussi HLS Live possono bloccarsi quando si passa all’annuncio successivo o dall’annuncio al contenuto, nel caso in cui l’interruzione pubblicitaria contenga più di un annuncio.</p> 
    <ul> 
     <li>Gli annunci nella finestra DVR dei flussi HLS Live non vengono risolti.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>L’SDK non rispetta l’attributo di sequenza all’interno della risposta VMAP per VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: l’SDK non rispetta l’attributo di sequenza all’interno della risposta VMAP per VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: attributo di ripetizione VMAP non supportato.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Reimballaggio creativo</td> 
   <td> </td> 
   <td>21464: la risposta dell’annuncio viene eliminata completamente se il riconfezionamento creativo non riesce per uno degli annunci nell’interruzione pubblicitaria.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 20: Funzioni Ad Insertion avanzate (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzionalità</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo annuncio</td> 
   <td> </td> 
   <td>20056: la proprietà della tecnologia del lettore non è rilevante perché si basa sul contenuto principale che è vuoto in caso di riproduzione solo annuncio</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Criterio annuncio personalizzato</td> 
   <td> </td> 
   <td><p>· I comportamenti pubblicitari non sono supportati con annunci MP4 e contenuti MP4.</p> <p>· 13973: comportamenti di annunci personalizzati - I criteri SKIP non generano un evento completo se utilizzati con MSE.</p> <p>· 14939: i criteri di comportamento degli annunci personalizzati per saltare e saltare le interruzioni pubblicitarie non funzionano per il contenuto DASH.</p> <p>· 17131: il primo fotogramma dell’annuncio è visibile e quindi il contenuto riprende in caso di criteri per ignorare l’interruzione dell’annuncio.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Annunci per i compagni/banner/annunci cliccabili</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Gli annunci banner non sono visibili quando si utilizza il lettore di riferimento.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>· I comportamenti degli annunci non sono supportati per gli annunci VPAID.</p> <p>· 15032: gli annunci VPAID in combinazione con annunci MP4 o HLS in un’interruzione pubblicitaria non sono supportati.</p> <p>· 19001: su Android e iOS quando l’annuncio VPAID viene riprodotto con MP4 come contenuto principale, le doppie tracce audio sono udibili, una tra i contenuti principali e una tra gli annunci.</p> <p>· 20762: gli annunci VPAID non sono supportati con Picture in Picture (PIP).</p> <p>· 21172: non viene ricevuto l’evento Play complete per i contenuti VOD HLS con annunci VPAID.</p> <p>· 21173: onAdBreakCompleteEvent non viene ricevuto per contenuti VOD HLS e annunci VPAID post-roll.</p> </td> 
   <td>Il lettore passa dalla modalità normale alla modalità a schermo intero quando si passa da VPAID ad Main content e viceversa.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 21: Integrazioni**

| **Tipo di contenuto** | **Funzionalità** | **Flash** | **HTML5 in Firefox, IE, Chrome, Android Chrome** | **HTML5 in Safari, iOS Safari** | **Chromecast (solo riproduzione DASH)** |
|---|---|---|---|---|---|
| VOD + Live | Integrazione Adobe Analytics VHL |  | 19004: il tracciamento di Video Analytics non è disponibile tramite lo strumento di configurazione dell’interfaccia utente. |  |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
