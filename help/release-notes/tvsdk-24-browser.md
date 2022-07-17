---
title: Note sulla versione del browser TVSDK 2.4
description: Le note sulla versione TVSDK 2.4 per browser descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '6812'
ht-degree: 0%

---

# Note sulla versione del browser TVSDK 2.4 {#browser-tvsdk-release-notes}

Le note sulla versione TVSDK 2.4 per browser descrivono le funzioni nuove, supportate e non supportate e i problemi noti nel browser TVSDK 2.4.

## Introduzione {#introduction}

Browser TVSDK è un toolkit che consente di aggiungere funzionalità avanzate di riproduzione video, protezione dei contenuti e pubblicità alle applicazioni di lettore video basate su browser.

Il browser TVSDK 2.4 fornisce API JavaScript per creare applicazioni video basate su browser e include il supporto per la riproduzione nelle seguenti modalità:

* Solo HTML5
* HTML5 con fallback auto flash
* Flash sempre

Questa versione include le seguenti informazioni:

・ [Documentazione API TVSDK per browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

・ [Guida alla programmazione TVSDK per browser](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

・ [Guida alla migrazione a TVSDK 2.4 per 1.4 da DHLS al browser](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

・ [Conversione da browser TVSDK 2.4.6 a versione 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

・ Un’implementazione di riferimento, inclusa nella build.

>[!NOTE]
>
>*Per un elenco completo delle considerazioni sulla sicurezza per questa versione, vedere Considerazioni sulla sicurezza.

## Novità e funzionalità supportate {#what-s-new-and-supported-features}

Questa versione del TVSDK per browser fornisce nuove funzioni che è possibile utilizzare per migliorare le applicazioni video.

**Novità dell’aggiornamento 2.4.12 (Build 204)**

La seguente aggiunta è disponibile come parte dell’aggiornamento del browser TVSDK 2.4.12 (Build 204):

* L&#39;implementazione dell&#39;API del volume di AdobePSDK.MediaPlayer viene modificata per consentire la riproduzione automatica su iOS quando la riproduzione è disattivata.

・ Una nuova API, `auditudeSettings.ignoreVPAIDAds`, viene aggiunto per consentire di ignorare gli annunci VPAID ricevuti dal server Auditude . L’API non funziona per Fallback di Flash.

**Versione 2.4.11**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.11:

・ Il failover dei segmenti HLS Live è supportato per le modalità di fallback MSE e Flash.

・ Supporto per `AuditudeSettings.creativeRepackagingDomain` API è ora disponibile anche per MSE. In precedenza era supportato solo con la modalità di fallback del Flash.

・ La versione contiene correzioni per problemi critici dei clienti. Vedi *Problemi risolti* un elenco.

**Versione 2.4.10**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.10:

・ TVSDK fornisce enableLogging() per abilitare o disabilitare la registrazione. Fai riferimento a [Documentazione API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)per l&#39;utilizzo.

・ TVSDK non supporta più i capitoli predefiniti quando si utilizza Adobe Analytics. Definisci e gestisci i capitoli utilizzando l’applicazione.

・ La versione contiene correzioni per problemi critici dei clienti. Vedere *Problemi fissi *un elenco.

**Versione 2.4.9**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.9:

・ Flussi HLS VOD e Live con discontinuità temporale ma senza marcatori di discontinuità sono supportati.

・ I frame ID3 v2.4.0 sono supportati con tag video Safari per flussi HLS VOD e Live.

・ L’implementazione del caricamento sicuro degli annunci assicura che le chiamate ad server siano aggiornate per proteggere HTTP in base alla configurazione API. Per informazioni dettagliate, consulta le classi AdobePSDK.AdvertisingMetadata e AdobePSDK.ForceHttpsAdConfiguration . Questa funzione non è supportata nella modalità di fallback del Flash.

・ Le informazioni sull&#39;Ad ID e le informazioni sull&#39;estensione associate alle risposte VAST 3.0 sono ora rese disponibili all&#39;applicazione da TVSDK e possono essere utilizzate per implementare l&#39;integrazione Moat per le misurazioni dell&#39;Ad. Per informazioni, consulta API AdobePSDK.NetworkAdInfo . Questa funzione non è supportata nella modalità di fallback del Flash.

・ La classe AdobePSDK.ForceHttpsConfiguration non è più disponibile. È riuscita da

Classe AdobePSDK.ForceHttpsAdConfiguration .

・ È ora disponibile una nuova API, AdobePSDK.optimizeFlashCalls, per ottimizzare le chiamate per migliorare l’esperienza di riproduzione HLS in modalità di fallback del Flash. Questa opzione è disabilitata per impostazione predefinita.

**Novità dell’aggiornamento 2.4.8 (build 6002)**

Questo aggiornamento contiene correzioni di problemi critici per i clienti. Vedi *Problemi risolti*, per l’elenco.

**Versione 2.4.8**

I seguenti miglioramenti e aggiunte sono disponibili come parte del rilascio del browser TVSDK 2.4.8:

・ L’SDK è ora compatibile con Chrome EME e le modifiche alle best practice disponibili a partire da Chrome v58. Per ulteriori dettagli vedi [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

・ Il framework dell&#39;interfaccia utente ora supporta HLS Access DRM sul flusso di lavoro Flash, Solo annuncio e Informazioni di targeting.

・ L&#39;API setDRMAuthenticateData viene aggiunta al framework dell&#39;interfaccia utente. Per riprodurre flussi protetti con Adobe Access DRM, richiama questa API. In alternativa, è possibile specificare l’attributo drmAuthenticateData nel lettore. Vedi [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)per i dettagli.

**Versione 2.4.7**

Nella versione 2.4.7 di sono state introdotte le seguenti funzioni:

・ Aggiunta del configuratore dell&#39;interfaccia utente nel framework dell&#39;interfaccia utente

Puoi configurare il lettore in uno dei seguenti modi:

・ Utilizzo di un oggetto JSON

・ Utilizzo delle API

Per facilitare la generazione dell’oggetto JSON, il browser TVSDK fornisce uno strumento **UI Configurator **4.

In questo strumento, puoi selezionare varie impostazioni, fare clic su **Test Configuration **per verificare le impostazioni, quindi fare clic su **Scarica configurazione **per scaricare le impostazioni. Dopo aver scaricato il file, puoi passare il contenuto di questo file come oggetto JSON all&#39;API ptp.videoPlayer.

・ Aggiunta dell&#39;API MediaPlayerItemConfig al framework dell&#39;interfaccia utente

È possibile configurare tramite MediaPlayerItemConfig varie funzioni, tra cui advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscriTags, thumbnailScrubber, billingMetricsConfiguration. Per ulteriori informazioni, consulta la documentazione di AdobePSDK.MediaPlayerItemConfig nella sezione [API TVSDK per browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* [documentazione](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

Nel framework dell&#39;interfaccia utente, è stato modificato il modo in cui si trasmettono le configurazioni di rete attraverso la configurazione del lettore.

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

Le configurazioni DRM e il tracciamento di Analytics possono essere abilitati tramite l’interfaccia utente Framework.

* Aggiunta di `AdobePSDK.embedSWFinFullScreenDiv` API

Questa nuova API offre flessibilità all’app di riproduzione per selezionare il div in cui può incorporare il file FlashFallback.swf.

* Sostituito `getVersion`API da `AdobePSDK.MediaPlayer` classe con `AdobePSDK.Version` per informazioni relative alla versione TVSDK. Per maggiori dettagli, vedi `AdobePSDK.Version` API [qui](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Versione 2.4.6**

Nella versione 2.4.6 di sono state introdotte le seguenti funzioni:

* **Supporto per la ricerca**

La ricerca consente di utilizzare i moduli di stile node.js nel browser. Puoi definire le dipendenze e browserify raggruppa tutto in un file JavaScript.

* **Fatturazione**

Con l&#39;aiuto della fatturazione, Browser TVSDK può raccogliere le metriche di utilizzo del lettore per fatturare ai clienti Primetime.

>[!NOTE]
>
>L&#39;enum MediaPlayer.Events obsoleto e le costanti obsolete in Enum PSDKErrorCode sono state rimosse nella versione 2.4.6. Per ulteriori informazioni, vedi [Conversione da browser TVSDK 2.4.5 a versione 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Versione 2.4.5**

Nella versione 2.4.5 sono state introdotte le seguenti funzioni:

* **Riproduzione e annunci eventi completi**

   I flussi HLS Full Event Replay (FER) ora supportano la risoluzione degli annunci e i comportamenti degli annunci. Per abilitare questo supporto, imposta la modalità di segnalazione degli annunci su `MANIFEST_CUES` quando si crea `MediaPlayerItemConfig` oggetto.

* **Supporto di MediaView ScalePolicy**

   Gli sviluppatori di applicazioni ora possono specificare un parametro scalePolicy diverso per la visualizzazione utilizzando la proprietà scalePolicy di MediaplayerView.

* **Supporto dei contenuti anamorfici**

   La riproduzione di contenuti anamorfici è ora supportata quando si utilizza la riproduzione MSE e Flash.

* **Applicazione selettiva di`withCredentials`**

Quando `withCredentials` è impostato su true, il `Access-Control-Allow-Origin` impossibile impostare l&#39;intestazione su un carattere jolly. A seconda della risposta del server, Browser TVSDK imposterà in modo selettivo il `withCredentials` attributo. Per ulteriori informazioni su questo supporto, consulta [Documenti API TVSDK per browser](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Versione 2.4.4**

Nella versione 2.4.4 sono state introdotte le seguenti funzioni:

* **App di esempio per Chromecast**

Questa versione fornisce il supporto per un’app mittente e ricevente che dimostra la riproduzione di flussi DASH VOD e di flussi DASH Widevine con inserimento di annunci lato client.

* **Supporto di failover avanzato**

Questa versione contiene il supporto per casi di utilizzo di failover avanzati (failover di segmenti e server) per i flussi VOD HLS.

**Versione 2.4.3**

Nella versione 2.4.3, le seguenti funzioni erano nuove:

* **Tag personalizzati per DASH VOD**

   I tag personalizzati in linea (Eventi) possono essere sottoscritti e ricevuti come oggetto TimedMetadata.

* **Riproduzione di flussi senza estensioni**

   I flussi HLS e DASH senza estensioni sono ora supportati. Per il file manifesto, è necessario specificare resourceType al caricamento della risorsa. Per i segmenti e i file VTT, l’intestazione di risposta Content-Type viene utilizzata per determinare il tipo di contenuto.

**Versione 2.4.2**

Nella versione 2.4.2 sono state introdotte le seguenti funzioni:

* **Parità API**

Per un elenco completo della parità API, consulta [Guida alla migrazione a TVSDK 2.4 per 1.4 da DHLS al browser](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Supporto di Sample-AES**

   Questa versione aggiunge il supporto per la riproduzione di contenuti crittografati Sample-AES su MSE e fallback di Flash. Il requisito di ospitare contenuti AES su origine protetta su Google Chrome è stato rimosso.

* **Supporto per contenitori AAC**

   È ora supportata la riproduzione di file con estensione aac. Può trattarsi di flussi solo audio o di audio alternativo.

   >[!NOTE]
   >
   >I codec AC3 e avanzati AC3 non sono ancora supportati.

* **Riproduzione del flusso token**

I flussi HLS che vengono consegnati tramite una rete CDN (Content Delivery Network) possono a volte utilizzare token di autenticazione nelle richieste di verifica del manifesto e del segmento e possono essere forniti come parametri URL o come intestazioni di cookie. La riproduzione di tali flussi è ora supportata.

**Versione 2.4.1**

Nella versione 2.4.1, le seguenti funzioni erano nuove:

* **Framework dell&#39;interfaccia utente**

Questo framework, progettato per accelerare lo sviluppo dell’interfaccia utente per le applicazioni di lettore video basate su JavaScript, è costituito da API per includere controlli di base come riproduzione/pausa e volume e per aggiungere o rimuovere facilmente elementi come gli stati della barra di scorrimento e le impostazioni dei sottotitoli. È possibile specificare il comportamento associato ai controlli, creare controlli personalizzati e applicare lo skin all&#39;interfaccia utente del lettore. Tutto questo avviene attraverso il framework, senza la necessità di manipolare direttamente la struttura DOM.

* **Miglioramenti della riproduzione HLS per i flussi in tempo reale**

Questa versione supporta le discontinuità causate dall’inserimento di annunci. Utilizza il tag EXT-PROGRAM-DATE-TIME seguito dal tag EXT-MEDIA-SEQUENCE per eseguire la sincronizzazione tra i profili a bit rate adattivo per una riproduzione fluida.

* **Supporto VPAID 2.0**

La versione 2.0 del lettore video ad-serving interface definition (VPAID) offre agli utenti un’esperienza multimediale avanzata e consente agli editori di eseguire meglio il targeting degli annunci, tenere traccia delle impressioni degli annunci e monetizzare i contenuti video. Questa versione supporta annunci JavaScript VPAID lineari per contenuti video on demand (VOD).

* **Tag HLS personalizzati**

I flussi multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifesto. Il browser TVSDK consente di specificare e sottoscrivere altri tag e ricevere una notifica quando tali tag vengono visualizzati nel manifesto.

* **Indicatori di annunci visualizzati sulla timeline del lettore**

Questa versione supporta la visualizzazione di indicatori di annunci sulla timeline del lettore per i contenuti VOD e Live. Questo comportamento è visibile nel lettore di riferimento.

**Supportato in 2.4**

Nella versione 2.4 erano disponibili le seguenti funzioni:

* **Riproduzione audio MP3**

   Questa versione supporta la riproduzione audio MP3 sui browser con Media Source Extensions (MSE) e con il tag video Safari.

* **Riproduzione video MP4**

   Sono supportate le seguenti funzioni:

   * Riproduzione a flusso singolo
   * Annunci MP4 pre-roll e post-roll con comportamenti e tracciamento degli annunci
   * Annunci HLS pre-roll e post-roll con comportamenti e monitoraggio degli annunci
   * Annunci DASH pre-roll e post-roll con comportamenti e monitoraggio degli annunci

## Piattaforme supportate {#supported-platforms}

Il browser TVSDK ha requisiti specifici per i livelli di piattaforme e software su cui deve essere eseguito. Sono supportate le seguenti piattaforme e livelli software:

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

### Configurazioni web per dispositivi mobili {#mobile-web-configurations}

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

**Google Chromecast (seconda generazione; solo riproduzione DASH)**

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

* *Caratteristiche audio MP3 — Riproduzione core*
* *Funzioni video MP4 — Riproduzione core*
* *Funzioni video MP4 — Core Ad Insertion*

>[!NOTE]
>
>*Nelle tabelle della matrice delle funzioni riportate di seguito, un valore &quot;Y&quot; indica che la funzione è supportata nella versione corrente.*

### Caratteristiche audio MP3 {#mp-audio-features}

**Tabella 1: Riproduzione core{#table-core-playback}**

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | MP3 VOD | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

1 Il tag video TVSDK del browser non supporta lo streaming e DRM. Il supporto per codec e contenitori non è lo stesso in tutti i browser.

2 Firefox utilizza per impostazione predefinita il Flash Player per le versioni 41 o precedenti.

### Caratteristiche audio MP4 {#mp-audio-features-1}

**Tabella 2: Riproduzione core**

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Riproduzione | MP4 VOD | Riproduzione generale (riproduzione, pausa, ricerca) | Non supportato | Y | Y |

**Tabella 3: Core Ad Insertion**

| Categoria | Tipo di contenuto | Funzione | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | MP4 VOD | Pre-roll (MP4) | Non supportato | Y | Y |
| Ad Insertion | MP4 VOD | Post-roll (MP4) | Non supportato | Y | Y |

Per ulteriori informazioni sul supporto delle funzioni HLS o DASH, consulta di seguito.

## Matrice di funzioni HLS {#hls-feature-matrix}

Ecco la matrice delle funzioni per le funzioni HLS nel browser TVSDK.

* *Riproduzione HLS Core*
* *Funzioni di riproduzione avanzate HLS*
* *Funzioni di protezione dei contenuti HLS*
* *Funzioni di inserimento degli annunci principali di HLS*
* *Funzioni avanzate di inserimento annunci HLS*
* *Integrazioni HLS*

>[!NOTE]
>
>*Nelle tabelle della matrice delle funzioni riportate di seguito, un valore &quot;Y&quot; indica che la funzione è supportata nella versione corrente.*

### Funzioni HLS {#hls-features}

Sono supportate le seguenti funzioni:

**Tabella 4: Riproduzione HLS Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Bit rate adattivo</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>sottotitoli 608/708</p> </td> 
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
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Notifiche di QoS e del lettore</p> </td> 
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
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Impostazione dei parametri di controllo del buffer</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Imposta adattivo</p> <p>controlli a bit rate</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tag personalizzati</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>Audio con associazione ritardata</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Reindirizzamento 302</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 5: Funzioni di riproduzione avanzate HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Gioco A Trick</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Giocare con liscio</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
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
   <td><p>Supporto per marker discontinuità</p> </td> 
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
   <td><p>Limitazione della piattaforma</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Accesso Adobe</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 7: Funzioni di inserimento degli annunci principali di HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>Limitazione della piattaforma</p> </td> 
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
   <td><p>FER VOD</p> </td> 
   <td><p>Risoluzione degli annunci e comportamenti</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Criterio annuncio predefinito</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
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
   <td><p>Repackaging creativo (da MP4 a HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 8: Funzioni avanzate di inserimento annunci HLS**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy annuncio caricamento</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Non supportato</p> </td> 
   <td><p>Limitazione della piattaforma</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci da compagnia, annunci banner, annunci cliccabili</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
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

## Matrice di funzioni DASH {#dash-feature-matrix}

Ecco la matrice delle funzioni per le funzioni DASH nel browser TVSDK.

・ *Funzioni di riproduzione DASH Core*

・ *Funzioni avanzate di riproduzione DASH*

・ *Funzioni di protezione dei contenuti DASH*

・ *Funzioni di inserimento degli annunci core DASH*

・ *Funzioni avanzate di inserimento annunci DASH*

・ *Integrazioni DASH*

>[!NOTE]
>
>Nelle tabelle della matrice delle funzioni riportate di seguito, un Y indica che la funzione è supportata nella versione corrente.

### Funzioni DASH {#dash-features}

Sono supportate le seguenti funzioni:

**Tabella 10: Funzioni di riproduzione DASH Core**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Bit rate adattivo</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Riproduzione</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>sottotitoli 608/708</p> </td> 
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
   <td><p>Notifiche di QoS e del lettore</p> </td> 
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
   <td><p>Imposta controlli del bit rate adattivo</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Giocare con liscio</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>・ Widevine su Chrome, Firefox 47 e versioni successive e Chromecast</p> <p>・ PlayReady su Internet Explorer su Windows 8.1 e Edge</p> <p>・ Primetime DRM per Windows Firefox (solo video)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 13: Funzioni di inserimento degli annunci core DASH**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Categoria</strong></p> </td> 
   <td><p><strong>Tipo di contenuto</strong></p> </td> 
   <td><p><strong>Funzione</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/DASH)</p> </td> 
   <td><p>Solo VOD</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
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
   <td><p>FER VOD</p> </td> 
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
   <td><p>Repackaging creativo (da MP4 a DASH)</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
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
   <td><p>Lazy annuncio caricamento</p> </td> 
   <td><p>Non supportato</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Annunci da compagnia, annunci banner, annunci cliccabili</p> </td> 
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
   <td><p><strong>Funzione</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
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

I seguenti problemi sono stati risolti nell’aggiornamento del browser TVSDK versione 2.4.12 (Build 204):

・ **21647**- TVSDK dovrebbe consentire la riproduzione video automatica sui dispositivi iOS quando l&#39;audio è disattivato.

・ **21465**- Accesso chiave di errore negato durante la riproduzione di un flusso DASH protetto da DRM dopo la riproduzione di un flusso DASH Live.

・ **21442**- Abilita la riproduzione automatica dei contenuti su iOS Web, dopo che l’annuncio preroll viene riprodotto con un gesto dell’utente.

・ **21240**- API fornita per filtrare gli annunci VPAID analizzati da Auditude/VMAP.

**Problemi risolti nella versione 2.4.11**

I seguenti problemi sono stati risolti nella versione 2.4.11 del browser TVSDK:

**Funzioni di riproduzione principali:**

・ **19192**: TVSDK ora implementa TextFormat:bottomInset e TextFormat:safeArea. A causa di questi miglioramenti, i sottotitoli codificati possono essere riposizionati se la barra di controllo è visualizzata sullo schermo.

・ **21009**: I sottotitoli codificati persistono sullo schermo in caso di discontinuità nella ricerca fino a quando non vengono visualizzati nuovi sottotitoli.

・ **21141**: La richiesta di ritorno viene rifiutata a causa di una situazione di tipo &quot;race condition&quot; durante l’aggiunta del segmento.

・ **21142**: Rendere disponibili intervalli di riproduzione ricercabili quando il lettore è in stato INITIALIZED. A causa di queste modifiche, ora è supportato l’avvio della sessione in posizione .

・ **21363**: I sottotitoli codificati 608/708 non vengono sincronizzati dopo l’inserimento di annunci per i flussi DASH.

**Funzioni di inserimento annunci:**

・ **21179**: I problemi relativi alla modalità mid-roll (pause lunghe, fotogrammi neri) con contenuto VOD ora sono risolti impostando correttamente la proprietà ad.primaryAsset.adParameters .

・ **21257**: Il file MP4 con bit rate più alto viene selezionato per la transcodifica se MP4 non è un tipo di mime valido e la funzione di ricompilazione creativa è abilitata.

・ **21361**: TVSDK ora trasmette l’ID creativo e del sistema di annunci dalla risposta VAST come parametri di query nella richiesta di packaging creativo per supportare regole di normalizzazione aggiuntive.

**Problemi risolti nella versione 2.4.10**

I seguenti problemi sono stati risolti nella versione 2.4.10 del browser TVSDK:

**Funzioni di riproduzione principali:**

・ **21060**: Errore codec non valido generato con flussi HLS che contengono discontinuità e le caselle ISO BMFF vengono eseguite alla fine del flusso.

・ **21045**: La riproduzione automatica non funziona su iOS al termine della prima riproduzione video in una playlist.

・ **20975**: Il frame rate viene restituito come NaN dal provider QoS sul browser Chrome.

・ **20823**: Errore codec non supportato generato quando si incontrano segmenti senza dati.

・ **20769**: L&#39;SDK ora inizia con il bit rate corrente alla ricerca invece di passare immediatamente alla modalità in base ai criteri ABR.

・ **2003**: In modalità verticale su IE11 (Windows 8.1), la schermata video diventa piccola. Funzione di protezione dei contenuti:

・ **19316**: Salta i segmenti che non riescono a decrittografare in caso di flussi HLS AES-128.

**Problemi risolti nella versione 2.4.9**

I seguenti problemi sono stati risolti nella versione 2.4.9 del browser TVSDK:

**Funzioni di riproduzione principali:**

・ **13407**: I flussi DASH possono arrestarsi se Firefox smette di inviare l&#39;evento &quot;ontimeupdate&quot; durante la riproduzione.

・ **16380**: Durante la riproduzione di contenuti video audio a mbox di segmenti con tempi di avvio non corrispondenti tramite MSE, l&#39;errore di sincronizzazione audio tra le rappresentazioni si accumula sugli switch ABR, dando luogo in ultima analisi a un errore (problema di cromo #663686).

・ **17985**: Quando si riproduce un particolare flusso ISO-BMFF sul browser Firefox, la riproduzione si blocca (problema Firefox #1342913). Questo è stato corretto a partire da Firefox v53.

・ **19141**: ReferenceError non rilevato (nella promessa): larghezza non definita.

・ **18997, 19299**: Problema di visualizzazione momentanea di altri video al limite del segmento. Ciò si verificava poiché l&#39;SDK non calcolava correttamente l&#39;offset del tempo di composizione dell&#39;ultimo campione.

・ **19780**: La riproduzione non viene avviata per i contenuti HLS e HLS Ad su Firefox v53 (problema Firefox #354653).

・ **2004**: Data programma L’ora viene ricevuta come chiave invece che come valore quando viene ricevuta come oggetto metadati temporizzati.

・ **20047**: useDefaultResizeHandler genera un errore con il fallback del Flash.

・ **2017**: Flash Fallback non funziona con Flash Player v25.0.0.171.

・ **20293**: Firefox interrompe il buffering dei dati per alcuni flussi HLS che portano all&#39;arresto.

・ **20626**: Il lettore genera un errore di decodifica dei contenuti multimediali su Chrome a causa di una gestione non corretta dei campioni video con durata zero.

・ **2007**: La riproduzione si arresta con l&#39;errore del browser &#39;QuotaSuperata&#39;.

・ **18639**: In HLS Live Stream 608 Il testo CC a volte appare come errato.

・ **20028**: Il parametro della dimensione ClosedCaptions non modifica la dimensione del font.

・ **20613**: Le caselle sottotitoli codificati si sovrappongono tra loro, rendendole illeggibili.

**Caratteristiche di Core Ad Insertion (CSAI):**

・ **20043**: Chiamate ad impression mancanti e di tracciamento degli annunci con più annunci e reindirizzamenti di terze parti.

・ **2004**: Quando si utilizza il riconfezionamento creativo, tutti gli annunci nell&#39;interruzione pubblicitaria devono essere ricompilati con successo, altrimenti l&#39;interruzione pubblicitaria viene completamente scartata.

・ **20097**: La riproduzione dell’annuncio viene ignorata e il contenuto principale riprende immediatamente anziché attendere il timeout di 20 secondi se il manifesto dell’annuncio non è disponibile.

**Problemi risolti nell’aggiornamento della versione 2.4.8 (Build 6002)**

I seguenti problemi sono stati risolti nell’aggiornamento del browser TVSDK versione 2.4.8 (Build 6002):

・ **14126:** La riproduzione potrebbe arrestarsi su Firefox (problema #1316024) a causa di un gap interno nel buffer sorgente MSE. Provare a cercare per riprendere la riproduzione

・ **19608:** Correzione per rispettare il valore di offset temporale dalla risposta Auditude VMAP.

・ **19635:** Correzione dell&#39;arresto video in Internet Explorer 11 in Windows 10.

・ **19761:** Correzioni di problemi di ABR con HLS.

・ **19780:** Corregge la riproduzione dell’annuncio con contenuto HLS interrotto in Mozilla Firefox v53.

・ **1987 e 1974:** I problemi risolvono l&#39;incoerenza nella selezione del bitrate dopo un&#39;operazione di ricerca. Ora la selezione del bitrate sulla ricerca è il valore più basso del bitrate corrente e il bitrate all&#39;avvio-up.

・ **1981:** La riproduzione bloccata e la sovrapposizione buffering appare per un tempo infinito dopo la ricerca viene eseguita per 3-4 volte.

・ **1984:** Conferma la conformità ai requisiti di Chrome 59 Beta Verified Media Path (VMP). bTVSDK è stato in grado di riprodurre contenuti DRM Widevine con Chrome 59 Beta.

・ **19916:** Riproduzione DRM nell&#39;interfaccia utente Framework interrotta. Ora, richiama acquisitionLicense anche se non vi è alcun criterio nei metadati.

**Problemi risolti nella versione 2.4.8**

I seguenti problemi sono stati risolti nella versione 2.4.8 del browser TVSDK:

・ **10075**: Quando si cerca in anticipo sulla timeline, l’evento di completamento della riproduzione non è stato ricevuto su Firefox e Chrome e l’evento di ricerca non è stato ricevuto su Firefox.

・ **15775**: Riproduci evento completo non ricevuto su Windows 8.1 Internet Explorer.

・ **17306**: Per i flussi SSAI, la riproduzione è supportata. Il tracciamento degli annunci uniti non è supportato.

・ **19142**: A volte il riavvolgimento fa sì che il lettore video rimanga in stato di buffering per sempre.

・ **19218**: I marcatori annunci non sono disponibili tramite il framework dell’interfaccia utente.

・ **19219**: La sola riproduzione degli annunci non funziona tramite il framework dell&#39;interfaccia utente.

・ **1922**: La chiave AES-128 viene richiesta una volta per una playlist e le richieste successive vengono servite dalla cache. In precedenza veniva richiesto per ogni segmento.

・ **19597**: &quot;TypeError non rilevato: Impossibile leggere la proprietà &#39;log&#39; di undefined&quot; visualizzata con le build del canale Chrome.

・ **19605**: adRequestDomain non era disponibile in modalità di fallback del Flash.

・ **19608**: Gli annunci VMAP non venivano inseriti per i flussi HLS Live. L&#39;SDK ora considera i marcatori di cue e non si basa sui valori di offset del tempo nelle risposte VMAP.

・ **19637**: La riproduzione degli annunci porta solo a errori di script alla fine dell’annuncio.

・ **19732**: Le richieste della playlist CRS non riuscivano con errore 404. Le richieste 1401 e 1403 dal browser TVSDK sono state aggiornate per gestirle.

・ **19762**: acquisitionLicense veniva chiamata prima di setAuthenticationToken a causa della quale veniva restituita una licenza valida indipendentemente dalla validità del token. Questo problema è corretto ora e acquisitionLicense viene chiamato solo dopo la risposta setAuthenticationToken.

**Problemi risolti nella versione 2.4.7**

I seguenti problemi sono stati risolti nella versione 2.4.7 di :

・ **8397**: I flussi HLS Live generati tramite Adobe Medium Server potrebbero non essere riprodotti se i segmenti non iniziano con un frame chiave.

・ **13606**: Sono stati risolti diversi problemi relativi alla ricerca per il flusso HLS sul browser Chrome.

・ **14807**: Nel browser Chrome, se la ricerca o la pausa viene attivata immediatamente dopo play(), la riproduzione potrebbe arrestarsi con l&#39;errore DOMException: La richiesta play() è stata interrotta da una chiamata...(Problema di cromo n. 593273).

・ **19085**: I parametri MediaPlayer come volume, abrControlParameters e ccStyle non sono impostati su Valori predefiniti al momento del ripristino del lettore.

**Problemi risolti nella versione 2.4.6**

Il seguente problema è stato risolto nella versione 2.4.6 di :

・ **18093**: TimedMetadata per il tag accanto al tag di sottoscrizione viene restituito quando si utilizza la versione 24 del Flash Player in modalità Fallback del Flash.

**Problemi risolti nella versione 2.4.4**

Nella versione 2.4.4 sono stati risolti i seguenti problemi:

・ **8711**: Con MSE, le didascalie 608/708 vengono lasciate giustificate per impostazione predefinita.

・ **13934**: Le impostazioni ABR per gli annunci non sono applicabili durante la riproduzione con flussi HLS Live.

・ **14079**: La longevità dei flussi HLS Live con finestra DVR bassa potrebbe non riuscire, poiché la riproduzione potrebbe essere in ritardo a causa di problemi di latenza della rete. Fare clic sul punto attivo per riprendere la riproduzione.

・ **15037**: Gli esempi forniti con il framework dell&#39;interfaccia utente del lettore non funzionano in Microsoft Internet Explorer 10 su Windows 7.

・ **15913**: Per i flussi VOD HLS, su Chrome, il flusso non verrà riprodotto se la risposta del manifesto è 304 non modificata. Questo è stato corretto a partire da Chrome v55 (Chromium issue 633696).

・ **16103**: Su Android Chrome, in condizioni di larghezza di banda bassa, la riproduzione potrebbe arrestarsi con TypeError non rilevato: Impossibile leggere la proprietà &#39;programDateTime&#39; di un errore non definito.

・ **16265**: Per i flussi HLS VOD e Live, cercare tra le discontinuità non funziona.

・ **16709**: La ripresa del flusso HLS Live con PDT e il marcatore di discontinuità può causare il blocco del lettore nel buffering.

## Problemi noti e limitazioni {#known-issues-and-limitations}

Le limitazioni e i problemi noti nel browser TVSDK sono indicati di seguito.

**Tabella 16: Funzioni di riproduzione core**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzione</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td><p>・ I formati multimediali diversi da HLS non sono supportati.</p> <p>8799: La funzione di fallback del Flash non si occupa dei contenuti misti, pertanto è necessario garantire che Contenuto, Annuncio e altri URL non portino a contenuti misti (contenuti protetti e non protetti insieme).</p> <p>・ 19271: La riproduzione multiview tramite framework di interfaccia utente non è supportata in modalità di fallback del Flash.</p> <p>・ Il fallback del Flash non funziona su Microsoft Internet Explorer 8 e 9 su Windows 7, in quanto queste versioni non sono supportate dall'SDK.</p> <p>・ 20262: Il fallback Flash aggiunge parametri personalizzati all'elenco di informazioni sul targeting. Anche l’ordine prioritario dei parametri personalizzati è diverso nel caso di Flash e MSE.</p> <p>・ 20653:Il fallback del Flash TVSDK del browser non funziona su Win10 con Creators Update.</p> <p>・ Flash Fallback funziona con il Flash Player versione 23 e successive.</p> <p>・ 20087 - Chrome 59 Beta con</p> <p>Flash 25.0.0.171</p> <p>Beta (impostazione predefinita), la riproduzione HLS non funziona in modalità Fallback Flash. Sta funzionando bene su Canary.</p> </td> 
   <td><p>・ 12563: I Dash Streams con codec audio mp4a.40.02 non riproducono su Firefox a causa della stringa di codec audio non supportata in MPD. È supportato il codec audio mp4a.40.2.</p> <p>15029: Quando si passa da un video all’altro in multiView nell’interfaccia utente Framework, il pulsante di riproduzione/pausa non viene aggiornato di conseguenza.</p> <p>・ 16034:Su Windows 8.1 IE, la chiamata di reset() porta a un errore di tipo MIME sconosciuto. Ricaricare il supporto per riprendere la riproduzione.</p> <p>・ 18235: Alcuni problemi di ricerca sono osservati con i flussi di vod DASH con Ads.</p> <p>・ 18727: L'API di errore non è supportata per MSE</p> <p>18750: Gli eventi di modifica dello stato potrebbero non essere ordinati in alcuni casi per il framework SDK e dell'interfaccia utente e in UI Framework, gli eventi IDLE e Inizializzazione di StatusChange potrebbero mancare per gli eventi Listener aggiunti dopo il caricamento della risorsa.</p> <p>・ 18889: Se MediaPlayer è in stato ERROR, l'oggetto di visualizzazione non viene restituito.</p> <p>・ 19039: Se AdobePSDK. MediaPlayer. searchToLocal() viene utilizzato con un valore maggiore di EOF, quindi la riproduzione inizia dall'inizio in caso di MSE.</p> <p>・ 19049: Non viene segnalato alcun stato di errore per Flash Player su Chrome, IE, Firefox quando il video è bloccato durante la riproduzione.</p> <p>・ 17205: La riproduzione video si arresta durante la riproduzione di un flusso non muxed per alcune ore mentre l'audio continua a essere riprodotto (Chromium issue# 664033).</p> <p>・ 12308: I flussi DASH con composizione_ time_offset specificato possono avere timeStampOffset applicato su di esso sul browser Chrome che porta a tempo di decodifica negativo e quindi errore MEDIA_ERR_ SRC_NOT_ SUPPORTED (problema di cromo #398141).</p> <p>・ 14126: La riproduzione potrebbe arrestarsi su Firefox (problema# 1316024) a causa di un gap interno nel buffer sorgente MSE. Provare a cercare per riprendere la riproduzione.</p> <p>・ 1915: MS Edge e IE 11 (Win 8.1 e 10) non imposta Origin su null nel reindirizzamento CORS, ma non riesce perché l'intestazione non è null e causa un errore di riproduzione.</p> <p>・ 19861:Problema con il comportamento di aggiunta sul buffer di origine per i supporti già riprodotti. Chrome rifiuta il frammento aggiunto, incluso moov, causando un successivo errore di decodifica. (Emissione di cromo #735335)</p> <p>19921: La riproduzione blocca per alcuni contenuti HLS anche se il buffered è riuscito (problema di cromo #713540)</p> <p>・ 20444:La ricerca della fine dell'intervallo buffered su IE e Edge può causare l'arresto della riproduzione.</p> <p>・ 20511: A volte può essere osservato il rifiuto per i flussi HLS con o senza annunci.</p> <p>・ 20743: Su Windows 10 Chrome, lo streaming HLS Live viene riprodotto per alcuni secondi prima della riproduzione MP4 pre-roll.</p> <p>・ 21043: La dimensione video potrebbe non essere corretta al caricamento iniziale a causa della mancanza di metadati.</p> <p>・ 21115: Il gesto dell'utente Android è necessario per avviare la riproduzione se l'annuncio pre-roll è disponibile per i video in una playlist.</p> <p>・ HLS Live non supporta il rollover del timestamp.</p> <p>・ Audio AAC-SSR non supportato.</p> <p>I codec audio AC3 e Enhanced AC3 non sono supportati.</p> <p>・ Per flussi con discontinuità timestamp ma senza marcatori di discontinuità</p> <p>・ La riproduzione potrebbe avere problemi e ricerca errata a causa di salti.</p> <p>・ La durata del contenuto e la durata della riproduzione potrebbero non corrispondere.</p> <p>・ Le discontinuità tra rappresentazioni e rappresentazioni devono corrispondere ad altri saggi possono portare a problemi di sincronizzazione e stallo.</p> <p>・ Sottotitoli e WebVTT potrebbero non essere visualizzati vicino alla fine del flusso.</p> <p>・ Le modifiche del codec audio non sono supportate tra i salti di marca temporale.</p> <p>・ L'inserimento di annunci non è supportato.</p> <p>・ La modalità di avanzamento rapido può portare a loop di riproduzione su Win 8.1 IE 11 (problema MS #12446268).</p> <p>DASH:</p> <p>・ Per i flussi live - è supportato il profilo live con tipo dinamico.</p> <p>・ Per i flussi VoD: è supportato il profilo live con tipo statico.</p> <p>Per i flussi VoD - il profilo on demand non è certificato per i flussi di lavoro di annunci.</p> </td> 
   <td><p>・ I flussi DASH Live e DASH Video on Demand non sono supportati.</p> <p>・ La riproduzione video PIP (Picture in Picture) non è supportata su iOS in modalità a schermo intero.</p> <p>In Safari (Video Tag) l’estensione meno manifesto senza l’intestazione corretta del tipo di contenuto non funziona.</p> </td> 
   <td><p>・ l'ID applicazione nell'app mittente deve essere lo stesso generato durante la registrazione dell'URL del Destinatario come app del Destinatario personalizzato.</p> <p>・ Il lettore di riferimento è certificato per i flussi di lavoro DASH. Il framework dell'interfaccia utente non è certificato.</p> <p>Per un elenco dei codec multimediali supportati, consulta <a href="https://developers.google.com/cast/docs/media"><em>qui</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>Riproduzione generale (riproduzione, pausa, ricerca)</td> 
   <td> </td> 
   <td>18098: Alcuni problemi di ricerca sono osservati con HLS LBA FER stream.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Bitrate adattivo</td> 
   <td><p>・ 20079: Riscrivi buffer alla ricerca all'interno dell'intervallo buffered.</p> <p>2008: Il comportamento ABR di Flash è in linea con MSE.</p> </td> 
   <td><p>・ La variante di fallback solo audio in un flusso ABR viene ignorata a causa di limitazioni relative al buffer.</p> <p>・ 12289: I parametri di controllo ABR non si applicano per l'audio in caso di flussi HLS/DASH non muxed.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Sottotitoli 608/708</td> 
   <td> </td> 
   <td><p>・ 7810: Su Android 4.4.4 Chrome non sembra avere il supporto per le famiglie di font CSS di base utilizzate dal lettore e quindi la funzione di modifica dello stile del font non funziona.</p> <p>・ I canali CC non possono essere modificati nel caso di 608 didascalie.</p> <p>・ Le funzioni di stile avanzate non sono supportate per i sottotitoli 608.</p> <p>Sono supportati i sottotitoli incorporati (608/708), segnalati tramite il tag Accessibilità .</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>・ 5206: I tag di area nel file WebVTT vengono ignorati dal lettore durante la visualizzazione delle didascalie.</p> <p>・ DASH: I file VTT frammentati/segmentati non sono supportati.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover manifesto</td> 
   <td>21056: Con Fallback di Flash, il failover non si verifica per il flusso Live se il flusso primario restituisce un errore 404 durante la riproduzione.</td> 
   <td>Il failover manifesto è applicabile solo per il contenuto e non per gli annunci.</td> 
   <td>Il failover della playlist mancante funziona solo su Safari per il codice di errore HTTP 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Failover avanzato</td> 
   <td> </td> 
   <td><p>・ Il failover dei segmenti non supporta il mancato superamento dei segmenti non disponibili e la riproduzione continua.</p> <p>20533: I segmenti mancanti in una playlist devono essere trattati come discontinuità e la riproduzione deve riprendere dal segmento successivo disponibile.</p> <p>21267: La commutazione del flusso a causa di un failover può causare il download di segmenti meno recenti.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Notifiche di QoS e Player</td> 
   <td>21129: Il frame rate non è disponibile in caso di Fallback del Flash.</td> 
   <td><p>・ 11170:</p> <p>Timed_Event non è disponibile per il browser TVSDK con MSE a differenza del browser TVSDK con fallback del Flash.</p> <p>21129: Il frame rate non viene calcolato per i flussi in tempo reale.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto per le intestazioni dei cookie</td> 
   <td> </td> 
   <td> </td> 
   <td><p>Le intestazioni dei flag withCredentials e dei cookie non sono supportate in Safari.</p> <p>21051: Per consentire i cookie in Safari, abilita l’impostazione "Cookie e dati del sito web" da Preferenze &gt; Privacy.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Tag personalizzati</td> 
   <td>14763: I tag personalizzati diversi da quelli che iniziano con # non devono essere supportati. In questo momento l'oggetto TimedMetadata viene creato e segnalato per tali tag durante il Flash Fallback.</td> 
   <td>I flussi con tag personalizzati in banda non sono certificati.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Audio di associazione tardiva</td> 
   <td> </td> 
   <td><p>・ L'inserimento di annunci non è supportato con flussi HLS Live LBA.</p> <p>・ 17273: Lo switch di flussi LBA VOD HLS consente il rendering predefinito in caso di failover e non può essere ripristinato all'ultima selezione.</p> <p>・ 20251: Il flusso HLS Live LBA potrebbe arrestarsi alla ricerca.</p> <p>・ 20497: Il lettore rimane in stato di buffering se i flussi non muxed HLS LBA presentano fotogrammi audio o video mancanti vicino alla fine del flusso.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302 Reindirizzamento</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>l'ottimizzazione del reindirizzamento non è supportata nei browser windows Edge e IE in quanto non supportano la proprietà responseURL nell'oggetto XMLHttpRequest.</p> </td> 
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
   <td>Funzione</td> 
   <td>Flash</td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Riproduzione a offset</td> 
   <td><p>L'avvio della riproduzione con un particolare valore di offset non è supportato per i contenuti MP4.</p> </td> 
   <td>20492: Gli annunci a scorrimento intermedio prima dell'offset vengono riprodotti prima che il contenuto riprenda dal valore di offset.</td> 
   <td>La riproduzione con funzione di offset non è supportata in iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Gioco A Trick</td> 
   <td>Il Trickplay uniforme non funziona per i flussi con rappresentazioni iFrame prive.</td> 
   <td><p>・ Gli adattamenti di Trick Play non sono supportati su Firefox e Internet Explorer e quindi la modalità di gioco inversa non è disponibile su questi browser.</p> <p>・ Trickplay non è disponibile quando si riproducono contenuti insieme agli annunci.</p> <p>・ 10435: Durante la riproduzione DASH, il video si blocca durante la riproduzione di trucco in avanti su Internet Explorer (Win 8.1)</p> <p>a intermittenza. Questo sta accadendo in quanto stiamo utilizzando la proprietà playbackRate degli elementi video senza l'adattamento del gioco di trucco.</p> <p>14182: A volte, durante il riavvolgimento sul browser Chrome, l'evento di ricerca potrebbe non essere ricevuto e quindi la modalità di trucco non funzionerà.</p> <p>・ 14942: Le percentuali di riproduzione possono essere impostate su Chrome per Android anche in caso di flussi di riproduzione non trabocchetto, ma l'impostazione non verrà applicata e la riproduzione continuerà a velocità normale.</p> <p>・ 17308: La ricerca non funziona in modalità Trickplay.</p> <p>・ 17309: Nel browser Chrome, la modalità di gioco a ritroso non può essere sostenuta per più di 2 secondi.</p> <p>19272: La riproduzione dei mattoni potrebbe non essere recuperata dal buffering sul browser Windows 10 Edge in caso di flussi DASH.</p> </td> 
   <td>La modalità di riavvolgimento non è supportata.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Analisi ID3</td> 
   <td>20346: Anche il byte di codifica del testo dei fotogrammi ID3 deve essere restituito dall'SDK.</td> 
   <td><p>I tag ID3 disponibili nei flussi di trasporto di dati audio (ADTS) vengono ignorati dall’SDK.</p> <p>・ 12378: I metadati temporizzati ID3 vengono analizzati in momenti diversi del Flash e del browser con supporto MSE e quindi anche il comportamento di visualizzazione sulla timeline del lettore di riferimento è diverso.</p> <p>・ 19247: L'analisi ID3 non è supportata nel framework dell'interfaccia utente.</p> </td> 
   <td><p>・ 20323: Il tag PRIV ID3 utilizzato per segnalare la marca temporale del primo campione di un segmento ac non viene analizzato da Safari (problema Safari #32422733)</p> <p>・ 20350: Su alcuni dispositivi (tra cui MAC OS X 10.1, iPad10) Safari non fornisce un evento di cambiamento di cue quando è in modalità di trucco e quindi i fotogrammi ID3 non vengono ricevuti. (Problema Safari #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Supporto per marker discontinuità</td> 
   <td> </td> 
   <td><p>・ L'inserimento di annunci lato client non è supportato con flussi HLS contenenti discontinuità.</p> <p>・ La modifica del codec audio non è consentita nelle discontinuità del flusso HLS.</p> <p>・ Lo switch Audio Track non è supportato per lo streaming HLS con marcatori di discontinuità</p> </td> 
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
   <td><strong>Funzione</strong></td> 
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
   <td><p>・ 12660: Il lettore HTML5 genera l'errore interno del server per i contenuti crittografati PlayReady scaduti.</p> <p>・ 16720: Il contenuto crittografato DASH DRM non funziona se manca l'attributo start nel tag punto.</p> <p>・ 18589: La riproduzione non è supportata per i flussi multiperiodo DRM protetti VoD con Xlink.</p> <p>・ 18653: La riproduzione di contenuto Widevine MultiPeriod con più chiavi, si arresta al primo punto e non può passare al punto successivo.</p> <p>・ 18656: Streaming MultiPeriod Playready, crittografato con chiavi diverse, non esegue la riproduzione.</p> <p>Playready 2.0 per Dash non è certificato.</p> <p> </p> <p> </p> </td> 
   <td>12602: I metadati HLS Fairplay DRM vengono continuamente aggiornati dal lettore HTML5 su Safari</td> 
   <td><p>È possibile riprodurre contenuti DASH Widevine DRM confezionati tramite Bento4. Il contenuto confezionato tramite il Packager offline e il packager Shaka non viene riprodotto. DASH PlayReady DRM non supportato.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 19: Funzionalità di Ad Insertion core (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzione</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>・ Gli annunci preroll con contenuti live HLS vengono riprodotti in modalità dual player.</p> <p>・ Gli annunci DASH con contenuti HLS e gli annunci HLS con contenuti DASH non sono supportati.</p> <p>・ 19002: In HTML5 Player con MSE adBreak. L'oggetto insertType non restituisce il valore corretto per rappresentare il tipo di inserimento corretto, ovvero client inserito e o server inserito.</p> <p>7794: Sui dispositivi mobili (iOS, Android con Chrome 33 o versione inferiore o Native Browser) in cui la barra di controllo predefinita è visibile in modalità a schermo intero, sono disponibili i pulsanti di ricerca e avanzamento rapido quando Ads Play.</p> <p>・ 11048: Il passaggio da ad a contenuti HLS Live non è uniforme nel caso di estensioni Media Source.</p> <p>・ 16083: Su Android 4.4 Chrome v52, A volte HLS e con contenuto HLS possono portare a un errore di decodifica della pipeline dopo la riproduzione in stallo.</p> <p>・ 16097: Gli errori rilevati durante l'interruzione dell'annuncio non vengono gestiti. È possibile che il flusso principale interrompa la riproduzione.</p> <p>・ 18095: Gli annunci MP4 non sono supportati con il contenuto live HLS.</p> <p>19120: La ricerca multipla su annunci HLS con contenuti HLS può causare l'arresto della riproduzione del flusso.</p> <p>・ 19131: La sovrapposizione buffering può comparire quando si passa da pre-roll ad break al contenuto.</p> <p>・ 20296: In caso di flussi HLS Live, la ricerca di nuovo nella finestra DVR seguita dalla ricerca di rulli medi risolti può portare a un arresto di riproduzione.</p> <p>・ 20298:I flussi live HLS con rulli medi bloccano il momento primo mid roll e si sposta fuori dalla finestra DVR.</p> <p>・ 20317: I flussi HLS Live possono arrestarsi quando si passa all'annuncio successivo o dall'annuncio al contenuto nel caso in cui l'interruzione dell'annuncio contenga più di un annuncio.</p> 
    <ul> 
     <li>Gli annunci nella finestra DVR dei flussi HLS Live non sono risolti.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>L'SDK non rispetta l'attributo della sequenza all'interno della risposta VMAP per VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: L'SDK non rispetta l'attributo della sequenza all'interno della risposta VMAP per VAST adSource.</td> 
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
   <td>Repackaging creativo</td> 
   <td> </td> 
   <td>21464: La risposta dell’annuncio viene scartata completamente se il repackaging creativo non riesce per uno degli annunci nell’interruzione dell’annuncio.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 20: Funzioni avanzate di Ad Insertion (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Tipo di contenuto</strong></td> 
   <td><strong>Funzione</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (solo riproduzione DASH)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Solo annuncio</td> 
   <td> </td> 
   <td>20056: La proprietà della tecnologia del lettore non è rilevante in quanto si basa sul contenuto principale che è vuoto in caso di riproduzione solo annunci</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Criterio annuncio personalizzato</td> 
   <td> </td> 
   <td><p>・ I comportamenti degli annunci non sono supportati con annunci MP4 e contenuti MP4.</p> <p>・ 13973: Comportamenti di annunci personalizzati - La policy SKIP non genera eventi completi quando viene utilizzata con MSE.</p> <p>・ 14939: I criteri di comportamento degli annunci personalizzati saltano e saltano l’interruzione degli annunci non funzionano per il contenuto DASH.</p> <p>・ 17131: Il primo fotogramma dell’annuncio è visibile e il contenuto riprende in caso di politica di interruzione dell’annuncio SKIP.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Annunci companion / banner pubblicitari/ Annunci cliccabili</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Gli annunci banner non sono visibili quando si utilizza il lettore di riferimento.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>・ I comportamenti degli annunci non sono supportati per gli annunci VPAID.</p> <p>・ 15032: Gli annunci VPAID in combinazione con annunci MP4 o HLS in un'interruzione pubblicitaria non sono supportati.</p> <p>・ 19001: Su Android e iOS quando l'annuncio VPAID viene riprodotto con MP4 come contenuto principale, le tracce audio doppie sono udibili, uno dei contenuti principali e uno degli annunci.</p> <p>・ 20762: Gli annunci VPAID non sono supportati con Picture in Picture (PIP).</p> <p>・ 21172: L’evento Play complete non viene ricevuto per il contenuto HLS VOD con annunci VPAID.</p> <p>・ 21173: onAdBreakCompleteEvent non viene ricevuto per il contenuto VOD HLS e gli annunci VPAID post-roll.</p> </td> 
   <td>Il lettore passa dalla modalità normale alla modalità a tutto schermo quando si passa da un annuncio VPAID al contenuto principale.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Tabella 21: Integrazioni**

| **Tipo di contenuto** | **Funzione** | **Flash** | **HTML5 in Firefox, IE, Chrome, Android Chrome** | **HTML5 in Safari, iOS Safari** | **Chromecast (solo riproduzione DASH)** |
|---|---|---|---|---|---|
| VOD + Live | Integrazione Adobe Analytics VHL |  | 19004: Il tracciamento di Video Analytics non è disponibile tramite lo strumento di configurazione dell’interfaccia utente. |  |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa dell’Aiuto all’indirizzo [Informazioni e supporto per Adobe Primetime](https://experienceleague.adobe.com/docs/primetime.html) pagina.
