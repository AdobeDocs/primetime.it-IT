---
title: Note sulla versione di TVSDK 1.4 per Android
seo-title: Note sulla versione di TVSDK 1.4 per Android
description: Note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.
seo-description: Note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '7830'
ht-degree: 0%

---


# TVSDK 1.4 per Android - Note sulla versione {#tvsdk-for-android-release-notes}

Note sulla versione di TVSDK 1.4 per Android descrivono le novità o le modifiche, i problemi risolti e noti e i problemi del dispositivo in TVSDK Android 1.4.

## Nuove funzioni {#new-features}

**Versione 1.4.43**

**Proteggere il caricamento di annunci tramite HTTPS**

 Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server di annunci primetime e al CRS attraverso HTTPS.

**alwaysUseAudioOutputLatency(valore booleano) nella classe MediaPlayer**

Quando questo parametro è impostato, utilizzate la latenza di output audio nel calcolo della marca temporale audio.

Accetta un valore di parametri booleani. Se il valore è `True`, il client utilizza la latenza di output audio nel calcolo delle marche temporali audio.

**Versione 1.4.42**

**Inserimento parziale di annunci pubblicitari:esperienza**
televisiva di partecipare al centro di un annuncio senza attivare il tracciamento per l&#39;annuncio parzialmente guardato.
Esempio: L&#39;utente si unisce al centro (a 40 secondi) di un annuncio pubblicitario di 90 secondi composto da tre annunci da 30 secondi. Questo è 10 secondi dopo il secondo annuncio nell&#39;interruzione.
* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori annunci per l&#39;annuncio parziale riprodotto (secondo annuncio) non vengono attivati. I tracciatori solo per il terzo annuncio vengono attivati.

**Versione 1.4.41**

Nessuna nuova funzionalità.

**Versione 1.4.40**

Nessuna nuova funzionalità.

>[!NOTE]
>
>Se utilizzi una versione precedente alla 1.4.39, non avrai bisogno delle modifiche alle API.

**Versione 1.4.39**

* TVSDK è certificato con VHL 2.0.1 e con VHL 2.0.1 con Nielsen.
* Android TVSDK viene aggiornato per effettuare richieste CRS dal nuovo host Akamai `primetime-a.akamaihd.net`.
* La nuova configurazione del nome host consente la distribuzione delle risorse CRS sia tramite HTTP che HTTPS (SSL) su scala maggiore.
* TVSDK supporta la versione Android Open.
* Alla classe `AdClientFactory` viene aggiunta una nuova funzione per supportare la registrazione di più Rilevatori opportunità:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   Deve restituire un array di PlacementOpportunityDetector. Ora potete registrare più Rilevatori opportunità. Ad esempio, per la funzione di uscita anticipata e uscita, erano necessari due rilevatori opportunità: uno per l’inserimento di annunci e l’altro per l’uscita anticipata dall’annuncio. L&#39;implementazione di questa nuova funzione ha un impatto solo se avete implementato la vostra AdvertisingFactory (e non utilizzate DefaultAdvertisingfactory). Per ottenere il comportamento esistente, è necessario creare un singolo Rilevatore opportunità, come nella funzione createOpportunityDetector() e inserirlo in un array e restituire:

   ```
   public class MyAdvertisingFactory extends AdvertisingFactory {  
   …  
   @Override  
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
   return opportunityDetectors;  
   } }
   ```

>[!NOTE]
>
>Se utilizzi una versione precedente alla 1.4.39, non avrai bisogno delle modifiche alle API.

**Versione 1.4.36**

Correzione di bug per Salta contenuto su Android.

**Versione 1.4.35**

* **Informazioni annuncio di rete**

   Le API TVSDK ora forniscono informazioni aggiuntive sulle risposte VAST di terze parti. Ad ID, Ad System e VAST Ad Extensions sono forniti nella classe NetworkAdInfo accessibile tramite la proprietà networkAdInfo su una Ad Asset. Queste informazioni possono essere utilizzate per l&#39;integrazione con altre piattaforme di Ad Analytics come **Moat Analytics**.

**Versione 1.4.31**

**Supporto multi-CDN per annunci CRS**
* Per impostazione predefinita, tutte le risorse transcodificate saranno ospitate  CDN di proprietà del Adobe su Akamai. Con la versione più recente,  Adobe Creative Repackaging Service (CRS) consente di caricare i creativi transcodificati in più CDN, come specificato dal cliente.
* Nuove API vengono aggiunte a TVSDK per abilitare la specifica dell&#39;URL creativo CRS finale quando l&#39;URL predefinito non è utilizzato. Per informazioni sull&#39;utilizzo di queste nuove API, consultate la documentazione.

**La versione 1.4.18**
Primetime Android TVSDK ora supporta i creativi Javascript VPAID 2.0 per consentire un&#39;esperienza pubblicitaria interattiva avanzata. Per ulteriori informazioni su VPAID 2.0, vedere [Supporto per annunci VPAID](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Versione 1.4.17**

AC-3 5.1 è supportato solo su  Amazon FireTV.

**Versione 1.4.11**

* **Ad Fallback, concatenamento margherita nella logica di selezione degli annunci (Zendesk #3103** Per annunci VAST (creativi) con la regola di fallback abilitata, TVSDK tratta un annuncio con un tipo MIME non valido come annuncio vuoto e tenta di utilizzare gli annunci di fallback al suo posto. Potete configurare alcuni aspetti del comportamento di fallback.

Per ulteriori informazioni, consultate [Ad fallback for VAST and VMAP ads](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md) (Annunci di fallback per VAST e VMAP annunci).

* **Video Heartbeats Library (VHL) aggiornato alla versione 1.5**
   * Possibilità di inviare i metadati con inizio video e/o inizio video/ad/capitolo come dati contestuali
   * Meno traffico di rete - I battiti cardiaci sono meno in media e di dimensioni più piccole

**Versione 1.4.7**

* **Supporto per l&#39;** individuazione localeSupporto per le installazioni aziendali interne del server di Individuazione del Adobe  per personalizzare la richiesta di individualizzazione del client per passare a un endpoint diverso.

**Versione 1.4.6**

* **Cifratura AES di esempio (richiede la versione di Flash Player 17.0.0.134)**È ora supportata la crittografia AES basata su campione.

**Versione 1.4.2**

* **Video Heartbeats Library (VHL) aggiornamento alla versione 1.4.0.1**

   * Aggiunta la possibilità di raggruppare diversi casi di utilizzo di analisi, da altri SDK o lettori, con  Adobe Analytics Video Essentials.
   * Il tracciamento degli annunci è stato ottimizzato rimuovendo i metodi trackAdBreakStart e trackAdBreakComplete. L’interruzione dell’annuncio viene ricavata dalle chiamate dei metodi trackAdStart e trackAdComplete.
   * La proprietà playhead non è più necessaria per il tracciamento degli annunci.

* **Nielsen SDK** IntegrationTVSDK ora supporta l’invio di informazioni di tracciamento utenti all’SDK Nielsen senza alcuna integrazione personalizzata.

**Versione 1.4.0**

* **Segnalazione di blackout con** sostituzione di contenuti alternativiCome parte dell’aggiornamento TVSDK 1.4, TVSDK ora supporta anche l’accesso e la restituzione dai blackout regionali rispetto ai contenuti lineari. Il TVSDK ora può elaborare due file manifest in parallelo, principale e alternativo, per monitorare i segnali di blackout anche quando la programmazione alternativa viene mostrata al posto della programmazione originale.

* **Rimuovi/Sostituisci** Ads C3Now, non è necessario alcun lavoro di preparazione aggiuntivo per inserire dinamicamente nuovi annunci nelle risorse video-on-demand (VOD) che escono dalla finestra C3. TVSDK fornisce ora un&#39;API per rimuovere intervalli di contenuto personalizzati e inserire nuovi annunci in modo dinamico. Questa nuova potente funzionalità è utile anche nei casi in cui i contenuti live/lineari vengono inviati in onda durante la trasmissione e immediatamente ridotti per essere utilizzati come contenuti on demand senza il tempo necessario per &quot;pulire&quot; la risorsa.

* L&#39;interfaccia PlaybackEventListener dispone di un nuovo metodo denominato onReplaceMediaPlayerItem, che è possibile utilizzare per ascoltare un nuovo evento, `ITEM_REPLACED`. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita in MediaPlayer. L&#39;applicazione client che implementa questo oggetto PlaybackEventListener deve implementare o ignorare questo nuovo metodo.
* AdClientFactory ha una nuova funzione aggiunta alla classe per registrarsi per più Rilevatori opportunità:

   ```
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
   
   For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
   
   To override this new function create a single Opportunity Detector, and put into an array and return:
   
   @Override
   
   public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
   
   List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
   
   opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
   
   return opportunityDetectors;
   }
   
   }
   ```

## Modifiche TVSDK per 1.4 {#tvsdk-changes}

* L’interfaccia PlaybackEventListener dispone di un nuovo metodo denominato onReplaceMediaPlayerItem, che consente di ascoltare un nuovo evento ITEM_REPLACED. Questo evento viene inviato ogni volta che un&#39;istanza MediaPlayeritem viene sostituita in MediaPlayer. L&#39;applicazione client che implementa questo oggetto PlaybackEventListener deve implementare o ignorare questo nuovo metodo.

* AdClientFactory ha una nuova funzione aggiunta alla classe per registrarsi per più Rilevatori opportunità:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

Ad esempio, per la funzione di uscita anticipata e in uscita, sono necessari due Rilevatori opportunità, uno per l’inserimento di annunci e l’altro per l’uscita anticipata dall’annuncio.

Per ignorare questa nuova funzione, create un singolo Rilevatore opportunità, quindi inserite in un array e restituite:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Certificazione e supporto dei dispositivi in 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>Le seguenti funzionalità sono **non** supportate nel TVSDK:
>
>* Slow motion, su qualsiasi piattaforma o versione.
>* Giochi di trucchi dal vivo.


**Versione 1.4.43**

TVSDK 1.4.43 è stato certificato con dispositivi Android con Android 6.0.1/ 7.0 e 8.1 (Oreo).

* **Versione 1.4.23:**

   * TVSDK 1.4.23 è stato certificato per dispositivi Android con Android N.

* **Versione 1.4.18:**

   * Primetime è stata certificata per  Amazon Fire TV.
   * VPAID 2.0 è supportato solo sui dispositivi con Android 4.0 e versioni successive.

## Risolti i problemi in 1.4 {#resolved-issues-in}

>[!NOTE]
>
>Tutti i clienti TVSDK che utilizzano CRS sono invitati ad effettuare l&#39;aggiornamento a TVSDK 1.4.39 o versioni successive su iOS e Android. Questo aggiornamento sostituisce l&#39;implementazione dell&#39;app esistente. Dopo l&#39;aggiornamento, verificate che CRS richieda URL creativi in uno strumento proxy (ad esempio, Charles) per verificare che la versione nel percorso rifletta la versione 3.1. Ad esempio:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Versione 1.4.43**

* Biglietto #27143 - Impossibile riprodurre la traccia audio 5.1 sui dispositivi FireTV

   * TVSDK è ora in grado di riprodurre audio AC3 su dispositivi FireTV. La riproduzione è sempre in stereo.

* Ticket #33902 - Consegna pubblicitaria sicura tramite HTTPS

   *  Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata a server di annunci primetime e CRS attraverso https.

* Biglietto #34493 - Ritardo audio Bluetooth

   * È stato aggiunto `alwaysUseAudioOutputLatency` nella classe MediaPlayer che, se impostata, determinerà l&#39;utilizzo della latenza di output audio nel calcolo delle marche temporali audio.

* Ticket #34949 - Nuova versione della libreria heartbeat video (VHL) integrata.

**Versione 1.4.42 (1791)**

* Zendesk #33719: FireTV a 4k bitrate adattivo viene ridimensionato lentamente. È stato aggiunto il supporto per ABR per dispositivi FireTV 4K.
* Zendesk #33338:  resetDRM cancella tutti i dati dell&#39;applicazione.  Sono stati gestiti casi aggiuntivi in cui le eccezioni nei thread non TVSDK causavano la compilazione delle code dell&#39;operazione TVSDK.

**Versione 1.4.41 (1776)**

* Zendesk #33002 - Dati delle risorse Companion da TVSDK su Fire TV. È stata implementata una nuova classe AdBannerAsset che restituirà i dati Companion come Elenco &lt;AdBannerAsset> e AdAsset::id ora è un oggetto String anziché long.
* Zendesk #32821 - Il lettore Android Primetime si blocca quando incontra la marca temporale della presentazione (PTS) per WWE. Questo problema è stato risolto in questa versione.
* Zendesk #33572 - VideoAnalyticsProvider Ad Start Crash. Questo problema è stato risolto grazie alla combinazione corretta della versione SDK congiunta VHL+Nielsen di VideoHeartbeat.jar.
* Zendesk #33355 - Tv antincendio: Scorri indietro di 15 secondi. Nessuna correzione da parte di TVSDK e del cliente ne sta verificando la conformità alla parte finale e terza.

**Versione 1.4.40 (1764)**

* Zendesk #33068 -  problema di sincronizzazione labbro Amazon sul nuovo dispositivo. È stato corretto un problema di sincronizzazione labbra in questa release.
* Zendesk #32215 - Android TVSDK 1.4.38 Problemi di sicurezza `[Hotlist]`. Aggiornati alla versione più recente di OpenSSL-1.1.0 e curl-7.55.1.
* Zendesk #32920 - Schermo vuoto all&#39;interno di un&#39;interruzione pubblicitaria e nessun completamento interruzione annuncio. È stato risolto un problema per il quale un contenitore VPAID poteva trovarsi in uno stato sospeso e gestiva un problema per cui gli annunci VPAID Facebook spesso restituivano più blocchi CDATA in un singolo \&amp;lt;AdParameters\&amp;gt; Nodo VAST.

**Versione 1.4.39 (1744)**

* Zendesk #28976 - La richiesta di licenza richiede più di un secondo. Mentre sono in esecuzione le chiamate di richiesta di licenza DRM che utilizzano POST, Curl aggiunge &quot;Aspettate: 100 continue&quot;. È stata rimossa l’intestazione &quot;Expect:&quot; in TVSDK.
* Zendesk #27707 - Gli ambienti CSAI che non rispettano i marcatori CUE IN per un ritorno anticipato o un ritorno ai contenuti. Supporto per più generatori di opportunità.

**Versione 1.4.38 (1722)**

* Zendesk #21590 - Prestazioni video e monitoraggio nelle ultime build di origine

Integrazione e certificazione di VHL 2.0 in TVSDK per ridurre la barriera nell&#39;implementazione di VideoHeartbeatsLibrary riducendo la complessità delle API.

* Zendesk #29688 - Supporto per i clienti Android O Beta.

Supporto TVSDK per la nuova versione Android Beta.

**Versione 1.4.36 (1713)**

* Zendesk #27392 - Salta dei contenuti su Android

Per contenere la decrittazione, Android TVSDK stava ampliando erroneamente l&#39;intervallo di byte del contenuto non iframe di 16 byte. L&#39;ampliamento è necessario per i flussi Iframe, ma non per i flussi non iframe.

**Versione 1.4.34 (1702)**

* Zendesk #27638 - Errore nell&#39;oggetto cURL INet

L&#39;oggetto POsix cURL INet presentava una perdita mentre si teneva il gestore condivisione e la cache DNS utilizzata nelle connessioni cURL.

Questo problema è stato risolto eliminando l&#39;oggetto INet Posix cURL dal decostruttore INet.

**Versione 1.4.33 (1694)**

* **Libreria OpenSSL**

La libreria OpenSSL è stata aggiornata con OpenSSL versione 1.0.2j.

* Zendesk #21701 - Inviate l’URL creativo originale per la richiesta CRS 1401 invece dell’URL normalizzato.
Questo problema viene risolto inviando gli URL creativi originali.

* Zendesk #25023 - Riproduzione video di lunga durata: fermo video, sfarfallio dello schermo
Questo problema è stato risolto impostando le dimensioni massime del formato video per i dispositivi set-top box CenturyLink.

* Zendesk #27460 - Il nuovo account Akamai non è in grado di gestire una richiesta di POST cdn.
Il codice è stato aggiornato in modo da rendere la richiesta di annuncio `cdn.auditude.com` GET invece di POST.

* Zendesk #28245 - Lo stato di riproduzione non viene notificato correttamente quando l&#39;app va dallo sfondo al primo piano
Questo problema è stato risolto ripristinando correttamente lo stato di riproduzione per la riproduzione o la pausa quando l’applicazione torna in primo piano.

**Versione 1.4.32 (1682)**

* Zendesk #25779 - Vulnerabilità di sicurezza rilevata con TVSDK
Android 4.2 e versioni successive presentano una vulnerabilità di sicurezza quando JavaScript è abilitato in una visualizzazione Web. L&#39;utilizzo di WebView da parte di TVSDK è stato disattivato per i dispositivi con sistema operativo 4.2 o inferiore. In questo modo viene disattivato l&#39;uso di annunci VPAID in TVSDK su questi dispositivi.

* Zendesk #26890 - Problema di utilizzo dello schermo (ON/OFF) Lettore
Quando il motore video  Adobe (AVE) riprende da uno stato SOSPESO, DefaultMediaPlayer non ne aggiorna lo stato. Di conseguenza, DefaultMediaPlayer rimane in stato SOSPESO anche se l’AVE è in stato di riproduzione. Questo problema è stato risolto impostando lo stato DefaultMediaPlayer su PLAYING quando viene ricevuto uno stato PLAY dall&#39;AVE, anche se lo stato corrente di DefaultMediaPlayer è SOSPESO.

**Versione 1.4.31 (1675)**

* Zendesk #21974 - Eccezioni dovute a oggetti nulli
   * AdIndex viene raramente incrementato se null. Ciò potrebbe essere dovuto a chiamate API non corrette ricevute per pre-roll adBreak. Sono stati corretti i tipi di dati per evitare tali eccezioni

* Zendesk #24714 - Disattivazione della registrazione estranea
   * Aggiornato TVSDK per disattivare la registrazione estranea

* Zendesk #24488 - Problemi di sincronizzazione AV su Fire TV
   * Risolto migliorando la gestione dei thread di decodifica AV. In modo specifico, ogni volta che vengono modificate le code dei fotogrammi di input o di output, viene eseguito il thread di decodifica specifico per il tipo di contenuto della cornice.

* Zendesk #26551 - Correggere i guasti del CRS
   * Quando la richiesta è HEAD (http head), non è necessario leggere il contenuto perché è vuoto. Mentre è ok provare a leggerla, Android precedente (4.0.x) si blocca mentre chiamiamo read() e Android più recente restituisce il valore corretto (-1) quando chiamiamo read(). In base a questo, il codice è stato modificato in modo da non leggere il contenuto per &quot;head&quot;

* Zendesk #26696 Null Puntatore Eccezione durante l&#39;accesso a TrickPlayManager
   * È stato corretto controllando se l&#39;oggetto TrickPlayManager non è null prima di utilizzarlo.

**Versione 1.4.30 (1659)**

* Zendesk #22675 La durata delle risorse non viene aggiornata per i flussi live/lineari
Questo problema è stato risolto fornendo una nuova API, assetDuration, in PTVideoAnalyticsTrackingMetadata che fornisce la durata della risorsa per i flussi live e lineari.

* Zendesk #25853 Perdita di memoria in TVSDK quando si cambiano i canali
È stato risolto il problema per cui un buffer di lettura del file veniva perso quando MediaPlayer veniva reimpostato o rilasciato durante il download di un file.

**Versione 1.4.29 (1653)**

* Zendesk #21200 - Il lettore non si riprende dallo stato sospeso quando l&#39;app era in background
Quando il lettore è stato sospeso dopo la segnalazione dell&#39;interruttore del flusso, la risoluzione consente al lettore di eseguire l&#39;interruttore del flusso durante il ripristino dello stato di sospensione, invece di ripristinare la posizione precedente.

* Zendesk #23412 - Il giocatore è bloccato con una casella nera se si fa clic su un Annuncio negli ultimi 3 s dell&#39;interruzione annuncio
Questo problema è lo stesso di Zendesk #21200.

* Zendesk #23616 - Skipped ad break cerca troppo in futuro
A seconda del tipo di inserimento annuncio (inserimento/sostituzione), TVSDK determina se la durata dell&#39;annuncio viene utilizzata nel calcolo per determinare il punto finale dell&#39;interruzione annuncio.

* Zendesk #25078 - Perdita di memoria DRM TVSDK su Android TV STB
La perdita di memoria per l&#39;oggetto adattatore DRM è stata individuata e corretta.

* Zendesk #25067 - Arresto anomalo in VideoEngineTimeline
Ciò accade perché gli oggetti non sono stati puliti correttamente e gli eventi sono stati richiamati dopo la distruzione degli oggetti. Il problema è stato risolto mediante l&#39;aggiunta di controlli per evitare eccezioni null.

* Zendesk #25352 - Imposta intestazione HTTP personalizzata
Questo problema è stato risolto aggiungendo una nuova intestazione personalizzata al elenco consentiti  su TVSDK.

* Zendesk #25617 - Il rollover PTS del flusso live causa la discontinuità del lettore e l&#39;arresto della memoria
Questo problema è stato risolto aggiungendo una gestione di rollover PTS in FragmentalHTTPStreamer quando si verifica un rollover al centro di un segmento.

**Versione 1.4.28 (1637)**

* Zendesk #23618 - Eventi di interruzione pubblicitaria attivi prima che venga consultata la politica di annunci
Questo problema è stato risolto non attivando gli eventi AD_BREAK_START e AD_START quando l&#39;annuncio viene ignorato a causa di adPerdono. L&#39;evento AD_BREAK_SKIPPED viene inviato.

**Versione 1.4.27 (1631)**

* Zendesk #23174 - Problema di prestazioni durante il ridimensionamento del video
Questo problema è stato risolto dimostrando una nuova API, MediaPlayerView.setSurfaceFixedSize, che consente a TVSDK di accedere a SurfaceHolder.setFixedSize() da MediaPlayerView.

* Zendesk #24450 - TVSDK effettua richieste pubblicitarie duplicate
Questo problema si verificava quando il tempo trascorso era stato convertito in un tempo lungo e non doppio e questo problema era stato risolto.

**Versione 1.4.26 (1627)**

* Zendesk #21436 - Aggiornamento della libreria OpenSSL alla versione 1.0.2h Aggiornata la libreria OpenSSL a OpenSSL versione 1.0.2h
* Zendesk #23825 - I cookie non vengono inclusi nelle callback Corrette fornendo il supporto per i cookie android.

**Versione 1.4.25 (1620)**

* Zendesk #22900 - Lo streaming DRM  Adobe Primetime live non viene riprodotto sul lettore di riferimento Android
Il problema di allocazione della memoria è stato risolto.
* Zendesk #23176 - Arresto anomalo dell&#39;applicazione durante il tentativo di riprodurre annunci VPAID
L&#39;arresto anomalo si è verificato perché l&#39;applicazione non crea una visualizzazione annunci personalizzata per il rendering di un annuncio VPAID. Questo problema è stato risolto ignorando gli annunci VPAID nella risposta del server di annunci in assenza di una visualizzazione annunci personalizzata.

* Zendesk #23153 - SampleAES DRM Stream - Arresto della riproduzione nel lettore di riferimento TVSDK
Questo problema è lo stesso di Zendesk #22900.

**Versione 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Attivazione di contenuti completi per transizioni video live
Questo problema è stato risolto aggiungendo un’API (trackVideoComplete) per attivare manualmente il completamento del contenuto durante una sessione di tracciamento video live/lineare.

* Zendesk #21977 VideoEngineArresto anomalo della timeline durante il funzionamento di placeAdBreak/AcceptAd
   * In questo problema, sono state aggiornate le seguenti librerie:
      * Libreria AdobeMobile alla versione 4.10.0
      * Libreria VHL alla versione 1.5.6
      * Libreria VHL-Nielsen alla versione 1.6.7

Questo problema è stato risolto aggiungendo un controllo null prima di aggiungere annunci all&#39;elenco di annunci accettati.

* Zendesk #22313 Il bitrate per gli STB con chipset Amilogic non supera 1,2 M
Questo problema è stato risolto precaricando le funzionalità dei codec multimediali e disabilitando lo switch senza soluzione di continuità per i dispositivi chipset Amilogic.

* Zendesk #19520 La risorsa AES HLS di esempio non viene riprodotta nei lettori TVSDK
Questo problema è stato risolto gestendo più descrittori PMT per flussi HLS crittografati AES di esempio.

**Versione 1.4.23 (1602)**

* Zendesk #18852 - Aggiornare la logica di selezione creativa in base alle regole CRS
Questo problema è stato risolto aggiungendo un file di configurazione JSON per specificare la priorità di selezione creativa.

* Zendesk #20861 - Android N
Questa release fornisce supporto per Android N rimuovendo la capacità di utilizzare direttamente le librerie native della piattaforma Android che non sono più accessibili alle applicazioni che vengono eseguite su Android N.

* Zendesk #21018 - Android N crash
Stessa risoluzione di ZD# 20861.

* Zendesk #21266 - L&#39;adattatore VideoEngine si blocca in caso di errore Invalid_Key
L&#39;errore Invalid_Key non include una descrizione da AVE, pertanto l&#39;analisi del testo risultava in NPE. Il problema è stato risolto aggiungendo un controllo null per la descrizione durante onError prima di analizzare la descrizione.

* Zendesk #22286 - La libreria nativa continua a allocare la chiave di lettura della memoria/frammento causando un arresto anomalo
Questo arresto anomalo che si verificava su Android quando si tentava di caricare un manifesto con più chiavi contemporaneamente è stato risolto.

**Versione 1.4.22 (1581)**

* Zendesk #17236 - Tempo inaffidabile per la testina di riproduzione per i video HLS con DRM
È stato corretto il salto temporale con i flussi LBA, dove l&#39;ora di inizio del segmento audio non corrisponde all&#39;ora di inizio del segmento video.

* Zendesk #17680 - La riproduzione video si blocca sulla casella di selezione Andredo
Il decodificatore video su questo dispositivo a volte restituisce un significativo salto nel tempo di output durante la decomposizione del fotogramma video dal buffer di output, e questa marca temporale di output rimane alta. Questo problema è stato risolto restituendo un errore *profilo video non supportato* che non obbliga il lettore a ripetere lo stesso profilo o a scegliere un profilo diverso.

* Zendesk #19074 - Fermo video durante il gioco di trucchi FFWD e REW
Questo problema è stato risolto aggiungendo un nuovo avviso TRICKPLAY_ENDED_DUE_TO_ERROR per notificare all’applicazione che trickplay è uscito e che il video è stato messo in pausa a causa di un errore irreversibile.

* Zendesk #19574 - TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM
Questo problema è stato risolto nei seguenti modi:

* Zendesk #19986 - Comportamento OP interrotto per alcuni dispositivi come Android TV
* Aggiunta di un errore FILE_NOT_FOUND alla condizione.
* Quando l&#39;errore proviene da un errore *file non trovato*, separando l&#39;URL e la risposta dalla descrizione dell&#39;errore, se la risposta è disponibile.
L&#39;errore logico introdotto dal supporto OP per lo scudo NVidia è stato risolto. Sui dispositivi di protezione non NVidia, considerare affidabili i flag di protezione visualizzati anche quando il tipo di visualizzazione è sconosciuto.

* Zendesk #20549 - Gestione di playlist obsolete. Questo problema è stato risolto riducendo l&#39;intervallo tra l&#39;aggiornamento del manifesto live alla metà della durata prevista del segmento, se il recupero precedente non riceve nuovi segmenti.

* Zendesk #20742 - L&#39;utilizzo della memoria sembra continuare ad aumentare durante la riproduzione di contenuti live su FireTV. L&#39;arresto anomalo è causato dalla tabella di riferimento dell&#39;oggetto JNI che ha raggiunto il limite. Questo problema è stato risolto eliminando il riferimento all&#39;oggetto MediaFormat creato durante il riavvio del decoder.

* Zendesk #21125 - Ritorno dall&#39;annuncio live/lineare all&#39;inizio (CSAI). È stata aggiunta una funzione che consente al lettore di tornare al contenuto principale durante un&#39;interruzione pubblicitaria se il lettore registra la giunzione in segnali pubblicitari utilizzando la giunzione nel rilevatore di opportunità.

* Zendesk #21334 - Valore di timeout della richiesta TVSDK per richieste di annunci di terze parti. Un&#39;impostazione adRequestTimeout è stata aggiunta a AdvertisingMetadata che consente un timeout globale per la chiamata dell&#39;annuncio.

**Versione 1.4.21 (1566)**

* Zendesk #17781 - La schermata ADB non funziona più
Questo problema è stato risolto aggiungendo l&#39;API DefaultMediaPlayer.create(Context context, boolean secureSurface), che consente l&#39;acquisizione dello schermo.
Per consentire l&#39;acquisizione dello schermo, trasmettere false per secureSurface.
Importante: È consigliabile non abilitare questa funzione di acquisizione dello schermo in un&#39;impostazione di produzione.

* Zendesk #19074 - Fermo video durante il gioco di trucchi FFWD e REW
Sono stati risolti i seguenti problemi che si verificavano quando il truccoPlay poteva bloccarsi nella riproduzione:

* Zendesk #19532 - La didascalia chiusa appare fuori ordine
   * FHS avvia la riproduzione del trickplay, ma il primo segmento iframe non aveva un frame al suo interno.
   * Durante il download di un segmento iframe, se FHS raggiunge una condizione di errore, esce dal trickplay e mette in pausa la riproduzione.
   * L&#39;implementazione di Android MediaCodec attende per sempre la disponibilità della coda di input mentre gli è stato chiesto di cancellare tutti i buffer di ingresso/uscita.
Questo problema è stato risolto invertendo l&#39;ordine dei suggerimenti WebVTT in modo che più suggerimenti sovrapposti risultino &quot;scorrere verso l&#39;alto&quot;.

* Zendesk #19574 - TVSDK non restituisce i dati di risposta M3U8 per il contenuto DRM o non DRM
Nel caricamento iniziale del file manifesto in PTMediaPlayerItem.PreparateToPlay, se il caricamento non riesce, TVSDK non segnala il corpo della risposta di errore all’applicazione.
Questo problema è stato risolto consentendo al TVSDK di segnalare la risposta di errore come un errore all&#39;applicazione.

* Zendesk #19701 - Congelamento della riproduzione con SAP/Discontinuità
Il lettore si blocca quando l&#39;audio e il video non sono allineati alla discontinuità è stato risolto.

* È stato corretto il bug #PTPLAY-11162 - Aggiornamento della libreria OpenSSL alla versione 1.0.2f.

**Versione 1.4.20 (1546)**

* Zendesk #17384 - Richiesta di funzioni: Supporto di metadati ID3 per la riproduzione AAC
Il supporto per i tag ID3 nei supporti AAC è stato fornito in TVSDK per Android a partire dalla versione 1.4.20.

* Zendesk #18358 - Il lettore blocca l&#39;interruttore del bitrate con discontinuità fuori sincronizzazione
Questo problema è stato risolto gestendo in modo appropriato i casi limite ABR.

* Zendesk #19232 - L&#39;app che utilizza TVSDK 1.4.18 si comporta in modo strano sulla precedente  Amazon OS versione 4
Questo problema è stato risolto rimuovendo la creazione della visualizzazione Web nascosta nel processo di inizializzazione del lettore TVSDK per evitare conflitti con i dispositivi che non supportano Android Webview.

* Zendesk #19585 - Riproduzione slow motion in caso di transizione con bitrate adattivo.
Durante lo switch ABR, se il nuovo profilo ha una frequenza di campionamento audio diversa dal profilo corrente, la riproduzione diventa veloce o slow motion. Questo perché al relatore video non viene notificato che il formato audio è cambiato.
Questo problema è stato risolto verificando che il flag di notifica sia impostato nella posizione corretta.

* Zendesk #19683 - Riproduzione SAP DAI - Nessun audio per pochi secondi.
Per diversi casi nella logica di TVSDK, quando la marca temporale di due segmenti di rappresentazioni è stata confrontata, RENDITION_TIMEOUT_THRESHOLD è stato utilizzato come intervallo di valori accettabile, perché la marca temporale non sempre corrisponde a una differenza di 0 ms. Se lo spazio vuoto è compreso nell&#39;intervallo di RENDITION_TIMEOUT_THRESHOLD, si suppone che si tratti di una corrispondenza.

RENDITION_TIMEOUT_THRESHOLD è stato impostato su 100 ms, ma si è scoperto che era insufficiente per alcuni flussi. Questo problema è stato risolto aumentando il RENDITION_TIMEOUT_THRESHOLD a 200 ms.

* Zendesk #19699 - Il TVSDK non passa tra le tracce dei sottotitoli VTT
Questo problema è stato risolto creando il dump del lettore e ricaricando il manifesto quando una traccia cambia e correggendo il problema di conversione della stringa UTF8 che ha interessato i nomi di traccia della didascalia WebVTT a doppio byte.

* Zendesk #19717 - Problema di visualizzazione delle opzioni CC
Questo problema è stato risolto gestendo correttamente la stringa Unicode.

* Zendesk #19910 - Tag TIT2 ID3 non rilevati
Questo problema è stato risolto fornendo supporto più completo per le codifiche di stringhe ID3 v2.4 e per il supporto per ID3 v2.3.

* Zendesk #20135 - TVSDK sta attivando più eventi onComplete per i contenuti VOD.
Questo problema è stato risolto aggiungendo il listener di eventi post_roll_complete al posto giusto, anziché al caso completo dell&#39;evento di modifica dello stato.

**Versione 1.4.19 (1521)**

* Zendesk #4180 - TVSDK non applica HDCP.
   * Questa è una correzione parziale per questo ticket e risolve solo il problema dei dispositivi di protezione NVidia.
Per monitorare in modo dinamico lo stato HDCP, è necessario utilizzare l&#39;API di rilevamento HDCP correttamente implementata in Nvidia Shield.

* Zendesk #18358 - Il TVSDK blocca l&#39;interruttore del bitrate con discontinuità della sincronizzazione.
   * Questo problema è stato risolto aggiungendo un nuovo avviso per rilevare la discontinuità PTS e forzando il controllo PTS a ripetere la ricerca del segmento corretto per ogni switch ABR.
Per correggere il blocco, la chiamata al metodo mediaPlayer.setCustomConfiguration deve includere come argomento forcePTSCheckForABR.

* Zendesk #19038 - Nessun flusso live su Asus Zenpad 10.

   Questo problema è stato risolto precaricando le informazioni sul codec multimediale, in modo da non eseguire query sulla funzione in fase di esecuzione.

* I seguenti problemi sono gli stessi di Zendesk #19038:
   * Zendesk #19483 - Il TVSDK si blocca sulla piattaforma Intel.
   * Zendesk #19171 - Arresti anomali su Asus Memo Pad 7 con Android 5.0.

**Versione 1.4.18 (1503)**

* Zendesk #3324 - Il reporting degli annunci Primetime non tiene traccia degli annunci pubblicitari interrotti quando non ci sono annunci multimediali in un VMAP.
Quando un&#39;interruzione pubblicitaria è vuota, gli eventi di tracciamento dell&#39;interruzione dell&#39;annuncio non venivano ping. Questo problema è stato risolto inviando ping di inizio dell&#39;interruzione dell&#39;annuncio su interruzioni pubblicitarie vuote, come VMAP AdBreak, con un nodo AdSource valido.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) viene ignorato dopo la chiamata a MediaPlayer.reset()
Questo problema è stato risolto aggiungendo setCCVisibility(Visibility.INVISIBLE); alla funzione reset() nella classe MediaPlayer.

* Zendesk #18328 - È stato risolto un problema di frame su dispositivi Amazon Fire TV di seconda generazione per i contenuti con 60FPS
Questo problema è stato risolto applicando il FPS codificato per il processo decisionale relativo al tempo di sospensione e con una logica di previsione FPS meglio codificata.

**Versione 1.4.17 (1472)**

* Zendesk #2231 - Errore restituito dal recupero del manifesto non disponibile in MediaPlayerNotification
Questo problema è stato risolto includendo il corpo della risposta del manifesto in caso di errore di analisi.

* Zendesk #17703 - VideoEngineView non impedisce le schermate durante la riproduzione video
Il metodo setSecure è disponibile dall&#39;API 17, ma poiché API 17 copre 4.2, 4.2.1 e 4.2.2, non è noto quale genererà un&#39;eccezione o se è specifico del dispositivo. Questo problema è stato risolto racchiudendo VideoEngineView.setSecure nella clausola try catch.

* Zendesk #17919 - La ricerca del contenuto causa un errore heartbeat
Si è verificato un errore di posizione dei dati di input non valido a seguito della chiamata heartbeat generata quando la ricerca è stata avviata dopo il pre-roll. Questo problema è stato risolto.

**1.4.16a** (1454a)

* Zendesk #18215 - Alcuni flussi AES non possono essere caricati.
Questo problema è stato risolto controllando la dimensione dei metadati DRM del profilo prima di caricare la chiave AES.

**Versione 1.4.16 (1454)**

* Zendesk #3875 - Tabulazione S Arresti anomali durante la riproduzione
Ripristino della dipendenza di OKHTTP su Auditude per CRS in quanto TVSDK ora utilizza direttamente httpurlconnection invece di curl. Il problema è stato risolto eliminando le eccezioni prima di effettuare qualsiasi altra chiamata JNI.

* Zendesk #4487 - Tracciamento del canale lineare dei contenuti
Il problema è stato risolto consentendo la riinizializzazione del tracciatore heartbeat video durante una sessione di riproduzione del flusso lineare.

* Zendesk #17919 - Android - la ricerca del contenuto causa un errore heartbeat
Problema relativo al momento in cui il heartbeat si trova in uno stato di errore in presenza di una ricerca in un capitolo, risolto.

* Zendesk #18053 -  arresti di Adobe Primetime su Marshmallow
TVSDK si arrestava in modo anomalo su Android M OS quando la libreria TVSDK utilizzava il codice neon che esegue la conversione colore YUV -> RGB. Il problema è stato risolto aggiornando le funzioni che causano il problema utilizzando la versione non neon del codice.

* Zendesk #18072 - Android M - Arresto anomalo dell&#39;applicazione
Quando si verifica se il profilo e il livello sono supportati, si verifica un arresto anomalo durante la chiamata delle API MediaCodecList e MediaCodecInfo. Il problema è stato risolto fornendo una soluzione temporanea caricando in anticipo tutte le informazioni del codec per evitare di chiamare queste API solo quando sono necessarie informazioni sul codec.

* Zendesk #18074 - Sottotitoli arabi non funzionanti su Nexus con Android 6.0
Il problema è stato risolto fornendo il supporto per la mappa dei font CTS per Android.

**Aggiornamento versione 1.4.15 (1438)**

* Zendesk #17437 - Ritardo prolungato nell&#39;avvio dei contenuti VOD con alcuni flussi AES.
Per risolvere questo problema, se più chiavi sono elencate in manifest, scaricate tutte le chiavi AES in parallelo.

**Versione 1.4.15 (1435)**

* Zendesk #4278 - Glitches su Android set top box quando il bitrate adattivo cambia (ABR).
La correzione consisteva nell&#39;aggiungere il supporto per switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* Zendesk #17063 - La chiamata a mediaPlayer.reset() causa un errore di reimpostazione del motore video.
La correzione consisteva nell&#39;includere il codice MediaErrorCode originale da VideoEngineExceptions durante l&#39;invio di ErrorEvents.

* Zendesk #17130 - Una breve ma notevole pausa quando si cambia il bitrate visto su FireTV.
(Come #4278 precedente) La correzione era di aggiungere il supporto per lo switch ABR senza soluzione di continuità con il codec multimediale Android più recente.

* Zendesk #17666 - Indicatori di annunci aggiuntivi, Imprevisti o Nessun annuncio al momento della ripresa del contenuto.
La correzione si è verificato un problema durante l&#39;esecuzione del contenuto PreparaToPlay su video-on-demand (VOD). La ricerca iniziale viene eseguita sull&#39;ora locale invece che sull&#39;ora virtuale.

* Zendesk #17437 - Ritardo prolungato nell&#39;avvio dei contenuti VOD con alcuni flussi AES.
La correzione consisteva nel scaricare tutte le chiavi AES in parallelo quando nel manifesto sono elencate più chiavi.

* Zendesk #17851 - TV Android - Fotogramma nero durante l&#39;ABR
La correzione consisteva nel specificare KEY_MAX_WIDTH e KEY_MAX_HEIGHT per abilitare la riproduzione adattiva.

**Versione 1.4.14 (1415)**

* Zendesk #3875 - Tabulazione S Arresti anomali durante la riproduzione.
Per evitare l&#39;arresto anomalo era necessaria una correzione aggiuntiva.

* Zendesk #17245 - Il fallback su Android TV non funziona.
È stato risolto un problema aggiuntivo per il quale la riproduzione si blocca quando il fallback è abilitato e la risposta VMAP ha un&#39;interruzione annuncio vuota.

**Versione 1.4.14 (1412)**

* Zendesk #17245 - Il fallback su Android TV non funziona.
È stata rimossa una restrizione per disattivare la ricompilazione creativa per gli annunci di fallback.

**Versione 1.4.13 (1388)**

* Zendesk #3502 - Supporto del failover basato su client HLS durante un&#39;interruzione dell&#39;annuncio
Consenti failover al manifesto principale quando si aggiorna l&#39;errore del profilo attivo durante il periodo di interruzione dell&#39;annuncio.

* Zendesk #3875 - Tabulazione S Arresti anomali durante la riproduzione
Per risolvere il conflitto tra HttpUrlConnection e cURLm, utilizzate una libreria di terze parti.

* Zendesk #4450 - impostazione dei metadati personalizzati per una singola posizione in un risolutore di contenuti
Aggiungete un setter alle impostazioni Opportunità.

**Versione 1.4.12 (1388)**

* Zendesk #2751 - CSAI e CRS | Miglioramento: Gestire gli elementi dinamici in alcuni URL di file multimediali.
Creative Repackaging Service è stato aggiornato per gestire correttamente gli annunci con URL creativi dinamici.

* Zendesk #3965 - Il passaggio alla riproduzione normale dal trickplay determina un salto in avanti un po&#39; prima di avviare la riproduzione.
   * La correzione include la restituzione di TVSDK prima della modifica della velocità fino all&#39;aggiornamento di tutte le variabili, invece di cercare di calcolare il GetStreamTime.
   * È stato corretto un arresto anomalo durante la modifica della velocità di riproduzione del trucco vicino alla fine del flusso.
   * Corretto il calcolo del tempo corrente durante il gioco a tre.

* Zendesk #3978 - Trickplay a 8x e 16x spesso si blocca.
   * Scegli sempre il profilo di riproduzione trucco con il bit rate più basso per evitare buffering costanti.
   * Aumenta l&#39;intervallo di salti per un&#39;elevata frequenza di gioco.
   * È stato corretto un problema a causa del quale il buffer continua a crescere dopo aver raggiunto la lunghezza di destinazione durante la riproduzione del trucco.

* Zendesk #3992 - Velocità aggiuntive di Trickplay.
TrickPlay è stato aggiornato per accettare tassi superiori a 16x; Sono ora consentiti anche +/- 32, +/-64 e +/-128.

* Zendesk #4007 - Interpretazione dell’oggetto GEOB come parte dei metadati della cronologia (Android e Web).
Sono state aggiunte le API setByteArray e getByteArray.

* PTPLAY-7301: avvio immediato all&#39;avvio casuale.
Instant On è stato aggiornato per consentire un punto iniziale diverso da zero.

**Versione 1.4.11 (1363)**

* Zendesk #2076 - Schiacciamento frequente durante la riproduzione di video su Motorola Xoom con Android 4.0.3
Sono stati aggiunti dispositivi al elenco consentiti  per impedire loro di provare a riprodurre contenuti di alto profilo.

* Zendesk #2197 - `[Ads]` Errori annuncio di tracciamento
invio OperationFailedEvent con notifica di avviso.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro non popolata
   * il codice di errore 400 sarà esposto se l&#39;annuncio in linea ha un cattivo creativo.
   * `[ERRORCODE]` macro verrà codificata nell&#39;URL

**Versione 1.4.10 (1354)**

* Zendesk #2941 - Le risorse live non hanno &quot;0&quot; nell&#39;intervallo ricercabile
Precedentemente c&#39;era un buffer di 3 segmenti quando si cercava l&#39;inizio di un flusso live, ora è possibile cercare all&#39;inizio di un flusso live (cioè l&#39;inizio del primo segmento).

* Zendesk #3169 - Aggiornamento del lettore di riferimento con  integrazione Adobe AnalyticsIl lettore di riferimento è stato aggiornato con la  libreria Adobe Analytics come impianto di esempio.
* Zendesk #3299 - Comportamento di gioco ingannevole inspiegabile
   * È stato corretto un bug a causa del quale il ripristino dello stato di riproduzione dopo l’arresto della riproduzione potrebbe richiedere alcuni secondi (a volte più di 25 secondi).
   * È stato corretto un bug a causa del quale il trucco di richiamo veniva riprodotto una seconda volta sullo stesso supporto, che causava il blocco del flusso al momento corrente.
* Zendesk #3433 - Android e Flash - Problemi con i sottotitoli

GetLine per WebVTT non rispettava una lunghezza &lt;CR>&lt;LF> regolata per un pacchetto; l&#39;ultima didascalia può contenere caratteri provenienti da didascalie precedenti.

* PTPLAY-6243 - Migliora il lettore di riferimento per acquisire le informazioni di debug

I lettori di riferimento di esempio Android sono stati migliorati con un&#39;opzione per attivare i registri di debug e inviare per e-mail i risultati. Questa opzione si trova nel menu Registro del lettore di riferimento.

**Versione 1.4.9 (1332)**

* Zendesk #2649 - Il buffer completo si verifica prima che il buffer iniziale sia pieno

Dopo una ricerca, è possibile che il motore video imposti lo stato su PLAYING prima che il relatore video sia pronto per la riproduzione. Si verifica quando lo stato del buffer è elevato prima della ricerca. Correzione mediante notifica dello stato basso del buffer al motore video. Con il motore video a basso stato del buffer, la chiamata di Play causa la modifica dello stato in BUFFERING invece di PLAYING. La riproduzione riprende quando lo stato cambia in PLAYING.

* Zendesk #2846 - Richiesta di miglioramento: Consente di impostare una stringa agente utente diversa per le chiamate effettuate dalla libreria Auditude

È stata aggiunta una nuova API per impostare l’agente utente per le chiamate correlate agli annunci, auditudeSettings.setUserAgent(&quot;user/agent&quot;). Se non è impostato alcun agente utente, verrà utilizzato il valore predefinito. Questo incide solo sull’agente utente per le chiamate correlate agli annunci, l’agente utente per le chiamate ai supporti non subisce modifiche, che è &quot; Adobe Primetime&quot;+&lt;agente utente predefinito>.

**Versione 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Errore con locale ... Se il caricamento del manifesto in FragmentalHTTPStreamer::ThreadParseManifest() non riesce, verificare se il dominio URL è localhost e, in tal caso, modificare il dominio in 127.0.0.1 e richiamare ThreadParseManifest.
* Zendesk #3072 - Passaggio automatico a bitrate inferiori. Il calcolo della lunghezza del buffer è stato modificato per saltare il payload PTS zero.
* Zendesk #3168 - Sottotitoli WebVTT visualizzati solo per i primi 10 secondi.
* Zendesk #3193 - È stata aggiunta la richiesta di una modifica dell&#39;API di profilo in TVSDK, PlaybackEventListener.onProfileChanged().

**Versione 1.4.7 (1311)**

* Zendesk #2197 - Tracciamento degli errori di annuncio. Aggiunta notifica per il caricamento del manifesto della risorsa non riuscita
* Zendesk #2575 - PSDK ignora l&#39;annuncio in streaming personalizzato di MARK prima del video
* Zendesk #2719 - Win Death with auditude ads, tracciamento del beacon fisso quando viene reindirizzato all&#39;URL relativo nel plug-in auditude
* Zendesk #2760 - Tag DISCONTINUITÀ ignorato durante la modalità TrickPlay
* Zendesk #2805 - Arresto anomalo del lettore all&#39;inizio della riproduzione, stessa correzione di Zendesk #2719
* Zendesk #2817 - Lettore Android - Il lettore a volte si blocca e si interrompe la riproduzione, risolto estendendo i buffer di decodifica da 2.0 a 3.0 secondi
* Zendesk #2839 -  Adobe Primetime PSDK supporta i chipset ARMv8?, è stata aggiunta una correzione per l&#39;arresto anomalo trovato su Galaxy S6.
* Zendesk #2885 - Riproduzione di Auditude Crash, stesso problema di Zendesk #2719
* Zendesk #2895 - Errore HLS live in modo coerente dopo 10 minuti di riproduzione
* Zendesk #2925 - Feedback sulla build Android dev (1.4.5), su alcuni dispositivi quando mettiamo in coda il pacchetto alla coda di ingresso, se il PTS è negativo, il decoder va in uno stato strano che otteniamo sempre un PTS di output negativo per i pacchetti futuri. La correzione imposta l&#39;input PTS su zero se è negativo per evitare questo problema.
* PTPLAY-4645 - Disattivare il supporto per i caratteri RC4 in open. Esistono degli usi noti per RC4. Ciò significa che se viene eseguito un tentativo di connessione con un server che supporta solo RC4, non riuscirà.

**Versione 1.4.6 (1282)**

* Zendesk #2192 - Il bitrate non diminuisce sempre in condizioni di rete scadenti, risolto rimuovendo l&#39;implementazione rapida degli switch.
* Zendesk #2631 - Sottotitoli in arabo su Android: Il testo su più righe appare troncato, corretto regolando la dimensione del font per i font arabi.
* Zendesk #2844 - Il buffer sulla nota 4 e il tempo di download del frammento non sono precisi.

Questo problema è stato risolto aggiungendo la latenza tra i download dei segmenti video nel calcolo della larghezza di banda e avendo la logica di calcolo del tempo di download utilizzato il tempo di ciclo di richiesta completo.

* Zendesk #2908 - Sottotitoli arabi non funzionanti in Nexust 5, 6 e 7, corretti aggiungendo altri 2 font di fallback per gli script arabi.
* PTPLAY-4627 - Aggiornate Nielson appsdk alla versione 1.2.3.7
* PTPLAY-5084 - Supporto del failover di aggiornamento del manifesto dal vivo

**Versione 1.4.5 (1248)**

* Zendesk #1757 - È stato corretto l&#39;arresto anomalo di Nexus 4 e Nexus 7 solo per l&#39;audio riprodotto o per il lettore
* Zendesk #2072 - TimedMetadata for AdEvent non contiene l’URL completo solo &quot;http&quot;
* Zendesk #2192 - Il bitrate non sempre si riduce in condizioni di rete scadenti
* Zendesk #2256 - Accesso alla playlist principale, PSDK aggiornato per l&#39;invio di eventi TimedMetadata per i tag sottoscritti nella playlist principale.
* Zendesk #2269 - Due lingue di sottotitoli diversi vengono visualizzate sullo schermo contemporaneamente con WebVTT
* Zendesk #2417 - Lettore che tenta di scaricare i sottotitoli prima dell&#39;avvio della riproduzione, WebVTT utilizzava la variabile del numero di segmento errata per la corrispondenza del numero di segmento. Il bug veniva visualizzato solo per i supporti con indici di segmento a partire da zero.
* Zendesk #2470 - PSDK che non ritorna dallo stato SOSPESO quando si verifica un cambiamento del bitrate dopo la sospensione. In una situazione speciale in cui la ricerca intelligente viene chiamata da RestoreGPUResource (ripristino del lettore dallo stato di sospensione) e l&#39;interruttore di flusso rilevato in precedenza, la ricerca intelligente non è in grado di completare e ottenere buffering costante.
* Zendesk #2451 - Sottotitoli codificati &#39;bottomInset&#39;, aggiunto il parametro &#39;bottomInset&#39; al codice della didascalia
* Zendesk #2480 - Disattivazione dell&#39;ottimizzazione del reindirizzamento HTTP 302. È stato aggiunto il supporto per l&#39;impostazione della proprietà useRedirectUrl
* Zendesk #2486 - beacon di terze parti
* Zendesk #2547 - Sottotitoli in arabo: Il testo deve essere allineato a destra

**Versione 1.4.4 (1195)**

* Zendesk #1158 - La riproduzione non riesce su Huawei Valiant (Y301A1)
* Zendesk #1709 - Dimensioni dei supporti errate e video allungato
* Zendesk #1757 - Solo l&#39;audio riprodotto dopo l&#39;interruttore di profilo tra flussi con dati spa/pps identici
* Zendesk #2095 - Stato HTTP 307 (reindirizzamento) causa l&#39;arresto della riproduzione  lettore Adobe
* Zendesk #2126 - Evento TimedMetaData mancante per l&#39;ultimo evento ADEVENT, i tag Sottoscritti esistenti dopo l&#39;ultimo segmento non sono stati segnalati a PSDK da AVE
* Zendesk #2227 - Blocchi in VideoEngine nativiReset e nativiPausa
* Bug #3921755 - Aggiornamento della libreria OpenSSL alla versione 1.0.1L

**Versione 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 - Accensione e disattivazione dei sottotitoli codificati
* PTPLAY-1818 - Il gioco dei trucchi di riavvolgimento si ferma all&#39;annuncio invece di riavvolgerlo
* PTPLAY-2736 - Una didascalia WebVTT visualizzata in precedenza viene visualizzata sullo schermo al termine della riproduzione di un flusso con la didascalia WebVTT
* PTPLAY-3773: un annuncio mid-roll non viene riprodotto quando la riproduzione in streaming viene avviata dopo la posizione dell&#39;annuncio

**Versione 1.4.2**

* Zendesk #1561 - Supporto del failover basato su client HLS in primetime. Utilizzerà l&#39;ora della data del programma per risolvere il failover
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0 (non fisso per solo audio)
* Zendesk #1626 - Potenziale perdita di memoria nel lettore. Non si è verificata una perdita di memoria effettiva. Il problema è stato il salvataggio delle ultime 1000 notifiche da parte di NotificationHistory, che è stato ridotto a 100.
* Zendesk #2192 - Il bitrate non sempre si riduce in condizioni di rete scadenti

**Versione 1.4.1 (1121)**

* Zendesk #1951 - Blocco in VideoEngine.nativeReset() su dispositivi 4.0.x
* Zendesk #2064 - Native Crash SIGSEGV su dispositivi Android basati su informazioni specifiche
* Zendesk #2075 - Blocco in VideoEngine.nativeReleaseGPUResource su dispositivi 4.0.x
Nota: Questa build è ***obbligatorio*** per il supporto di Android 5.0 (Lollipop)
* Zendesk #1513 - Supporto Lollipop per Android
* Zendesk #1709 - Dimensioni dei supporti errate e video allungato
* Zendesk #1871 - I sottotitoli WebVTT a volte scompaiono e quindi riappaiono quando si visualizza un livestream con i sottotitoli WebVTT
* Zendesk #1996 - Nessun indicatore della timeline visibile in PSDK 1.4.0
* Zendesk #2046 - Arresto anomalo con PSDK 1.4.1.1113, arresto anomalo fisso per i flussi live quando non viene restituito nessun annuncio dall&#39;audience
* Bug #3769657 - Aggiornare la versione del curl a 7.38.0
* PTPLAY-1575 - Quando la riproduzione ABR inizia con lo streaming solo audio e poi passa allo streaming audio/video, il video non viene mai riprodotto mentre l&#39;audio continua
* PTPLAY-2499 - Aggiornamento di OpenSSL alla versione 1.0.1j per risolvere le vulnerabilità recenti
* PTPLAY-2632 - Il video non si riprende dopo il mid roll Ad completato su Android Lollipop
* PTPLAY-2678 - Fermo video durante i test di longevità live su Android Lollipop

**Versione 1.4.0**

* Zendesk #1024 - Funzione per rimuovere gli annunci dal flusso tramite manifesto
* Zendesk #1293 - Problema di selezione delle tracce dei sottotitoli codificati.
* Zendesk #1590 - LoadInfo.MediaDuration è sempre 0, mediaDuration ora mostra il valore corretto.
* Zendesk #1629 - Arresti di lettori/app al termine della riproduzione di annunci su Galaxy S4
* Zendesk #1674 - ClosedCaption Non visualizzato, corretta visualizzazione della didascalia 708 quando mancano i codici ETX 0x03.
* PTPLAY-2157: gli stili di sottotitoli codificati predefiniti venivano restituiti dai getter anche se dopo l&#39;impostazione e la verifica visiva di stili diversi nello streaming. Le proprietà dello stile dei sottotitoli codificati ora mostrano il valore impostato.

## Problemi noti in 1.4 {#known-issues-in}

**Versione 1.4.31**

* PTPLAY-16803: i sottotitoli codificati non funzionano solo con contenuto audio, in quanto il sistema di sottotitoli necessita di video per funzionare. Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione, non è possibile visualizzare alcun elemento grafico per le didascalie.
* PTPLAY-1634 - Lo stesso tag con iscrizione ha marche temporali diverse in diverse finestre dal vivo. Quando la finestra dal vivo si sposta, lo stesso tag deve avere le stesse marche temporali. Tuttavia, a volte anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-3197 - Arresto anomalo con segnale 11 errore SIGSEGV sul dispositivo Acer Iconia dopo ~ 1 ora di riproduzione continua
* PTPLAY-3310 - Con un audio con bitrate inferiore, l&#39;audio diventa discontinuo/stuttery su Acer Iconia
* PTPLAY-3355 - WIN DEATH crash su Motorola Xoom con 4.0.x dopo ~ 1 ora di riproduzione continua.
* PTPLAY-3557 - Il riavvolgimento in corrispondenza di un&#39;interruzione di annuncio causa il completamento del flusso
* PTPLAY-7079 - La finestra di riproduzione sul client Android non funziona con l&#39;arresto sicuro/arresto rigido
* Bug #3760144 - La risoluzione può variare o apparire all&#39;impulso quando il flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabili solo a stretto controllo
* Bug #3761170 - searchToLocal in Live with Ads non è in grado di recuperare contenuti di annunci, è la soluzione migliore per utilizzare le API currentTime per i flussi live
* Bug #3763370 - I flussi live con annunci pubblicitari mostreranno occasionalmente due indicatori di annunci vicini quando ce ne dovrebbe essere solo uno. Questi indicatori di annunci rappresentano lo stesso annuncio pubblicitario, e solo uno verrà riprodotto
* Bug #3763373 - Il marcatore annuncio potrebbe scomparire brevemente quando si cerca oltre un annuncio nei flussi VOD. L&#39;indicatore pubblicitario viene ripristinato e non vi sono altri effetti negativi sulla timeline
* Alcuni dispositivi presentano problemi noti di riproduzione. Vedere [Problemi noti dei dispositivi in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento - La riproduzione dei mattoni non è implementata nell&#39;applicazione di esempio
* Su alcuni dispositivi Android TV è possibile visualizzare un fotogramma nero a causa di un ripristino del decoder ai seguenti punti di transizione:
   * in e fuori dalla modalità trickplay
   * commutazione tra le tracce audio di rilegatura
   * da un annuncio al contenuto principale.

**Versione 1.4.23**

* I sottotitoli codificati non funzionano con il contenuto solo audio, perché il sistema dei sottotitoli richiede il funzionamento del video. Senza video, non esiste una dimensione di visualizzazione e senza una dimensione di visualizzazione non è possibile visualizzare alcuna grafica per le didascalie.
* A partire dalla versione 1.4.23, TVSDK non supporterà Gingerpan OS 2.3. Questo perché TVSDK ha utilizzato le seguenti librerie Android private per raccogliere informazioni hardware sui dispositivi con il sistema operativo Gingerpan:

   * `libstagefright.so`
   * `libcutils.so`

Nella versione Android N, Google ha rimosso l&#39;accesso a queste librerie private. Il sistema operativo Gingerpan rappresenta attualmente meno dell&#39;1% della quota di mercato del sistema operativo Android a livello globale, quindi dopo la versione 1.4.23, il sistema operativo Gingerpan non sarà più supportato dal TVSDK.
Quando utilizzate la versione 1.4.23 (che include il supporto per Android N) o versioni successive:
* Aggiornate le app per utilizzare minSdkVersion versione 11.
* Se l&#39;utente finale esegue OS 2.3, la versione dell&#39;SDK è inferiore alla versione minSdkVersion dell&#39;applicazione. Il sistema interrompe l&#39;installazione o l&#39;aggiornamento dell&#39;applicazione.
* Se l&#39;utente finale esegue una versione superiore a OS 2.3, l&#39;applicazione verrà installata correttamente.

Se aggiornate minSdkVersion:

* Se l&#39;utente finale esegue OS 2.3, l&#39;applicazione è installata ma la riproduzione non funziona.
Questo vale sia per l&#39;aggiornamento che per la nuova installazione.
* Se l&#39;utente finale esegue un sistema superiore a OS 2.3, l&#39;app viene installata correttamente e il contenuto viene riprodotto correttamente.

**Versione 1.4.22**

* L&#39;uscita anticipata dagli annunci non funziona con alcuni degli annunci mid-roll quando i tag splice-out e splice-in sono troppo vicini tra loro.

**Versione 1.4.2**

* Il riavvolgimento in corrispondenza di un&#39;interruzione annuncio causa il completamento del flusso.

Media Player invia erroneamente MediaPlayer PlayerState.Complete durante l’operazione di riavvolgimento di Trick Play quando raggiunge un limite annuncio. In caso contrario, l’SDK lo gestisce correttamente.

**Versione 1.4.0 (1086)**

* PTPLAY-1634 - Lo stesso tag Subscribed ha marche temporali diverse in diverse finestre dal vivo. Quando le finestre attive si spostano, lo stesso tag in ognuna di esse deve avere le stesse marche temporali. Tuttavia, a volte anche gli stessi tag hanno marche temporali diverse.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE è talvolta visibile dopo diversi switch da/verso il flusso alternativo nei blackout
* Bug #3726865 - Se un flusso LBA MultiBitrate inizia da un flusso solo audio, il video non verrà visualizzato se si passa a un flusso audio/video. A partire da un flusso audio/video questo problema non viene visualizzato e può passare correttamente da un flusso audio a un flusso video
* Bug #3760144 - La risoluzione può variare o apparire all&#39;impulso quando un flusso viene messo in pausa su alcuni dispositivi come Kindle Fire 7 e Samsung Galaxy Nexus. Osservabili solo a stretto controllo
* Bug #3761170 - searchToLocal in Live with Ads not retrieve into ad ad content; è consigliabile utilizzare le API currentTime per i flussi live
* Bug #3763370 - I flussi live con annunci pubblicitari mostreranno occasionalmente due indicatori di annunci vicini quando ce ne dovrebbe essere solo uno. Questi indicatori di annunci rappresentano lo stesso annuncio pubblicitario, e solo uno verrà riprodotto
* Bug #3763373 - Il marcatore annuncio potrebbe scomparire brevemente quando si cerca oltre un annuncio nei flussi VOD. L&#39;indicatore pubblicitario viene ripristinato e non vi sono altri effetti negativi sulla timeline
* Alcuni dispositivi presentano problemi noti di riproduzione. Per ulteriori informazioni, vedere [Problemi noti dei dispositivi in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Implementazione di riferimento - La riproduzione dei mattoni non è implementata nell&#39;applicazione di esempio.

## Problemi noti dei dispositivi in 1.4 {#known-device-issues-in}

| Dispositivo | Chipset | Problema | Causa | Soluzione |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | È previsto un ritardo ABR in quanto sta riavviando il decodificatore. |  |  |
| HTC Desire (diverso da HTC Desire HD) | QSD8250 | Impossibile riprodurre il video. Restituisce un errore VIDEO_PROFILE_NOT_SUPPORTED. | Desire non fornisce un decodificatore HW corretto. Fornisce il decodificatore SW di Stagefright. | Riavviare il dispositivo. |
| HTC EVO 4G | QSD8650 | Nessun decodificatore HW. | Qualcomm non dispone di un decodificatore HW. | Aggiornamento ad Android 4.x. |
| Kindle FireSystem versione 6.0 | TI OMAP4 | Non riproduce flussi HLS. Il video su AIR non funziona. |  | Aggiornamento alla versione di sistema 6.3. |
| Kindle Fire HD | TI OMAP4 | Può trovarsi in uno stato in cui non è possibile riprodurre il video. Restituisce gli errori VIDEO_PROFILE_NOT_SUPPORTED e UNRECOVERABLE_ERROR. | Il decodificatore HW si trova in uno stato irrecuperabile quando l&#39;app non arresta completamente il decodificatore HW, ad esempio dopo un arresto anomalo. Si verifica anche sulle app native sul dispositivo. | Riavviate il dispositivo. |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE si arresta in modo anomalo dopo più interruttori ABR. |  |  |
| Motorola Atrix | Tegra2 | Problemi generali di prestazioni con AVE anziché con AIR. La riproduzione audio/video non sincronizzata si blocca dopo 9-15 minuti. Arresti anomali. | È possibile che si tratti di openGLES abilitato su AIR. In corso di indagine. |  |
| Nexus 7 (2a generazione) | S4Pro APQ8064 (Qualcomm) | Il dispositivo si blocca quando un filmato viene messo in pausa per più di 30 minuti. | Problema del dispositivo segnalato a Google. | L&#39;app deve avere un timeout per non consentire uno stato di pausa lungo. |
| Nexus S (GB) | Uccello Umanitario | Non è possibile riprodurre alcun video con il decodificatore HW. | Non esiste un decodificatore HW basato su Stagefright in Nexus S, quindi per Android 2.3 stiamo utilizzando un decodificatore SW. | Aggiornamento a ICS. |
| Nexus S (ICS) | Uccello Umanitario | Video a volte sfarfallio. | Dati errati possono causare il deterioramento dello stato del decodificatore. | Riavviate il dispositivo. |
| Tablet PC Android: 2.3 | TI OMAP 4 | Il video non viene riprodotto e l&#39;app si blocca. | Stagefright entra in uno stato instabile dopo aver eseguito l&#39;app per alcune volte. Chiamate a mediaplayer::QueryCodecs hang. | Riavviate il dispositivo per ripristinare lo stato. |
| Samsung Galaxy ACE | Qualcomm MSM7227 | Impossibile installare l’app SampleMediaPlayer. | Utilizza ARM v6 invece del chipset ARM v7 più comune. FP/AIR non supporta questo dispositivo. |  |
| Samsung Galaxy ACE2Android OS: 2.3.6 | NovaThor U8500 | Impossibile riprodurre il video. | Questo chipset è un decodificatore sconosciuto per Android pre-ICS in AVE. |  |
| Samsung Galaxy S2 (GT-I9100) | Exynos | Le prestazioni video non sono all&#39;altezza del dispositivo. | Il decodificatore HW restituisce fotogrammi decodificati con PTS errato. Il decodificatore utilizza il tempo di decodifica invece del tempo di presentazione. |  |
| Samsung Galaxy S2 GAndroid OS: 2.3.6 | TI OMAP4 | Arresti anomali all&#39;avvio del video. |  | Aggiornamento ad Android 2.3.7 o 4.x. |
| Samsung Galaxy S3 (I747) | Qualcomm MSM8960 | In modo intermittente, il video si blocca e solo l&#39;audio viene riprodotto, quindi non risponde. |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | Il video si blocca. | Indagare. |  |
| Samsung Galaxy Tab 1 v10.1 | Tegra 2 | La transizione MBR potrebbe richiedere fino a tre secondi. | Come correzione per gli arresti anomali MBR, riavviamo il decodificatore per ogni switch di flusso, che può richiedere fino a tre secondi. |  |
| Samsung Galaxy Y |  | Impossibile installare l’app SampleMediaPlayer. | Utilizza ARM v6 invece del chipset ARM v7 più comune. FP/AIR non supporta questo dispositivo. |  |
| Xoom | Tegra | Alcuni fotogrammi vengono ignorati per il passaggio. Il decodificatore non viene riavviato. | Limitazione OMXAL. |  |

## Risorse utili {#helpful-resources}

* Consulta la documentazione completa della guida in linea alla pagina [ Informazioni e supporto per Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
